# Partie D — Réponses aux questions de l'exercice 8

## 1. Pourquoi utiliser `--import` au lieu d'une installation depuis un ISO ?

L'option `--import` permet de créer une machine virtuelle à partir d'un disque contenant déjà un système d'exploitation installé.

Dans notre TP, l'image `ubuntu-os-capture-v2.qcow2` contient déjà Ubuntu 20.04.6 LTS, sa configuration et ses fichiers.

Il n'est donc pas nécessaire de démarrer un programme d'installation depuis un fichier ISO. L'option `--import` permet à libvirt d'utiliser directement le disque existant pour démarrer la nouvelle machine virtuelle.

## 2. Pourquoi s'agit-il d'une image de système d'exploitation et non d'un disque QCOW2 vide ?

Un disque QCOW2 vide est uniquement un espace de stockage virtuel. Il ne contient pas nécessairement de système d'exploitation installé.

Notre image est différente : elle provient du disque d'une machine virtuelle Ubuntu déjà configurée.

Elle contient notamment :
- Le système Ubuntu 20.04.6 LTS.
- Les partitions et systèmes de fichiers.
- Les fichiers système et les configurations.
- Les logiciels installés, notamment OpenSSH Server et QEMU Guest Agent.
- Le fichier témoin `/opt/tp1/version.txt`.

Le test de restauration a confirmé la présence de ces éléments et le démarrage correct du système.

## 3. Que faut-il préserver pour restaurer une VM utilisant plusieurs disques, UEFI ou TPM ?

Pour une restauration fidèle, il faut conserver les éléments de configuration associés à la machine virtuelle.

**Plusieurs disques :**
- Capturer chaque disque virtuel nécessaire.
- Conserver leur association avec la VM.
- Respecter les contrôleurs, les bus et l'ordre de connexion des disques.
- Garantir la cohérence des données entre les disques, idéalement avec la VM arrêtée ou une méthode de snapshot cohérente.

**Firmware UEFI :**
- Conserver la configuration du firmware et le chargeur UEFI.
- Préserver le fichier NVRAM contenant les variables de démarrage de la VM.
- Réassocier correctement ces éléments lors de la restauration.

**TPM :**
- Conserver la configuration du périphérique TPM virtuel.
- Préserver son état persistant, notamment les données gérées par swtpm lorsqu'il est utilisé.
- Réutiliser un état TPM compatible avec la VM restaurée.

La sauvegarde du seul disque QCOW2 peut donc être insuffisante lorsque la VM utilise ces composants.

## 4. Pourquoi éviter d'exécuter plusieurs copies non généralisées en production ?

Une image non généralisée conserve l'identité et certains paramètres de la machine source.

Plusieurs copies peuvent donc partager :
- Le même `machine-id`.
- Le même nom d'hôte.
- Les mêmes clés SSH de serveur.
- Certaines configurations réseau et identifiants de services.

Cela peut provoquer des conflits d'identité, des problèmes de communication réseau et des risques de sécurité.

Avant un déploiement en production, il faut généraliser l'image et personnaliser chaque instance : identité système, nom d'hôte, clés SSH et configuration réseau, entre autres.

**Conclusion :**

La capture `ubuntu-os-capture-v2.qcow2` a été créée, vérifiée et documentée. Sa restauration dans `ubuntu-restore-v2` a permis de confirmer le démarrage d'Ubuntu 20.04.6 LTS et la conservation du fichier témoin. La validation de la restauration est donc réussie.
