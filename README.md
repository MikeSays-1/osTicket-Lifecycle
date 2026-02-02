<p align="center">
<img width="600" alt="Microsoft Active Directory Logo" src="images/osTicket Logo.png" />

</p>

<h1>osTicket Ticket Lifecycle Simulation</h1>
This project expands on the previous osTicket configuration lab by moving beyond setup and into a realistic end-to-end ticket lifecycle. Building on previously created departments, roles, and permissions, this scenario simulates a business-critical outage from initial end-user ticket creation through triage, escalation, role-based access changes, and final resolution. The lab emphasizes proper permission boundaries, escalation procedures, SLA prioritization, and real-world support workflows across Tier I and SysAdmin roles.<br />


<!--
<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)
-->

<h2>Environments and Technologies Used</h2>
<p align="left">
<img src="https://skillicons.dev/icons?i=azure,windows" />&nbsp;&nbsp;<img src="images/osticket-icon-dark.png" width="48"></p>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- osTicket

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>


**Key Actions**
- Clean up initial osTicket configuration to ensure tickets route correctly
- Create and review a ticket as an end user and a limited-permission agent
- Simulate ticket triage, escalation, and role-based access changes
- Transfer the ticket to the appropriate department for resolution
- Resolve and close the ticket after verifying service restoration

> [!IMPORTANT]
> Each step includes written instructions followed by a corresponding screenshot.
<br>Expand the **See screenshots** section to view the images.


> [!NOTE] 
> This project builds upon a prior lab where the Azure environment, virtual machine, osTicket and various users and teams were created. **ADD LINK HERE**

**Admin/Analyst/Agent Login Page:**
http://localhost/osTicket/scp/login.php 

**End Users osTicket URL:**
http://localhost/osTicket 

<h2>osTicket Configurations</h2> 

<h3>1. DELETE DEFAULT DEPARTMENT</h3>
<p>We need to delete the default Maintenance Department, as new tickets get automatically assigned to this department and not to the departments we created in the prior lab. In Admin panel, select Agents tab, select Department section. Select the Maintenance Department, and select More near the top-right, and select Delete.</p>

<details><summary>See screenshots</summary>
<img src="images/Step 1a.PNG" width="60%" >
</details> 

<h3>2. TICKET CREATION AND REVIEW</h3>
<p>End-user reports that the online banking system is down.

Login the End Users osTicket URL and as an end-user, Karen, open a new ticket. Intentionally choose the incorrect Help Topic, General Inquiry/Other and explain the online banking system is down, and submit.  </p>

<details><summary>See screenshots</summary>
<img src="images/Step 2a.PNG" width="60%" >
</details> 


Login into the Admin portal as John Doe. Review the ticket. Observe that John can only view the ticket, and leave an internal note.  

Let's leave a note, <i>"This ticket requires elevated permissions. I will reach out to the SysAdmin department to request a role upgrade"</i>

<details><summary>See screenshots</summary>
<img src="images/Step 2b.PNG" width="60%" >
</details> 

In osTicket, we cant @ or send the ticket directly to SysAdmin, but we can simulate, John leaving a note, reaching out to the department by external email to request elevated permissions to his account.

<h3>3. TICKET TRIAGE AND ESCALTION SIMULATION</h3>

Logout as John, and log back in as the Admin user, and elevate John to Super Admin role. Log back in as John, and we'll triage the ticket as best as we can as Tier I support Agent. Update priority to Emergency, and reason for update: <i>"Called Karen and confirmed all tellers systems have been down since lunch."</i>. Update the SLA Plan to Sev-A, as the issue is Business Critical. Update the Help Topic to Business Critical Outage and note <i>"Entire branch system is offline."</i> In response text field, explain the steps taken, and advise "Escalating and assigning ticket to SysAdmin Department after triaging." and Post Reply.  Lastly, assign the ticket to Jane Doe, transfer the ticket out of Support Department and into SysAdmin Department. 

<details><summary>See screenshots</summary>
<img src="images/Step 3a.PNG" width="30%" > <img src="images/Step 3b.PNG" width="30%" > <img src="images/Step 3c.PNG" width="30%" >
</details> 

> [!NOTE]
> Observe that John no longer has access to the original ticket, because of how our permissions are configured.

<h3>4. TICKET RESOLUTION</h3>

Logout as John, and log back in as Jane, our SysAdmin. Review the ticket as Jane, and observe the timeline, review the actions and notes given by Karen and John. 

<details><summary>See screenshots</summary>
<img src="images/Step 4a.PNG" width="60%" >
</details> 

In a real work environment, system outages can be caused by many different factors. For the purposes of this lab, we will assume the issue was caused by an accidental restart of the online banking system’s backend server during business hours due to a configuration issue.

Post the following message as a ticket reply:

“We accidentally restarted the online banking system’s backend server during business hours due to a configuration issue. We will review the settings and attempt to restart the service.”

<details><summary>See screenshots</summary>
<img src="images/Step 4b.PNG" width="60%" >
</details> 

In this scenario, Jane restarts the server and verifies the online banking system status. Once service is confirmed to be restored, post the following update:
“Server successfully restarted. Online banking systems appear to be operational. Confirmed with Karen. Resolving and closing ticket." Set the ticket status to Resolved. 

<details><summary>See screenshots</summary>
<img src="images/Step 4c.PNG" width="30%" > <img src="images/Step 4d.PNG" width="30%" >
</details> 

> [!NOTE]
> In osTicket, setting a ticket’s status to Resolved automatically marks the ticket as Closed. Other ticketing systems may separate these steps, where a ticket is marked as Resolved after a fix is applied and Closed only after confirmation that no further action is required.
