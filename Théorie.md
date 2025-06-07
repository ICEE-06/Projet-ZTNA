## ZTA
### Principes de bases
- **Never trust - Always verify**: utilisation de **NAC**(gestion de l'accès au réseau) par exemple
- **Minimal Access**
- **Asssum breach**: toujours **présumer** qu'on est attaquer (tout le monde peut être un danger, même un employer en interne)

## ZTNA
Le ZTNA est un façon d'appliquer le **ZTA**. Avec le ZTNA pas besoin de créer un VPN pour se connecter à distance.

Le ZTNA est un concept selon lequel quand un utilisateur est déjà reconnue par le réseau et le réseau peut connaitre l'état de cet utilisateur en thermes de **sécurité** (Anti-virus, ...) mais aussi est ce que l'ordinateur appartient à la compagnie. **Comment ça se fait?**
	Il faut d'abord qu'un **Client** soit installé dans l'ordinateur en question. Ce **client** doit être gérer par une entité qui permet de **determiner le statut d'un équipements**. Cette entité est ce qu'on appelle **EMS** pour End-point Management Server. C'est à l' EMS de partager les infos à propos de la machine avec le **Pare-feu** (exemple FortiGate). On utilise après le **Pare-feu** comme **Access-proxy**

![[EMS_FGT.png]]

- À l'**extérieur**( quand un user est à distance), on fait du **ZTNA proxy policy**
- À l'**intérieur**, on fait du **ZTNA IP/MAC Filtring** 
