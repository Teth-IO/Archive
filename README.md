-------------------------------------- infra -------------------------------------- <br />

=> [uCore NAS % hosting platform](./uCore%20-%20NAS/NAS.txt)

Fedora CoreOS (FCOS) rebase en uCore :
- Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)
- uCore-ZFS avec module signé et batteries included (docker, sanoid, firewalld, ...)
- home drive avec owncloud infini scale (version cloud native)
- data sous un RAID ZFS avec sbapshot journalière
- hosting de searxng sous macvlan

=> [OpenWRT IPS & home router](./OpenWRT%20-%20home%20router/note.txt)

Config d'OpenWRT en home router et IPS :
- Recup de la delegation de prefixe IPv6
- acceleration materielle (HFO + WED)
- snort inline (IPS)
- wireguard

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

 => [cisco](./Znote%20-%20conf%20switch/)<br />
 => [netdisco](./Znote%20-%20netdisco/)<br />

-------------------------------------- OBSOLÈTE --------------------------------------

=> [VPS SearXNG](./ZZold%20-%20vps%20searxng/)
-> maintenant sous docker-compose sur les [NAS](./ZZold%20-%20NAS/)

Métamoteur de recherche, permet de choisir ce que l'on veut comme outil de recherche. 

Sur un debian truc en plus dessus :
 - swapfile
 - Zram
 - tmpfs
 - congestion TCP en BBR
 - DNScrypt Proxy
 
=> [OpenWrt no box](./ZZold%20-%20no%20box%20OpenWrt/)
-> nouvelle version sous GL.iNET MT 6000 [OpenWRT IPS & home router](./OpenWRT%20-%20home%20router/note.txt)

Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEX s.
Internet en dual stack fonctionnel.
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :
 - routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)
 - inclure wan4 dans la zone wan du pare-feu
 - une option dans les DHCP pour ajouter les DNS interne

=> [raspberrypi-hole](./ZZold%20-%20raspberry%20pi-hole/)
-> tout passer sous cloudflare pour DNSSEC et ECH en nomade

Serveur DNS menteur sous Raspberry Pi OS Lite, redirige les requête sur DNScrypt Proxy :
 - Zram
 - tmpfs
 - DNScrypt Proxy
 - DoH (pour ECH) + DNSSEC + non-logging et non-blocking
 - IPv6 statique
 
=> [NAS](./ZZold%20-%20NAS/)
-> WIP pour passage sous fedora coreos uCore pour passer a de l'immutable et approcher la zero maintenance

<details>
<summary><b> 1 sous ROCKPro64 </b></summary>

NAS DIY avec la ROCKPro64 sous Dietpi :
 - RAID 1 par btrfs
 - Syncthing
 - Zram
tmpfs par défaut
</details>

<details>
<summary><b> 2 sous OpenBSD + hyperviseur </b></summary>

 - NAS Nextcloud sous RAID1 <br />
    - Backup incrémentielles journalières & smartd <br />
 - SearxNG dans une vm alpine linux <br />
    - Proxifié dans un tunnel wireguard (tor aurait été mieux mais trop lent et settings de searxng instable) <br />
    - HAProxy pour TLS <br />
 - Packet Filtering <br />
</details>
 
<details>
<summary><b> 3 HardenedBSD NAS & hosting platform] </b></summary>

HardenedBSD NAS & hosting platform :
 - NAS sous zfs pour self-healing, RAID (volume manager) et backup (snapshot) automatisées par zfsnap
 - CBSD pour gestion des jail et vm bhyve
 - nextcloud (avec clamav) sous jail pour isolation et recovery
 - vm ubuntu cloud-init sous bhyve pour stack docker SearXNG+gluetun <br />
</details>
 
=> [workstation](./ZZold%20-%20workstation/)
-> maintenant sous bazzite, immutable et secure ootb, zero customization necessaire, zero maintenance
 
<details>
<summary><b> 1 hardened archlinux </b></summary>
- kernel : linux-hardened en lockdown<br />
=>! revoir pour chercher la source d'upsstream et la KSPP
- Chiffrement : tous sous LUKS2, seule l'UKI est exposée mais verifier par secure-boot<br />
=>! revoir pour implémenter systemd-cryptenroll (dechiffrement LUKS non plus avec mot de passe mais clef FIDO2)
- MAC : AppArmor<br />
=>! revoir pour passer à SELinux<br />
- Firewall : Firewalld
- blacklisting de plusieurs modules de kernel et hardening de divers paramètres du kernel en plus
- Hardened malloc, appliqué pour l'ensemble du système
</details>

<details>
<summary><b> 2 hardened gentoo </b></summary>
 - Compiler and runtime stack	-> GCC hardened
 - MAC	-> SELinux
 - UKI & Secure boot	-> Dracut & sbsigntools
 - kernel	-> kernel hardened (KSSP)
</details>
 
<details>
<summary><b> 3 QubesOS secure workstation </b></summary>

Notes d'install perso de Qubes OS
- qubes perso sous kicksecure (debian morph)
- FDE avec cryptenroll
- install de mirage firewall (unikernel, moins de RAM, moins de surface d'attaque) <br />
- i3, rofi, adwaita-dark & icon Tela-dark pour dom0, xfce adwaita-dark & icon Tela-dark pour le reste <br />
</details>

<details>
<summary><b> 4 MicroOS aeon hardened workstation </b></summary>

 Attente upstream : nouvel installeur pour le support de combustion, systemd-cryptenroll
 Renforcement de MicroOS :
 - Hardened memory allocator => ne marche pas avec flatpak
 - KSPP aux kernel command line options et sysctls<br />
 
 (par défaut MicroOS assure : rolling release cycle, SELinux en enforcing, fs en readonly (immutable), snpashot BTRFS, auto update, secure boot, et des protocoles modernes (wayland, pipewire, systemd-boot))
</details>
 
