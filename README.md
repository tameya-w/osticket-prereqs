<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket Help Desk Deployment on Azure Virtual Machine</h1>
This tutorial will outline the prerequisites and installation steps of the open-source help desk ticketing system osTicket. The setup includes configuring IIS (Internet Information Services), PHP (Hypertext PreProcessor), MySQL (My Structured Query Language), and osTicket installation. Upon completion of this tutorial we will have a working ticketing system and an understanding of each part of ticketing systems, including: ticket properties, SLAs (service level agreements), departments, permissions, and users.  <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Prerequisites</h2>

- Microsoft Azure Subscription
- Remote Desktop Client (RDP)


<h2>Installation Steps</h2>

<h2>Step 1: Create an Azure Virtual Machine</h2>

- Log into Azure and navigate to the Azure Portal.

- Create a Windows 10 VM with the following specifications:

      Name: osticket-vm

- vCPUs: 4

      Username: labuser

      Password: osTicketPassword1!

  ![Screenshot 2025-03-13 152442](https://github.com/user-attachments/assets/afd85f54-0959-442e-8b43-26b0ba710838)

  ![Screenshot 2025-03-13 152728](https://github.com/user-attachments/assets/f64ee2e8-2cc3-409b-9ff3-b0c6c9bfcc97)

  ![Screenshot 2025-03-13 153714](https://github.com/user-attachments/assets/e6b4906c-6237-425b-a586-5e3c8e4a8183)



- Once deployed, connect to the VM via Remote Desktop (RDP).

![Screenshot 2025-03-13 154338](https://github.com/user-attachments/assets/4296dd2a-b0d0-449e-a490-511ca6ab3066)

![Screenshot 2025-03-13 155106](https://github.com/user-attachments/assets/6e249371-23e6-4d21-b655-e59506188a6c)


<h2>Step 2: Prepare the Windows Environment</h2>

Download & Extract osTicket Installation Files

Unzip the file to the desktop.

The folder should be named osTicket-Installation-Files.

Enable IIS with CGI Support

Open Control Panel → Turn Windows features on or off.

Enable:

✅ Internet Information Services (IIS)

✅ World Wide Web Services

✅ Application Development Features → CGI

<h2>Step 3: Install Required Dependencies</h2>

Install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi).

Install the IIS Rewrite Module (rewrite_amd64_en-US.msi).

Set Up PHP:

Create a directory: C:\PHP

Unzip php-7.3.8-nts-Win32-VC15-x86.zip into C:\PHP.

Install VC++ Redistributable (VC_redist.x86.exe).

Install MySQL 5.5.62 (mysql-5.5.62-win32.msi):

Choose Typical Setup.

Launch Configuration Wizard → Standard Configuration.

Set:

Username: root

Password: root

<h2>Step 4: Configure IIS & PHP</h2>

Open IIS as Administrator.

Register PHP in IIS:

Open PHP Manager → Register: C:\PHP\php-cgi.exe.

Restart IIS:

Open IIS, Stop and Start the server.

<h2>Step 5: Install osTicket</h2>

Extract osTicket v1.15.8:

Copy the upload folder to C:\inetpub\wwwroot.

Rename upload → osTicket.

Restart IIS.

Open osTicket in a Web Browser:

In IIS, go to Sites → Default → osTicket.

Click *Browse :80.

<h2>Step 6: Enable PHP Extensions</h2>

Open IIS → Sites → Default → osTicket.

Go to PHP Manager → Enable Extensions:

✅ php_imap.dll

✅ php_intl.dll

✅ php_opcache.dll

Refresh the osTicket browser page.

<h2>Step 7: Configure osTicket</h2>

Rename Configuration File:

From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php

To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Set File Permissions:

Disable inheritance, remove all.

Add Everyone → Full Control.

Continue osTicket Setup in Browser:

Enter Helpdesk Name.

Enter Default Support Email.

<h2>Step 8: Set Up MySQL Database for osTicket</h2>

Install HeidiSQL.

Open HeidiSQL & Create a New Session:

Username: root

Password: root

Create a database: osTicket.

Complete osTicket Setup in Browser:

MySQL Database: osTicket

MySQL Username: root

MySQL Password: root

Click Install Now!

Verify Installation:

Admin URL: http://localhost/osTicket/scp/login.php

End-User URL: http://localhost/osTicket/

<h2>Step 9: Post-Installation Cleanup & Security</h2>

Delete the setup directory:

Remove: C:\inetpub\wwwroot\osTicket\setup

Secure the Configuration File:

Set C:\inetpub\wwwroot\osTicket\include\ost-config.php to Read-Only.

<h2>Step 10: Final Testing</h2>

Log into the osTicket Admin Panel.

Test creating and resolving helpdesk tickets.

Ensure PHP extensions are correctly enabled.

<h2>Conclusion</h2>

By following this guide, you have successfully:

Set up a Windows 10 VM in Azure.

Installed and configured IIS, PHP, and MySQL.

Deployed and secured osTicket Help Desk.













