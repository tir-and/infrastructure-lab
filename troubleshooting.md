# Troubleshooting Log

---

## Session 2 - Linux Server and SSH

### VM boots into installer upon Ubuntu installation

**When it happend**
After Ubuntu Server instalaiton completed and the VM restarted, the VM installer started again instead of booting into the installed system.

**Cause**
The Ubuntu Server ISO was still attached to the VM virtual optical drive. 

**How I fixed it**

1. Shut down the VM (Machine > Close > Power off)
2. Go to VM Setings > Storage
3. Click the optical drive
4. Click the small icon and select Remove Disk from Virtual Drive
5. Start the VM again

The VM booted correctly in the installed Ubuntu Server.

**How to prevent it**
During Ubuntu Server installation final steps, remove the ISO from virtual optical drive.

**Lesson**
Alwways check the optical drive in Settings after a fresh instalation 
