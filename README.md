# PROJECT-6
WEB SOLUTION WITH WORDPRESS

**Launch an EC2 instance that will serve as “Web Server”.**
![image](https://user-images.githubusercontent.com/113097621/213337867-5881a4c9-d2f9-45c9-a45f-63165215d6be.png)

**Use lsblk command to inspect what block devices are attached to the server**
![image](https://user-images.githubusercontent.com/113097621/213338098-c3475081-9c2b-43c7-a6c6-c22cdbc77ff3.png)

**Use gdisk utility to create a single partition on each of the 3 disks**
sudo gdisk /dev/xvdf
![image](https://user-images.githubusercontent.com/113097621/213338304-b4dfc5ce-8734-44e1-a073-747db89accb0.png)

**Use pvcreate utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM**
![image](https://user-images.githubusercontent.com/113097621/213339459-88b88d59-ab20-430e-b5b2-609206a3f4cb.png)

**Verify that your Physical volume has been created successfully by running sudo pvs**
![image](https://user-images.githubusercontent.com/113097621/213339610-dda4a0a4-310d-4d14-a769-a3baa6358b28.png)

**Use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg**
![image](https://user-images.githubusercontent.com/113097621/213340313-2392bf59-cf68-4c61-829b-262ac8494c8c.png)

**Verify that your VG has been created successfully by running sudo vgs**
![image](https://user-images.githubusercontent.com/113097621/213340482-638101b0-03cf-46b9-bb26-1cb1245ceeb2.png)

**Use lvcreate utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv Use the remaining space of the PV size. NOTE: apps-lv will be used to store data for the Website while, logs-lv will be used to store data for logs.**
![image](https://user-images.githubusercontent.com/113097621/213340698-95dcf603-5c66-44e1-b016-1a9160ae1847.png)

**Verify that your Logical Volume has been created successfully by running sudo lvs**
![image](https://user-images.githubusercontent.com/113097621/213340905-e7eef604-dec1-4c51-abe2-7856513ee919.png)

**Verify the entire setup**
![image](https://user-images.githubusercontent.com/113097621/213341184-69f1ccf8-1262-4746-9b81-5e2ea69d348b.png)

sudo lsblk 
![image](https://user-images.githubusercontent.com/113097621/213341385-b6e2239e-7c5e-46cf-962f-88fc9ac89ff5.png)

**Use mkfs.ext4 to format the logical volumes with ext4 filesystem**
![image](https://user-images.githubusercontent.com/113097621/213341925-4e4fa90c-5cc6-476b-bc32-52a5911622bf.png)

**Create /var/www/html directory to store website files**
sudo mkdir -p /var/www/html

**Create /home/recovery/logs to store backup of log data**
sudo mkdir -p /home/recovery/logs
![image](https://user-images.githubusercontent.com/113097621/213342969-f5c4029e-2867-452c-84b0-847d404f096c.png)

**Mount /var/www/html on apps-lv logical volume**
sudo mount /dev/webdata-vg/apps-lv /var/www/html/


Restore log files back into /var/log directory
sudo rsync -av /home/recovery/logs/. /var/log

**update the `/etc/fstab` file**
sudo blkid
![image](https://user-images.githubusercontent.com/113097621/213346365-5ad1891c-6547-4ca1-a4da-2a9964dd0181.png)







