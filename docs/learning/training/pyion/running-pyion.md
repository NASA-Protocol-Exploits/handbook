# Running PyION

## Using PyION within a virtual container

***Note:** If you want to use it within a container, there’s some quirks with overlapping Python2 and Python3. You’ll need to run `unset PYTHONPATH` in every shell you want to run python scripts in. There’s probably a more innovative way of doing this. However, this is the current workaround, as displayed below in _figure 1_.*

<figure align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/executing-unset-pythonpath.PNG?raw=true"/>
  <figcaption><i>Figure 1: A screenshot of the `unset PYTHONPATH` being executed on node three inside the virtual enviroment.</i></figcaption>
</figure>

*Also, remember that containers die every time you stop them. So write the python script on your host, copy them across to the container, and run them with `python3 script.py.`*

## Setting up the Transmitter and Receiver  (Step by Step Guide)

To execute python scripts utilizing the PyION library, you will first need to spin up a virtual container on the respective **transmitting** and **receiving** nodes within the ION-DTN scenario inside CORE.

**Step One**
Launch the core emulator using the `core-gui` command from the terminal, and load any scenario from the  NASA_DTN_DEV_KIT or NASA_Exploit_Scenarios. For the purpose of the exercise we will be loading the ImageTransfer.imn file found here `/home/core/NASA_DTN_CORE_Scenarios/CORE_configs/ImageTransfer/ImageTransfer.imn`

<figure align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/load-base-image-transfer-scenario.PNG?raw=true"/>
  <figcaption><i>Figure 2: A screenshot of the 'ImageTransfer.imn' sceanrio file being loaded into the CORE enviroment</i></figcaption>
</figure>

**Step Two**
Start the session by click the green "Start the session" icon in the left hand toolbar of CORE enviroment. Then, Open a shell on both node 3 and node 4 by double clicking on each node. Right click on each terminal tab to detach them if you prefer to have seperate windows. 

Next, run the `unset PYTHONPATH` on the node 3 and node 4 shells to avoid the overlapping python2/python3 errors. 

<figure align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/spawn-shells-for-node3-and-node4.PNG?raw=true"/>
  <figcaption><i>Figure 3: A screenshot of the node 3 and node 4 shells open on the virtual machine</i></figcaption>
</figure>

**Step Three**
Repeat step two a second time except place the resepective terminal windows underneath the existing terminals so that they are both readable and easily acceisble as depict in the screenshot below. 

Next, run the `vim sender.py` on node 3 and `vim receiver.py` on node 4 top shells, this is where we will create and edit of scripts, and below is where we will execute them.

<figure align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/spawn-shells-for-node3-and-node4-again.PNG?raw=true"/>
  <figcaption><i>Figure 1: A screenshot of all four shell windows open on the virtual machine</i></figcaption>
</figure>
