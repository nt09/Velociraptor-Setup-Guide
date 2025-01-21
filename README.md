# Velociraptor-Setup-Guide 

<img src="https://github.com/user-attachments/assets/9dddc540-60ad-4135-b2af-6691cef1e83d"  alt="Velociraptor Logo" width="100" style="float: left; margin-right: 10px;"/>
Velociraptor is an open-source tool designed to monitor, investigate, and respond to security threats in real time. This guide explains how to install and use Velociraptor on a Linux server and configure clients on Windows and Linux systems.

## Table of Contents
* Introduction
* Server Installation on Kali Linux
* Client Installation on Windows
* Client Installation on Linux

## Introduction
Velociraptor provides powerful capabilities for:

- **Data Collection**: Collect key information from systems to identify security events and anomalies.
- **Incident Response**: Execute remote commands to gather evidence or quickly isolate and neutralize threats.
- **Real-time Monitoring**: Continuously monitor systems for suspicious activity or security violations.
- **Forensic Analysis**: Capture and examine digital artifacts to analyze the scope and nature of attacks.

# Server Installation on Kali Linux
### Steps:

#### 1. Download Velociraptor Binary:

* Visit the [official release page](https://github.com/Velocidex/velociraptor/releases) and download the Linux binary.
  
  ![image](https://github.com/user-attachments/assets/c4f3582e-07e4-4a7c-ab55-916fd8d89412)


#### 2. Setup Directory:


    mkdir velociraptor  
    cd velociraptor  
  ![Screenshot 2025-01-21 131327](https://github.com/user-attachments/assets/d705c1e0-e336-4fdd-ac30-b4af50b42470)

#### 3. Make Binary Executable:


    chmod +x velociraptor-v0.73.1-linux-amd64  
  ![Screenshot 2025-1-21 131327](https://github.com/user-attachments/assets/83f1455d-f689-47b6-8963-6228484aedea)

#### 4. Generate Server Configuration:


    ./velociraptor-v0.73.1-linux-amd64 config generate -i  
  ![image](https://github.com/user-attachments/assets/3695b38b-3a6c-4550-8deb-4f2981cef545)

* Username: "admin"
* Password: ******
  
  ![image](https://github.com/user-attachments/assets/68abecaf-814e-40f3-9cd6-ffa108e7b262)


#### 5. Optional Configuration Adjustments:

* Modify " server.config.yaml " as needed:

      nano server.config.yaml
  ![image](https://github.com/user-attachments/assets/d87f7cea-8954-4a3d-82bf-c91dd42b40a6)
  ![image](https://github.com/user-attachments/assets/0049e4f4-0743-4c9a-a104-09f80e69143e)


#### 6. Install and Start the Server:


    ./velociraptor-v0.73.1-linux-amd64 --config server.config.yaml debian server --binary velociraptor-v0.73.1-linux-amd64  
  ![image](https://github.com/user-attachments/assets/affc96ae-39f6-4c8b-bdc9-c1cf5c6a1519)
  ![image](https://github.com/user-attachments/assets/0002490a-90c4-4abb-a9aa-5c55b7c1379d)


    dpkg -i velociraptor_server_0.73.1_amd64.deb  
 ![image](https://github.com/user-attachments/assets/fd14e98c-79ba-4713-ba1f-136e001377d1)
 
#### 7. Check the service status:


    systemctl status velociraptor_server  
 ![image](https://github.com/user-attachments/assets/deddfeda-fe31-45dd-a351-4d80abff996a)
 
#### 8. Access the Web Interface:

* URL: " https://<server_ip>:8889/ "
* Login: " admin "
* Password: ******
![image](https://github.com/user-attachments/assets/0975ae99-c480-4fda-b1a0-4cac886c6e39)
![image](https://github.com/user-attachments/assets/d0a0f228-fce5-4b4c-bbcb-f1cc21185f56)



# Client Installation on Windows
### Steps:
#### 1. Download Configuration File:
   
* Start an HTTP server on Kali Linux:

       python3 -m http.server 8888
![image](https://github.com/user-attachments/assets/1062222a-2178-4d36-a870-de077673bb5b)

* Access " http://<server_ip>:8888 " on the Windows machine to download " client.config.yaml ".
  
![image](https://github.com/user-attachments/assets/e8ce9c8c-84e8-4dc4-b260-e9d372829535)

* Create a folder " C:\Windows\System32\velociraptor " and place the " client.config.yaml " file inside.
  
 ![image](https://github.com/user-attachments/assets/5622c862-489c-44de-9898-c29ea743104a)
 

#### 2. Download the Velociraptor Binary:

* Visit the [official release page](https://github.com/Velocidex/velociraptor/releases) and download the Windows binary.
  ![image](https://github.com/user-attachments/assets/d544dabd-b68a-427a-a0b2-ca303a7f7b9e)

* Place " velociraptor-v0.73.1-windows-amd64.exe " in the " C:\Windows\System32\velociraptor " folder.

#### 3. Install and Start the Client:

    .\velociraptor-v0.73.1-windows-amd64.exe --config .\client.config.yaml service install  
  ![image](https://github.com/user-attachments/assets/f636d128-b0ec-410a-896e-0fb81fbfaff4)

    
#### 4. Verify the Installation:

       dir "C:\Program Files\velociraptor"  
 ![image](https://github.com/user-attachments/assets/d9188283-9e43-495f-9f27-a77405a4982b)
 
#### 5. Check the Service Status:
* Open " Services.msc " and verify the Velociraptor client service is running.
#### 6. Verify Client Addition:
* Log in to the Velociraptor web interface and confirm the client appears in the dashboard.
  ![image](https://github.com/user-attachments/assets/2698b627-93bc-41f3-a8f5-bc56b66cc513)


# Client Installation on Linux
### Steps:

#### 1. Install the Client on the Server (Kali Linux):

       ./velociraptor-v0.73.1-linux-amd64 --config client.config.yaml debian client  
  ![image](https://github.com/user-attachments/assets/bc0aa83c-a20a-42ff-8200-d09732a32fb4)
  ![image](https://github.com/user-attachments/assets/a1592555-6e07-42db-a69d-c351c1e0048d)


       python3 -m http.server 8888
  ![image](https://github.com/user-attachments/assets/32864505-e0be-42a2-8084-c66feaa51a84)

   
#### 2. Install the Client on the Target Machine (Ubuntu):
   
* Create a directory and Download the client binary:

      mkdir velociraptor  
      wget http://<server_ip>:8888/velociraptor_client_0.73.1_amd64.deb
  ![Screenshot 2025-01-21 1 2](https://github.com/user-attachments/assets/e48ae6df-5b5d-4704-a6a7-df5e0b7c26a1)

* Install the client:

         dpkg -i velociraptor_client_0.73.1_amd64.deb
  ![Screenshot 2025-01-21 3](https://github.com/user-attachments/assets/ab938c35-ff15-4e8f-be40-f1319ce64da4)

* Check the service status:

       systemctl status velociraptor_client
![Screenshot 2025-01-21 4](https://github.com/user-attachments/assets/7ac4e7cc-1266-4b78-a57e-39102737e603)

    
#### 3. Verify Client Addition:
   
* Log in to the Velociraptor web interface and confirm the client appears in the dashboard.
 ![image](https://github.com/user-attachments/assets/6cf38229-db0e-448a-a745-1ccdf5cd0653)
 
