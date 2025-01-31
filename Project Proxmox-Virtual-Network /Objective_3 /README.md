# **Objective 3: Initial Configuration of Proxmox VE**

## Description
This objective covers logging into the Proxmox web interface, managing storage, and performing initial system configurations. The tasks include removing unnecessary storage volumes, expanding the existing storage, and ensuring the system is up to date. These actions prepare the system for future virtual machine deployments and remote administration.

## Actions Taken

1. **Login to Proxmox Web Interface**  
   Enter the IP address of your Proxmox server into a web browser to open the Proxmox web interface.  
   ![IMG_20250131_094438355_HDR](https://github.com/user-attachments/assets/28d17a45-8200-462c-a9c8-d43d3911c4a9)

2. **Enter Credentials**  
   On the login page, enter the credentials:  
   - **Username**: root  
   - **Password**: The password set during installation.  
   ![2025-01-31 09_54_25-Window](https://github.com/user-attachments/assets/18818e78-a64e-4e7c-b30c-fc1b2ed1ae00)

3. **Check Storage Configuration**  
   After installation, Proxmox automatically creates two storage locations: **local** and **local-lvm**. By default, Proxmox uses these for file storage.  
   ![2025-01-31 11_20_59-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/5a8cdbc5-0017-4583-8326-f19418317e78)

4. **Remove local-lvm Storage and Expand local Storage**  
   Since the second storage is not needed, I decided to remove **local-lvm** and expand **local** storage.

   **Step 4.1**: Remove **local-lvm** storage.  
   ![2025-01-31 11_25_14-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/7d2c5e51-f620-42be-82e3-9e5b8d3ae9f7)

   **Step 4.2**: Open the Proxmox shell.  
   ![2025-01-31 11_31_50-Window](https://github.com/user-attachments/assets/85e83519-dda7-40ef-81b2-0aa80d73298b)

   **Step 4.3**: Enter the following commands to resize the **local** storage:  
   `lvremove /dev/pve/data`  
   Confirm the removal by typing `y`.  
   `lvresize -l +100%FREE /dev/pve/root`  
   `resize2fs /dev/mapper/pve-root`  
   ![2025-01-31 11_39_15-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/52dd74fb-600d-494c-9f75-8512d5a78395)

   **Step 4.4**: Finally, modify the directory content rules to allow installing disk images on **local** storage.  
   ![2025-01-31 11_47_19-Window](https://github.com/user-attachments/assets/82b2cc3b-a98f-40ec-99b3-afae7872e46d)  
   ![2025-01-31 11_48_19-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/8aea5668-3a3b-488a-8f2d-ef3c916f13da)

5. **Update System and Packages**  
   To ensure the system is up-to-date, I ran the following commands:  
   `apt update && apt full-upgrade -y`  

6. **Check SSH Status**  
   I checked if the SSH service was running with the following command:  
   `systemctl status ssh`  
   The SSH service was active, and no further action was needed.

---

## Issues & Troubleshooting  
*No issues encountered; smooth process.*

## Lessons Learned
- How to remove local-lvm storage, resize local storage, and change storage rules.
- How to configure Proxmox remotely from a browser and access the Proxmox terminal.
- Proxmox interface usage.
