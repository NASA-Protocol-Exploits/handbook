## How to Create a New Scenario
### Introduction
In this tutorial we create a new scenario in the ION environment consisting of 3 nodes. Node 1 <-> Node 2 <-> Node 3.

### Running ION and Setting up the Scenario
For this exercise we will assume you have the NASA ION VM set up and running. If not, please follow the tutorial on installing the VM.

 **1. Open the VM and start the ION GUI.**

From the desktop of the virutal machine, right click -> Open Terminal.

Enter the command:

    core-gui &

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/304e0af8d5aa8136ea8187db0a155027d6a4640c/docs/image-resources/create-modify-doc/terminal-command.png?raw=true"/>
</p>

You should now see a blank canvas:

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/304e0af8d5aa8136ea8187db0a155027d6a4640c/docs/image-resources/create-modify-doc/blank-canvas.png?raw=true"/>
</p>

This is the canvas we will be creating our scenario in.

 **2. Create our working directory and save the scenario**

In the CORE GUI navigate to File -> Save as imn 

We want to save this file in a new folder in the directory: /home/core/NASA_DTN_CORE_Scenarios/CORE_configs

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/savenewscenario.png?raw=true"/>
</p>

**3. Create our Nodes**

We will be using 3 regular routers as our nodes for this example.

Select the blue cylinder, ensure not to select the blue cylinder with MDR on it.

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/add-3-normal-nodes.png?raw=true"/>
</p>

Click 3 times on the blank canvas to create 3 nodes, n1, n2 and n3.

Select the link tool and click and drag between nodes to connect them. 
Draw a link between n1 and n2, and one between n2 and n3.

Your canvas should now look like this:

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/connect-routers.png?raw=true"/>
</p>

### Creating Directories and Node files
We now need to create the configuration files for each node.

In our project directory /home/core/NASA_DTN_CORE_Scenarios/CORE_configs/New-Scenario 
Create folders for each of the 3 nodes, n1, n2 and n3.

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/directories.png?raw=true"/>
</p>

In each of these folders we need to create 7 files:

 - contacts.ionrc
 - X.bprc
 - X.ionconfig
 - X.ionrc
 - X.ionsecrc
 - X.ipnrc
 - X.ltprc

Where X is the node number, ie n1, n2 or n3

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/n1files.png?raw=true"/>
</p>

**Contents of each file:**

**contacts.ionrc**
This file is common across all 3 nodes and defines how the nodes are connected.

    #  FILE:          contacts.ionrc
    #  CONTENT:       contact graph commands
    #  FOR:           bpadmin
    #  BUILDER:       ION Configuration Editor
    #  NETWORK:       3node
    #  CONTACT GRAPH: contacts
    #  DATE:          Thu Jan 01 01:21:31 EST 1970
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         1         [Source Node: n1  with IP Name: 10.0.0.2]
    #  Destination node num:    1         [Dest Node: n1    with IP Name: 10.0.0.2]
    #  Distance (light secs):   1
    a range +0 +100000 1 1 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         2         [Source Node: n2  with IP Name: 10.0.2.1]
    #  Destination node num:    2         [Dest Node: n2    with IP Name: 10.0.2.1]
    #  Distance (light secs):   1
    a range +0 +100000 2 2 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         3         [Source Node: n3  with IP Name: 10.0.2.2]
    #  Destination node num:    3         [Dest Node: n3    with IP Name: 10.0.2.2]
    #  Distance (light secs):   1
    a range +0 +100000 3 3 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         1         [Source Node: n1  with IP Name: 10.0.0.2]
    #  Destination node num:    2         [Dest Node: n2    with IP Name: 10.0.0.1]
    #  Distance (light secs):   1
    a range +0 +100000 1 2 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         2         [Source Node: n2  with IP Name: 10.0.0.1]
    #  Destination node num:    1         [Dest Node: n1    with IP Name: 10.0.0.2]
    #  Distance (light secs):   1
    a range +0 +100000 2 1 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         2         [Source Node: n2  with IP Name: 10.0.2.1]
    #  Destination node num:    3         [Dest Node: n3    with IP Name: 10.0.2.2]
    #  Distance (light secs):   1
    a range +0 +100000 2 3 1
    #
    #  RANGE
    #  Start time (secs):       +0
    #  Stop time (secs):        +100000
    #  Source node num:         3         [Source Node: n3  with IP Name: 10.0.2.2]
    #  Destination node num:    2         [Dest Node: n2    with IP Name: 10.0.2.1]
    #  Distance (light secs):   1
    a range +0 +100000 3 2 1
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +100000
    #  Source node num:                    1         [Source Node: n1  with IP Name: 10.0.0.2]
    #  Destination node num:               1         [Dest Node: n1    with IP Name: 10.0.0.2]
    #  Transmit data rate (bytes per sec): 100000     [(KB/sec): 100  (MB/sec): 0  with K=1000]
    a contact +0 +100000 1 1 100000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +100000
    #  Source node num:                    2         [Source Node: n2  with IP Name: 10.0.2.1]
    #  Destination node num:               2         [Dest Node: n2    with IP Name: 10.0.2.1]
    #  Transmit data rate (bytes per sec): 100000     [(KB/sec): 100  (MB/sec): 0  with K=1000]
    a contact +0 +100000 2 2 100000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +100000
    #  Source node num:                    3         [Source Node: n3  with IP Name: 10.0.2.2]
    #  Destination node num:               3         [Dest Node: n3    with IP Name: 10.0.2.2]
    #  Transmit data rate (bytes per sec): 100000     [(KB/sec): 100  (MB/sec): 0  with K=1000]
    a contact +0 +100000 3 3 100000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +1000000
    #  Source node num:                    1         [Source Node: n1  with IP Name: 10.0.0.2]
    #  Destination node num:               2         [Dest Node: n2    with IP Name: 10.0.2.1]
    #  Transmit data rate (bytes per sec): 1000000     [(KB/sec): 1000  (MB/sec): 1  with K=1000]
    a contact +0 +1000000 1 2 1000000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +100000
    #  Source node num:                    2         [Source Node: n2  with IP Name: 10.0.2.1]
    #  Destination node num:               1         [Dest Node: n1    with IP Name: 10.0.0.2]
    #  Transmit data rate (bytes per sec): 1000000     [(KB/sec): 1000  (MB/sec): 1  with K=1000]
    a contact +0 +100000 2 1 1000000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +1000000
    #  Source node num:                    2         [Source Node: n2  with IP Name: 10.0.2.1]
    #  Destination node num:               3         [Dest Node: n3    with IP Name: 10.0.2.2]
    #  Transmit data rate (bytes per sec): 1000000     [(KB/sec): 1000  (MB/sec): 1  with K=1000]
    a contact +0 +1000000 2 3 1000000
    #
    #  CONTACT
    #  Start time (secs):                  +0
    #  Stop time (secs):                   +1000000
    #  Source node num:                    3         [Source Node: n3  with IP Name: 10.0.2.2]
    #  Destination node num:               2         [Dest Node: n2    with IP Name: 10.0.2.1]
    #  Transmit data rate (bytes per sec): 1000000     [(KB/sec): 1000  (MB/sec): 1  with K=1000]
    a contact +0 +1000000 3 2 1000000
     
    

These are examples of the n1 files. Ensure to alter each file to suit the node.


**n1.bprc**

    # Initialization command (command 1).
    1
    # Add an EID scheme.
    a scheme ipn 'ipnfw' 'ipnadminep’
    # Add some endpoints
    # a endpoint <endpoint> ‘x’ or ‘q’
    a endpoint ipn:1.0 x
    a endpoint ipn:1.1 x
    a endpoint ipn:1.2 x
    # Add protocols for external nodes.
    #-----------------------------------------------------------------
    # Estimate transmission capacity assuming 1400 bytes of each frame for payload, and 100 bytes for overhead.
    # a protocol [tcp|udp|ltp] 1400 100
    #
    # The following line will support a 'loopback’ communication capability using UDP
    a protocol udp 1400 100
    # Add inducts. (listen)
    #-----------------------------------------------------------------
    # a induct [tcp|udp] 0.0.0.0:4556 [PROTO]cli
    # a induct ltp X ltpcli
    a induct udp 0.0.0.0:4556 udpcli
    # Add outducts.
    #-----------------------------------------------------------------
    # a outduct [tcp|udp] DEST_IP_ADDR:DEST_IP_PORT [udpclo|””]
    #a outduct ltp x ltpclo
    #
    # The following line adds a ‘loopback’ UDP outduct
    a outduct udp 127.0.0.1:4556 udpclo
    # Select level of BP watch activities - 0 = None; 1 = All
    #-----------------------------------------------------------------
    w 1
    # RUN
    # Program: ipnadmin
    # On the configuration file name: n1.ipnrc
    r 'ipnadmin n1.ipnrc'
    # Start all declared schemes and protocols on the local node
    s

**n1.ionconfig**

    #  FILE:    n1.ionconfig
    #  CONTENT: configuration parameters
    #  FOR:     ionadmin
    #  BUILDER: ION Configuration Editor
    #  NETWORK: 3node
    #  NODE:    n1
    #  IP NAME: 10.0.2.1
    #  DATE:    Thu Jan 01 01:21:31 EST 1970
    
    
    wmKey 0
    sdrName ion
    wmSize 5000000
    configFlags 15
    heapWords 5000000
    pathName /var/ion

**n1.ionrc**

    #  INITIALIZE
    #  Ion node number:  1
    #  Ion configuration file name:  n1.ionconfig
    1 1 n1.ionconfig
    #
    #  START
    #  Program:   rfxclock
    s

**n1.ionsecrc**

    1
    e 1

**n1.ipnrc**

    #  FILE:    n1.ipnrc
    #  CONTENT: configuration commands
    #  FOR:     ipnadmin
    #  BUILDER: ION Configuration Editor
    #  NETWORK: 3node
    #  NODE:    n1
    #  IP NAME: 10.0.2.1
    #  DATE:    Thu Jan 01 01:21:31 EST 1970
    #
    #  PLAN
    #  Destination node:   1         [To Node: n1  with IP Name: 10.0.0.2]
    #  Duct Expression:    udp/*
    a plan 1 udp/10.0.0.2
    
    #
    #  PLAN
    #  Destination node:   2         [To Node: n2  with IP Name: 10.0.0.1]
    #  Duct Expression:    udp/*
    a plan 2 udp/10.0.0.1

**n1.ltprc**

    #Initialization command (command 1).
    #Establish the LTP retransmission window.
    #A maximum of 64 sessions. 1 session ~ 1 second of transmission
    #Set a block size limit of 1000000 bytes. (approx data sent per session)
    ####1 [MAX_SESSIONS] [MAX_BLOCK_SIZE]
    1 100 100000
    #-----------------------------------------------------------------
    #Add a span (a connection)
    # peer_engine_nbr
    # max_export_sessions
    # max_import_sessions
    # max_segment_size
    # aggregation_size_limit
    # aggregation_time_limit
    # LSO_command
    # [queuing_latency]
    # e.g. a span <PEER_NUM> 100 100 64000 100000 1 'udplso x.x.x.x:1113 40000000’
    #-----------------------------------------------------------------
    # Listener on 0.0.0.0
    # s 'udplsi 0.0.0.0:1113'
    w 1

### Assigning Directories in ION

For each node in the ION environment we must give it its own private directory.

**For each node:**

 1. Right click on the node -> Services

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/privatedirectories.png?raw=true"/>
</p>

2. UserDefined

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/directories-userdefined.png?raw=true"/>
</p>

 3. (Top Ribbon) Directories -> Bottom Right (Paper with a star icon) 

The directory should be /var/ion

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/var-ion.png?raw=true"/>
</p>

 4. OK -> Apply -> Apply

**Repeat these steps for each node**

### Running the nodes
We will now run the nodes and get the services running.

For each node navigate to the directory with the contacts.ion, n1.bprc etc and open a new terminal.

 1. Enter the following commands one line at a time:

. 

    ionadmin n1.ionrc
    
.

    ionadmin contacts.ionrc
   .

    ionsecadmin n1.ionsecrc
   .

    bpadmin n1.bprc
   .
   

    ltpadmin n1.ltprc
   .



<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/starting%20n1.png?raw=true"/>
</p>


2. Enter the command to see the services running on the node:

    ps auxww

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/c0575d1c06ae83580fb207af26b6ce135d2a2c43/docs/image-resources/create-modify-doc/n1services%20running.png?raw=true"/>
</p>

**Repeat for nodes n2 and n3**


**We now have the nodes running and ready to communicate**
****
