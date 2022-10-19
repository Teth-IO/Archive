# infra

=> [VPS SearXNG](./vps%20searxng/installation.txt)

Métamoteur de recherche, permet de choisir ce que l'on veut comme outil de recherche. 

truc en plus dessus :
 - swapfile
 - Zram
 - tmpfs
 - congestion TCP en BBR
 - DNScrypt Proxy

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

=> [raspberrypi-hole](./raspberry%20pi-hole/pi-hole%20dnscrypt-proxy.txt)

Serveur DNS menteur, redirige les requête sur DNScrypt Proxy :
 - Zram
 - tmpfs
 - DNScrypt Proxy
 - IPv6 statique

=> [OpenWrt](./no%20box%20OpenWrt/OpenWrt.txt)

Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEX s.
Internet en dual stack fonctionnel.
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :
 - routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)
 - inclure wan4 dans la zone wan du pare-feu
 - une option dans les DHCP pour ajouter les DNS interne
