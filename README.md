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
</ol>



        
<h2>Step 4: Implement Access Control Policies </h2>
<ol>
   <li>Define User Roles: Assign specific roles to users based on their function in the lab.</li>
   <ul>
      <li>Administrators: Full access to all VMs, Active Directory management, and Splunk configurations.</li>
   </ul>
   <ul>
      <li>Standard Users: Limited access to specific Windows or Linux machines for testing and learning purposes.</li>
   </ul>
   <ul>
      <li>Guests: Minimal access, primarily for observing system activity without making changes.</li>
   </ul>
   <ul>
      <br></br>
      <li>Create groups for specific roles (e.g., admin, user, guest) by running the following code:</li>
   </ul>
   <img src="https://i.imgur.com/RXI5kjZ.png" height="30%" width="30%" alt="script"/>
   <br/>
   <li>Assign Permissions to Groups</li>
   </ul>
   <ul>
      <li>Use the chmod and chown commands to set directory permissions.</li>
   </ul>
   <img src="https://i.imgur.com/9c335UK.png" height="30%" width="30%" alt="script"/>
   <li>Enforce Access Control</li>
   <ul>
      <li>Verify permissions by switching to different users and testing to see if you can access the created directories.</li>
   </ul>
   <img src="https://i.imgur.com/pY3M8ON.png" height="30%" width="30%" alt="script"/>
</ol>
<h2>Step 5: Automate Password Policies </h2>
<ol>
   <li>Password Policy: Configure strong password requirements on all systems</li>
   <ul>
      <li>Minimum length: 12 characters.</li>
   </ul>
   <ul>
      <li>Must include uppercase, lowercase, numbers, and special characters.</li>
   </ul>
   <ul>
      <li>Prevent the reuse of the last five passwords.</li>
   </ul>
   <ul>
      <li>Implement password expiration policies: Set passwords to expire every 60 days on all machines (via Group Policy for Windows and /etc/login.defs for Linux).</li>
   </ul>
   <li>Password Requirements</li>
   <ul>
      <li>Modify /etc/login.defs for system-wide policies by running the following:</li>
      <img src="https://i.imgur.com/u0ywtmF.png" height="40%" width="40%" alt="script"/>
      <br/>
   </ul>
   <ul>
      <li>Set these parameters:
         <br/>
      </li>
      <ul>
         <li>PASS_MAX_DAYS: Sets the maximum number of days a user can use their current password before being required to change it.</li>
      </ul>
      <ul>
         <li>PASS_MIN_DAYS: Defines the minimum number of days a user must wait before they can change their password again after setting it.</li>
      </ul>
      <ul>
         <li>PASS_MIN_LEN: Sets the minimum length for user passwords to 12 characters.</li>
      </ul>
      <ul>
         <li>PASS_WARN_AGE: Sends a warning to the user 7 days before their password is set to expire.</li>
      </ul>
      <img src="https://i.imgur.com/lhys6XV.png" height="25%" width="25%" alt="script"/>
   </ul>
   <li>Implement Account Lockout:</li>
   <ul>
      <li>Edit /etc/pam.d/common-auth to lock accounts after three failed login attempts by running the following:</li>
      <img src="https://i.imgur.com/mdQCxCn.png" height="25%" width="25%" alt="script"/>
      <br/>
      <ul>
         <li>Add the following line of code:</li>
         <img src="https://i.imgur.com/nsauMaI.png" height="40%" width="40%" alt="script"/>
         <br/>
         <li>auth required pam_tally2.so: Specifies the use of the pam_tally2 module, which keeps a tally of failed login attempts for user accounts.
         <li>deny = 3: Sets a limit of 3 failed login attempts before the account is locked.</li>
         <li>unlock_time=600: Configures the lockout period to 600 seconds (10 minutes). After this time, the account is automatically unlocked.</li>
         <li>onerr=fail: Ensures that if there’s an error in the PAM module, access is denied by default.</li>
         <li>audit: Enables logging of authentication attempts, including both successful and failed logins.</li>
         </li>
      </ul>
   </ul>
</ol>

<h2>Step 6: Monitor User Activity </h2>
<ol>
   <li>Enable Audit Logging</li>
   <ul>
      <li>Install auditd:</li>
   </ul>
   <br/>
   <img src="https://i.imgur.com/tBsG67J.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Start and enable the service:</li>
   <img src="https://i.imgur.com/TWlGzOR.png" height="40%" width="40%" alt="script"/>
   <br/>
   <li>Define Audit Rules</li>
   <img src="https://i.imgur.com/y0pv2di.png" height="40%" width="40%" alt="script" "/>
   <br/>
   </li></ul>
   <h2>Step 7: Conclusion</h2>
 In this project, I developed an automated user management solution for Linux, covering onboarding, access control, and offboarding. I created a Bash script to automate account creation with secure default settings, restricted SSH access based on roles, and implemented group-based access controls. The project also includes login monitoring for proactive security and regular user access reviews, ensuring that only authorized users have access. This demonstrates my skills in Linux administration, automation, and security, showcasing essential competencies for a System Administrator role.     
</ol>
