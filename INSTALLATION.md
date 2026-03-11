# Debian SYSTEM INSTALLATION

## VirtualBox Configuration
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

## Configurer l'Outil de gestion des paquets

Sur la question **Fault-il analyser d'autres supports d'installation ?**, il faut toujours dire `Non`

Sur la question **Fault-il utiliser un miroir sur le reseau ?**, il faut toujours dire `Non`

Sur la question **Souhaitez-vous participer a l'etude statistique sur l'utilisation des paquets ?**, il faut toujours dire `Non`

## Selection des logiciels

Selectionner seulement :
 - Serveur SSH
 - Utilitaires usuels du systeme

Il faut decocher les autres pour ne pas installer l'environnement graphique ou l'environnement de bureau