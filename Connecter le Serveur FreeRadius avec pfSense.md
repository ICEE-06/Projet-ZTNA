## Configuration du DMZ
- **Création d'une nouvelle interface réseau LAN appelé DMZ**
![[interfaceDMZ.png]]

- **Connecter l'interface réseau du serveur freeRadius à ce LAN**
![[connexionFreeRadiusDMZ.png]]

- Assigner une adresse IP à l'interface DMZ dans pfSense avec tout les configs habituelles.

## Tester l'authentification RADIUS avec pfSense

- **Modifier le fichier clients.conf dans le serveur freeRadius**:
```
sudo nano /etc/freeradius/3.0/clients.conf
```

Ajouter les lignes suivantes à la fin du fichiers:
```
client PFSENSE {
ipaddr = 10.10.10.1 #IP du pfSense
secret = pfsecret123
}
```

- **Modifier le fichier users dans le serveur freeRadius**:
```
sudo nano /etc/freeradius/3.0/users
```

Ajouter les lignes suivantes à la fin du fichiers:
```
admin Cleartext-Password := "123qwe.."
	Class = "pfsense-admin"
```

- **Redémarrer le services freeRadius**:
```
service freeradius restart
```

- Dans pfSense, aller sur l'onglet: **System/User Manager/ Authentication Server**
![[pfsense-authentication-servers.png]]
Sur la zone de paramètres Serveur, effectuez la configuration suivante :
**Nom de description: RADIUS  
Type: RADIUS**
![[serverSettings.png]]

Sur la zone de paramètres RADIUS Server, effectuez la configuration suivante :

```
Protocole - PAP  
Nom d’hôte ou adresse IP - 10.10.10.10 #IP du serveur freeRadius
Secret partagé - pfsecret123
Services offerts - Authentification et comptabilité  
Port d’authentification - 1812  
Port d’Acconting - 1813  
Temps d’arrêt de l’authentification - 5
```

- Aller sur l'ongler **Diagnostics/ Authentication**
Entrez le nom d’utilisateur Admin, son mot de passe et cliquez sur le bouton Test.
![[test authentification.png]]