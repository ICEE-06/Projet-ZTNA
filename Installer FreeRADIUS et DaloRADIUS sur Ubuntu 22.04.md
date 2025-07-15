[FreeRADIUS](https://freeradius.org/) est un serveur RADIUS open-source largement utilisé pour l’authentification, l’autorisation et la comptabilité des utilisateurs réseau.

DaloRADIUS est une interface web open-source pour FreeRADIUS, conçue pour simplifier la gestion et l’administration d’un serveur FreeRADIUS.

Cela permet aux administrateurs réseau de configurer, surveiller et gérer leur serveur RADIUS via une interface conviviale basée sur le web.

### Mise à jour des paquets
```
sudo apt update & sudo apt upgrade
```
### Installer le serveur web Apache
```
sudo apt install apache2
```
#### **Activez Apache pour qu’il démarre au démarrage d’Ubuntu.**
```
sudo systemctl enable --now apache2
```
### Installer PHP et ses modules supplémentaires
```
sudo apt -y install php libapache2-mod-php php-{gd,common,mail,mail-mime,mysql,pear,db,mbstring,xml,curl}
```
### Installer MySQL
```
sudo apt install mysql-server
```
### Configurer MySQL
```
sudo mysql_secure_installation
```
### Installer FreeRADIUS et ses modules
```
sudo apt -y install freeradius freeradius-mysql freeradius-utils -y
```
### Tester le serveur FreeRADIUS

- Arrêtez le serveur FreeRADIUS :
```
sudo systemctl stop freeradius
```
- Exécutez FreeARDIUS en mode débogage :
```
sudo freeradius -X
```
![[Pasted image 20250711132101.png]]

Redémarrez et activez le service FreeRADIUS :
```
sudo systemctl enable --now freeradius
```
### Autoriser FreeRADIUS dans le pare-feu
```
sudo ufw allow to any port 1812 proto udp
sudo ufw allow to any port 1813 proto udp
```
### **Créer la base donnée et utilisateur MySQL pour FreeRADIUS**

**Se connecter à la base de donnée :**
```
sudo mysql -u root -p
```
**Créer la base de donnée et utilisateur :**
```
CREATE DATABASE radius;
CREATE USER 'radius'@'localhost' IDENTIFIED by 'R@duisp@ssword123';
GRANT ALL PRIVILEGES ON radius.* TO 'radius'@'localhost';
FLUSH PRIVILEGES;
quit;
```
### Importer le schéma de la base donnée RADIUS MySQL

```
sudo su
```
**Importer le schéma :**
```
mysql -u root -p radius < /etc/freeradius/3.0/mods-config/sql/main/mysql/schema.sql
```
**Vérification de la base donnée :**
```
sudo mysql -u root -p -e "use radius;show tables;"
```

![[Pasted image 20250711133433.png]]

#### Créez un lien symbolique vers le module SQL vers /etc/freeradius/3.0/mods-enabled :

```
sudo ln -s /etc/freeradius/3.0/mods-available/sql /etc/freeradius/3.0/mods-enabled/
```
### Configurer FreeRADIUS
```
sudo nano /etc/freeradius/3.0/mods-enabled/sql
```
Remplacer **dialect = « sqlite »** par **dialect = « mysql »**

Remplacer **driver = « rlm_sql_null »** par **driver = « rlm_sql_${dialect} »**

Pour les besoins de ce tuto, nous n’utiliserons pas de certificats TLS.

Commenter la section TLS de MySQL en ajoutant un signe **#** au début de chaque ligne de la section **tls**.

Ça :
![[Pasted image 20250711133908.png]]

En ça :

![[Pasted image 20250711134010.png]]

Décommentez la section Informations de connexion :

![[Pasted image 20250711134516.png]]

Configurer le nom de la base de données :

![[Pasted image 20250711140229.png]]

Décommentez une ligne contenant read_clients = yes.

![[Pasted image 20250711135924.png]]

Modifiez maintenant les droits de groupe du fichier que nous venons de modifier :
```
sudo chgrp -h freerad /etc/freeradius/3.0/mods-available/sql
sudo chown -R freerad:freerad /etc/freeradius/3.0/mods-enabled/sql
```
Redémarrez le service FreeRADIUS :
```
sudo systemctl restart freeradius.service
```
## Installer daloRADIUS

Installer unzip :
```
sudo apt -y install wget unzip
```
Télécharger daloRADIUS :
```
wget https://github.com/lirantal/daloradius/archive/1.3.zip
```
Décompresser daloRADIUS :
```
unzip 1.3.zip
cd daloradius-1.3
```
Remplissez la base de données avec le schéma daloRADIUS :
```
sudo mysql -u root -p radius < contrib/db/fr2-mysql-daloradius-and-freeradius.sql
sudo mysql -u root -p radius < contrib/db/mysql-daloradius.sql
```
Déplacez le dossier dans la racine du document comme :
```
cd 
sudo mv daloradius-1.3 /var/www/html/daloradius
```
Changer le propriétaire et le groupe du dossier daloradius en www-data:www-data, qui sont l’utilisateur et le groupe sous lesquels le serveur Web Apache s’exécute.
```
sudo chown -R www-data:www-data /var/www/html/daloradius/
```
Créer le fichier de configuration daloRADIUS. Copier de cet exemple de fichier :
```
sudo cp /var/www/html/daloradius/library/daloradius.conf.php.sample /var/www/html/daloradius/library/daloradius.conf.php
```
Modifier également les autorisations pour le fichier de configuration daloRADIUS :
```
sudo chmod 664 /var/www/html/daloradius/library/daloradius.conf.php
```
#### Configurer les informations de base de données FreeRADIUS
```
sudo nano /var/www/html/daloradius/library/daloradius.conf.php
```
Après avoir modifié les détails de la base de données :

![[Pasted image 20250711142141.png]]
Redémarrer FreeRADIUS et Apache
```
sudo systemctl restart freeradius.service apache2
```
### Accéder à daloRADIUS

Pour accéder à daloRADIUS via un navigateur Web en visitant :



![[Pasted image 20250711142645.png]]
