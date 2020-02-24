#### NFS
#### centos
```bash
yum -y install nfs-utils 
mkdir /nfsroot 
vim /etc/exports
```

#### ubuntu 
```bash
sudo apt-get update
sudo apt install nfs-kernel-server
sudo mkdir -p /mnt/sharedfolder
sudo chown nobody:nogroup /mnt/sharedfolder
sudo chmod 777 /mnt/sharedfolder
sudo vim /etc/exports
/mnt/sharedfolder <subnet>/24(rw,sync,no_subtree_check)
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

Add the line below
```
 /nfsroot 192.168.5.0/24(ro,no_root_squash,no_subtree_check) 
```
```bash
exportfs -r 
/etc/init.d/nfs start 
showmount -e 
```
