# ✅ **Fix: Disable KVM so VirtualBox can use AMD-V**

Run these commands on your **host machine (Ubuntu/Linux)**:

### **1. Stop KVM modules**

`sudo systemctl stop libvirtd 
sudo systemctl disable libvirtd`

### **2. Unload the KVM modules**

`sudo modprobe -r kvm_amd sudo modprobe -r kvm`

If it says “module is in use”, force unload:

`sudo rmmod kvm_amd 
sudo rmmod kvm`