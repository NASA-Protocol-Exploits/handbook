

## How BP/LTP works in ION-DTN
### Introduction
After completing the [NASA ION-DTN Course](ion-dtn-course.md), you should have some understanding of the Interplanetary Overlay Networks (ION) with Delay/Disruption Tolerant Networking (DTN) architecture and why it is crucial for space communication.

This document intends to explain how the C implementation of the Bundle Protocol (BP) and Licklider Transmission Protocol (LTP) function within the ION-DTN virtual machine environment. These two protocols have been highlighted below in _figure 1_ via the red box to assist users in understanding where they reside in the stack.

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/how-bp-and-ltp-work-doc/dtn-stack-with-bp-ltp-highlighted.PNG?raw=true"/>
</p>


### Understanding Software Elements and their responsibilities
At this point it is also good to understand the functional dependencies among the various ION software elements and their respective responsibilities which are as follows:

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/how-bp-and-ltp-work-doc/software-element-dependencies.PNG?raw=true"/>
</p>

|   **Component**  |                                  **Role / Responsibilities**                                                    |
|:----------------:|:---------------------------------------------------------------------------------------------------------------:|
| BP/LTP Protocols | Bundle Protocol and Licklider Transmission Protocol libraries and daemons.                                      |
| ZCO              | Zero-copy objects capability: Minimize data copying up and down the stack.                                      |
| SDR              | Spacecraft Data Recorder: Persistent object database in shared memory, using PSM and SmList.                    |
| SmList           | Linked Lists in shared memory using PSM.                                                                        |
| SmRbt            | [Red-Black Trees](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/) in shared memory using PSM                                                                      |
| PSM              | Personal Space Management: Memory management within a pre-allocated memory partition.                           |
| Platform         | Common access to operating system; Shared memory, system time and [IPC mechanisms](https://www.geeksforgeeks.org/inter-process-communication-ipc/#:~:text=Inter%2Dprocess%20communication%20(IPC),Shared%20Memory). |
| Operating System | [POSIX](https://en.wikipedia.org/wiki/POSIX) thread spawn/destroy, file systems and time.                                                              |

From 

### How BP/LTP Functions in ION
Regardless of the complexitities associated with the ION environment. The entire system of the BP utilizing the LTP convergence layer can be depict in one single diagram as seen below in _Figure 2_. 
<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/how-bp-and-ltp-work-doc/how-bp-and-ltp-work-overall.PNG?raw=true"/>
</p>

### 1.1.0	Databases
In this section we discuss architecture of both Bundle Protocol (BP) and Licklider Transmission Protocol (LTP) Database. 
#### BP Database
![BP Database Diagram](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/bundle-protocol-database.PNG)
Before understanding the above diagram we need to clarify meaning of some terms and signs

 1. Dashed Line  (----) : 	Many to One 
 2. Solid Arrows (->):		One to Many
 3. Dark Grey Circle:		Non - volatile data retained heap storage
 4. Light Grey  Circle:	Volatile data retained in dynamic  RAM
 5. CL Protocol:				Convergence Layer Protocol

With these in mind let's look into the BP Database diagram. The BP database initially works with the dynamic RAM on both sides showing the volatile induct and outduct state left side and then on the right side the scheme and endpoint ID. In both cases we can see that according to its  feature BP starts the process with volatile or dynamic RAM except to the convergence layer protocol (CLP) which handles the data transmission but all in one to many relationships. This CLP handles the  inducts and outducts of the database. In the CL protocol the re-forwarding policy is mentioned for induct and outduct adapter tasks. BP   checks with CL protocol for transmission policies. This is important because when BP detects CL protocol failure. Based on the detection BP might try re-transmission again based on two factors first one being if receiving entity aborts the bundle and the second one being if the possible nodes ( called neighbors ) are blocked. If the later happens then the packets or bundles are put in the list for future transmission in the datagram which can be seen on the right most part circles which brings us to the endpoint and scheme circles. According to the naming scheme   defined the endpoint ID and the scheme is made. Then the circles on the most left represent the bundles that were prepared or failed to re-transmit. The one on the bottom are bundles to be retransmitted and the one on top represent the induct bundles that failed to re-transmit due to neighbor being blocked. Now the last bottom part shows the bundle that represent all bundles awaiting TTL. In this whole re-transmission process if after multiple attempts (unclear how many) if the bundle still fails to go ahead and the TTL nears expiration (bottom part of the diagram) the bpclock task will send a system status report to that bundle's endpoint noting TTL expiration and destruction report and then destroys the bundle. And these are handled on the application specific layer. 

#### LTP Database
![LTP Database](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/licklider-transmission-protocol-database.PNG)

Terms to consider:

 1. Span - Current state or relationship or link between local and remote LTP Engine
 
This database is pretty self-explanatory with the headers below the circles explaining each data object. In BP there are 4 tasks Induct, Outduct, Scheme and Endpoint but in LTP there are Xmit session, Recv Session, Span and Clients. Xmit session represents the the receivers session, Recv session represents senders session. The Xmit session (own session) is connected with the checkpoint segment and Recv session is connected with the report segment. Xmit  session is connected with Recv session through span (remote engine ID). The volatile span and client state is handled from the dynamic RAM to save resources unline DTN. The retransmission is directly connected in one to many reference with the LTP database. Here Recv session handles session assembly buffer and Xmit session handles session re-xmit buffer 

### 1.2.0 Control and Data Flow
#### 1.2.1 Bundle Protocol
![BP Data Flow](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/bundle-protocol-dataflow.PNG)

 1. RFX: Contact Plan Database
 2. IPN: Exits defined database for local nodes
 3. bpclm: Bundle Protocol Convergence Convergence Layer Management
 4. ipnfw: IPN forwarder
 5. Semaphore: Variable or abstract data type used for process isolation

After learning about the terms this graph is self-explanatory as well. The rfxadmin database has the contact plans with nodes, routs and hops for the bundles to connect with nodes and the ipnadmin database holds the plans, rules and groups for the local nodes. Below are the steps described for the process:
1. Waits for forwarding needed semaphore. 
2. Gets bundle from queue. 
3. Consults routing table and forwarding table to determine all plausible proximate destinations  
4. Appends bundle to transmission queue (based on priority) for best plausible proximate destination. 
5. Gives duct selection needed semaphore for that transmission queue.
6. Convergence-layer manager daemon waits for duct selection needed semaphore. 
7. Gets bundle from queue. Imposes flow control, fragments as needed. Consults mission-provided code (if provided), selects outduct to use for transmission of bundle to this proximate destination. 
8. Inserts bundle into transmission buffer for selected outduct. 
9. Gives transmission needed semaphore for this buffer. 

![BP Convergence Layer Output](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/bp-forwarder-dataflow.PNG)
Above picture represents  BP Convergence Layer Output

 1. LTPCLO: LTP convergence layer output task for Bundle Protocol

Below are the steps how BP Convergence Layer Output is handled:
1. Waits for buffer open semaphore (indicating that the link’s session buffer has room for the bundle). 
2. Waits for transmission needed semaphore. 
3. Gets bundle from queue, subject to priority. 
4. Appends bundle to link’s session buffer – aggregation. Buffer size is notionally limited by aggregation size limit, a persistent attribute of the Span object: implicitly, the rate at which we want reports to be transmitted by the destination engine. 
5. Gives buffer closed semaphore when buffer occupancy reaches the aggregation size limit

#### 1.2.2 Licklider Transmission Protocol
![LTP transmission metering](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/ltp-meter-dataflow.PNG)

The above figure shows the LTP transmission metering process

 1. LTPMETER - LTP daemon task for aggregating and segmenting transmission blocks
ltpmeter works 
 2. MTU - Maximum Transfer Unit
 
 Below are the steps:
 3. Initializes session buffer, gives buffer open semaphore.  The session buffer waits until open semaphore or process is given
 4. Waits for buffer closed semaphore (indicating that the session buffer is ready for transmission). 
 5. Segments the entire buffer into segments of managed MTU size – fragmentation. 
 6. Appends all segments to segments queue for immediate transmission. 
 7. Gives segment enqueued semaphore.

![LTP Link Service Output](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/ltp-link-service-output-dataflow.PNG)
Above diagram shows LTP Link Service Output.
1. Link Service  Protocol: ltpclo aggregates output tasks buffered bundles into blocks to be completed while ltpmeter waits for them to be completed. This is where Link service protocol comes in. Then ltpclo segments each block bundle and then passes onto the underlying link service protocol.  
After the transmission metering below are the steps how service outputs happen:
2. Waits for segment enqueued semaphore (indicating that there is now something to transmit). 
3. Gets segment from queue. 
4. Sets retransmission timer if necessary. 
5. Transmits the segment using link service protocol

Next is the process of input: 
![LTP Link Service Input](https://raw.githubusercontent.com/NASA-Protocol-Exploits/handbook/main/docs/image-resources/how-bp-and-ltp-work-doc/ltp-link-service-input-dataflow.PNG)
 
 xxx(lsi) - This term is better understood if divided into two parts xxx  and lsi. Lsi here refers to link service input.  and the 'xxx' part refers the type of network activity that the message is reporting on which could be 8 types: 
 1. **src** This message reports on the bundles sourced at the local node during the indicated interval. 
 2. **fwd** This message reports on the bundles forwarded by the local node. When a bundle is re-forwarded due to custody transfer timeout it is counted a second time here.
 3.  **xmt** This message reports on the bundles passed to the convergence layer protocol(s) for transmission from this node. Again, a re-forwarded bundle that is then re-transmitted at the convergence layer is counted a second time here. 
 4. **rcv** This message reports on the bundles from other nodes that were received at the local node. 
 5. **dlv** This message reports on the bundles delivered to applications via endpoints on the local node. 
 6. **ctr** This message reports on the custody refusal signals received at the local node. 
 7. **rfw** This message reports on bundles for which convergence-layer transmission failed at this node, causing the bundles to be re-forwarded. 
 8. **exp** This message reports on the bundles destroyed at this node due to TTL expiration

Below are the steps for LTP link service input:
1. Receives a segment using link service protocol. 
2. If data, generates report segment and appends it to queue – reliability. Also inserts data into reception session buffer “red part” and, if that buffer is complete, gives notice semaphore to trigger bundle extraction and dispatching by ltpcli. 
3. If a report, appends acknowledgement to segments queue. 
4. If a report of missing data, recreates lost segments and appends them to queue. 
5. Gives segment enqueued semaphore   
