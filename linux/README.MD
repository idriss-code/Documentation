su
su root
su - 	##change les variable environnement (lang)
su - root

##  mémoire vive
free
free -h:q

## info cpu
arch
lscpu
cat /proc/cpuinfo

##  creer un utilisateur (redhat)
useradd toto ##  sudo adduser (debian ubuntu)
passwd toto

##  creer un groupe et un utilisateur(redhat)
groupadd g2
useradd -g g2 titi   ##  -G grpInvite
passwd titi

##  sous unbuntu pour avoir acces a root
sudo passwd root 

##  lire le type de fichier
file fichier

##  voir les systeme de fichier monter
df -hT

## lister les partitions
fdisk -l
blkid
lsblk

##  voir partition
more /proc/partitions
fdisk -l /dev/sda

##  creation partion
fdisk /dev/sda

##  creation systemede fichier et formatage
mkfs.ext3 /dev/sda1
mkfs.ext4 /dev/sda2
mkfs.xfs /dev/sda3
mkfs.xfs /dev/monGroupeDeDisk1/mesVideos1 	##LVM

##  montage volume
mount /dev/sdc6 /home/bob/HD
chown bob:g1 /home/bob/HD
vi /etc/fstab				##  montage au demarage  
ls -lha /dev/disk/by-uuid/		##  trouver les UUID
umount /home/bob/HD			##  test
mount -a

##  montage volume ntfs
sudo apt-get install ntfs-3g
sudo mount -t ntfs-3g  /dev/sdg2 hdextern

##  LVM
## voir les groupe de volume,volume phy et volume log
vgdisplay -v  
pvdisplay
lvdisplay

#extention d'un LVM ?? a voir
lgextend -L +10G -r /dev/monGroupeDeDisk1/mesVideos1

## création d'un LVM
more /proc/partitions
pvcreate /dev/sdb
vgcreate lvm /dev/sdb
lvcreate -l 100%FREE -n data lvm
mkfs.xfs /dev/lvm/data
cd /
mkdir home
mount /dev/lvm/data /home/

### modif fstab
vi /etc/fstab

/dev/mapper/lvm-data /home               xfs     defaults        0       0

df -h
umount /home
df -h
mount -a

## extinction reeboot

init 0
halt
shutdown

init 6
reboot

## identifie le process utilisant un fichier ou un socket
fuser -k /HD1

# utilisation fichier par process
lsof -p <pid>

#divert 
ls -l | od -tx1c

# find
find ./ -name "core*" -mtime -1

# surveillance processus
##  voir les processus de tous les utilisateurs
ps -faux
htop
ps -edf
pstree

## user courant
pstree -ap $USER

#surveillance reseau
iftop
netstat -tunlp

------------------------------------------------------------------------------------

# C compil

#gdb
gdb -c <core_file> <binary_exe>
file core

# verif bin
strings <file>

# dependance
ldd <binary_exe>

#voir objet
nm <binary_exe>
readelf -s <binary_exe>

#effacer objet
strip <binary_exe>



------------------------------------------------------------------------------------
#TAR
tar -cvzf /tmp/kit_pkmaster_v1_64-180.tgz --exclude="*.log" --exclude="core*" ./*

## follow symlinks
tar -cvzf archive.tgz rep

tar -xvzf .tgz

tar -xvf .tar

------------------------------------------------------------------------------------

## ou sont generer les core ?

cat /proc/sys/kernel/core_pattern
/kernel-core/core.%e.%p.%h.%t

core.ftm_oftp.13413.sv1.hubmaster.net.1615543194

cat /proc/sys/kernel/core_pattern
core

-------------------------------------------------------------------------------------

#SSH 
##install rsa key

ssh-copy-id -i ~/.ssh/id_rsa.pub -p 22 user@machine

-------------------------------------------------------------------------------------

CSH mode debug

csh -bvx monscript.sh

------------------------------------------------------------------------------------

#RSYNC

##exclude .git 

rsync -vaz mon_repo root@ma_machine:/home/user

------------------------------------------------------------------------------------

#TCP dump

tcpdump -w dump -s 2000 host host_a_surveiller

------------------------------------------------------------------------------------

#OPEN SSL

lister le contenu d'un fichier pkcs7-data

openssl asn1parse -i -dump -inform der -in mon_fichier 

------------------------------------------------------------------------------------

touch fic{1,2,3}
LANG=C man ls		#man en vo
\rm fichier		#pas d'alias
rm "mon fichier à moi"
rm mon\ fichier à\ moi
mkdir rep1 ; cd !*	#creer un fichier et retrer dedans
#  recherche ds /home de fichier dont le nom est bob  sans messge d'erreur 
find /home -name bob 2>/dev/null
#  recherche ds / de fichier * sans messge d'erreur 
find /bin/ -name "*" >commande 2>/dev/null

find /bin/ -name "*" 2>/dev/null | tee commande | less

alias		#affiche les alias
env		#affiche les variable d'env
set | less	#affiche les variable
echo mon adresse ip est $(ip a | grep 192.168.2 | cut -c10-21)
ip a		#ifconfig

# dans .bashrc
PATH=$PATH:.	#ajoute au PATH le rep courant

ps -ef		#affiche les processus
file fichier	#donne le type de fichier