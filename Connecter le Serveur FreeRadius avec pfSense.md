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

## Intégration de l'authentification pfSense avec FreeRADIUS, serveur RADIUS

Pour que pfsense utilise le serveur FreeRadius comme son portail captif, nous allons ajouter pfsense comme client NAS du serveur freeradius pour sécurisé l'accès au réseau locale.

Pour faire cela, on va visité le site de daloradius en cliquant sur le navigateur le
http://10.10.10.10/daloradius et on entre le nom de d'utilisateur et son mot de passe (par défaut le nom d'utilisateur est **administrator** et le mot de passe est **radius**)
![[Pasted image 20250716050158.png]]


Pour ajouter le client de freeradius, nous devons cliquer sur le barre de menu **Management > Nas**

cliquons ensiute **New NAS**

![[Pasted image 20250716050440.png]]
Et appliquer le configuration en cliquant sur le boutons **apply** et verifions en cliquant sur le barre de menu **List NAS**

![[Pasted image 20250716050534.png]]
#### création des groupes des utilisateurs
Pour que les utilisateurs soient classé dans un  groupe qui leurs conviennent, il faut créer des groupes et y affecter des utilisateurs .

pour créer nous allons sur **Management > Profiles > New Profile** et ajoutons le nom du profile et on va sélectionner **quickly Locate attribute with autocomplete input** en entrant **Filter-Id** et cliquons sur le boutons **Add Attribute**
![[Pasted image 20250716052052.png]]



Et ensuite, nous allons remplir les formulaire qui apparaît ci-dessous par :

**Value:** *USERS_BDD*

**Op:**  *:=*

**Target:** *reply*

et on clique sur le boutons **apply** ci-dessus

Grace à cette étapes nous pouvons créer plusieurs profiles

Voici, les listes des groupes que nous avons crée:

![[Pasted image 20250716053147.png]]
On voit qu'il y un groupe qui est crée par défaut dans daloradius et aussi les totales des utilisateurs qui sont dans chaque groupe sont nulle
#### création des utilisateurs pour le teste et affectation dans un groupe
Pour créer un utilisateur, nous allons cliqué sur le barre de menu  **Users > New User**  et remplissons les informations de l'utilisateur
![[Pasted image 20250716053604.png]]

D'après la figure montre qu'on a trois options pour s'authentifier que se soit par le nom d'utilisateur ou par adresse MAC ou Par Code PIN

Mais dans cette simulation, nous allons utilisé l'authentification par Username

![[Pasted image 20250716054124.png]]

pour l'ajouter l'utilisateur bob, nous devons cliqué sur le bouton **apply**

En suivant ces étapes, nous pouvons créée plus des utilisateurs
voici donc la listes des utilisateurs que nous avons crées:

![[Pasted image 20250716054410.png]]

Et maintenants, nous pouvons maintenant ajouté le serveur freeradius comme le serveur d'authentification de pfsense

#### Configurations sur pfsense

Pour faire cela, nous allons rendre sur **System > User Manager  >  Authentication Servers** et nous allons cliqué sur le bouton **+ add**

![[Pasted image 20250716054946.png]]

Ici le nom du serveur est nommé par RADIUS et évidement le type du serveur est RADIUS

![[Pasted image 20250716055050.png]]


On remplies les informations du serveur freeradius : le protocole utilisé, l'adresse IP du serveur, le mot de passe qui doit être le même ce qu'on ajouter sur serveur freeradius Client NAS , le service que Radius doit offrir et l'adresse IP NAS que nous avons attribué dans le serveur. 

Cliquons sur le boutons save pour enregistrer

![[Pasted image 20250716055242.png]]



Et maintenant, nous allons créer une règle pour assurer la communication entre le serveur freeradius et Pfsense

Pour créer une règle sur pfsense, nous allons navigué sur **Firewall > Rules > DMZ

Cliquons sur le boutons **add**

![[Pasted image 20250716055537.png]]
![[Pasted image 20250716055646.png]]
![[Pasted image 20250716055740.png]]

Dans cette règle, nous avons autorisé le serveur freeradius de tous ls flux réseaus TCP/UDP avec l'autorisation des port 1812 pour l'authentification et 1813 pour la comptabilité

Enfin, nous devons appliquer le règle que nous avons créées en cliquant sur le boutons **Apply Changes** qui affiche au dessus lorsqu'on crée une nouvelle règle.

### Teste de la configuration de l'intégration du serveur Radius dans pfsense
 Pour tester de la configuration de freeradius sur pfsense, nous allons sur le barre de menu **Doagnostics > Authentication**

![[Pasted image 20250716060121.png]]
Résultat:

![[Pasted image 20250716060203.png]]

Alors, nous avons réussi la communication entre le serveur freeRadius externe avec pfsense