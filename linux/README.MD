# Admin linux

## hostname

```bash
sudo vim /etc/hostname
sudo vim motd
sudo reboot
```

## user

### changement de user

```bash
su
su root
su -  ##change les variable environnement (lang)
su - root
```

### creer un utilisateur (redhat)

```bash
useradd toto ##  sudo adduser (debian ubuntu)
passwd toto
```

### creer un groupe et un utilisateur(redhat)

```bash
groupadd g2
useradd -g g2 titi   ##  -G grpInvite
passwd titi
```

### sous unbuntu pour avoir acces a root

```bash
sudo passwd root 
```

## disque et partition

### voir les systeme de fichier monter

```bash
df -hT

```

### lister les partitions

```bash
fdisk -l
blkid
lsblk
```

### voir partition

```bash
more /proc/partitions
fdisk -l /dev/sda
```

### creation partition

```bash
fdisk /dev/sda
partx ## notifie le kernel
```

### creation systeme de fichier et formatage

```bash
mkfs.ext3 /dev/sda1
mkfs.ext4 /dev/sda2
mkfs.xfs /dev/sda3
mkfs.xfs /dev/monGroupeDeDisk1/mesVideos1  ##LVM
```

### montage volume

```bash
mount /dev/sdc6 /home/bob/HD
chown bob:g1 /home/bob/HD
vi /etc/fstab    ##  montage au demarage  
ls -lha /dev/disk/by-uuid/  ##  trouver les UUID
umount /home/bob/HD   ##  test
mount -a
```

### montage volume ntfs

```bash
sudo apt-get install ntfs-3g
sudo mount -t ntfs-3g  /dev/sdg2 hdextern
```

### LVM

#### voir les groupe de volume,volume phy et volume log

```bash
vgdisplay -v  
pvdisplay
lvdisplay
```

#### extention d'un LVM ?? a voir

```bash
lgextend -L +10G -r /dev/monGroupeDeDisk1/mesVideos1
```

#### création d'un LVM

```bash
more /proc/partitions
pvcreate /dev/sdb1
vgcreate lvm /dev/sdb1
lvcreate -l 100%FREE -n data lvm
mkfs.xfs /dev/lvm/data
cd /
mkdir home
mount /dev/lvm/data /home/
```

#### modif fstab

```bash
vi /etc/fstab

/dev/mapper/lvm-data /home               xfs     defaults        0       0

df -h
umount /home
df -h
mount -a
```

------------------------------------------------------------------------------------

## surveillance processus

### voir les processus de tous les utilisateurs

```bash
ps -faux
htop
atop
ps -edf
pstree
```

### user courant

```bash
pstree -ap $USER
```

### identifie le process utilisant un fichier ou un socket

```bash
fuser -k /HD1
```

### utilisation fichier par process

```bash
lsof -p <pid>
```

### recupération environnement d'un process

```bash
cat /proc/$PID/environ | tr -s "\0" "\n"
```

------------------------------------------------------------------------------------

## info general

```bash
neofetch
lshw
```

## surveillance reseau

```bash
iftop
netstat -tunlp
```

## mémoire vive

```bash
free
free -h:q
```

## info cpu

```bash
arch
lscpu
cat /proc/cpuinfo
```


## info IO (HDD SSD)

```bash
iotop
```

## info version linux

```bash
uname -a
cat /etc/debian_version 
```

## info command

```bash
type ls
which ls
```

## find

```bash
find ./ -name "core*" -mtime -1
```

------------------------------------------------------------------------------------

## compilation C

### gdb

```bash
gdb -c <core_file> <binary_exe>
file core
```

### verif bin

```bash
strings <file>
```

### dependance

```bash
ldd <binary_exe>
```

### voir objet

```bash
nm <binary_exe>
readelf -s <binary_exe>
```

### effacer objet

```bash
strip <binary_exe>
```

### ou sont generer les core ?

```bash
cat /proc/sys/kernel/core_pattern
/kernel-core/core.%e.%p.%h.%t

core.ftm_oftp.13413.sv1.hubmaster.net.1615543194

cat /proc/sys/kernel/core_pattern
core
```

------------------------------------------------------------------------------------

## TAR

```bash
tar -cvzf /tmp/nom_archive.tgz --exclude="*.log" --exclude="core*" ./*

# on copie les liens symbolique
tar -cvzf archive.tgz rep

# on copie les fichier poité par les liens symbolique: -h
tar -cvzhf archive.tgz rep

tar -xvzf .tgz

tar -xvf .tar
```

## SSH

install rsa key

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub -p 22 user@machine
```

## RSYNC

sync dossier local vers distant

```bash
rsync -vaz mon_repo root@ma_machine:/home/user

```

exclude .git

-C, --cvs-exclude           auto-ignore files in the same way CVS does

```bash
rsync -vazC mon_repo root@ma_machine:/home/user

```

## TCP dump

```bash
tcpdump -w dump -s 2000 host host_a_surveiller
```

## OPEN SSL

```bash
#lister le contenu d'un fichier pkcs7-data

openssl asn1parse -i -dump -inform der -in mon_fichier 
```

## CSH

mode debug

```bash
csh -bvx monscript.sh

```

## extinction reboot

```bash
init 0
halt
shutdown

init 6
reboot
```

## variable et environnement

```bash
env #affiche les variable d'environnement
set #affiche les variable
myvar=hello
export myvar
unset myvar #supprime 
```

## changement charset

```bash
apt-get install locales
dpkg-reconfigure locales

cat /etc/default/locale
echo $LANG
```

## affichage specifique

### hexadecimal

```bash
ls -l | od -tx1c
xxd file.txt
```

### affichage en 80 collonnes

```bash
fold test.txt
```

## divers

```bash
touch fic{1,2,3}
LANG=C man ls  #man en vo
\rm fichier  #pas d'alias
rm "mon fichier à moi"
rm mon\ fichier à\ moi
mkdir rep1 ; cd !* #creer un fichier et retrer dedans
#  recherche ds /home de fichier dont le nom est bob  sans messge d'erreur 
find /home -name bob 2>/dev/null
#  recherche ds / de fichier * sans messge d'erreur 
find /bin/ -name "*" >commande 2>/dev/null

find /bin/ -name "*" 2>/dev/null | tee commande | less

alias  #affiche les alias

echo mon adresse ip est $(ip a | grep 192.168.2 | cut -c10-21)
ip a  #ifconfig

# dans .bashrc
PATH=$PATH:. #ajoute au PATH le rep courant

ps -ef  #affiche les processus
file fichier #donne le type de fichier
```
