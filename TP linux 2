# TP2 : Explorer et manipuler le système


## 1. Une machine xubuntu fonctionnelle

## 2. Nommer la machine

🌞 **Changer le nom de la machine**

`sudo hostname <NOM_MACHINE>`
`sudo nano /etc/hostname`
`sudo cat /etc/hostname`
 
## 3. Config réseau

➜ **Vérifiez avant de continuer le TP que la configuration réseau de la machine est OK. C'est à dire :**

- la machine doit pouvoir joindre internet
- votre PC doit pouvoir `ping` la machine

Pour vérifier que vous avez une configuration réseau correcte (étapes à réaliser DANS LA VM) :

```bash
# Affichez la liste des cartes réseau de la machine virtuelle
# Vérifiez que les cartes réseau ont toute une IP
$ ip a

# Si les cartes n'ont pas d'IP vous pouvez les allumez avec la commande
$ nmcli con up <NOM_INTERFACE>
# Par exemple
$ nmcli con up enp0s3

# Vous devez repérer l'adresse de la VM dans le host-only

# Vous pouvez tester de ping un serveur connu sur internet
# On teste souvent avec 1.1.1.1 (serveur DNS de CloudFlare)
# ou 8.8.8.8 (serveur DNS de Google)
$ ping 1.1.1.1

# On teste si la machine sait résoudre des noms de domaine
$ ping ynov.com
```

Ensuite on vérifie que notre PC peut `ping` la machine :

```bash
# Afficher la liste de vos carte réseau, la commande dépend de votre OS
$ ip a # Linux
$ ipconfig # Windows
$ ifconfig # MacOS

# Vous devez repérer l'adresse de votre PC dans le host-only

# Ping de l'adresse de la VM dans le host-only
$ ping <IP_VM>
```

🌞 **Config réseau fonctionnelle**

- dans le compte-rendu, vous devez me montrer...
  - depuis la VM : `ping 1.1.1.1` fonctionnel
  - depuis la VM : `ping ynov.com` fonctionnel
    - depuis votre PC : `ping <IP_VM>` fonctionnel
```bash
anthonygaillard@iMac-de-Anthony ~ % ping  192.168.64.2
PING 192.168.64.2 (192.168.64.2): 56 data bytes
64 bytes from 192.168.64.2: icmp_seq=0 ttl=64 time=0.981 ms
64 bytes from 192.168.64.2: icmp_seq=1 ttl=64 time=1.128 ms
```
# Partie 1 : SSH


# II. Setup du serveur SSH


## 1. Installation du serveur


🌞 **Installer le paquet `openssh-server`**

 On tape la commande sur le terminal sudo apt install openssh-server et ca nous demande le mdp et ensuite cela nous met :

Lecture des listes de paquets... Fait
Construction de l'arbre des d\u00e9pendances... Fait
Lecture des informations d'\u00e9tat... Fait      
openssh-server est d\u00e9j\u00e0 la version la plus r\u00e9cente (1:8.4p1-6ubuntu2).
openssh-server pass\u00e9 en \u00ab\u00a0install\u00e9 manuellement\u00a0\u00bb.
0 mis \u00e0 jour, 0 nouvellement install\u00e9s, 0 \u00e0 enlever et 12 non mis \u00e0 jour.>



## 2. Lancement du service SSH

🌞 **Lancer le service `ssh`**

```bash
anthony@node1:~$ sudo systemctl start ssh
```

- vérifier que le service est actuellement actif 

```bash
anthony@node1:~$ sudo systemctl status ssh
[sudo] password for anthony: 
\u25cf ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2021-11-08 21:17:10 UTC; 30min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 2800 (sshd)
      Tasks: 1 (limit: 9391)
     Memory: 1.0M
        CPU: 17ms
     CGroup: /system.slice/ssh.service
             \u2514\u25002800 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

nov. 08 21:17:10 node1.tp2.linux systemd[1]: Starting OpenBSD Secure Shell server...
nov. 08 21:17:10 node1.tp2.linux sshd[2800]: Server listening on 0.0.0.0 port 22.
nov. 08 21:17:10 node1.tp2.linux sshd[2800]: Server listening on :: port 22.
nov. 08 21:17:10 node1.tp2.linux systemd[1]: Started OpenBSD Secure Shell server
```


## 3. Etude du service SSH

🌞 **Analyser le service en cours de fonctionnement**


- afficher le statut du *service*
```bash
anthony@node1:~$ sudo systemctl status ssh
\u25cf ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2021-11-08 21:17:10 UTC; 32min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 2800 (sshd)
      Tasks: 1 (limit: 9391)
     Memory: 1.0M
        CPU: 17ms
     CGroup: /system.slice/ssh.service
             \u2514\u25002800 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

nov. 08 21:17:10 node1.tp2.linux systemd[1]: Starting OpenBSD Secure Shell server...
nov. 08 21:17:10 node1.tp2.linux sshd[2800]: Server listening on 0.0.0.0 port 22.
nov. 08 21:17:10 node1.tp2.linux sshd[2800]: Server listening on :: port 22.
nov. 08 21:17:10 node1.tp2.linux systemd[1]: Started OpenBSD Secure Shell server
```
- afficher le/les processus liés au *service* `ssh`
  ```bash 
  anthony@node1:~$ ps -e
    PID TTY          TIME CMD
     2800 ?        00:00:00 sshd
  ```
- afficher le port utilisé par le *service* `ssh`
  ```bash
  anthony@node1:~$ ss -l
    Netid      State       Recv-Q      Send-Q                                        Local Address:Port                           Peer Address:Port       Process                           
    tcp        LISTEN      0           128                                                    [::]:ssh                            [::]:
    ```              



---

🌞 **Connectez vous au serveur**

- depuis votre PC, en utilisant un **client SSH**

```bash
anthonygaillard@iMac-de-Anthony ~ %  ssh anthony@192.168.64.2
The authenticity of host '192.168.64.2 (192.168.64.2)' can't be established.
ED25519 key fingerprint is SHA256:DZWLlb386GoV+bKuiWfzw5Ns9H9FyGGPGeYlIFxqtPk.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.64.2' (ED25519) to the list of known hosts.
anthony@192.168.64.2's password: 
Welcome to Ubuntu 21.10 (GNU/Linux 5.13.0-20-generic aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of lun. 08 nov. 2021 22:06:13 UTC

  System load:             0.07
  Usage of /:              4.8% of 195.80GB
  Memory usage:            8%
  Swap usage:              0%
  Processes:               204
  Users logged in:         1
  IPv4 address for enp0s9: 192.168.64.2
  IPv6 address for enp0s9: fde4:dbb2:b508:3d96:f8df:a5ff:feac:aefe

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

20 updates can be applied immediately.
To see these additional updates run: apt list --upgradable


Last login: Mon Nov  8 14:56:19 2021
anthony@node1:~$ 

```

## 4. Modification de la configuration du serveur

🌞 **Modifier le comportement du service**

```bash 
anthony@node1:~$ cat /etc/ssh/sshd_config
#	$OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Include /etc/ssh/sshd_config.d/*.conf

Port 1050

```
- pour cette modification, prouver à l'aide d'une commande qu'elle a bien pris effet
  - une commande `ss -l` pour vérifier le port d'écoute



🌞 **Connectez vous sur le nouveau port choisi**

- depuis votre PC, avec un *client SSH*

```bash
anthonygaillard@iMac-de-Anthony ~ % ssh anthony@192.168.64.2 -p 1050
anthony@192.168.64.2's password: 
Welcome to Ubuntu 21.10 (GNU/Linux 5.13.0-20-generic aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of lun. 08 nov. 2021 22:31:18 UTC

  System load:             0.0
  Usage of /:              4.8% of 195.80GB
  Memory usage:            8%
  Swap usage:              0%
  Processes:               206
  Users logged in:         1
  IPv4 address for enp0s9: 192.168.64.2
  IPv6 address for enp0s9: fde4:dbb2:b508:3d96:f8df:a5ff:feac:aefe

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

20 updates can be applied immediately.
To see these additional updates run: apt list --upgradable


Last login: Mon Nov  8 22:25:32 2021 from 192.168.64.1
anthony@node1:~$ 
```

# Partie 2 : FTP

# II. Setup du serveur FTP


## 1. Installation du serveur

🌞 **Installer le paquet `vsftpd`**

```bash 
anthony@node1:~$ sudo apt-get install vsftpd
Lecture des listes de paquets... Fait
Construction de l'arbre des d\u00e9pendances... Fait
Lecture des informations d'\u00e9tat... Fait      
Les NOUVEAUX paquets suivants seront install\u00e9s\u00a0:
  vsftpd
0 mis \u00e0 jour, 1 nouvellement install\u00e9s, 0 \u00e0 enlever et 15 non mis \u00e0 jour.
Il est n\u00e9cessaire de prendre 117 ko dans les archives.
Apr\u00e8s cette op\u00e9ration, 309 ko d'espace disque suppl\u00e9mentaires seront utilis\u00e9s.
R\u00e9ception de\u00a0:1 http://fr.ports.ubuntu.com/ubuntu-ports impish/main arm64 vsftpd arm64 3.0.3-13build1 [117 kB]
117 ko r\u00e9ceptionn\u00e9s en 0s (353 ko/s)
Pr\u00e9configuration des paquets...
S\u00e9lection du paquet vsftpd pr\u00e9c\u00e9demment d\u00e9s\u00e9lectionn\u00e9.
(Lecture de la base de donn\u00e9es... 151192 fichiers et r\u00e9pertoires d\u00e9j\u00e0 install\u00e9s.)
Pr\u00e9paration du d\u00e9paquetage de .../vsftpd_3.0.3-13build1_arm64.deb ...
D\u00e9paquetage de vsftpd (3.0.3-13build1) ...
Param\u00e9trage de vsftpd (3.0.3-13build1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/vsftpd.service \u2192 /lib/systemd/system/vsftpd.
service.
Traitement des actions diff\u00e9r\u00e9es (\u00ab\u00a0triggers\u00a0\u00bb) pour man-db (2.9.4-2)\u00a0...
Scanning processes...                                                                                   
Scanning linux images... 
```

## 2. Lancement du service FTP

🌞 **Lancer le service `vsftpd`**

```bash
anthony@node1:~$ sudo systemctl start vsftpd
anthony@node1:~$ sudo systemctl status vsftpd
\u25cf vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2021-11-08 21:26:17 UTC; 1h 9min ago
    Process: 3031 ExecStartPre=/bin/mkdir -p /var/run/vsftpd/empty (code=exited, status=0/SUCCESS)
   Main PID: 3032 (vsftpd)
      Tasks: 1 (limit: 9391)
     Memory: 628.0K
        CPU: 3ms
     CGroup: /system.slice/vsftpd.service
             \u2514\u25003032 /usr/sbin/vsftpd /etc/vsftpd.conf

nov. 08 21:26:17 node1.tp2.linux systemd[1]: Starting vsftpd FTP server...
nov. 08 21:26:17 node1.tp2.linux systemd[1]: Started vsftpd FTP server.
anthony@node1:~$ 

```

## 3. Etude du service FTP

🌞 **Analyser le service en cours de fonctionnement**

- afficher le statut du service
  ```bash
anthony@node1:~$  sudo systemctl status vsftpd
\u25cf vsftpd.service - vsftpd FTP server
     Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2021-11-08 21:26:17 UTC; 1h 12min ago
    Process: 3031 ExecStartPre=/bin/mkdir -p /var/run/vsftpd/empty (code=exited, status=0/SUCCESS)
   Main PID: 3032 (vsftpd)
      Tasks: 1 (limit: 9391)
     Memory: 628.0K
        CPU: 3ms
     CGroup: /system.slice/vsftpd.service
             \u2514\u25003032 /usr/sbin/vsftpd /etc/vsftpd.conf

nov. 08 21:26:17 node1.tp2.linux systemd[1]: Starting vsftpd FTP server...
nov. 08 21:26:17 node1.tp2.linux systemd[1]: Started vsftpd FTP server.
```
- afficher le/les processus liés au service `vsftpd`
```bash
  anthony@node1:~$ ps -e
    PID TTY          TIME CMD
   3032 ?        00:00:00 vsftpd
```

- afficher le port utilisé par le service `vsftpd`
  - avec une commande `ss -l`
  - isolez uniquement la/les ligne(s) intéressante(s)
  ```bash
 anthony@node1:~$ ss -l
 Netid State  Recv-Q Send-Q                              Local Address:Port                 Peer Address:Port                                               Process                                              
   tcp   LISTEN 0      32                                              *:ftp                             *:
```

---

