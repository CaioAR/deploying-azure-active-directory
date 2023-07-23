<h1>Setting up Azure Active Directory</h1>
Deploying Azure Active Directory and create Users

<h2> Overview </h2>
This lab will explore Azure Active Directory, in it will provision virtual machines within the same subnet, install Active Directory on Windows Server, create a new Organizational Unit, manage Group Policy, link a client to our Server using DNS, and use Powershell to automate the creation of new users.
<br />
<br />

<h2>Process</h2>
We start by building a new Azure Virtual Network. When one is created, hidden services are automatically created, like DHCP and DNS.
<img src="https://imgur.com/UgpFaqY" alt="create virtual machine"/>

<img src="https://imgur.com/u6ke0n5" alt="create client" />

We can now take a look at Network Watcher > Topology in Azure Portal to ensure that both virtual machines are on the same subnet.
<img src="https://imgur.com/5RAu0Wz" alt="network watcher" />

At this point we want to change our domain controller's IP address from dynamic to static.
<img src="https://imgur.com/UaWkztS" alt="ipconfig" />
<img src="https://imgur.com/QX6B322" alt="edit ip configuration" />

At this point we'll allow DC-1 to use ICMP so we can ping it.
We'll connect to DC-1 using RDP.

<img src="https://imgur.com/JVKApZm" alt="windows defender firewall" />

Now we are able to ping our client virtual machine.
<img src="https://imgur.com/5kA34UA" alt="ping" />

<h2>Installing Active Directory</h2>
Now we will install and deploy Active Directory on our domain controller.
<img src="https://imgur.com/HqNApWm" alt="deployment of AD" />
<img src="https://imgur.com/QcnfHvJ" alt="Active Directory" />

We can now create an organizational unit for employees.
<img src="https://imgur.com/Ffm41Zy" alt="OU" />
<img src="https://imgur.com/cosPQrc" alt="employees" />

We can then create our first user
<img src="https://imgur.com/Ycb2LJm" alt="User creation" />
<img src="https://imgur.com/uS2Zudu" alt="first user" />

Once the profile has been established we will add it to the domain admin's OU.
<img src="https://imgur.com/HNQTBkZ" alt="domain admin" />
We can now log in with the new credentials.

<img src="https://imgur.com/qDG3KN6" alt="login for john-admin" />
Checking our command line we can see we're logged in as our new user.

<img src="https://imgur.com/miNo8qH" alt="john-admin command line" />
Now we'll joing our client to our domain controller.
We'll redirect its DNS settings to our domain controller so it's not searching throughout the internet for it and we'll set the DNS setting within Azure Portal.
<img src="https://imgur.com/TI5xBca" alt="DNS servers" />
<img src="https://imgur.com/e7A7JlW" alt="ipconfig" />
We can enter system settings to to change the name of the PC so it will have permission to join the domain.
<img src="https://imgur.com/iahK7pE" alt="domain changes" />
<img src="https://imgur.com/VbK1VIZ" alt="change name" />
And it works! Logging in with our changed name will show that your are now logging in as the new user joined into our domain.
<img src="https://imgur.com/cVw28WT" alt="domain changes" />
<img src="https://imgur.com/IY3QRUr" alt="login screen for john" />
<img src="https://imgur.com/eCqfYl1" alt="Active Directory Users and Computers" />
So normally, this would be done at scale with group policy, but in the interest of scope, we'll just be doing this with individual users.
<br />
Now on our client machine we'll add all of the domain users to RDP capabilities.
<img src="https://imgur.com/EkuXStB" alt="RDP" />
I have a powershell script to randomly assign names and create new users within our OU at scale that I'll run within Powershell ISE.
<img src="https://imgur.com/T0fg9MI" alt="powershell" />
I can pull out one of these randomly generated names and attempt a login with it after the domaincorp.com domain, and we're able to log in!
<img src="https://imgur.com/hpMlum7" alt="login as new user" />

