Pour créer un **portail captif** sur pfSense, nous devons d'abord se rendre sur l'onglet **Service/captive portal**
On peut maintenant créer un portail captif qui va permettre aux pc clients de s'authentifier sur le serveur FreeRadius via pfSense:
![[Creation_portail_captif.png]]

Passons maintenant à la configuration du portail captif:
![[Configuration_portail_captif.png]]

Configuration de la page d'authentification:
![[conf_page_authentification.png]]

Choisir la méthode d'authentification:
![[Methode_authentification.png]]

Activer l'envoie au serveur radius des paquets pour qu'il puisse vérifier la compatibilité des informations transmises:
![[activation-transmission_info_to_freeradius.png]]

Maintenant, il ne reste plus qu'à sauvegarder!!