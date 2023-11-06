<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com/watch?v=O3ISo0YCi5Q))

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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>
<p>
1. Login to your Microsoft Azure Portal and type in resource groups in the search bar.
</p>
<p>
  
  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4c250aab-d539-4c24-b585-71a745a4e604)
</p>
<p>2. Click resource group and then click the plus sign to create a resource group.
</p>
<br />
<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8cbb8498-cb27-4417-a85f-f3612a6152fa)
</p>


<p>
3. Input a name for the resource group, select a region, then click Review + create (I have named my resouce group Network-Lab and the region is (US) West US 3) 
</p>
<br />

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8d836566-ad04-4815-b48a-f1b741080e45)
</p>


<p>
4. Once the resource group has finished being created, search for virtual machines in the search bar.
</p>
<br />

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/82455546-218c-48ef-b58e-9be39ad0aef9)

</p>


<p>
5. Click virtual machines, click the plus sign, and next click "Create a virtual machine hosted by Azure"
</p>
<br />

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f7bbbf29-729a-4c55-88d1-55968ec8ce86)
</p>


<p>
6. Select the resource group that was created in step 3, input a name for the virtual machine (I have enetered VM1), Select the region for this virtual machine (I have selected the same region for my resource group (US) West US 3)
</p>
<br />

<p>

  ![2023-11-05_16-24-31](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/ec2f613b-8b2e-40aa-976d-7e36a9b4fc3c)

</p>

<p>
7. Select Windows 10 Pro version 22H2 - x64 Gen2 for the image, select Standard_E_2s_v3 - 2 vcpus 16 GiB memory for the size, and create a username and password (labuser is th username I created and the password is Password1234)
</p>
<br />

<p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b3b44d8e-3c90-473d-ab93-427dd1dc2e27)
</p>


<p>
8. Click "I confirm" at the bottom, click review + create, and once validation passes click create.
</p>
<br />

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/57312900-f4c5-4b67-a339-f9a82e6f51eb)
  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b33c73fd-8b46-47a2-88d3-67fa705d7e01)
</p>


<p>
9. Navigate back to virutal machines to create another virtual machine. Repeat Step 6 but do not create another windows machine and select a new name for this virtual machine. (I have named this virtual machine VM2, it will be running Ubuntu)
</p>

<p>
10. Select Ubuntu Server 20.04 LTS - x64 Gen2 for the image and select Standard_E_2s_v3 - 2 vcpus 16 GiB memory for the size.
</p>

![2023-11-05_16-51-36](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b73f1e81-f2ee-410a-bb3d-a544357754fc)

<p>
 11. For authentication type select password and create a username and password. (I used the same username and password for VM1)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/73966a9e-4de3-44fe-b6ec-624e24836123)


<p>
12. Click next twice at the bottom to get to the Networking screen. It will show that the VM2 will be on the same virtual network as VM1. (Azure already created a virtual network for VM1 and now that we created VM2 in the same reource group it will also use the same virtual netowrk as VM1. Azure has created VM1-vnet for my virtual network)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/309eb96b-b178-474d-9cb7-0da9c521a819)


<p>
13. Click review + create and once validation has passed click create again to build VM2. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/44bfd1d6-3f6a-4ed9-ace4-34e7052f1ccd)


<p>
14. Now that we have two virtual machines VM1 and VM2 we will use microsoft remote desktop to access VM1. Grab the the public IP address for VM1. This can be found by going to Virtual machines, clicking on VM1, and Public IP address is right under size. (I'm using a macbook. I downloaded Microsoft Remote desktop)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f43b9191-dd51-4890-89fc-d695e99544ed)


<p>
15. Start up Microsoft Remote desktop, click add PC, input the public IP address for VM1, and click add.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/6460d0aa-949a-45e8-a6d6-41efd3adf457)
![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/e95fda3c-1886-4a3b-a7df-b1db16d4441e)


<p>
16. Double click on the box that shows the public IP address for VM1 and input the username and password for VM1. You are now in VM1
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8a998e46-2a17-4f27-90e3-b7260df1ee94)

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/424d077e-b0e4-4156-bbdd-bcc8fef56ac9)


<p>
17. Open Microsoft Edge and go to google.com, type in the search bar download Wireshark, and click on the first link.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/df0eff56-b8f7-4ba4-960b-d1dce45bf309)


<p>
 18. Click on Windows x64 Installer and Wireshark will start to download.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/84ac522b-f461-4a3e-a12d-4db31d098853)


<p>
 19. Open the Wireshark Installer, keep clicking next (leave every option to the default setting), and click install until you get to the last screen that shows finish.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/d51d62d8-0270-4554-8a01-99f341466688)


<p>
 20. Open wireshark, click ethernet, and click the blue icon in the top left. (when you hover over the icon it should say "start capturing packets")   
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f1e6d21f-7895-47c3-86a2-363a60a1323b)


<p>
 21. There will be alot of traffic showing because there is so much running in the background. Type in ICMP where it says "apply a display filter" and press enter.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4ebe27e3-1cd7-45a1-b78d-da65b0171568)

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/faca18dc-d4c4-4f77-b3e8-e3a9e680d49f)


<p>
 22. Notice the traffic stopped. ICMP is the protocol that ping uses. I will now ping VM2 to view the traffic between VM1 and VM2.
</p>


<p>
 23. Go back to your azure portal, go into VM2, and copy the Private IP address for VM2 (The private IP address for my VM2 is 10.0.0.5)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/92bf187a-ff82-4224-9f37-36702a491e2b)


<p>
23. Go back into VM1 and open Windows Powershell.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/89440f12-0fd0-4d43-aa49-e75ebfd09349)

<p>
 24. Type in ping and the private IP address (10.0.0.5) of VM2 and press enter. You should now see the traffic that occurred between VM1 and VM2 on Wireshark.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a19fd72e-90de-4bb3-a32f-c63b5e1f7c09)












