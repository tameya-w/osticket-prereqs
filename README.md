<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket Help Desk Deployment on Azure Virtual Machine</h1>
This tutorial will outline the prerequisites and installation steps of the open-source help desk ticketing system osTicket. The setup includes configuring IIS, PHP, MySQL, and osTicket installation. Upon completion of this tutorial we will have a working ticketing system and an understanding of each part of ticketing systems, including: ticket properties, SLAs (service level agreements), departments, permissions, and users.  <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Prerequisites</h2>

- Microsoft Azure account
- Windows 10 Virtual Machine (4 vCPUs)
- Remote Desktop access to the VM

## Step 1: Create a Virtual Machine in Azure
1. **Create a Windows 10 VM** with the following settings:
   - **Name:** osticket-vm
   - **vCPUs:** 4
   - **Username:** labuser
   - **Password:** osTicketPassword1!

![Screenshot 2025-03-13 152442](https://github.com/user-attachments/assets/99297f09-7b1c-4332-a8f4-9e308c74ffd3) ![Screenshot 2025-03-13 153714](https://github.com/user-attachments/assets/5d6784aa-fbb6-4ccf-a566-4a7e88e6476b)


2. **Log into the VM** using **Remote Desktop**.

![Screenshot 2025-03-13 154338](https://github.com/user-attachments/assets/36e15c6d-0c36-4c03-b10c-240effa320f2) ![Screenshot 2025-03-13 155106](https://github.com/user-attachments/assets/7dbc5939-535f-4e34-9be7-04401fddaadc)

Copy your newly created Virtual Machine's public IP Address and paste it into the remote browser to connect. Then login using the username and password created in the previous step.



## Step 2: Download osTicket Installation Files
1. Inside the VM, **download** `osTicket-Installation-Files.zip`.

![Screenshot 2025-03-17 123051](https://github.com/user-attachments/assets/a626be5f-a39c-4e3f-8210-865c32376924)

2. **Extract** the folder to the **desktop**.

![Screenshot 2025-03-17 123204](https://github.com/user-attachments/assets/23578737-97a4-4ab1-ac63-39309901ca19)

![Screenshot 2025-03-17 123300](https://github.com/user-attachments/assets/5bf8f6c9-dfcd-4b02-b870-0f9d157b9d70)

## Step 3: Install IIS and Enable CGI
1. Open **Windows Features** and enable:
   - **Internet Information Services (IIS)**
   - **World Wide Web Services**
   - **Application Development Features → [X] CGI**

![Screenshot 2025-03-17 124055](https://github.com/user-attachments/assets/6767cd5d-1560-4062-9d7b-4bf53be7376c)

## Step 4: Install Required Components
From the `osTicket-Installation-Files` folder:
1. Install **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`).

![Screenshot 2025-03-17 124640](https://github.com/user-attachments/assets/ea267a4c-f931-4a07-a6af-e72e3385bc3c)

2. Install **IIS Rewrite Module** (`rewrite_amd64_en-US.msi`).

![Screenshot 2025-03-17 125312](https://github.com/user-attachments/assets/f9cc4183-27aa-43e8-a9d9-4d88319022a9)


## Step 5: Configure PHP
1. Create the directory `C:\PHP`.

![Screenshot 2025-03-17 130149](https://github.com/user-attachments/assets/ab9bab03-4e53-411a-b360-0a275e6501ce)

 
2. Extract **PHP 7.3.8** (`php-7.3.8-nts-Win32-VC15-x86.zip`) to `C:\PHP`.

![Screenshot 2025-03-17 130920](https://github.com/user-attachments/assets/98a54c87-1619-4d94-bcf1-36ae570886ec)

3. Install **Visual C++ Redistributable** (`VC_redist.x86.exe`).

![Screenshot 2025-03-17 131216](https://github.com/user-attachments/assets/ba1cc980-0d8e-42ce-b8ba-907749470f9d)

## Step 6: Install MySQL
1. Install **MySQL 5.5.62** (`mysql-5.5.62-win32.msi`).
2. Select **Typical Setup**.

![Screenshot 2025-03-17 132328](https://github.com/user-attachments/assets/5bb24818-1052-4438-a2f7-627c2d51f102)

3. Run the **Configuration Wizard**:
   - Choose **Standard Configuration**.
   - Set **Username: root**.
   - Set **Password: root**.

![Screenshot 2025-03-17 133349](https://github.com/user-attachments/assets/2180250d-e4f4-4dbb-ac84-22a601156d5f)

![Screenshot 2025-03-17 133522](https://github.com/user-attachments/assets/3cf18d5c-5fc0-4e86-bc5f-0643706dab00)


## Step 7: Configure IIS for PHP
1. Open **IIS as an Administrator**.

![Screenshot 2025-03-17 134842](https://github.com/user-attachments/assets/0abbb10d-9873-4517-b16b-54df095385ed)


2. Register PHP:
   - Open **PHP Manager** → Select `C:\PHP\php-cgi.exe`.

![Screenshot 2025-03-17 135732](https://github.com/user-attachments/assets/0c6d54bd-41f2-49bf-97e4-596aee607285)

![Screenshot 2025-03-17 135634](https://github.com/user-attachments/assets/005f8f63-f2ed-4295-98d0-f370db1c36f8)



3. Restart IIS (**Stop and Start the server**).

![Screenshot 2025-03-17 140652](https://github.com/user-attachments/assets/bfa2aeb4-405f-4e99-ad1a-277f2b289013)

![Screenshot 2025-03-17 140714](https://github.com/user-attachments/assets/dd37e164-0650-4d45-b7a1-d55a7be6f52a)

## Step 8: Install osTicket
1. Extract `osTicket-v1.15.8.zip`.

![Screenshot 2025-03-17 143846](https://github.com/user-attachments/assets/2cee9dbb-e6dc-4e45-9149-13f8dd2cd9c4)


2. Copy the `upload` folder to `C:\inetpub\wwwroot`.

![Screenshot 2025-03-17 144322](https://github.com/user-attachments/assets/7fc1cf38-9c97-47fd-9e9b-acb3c1c59665)


3. Rename the folder from `upload` to `osTicket`.

![Screenshot 2025-03-17 144453](https://github.com/user-attachments/assets/6fe34ff4-6425-4558-b5e8-47cdfe3c55ed)


4. Restart IIS.


5. Open IIS → Go to **Sites → Default → osTicket**.

![Screenshot 2025-03-17 145510](https://github.com/user-attachments/assets/ff391d91-53a4-4839-816f-f61695e4e6c6)

6. Click **Browse *:80** to open osTicket in a browser.

![Screenshot 2025-03-17 145525](https://github.com/user-attachments/assets/392df4d7-fe68-493b-b494-5fe2ba5ec491)

![Screenshot 2025-03-17 145657](https://github.com/user-attachments/assets/ae585826-eb53-4202-a80a-af819d8cfd86)


## Step 9: Enable PHP Extensions
1. In IIS, go to **Sites → Default → osTicket**.
2. Open **PHP Manager**.
3. Click **Enable or Disable an Extension**.
4. Enable the following:
   - `php_imap.dll`
   - `php_intl.dll`
   - `php_opcache.dll`

![Screenshot 2025-03-17 154252](https://github.com/user-attachments/assets/39b2c13e-a3f8-425d-a8f2-f8ec05d185c5)


5. Refresh the osTicket site.

![Screenshot 2025-03-17 154907](https://github.com/user-attachments/assets/c807b3e8-1734-4d9b-9b7c-2b7d1e8806b7)

## Step 10: Configure osTicket
1. Rename `ost-config.php`:
   - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
   - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

![Screenshot 2025-03-17 160041](https://github.com/user-attachments/assets/afd38fb2-a8c6-40a8-bd5a-cde870f6bc50)

![Screenshot 2025-03-17 160246](https://github.com/user-attachments/assets/9736f437-5fec-418d-b7e2-7f7a40ecbb65)


2. Set file permissions:
   - **Disable inheritance → Remove All**
   - **Assign new permissions:** Everyone → All

![Screenshot 2025-03-17 161315](https://github.com/user-attachments/assets/4b076a7e-71d6-4ea2-9361-3222dac384ec)


## Step 11: Set Up Database
1. Install **HeidiSQL**.

![Screenshot 2025-03-17 162719](https://github.com/user-attachments/assets/10f59e4d-fa65-4549-92f7-7624688f9a01)

2. Open **HeidiSQL** and create a new session (`root/root`).
3. Connect to the session and create a database named `osTicket`.

![Screenshot 2025-03-17 163117](https://github.com/user-attachments/assets/ae2d5c4b-3d9b-4099-9127-9623ca662686)

## Step 12: Finalize osTicket Installation
1. Continue the setup in the browser.
2. Set Helpdesk Name and Default Email.

![Screenshot 2025-03-17 162529](https://github.com/user-attachments/assets/bd779ee0-32f2-4417-b859-afe1d07c4013)

3. Configure MySQL:
   - **Database:** osTicket
   - **Username:** root
   - **Password:** root

![Screenshot 2025-03-17 163408](https://github.com/user-attachments/assets/2e69138f-d172-4f85-8c5c-09710c97a74e)

4. Click **Install Now!**

![Screenshot 2025-03-17 163514](https://github.com/user-attachments/assets/fe4f6d20-1a0d-4550-9d35-782a355238b5)

![Screenshot 2025-03-17 163907](https://github.com/user-attachments/assets/61f3b5b9-5c76-437f-87a7-d24afc8b9fc9)

5. Access the **Admin Panel:** `http://localhost/osTicket/scp/login.php`

![Screenshot 2025-03-17 164245](https://github.com/user-attachments/assets/2ddbcb45-726a-4c44-8b54-d08aff7b28a8)

6. End User Portal: `http://localhost/osTicket/`

![Screenshot 2025-03-17 164419](https://github.com/user-attachments/assets/4b5fe8ce-801b-4711-8657-9a542b2fe027)



