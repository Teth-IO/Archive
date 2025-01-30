-------------------------------------- current infra -------------------------------------- <br />

=> [slef-hosting sous k3s](./Current%20-%20Self-Hosting%k3s/iac%k3s.txt)

One node cluster k3s :
- OS Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)
- stockage : RAID ZFS avec snapshot (sanoid) et backup (restic vers S3)
- hosting sous cluster k3S maintenu en GitOps avec fluc CD
- maj auto : server, cluster et pods
- tailscale pour accès nomade

-------------------------------------- diverses install --------------------------------------

=> [Bation guacamole](./ZZold%20-%20Projets/)<br />
=> [Suricata IPS layer 2 avec ELK](./ZZold%20-%20Projets/)<br />
=> [MAAS/JUJU - OpenStack](./ZZold%20-%20Projets/)<br />
=> [MAAS/JUJU - Kubernetes](./ZZold%20-%20Projets/)<br />
=> [cisco](./ZZold%20-%20Projets/)<br />
=> [netdisco](./ZZold%20-%20Projets/)<br />

-------------------------------------- OBSOLÈTE --------------------------------------

=> [Self-Network](./ZZold%20-%20Self-Networking/)

<details>
<summary><b> OpenWrt no box </b></summary>

Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEX s.
Internet en dual stack fonctionnel.
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :
- routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)
- inclure wan4 dans la zone wan du pare-feu
- une option dans les DHCP pour ajouter les DNS interne
</details>

<details>
<summary><b> raspberrypi-hole </b></summary>

Serveur DNS menteur sous Raspberry Pi OS Lite, redirige les requête sur DNScrypt Proxy :
- Zram
- tmpfs
- DNScrypt Proxy
- DoH (pour ECH) + DNSSEC + non-logging et non-blocking
- IPv6 statique
</details>

<details>
<summary><b> OpenWRT home router </b></summary>

Config d'OpenWRT en home router et IPS :
- Recup de la delegation de prefixe IPv6
- acceleration materielle (HFO + WED) + irqbalance
- DNScrypt-proxy pour DOH + règle de redirection des requetes dns pour enforcing
- wireguard
- test snort en inline
</details>
 
=> [Self-Hosting](./ZZold%20-%20Self-Hosting/)

<details>
<summary><b> 0 VPS SearXNG </b></summary>

Métamoteur de recherche, permet de choisir ce que l'on veut comme outil de recherche. 

Sur un debian truc en plus dessus :
- swapfile
- Zram
- tmpfs
- congestion TCP en BBR
- DNScrypt Proxy
</details>

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
<summary><b> 3 HardenedBSD hosting platform] </b></summary>

HardenedBSD hosting platform :
- stockage sous zfs pour self-healing, RAID (volume manager) et backup (snapshot) automatisées par zfsnap
- CBSD pour gestion des jail et vm bhyve
- nextcloud (avec clamav) sous jail pour isolation et recovery
- vm ubuntu cloud-init sous bhyve pour stack docker SearXNG+gluetun <br />
</details>

<details>
<summary><b> 4 et 5 uCore hosting platform] </b></summary>
Fedora CoreOS (FCOS) rebase en uCore :

    Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)
    uCore-ZFS avec module signé et batteries included (podman, docker, sanoid, firewalld, cockpit ...)
    data sous un RAID ZFS avec sbapshot journalière
    hosting de diférent container sous podman quadlet en rootless
    services accessible par traefik avec routage par domaine + tls
    services : searxng, owncloud ocis, navidrome, homepage
</details>
 
=> [workstation](./ZZold%20-%20Workstation/)
 
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

<details>
<summary><b> 5 hardened gentoo v2 </b></summary>

Gentoo moderne :
- secure boot, selinux, btrfs, binaires opti, zram ... etc

</details>
