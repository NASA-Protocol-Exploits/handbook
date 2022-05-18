# Installing PyION & Obtaining ION Open Source 
This guide will show installation on the NASA ION Dev Kit, but the same steps can work in any Ubuntu-based OS.

***Note:** A package does exist on `pip` which is called pyion, but this is **_not_** the one we’re after – that one is some maths utilities. In fact, the version we’re after is not available on any packaging service.*

Reference steps here: [https://pyion.readthedocs.io/en/latest/install.html](https://pyion.readthedocs.io/en/latest/install.html)

## Introduction
Firstly, we need to decide what version of ION Open Source we will be using. The NASA Dev Kit comes with version v3.6.2, and it is essential to match your ION version to your PyION version. Skip this step if you are not changing ION Open Source Version. You will still need a copy of the ION source code, however

***Note:** Skip to here if you already have the ION source code downloaded and your chosen version installed.*

## Updating ION
<details>
<summary>I updating my ION version and I  am aware it may be lacking features, where should I begin?</summary>  

 **1**. Download the correct version of ION from [https://sourceforge.net/projects/ion-dtn/](https://sourceforge.net/projects/ion-dtn/)
 
 **2.** Download the latest version of [automake](https://www.gnu.org/software/automake/#downloading) v1.16 at this time. The version on the apt repos is unfortunately way out of date. Thanks, Canonical.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Download to your ubuntu virtual machine.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**b.** `cd` to extracted dir  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**c.** Extract the contents with `tar –xvf automake-1.16.tar.xz`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**d.** Run `./configure`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**e.** Run `make`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**e.** Run `sudo make install`  

 **3.** Next, `cd` to the download location for ION Open Source
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Extract the contents with `tar –xvzf [filename]`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**b.** Run the following:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**i.** `autoheader`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ii.** `aclocal`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**iii.** `autoconf`	  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**iv.** `automake`  	
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**v.** `./configure CFLAGS='-O0 -ggdb3' CPPFLAGS='-O0 -ggdb3' CXXFLAGS='-O0 -ggdb3'`    		
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**vi.** `make`	 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**vii.** `sudo make install`	  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**vii.** `sudo Idconfig`	 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**c.** Congratulations you've updated your version of ION.  
</details>

## Installing PyION
**1**. Download the correct version of PyION from [https://github.com/msancheznet/pyion]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Alternatively, use `git clone https://github.com/msancheznet/pyion.git`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**b.** `cd` to downloaded dir  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**c.** Checkout to the correct branch. You can look at branches with `git branch -a`. I’m choosing v3.6.2 in this case.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**d.** Run `git checkout v3.6.2`  

**2**. Install the python dev tools with `sudo apt-get install autotools-dev automake python3-dev`  

**3**. Install some more python dependencies:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Run `sudo apt-get install python3-setuptools`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**b.** Run `pip install pathlib`  

**4.**	Set the `ION_HOME` environment variable to the location of the ION source code we downloaded above. For me this is found at `/home/core/ion-open-source-3.6.2`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Run `export ION_HOME=/home/core/ion-open-source-3.6.2`   

**5.**	Finally it is ready to install:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**a.** Run `sudo -E python3 setup.py install`   
