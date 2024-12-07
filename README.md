# Traffic Analysis on Azure Virtual Machines Using WireShark
<h2>Description</h2>
Description: In this project, we’ll set up Azure Virtual Machines to perform network traffic analysis using Wireshark. This setup will allow us to capture and analyze live network traffic in a cloud environment, helping to identify patterns, troubleshoot issues, and enhance security monitoring.

<h2>Environments, Technologies, and Operating Systems to be Used </h2>
<ol>
   <li>Microsoft Azure (Virtual Machines/Compute)</li>
   <li>Remote Desktop</li>
   <li>Go to the CentOS Website</li>
   <li>Various Command-Line Tools</li>
   <li>Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)</li>
   <li>Wireshark (Protocol Analyzer)</li>
   <li>Windows 10 (21H2)</li>
   <li>Ubuntu Server 20.04</li>
  
</ol>
<h2>Step 1: Create Our Resources </h2>
<ol>

  
   <li>Create a Resource Group</li>
   <ul>
      <li>Sign in to the Azure Portal.</li>
   </ul>
   <ul>
      <li>In the left-hand menu, click on "Resource Groups."</li>
   </ul>
   <ul>
      <li>Click "Add" to create a new Resource Group.</li>
   </ul>
   <ul>
      <li>Fill in the required details, including a unique name and your preferred region.</li>
   </ul>
   <ul>
      <li>Click "Review + create" and then "Create" to confirm.</li>
   </ul>

  
   <li>Create a Windows 10 Virtual Machine (VM)</li>
   <ul>
      <li>In the Azure Portal, click on "Create a resource" in the left-hand menu.</li>
   </ul>
   <ul>
      <li>Search for "Windows 10" and select the appropriate VM image.</li>
   </ul>
   <ul>
      <li>Click "Create" to start the VM creation process.</li>
   </ul>
   <ul>
      <li>Fill in the required details, such as VM name, region, and admin username and password./li>
   </ul>
     <ul>
      <li>Under the "Resource Group" section, select the Resource Group created earlier.</li>
   </ul>
     <ul>
      <li>For the Virtual Network (Vnet) and Subnet, let the VM create a new one.</li>
   </ul>
     <ul>
      <li>Complete the remaining VM configuration settings as needed.</li>
   </ul>
     <ul>
      <li>Click "Review + create" and then "Create" to confirm.</li>
   </ul>

   
 <li>Create a Linux (Ubuntu) VM</li>
   <ul>
      <li>In the Azure Portal, click on "Create a resource" in the left-hand menu.</li>
   </ul>
   <ul>
      <li>Search for "Ubuntu" and select the appropriate VM image.</li>
   </ul>
   <ul>
      <li>Click "Create" to start the VM creation process.</li>
   </ul>
   <ul>
      <li>Fill in the required details, such as VM name, region, and admin username and password./li>
   </ul>
     <ul>
      <li>Under the "Resource Group" section, select the Resource Group created earlier.</li>
   </ul>
     <ul>
      <li>For the Virtual Network (Vnet) and Subnet, select the one created while setting up the Windows 10 VM.</li>
   </ul>
     <ul>
      <li>Complete the remaining VM configuration settings as needed.</li>
   </ul>
     <ul>
      <li>Click "Review + create" and then "Create" to confirm.</li>
   </ul>


 <li>Observe Your Virtual Network within Network Watcher</li>
   <ul>
      <li>In the Azure Portal, click on "Network Watcher" in the left-hand menu.</li>
   </ul>
   <ul>
      <li>Select the Virtual Network you created earlier.</li>
   </ul>
   <ul>
      <li>Observe the details of your Virtual Network, including the connected VMs and subnets.</li>
   </ul>
   <ul>
      <li>Add pic for reference</li>
   </ul>
   
</ol>
</ol>
<h2> Step 2: Observing ICMP Traffic </h2>
In this section, we will use Wireshark to observe ICMP traffic between the Windows 10 and Ubuntu VMs, and also between the Windows 10 VM and a public website. We will also demonstrate how Network Security Group rules can be used to control ICMP traffic.
<ol>
   <li>Connect to Windows 10 VM and Install Wireshark</li>
   <ul>
      <li>Use Remote Desktop to connect to your Windows 10 Virtual Machine.</li>
   </ul>
    <ul>
      <li>Within your Windows 10 Virtual Machine, download Wireshark from the official website: https://www.wireshark.org/#downloadLink </li>
   </ul>
    <ul>
      <li>Install Wireshark following the installation wizard instructions.</li>
   </ul>
   <li>Filter and Observe ICMP Traffic</li>
    <ul>
      <li>Open Wireshark and start a new capture.</li>
   </ul>
    <ul>
      <li>Set the filter to "icmp" to display only ICMP traffic.</li>
   </ul>
    <ul>
      <li>Retrieve the private IP address of the Ubuntu VM from the Azure Portal.</li>
   </ul>
    <ul>
      <li>Open Command Prompt or PowerShell in the Windows 10 VM and ping the Ubuntu VM using the command: 'ping <Ubuntu_VM_IP>'</li>
   </ul>
    <ul>
      <li>Observe the ping requests and replies within Wireshark.</li>
   </ul>
   <li>Ping a Public Website and Observe Traffic</li>
    <ul>
      <li>From the Windows 10 VM, attempt to ping a public website (e.g., www.amazon.com) using the command: ping www.amazon.com</li>
   </ul>
       <ul>
      <li>Observe the ICMP traffic between the Windows 10 VM and the public website in Wireshark.</li>
   </ul>
  <li>Control ICMP Traffic Using Network Security Group</li>
    <ul>
      <li>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM using the command: 'ping -t <Ubuntu_VM_IP>'</li>
   </ul>
    <ul>
      <li>In the Azure Portal, navigate to the Network Security Group (NSG) associated with your Ubuntu VM.</li>
   </ul>
    <ul>
      <li>Click on "Inbound security rules" in the left menu.</li>
   </ul>   
    <ul>
      <li>Click on the "+ Add" button in the top menu.</li>
   </ul> 
    <ul>
      <li>Configure the new rule as follows:</li>
      <ul><li>Source: Any</li></ul>
      <ul><li>Source Port Ranges: *</li></ul>
      <ul><li>Destination: Any</li></ul>
      <ul><li>Service: Custom</li></ul>
      <ul><li>Destination Port Ranges: *</li></ul>
      <ul><li>Protocol: ICMP</li></ul>
      <ul><li>Action: Deny</li></ul>
   </ul> 
    <ul>
      <li>Click "Add" to create the rule.</li>
    </ul>
   <ul>
      <li>Observe the ICMP traffic in Wireshark and the command line Ping activity, which should be interrupted due to the new rule.</li>
   </ul>
   <li>Re-enable ICMP Traffic and Observe the Result</li>
    <ul>
      <li>In the Azure Portal, navigate to the NSG associated with your Ubuntu VM.</li>
   </ul>  
   <ul>
      <li>Locate the ICMP rule you created earlier and delete it to re-enable ICMP traffic.</li>
   </ul>
   <ul>
      <li>Observe the ICMP traffic in Wireshark and the command line Ping activity, which should resume.</li>
   </ul>
    <li>Stop the Ping Activity</li>
    <ul>
      <li>In the Command Prompt or PowerShell, press Ctrl+C to stop the continuous ping activity.</li>
   </ul>  
</ol>



        
<h2>Step 4: Observing SSH Traffic </h2>
In this section, we will use Wireshark to observe SSH traffic between the Windows 10 and Ubuntu VMs. We will establish an SSH connection and execute commands within the Ubuntu VM, monitoring the SSH traffic in Wireshark.
<ol>
   <li>Filter for SSH Traffic in Wireshark</li>
   <ul>
      <li>In Wireshark, update the filter to "ssh" to display only SSH traffic.</li>
   </ul>
  <li>Establish an SSH Connection</li>
   <ul>
      <li>If you don't have an SSH client installed on your Windows 10 VM, download and install one such as PuTTY: https://www.putty.org/ </li>
   </ul>
   <ul>
      <li>Open the SSH client and enter the private IP address of your Ubuntu VM.</li>
   </ul>
   <ul>
      <li>Connect to the Ubuntu VM using the appropriate username and password.</li>
   </ul>
   <ul>
      <li>Observe the SSH traffic in Wireshark as the connection is established.</li>
   </ul>
   <img src="https://i.imgur.com/RXI5kjZ.png" height="30%" width="30%" alt="script"/>
   <br/>
   <li>Execute Commands and Observe SSH Traffic</li>
   </ul>
   <ul>
      <li>In the SSH session, type the following command and press [Enter]: ls -lasth</li>
   </ul>
   <ul>
      <li>Observe the SSH traffic in Wireshark.</li>
   </ul>
   <ul>
      <li>Type the following command and press [Enter]: touch hi.txt</li>
   </ul>
      <ul>
      <li>Observe the SSH traffic in Wireshark.</li>
   </ul>
   <li>Close the SSH Connection</li>
   <ul>
      <li>In the SSH session, type exit and press [Enter] to close the connection.</li>
   </ul>
    <ul>
      <li>Observe the SSH traffic in Wireshark as the connection is closed.</li>
   </ul>
</ol>
<h2>Step 5: Observing DNS Traffic </h2>
In this section, we will use Wireshark to observe DNS traffic within the Windows 10 VM. We will use the nslookup command to query the IP addresses of two websites and monitor the DNS traffic in Wireshark.
<ol>
   <li>Filter for DNS Traffic in Wireshark</li>
   <ul>
      <li>In Wireshark, update the filter to "dns" to display only DNS traffic.</li>
   </ul>
   <li>Query IP Addresses Using nslookup</li>
   <ul>
      <li>Open Command Prompt or PowerShell in the Windows 10 VM.</li>
   </ul>
   <ul>
      <li>Type the following command and press [Enter]: nslookup ufc.com</li>
   </ul>
   <ul>
      <li>Observe the DNS traffic in Wireshark as the IP address for ufc.com is resolved.</li>
   </ul>
</ol>

   <h2>Step 6: Conclusion</h2>
 Through this project, we successfully leveraged Wireshark on Azure VMs to monitor and analyze various types of network traffic, including RDP, DNS, DHCP, SSH, and ICMP. This hands-on setup provided valuable insights into common traffic patterns, allowing us to observe and understand these protocols in action, troubleshoot potential issues, and strengthen network security awareness in a cloud environment.     
</ol>
