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
<img src="https://imgur.com/EaWS0ts.png" height="50%" width="40%" alt="VMware"/>
<p>Click Enter</p>
<p align="center">
<img src="https://imgur.com/oFQLCoP.png" height="50%" width="60%" alt="VMware"/>
<p>Select the EVAL option</p>
<p align="center">
<img src="https://imgur.com/ahqJoA7.png" height="50%" width="40%" alt="VMware"/>
<p>Type "AGREE"</p>
<p align="center">
<img src="https://imgur.com/wyFoIFV.png" height="50%" width="40%" alt="VMware"/>
<p>Select "Standard"</p>
<p align="center">
<img src="https://imgur.com/4MFfHZH.png" height="50%" width="60%" alt="VMware"/>
<p>Set a hostname, and a short description</p>
<br>
<p>Click the spacebar to select ens33 as the managment interface</p>
<p align="center">
<img src="https://imgur.com/v88HfCr.png" height="50%" width="40%" alt="VMware"/>
<p>Set the addressing to DHCP:</p>
<p align="center">
<img src="https://imgur.com/68eGJnw.png" height="50%" width="40%" alt="VMware"/>
<p>Select "YES" at the next prompt.</p>
<br>
<p>Select "OK" at the next promp.t</p>
<br>
<p>Select "Direct" at the next prompt.</p>
<br>
<p>Select "ens34" as the Monitor Interface.</p>
<p align="center">
<img src="https://imgur.com/2RDioHB.png" height="50%" width="40%" alt="VMware"/>
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
<img src="https://imgur.com/DCQlEEc.png" height="50%" width="60%" alt="VMware"/>
<p>Select "Yes" for the NTP server & accept the defaults</p>
<br>
<p>Take note of your final settings before proceeding! If possible take a screenshot.</p>
<br>
<p><b>Most important detail is the IP address for web access.</b></p>
<br>
<p>Select "Yes"</p>
<p align="center">
<img src="https://imgur.com/rB9WQe4.png" height="50%" width="60%" alt="VMware"/>
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
<p>Head back to your Security Onion instance and run the following command "<b>sudo so-allow</b>"</p>
<br>
<p>Enter your password</p>
<br>
<p>Type "a" and wait for the process to complete.</p>
<p align="center">
<img src="https://imgur.com/gDL9kG8.png" height="50%" width="60%" alt="VMware"/>
<p>Type in the IP address from the Ubuntu Desktop</p>
<br>
<p>This will create a firewall rule on Security Onion that will allow you web access from your Ubuntu Desktop.</p>
<br>
<p>Navigate to the Security Onion IP address on your Ubuntu Desktop:</p>
<p align="center">
<img src="https://imgur.com/T5VN7zY.png" height="50%" width="60%" alt="VMware"/>
<p>This ends the configuration of the Security Onion VM.</p>
<br>
<p><b>Configuring Kali Linux</b></p>
<br>
<p>Kali Linux will be used as an attack machine to propagate different forms of offensive actions against the Domain Controller and the other machines attached to it.</p>
<a href="https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/">Download the Kali Linux ISO from here</a>
<br>
<br>
<p>Since you're downloading the VM file, all you'll need to do is click on the .vmx file from the Kali folder you downloaded and it will automatically load up the default Kali image in VMware.</p>
<br>
<p>Before powering on the Kali, change the network adapter to <b>Vmnet2</b> and its memory to <b>4GB</b>, then power it on and use default credentials as specified.</p>
<p align="center">
<img src="https://imgur.com/Qc2jTde.png" height="50%" width="40%" alt="VMware"/>
<p>After powering on, use this command to change the default password to a more secure one of your choice:</p>
<br>
<p>The Kali Machine is ready for use now.</p>
<p><b>pfsense Interfaces and Rules</b></p>
<br>
<p>Now that the Kali machine is set up, the pfsense WebConfigurator can be accessed in order to make some changes to the pfsense interface and firewall rules.</p>
<br>
<p>Navigate to the web browser and search for <b>192.168.1.1</b></p>
<br>
<p>Select "Advanced.." at this screen:</p>
<p align="center">
<img src="https://imgur.com/QRZfyWg.png" height="50%" width="60%" alt="VMware"/>
<p>Accept the risk and continue:</p>
<p align="center">
<img src="https://imgur.com/p6tIMXt.png" height="50%" width="60%" alt="VMware"/>
<p>Sign into pfsense using default credentials "<b>admin</b>" & "<b>pfsense</b>".</p>
<br>
<p>You'll be greeted with a "<b>Wizard/pfSense Setup/</b>" page.</p>
<br>
<p>Click next until you get to Step <b>2 of 9</b>.</p>
<br>
<p>Add <b>8.8.8.8</b> as your primary DNS server.</p>
<br>
<p>Add <b>4.4.4.4</b> as your secondary DNS server.</p>
<br>
<p>Click Next.</p>
<p align="center">
<img src="https://imgur.com/I7g76Ii.png" height="60%" width="60%" alt="VMware"/>
<p>At step <b>3 of 9</b>, choose your timezone, then click Next.</p>
<br>
<p>At step <b>4 of 9</b>, untick the last two options</p>
<br>
<p>At step <b>5 of 9</b>, Click Next</p>
<p align="center">
<img src="https://imgur.com/kEu1SRn.png" height="50%" width="60%" alt="VMware"/>
<p>At step <b>6 of 9</b>, set a new Admin Password</p>
<br>
<p>Click Next</p>
<br>
<p>At step <b>7 of 9</b>, Click <b>Reload</b></p>
<br>
<p><b>Finish</b></p>
<br>
<p>At this point, pfsense Wizard is complete and changes can now be made to the interfaces.</p>
<br>
<p>Click on <b>Interfaces</b></p>
<br>
<p>Select <b>LAN</b></p>
<br>
<p>For "Description", change <b>LAN</b> to <b>Kali</b> as this is the Kali Interface.</p>
<br>
<p>Scroll all the way down and click <b>Save</b>.</p>
<p align="center">
<img src="https://imgur.com/oJFXYwL.png" height="50%" width="60%" alt="VMware"/>
<p>If you get an error, use this <a href="https://blog.matrixpost.net/pfsense-2-5-0-bug-renaming-of-lan-interface-runs-into-an-error-regarding-router-advertisements-server-is-active/">Article</a> to troubleshoot and fix it.</p>
<br>
<p>Then do this for the rest of the Interfaces as shown below</p>
<p align="center">
<img src="https://imgur.com/TPrHxpT.png" height="50%" width="40%" alt="VMware"/>
<p>For <b>OPT3</b> be sure to enable interface as shown below</p>
<p align="center">
<img src="https://imgur.com/bgSoKW5.png" height="50%" width="60%" alt="VMware"/>
<p>Back at <b>Interfaces Assignment</b> select <b>Bridges</b></p>
<br>
<p>Click <b>Add</b></p>
<br>
<p>Select <b>VictimNetwork</b> as the member interface.</p>
<p align="center">
<img src="https://imgur.com/azegOqX.png" height="50%" width="60%" alt="VMware"/>
<p>Then select <b>Display Advanced</b></p>
<br>
<p>Under <b>Advanced Configuration</b> for <b>SpanPort</b>, select "<b>SPANPORT</b>"</p>
<br>
<p>Scroll all the way down and click <b>Save</b></p>
<br>
<p>Click Firewall >> Rules</p>
<br>
<p>Select the <b>Add</b> button with the arrow pointed downward</p>
<br>
<p>~ Under "Edit Firewall Rule" for Protocol select <b>Any</b></p>
<br>
<p>~ Scroll all the way down and <b>SAVE</b></p>
<p align="center">
<img src="https://imgur.com/e4YqjTp.png" height-"50%" width="65%" alt="VMware"/>
<p>This is the majority of the firewall configuration needed for pfsense.</p>
<br>
<p><b>Configuring Windows Server as a Domain Controller</b></p>
<br>
<p>The goal of this portion of the lab is to set up an Active Directory domain with a Windows 2019 server as the Domain Controller and 2 Windows 10 machines. This portion of the lab is very easy to set up and I'll be using <a href="https://www.youtube.com/watch?v=xftEuVQ7kY0">The Cyber Mentor's youtube guide</a> for an Active Directory Hacking Lab.</p>
<br>
<a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019">Dowload the Windows 2019 Server Evaluation Copy</a>
<br>
<br>
<a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise">Dowload the Windows 10 Evaluation Copy</a>
<br>
<br>
<p>~ Important Details for Windows Server Installation</p>
<br>
<p>(Please read below before installing the Windows Server on VMware)</p>
<br>
<p>*Install in VMware as usual with defaults</p>
<br>
<p>*Do not worry about a product key, simply click <b>Next</b></p>
<br>
<p>*At the end of the installation, be sure to change the Network Adapter to <b>Vmnet3</b></p>
<br>
<p>*<b>Make sure to UNCHECK "</b>Power on this virtual machine after creation.<b>"</b></p>
<br>
<p>*After the VM has been installed, click "Edit virtual machine settings" and remove the Floppy drive.</p>
<br>
<p>Power on the Virtual Machine and immediately click any key.</p>
<br>
<p>Click <b>Next</b></p>
<br>
<p>Click <b>Install Now</b></p>
<p align="center">
<img src="https://imgur.com/FHdfXHK.png" height="50%" width="50%" alt="VMware"/>
<p>Select the <b>Windows Server 2019 standard Evaluation (Desktop Experience)</b></p>
<br>
<p>Accept the License Terms</p>
<br>
<p>Click <b>Next</b></p>
<br>
<p>Select the <b>Custom Install</b></p>
<p align="center">
<img src="https://imgur.com/RU6Js6Q.png" height="50%" width="50%" alt="VMware"/>
<p>Click <b>New</b></p>
<br>
<p>Click <b>Apply</b></p>
<br>
<p>Click <b>OK</b></p>
<br>
<p>Click <b>Next</b></p>
<br>
<p>You should have this screen now</p>
<p align="center">
<img src="https://imgur.com/Uu4GuMo.png" height="50%" width="60%" alt="VMware"/>
<p>Create password</p>
<br>
<p>After the installation, you should end up with this screen</p>
<p align="center">
<img src="https://imgur.com/cPX2vs1.png" height="50%" width="40%" alt="VMware"/>
<p>Rename the Domain Controller</p>
<br>
<p>~ Navigate to Settings in the search bar</p>
<br>
<p>~ Search for settings in the search bar</p>
<br>
<p>~ Search for "pc name" in the settings search</p>
<br>
<p>~ Select Rename PC and rename the PC your choice name</p>
<p align="center">
<img src="https://imgur.com/6QbXeOd.png" height="50%" width="50%" alt="VMware"/>
<p>~ Select Restart now</p>
<br>
<p>After the reboot, on the Server Manager Dashboard, click Manage >> Add Roles and Features</p>
<p align="center">
<img src="https://imgur.com/f4fbHvD.png" height="50%" width="60%" alt="VMware"/>
<p>Keep clicking <b>Next</b> until you get to <b>Server Roles</b menu></p>
<br>
<p>Select <b>Active Directory Domain Services</b></p>
<br>
<p>Select "<b>Add Features</b>"</p>
<p align="center">
<img src="https://imgur.com/RbVWmZ8.png" height="50%" width="50%" alt="VMware"/>
<p>Click on <b>Next</b> until you get to the Confirmation menu, then click <b>Install</b></p>
<br>
<p>After the install, click <b>Close</b></p>
<br>
<p>Click on the flag with the yellow caution triangle</p>
<p align="center">
<img src="https://imgur.com/fHMrjTr.png" height="50%" width="60%" alt="VMware"/>
<p>*Select "<b>Promote this server to a domain controller</b>"</p>
<br>
<p>*Select <b>Add a new forest</b></p>
<br>
<p>*Specify a domain name</p>
<br>
<p>*Click <b>Next</b></p>
<br>
<p>*Set a password</p>
<p align="center">
<img src="https://imgur.com/X6tB600.png" height="50%" width="50%" alt="VMware"/>
<p>Click <b>Next</b> to get to the <b>Prerequisites Check</b> Menu</p>
<br>
<p>Click <b>Install</b></p>
<br>
<p><b>Wait for reboot</b></p>
<br>
<p>After the reboot, log back in</p>
<br>
<p>Select Manage >> Add Roles & Features again on the Server Manager</p>
<br>
<p>Click <b>Next</b> until you get to <b>Server Roles</b></p>
<p align="center">
<img src="https://imgur.com/xAJxA6i.png" height="50%" width="50%" alt="VMware"/>
<p>Select <b>Active Directory Certificate Services</b></p>
<br>
<p>Select <b>Add Features</b></p>
<br>
<p>Click <b>Next</b> until you get to the "<b>Confirmation</b>" menu</p>
<br>
<p>Check "<b>Restart the destination server automatically if required</b>"</p>
<br>
<p>Select <b>Yes</b></p>
<br>
<p>Select <b>Install</b></p>
<br>
<p>After the installation, Click <b>Close</b></p>
<p align="center">
<img src="https://imgur.com/xfpXGZq.png" height="50%" width="60%" alt="VMware"/>
<p>Click on the flag with the yellow caution triangle</p>
<p>Select "<b>Configure Active Directory Certificate Services on the destination server</b>"</p>
<p align="center">
<img src="https://imgur.com/fHMrjTr.png" height="50%" width="60%" alt="VMware"/>
<p>Click <b>Next</b> on <b>Credentials</b></p>
<br>
<p>On the <b>Role Services</b> menu, check <b>Certification Authority</b></p>
<p align="center">
<img src="https://imgur.com/hLQI7wF.png" height="50%" width="40%" alt="VMware"/>
<p>Click <b>Next</b> until you get to the <b>Validity period</b> menu and change it to <b>99</b> years</p>
<p align="center">
<img src="https://imgur.com/nYSKOao.png" height="50%" width="40%" alt="VMware"/>
<p>Click <b>Next</b> until you get to the <b>Confirmation</b> menu</p>
<br>
<p>Then select <b>Configure</b></p>
<br>
<p>Manually restart the server in order for all the settings to take effect.</p>
<br>
<p>Now add some Users:</p>
<br>
<p>~ Back at the Server Manager Select <b>Tools</b> > <b>Active Directory Users and Computers</b></p>
<p align="center">
<img src="https://imgur.com/R43PcsT.png" height="50%" width="40%" alt="VMware"/>
<p>Select your <b>Domain Name (CYBERWOX.local)</b>><b>Users</b>, Right Click & Select <b>New</b>><b>User</b></p>
<br>
<p>~ Enter a First, Last & User logon name for the user (Disregard the "WIN10" and just set a preferred logon name).</p>
<p align="center">
<img src="https://imgur.com/Ym7fejh.png" height="50%" width="40%" alt="VMware"/>
<p>Set a new password that never expires. Select <b>Finish</b>.</p>
<p align="center">
<img src="https://imgur.com/wtrBvKp.png" height="50%" width="40%" alt="VMware"/>
<p>Right Click on the previous user you created, Select Copy, and create another user.</p>
<br>
<p>Disregard the "<b>WIN7</b>" and set a preferred logon name.</p>
<br>
<p>After this, add a password that never expires.</p>
<br>
<p>Search for "<b>Windows Defender Firewall</b>" > <b>Turn Windows Defender Firewall on or off</b>.</p>
<br>
<p>Turn off the firewall for all Networks</p>
<p align="center">
<img src="https://imgur.com/UrByb7f.png" height="50%" width="40%" alt="VMware"/>
<p>Now use pfsense as the default gateway for the Domain Controller</p>
<br>
<p>~ Navigate to <b>Control Panel</b> > <b>Network and Internet</b> > <b>Network Connections</b></p>
<br>
<p>~ Enter the following configuration</p>
<p align="center">
<img src="https://imgur.com/TwSedG8.png" height="50%" width="60%" alt="VMware"/>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
