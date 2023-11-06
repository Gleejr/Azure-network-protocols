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

(Windows Powershell shows that four packets were sent to VM2 (10.0.0.5) and four packets were received. Wireshark shows requests that were sent out to 10.0.0.5 (VM2) and replies were sent back to 10.0.0.4 (VM1).

<p>
 25. Next type in ping 10.0.0.5 -t to send a continuous ping to VM2. I will now change the firewall to block inbound traffic coming to VM2.  
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/50b562a7-49de-4fcd-b667-8573a4488622)


<p>
26. Go back to the Azure portal and type in network security groups.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3fa8a8de-7489-4b4e-9bcc-d9222c2df35b)


<p>
 27. Click on VM2-nsg, click on inbound security rules, and click the plus sign to add a rule. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/813130a1-4653-47d4-80c1-5c8735b2637b)


<p>
28. Under protocol select ICMP, under action select deny, under priority change thenumber to 200, input a name (I enteter the name Deny_ICMP_from_anywhere), and click add.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/7715c66e-f427-443b-a559-323fb390a0ee)


<p>
29. Click refresh and go back to VM1. The ping request should now be timing out (message will say "Request timed out"). This is because the new rule that was added in now blocking all ping request. Wireshark will also just show request being sent, but won't show any replies. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a39e4aab-4ed1-4c5e-b508-ba1cf291afd3)


<p>
30. To fix this delete the rule that was created or edit the rule to allow ICMP. Save the change and click refresh again. ICMP ping request should now be receving replies again,
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/91bfeb5a-4484-4b9c-98bf-d17c55043ac5)


<p>
31. Clear wireshark by clicking the green icon and select continue without saving. Next change the filter to ssh and click enter. Next we will connect to VM2 using SSH.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/62cbc74c-44c6-4a55-a099-703b6a0d4aa0)


<p>
32. Next type in ssh, the username for your VM2, the "@" sign, the Private IP address for VM2, and press enter. (it should look like this ssh @labuser10.0.0.5)
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a7f3c960-3c47-4055-ada6-d42113669169)


<p>
 33. Enter yes for "Are you sure you want to continue connecting", input the password for VM2 (my password is Password1234), press enter and you should receive a meesage thats says you're connnected to VM2. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3bd3f24c-1c53-419b-9fdc-478d297de58b)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/2cfd6e0d-0f8b-4ccc-a33e-895612427f32)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/98a184e9-82bd-4d96-bd65-5d7d138daea8)



<p>
34. Since the filter was set for ssh, Wireshark shows the traffic of connecting VM1 to VM2 using ssh.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/0928ac7d-b545-4463-a436-e03f7e6a0cf0)


<p>
35. Next I will observe DHCP traffic. I will clear Wireshark and change the filter to dhcp.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/6fe8997b-fdd7-4145-b2a8-fb3720cf9b5f)


<p>
36. Type in ipconfig /renew, this command will reassign the IP address to VM1 and show the traffic on Wireshark.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3d9b521e-9145-4636-b157-df2da53ed34d)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/9a02b62e-a52c-49cf-8ddb-e4caba8e2e20)


<p>
37. Next I will observe DNS traffic. I will clear Wireshark and change the filter to dns.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/367e4486-0cd5-4ffa-8790-2b40c6415213)

<p>
38. Type in nslookup www.disney.com (it can be any website) and click enter. The traffic will appear on wireshark.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/becd9f91-c94c-42a4-9a04-2d57fe6906f4)


<p>
39. Next I will observe RDP traffic. I will clear Wireshark and change the filter to tcp.port == 3389.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f8689968-763b-4b60-bb67-db40c76bc6ba)

<p>
40. Since I am actively using remote desktop to use VM1 there is alot traffic that will appear on Wireshark.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4122c6f8-a365-45ef-82fc-87c1393891ee)

