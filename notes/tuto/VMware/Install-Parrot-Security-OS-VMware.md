# Install Parrot Security OS on VMware Workstation

A concise step-by-step guide to install **Parrot Security OS** in **VMware Workstation Pro**.

> ⚠️ This guide installs Parrot inside a virtual machine. Nothing here modifies your host system if you follow the VM steps. Use snapshots before trying risky actions.

---

## Table of contents

* [Download Parrot ISO](#download-parrot-iso)
* [Create a New Virtual Machine](#create-a-new-virtual-machine)
* [Boot the VM](#boot-the-vm)
* [Install Parrot Security OS](#install-parrot-security-os)
* [Finish and first boot](#finish-and-first-boot)
* [Tips and recommended settings](#tips-and-recommended-settings)
* [Next steps](#Next-steps)

---

## Download Parrot ISO

1. Open the official website: [https://parrotsec.org](https://parrotsec.org)
   ![Parrot OS webpage](../../img/VMware/parOSWebpage.png)
2. Go to **Download → Live → Security** and select the appropriate ISO (64-bit most likely).
3. Click **Download ISO image** and wait for the download to complete.

---

## Create a New Virtual Machine

1. Launch **VMware Workstation Pro**.
2. Click **Create a New Virtual Machine**.
3. Choose **Installer disc image file (iso)** and browse to the Parrot ISO you downloaded.
   ![Create New VM](../../img/VMware/VMwareCreateNewVM.png)
4. Give the VM a name you will recognize.
5. Configure disk size (optional): change the maximum disk size if you want to allocate more or less space.
   ![Max Disk VMware](../../img/VMware/maxDiskVMware.png)
6. Adjust memory and CPU allocations based on your host resources (see Tips below).

---

## Boot the VM

1. Start the newly created VM.
2. From the boot menu, choose **Try / Install** to load the live session.
   ![Try ParrotOS](../../img/VMware/TryParrotOS.png)

---

## Install Parrot Security OS

1. In the live environment, launch **Install Debian**.
   ![Install Debian](../../img/VMware/IntsallDebian.png)
2. Select your **language**, **location**, and **keyboard layout**.
3. When prompted about partitioning, selecting **Erase disk** will only affect the VM virtual disk. Confirm if that is what you want.
   ![Erase Disk](../../img/VMware/eraseDisk.png)
4. Enter your **full name**, **username**, and **password** when requested. Keep a note of these credentials.
5. Start the installation and wait for it to complete (several minutes).

---

## Finish and first boot

1. After installation finishes, choose to **restart the VM**.
2. Remove or unmount the ISO from the virtual CD/DVD if VMware prompts you.
3. Boot with the installed system and log in with the username and password you created.
4. You now have Parrot Security OS running in VMware.

---

## Tips and recommended settings

* Memory: allocate at least **2–4 GB** for smoother performance (more if your host allows).
* CPU: 1–2 vCPUs is fine for basic use; increase if you plan heavy tasks.
* Disk: 20–40 GB recommended for typical pentest tools and updates.
* Snapshots: take a snapshot before making major changes or installing risky software.
* Networking: usually set to NAT for internet access while isolating the VM; use Host-only if you want a network-isolated environment.
* VMware Tools / Open VM Tools: install them in the guest for better performance and shared clipboard if needed.

## Next steps

Now that Parrot Security OS is installed, I recommand you to:

* [Enable clipboard sharing, better performance and other](./Vmware-Tools.md)