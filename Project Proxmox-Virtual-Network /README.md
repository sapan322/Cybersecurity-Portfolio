# **Proxmox Virtual Network**

## **Description**
This project is designed to learn how to use the **"Type 1" Hypervisor Proxmox VE** by building a **corporate-like virtual network**.  
The project includes creating **DMZ, LAN, and ADMIN** zones using **pfSense** as a firewall and router.
The goal is to simulate a realistic IT infrastructure, enabling secure communication and network segmentation.

![#0 1](https://github.com/user-attachments/assets/aa3bc070-f3a0-4e48-83a3-17f38b9c4880)



## **Objectives**
- **Objective 1:** Preparation  
- **Objective 2:** Proxmox VE Installation  
- **Objective 3:** Initial Configuration of Proxmox VE  
  - **3.1:** System update  
  - **3.2:** Install and configure SSH for remote connection and automation  
- **Objective 4:** VLANs and pfSense  
  - **4.1:** Configure network bridges and VLANs  
  - **4.2:** Install and configure pfSense  
- **Objective 5:** Server Deployment  
  - **5.1:** Deploy a VM with a Web server  
  - **5.2:** Deploy a VM with a Database server  
  - **5.3:** Deploy user VMs (Windows, Linux)  
  - **5.4:** Deploy a VM with Windows Server and set up Active Directory (Groups & Users)  
- **Objective 6:** Security and Monitoring  
  - **6.1:** Configure firewall rules in pfSense  
  - **6.2:** Install monitoring tools and set up logging  
- **Objective 7:** Testing & Validation  
  - **7.1:** Test basic network connectivity  
  - **7.2:** Perform network scans (Nmap)  
  - **7.3:** Evaluate network security  

## **Technologies Used**
- **Proxmox VE** (Virtualization)  
- **pfSense** (Firewall & Router)  
- **Ubuntu, Windows 10/11, Windows Server** (VMs)  
- **Nginx/Apache, MySQL/PostgreSQL** (Web & Database)  
- **Monitoring Tools** (e.g., Prometheus, Grafana)  


## Installation
[Objective 1: Preparation](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_1)

[Objective 2: Proxmox VE Installation](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_2)

[Objective 3: Initial Configuration of Proxmox VE](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_3%20)

[Objective 4: VLANs and pfSense](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_4%20)

## Challenges & Solutions

- **Challenge 1:** Proxmox doesn’t boot after installation (only "Rescue Boot" from USB works).
    - [**Solution:**](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_2#problem-1-proxmox-doesnt-boot-after-installation-only-rescue-boot-from-usb-works)
- **Challenge 2:** "Virtualization support not enabled" error message.
    - [**Solution:**](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_2#problem-2-virtualization-support-not-enabled-error-message)
- **Challenge 3:** "Proxmox VE shuts down when the laptop lid is closed."  
    - **Solution:** Modify system settings to prevent the system from suspending when the lid is closed.  
      1. Open the Proxmox shell.  
      2. Edit the **login.conf** file using nano:  
         ```
         nano /etc/systemd/logind.conf
         ```
      3. Find the following lines, remove the `#` at the beginning, and update them as follows:  
         ```
         HandleLidSwitch=ignore
         HandleLidSwitchDocked=ignore
         ```
      4. Save the file (`CTRL + X`, then `Y`, and `Enter`).  
      5. Restart the logind service to apply changes:  
         ```
         systemctl restart systemd-logind.service
         ```
- **Challenge 4:** ["Network configuration with errors, causing the inability to reconnect to the vmbr0"](https://github.com/sapan322/Cybersecurity-Portfolio/tree/main/Project%20Proxmox-Virtual-Network%20/Objective_4%20#problem-1)  
    - **Solution:** I accessed the server directly, manually restored the configuration to the default settings, and was able to reconnect remotely.


## Lessons Learned
- I learned how to properly install Proxmox and configure BIOS settings for virtualization support.
- It's important to check the boot mode (Legacy vs. UEFI) before installation.
- I gained hands-on experience in configuring network interfaces in Proxmox VE, especially regarding VLANs and network bridges.
- How to remove local-lvm storage, resize local storage, and change storage rules.
- How to configure Proxmox remotely from a browser and access the Proxmox terminal.
- Proxmox interface usage.
- Understanding Proxmox interface relationships and how to configure them.
- Creating subinterfaces and bridges to handle VLANs.
- Manual configuration of Proxmox networking.
- How the physical interface (enp0s25) and the bridge (vmbr0) interact to enable VLAN tagging and network separation.


## Future Improvements

Suggestions or ideas for improving the project in the future.

## Acknowledgements
Special thanks to: 

**ChatGPT dev team**

**NetworkChuck**
