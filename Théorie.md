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

## ZTNA x VPN


![[ZTNAxVPN.jpg]]

## sécurité:
ZTNA accorde un accès basé sur la philosophie «savoir pour accéder». Cela signifie que seuls les utilisateurs et les appareils autorisés sont explicitement identifiés et authentifiés avant d'avoir accès aux ressources à chaque fois. En revanche, un VPN n'authentifie qu'une seule fois au début de la connexion. Cela peut être problématique car il expose potentiellement le réseau aux menaces d'initié une fois que la confiance initiale est établie.

### Contrôle d'accès:
ZTNA restreint l'accès uniquement aux applications ou aux données requises, réduisant considérablement la surface d'attaque. Les VPN, en revanche, accordent aux utilisateurs un accès général à toutes les ressources des entreprises une fois authentifiées. Cela peut amener les utilisateurs à avoir plus d'accès que nécessaire, posant un risque potentiel pour les violations de la conformité.

### Gestion du trafic:
ZTNA interdit uniquement le trafic Internet nécessaire dans le tunnel, réduisant les temps d'attente. En revanche, les VPN acheminent tout le trafic via le réseau d'entreprise, créant des goulots d'étranglement qui peuvent entraîner des retards et des perturbations pour les utilisateurs accédant à la fois sur les ressources internes et les sites Web externes.

### Évolutivité:
ZTNA est une solution basée sur le cloud et sans matériel, ce qui facilite l'évolutivité au besoin. Les VPN traditionnels sont livrés avec des piles de sécurité qui nécessitent des investissements coûteux et une gestion complexe, ce qui rend difficile l'évolution.

## Avantages du ZTNA
 - **Sécurité amélioré**: 
	 ZTNA crée un tunnel sécurisé et crypté pour l'accès au réseau et la transmission des données, empêchant l'accès non autorisé et les acteurs malveillants.

- **Accès authentifié**:
	ZTNA s'assure que chaque fois que l'accès à votre réseau ne se limite qu'aux appareils et applications autorisés avec des configurations de sécurité appropriées, minimisant le risque de violation à chaque fois.

- **Surface d'attaque réduite**:
	ZTNA accorde l'accès uniquement aux applications ou données requises en fonction des politiques configurées, réduisant ainsi la surface d'attaque en cas de menaces d'initié.

- **Accès BYOD sécurisé:**
	ZTNA garantit que les appareils personnels accédant aux ressources des entreprises respectent les exigences de sécurité par le biais de l'architecture de fiducie zéro intégrée.

- **Travail de n'importe où**:
	ZTNA permet aux employés éloignés d'accéder en toute sécurité aux ressources des entreprises à partir de n'importe quelle partie du monde et à tout moment.

- **Atténuation de la violation des données:**
	Le trafic Internet est en toute sécurité  via le tunnel ZTNA, éliminant les risques des violations de données et un accès non autorisé.