# **Objective 4.1: VLANs**

## Description
This objective focuses on configuring VLANs for different network zones and integrating them with Proxmox using network bridges. The VLAN IDs were assigned for DMZ (VLAN 30), LAN (VLAN 20), and ADMIN (VLAN 10). After understanding how interfaces relate to each other in Proxmox, I successfully created the necessary subinterfaces and bridges. The configuration was initially broken and restored for a better understanding.

## Actions Taken

1. **Decided on VLAN IDs for each zone:**  
   - DMZ zone = "VLAN 30"  
   - LAN = "VLAN 20"  
   - ADMIN = "VLAN 10"  
   ![VLAN scheme](https://github.com/user-attachments/assets/bea93cfc-c317-4faa-b650-ef7f97e7f37a)

2. **Identified Proxmox physical interface and bridge:**  
   - Proxmox uses the physical interface "enp0s25" and a bridge called "vmbr0."  
   ![Network understanding](https://github.com/user-attachments/assets/7779f008-2e03-42c0-9430-01ef17071e2a)

3. **Opened the network configuration file**:  
   I accessed the default configuration file after the Proxmox installation using:  
   `nano /etc/network/interfaces`  
   ![Network configuration](https://github.com/user-attachments/assets/1a0118c3-7aa7-4bd9-b1c5-53032825dbae)

4. **Created subinterfaces for each VLAN**:  
   In the `/etc/network/interfaces` file, I added subinterfaces for each VLAN (10, 20, 30) to use "enp0s25" as the raw device for tagging VLAN packets:
   
      auto enp0s25.10
      iface enp0s25.10 inet manual
      vlan-raw-device enp0s25
   
   ![Subinterfaces](https://github.com/user-attachments/assets/4bc3dca6-72ea-4fd5-a6ad-1fc1944c9ff9)

6. **Created bridges for each subinterface**:  
I created bridges for each subinterface. No IP address or gateway was required because pfSense would handle routing:  

      auto vmbr10
      iface vmbr10 inet manual
      bridge-ports enp0s25.10
      bridge-stp off
      bridge-fd 0

   ![Bridges](https://github.com/user-attachments/assets/d688cb8f-f6ea-4c0e-93df-f7b8d40b05c5)

6. **Saved and closed the configuration file**:  
After saving the changes (CTRL + S), I restarted the network service with:  
`systemctl restart networking`  
If the connection to Proxmox was restored within a few seconds, the configuration was successful (see [Problem 1](https://github.com/sapan322/Cybersecurity-Portfolio/blob/main/Project%20Proxmox-Virtual-Network%20/Objective_4%20/README.md#problem-1))  

![Proxmox environment](https://github.com/user-attachments/assets/8fa6d1f7-50f3-4bd1-a324-848f5fbf37d5)

7. **Checked the new interfaces**:  
I ran the command `ip a` to verify that the subinterfaces and bridges were created successfully. The output should show `enp0s25.10`, `enp0s25.20`, `enp0s25.30` and the bridges `vmbr10`, `vmbr20`, `vmbr30`.  
![IP addresses](https://github.com/user-attachments/assets/d787aecd-2496-4d37-999c-2eb90e3e3ebc)

## **Issues & Troubleshooting**

### **Problem 1:**  
On the first configuration attempt, I made a couple of errors, causing the inability to reconnect to the `vmbr0` IP address after restarting network services.  
- **Solution:**  
I accessed the server directly, manually restored the configuration to the default settings, and was able to reconnect remotely.

---

## **Lessons Learned**
- Understanding Proxmox interface relationships and how to configure them.
- Creating subinterfaces and bridges to handle VLANs.
- Manual configuration of Proxmox networking.
- How the physical interface (`enp0s25`) and the bridge (`vmbr0`) interact to enable VLAN tagging and network separation.
