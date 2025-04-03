# VFIO-GPU-Passthrough-Muxless

1. lspci -nnv | grep NVIDIA

01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GA106M [GeForce RTX 3060 Mobile / Max-Q] [10de:2520] (rev a1) (prog-if 00 [VGA controller])
01:00.1 Audio device [0403]: NVIDIA Corporation GA106 High Definition Audio Controller [10de:228e] (rev a1)

2. /etc/default/grub or if your using systemd-boot /boot/loader/entries/linux.conf

vfio-pci.ids=10de:2520,10de:228e intel_iommu=on

sudo update-grub

3. /etc/modules or /etc/mkinitcpio.conf 

vfio
vfio_iommu_type1
vfio_pci

4. /etc/modprobe.d/blacklist-nvidia.conf

blacklist nvidia
blacklist nvidia_drm
blacklist nvidia_modeset
blacklist nvidia_uvm

sudo mkinitcpio -P 

5. Passthrough PCI (GPU) 01:00.0 and 01:00.1 in Virt-Manager

6. on your Host install Looking Glass Client with yay -S looking-glass on Arch Linux on other distribution compile it manually 

7. on your Guest (Windows VM) install GPU Drivers, Looking Glasss Host and Virtual-Display-Driver (Select your GPU for you Virtual Display)

8. and run Looking Glass with that argument : looking-glass-host.exe dxgi:output=2 (Display Number)

9. run Looking Glass Client on your Host with looking-glass-client -F for fullscreen

10. go to ms-settings: and set your Desktop only on the second Display .

11. Normally now you got the 3D Acceleration of your GPU Passthrough

























