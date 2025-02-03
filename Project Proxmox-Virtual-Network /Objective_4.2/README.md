# **Objective 4.2: pfSense**

## Description


## Actions Taken
1. Download pfSense ISO image from [official site](https://www.pfsense.org/download/).

2. Upload pfSense ISO image to local storage.
   
    ![Iso upload](https://github.com/user-attachments/assets/887f8d92-ab12-449a-9f98-2de063bb8e87)

3. Hit button "Create VM" in Proxmox web interface. 

    ![Create Vm](https://github.com/user-attachments/assets/4a04b823-e181-41a6-8971-9d9da4d15ec5)

      All default, except: 
      Name: pfSense; Type: Other; ISO Image: uploaded image; Disk size: 8gb (you can use more); Cores: 2; Type: host; Model: VirtIO (paravirtualized); Bridge: vmbr0; Firewall: empty

3. Configure Network Interfaces in pfSense VM Hardware
Add 3 additional "Network Device" with random generated MAC address
![vmbr0](https://github.com/user-attachments/assets/999e8862-e5ad-4b6a-9719-b0419f9d5a50)
![vmbr10](https://github.com/user-attachments/assets/e998d120-5fa2-4399-a297-616add1411ee)
![vmbr20](https://github.com/user-attachments/assets/0dcc6148-b4a1-4b08-bfcf-1e45f3d50020)
![vmbr30](https://github.com/user-attachments/assets/afde08c6-a4cd-4ad5-be3a-d2095ab9fc31)

4. Start VM

    ![VM start](https://github.com/user-attachments/assets/053e2246-0876-4aeb-8d19-766bac7edc7f)

   Hit "Install pfSense"

    ![Install](https://github.com/user-attachments/assets/62d19912-5b10-40ab-965c-726191aee378)

4. Select WAN Interface - VMBR0 = vtnet0

      ![Select interface](https://github.com/user-attachments/assets/124d7f1d-18df-4807-a389-209227b0a4c1)

5. WAN-interface setup by default.

      ![2025-02-01 14_35_41-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/f724fa3a-1b0c-477b-977f-4beba37c7048)

6. Select LAN Interface. We start with VMBR10 (Admin zone VLAN)

      ![2025-02-02 18_36_50-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/e0c3de81-5020-46bb-b20e-4bd74d0040bc)

   And i choose this configuration for LAN
   
   - Interface Mode: STATIC - i dont need dynamic ip address for VLAN
   - VLAN Settings: Disabled - we already have VLAN tagging in sub-interfaces configured
   - IP Address: 192.168.10.1/24 - VLAN10
   - DHCP Enabled: True - pfSense will assign IP address for devices
   - DHCP Range 192.168.10.100 – 192.168.10.150 - DHCP will assgign IP addresses in this range.

8. Confirm network configuration and wait until "connectivity check" end. When installer ask about subscription - select "Install CE".

    ![2025-02-02 18_52_13-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/7707bb80-9deb-446a-86d5-a8202c6f1ceb)

   
9. Filesystem and Partition Settings as default. Confirm other minor configurations and installation starts.

      ![2025-02-02 19_01_06-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/534d6dac-d36a-451f-8e3e-44d1af88f124)

10. After installation is completed - remove ISO file in VM hardware settings and click "reboot".

      ![2025-02-02 19_08_41-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/fe524921-38b0-477c-a6fd-286c659ec349)

11. After reboot pfSesne ask about WAN and LAN interfaces - for WAN vtnet0 as VMBR0, for LAN vtnet10 as VMBR10. After that we get IP address assigned by router DHCP for connection to web interface.

      ![2025-02-02 19_47_17-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/00f5c8fa-a307-4fe2-942f-5442e574185d)

12. VLANS configuration need to be finished - open up pfSense shell and [temporary enable pfSense web GUI access](https://github.com/sapan322/Cybersecurity-Portfolio/blob/main/Project%20Proxmox-Virtual-Network%20/Objective_4.2/README.md#problem-1) from the WAN by command that will disable firewall "pfctl -d"

      ![2025-02-02 20_00_06-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/d2a5ad9e-c782-4f12-89e4-63a1f587bb65)

13. So now i can enter WAN address in main machine browser and access to pfSense Web GUI. Default credentials:
     - Username: admin
     - Password: pfsense

       ![2025-02-02 20_06_05-pfSense - Login](https://github.com/user-attachments/assets/e83c5440-937c-4f79-a7a1-e46f6a67cefd)

14. Now Wizard pfSense Setup by 
    
      ![2025-02-02 20_34_46-pfSense home arpa - Wizard_ pfSense Setup_ General Information](https://github.com/user-attachments/assets/9093f47d-2c1a-4f13-89fb-3f782a549d25)

   I use https://docs.netgate.com/pfsense/en/latest/config/setup-wizard.html guide.
   
   Configure LAN Interface - use 192.168.10.1/24 for LAN which VMBR0 (ADMIN zone)
   
   ![2025-02-02 20_50_37-pfSense home arpa - Wizard_ pfSense Setup_ Configure LAN Interface](https://github.com/user-attachments/assets/3ec83819-5550-4033-a30c-8539cbf53f60)

15. In Interfaces / Interface Assignments add two other interfaces "vtnet2" and "vtnet3" and configure them.

   ![2025-02-02 21_14_43-pfSense pfsense home arpa - Interfaces_ Interface Assignments](https://github.com/user-attachments/assets/78f4616b-e433-4ce6-844c-0486d8b25dc3)

   - vtnet2 = LAN zone IPv4 192.168.20.1
   - vtnet3 = DMZ zone IPv4 192.168.30.1

16. In Services / DHCP Server / *LAN name* also configure DHCP server for each zone

   - ADMIN (vmbr10): 192.168.10.100 - 192.168.10.150
   - LAN (vmbr20): 192.168.20.100 - 192.168.20.150
   - DMZ (vmbr30): 192.168.30.100 - 192.168.30.150






## **Issues & Troubleshooting**

### **Problem 1:**  
After installation - Web interface access are blocked from WAN for security concerns. 
- **Solution:**  
Temporary enable pfSense web GUI access from the WAN by command that will disable firewall "pfctl -d"

---

## **Lessons Learned**

