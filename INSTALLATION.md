# SYSTEM INSTALLATION

## Configuration de VirtualBox
**Name :** Born2BeRoot  
**Folder :** /home/nramaan/sgoinfre/VirtualBox VMs  
**ISO Image :** /home/nramalan/Downloads/debian-13.3.0-amd64-netinst.iso


## Disk Partition
### 1. Initial Disk Setup

When the installer asks for the partitioning method, select **Manual**.

1. **Create `/boot` partition:**
* Select your free space (sda).
* Create a new partition of **500M**.
* Type: **Primary**.
* Use as: **Ext4**.
* Mount point: **`/boot`**.


2. **Create the Encrypted Container:**
* Select the remaining free space.
* Create a new partition (this will become `sda5` in an extended partition).
* Use as: **physical volume for encryption**.


3. **Configure encrypted volumes:**
* Select "Configure encrypted volumes" at the top.
* Select your partition and "Create encrypted volumes".
* Set your **Disk Encryption Password** (don't lose this!).
* Finish. You will now see `sda5_crypt` in the menu.

---

### 2. LVM Configuration (The Logical Layers)

Now you need to put the LVM "inside" the encrypted space.

1. Select **Configure the Logical Volume Manager**.
2. **Create Volume Group:**
* Name it: `LVMGroup`.
* Select the encrypted space (`/dev/mapper/sda5_crypt`) as the backing device.


3. **Create Logical Volumes (LVs):**
Create each of the following LVs within `LVMGroup`:

| Name      | Size           |
| --------- | -------------- |
| `root`    | 10G            |
| `swap`    | 2.3G (or 2.4G) |
| `home`    | 5G             |
| `var`     | 3G             |
| `srv`     | 3G             |
| `tmp`     | 3G             |
| `var-log` | 4G             |

---

### 3. Mapping Mount Points

Once the LVs are created, you will return to the main manual partitioning screen. You must now tell Debian how to use each logical volume. For **each** LV listed under `LVMGroup`, select it and set:

* **root:** Use as `Ext4`, Mount point `/`.
* **swap:** Use as `swap area`.
* **home:** Use as `Ext4`, Mount point `/home`.
* **var:** Use as `Ext4`, Mount point `/var`.
* **srv:** Use as `Ext4`, Mount point `/srv`.
* **tmp:** Use as `Ext4`, Mount point `/tmp`.
* **var-log:** Use as `Ext4`, Mount point `/var/log`.

---

### 4. Why this matches your screenshot

The hierarchy in your `lsblk` output shows the **Physical -> Crypt -> LVM** nesting:

1. **`sda5`**: The physical partition on the disk.
2. **`sda5_crypt`**: The LUKS encryption layer.
3. **`LVMGroup-xxx`**: The logical partitions inside the encrypted "vault."

### Pro-Tip for the Evaluation

The evaluator will ask you why you have a separate partition for `/var/log`.

* **Answer:** "To prevent a sudden surge in log files from filling up the entire system (the root partition), which would crash the OS. By isolating it, only the log partition gets full."

Would you like the specific `sudo` configuration steps for the **Born2beRoot** requirements next?