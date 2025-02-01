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





4. 

5.

6. 

7. 

## **Issues & Troubleshooting**

### **Problem 1:**  

- **Solution:**  


---

## **Lessons Learned**

