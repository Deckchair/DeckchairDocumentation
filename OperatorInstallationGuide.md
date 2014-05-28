DeckchairOperator - Installation Guide
=========================================

Requirements:

* A computer or mobile phone that can connect to wifi networks and browse webpages. Your chosen device must be close to the camera unit so it can pick up the broadcast wifi network.
* Bolts to attach the mounting arm to the wall. We do not supply these as the choice is dependent upon the materials you are mounting to. The smaller box will contain the mounting arm should you wish to asses it before installation.

Before mounting the camera in it's final location, it is advisable to setup the internet connection in a more convenient place.


DeckchairOperator Setup
-------------------

Your package should contain three components:

*	Camera unit - Glass fronted, metal enclosure
*	Power Supply Unit - White, plastic box
*	Mounting Arm - This may vary per installation


**Step 1:**

Connect an ethernet cable to the camera housing via the ethernet plug cable gland.
If you have requested a WiFi connected unit, you can skip this step.


**Step 2:**

Connect the power cable from the _Camera unit_ to the contacts in the Power Supply Unit. Cable glands are provided inside the Power Supply Unit.

The documentation within the Power Supply Unit illustrates the correct location for each wire.


**Step 3:**

Connect the mains power to the Power Supply Unit and switch it on, you should be able to hear the fans start up in the Camera unit. Wait 2 minutes to allow the system to configure itself before continuing.


**Step 4:**

The Camera unit will broadcast a WiFi signal with the name (SSID) "DeckchairOperator-XXXX", the final four characters are unique to each system. Connect to this WiFi network using a smart phone or laptop near the unit.

The password to connect to the WiFi network is:

* Password: tumbleweed


**Step 5:**

Once connected to the WiFi network, open the web browser on your phone/laptop and navigate to [http://192.168.42.1](http://192.168.42.1)

*If you are on an Apple computer, iPad or iPhone you can use the friendlier address: [http://deckchairoperator.local](http://deckchairoperator.local)*

You will be prompted to enter a username and password, use the following:

* Username: deckchair
* Password: tumbleweed


**Step 6:**

You will now see the DeckchairOperator dashboard. The system performs a variety of tests whilst loading the dashboard, these are listed on the dashboard and highlighted with Green or Red.

The first block of tests in the "Information" table relate to components within the Camera enclosure. If any of these are red it could indicate a component or connection damaged in transit, if this is the case contact us immediately so we can assist you in resolving it.

The second block of tests in the "Remote Connectivity" table relate to the internet connection. The operator will attempt to connect to two Deckchair servers over the internet, atleast one of the two tests must succeed.

If atleast one of the "Remote Connectivity" tests succeeds skip to **Step 8**


**Step 7**

If the DeckchairOperator was not able to connect to the internet using default settings (DHCP), you will need to work with the relevant IT department to get it connected.

Click the "Setup Ethernet" link at the top of the DeckchairOperator dashboard.

*If you requested a DeckchairOperator with the ability to connect to WiFi netowrks, the same steps apply except you will need to click the "Setup Wifi" link.*

In the setup page you can configure the network definition that will be saved into the network configuration file. This is a standard Linux network configuration, usually found in a location such as */etc/network/interfaces*

The format is simple and documentation is provided at the bottom of the page. The input box should show the current configuration (DHCP) and some comments illustrating how to change this (if a line starts with a # it is a comment and ignored by the system).

Replacing the contents of the textbox with the following would setup a static IP connection, instead of the default DHCP:

>iface eth0 inet static  
>address 192.0.2.7  
>netmask 255.255.255.0  
>gateway 192.0.2.254

If you require MAC addresses for whitelisting on your network visit the "Advanced" link in the navigation and such details should be available in the "ifconfig" output.

You will need a working internet connection displayed in the dashboard before continuing to **Step 8**.

If you have any issues setting up your network, please contact us, with as much information as possible about your intended setup so we can assist you.


**Step 8:**

Before mounting it is advisable to test the cameras, to do this click the "Snapshot" link in the navigation.

This page will immediately request an image from both cameras, it can take upto a minute to capture, process and show the images.

The quality of image from the video camera is less important than the primary image camera.

You may decide you want to 'zoom' in a bit to crop the view slightly - to do this, remove the lid of the Camera unit - carefully and slowly. You will need to tilt it to avoid the camera lens and components when lifting.

Turn the zoom ring and re-check the snapshot as desired.

**Step 9:**

Choose camera mounting location, take into account the following:

• Cable length - power and ethernet cables are not provided unless requested so ensure your mounting location is within reach of power and ethernet.

• Power supply unit - we supply a short outdoor grade cable between the PSU and Camera, ensure the PSU can be mounted nearby your chosen camera mounting location.


  * Fix mounting arm into wall ensuring it is level
  * Mount camera to the mounting arm
  * Mount Power Supply Unit nearby
  
**Step 10:**

Done! The camera will communicate with us over your internet connection and we will be in touch to clarify it has successfully been setup.