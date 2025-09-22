# VMware Tools Tutorial (Parrot OS Example)

## 1. Prerequisites

* VMware Workstation Pro installed on your host
* A Linux guest OS (e.g., Parrot OS) running in a VM
* Internet connection (for installing packages)

---

## 2. Install VMware Tools in Parrot OS

1. Boot your Parrot OS VM.
2. Open a terminal and update the system:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
3. Install the VMware integration packages:

   ```bash
   sudo apt install open-vm-tools open-vm-tools-desktop -y
   ```

---

## 3. Enable Guest Isolation (Clipboard & Drag-and-Drop)

1. Shut down the VM.
2. In VMware Workstation, open **Settings** → **Options** → **Guest Isolation**.
    ![alt text](/img/VMware/guestIso.png)
3. Check:

   * ✅ Enable drag and drop
   * ✅ Enable copy and paste
4. Save and start the VM.

---

## 4. Verify

* After reboot, test copy-paste between host and VM in both directions.
