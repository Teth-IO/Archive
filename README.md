-------------------------------------- infra -------------------------------------- <br />

=> [HardenedBSD NAS & hosting platform](./HardenedBSD%20-%20nas/notes.txt)

HardenedBSD NAS & hosting platform :
 - NAS sous zfs pour self-healing, RAID (volume manager) et backup (snapshot) automatisées par zfsnap
 - CBSD pour gestion des jail et vm bhyve
 - nextcloud (avec clamav) sous jail pour isolation et recovery
 - vm ubuntu cloud-init sous bhyve pour stack docker SearXNG+gluetun <br />

WIP : passage d'ubuntu a MicroOS dès que possible. Actuellement les vm ne boot pas depuis un iso et pas de cloud-init de dispo

 => [Windows 11 hardened gaming station](./Windows%2011%20-%20hardened%20gaming%20station/)

 Renforcement de windows :
 - Au niveau de l'OS avec la sécurité windows (HVCI, DEP, CET, ASLR, sandboxing de defender... )
 - Un contrôle des fonctionnalités avec les GP
 - Si besoin d'app, préférer les UWP (windows store) qui bénéficient, entre autre, d'un sandboxing (AppContainer) et ne dépendent plus de l'api win32

 => [QubesOS secure workstation](./Qubes%20OS%20-%20secure%20workstation/QubesOS.txt)

Notes d'install perso de Qubes OS
- sys-* sous fedora pour selinux
- qubes perso sous kicksecure
- FDE avec cryptenroll
- install de mirage firewall (unikernel, moins de RAM, moins de surface d'attaque) <br />

WIP : attente d'upstream pour sys-audio et sys-gui-gpu


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

 => [hardened gentoo](./Znote%20-%20Hardened%20gentoo/)
 - Compiler and runtime stack	-> GCC hardened
 - MAC	-> SELinux
 - UKI & Secure boot	-> Dracut & sbsigntools
 - kernel	-> kernel hardened (KSSP)

  => [MicroOS aeon hardened workstation](/Znote%20-%20MicroOS%20aeon%20-%20hardened/) <br />
 Attente upstream : nouvel installeur pour le support de combustion, systemd-cryptenroll
 Renforcement de MicroOS :
 - Hardened memory allocator => ne marche pas avec flatpak
 - KSPP aux kernel command line options et sysctls<br />
 
 (par défaut MicroOS assure : rolling release cycle, SELinux en enforcing, fs en readonly (immutable), snpashot BTRFS, auto update, secure boot, modern solution (wayland, pipewire, systemd-boot))

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

=> [OpenBSD NAS & SearxNG](./ZZold%20-%20OpenBSD%20-%20nas/)

 - NAS Nextcloud sous RAID1 <br />
    - Backup incrémentielles journalières & smartd <br />
 - SearxNG dans une vm alpine linux <br />
    - Proxifié dans un tunnel wireguard (tor aurait été mieux mais trop lent et settings de searxng instable) <br />
    - HAProxy pour TLS <br />
 - Packet Filtering <br />
