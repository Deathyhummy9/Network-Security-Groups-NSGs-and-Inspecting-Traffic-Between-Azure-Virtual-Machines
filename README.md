<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Virtual Machines
- Observe ICMP Traffic
- Configuring a Firewall (Network Security Group)
- observe traffic (DNS,DHCP,RDP,SSH)

<h2>Actions and Observations</h2>

<p>
<img width="1929" height="889" alt="Screenshot (95)" src="https://github.com/user-attachments/assets/a936a77c-7d86-485d-896a-592581a221c4" />

</p>
<p>
Start by creating an azure resource group to allocate both virtual machines in for this labs after create a windows 10 Vm and create a new virtual net work to but both virtual machines(for lab we will just name ours lab)
</p>
<br />

<p>
<img width="1917" height="903" alt="Screenshot (97)" src="https://github.com/user-attachments/assets/b71aa31c-20c9-4dac-ad3e-e356a7302e5e" />

</p>
<p>
Create a linux ubuntu Vm and make sure its under the extract same resource group and virtual network  the resource group should look like the photo above 

</p>
<br />

<p>
<img width="1641" height="1014" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/3a096d2b-eae4-40c7-b7c6-e5c874313b86" />

</p>
<p>
First log into the windows VM search up wireshark and install the 64x version install wireshark and it should look like this when installed 

<p>
<img width="1685" height="1046" alt="Screenshot (98)" src="https://github.com/user-attachments/assets/f7b3e901-fcf5-4414-a191-6727d93c84b5" />

</p>
<p>
Within wire shark filter for icmp only and retrieve the Private ip address for the linux VM and attempt to ping it from the windows 10 VM it should look like this 


<p>
<img width="1661" height="987" alt="Screenshot (100)" src="https://github.com/user-attachments/assets/c6d19d3a-c2e7-4bd0-a19f-53416c59a968" />

<img width="1654" height="988" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/de3467bf-8f17-4705-a15e-f9e1c3074250" />

</p>
<p>
Log back into ut windows vm and go into wire shark  start up the packet capture again and filter for SSH only this time   Open PowerShell, and type: ssh labuser@<private IP address>  and fully connect into the ssh tunnel see th different on how all messages u send are encrypted and hashed play around with it by send all sorts of messages and observing the response and then exit it by typing exit and then enter 



<p>
<img width="1599" height="1043" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/7ed3f9cf-c177-4c7b-851a-41cda1ee5530" />

</p>
<p>
First filter to dhcp traffic to see So to observe dchp we open powershell and run ipconfig /release and then ipconfig/renew observer how the dhcp traffic is being tracked in wireshark take note at what the coumptuers are sending to each other





<p>
\<img width="1670" height="989" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/3cb714fc-818b-4710-ad27-784a67198953" />

</p>
<p>
Filter for dns so we can observe that next  from the powershell command line use nslook up to see different ip addresses like google  now the ip address wont work to go to the website but observe the different activity that flows through wire shark



<p>
<img width="1667" height="979" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/b91ac998-d131-4b14-bf05-128827924553" />

</p>
<p>
Head back to the azure cloud interface for linux vm  and add a new fire wall configuration rule that denys pings and make it priority access watch how the pinging starts returning that it never got the ack signal and watch how it goes back once u delete the rule



<p>
<img width="1655" height="989" alt="Screenshot (105)" src="https://github.com/user-attachments/assets/1a83e330-3250-4e41-a863-be537ebe1454" />

</p>
<p>
Next we will filter for rdp   rdp is unique since it is used to track remote desktop activity and its perfect for our test cause thats what we are using  see how it tracks everything from the move of a mouse to opening a page its like a live feed
