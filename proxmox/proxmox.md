steps to start install and start up Proxmox

1. download latest proxmox
2. create bootable image - use something like balena etcher
3. ssh into proxmox server
4. $ nano /etc/apt/sources.list
    add: 
    #not for production use 
    deb http://download.proxmox.com/debian bookworm pve-no-subscription
5. $ nano /etc/apt/sources.list.d/pve-enterprise.list
    comment out the line for enterprise
6. $ apt-get update
7. $ apt dist-upgrade
8. go to storate name > disk and set up the storage
    in the cli use fdisk to clear out disk then set up ZFS (or whatever)
    turn on smart monitor for the disk
9. turn on IOMMU (turn it on in the BIOS)
    ssh into proxmox server
    $ nano /etc/default/grub
    comment out GRUB_CMDLINE_LINUX_DEFAULT="quiet"
    add line below GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on"
    save and close
    $ update-grub
    $ nano /etc/modules
        add lines:
            vfio
            vfio_iommu_type1
            vfio_pci
            vfio_virqfd
    $ reboot
10. make proxmox vlan aware
    in proxmox gui go to server-name > network > select bridge > then click vlan aware
11. add nfs share
12. schedule backups
13. backup
14. upload KVM driver for windows winvirtio driver
15. upload OS iso
16. create NIC team - link aggregation
17. create template
18. add to cluster
