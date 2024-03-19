<h1>Building a Cybersecurity Homelab for Detection & Monitoring - In Progress</h1>

<p>Applying and implementing security ideas in cyberspace can be difficult if there is no practical and safe infrastructure to carry out these tasks.</p>

<h2>What is a Homelab?</h2>
As the name suggests, a home lab is a space where you may hone your talents in a particular area and practice. Large-scale infrastructure components and tools are mirrored in this home lab. Working with these parts and learning how they operate is safe here.
<br />


<h1>CONTENT</h1>

- <b>Installing VMware Workstation as hypervisor</b> 
- <b>Configuring pfSense firewall for Network Segmentation & Security</b>
- <b>Configuring Security Onion as an all-in-one IDS, Security Monitoring, and Log Management solution</b>
- <b>Configuring Kali Linux as an attack machine</b>
- <b>Configuring a Windows Server as a Domain Controller</b>
- <b>Configuring Windows desktops</b>
- <b>Configuring Splunk</b>
- <b>Ubuntu/CentOS/Metasploitable/DVWA/Vulnhub machines: All these are potential Linux machines that can be added to the network for exploitation, detection, or monitoring purposes.</b>

<h1>HOMELAB NETWORK DESIGN & TOPOLOGY</h1>
<p align="center">
<br/>
<img src="https://imgur.com/CYnPf1N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h2>Downloading & Installing VMware Workstation Pro</h2>
<p>For the purpose of this lab, I’ll be using VMware Workstation 16 Pro as my hypervisor. I currently cannot afford the pro at this time so I will be using the 30 day free trial, but I assure you it is a very worthwhile investment.</p>
<br>
<p align="center">
<a href="https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html">Downloading VMware Workstation Player</a>
<img src="https://imgur.com/9UIlBHo.png" height="80%" width="80%" alt="VMware"/>
</p>

<h1>Configuring pfsense</h1>
<p>pfsense will be configured as a firewall to segment our private homelab network and will be only accessible from our Kali Linux machine.</p>
<br>
<p>Download the pfsense ISO file from here: <a href="https://www.pfsense.org/download/">Download pfsense community edition</a></p>
<br>
<p>After you download pfsense, you will need to also download 7 zip file manager. Afterwards right click pfsense file, press 7-Zip and then extract to "pfsense".</p>
<p>Download 7 zip file manager here: <a href="https://www.7-zip.org/">Download 7-Zip file manager</a></p>
<br>
<p>Click “Create a New Virtual Machine” on VMware Workstation Homescreen.</p>
<br>
<p>Make sure “Typical (recommended)” is selected and click Next.</p>
<br>
<p align="center">
<img src="https://imgur.com/Uh8o283.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>Click “Browse” and navigate to the folder where your pfsense file is located.</p>

Click Next.

<p align="center">
<img src="https://imgur.com/4ukxCXk.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>Rename your Virtual Machine. Preferably “pfsense”</p>

Click Next.

<p align="center">
<img src="https://imgur.com/4ukxCXk.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>20GB disk size is sufficient for this VM.</p>
<br>
<p>Ensure that the “Split virtual disk into multiple files” option is selected.</p>

Click Next.

<p align="center">
<img src="https://imgur.com/2ydpTKr.png" height="40%" width="30%" alt="VMware"/>
</p>                                                                                                                  
<P>Click “Customize Hardware”.</P>
<br>
<p align="center">
<img src="https://imgur.com/ydTrmYm.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>Increase the memory to 2GB.</p>
<br>
<p align="center">
<img src="https://imgur.com/nTvzuwc.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>Add 5 network adapters and correspond them with a VMnet interface as shown below. Then click Finish.</p>
<br>
<p align="center">
<img src="https://imgur.com/BAqloDB.png" height="40%" width="30%" alt="VMware"/>
</p>
<p align="center">
<img src="https://imgur.com/6cmLvVh.png" height="40%" width="30%" alt="VMware"/>
</p>
<p>The pfsense machine will power on and start with this screen. Accept all the defaults. pfsense will configure and reboot.</p>

<p align="center">
<img src="https://imgur.com/xfbZVxy.png" height="40%" width="30%" alt="VMware"/>
<p>You should end up with a screen similar to this
<p align="center">
<img src="https://imgur.com/VxJqIWB.png" height="40%" width="30%" alt="VMware"/>
<p>Enter option 1</p>
<br>
<b>Should VLANS be set up now [y:n]?:</b>n</p>
<br>
<p>Enter <b>em0, em1, em2, em3, em4, em5</b> respectively for each consecutive question</p>
<br>
<b>Do you want to proceed? [y:n]?:</b> y
<br>
<p align="center">
<img src="https://imgur.com/yWjrChD.png" height="40%" width="30%" alt="VMware"/>
<p align="center">
<img src="https://imgur.com/yuabhaq.png" height="40%" width="30%" alt="VMware"/>
<p>Enter option 2</p>
<br>
<p>We'll start with a LAN interface (2)</p>
<br>
<p>The ip address <b>192.168.1.1</b> is going to be used to access the pfsense WebGUI via the Kali Machine</p>
<br>
<p>Use the configuration below for the LAN interface.</p>
<br>
<p align="center">
<img src="https://imgur.com/6kq8QcW.png" height="40%" width="30%" alt="VMware"/>
<p>Use the configeration below for the OPT1 interface.</p>
<p align="center">
<img src="https://imgur.com/CdyK6pC.png" height="40%" width="30%" alt="VMware"/>
<p>Use the configeration below for the OPT2 interface.</p>
<p align="center">
<img src="https://imgur.com/JaFfFJl.png" height="40%" width="30%" alt="VMware"/>
<p>Leave the OPT3 interface without an IP as it is going to have the span port with traffic that Security Onion will be monitoring.</p>
<br>
<p>Use the configertion for the OPT4 interface.</p>
<br>
<p align="center">
<img src="https://imgur.com/lr3hqNM.png" height="40%" width="30%" alt="VMware"/>
<p>This ends the configuration of the pfsensse VM. The rest of the configuration will be done via the kali machine through the WebConfigurator.</p>
<br>
<p><b>Configuring Security Onion</b></p>
<br>
<p>This will be the all-in-one IDS, Security Monitoring, and Log Management solution.</p>
<a href="https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md"> Dowload the Security Onion ISO file from here</a>
<br> 
<p>Select Typical installation >> Click Next</p>
<br>
<P>Installer disc imagine file >> SO ISO file path >> Click Next</P>
<br>
<p>Choose Linux, CentOS 7 64-Bit and Click Next</p>
<p align="center">
<img src="https://imgur.com/Quzqrvp.png" height="40%" width="30%" alt="VMware"/>
<p>Specify virtual machine name and click Next.</p>
<p align="center">
<img src="https://imgur.com/1ajkX7p.png" height="40%" width="30%" alt="VMware"/>
<p>Specify disk size (minimum 200GB), store as single file, click Next.</p>
<p align="center">
<img src="https://imgur.com/zYsDuOQ.png" height="40%" width="30%" alt="VMware"/>
<p>Click "Customize Hardware" and do the following:</p>
<br>
<p>~ Change memory to 4-32GB</p>
<br>
<p>~ Add two Network Adapters and assign them Vmnet 4 & Vmnet 5 respectively</p>
<br>
<p align="center">
<img src="https://imgur.com/fKhVcdR.png" height="40%" width="30%" alt="VMware"/>
<p>Click "Finish"</p>
<br>
<p>Power the virtual machine and click Enter when prompted:</p>
<br>
<p>After the initial stages of loading, type "yes" when prompted</p>
<p align="center">
<img src="https://imgur.com/Jt0TPgI.png" height="50%" width="60%" alt="VMware"/>
<p>~ Set a username & password:</p>
<br>
<p>After Securtiy Onion Reboots, proceed with the following:</p>
<br>
<p>Enter the username & password</p>
<br>
<p>Select "Yes"</p>
<p align="center">
<img src="https://imgur.com/npPhScU.png" height="50%" width="40%" alt="VMware"/>
<p>Click Enter</p>
<p align="center">
<img src="https://imgur.com/xx7Jy68.png" height="50%" width="60%" alt="VMware"/>
<p>Select the EVAL option</p>
<p align="center">
<img src="https://imgur.com/cufHdZi.png" height="50%" width="40%" alt="VMware"/>
<p>Type "AGREE"</p>
<p align="center">
<img src="https://imgur.com/J90fiKH.png" height="50%" width="40%" alt="VMware"/>
<p>Select "Standard"</p>
<p align="center">
<img src="https://imgur.com/DowDNhv.png" height="50%" width="60%" alt="VMware"/>
<p>Set a hostname, and a short description</p>
<br>
<p>Click the spacebar to select ens33 as the managment interface</p>
<p align="center">
<img src="https://imgur.com/NpwzMa3.png" height="50%" width="40%" alt="VMware"/>
<p>Set the addressing to DHCP:</p>
<p align="center">
<img src="https://imgur.com/sUmKZ7B.png" height="50%" width="40%" alt="VMware"/>
<p>Select "YES" at the next prompt.</p>
<br>
<p>Select "OK" at the next promp.t</p>
<br>
<p>Select "Direct" at the next prompt.</p>
<br>
<p>Select "ens34" as the Monitor Interface.</p>
<p align="center">
<img src="https://imgur.com/INA4Xxo.png" height="50%" width="40%" alt="VMware"/>
<p>Select "Automatic" for the OS patch schedule</p>
<br>
<p>Accept the default home network ip</p>
<br>
<p>Accept all the defaults</p>
<br>
<p>Enter an email address and password for the admin account</p>
<br>
<p>Select "IP"</p>
<p align="center">
<img src="https://imgur.com/gFJei0G.png" height="50%" width="60%" alt="VMware"/>
<p>Select "Yes" for the NTP server & accept the defaults</p>
<br>
<p>Take note of your final settings before proceeding! If possible take a screenshot.</p>
<br>
<p><b>Most important detail is the IP address for web access.</b></p>
<br>
<p>Select "Yes"</p>
<p align="center">
<img src="https://imgur.com/63Es9oc.png" height="50%" width="60%" alt="VMware"/>
<p><b>SecOnionMgmt/ Analyst Machine</b></p>
<br>
<p>After installing Security Onion, having access to the web interface will be done from an external Ubuntu Desktop simulation a SOC/Security Analyst accessing a SIEM or any other tool from their device.</p>
<br>
<p>In order to do this, you'll first have to configure an Ubuntu Desktop. This is a very easy process so it will not be in this write-up, but it is covered in the video. Be sure to use all the default settings for the Ubuntu Desktop configuration.</p>
<br>
<a href="https://ubuntu.com/download/desktop">Download Ubuntu Desktop</a>
<br>
<a href="https://getlabsdone.com/10-easy-steps-to-install-ubuntu-19-04-on-vmware-workstation-15/">Install Ubuntu Desktop</a>
<br>
<br>
<p>After this installation, run the <b>ifconfig</b> command on the Ubuntu Machine and take note of its IP address.</p>
<br>
<p>Head back to your Security Onion instance and run the following command</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
