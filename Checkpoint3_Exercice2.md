# Partie 1 : Gestion des utilisateurs

### Q.2.1.1

**Création d'un nouvel utilisateur**

![image](https://github.com/user-attachments/assets/b4108fcd-3be9-4aaf-ad4d-b89cdbdb2d60)

### Q.2.1.2

**Afin de faciliter l'utilisation avec ce nouvel utilisateur et pour renforcer la sécurité, je l'ajouterai au groupe "Sudoers" afin de lui donner les droits administrateurs, sans avoir à utiliser root**

---

# Partie 2 : Configuration de SSH

### Q.2.2.1

**Désactivation de l'accès distant pour root via le fichier de configuration /etc/ssh/sshd_config**

![image](https://github.com/user-attachments/assets/25e9507b-1c9e-40e5-be52-ff7db2e24763)

### Q.2.2.2

**Autorisation pour l'accès à distance via le compte nouvellement créé uniquement, via le fichier sshd_config**

![image](https://github.com/user-attachments/assets/7b56bf50-7eb4-4a9b-a17d-09a3c2ee85d0)

### Q.2.2.3

**Mise en place d'une authentification par clé et désactivation de l'authentification par mot de passe, via le fichier sshd_config**

![image](https://github.com/user-attachments/assets/5f94344f-b1b9-4111-a004-0cc241222284)

---

# Partie 3 : Analyse du stockage

### Q.2.3.1md

**Les systèmes de fichiers actuellemnt montés sont les suivants :**

![image](https://github.com/user-attachments/assets/5cfbdad4-f800-4897-b8ba-25a2bdd26c5c)

### Q.2.3.2

**Le système utilise un système de fichiers sur LVM (monté sur /dev/mapper) avec les systèmes sous-jacents suivants :**

![image](https://github.com/user-attachments/assets/e75e4624-f75e-4338-ab75-954cc8cd278d)

### Q.2.3.3

**Création d'un nouveau disque sur VirtualBox**

![image](https://github.com/user-attachments/assets/0640d526-74be-43f6-84ff-9caf67b6fa52)

![image](https://github.com/user-attachments/assets/ded13cde-63c1-455a-b39c-3ba5589b4c17)

**Réparation du RAID avec mdadm**

![image](https://github.com/user-attachments/assets/16f39cd3-aae8-401f-995f-b166fdd69969)

### Q.2.3.4

**Création d'un nouveau volume logique**

![image](https://github.com/user-attachments/assets/c137b132-3c06-4341-ad25-71f9c954388f)

**Formattage du volume logique**

![image](https://github.com/user-attachments/assets/8ab1cc8f-1ab7-45c3-809d-3738283be284)

**Création du point de montage**

![image](https://github.com/user-attachments/assets/0b751843-8668-42ad-ab12-85d3c63acbb0)

**Modifier le fichier /etc/fstab**

![image](https://github.com/user-attachments/assets/6ca4ef47-b9fa-4fd1-bbb5-3dd66892af4c)

**Monter le disque et vérifier**

![image](https://github.com/user-attachments/assets/c521dc80-72b6-425a-9947-e9038b3c9816)

### Q.2.3.5

**Il reste 1.8G dans le volume**

![image](https://github.com/user-attachments/assets/0d143fd8-2d1a-4c22-a74c-1cb785cdb77c)

---

# Partie 4 : Sauvegardes

### Q.2.4.1

- bareos-dir : Il planifie et contrôle toutes les tâches de sauvegarde, de restauration et de vérification. Il gère également la base de données Bareos, qui contient des informations sur les fichiers sauvegardés, les supports de stockage, etc.

- bareos-sd : Ce composant gère le transfert des données entre le client (bareos-fd) et le support de stockage (disque dur, bande magnétique, etc.). Il reçoit les données du client, les compresse et les crypte si nécessaire, puis les écrit sur le support de stockage spécifié par le directeur.

- bareos-fd : Il s'exécute sur le client et est responsable de la lecture des fichiers à sauvegarder et de leur envoi à bareos-sd. Il peut également effectuer des restaurations de fichiers à partir des sauvegardes.

---

# Partie 5 : Filtrage et analyse réseau

### Q.2.5.1

**Ci-dessous les règles de Netfilter, notamment l'ouverture du port 22 (ssh) et l'acceptation des pings (ICMP)**

![image](https://github.com/user-attachments/assets/40867b5e-823f-463d-9ece-62161f91435a)

### Q.2.5.2

- `ct state established, related accept` : Cela permet aux paquets qui font partie d'une connexion déjà établie ou qui sont liés à une connexion existante de passer. 

- `iifname "lo" accept` : Cela autorise tout le trafic sur l'interface lo, qui est utilisée pour la communication entre les processus sur la même machine.

- `tcp dport 22 accept` : SSH

- `ip protocol icmp accept` et `ip6 nexthdr ipv6-icmp accept` : PING

### Q.2.5.3

**Tout ce qui n'est pas autorisé est interdit**

### Q.2.5.4

**Ouverture des ports 9101 à 9103 pour Bareos**

```
sudo nft add rule inet inet_filter_table input tcp dport 9101 accept
sudo nft add rule inet inet_filter_table input tcp dport 9102 accept
sudo nft add rule inet inet_filter_table input tcp dport 9103 accept
```

---

# Partie 6 : Analyse de logs

### Q.2.6.1

**Liste des 10 derniers échecs de connexion ssh**

![image](https://github.com/user-attachments/assets/fa6bc0e9-cca7-4ca8-b9ea-1c1d6b6cc07e)







