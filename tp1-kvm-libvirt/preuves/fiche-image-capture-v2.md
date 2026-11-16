# Fiche descriptive — Image OS capture-v2

## 1. Identification
- Système : Ubuntu 20.04.6 LTS (Focal Fossa)
- Version système : 20.04
- Architecture : x86_64
- Nom d'hôte source : srv-source
- Version applicative témoin : v1
- Date de création de la capture : 10 novembre 2026
- Identifiant de la capture : ubuntu-os-capture-v2

## 2. Caractéristiques de l'image
- Fichier : /mnt/kvm-storage-60/ubuntu-os-capture-v2.qcow2
- Format : QCOW2
- Capacité virtuelle : 15 GiB
- Taille physique constatée : environ 10.2 GiB
- Image indépendante : oui
- Fichier backing : aucun
- Vérification qemu-img check : aucune erreur détectée

## 3. Logiciels et rôle
Logiciels vérifiés :
- OpenSSH Server : 1:8.2p1-4ubuntu0.13
- QEMU Guest Agent : 1:4.2-3ubuntu6.30
- cloud-init : 24.4.1-0ubuntu0~20.04.3

Service SSH : actif au moment de la vérification.

Rôle prévu : image de système d'exploitation de base destinée aux
exercices de capture, de réimportation et de test du TP1.

## 4. Configuration virtuelle source
- Mémoire : 2048 MiB
- Processeurs : 2 vCPU
- Type de machine : pc-q35-4.2
- Firmware : BIOS classique (aucun loader UEFI ni NVRAM dans le XML)
- Disque principal : vda, contrôleur VirtIO
- Lecteur CD-ROM : sda, contrôleur SATA
- Réseau : réseau libvirt default, modèle VirtIO
- Adresse MAC source : 52:54:00:c7:02:92

## 5. Identité et données présentes
- Utilisateur constaté : hiba
- Nom d'hôte : srv-source
- Machine ID : b06dd0e18d8347e1b03883d632747272
- Fichier témoin : /opt/tp1/version.txt
- Contenu du fichier témoin : Version applicative TP1 : v1

La capture n'est pas généralisée. Elle conserve l'identité de la machine,
les comptes et les données présents dans le système source. D'autres
fichiers ou configurations peuvent également être présents.

## 6. Empreinte et intégrité
SHA-256 :
ad238895cae00ecf4330854a528f7597782faf9325ee395137cdd64608727208

Le contrôle qemu-img check n'a détecté aucune erreur structurelle.
Cela ne garantit pas à lui seul le démarrage du système ni le bon
fonctionnement de toutes les applications.

## 7. Statut
Capture non généralisée.
Elle est destinée à un usage pédagogique et à des tests isolés,
pas à un déploiement direct de plusieurs serveurs en production.

## 8. Procédure de réimportation
1. Créer un nouveau disque de travail indépendant avec qemu-img convert.
2. Déclarer une nouvelle VM libvirt avec virt-install --import.
3. Conserver la configuration matérielle et le firmware compatibles
   avec la VM source.
4. Démarrer la VM restaurée.
5. Vérifier /etc/os-release, /opt/tp1/version.txt, le hostname
   et le machine-id.
6. Arrêter proprement la VM restaurée après les vérifications.
