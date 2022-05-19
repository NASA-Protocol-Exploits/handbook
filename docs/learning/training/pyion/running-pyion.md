
# Running PyION

## Using PyION within a virtual container

***Note:** If you want to use it within a container, there’s some quirks with overlapping Python2 and Python3. You’ll need to run `unset PYTHONPATH` in every shell you want to run python scripts in. There’s probably a more innovative way of doing this. However, this is the current workaround, as displayed below in _figure 1_.*

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/executing-unset-pythonpath.PNG?raw=true"/>
</p>

*Also, remember that containers die every time you stop them. So write the python script on your host, copy them across to the container, and run them with `python3 script.py.`*

## Step One
To execute python scripts utilizing the PyION library, you will first need to spin up a virtual container on the respective **transmitting** and **receiving** nodes within the ION-DTN scenario inside CORE.

Launch the core emulator using the `core-gui` command from the terminal, and load any scenario from the  NASA_DTN_DEV_KIT or NASA_Exploit_Scenarios. For the purpose of the exercise we will be loading the ImageTransfer.imn file found here `/home/core/NASA_DTN_CORE_Scenarios/CORE_configs/ImageTransfer/ImageTransfer.imn`

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/load-base-image-transfer-scenario.PNG?raw=true"/>
</p>

## Step Two

Start the session by click the green "Start the session" icon in the left hand toolbar of CORE enviroment. Then, Open a shell on both node 3 and node 4 by double clicking on each node. Right click on each terminal tab to detach them if you prefer to have seperate windows. 

Next, run the `unset PYTHONPATH` on the node 3 and node 4 shells to avoid the overlapping python2/python3 errors. 

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/spawn-shells-for-node3-and-node4.PNG?raw=true"/>
</p>

## Step Three

Repeat step two a second time except place the resepective terminal windows underneath the existing terminals so that they are both readable and easily acceisble as depict in the screenshot below. 

Next, run the `vim sender.py` on the node 3 shell and `vim receiver.py` on the node 4 shell, this is where we will create and edit of scripts, and below is where we will execute them.

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/spawn-shells-for-node3-and-node4-again.PNG?raw=true"/>
</p>

## Step Four
Enter the following code into the `sender.py` terminal, older vim can be confusing to use are first so check out this guide [here](https://www.howtoforge.com/vim-basics) :

    import pyion
    
    # Create a proxy to node 1 and attach to ION
    proxy = pyion.get_bp_proxy(1)
    proxy.bp_attach()

    # Open endpoint 'ipn:3.3' and send data to 'ipn:4.3'
    with proxy.bp_open('ipn:3.3') as eid:
	    eid.bp_send('ipn:4.3', b'hello')

Then, be sure to write the file with by `esc` then `:w` then `enter` to write it.  

Now repeat the above process for the `receiver.py` temrinal :

    import pyion
    
    # Create a proxy to node 2 and attach to it
    proxy = pyion.get_bp_proxy(2)
    proxy.bp_attach()

    # Listen to 'ipn:4.3' for incoming data
    with proxy.bp_open('ipn:4.3') as eid:
	    while eid.is_open:
		    try:
			    # This is a blocking call.
			    print('Received:, eid.bp_receive())
			except InterruptedError:
				# User has triggered interruption with Ctrl+C
				break
	    

Then, be sure to write the file with by `esc` then `:w` then `enter` to write it.  

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/add-code-to-node3-and-node4.PNG?raw=true"/>
</p>

## Step Four
Now, execute the python scripts from the bottom termianls begin with the receiver on node 4 run by running 'python3 receiver.py' followed by 'python3 sender.py' on node 3.
<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/main/docs/image-resources/running-pyion-doc/execute-script-on-node4-then-node3.PNG?raw=true"/>
</p>


## Step Five
Congratulations you have just learnt how to send packets with PyION.
