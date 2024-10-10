<p align="center">
<img src="https://github.com/user-attachments/assets/9cc225a5-e325-4e92-a012-975c7162f8ac" alt="osTicket logo"/>
</p>


<h1>Building Intuition for DNS</h1>

In this lab, we will explore the fundamentals of DNS and experiment with its various record types to gain a deeper understanding of how the system works.

<h2>Environments and Technologies Used</h2>

	•	Microsoft Azure (Virtual Machines/Compute)
	•	Remote Desktop
	•	DNS

<h2>Operating Systems Used</h2>

	•	Windows 10 (21H2)

<h2>List of Prerequisites</h2>

	•	An Active Directory Virtual Machine.
	•	A Client Machine joined to your domain.

<h2>Lab Steps</h2>

Step 1: Creating a DNS A-Record

An A-Record is a hostname to IP address mapping in DNS. We will create an A-Record on the DC-1 machine for mainframe and have it point to DC-1’s private IP address.

	1.	Go to AD > Tools > DNS > DC-1 > Forward Lookup Zones > mydomain.com.
	2.	Right-click and select New A Record.
	3.	Set the hostname to mainframe.
	4.	Assign DC-1’s private IP address to the record.

	•	Before creating the DNS record: If we try to ping mainframe from Client-1, it will not resolve, as it’s not defined in DNS.
	•	After creating the DNS record: If we go back to Client-1 and try to ping mainframe, we should see a successful reply.

<p align="center">
<img src="https://i.imgur.com/xKePr4k.png" height="80%" width="80%" alt="Creating A-Record"/>
<img src="https://i.imgur.com/yAlrhZw.png" height="80%" width="80%" alt="A-Record in DNS"/>
</p>


Step 2: Updating and Flushing DNS Records

	1.	Go back to the DNS Manager and update the mainframe record to use 8.8.8.8 instead of the original IP.
	2.	Try pinging mainframe again from Client-1. You will notice that the ping still points to the old IP address.

This occurs because DNS caching is in effect on the client machine.

	•	Flush the DNS cache:
Open Command Prompt on Client-1 and run the following command:

ipconfig /flushdns



	3.	After flushing the DNS cache, try pinging mainframe again. It should now resolve to 8.8.8.8.

<p align="center">
<img src="https://i.imgur.com/KYNmZMz.png" height="80%" width="80%" alt="Flush DNS Command"/>
<img src="https://i.imgur.com/80ARdZu.png" height="80%" width="80%" alt="Updated DNS Record"/>
</p>


Step 3: Creating a CNAME Record

A CNAME (Canonical Name) record is used to create an alias for a domain name. In this step, we will configure a CNAME record that points search to www.google.com.

	1.	Go back to DNS Manager on DC-1.
	2.	Right-click on mydomain.com and select New CNAME (Alias).
	3.	Enter the alias name as search.
	4.	For the Fully Qualified Domain Name (FQDN), enter www.google.com.
	5.	Click OK to create the record.

	•	Before creating the CNAME record: If you try to ping search from Client-1, it will not resolve.
	•	After creating the CNAME record: When we ping search, it should resolve to www.google.com.

<p align="center">
<img src="https://i.imgur.com/LgomfqN.png" height="80%" width="80%" alt="Creating CNAME Record"/>
<img src="https://i.imgur.com/NovtDrd.png" height="80%" width="80%" alt="CNAME Record for Google"/>
</p>


<h2>Summary</h2>

	•	We created and tested A-Records by mapping hostnames to IP addresses.
	•	We learned how to update DNS records and flush the DNS cache to see immediate changes.
	•	We configured a CNAME record to point to an external domain, demonstrating how aliases can be used in DNS.

This lab provided a foundational understanding of DNS record management and its practical use cases.

Let me know if you need any further modifications or have additional details to include!
