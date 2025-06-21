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

## Les solutions ZTNA possible

### Sophos
#### à propos de sophos
**Sophos** est une entreprise **spécialisée dans les solutions de cybersécurité**. Elle propose une large gamme de produits et services pour protéger les entreprises contre les menaces en ligne. Sophos se distingue par son approche innovante, axée sur l'intelligence artificielle, l'apprentissage automatique et le partage d'informations sur les menaces en temps réel. Sophos propose pour la plupart du temps des solutions **payantes**.

**ZTNA** fait partie de ses produits.

#### ZTNA de sophos

Le **Sophos ZTNA** est, en tant que ZTNA, une solution de contrôle d'accès réseau basée sur le principe du "**Zero Trust**". 
Le **Sophos ZTNA** présente de nombreux fonctionnalités principaux dont:

- **Connecter les travailleurs distants**:
	Sophos ZTNA permet à vos travailleurs distants d’accéder en toute sécurité et en toute transparence aux applications et aux données dont ils ont besoin, tout en simplifiant le déploiement, l’enrôlement et la gestion par rapport au VPN traditionnel.

- **Micro-segmentation des applications**:
	Sophos ZTNA fournit une micro-segmentation de pointe pour offrir un accès sécurisé aux applications, qu’elles soient hébergées sur site, dans un datacenter ou dans votre infrastructure de Cloud public. Vous bénéficiez également d’une visibilité en temps réel sur l’activité des applications en ce qui concerne leur statut, leur posture de sécurité et leur utilisation. Vous pouvez également contrôler l’accès à de nombreuses **applications SaaS** avec Sophos ZTNA en utilisant des restrictions d’adresse IP pour autoriser uniquement les connexions à partir de vos passerelles ZTNA.

- **Fourni dans le Cloud, Géré dans le Cloud**:
	**Sophos ZTNA** est fourni et géré dans le Cloud et intégré à **Sophos Central** qui est la plateforme de reporting et de gestion de la Cyber sécurité la plus fiable sur le marché

- **Protection Endpoint Next-Gen**
	- Sécurisations des accès aux applications, des postes, et des réseaux contre  les menaces.
	- Sophos ZTNA et Intercept X étant intégrés, partagent en permanences des informations sur l'état de sécurité du système afin d'isoler automatiquement ceux qui sont compromis.
	- Un agent unique, une console unique, un éditeur unique

- **Évolutivité des passerelles applicatives**
	Les passerelles Sophos ZTNA sont gratuites et faciles à déployer là où vous en avez besoin. Disponibles sous forme d’appliance virtuelle, vous pouvez aisément déployer des passerelles à haute disponibilité et les dimensionner selon les besoins de votre entreprise.

- **Intégration de l’identité**
	Avec le Zero Trust, l’identité est essentielle. Sophos ZTNA vérifie en permanence l’identité des utilisateurs grâce à la prise en charge des solutions **IDP (Identity Provider)** les plus populaires, notamment **Microsoft Azure** et **Okta**.


![[Sophos_ZTNA.png]]

**Spécification Technique**


| **Plateformes Prises en charge**           |                                                                                                                                                   |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fournisseurs d’identité                    | Microsoft Azure et Okta                                                                                                                           |
| Plateformes de passerelle Sophos ZTNA      | VMware ESXi 6.5+, Hyper-V 2016+ et AWS ; Prochainement : Sophos Firewall v20 (toutes les plateformes matérielles, virtuelles ou Cloud)            |
| Plateformes du client Sophos ZTNA          | Windows 10 1803 ou supérieur, macOS 11 (Big Sur) ou supérieur ; Toutes les plateformes prennent en charge l’accès sans agent aux applications web |
| État de sécurité de l’appareil Sophos ZTNA | Sophos Security Heartbeat (Intercept X)                                                                                                           |


| **Spécifications des passerelles**    |                                                                                                                 |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| VM recommandée                        | 2 cœurs / 4 Go                                                                                                  |
| Clustering multinœuds                 | Jusqu’à 9 nœuds avec équilibrage de la charge pour les performances, la capacité et la continuité des activités |
| Capacité et dimensionnement des nœuds | 10 000 connexions d’agents pour un seul nœud, jusqu’à 90 000 connexions d’agents dans un cluster (9 nœuds max.) |

### pfSense

#### à propos de pfSense
pfSense est une distribution logicielle libre et open source basée sur FreeBSD, conçue spécifiquement pour servir de **pare-feu (firewall)**, de **routeur**, de **VPN** notamment avec **OpenVPN**, entièrement administrable via une interface web intuitive. Développé initialement en 2004 à partir du projet m0n0wall, pfSense a évolué pour offrir une solution robuste, flexible et extensible, adaptée aussi bien aux petites entreprises, aux particuliers qu’aux grandes organisations.

pfSense est une solution de sécurité réseau complète, flexible et éprouvée, adaptée à tous types d’environnements, du particulier à l’entreprise. Son architecture modulaire, sa gestion centralisée via une interface web et la richesse de ses fonctionnalités en font un choix de référence pour la protection et la gestion des réseaux modernes


#### ZTNA avec pfSense

Grâce à ses nombreuses fonctionnalités et en ajoutant quelques outils supplémentaires, pfSense peut parfaitement être utilisé pour déployer un ZTNA dans un réseau. 

**Les fonctionnalités de pfSense pour un ZTNA**
	- **pare-feu**: Analyse et filtre le trafic réseau en temps réel, protège contre les intrusions et les attaques
	- **Routage**: Prend en charge le routage statique et dynamique, la gestion **multi-WAN**, le **load balancing** et le **failover** pour assurer la continuité de service
	- **VPN**: Support natif d’OpenVPN, IPsec, L2TP/IPsec, permettant la création de tunnels sécurisés pour le télétravail ou l’interconnexion de sites distants
	- **DHCP/DNS**: Serveur DHCP et relais, DNS Forwarder/Resolver, gestion de Dynamic DNS
	- **Gestion des VLAN et réseaux multiples**: Support complet du 802.1q, gestion de plusieurs interfaces et réseaux isolés.
	- **Client Idp (Identy Provider)**: pfSense peut agir comme un client du **EMS (Endpoint Management Server)**, envoyant les requêtes d'authentification des utilisateurs au **EMS**. C'est donc pfSense qui délègue les authentifications.  

