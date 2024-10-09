# UNIX-TP1
Premier TP en cours d'UNIX


# Lancement de la machine virtuelle

>> Vbox LicenceProPreInstalled-2024

### Connexion en root à la machine

>> login : root
>> mdp : root

####  Configuration de apt.conf

Ouverture du fichier

>> nano /etc/apt/apt.conf

Modification du fichier en mettant le bon Proxy

[ Acquire::http::Proxy "http://proxy.ufr-info-p6.jussieu.fr:3128"; ]

Mise à jour de apt

>> apt update

## 2 - Post-Installation

### Installation de SSH

>> apt install ssh

Verification des paquets SSH

>> apt search ssh

### Changement de configuration SSH permettant les connexions root à distance

Ouverture de sshd_config

>> nano /etc/ssh/sshd_config

Aller à la ligne correspondante

>> #PermitRootLogin prohibit-password

Modifier

>> PermitRootLogin yes

Ajouter 

>> PasswordAuthentication yes

### Connexion à la machine virtuelle

Connaitre l'adresse de la machine virtuelle

>> ip a

Connexion à la machine virtuelle via le terminal

>> ssh root@10.20.0.180

### Paquets 

Vérifier le nombre de paquets

>> dpkg -l | wc -l

### Utilisation de l'espace 

>> df -h

La racine représente moins de 1 GO d'espace

#### Resultat :

Sys. de fichiers Taille Utilisé Dispo Uti% Monté sur
udev               4,9G       0  4,9G   0% /dev
tmpfs              995M    572K  994M   1% /run
/dev/sda1          9,1G    1,6G  7,0G  19% /
tmpfs              4,9G       0  4,9G   0% /dev/shm
tmpfs              5,0M       0  5,0M   0% /run/lock
/dev/sda2          3,6G     40K  3,4G   1% /tmp
/dev/sda3          921M     25M  833M   3% /var/log
tmpfs              995M       0  995M   0% /run/user/0

### Locales

>> echo $LANG

#### Resultat :

fr_FR.UTF-8

### Nom machine

>> hostname

#### Resultat :

serveur-correction

### Nom de domaine

>> hostname -d

#### Resultat :

Pas de retour

### Verification emplacement dépots

>> cat /etc/apt/sources.list | grep -v -E '^#|^$'

####Resultat :

deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware

### passwd/shadow

>> cat /etc/shadow | grep -vE ':\*:|:!\*:'

#### Resultat :

root:$y$j9T$ioHBonpp60OIKIrc26rUd/$c1nIbMAvKsIxUAgrCB2qaePUV4NwHbN.v76/eMs1cXC:20004:0:99999:7:::
messagebus:!:19635::::::
sshd:!:20004::::::

### Comptes utilisateurs

>> cat /etc/shadow | grep -vE 'nologin|sync'

#### Resultat :

root:$y$j9T$ioHBonpp60OIKIrc26rUd/$c1nIbMAvKsIxUAgrCB2qaePUV4NwHbN.v76/eMs1cXC:20004:0:99999:7:::
daemon:*:19635:0:99999:7:::
bin:*:19635:0:99999:7:::
sys:*:19635:0:99999:7:::
games:*:19635:0:99999:7:::
man:*:19635:0:99999:7:::
lp:*:19635:0:99999:7:::
mail:*:19635:0:99999:7:::
news:*:19635:0:99999:7:::
uucp:*:19635:0:99999:7:::
proxy:*:19635:0:99999:7:::
www-data:*:19635:0:99999:7:::
backup:*:19635:0:99999:7:::
list:*:19635:0:99999:7:::
irc:*:19635:0:99999:7:::
_apt:*:19635:0:99999:7:::
nobody:*:19635:0:99999:7:::
systemd-network:!*:19635::::::
messagebus:!:19635::::::
sshd:!:20004::::::

### fdisk -l et fdisk -x

>> fdisk -l

#### Resultat :

Disque /dev/sda : 20 GiB, 21474836480 octets, 41943040 secteurs
Modèle de disque : HARDDISK        
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
Type d'étiquette de disque : gpt
Identifiant de disque : 3ED2EBFD-8995-4690-8EEF-8C65108F2339

Périphérique    Début      Fin Secteurs Taille Type
/dev/sda1        2048 19531775 19529728   9,3G Système de fichiers Linux
/dev/sda2    19531776 27344895  7813120   3,7G Système de fichiers Linux
/dev/sda3    27344896 29298687  1953792   954M Système de fichiers Linux
/dev/sda4    29298688 41940991 12642304     6G Partition d'échange Linux

>> fdisk -x

#### Resultat :

Disque /dev/sda : 20 GiB, 21474836480 octets, 41943040 secteurs
Modèle de disque : HARDDISK        
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
Type d'étiquette de disque : gpt
Identifiant de disque: 3ED2EBFD-8995-4690-8EEF-8C65108F2339
Premier LBA utilisable: 34
Dernier LBA utilisable: 41943006
LBA alternatif: 41943039
LBA de départ des entrées de partition: 2
Entrées de partitions allouées: 128
LBA de fin des entrées de partition: 33

Périphérique    Début      Fin Secteurs Type-UUID                            UUID                                 Nom Attr.
/dev/sda1        2048 19531775 19529728 0FC63DAF-8483-4772-8E79-3D69D8477DE4 7202EEDF-B999-47CC-BE80-70C80C2C83B0 la racine
                                                                                                                      
/dev/sda2    19531776 27344895  7813120 0FC63DAF-8483-4772-8E79-3D69D8477DE4 346085A8-A5AE-48BA-B6B7-BDA598DD7465 espace tempo
                                                                                                                      
/dev/sda3    27344896 29298687  1953792 0FC63DAF-8483-4772-8E79-3D69D8477DE4 8F880167-DE17-4896-BB95-EE5AAC9E2E9A les logs
                                                                                                                      
/dev/sda4    29298688 41940991 12642304 0657FD6D-A4AB-43C4-84E5-0933C84B4F4F 68C18C76-59A6-45DF-A745-F87FD1D412DA ma swap


#### EXPLICATIONS :

fdisk -l sert à afficher les les tables de partitions du disque, sa taille, le type d'etiquette de disque (gpt) et d'autres infos

fdisk -x est identique à fdisk -l, mais avec plus de détails

df -h permet d'afficher les tailles en puissance de 1024


## 3 - Aller plus loin


### Preseed

Un preseed est un fichier servant à installer des systemes d'exploitations basés sur Debian de manière automatisé, avec toutes les configurations pré configurées. Cela est très utile si l'on a besoin d'installer plusieurs OS sans avoir à les configurer un à un manuellement.

### Reinitialisation du mot de passe

Redémarrer la machine virtuelle : pendant le démarrage, accéder au menu GRUB en appuyant sur la touche esc rapidement

Menu GRUB -> Recovery mode

>> passwd root

Entrer un nouveau mot de passe

Redemarrer la machine

>> reboot

### Redimensionner partition

>> sudo fsck /dev/sdaX
