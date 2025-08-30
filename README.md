Dépôt d'archive pour les notes d'installation de mes vieilles infra et projets

# Divers notes d'installation

=> [Projets](./Projets/)

* Bation guacamole
* Suricata IPS layer 2 avec ELK
* MAAS/JUJU - OpenStack
* MAAS/JUJU - Kubernetes
* cisco
* netdisco

# Self-Networking

=> [Self-Network](./Self-Networking/)

<details>
<summary><b> 1 raspberry pi-hole </b></summary>
 
Serveur DNS menteur sous Raspberry Pi OS Lite, redirige les requête sur DNScrypt Proxy :<br />
* Zram<br />
* tmpfs<br />
* DNScrypt Proxy<br />
* DoH (pour ECH) + DNSSEC + non-logging et non-blocking<br />
* IPv6 statique<br />

</details>

<details>
<summary><b> 2 OpenWRT no box </b></summary>
 
Remplacement de la freebox mini 4k par OpenWrt sur un Mikrotik hEXs.<br />
Internet en dual stack fonctionnel.<br />
Une fois les interfaces fonctionnels il n'y a que quelques ajustements à faire :<br />
* routage static vers la wan pour l'IPv4 (l'IPv6 marche sans)<br />
* inclure wan4 dans la zone wan du pare-feu<br />
* une option dans les DHCP pour ajouter les DNS interne<br />

</details>

<details>
<summary><b> 3 OpenWRT home router </b></summary>
 
Config d'OpenWRT en home router et tentative d'IPS :<br />
* Recup de la delegation de prefixe IPv6<br />
* acceleration materielle (HFO + WED) + irqbalance<br />
* DNScrypt-proxy pour DOH + règle de redirection des requetes dns pour enforcing<br />
* wireguard<br />
* test snort en inline<br />

</details>

# Self-Hosting
=> [Self-Hosting](./Self-Hosting/)

<details>
<summary><b> 0 VPS SearXNG </b></summary>
 
Métamoteur de recherche sous un debian chez AWS. <br />
* swapfile<br />
* Zram<br />
* tmpfs<br />
* congestion TCP en BBR<br />
* DNScrypt Proxy<br />

</details>

<details>
<summary><b> 1 Dietpi ROCKPro64 </b></summary>
 
NAS DIY avec la ROCKPro64 sous Dietpi :<br />
* RAID 1 par btrfs<br />
* Syncthing<br />
* Zram<br />
tmpfs par défaut

</details>

<details>
<summary><b> 2 OpenBSD hyperviseur </b></summary>
 
* NAS Nextcloud sous RAID1 <br />
* Backup incrémentielles journalières & smartd <br />
* SearxNG dans une vm alpine linux <br />
* Proxifié dans un tunnel wireguard (tor aurait été mieux mais trop lent et settings de searxng instable) <br />
* HAProxy pour TLS <br />
* Packet Filtering <br />

</details>
 
<details>
<summary><b> 3 HardenedBSD CBSD </b></summary>
 
HardenedBSD hosting platform :<br />
* stockage sous zfs pour self-healing, RAID (volume manager) et backup (snapshot) automatisées par zfsnap<br />
* CBSD pour gestion des jail et vm bhyve<br />
* nextcloud (avec clamav) sous jail pour isolation et recovery<br />
* vm ubuntu cloud-init sous bhyve pour stack docker SearXNG+gluetun <br />

</details>

<details>
<summary><b> 4 uCore docker </b></summary>

Fedora CoreOS (FCOS) rebase en uCore :<br />
* Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)<br />
* uCore-ZFS avec module signé et batteries included (podman, docker, sanoid, firewalld, cockpit ...)<br />
* data sous un RAID ZFS avec snapshot journalière<br />
* hosting de diférent container sous docker<br />
* services : searxng, owncloud ocis, navidrome, homepage<br />

</details>

<details>
<summary><b> 5 uCore podman quadlet rootless </b></summary>

Fedora CoreOS (FCOS) rebase en uCore :<br />
* Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)<br />
* uCore-ZFS avec module signé et batteries included (podman, docker, sanoid, firewalld, cockpit ...)<br />
* data sous un RAID ZFS avec snapshot journalière<br />
* hosting de diférent container sous podman quadlet en rootless<br />
* services accessible par traefik avec routage par domaine + tls<br />
* services : searxng, owncloud ocis, navidrome, homepage<br />

</details>

<details>
<summary><b> 6 uCore k3S </b></summary>
 
One node cluster k3s :<br />
* OS Immutable, atomic auto update, secure (SELinux + SecureBoot + immutable)<br />
* stockage : RAID ZFS avec snapshot (sanoid) et backup (restic vers S3)<br />
* hosting sous cluster k3S maintenu en GitOps avec flux CD<br />
* 0 maintenance : maj auto du server, de k3s et des containers (rennovate)<br />
* tailscale pour accès nomade<br />
* propre CA et certifiat automatisé par cert-manager<br />
* gestion des sercrets avec SOPS<br />
* supervision avec headlamp<br />
* IDP avec keycloak : SSO et passwordless quand possible<br />

</details>

# Workstation
=> [workstation](./workstation/)
 
<details>
<summary><b> 1 hardened archlinux </b></summary>
 
* kernel : linux-hardened en lockdown<br />
* Chiffrement : tous sous LUKS2, seule l'UKI est exposée mais verifier par secure-boot<br />
* MAC : AppArmor<br />
* Firewall : Firewalld<br />
* blacklisting de plusieurs modules de kernel et hardening de divers paramètres du kernel en plus<br />
* Hardened malloc, appliqué pour l'ensemble du système<br />

</details>

<details>
<summary><b> 2 hardened gentoo </b></summary>
 
* Compiler and runtime stack	-> GCC hardened<br />
* MAC	-> SELinux<br />
* UKI & Secure boot	-> Dracut & sbsigntools<br />
* kernel	-> kernel hardened (KSSP)<br />

</details>
 
<details>
<summary><b> 3 QubesOS secure workstation </b></summary>
 
Notes d'install perso de Qubes OS<br />
* qubes perso sous kicksecure (debian morph)<br />
* FDE avec cryptenroll<br />
* install de mirage firewall (unikernel, moins de RAM, moins de surface d'attaque)<br />
* i3, rofi, adwaita-dark & icon Tela-dark pour dom0, xfce adwaita-dark & icon Tela-dark pour le reste<br />

</details>

<details>
<summary><b> 4 MicroOS aeon hardened workstation </b></summary>
 
Renforcement de MicroOS :<br />
* Hardened memory allocator => ne marche pas avec flatpak<br />
* KSPP aux kernel command line options et sysctls<br />
(par défaut MicroOS assure : rolling release cycle, SELinux en enforcing, fs en readonly (immutable), snpashot BTRFS, auto update, secure boot, et des protocoles modernes (wayland, pipewire, systemd-boot))

</details>

<details>
<summary><b> 5 hardened gentoo v2 </b></summary>
 
Gentoo moderne :
* secure boot, selinux, btrfs, binaires opti, zram ... etc

</details>
