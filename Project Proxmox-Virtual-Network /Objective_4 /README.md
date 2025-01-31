# **Objective 4: VLANs and pfSense** David McKone https://www.youtube.com/watch?v=ljq6wlzn4qo 

## Description




## Actions Taken
1. Proxmox use physical interface called "enp0s25" and bridge to it called "vmbr0"
      ![Network understanding](https://github.com/user-attachments/assets/7779f008-2e03-42c0-9430-01ef17071e2a)


2. Make a backup "Network Interfaces Configuration" file  

      ![2025-01-31 22_18_40-proxmox - Proxmox Virtual Environment](https://github.com/user-attachments/assets/353a79dd-948b-470b-b98d-6d2ff643f3ac)

3. DMZ zone will be "VLAN 30", LAN - "VLAN 20", ADMIN - "VLAN 10".
   ![VLAN scheme drawio - draw io](https://github.com/user-attachments/assets/bea93cfc-c317-4faa-b650-ef7f97e7f37a)

   Create interface for each VLAN in "/etc/network/interfaces" file what will use physical interface "enp0s25" for packets tag.

   auto vlan10
   iface vlan10 inet manual
       vlan_raw_device enp0s25

   ![vlan config](https://github.com/user-attachments/assets/1818cdd8-7495-413c-853b-0303ffde0942)

   Create bridges for each VLAN that we created for VM connection. IP address and gateway not neede, because we will use pfSense for routing.
   
   auto vmbr0.10
    iface vmbr0.10 inet manual
    bridge_ports enp0s25.10
    bridge_stp off
    bridge_fd 0

   ![bridges](https://github.com/user-attachments/assets/7165713f-439e-48b4-b10f-00c3ba5675ba)





5. Selected **"Install Proxmox VE (Graphical)"**.  
   ![#2](https://github.com/user-attachments/assets/d5b0b579-2228-4609-b5f1-a069f4baa729)  

6. Set up **administration password** and **email**.  
   ![#3](https://github.com/user-attachments/assets/e8ab1cb2-89e1-4c2b-811f-2679ef648e68)  

7. Selected **management interface** (Ethernet), **hostname** (device name in the network), **IP address** (assigned by the DHCP server on the physical router), **Gateway** (router's IP address), and **DNS Server** (Google DNS can be used).  
   ![#5](https://github.com/user-attachments/assets/07e30c4f-bfc2-4a7c-a03b-747e910f68b8)  

8. Reviewed the **summary screen** and confirmed the installation.  
   ![#6](https://github.com/user-attachments/assets/0a62479a-7b92-436e-88b3-663e03a1ad01)  

9. After installation, **removed the USB drive** and waited for Proxmox to boot. Once booted, the system displayed the **IP address** for remote configuration.  
   ![#7](https://github.com/user-attachments/assets/2cf25042-ea4c-4578-bb39-2fdf7edefa29)  

---

## **Issues & Troubleshooting**

### **Problem 1:** Proxmox doesn’t boot after installation (only "Rescue Boot" from USB works).  
- **Error Message:** *Boot device not found.*  
- **Solution:** Changed BIOS boot mode from **Legacy** to **UEFI Hybrid**, then reinstalled Proxmox to avoid future issues.  
  ![Fix #2](https://github.com/user-attachments/assets/5ba32817-d1dd-4455-b87b-b9ee051c3319)  

### **Problem 2:** *"Virtualization support not enabled"* error message.  
- **Error Message:** `No support for hardware-accelerated KVM virtualization detected`  
  ![Problem #1](https://github.com/user-attachments/assets/068dc661-093c-4d57-93e4-ebbb0cd8dbcd)  
- **Solution:** Enabled **"Virtualization Technology (VT-x)"** in BIOS settings.  

---

## **Lessons Learned**
- BIOS settings **must** be checked before installing a hypervisor.  
- Boot mode **must** be set to **UEFI Hybrid** (not Legacy).  
- Proxmox requires **correctly assigned network interfaces** for configuration.  

  

