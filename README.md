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
<p>Enter option 1
<br>
<b>Should VLANS be set up now [y:n]?:n</b>
<p>Enter <b>em0, em1, em2, em3, em4, em5</b> respectively for each consecutive question</p>
<b>Do you want to proceed? [y:n]?:</b> y

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
