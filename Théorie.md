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

## sécurité et confiance:
- **ZTNA**:
	ZTNA accorde un accès basé sur la philosophie «savoir pour accéder», c'est à dire qu'il fonctionne sur le principe du **"never trust, always verify"** . Chaque tentative d'accès est toujours authentifié et autorisé, en considérant l'identité de l'utilisateur, du contexte, de létat de l'appareil, etc.  Cela signifie que seuls les utilisateurs et les appareils autorisés sont explicitement identifiés et authentifiés avant d'avoir accès aux ressources à chaque fois. Aucun accès n'est accordé par défaut, même à l'intérieur du réseau.

- **VPN**:
	un VPN n'authentifie qu'une seule fois au début de la connexion. Cela peut être problématique car il expose potentiellement le réseau aux menaces d'initié une fois que la confiance initiale est établie.
	Une fois connecté, l’utilisateur a généralement un accès étendu à tout le réseau interne, ce qui augmente le risque en cas de compromission

### Contrôle d'accès:
- **ZTNA**:
	Applique le principe du moindre privilège par défaut. Il restreint l'accès uniquement aux applications ou aux données requises, réduisant considérablement la surface d'attaque. L'accès peut être révoqué automatiquement en cas de non conformité ou de changement de contexte. 
	
- **VPN**: 
	accordent aux utilisateurs un accès général à toutes les ressources des entreprises une fois authentifiées. Une fois connecté, il y a peu de vérifications supplémentaires. Cela peut amener les utilisateurs à avoir plus d'accès que nécessaire, posant un risque potentiel pour les violations de la conformité.

### Gestion du trafic:
ZTNA interdit uniquement le trafic Internet nécessaire dans le tunnel, réduisant les temps d'attente. En revanche, les VPN acheminent tout le trafic via le réseau d'entreprise, créant des goulots d'étranglement qui peuvent entraîner des retards et des perturbations pour les utilisateurs accédant à la fois sur les ressources internes et les sites Web externes.

### Évolutivité:
ZTNA est une solution basée sur le cloud et sans matériel, ce qui facilite l'évolutivité au besoin. Les VPN traditionnels sont livrés avec des piles de sécurité qui nécessitent des investissements coûteux et une gestion complexe, ce qui rend difficile l'évolution.

### Performance
- **ZTNA**:  
	Offre souvent une expérience plus fluide et moderne. L’accès peut se faire via un navigateur ou un agent léger, sans avoir à lancer un client VPN dédié. L’accès est direct, souvent optimisé pour le cloud, ce qui réduit la latence et améliore la performance, surtout pour les applications SaaS ou multi-cloud

- **VPN**: 
	Peut induire des ralentissements dus au chiffrement et au tunneling centralisé. L’utilisateur doit souvent lancer un client VPN spécifique, ce qui peut compliquer l’expérience, notamment en environnement hybride ou cloud

### Scalabilité
- **ZTNA**: 
	Conçu pour être hautement scalable, adapté aux environnements cloud, multi-cloud et hybrides. La gestion centralisée des politiques et l’automatisation facilitent le déploiement à grande échelle.

- **VPN**:
	Scalabilité plus limitée. Les performances peuvent se dégrader avec le nombre d’utilisateurs, et la gestion de multiples clients et configurations devient complexe à grande échelle.

| Critère                         | ZTNA                                  | VPN traditionnel                 |
| ------------------------------- | ------------------------------------- | -------------------------------- |
| Modèle de confiance             | Zéro confiance, vérification continue | Confiance après authentification |
| Portée d’accès                  | Applications spécifiques              | Réseau entier                    |
| Granularité du contrôle d’accès | Très fine, dynamique                  | Large, statique                  |
| Couche d’intervention           | Application                           | Réseau                           |
| Expérience utilisateur          | Moderne, directe, performante         | Plus lourde, parfois lente       |
| Scalabilité                     | Excellente, cloud-native              | Limitée, gestion complexe        |
| Visibilité & supervision        | Granulaire, centralisée               | Limitée                          |
| Adaptation cloud/SaaS           | Optimale                              | Peu adaptée                      |
| Surface d’attaque               | Minimisée                             | Large                            |
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