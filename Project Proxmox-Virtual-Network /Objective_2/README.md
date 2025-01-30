# **Objective 2: Proxmox VE Installation**

## Description
Install **Proxmox VE**, configure network settings, understand which network interfaces Proxmox uses as a router, and troubleshoot hardware issues.

## Actions Taken
1. Changed boot mode from **Legacy** to **UEFI Hybrid** (*see Problem 1*).  
   ![Fix #2](https://github.com/user-attachments/assets/3ee5aecf-6600-4f6e-a040-52113bc3ecfa)  

2. Enabled **Virtualization Technology (VT-x)** in BIOS settings (*see Problem 2*).  
   ![Fix #1](https://github.com/user-attachments/assets/5c9efb65-bc66-4e6b-9fbb-eb8de9794558)  

3. Booted from **USB drive** with the Proxmox installer.  
   ![#1](https://github.com/user-attachments/assets/431a5325-6c84-4553-83f5-c77fe12b96fa)  

4. Selected **"Install Proxmox VE (Graphical)"**.  
   ![#2](https://github.com/user-attachments/assets/d5b0b579-2228-4609-b5f1-a069f4baa729)  

5. Set up **administration password** and **email**.  
   ![#3](https://github.com/user-attachments/assets/e8ab1cb2-89e1-4c2b-811f-2679ef648e68)  

6. Selected **management interface** (Ethernet), **hostname** (device name in the network), **IP address** (assigned by the DHCP server on the physical router), **Gateway** (router's IP address), and **DNS Server** (Google DNS can be used).  
   ![#5](https://github.com/user-attachments/assets/07e30c4f-bfc2-4a7c-a03b-747e910f68b8)  

7. Reviewed the **summary screen** and confirmed the installation.  
   ![#6](https://github.com/user-attachments/assets/0a62479a-7b92-436e-88b3-663e03a1ad01)  

8. After installation, **removed the USB drive** and waited for Proxmox to boot. Once booted, the system displayed the **IP address** for remote configuration.  
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

  
