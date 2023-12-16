<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we analyze network traffic encompassing ICMP, SSH, HTTP/S, DNS, and RDP protocols using Azure Virtual Machines and Wireshark. Furthermore, we explore the experimentation of adding an Inbound rule to Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com/watch?v=O3ISo0YCi5Q))

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Languages</h2>

- Powershell or Command Prompt

<h2>Actions and Observations</h2>
<p>
1. Log in to your Microsoft Azure Portal and enter "resource groups" in the search bar.
</p>
<p>
  
  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4c250aab-d539-4c24-b585-71a745a4e604)
</p>
<p>2. Click "Resource groups," then click the plus sign to create a resource group.</p>

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8cbb8498-cb27-4417-a85f-f3612a6152fa)
</p>


<p>
3. Enter a name for the resource group, select a region, and click "Review + create" (e.g., "Network-Lab" and "US West US 3").
</p>

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8d836566-ad04-4815-b48a-f1b741080e45)
</p>


<p>
4. After the resource group is created, search for "virtual machines" in the search bar.
</p>

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/82455546-218c-48ef-b58e-9be39ad0aef9)
</p>


<p>
5. Click "Virtual machines," click the plus sign, and select "Create a virtual machine hosted by Azure."
</p>

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f7bbbf29-729a-4c55-88d1-55968ec8ce86)
</p>


<p>
6. Select the resource group created in step 3, enter a name for the virtual machine (e.g., "VM1"), choose the same region as the resource group (e.g., "US West US 3"). 
</p>

<p>

  ![2023-11-05_16-24-31](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/ec2f613b-8b2e-40aa-976d-7e36a9b4fc3c)
</p>

<p>
7. Select "Windows 10 Pro version 22H2 - x64 Gen2" for the image, and choose "Standard_E_2s_v3 - 2 vCPUs 16 GiB memory" for the size. Create a username and password (e.g., "labuser" and "Password1234").
</p>

<p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b3b44d8e-3c90-473d-ab93-427dd1dc2e27)
</p>


<p>
8. Click "I confirm," then "Review + create," and once validation passes, click "Create."
</p>

<p>

  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/57312900-f4c5-4b67-a339-f9a82e6f51eb)
  ![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b33c73fd-8b46-47a2-88d3-67fa705d7e01)
</p>


<p>
9. Create another virtual machine (e.g., "VM2") following similar steps as in step 6, but select "Ubuntu Server 20.04 LTS - x64 Gen2" for the image.
</p>

<p>
10. Select Ubuntu Server 20.04 LTS - x64 Gen2 for the image and select Standard_E_2s_v3 - 2 vcpus 16 GiB memory for the size.
</p>

![2023-11-05_16-51-36](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/b73f1e81-f2ee-410a-bb3d-a544357754fc)

<p>
 11. For authentication type, select "password" and create a username and password (you can use the same credentials as in step 8).
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/73966a9e-4de3-44fe-b6ec-624e24836123)


<p>
12. Go to the networking screen and verify that VM2 will be on the same virtual network as VM1.(Azure already created a virtual network for VM1 and now that we created VM2 in the same reource group it will also use the same virtual netowrk as VM1. Azure has created VM1-vnet for my virtual network)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/309eb96b-b178-474d-9cb7-0da9c521a819)


<p>
13. Click "Review + create," and once validation passes, click "Create" to build VM2.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/44bfd1d6-3f6a-4ed9-ace4-34e7052f1ccd)


<p>
14. Now that we have two virtual machines VM1 and VM2 we will use microsoft remote desktop to access VM1. Retrieve the public IP address for VM1. This can be found by going to Virtual machines, clicking on VM1, and Public IP address is right under size. (Download Microsoft Remote desktop if using MAC)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f43b9191-dd51-4890-89fc-d695e99544ed)


<p>
15. Use Microsoft Remote Desktop to access VM1 by entering its public IP address.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/6460d0aa-949a-45e8-a6d6-41efd3adf457)
![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/e95fda3c-1886-4a3b-a7df-b1db16d4441e)


<p>
16. Double click on the box that shows the public IP address for VM1 and input the username and password for VM1. You are now in VM1
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/8a998e46-2a17-4f27-90e3-b7260df1ee94)

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/424d077e-b0e4-4156-bbdd-bcc8fef56ac9)


<p>
17. Open Microsoft Edge, go to google.com, search for "download Wireshark," and click on the first link.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/df0eff56-b8f7-4ba4-960b-d1dce45bf309)


<p>
 18. Click "Windows x64 Installer" to download Wireshark.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/84ac522b-f461-4a3e-a12d-4db31d098853)


<p>
 19. Open the Wireshark Installer, proceed by clicking "Next" (leave every option at the default setting), and click "Install" until you reach the final screen showing "Finish."
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/d51d62d8-0270-4554-8a01-99f341466688)


<p>
 20. Open Wireshark, click "Ethernet," and click the blue icon in the top left to start capturing packets. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f1e6d21f-7895-47c3-86a2-363a60a1323b)

<h3>ICMP</h3> 
<p>
 21. There will be alot of traffic showing because there is so much running in the background. Type "ICMP" in the "Apply a display filter" box and press Enter.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4ebe27e3-1cd7-45a1-b78d-da65b0171568)

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/faca18dc-d4c4-4f77-b3e8-e3a9e680d49f)


<p>
 22. Notice the traffic has stopped; ICMP is the protocol used by ping. 
</p>

<p>
 23. Go to your Azure portal, access VM2, and copy its Private IP address (e.g., 10.0.0.5).
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/92bf187a-ff82-4224-9f37-36702a491e2b)


<p>
24. Return to VM1, open Windows Powershell or Command Prompt, and type "ping" followed by the private IP address of VM2.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/89440f12-0fd0-4d43-aa49-e75ebfd09349)

<p>
 25. Type in ping and the private IP address (10.0.0.5) of VM2 and press enter. You should now see the traffic that occurred between VM1 and VM2 on Wireshark.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a19fd72e-90de-4bb3-a32f-c63b5e1f7c09)

(Windows Powershell shows that four packets were sent to VM2 (10.0.0.5) and four packets were received. Wireshark shows requests that were sent out to 10.0.0.5 (VM2) and replies were sent back to 10.0.0.4 (VM1).

<p>
 26. Type "ping 10.0.0.5 -t" to send a continuous ping to VM2. Modify the firewall to block inbound traffic to VM2. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/50b562a7-49de-4fcd-b667-8573a4488622)


<p>
27. Go back to the Azure portal and search for "network security groups."
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3fa8a8de-7489-4b4e-9bcc-d9222c2df35b)


<p>
28. Click on "VM2-nsg," select "Inbound security rules," and click the plus sign to add a rule. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/813130a1-4653-47d4-80c1-5c8735b2637b)


<p>
29. Set the rule to deny ICMP traffic with a priority of 200 (e.g., "Deny_ICMP_from_anywhere").
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/7715c66e-f427-443b-a559-323fb390a0ee)


<p>
30. Refresh and return to VM1; ping requests to VM2 should time out. This is because the new rule that was added in now blocking all ping request. Wireshark will also just show request being sent, but won't show any replies. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a39e4aab-4ed1-4c5e-b508-ba1cf291afd3)


<p>
31. Delete or modify the rule to allow ICMP and refresh again; ping requests should work.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/91bfeb5a-4484-4b9c-98bf-d17c55043ac5)

<h3>SSH</h3>
<p>
32. Clear Wireshark and change the filter to "ssh." Connect to VM2 using ssh.
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/62cbc74c-44c6-4a55-a099-703b6a0d4aa0)


<p>
33. Connect to VM2 using SSH by typing "ssh labuser@10.0.0.5" (use your VM2 username and IP address).
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/a7f3c960-3c47-4055-ada6-d42113669169)


<p>
34. Enter "yes" to confirm connecting and input the password for VM2. There should receive a meesage thats says you're connnected to VM2. 
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3bd3f24c-1c53-419b-9fdc-478d297de58b)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/2cfd6e0d-0f8b-4ccc-a33e-895612427f32)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/98a184e9-82bd-4d96-bd65-5d7d138daea8)



<p>
35. Observe SSH traffic in Wireshark.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/0928ac7d-b545-4463-a436-e03f7e6a0cf0)

<h3>DHCP</h3>
<p>
36. Clear Wireshark again and change the filter to "dhcp."
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/6fe8997b-fdd7-4145-b2a8-fb3720cf9b5f)


<p>
37. Type "ipconfig /renew" in the Windows Powershell of VM1 to renew the IP address and observe DHCP traffic.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/3d9b521e-9145-4636-b157-df2da53ed34d)


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/9a02b62e-a52c-49cf-8ddb-e4caba8e2e20)


<h3>DNS</h3>
<p>
38. Clear Wireshark and change the filter to "dns". Type "nslookup www.disney.com" (or any website) in Windows Powershell.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/367e4486-0cd5-4ffa-8790-2b40c6415213)

<p>
39. Type "nslookup www.disney.com" (or any website) in Windows Powershell. Observe DNS traffic in Wireshark.
</p>


![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/becd9f91-c94c-42a4-9a04-2d57fe6906f4)

<h3>RDP</h3>
<p>
40. Clear Wireshark, change the filter to "tcp.port == 3389".
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/f8689968-763b-4b60-bb67-db40c76bc6ba)

<p>
41. Observe RDP traffic in Wireshark. (As we utilize Remote Desktop on VM1, expect a significant amount of traffic to appear on Wireshark.)
</p>

![image](https://github.com/Gleejr/Azure-network-protocols/assets/148407820/4122c6f8-a365-45ef-82fc-87c1393891ee)

