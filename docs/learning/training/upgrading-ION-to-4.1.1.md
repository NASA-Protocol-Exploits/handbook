## How to Upgrade ION
### Introduction

This tutorial will walk through upgrading the ION version to the most current version 4.1.1.

**Please Note:**
You may wish to perform this upgrade on a clone of your ION VM in order to retain a working version of the previous ION. 

This can be done by right clicking on your ION VM in Virtual Box and selecting Clone:

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/clone.png?raw=true"/>
</p>

Select Next -> Full Clone -> Clone


### Updating AutoMake

In order to install ION 4.1.1 we first must update AutoMake to version 1.16.1

 1. Open Firefox Browser 
 2. Copy the link: https://ftp.gnu.org/gnu/automake/automake-1.16.1.tar.gz

The file will be downloaded to the download folder.

 3. Navigate to the downloads folder and open a terminal
 4. Move the file to the /opt directory using the command:
 
 .
 
    sudo mv automake-1.16.1.tar.gz /opt

 5. Navigate to the /opt directory and open a terminal 
 6. Extract to this directory using the command:

.

    sudo tar -xf automake-1.16.1.tar.gz

 7. Navigate into the automake directory and open a terminal.
<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/beforemakeinstall.png?raw=true"/>
</p>


Enter the following commands 1 line at a time:

    sudo ./configure
    sudo make
    sudo make install

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/aftermakeinstall.png?raw=true"/>
</p>

**We have updated AutoMake to version 1.16.1**

### Updating ION

We will follow the same procedure for ION as we did for AutoMake.

 1. Open Firefox and copy the link: https://sourceforge.net/projects/ion-dtn/
 2. Download ION 4.1.1 by clicking the green download button

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/downloadION.png?raw=true"/>
</p>

3. Navigate to the downloads folder and open a terminal
 4. Move the file to the /opt directory using the command:
 
 .
 
    sudo mv ion-open-source-4.1.1.tar.gz /opt

 5. Navigate to the /opt directory and open a terminal 
 6. Extract to this directory using the command:

.

    sudo tar -xf ion-open-source-4.1.1.tar.gz

 7. Navigate into the ion directory and open a terminal.
<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/ionbeforemake.png?raw=true"/>
</p>


Enter the following commands 1 line at a time:

    sudo ./configure
    sudo make
    sudo make install

**Note: the make command may take a few minutes to complete**


<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/ionaftermake.png?raw=true"/>
</p>

 8. Check the ION version by enetering the following commands:
 

     ionadmin
     v

The console should display the version as ION-OPEN-SOURCE-4.1.1

<p align="center">
  <img src="https://github.com/NASA-Protocol-Exploits/handbook/blob/ee78a478a1ed4f7a8e6e5dec57736da66fa4380f/docs/image-resources/updating-ion-4/running4.png?raw=true"/>
</p>


**We have updated ION to version 4.1.1**

****
