install truenas notes


on core need legacy boot in proxmox
on scale need efi boot in proxmox

go to network settings and update the ip address to what you want it to be

create zfs in proxmox, then create storage in proxmox - i used ZFS 

go to hardware and pass that into the VM

inside of truenas:
set up user
set up storage pool

for nfs in ubuntu
$ sudo apt-get install nfs-common

After installing the module, connect to an NFS share by entering sudo mount -t nfs {IPaddressOfTrueNASsystem}:{path/to/nfsShare} {localMountPoint}. Where {IPaddressOfTrueNASsystem} is the remote TrueNAS system IP address that contains the NFS share, {path/to/nfsShare} is the path to the NFS share on the TrueNAS system, and {localMountPoint} is a local directory on the host system configured for the mounted NFS share. For example, sudo mount -t nfs 10.239.15.110:/mnt/Pool1/NFS_Share /mnt mounts the NFS share NFS_Share to the local directory /mnt.

in truenas under the nfs you need to set mapall user to root and map all group to root


in the vm create a mount folder i.e. /nfs/pve-vm-truenas_storage

update fstab (/etc/fstab) with the following:
    10.20.200.210:/mnt/pve-vm-truenas_storage               /nfs/pve-vm-truenas_storage      nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0

testing to see if it is mounted: 
    $ df -h