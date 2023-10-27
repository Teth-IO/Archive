# infra

 => [Windows 11 hardened Workstation](./windows%2011%20hardened%20workstation/windows%2011%20hardening.txt)

 Renforcement de windows :
 - Au niveau de l'OS avec la sécurité windows (HVCI, DEP, CET, ASLR, sandboxing de defender... )
 - Un contrôle des fonctionnalités avec les GP
 - Au niveau des application avec une préférence pour les UWP qui bénéficient, entre autre, d'un sandboxing (AppContainer) et ne dépendent plus de l'api win32
 
 => [raspberrypi-hole](./raspberry%20pi-hole/pi-hole%20dnscrypt-proxy.txt)

Serveur DNS menteur sous Raspberry Pi OS Lite, redirige les requête sur DNScrypt Proxy :
 - Zram
 - tmpfs
 - DNScrypt Proxy
 - DoH (pour ECH) + DNSSEC + non-logging et non-blocking
 - IPv6 statique

=> [ROCKPro64 NAS](./ROCKPro64%20NAS/DietPi.txt)

NAS DIY avec la ROCKPro64 sous Dietpi :
 - RAID 1 par btrfs
 - Rclone SFTP
 - DLNA/UPnP
 - Rsync
 - web monitoring
 - Syncthing
 - Zram
tmpfs par défaut

OBSOLÈTE :

=> [VPS SearXNG](./vps%20searxng/installation.txt)

Métamoteur de recherche, permet de choisir ce que l'on veut comme outil de recherche. 

Sur un debian truc en plus dessus :
 - swapfile
 - Zram
 - tmpfs
 - congestion TCP en BBR
 - DNScrypt Proxy
 
=> [OpenWrt](./no%20box%20OpenWrt/OpenWrt.txt)

Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEX s.
Internet en dual stack fonctionnel.
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :
 - routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)
 - inclure wan4 dans la zone wan du pare-feu
 - une option dans les DHCP pour ajouter les DNS interne