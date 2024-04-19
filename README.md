-------------------------------------- infra --------------------------------------

 => [Setup road warrior](./road-warrior/)

 - Conf et css pour LibreWolf <br />
 - docker-compose pour routage du métamoteur searxng sur VPN <br />
 - possibilité d'utiliser un [client shadoshock](https://shadowsocks5.github.io/en/download/clients.html) pour faire passer le traffic du navigateur sur VPN <br />

 => [Windows 11 hardened Workstation](./Conf%20Windows%2011%20hardened%20workstation/))

 Renforcement de windows :
 - Au niveau de l'OS avec la sécurité windows (HVCI, DEP, CET, ASLR, sandboxing de defender... )
 - Un contrôle des fonctionnalités avec les GP
 - Au niveau des application avec une préférence pour les UWP qui bénéficient, entre autre, d'un sandboxing (AppContainer) et ne dépendent plus de l'api win32

-------------------------------------- diverses install --------------------------------------

 => [Bation guacamole](./Zprojet%20-%20Bastion%20guacamole/)

 Bastion pour centraliser l'administration des serveurs.
 2 version :
   - Version OpenBSD (par les dépôts)
   - Version Docker-compose

 => [Suricata IPS avec ELK](./Zprojet%20-%20Suricata%20layer%202%20with%20ELK%20stack/)

Sous Oracle Linux :
  - Suricata en mode IPS en couche 2 (AF_PACKET)
  -  Stack ELK pour la partie SIEM

=> [MAAS/JUJU - OpenStack](./Zprojet%20-%20MAAS%20JUJU%20-%20OpenStack/)
 
 Déploiment d'openstack minimal distribué par MAAS (server provisionning) et JUJU (orchestration d'application)

=> [MAAS/JUJU - Kubernetes](./Zprojet%20-%20MAAS%20JUJU%20-%20kubernetes/)

 Déploiment de kubernetes minimal par MAAS (server provisionning) et JUJU (orchestration d'application)
 WIP changement de runtime avec kata-container pour unsafe workload

-------------------------------------- Note --------------------------------------

 => [WIP hardened gentoo](./Znote%20-%20Hardened%20gentoo/)
 - Compiler and runtime stack		-> GCC hardened
 - MAC	-> SELinux
 - UKI & Secure boot	-> Dracut & sbsigntools
 - kernel	-> kernel hardened (KSSP)

 => [cisco](./Znote%20-%20conf%20switch/)<br />
 => [netdisco](./Znote%20-%20netdisco/)<br />

-------------------------------------- OBSOLÈTE --------------------------------------

=> [VPS SearXNG](./ZZold%20-%20vps%20searxng/)

Métamoteur de recherche, permet de choisir ce que l'on veut comme outil de recherche. 

Sur un debian truc en plus dessus :
 - swapfile
 - Zram
 - tmpfs
 - congestion TCP en BBR
 - DNScrypt Proxy
 
=> [OpenWrt](./ZZold%20-%20no%20box%20OpenWrt/)

Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEX s.
Internet en dual stack fonctionnel.
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :
 - routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)
 - inclure wan4 dans la zone wan du pare-feu
 - une option dans les DHCP pour ajouter les DNS interne

=> [raspberrypi-hole](./ZZold%20-%20raspberry%20pi-hole/)

Serveur DNS menteur sous Raspberry Pi OS Lite, redirige les requête sur DNScrypt Proxy :
 - Zram
 - tmpfs
 - DNScrypt Proxy
 - DoH (pour ECH) + DNSSEC + non-logging et non-blocking
 - IPv6 statique

=> [ROCKPro64 NAS](./ZZold%20-%20ROCKPro64%20NAS/)

NAS DIY avec la ROCKPro64 sous Dietpi :
 - RAID 1 par btrfs
 - Syncthing
 - Zram
tmpfs par défaut
