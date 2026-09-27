# 1. Introduction et Concepts Fondamentaux

## 1.1. Généralités et Architecture

### 1.1.1. Système de Gestion de Base de Données (SGBD / DBMS)

Un **Système de Gestion de Base de Données (SGBD)**, ou **Database Management System (DBMS)**, est un logiciel permettant de **créer, stocker, organiser, manipuler, sécuriser et administrer les données** d'une base de données.

Il constitue une interface entre les **applications, les utilisateurs et les données**.

Un SGBD permet notamment :

* de créer et modifier la structure d'une base de données ;
* d'insérer, rechercher, modifier et supprimer des données ;
* de gérer les utilisateurs et leurs droits d'accès ;
* de garantir l'intégrité et la cohérence des données ;
* de gérer les accès simultanés aux données ;
* d'assurer la sauvegarde et la restauration des données.

**Exemples de SGBD :** PostgreSQL, MySQL, Oracle Database, Microsoft SQL Server, MongoDB.

> **Base de données ≠ SGBD**
>
> Une **base de données** est un ensemble organisé de données.
> Un **SGBD** est le logiciel qui permet de créer, gérer et exploiter cette base de données.

---

### 1.1.2. Objectifs d'un SGBD

Un SGBD répond à plusieurs objectifs fondamentaux.

#### a. Indépendance entre les données et les traitements

L'**indépendance des données** signifie que les applications utilisant les données ne doivent pas dépendre directement de leur organisation physique ou, dans une certaine mesure, de leur organisation logique.

On distingue principalement :

* **Indépendance physique** : possibilité de modifier la manière dont les données sont stockées physiquement sans modifier le schéma logique ou les applications.
* **Indépendance logique** : possibilité de modifier le schéma logique sans modifier les vues externes ou les applications concernées.

**Exemple :** ajouter un index pour accélérer une recherche ne doit normalement pas nécessiter de modifier le programme qui effectue cette recherche.

#### b. Réduction de la redondance

La **redondance** correspond au stockage répété d'une même information à plusieurs endroits.

Une bonne conception de la base de données permet de réduire cette redondance, notamment grâce à la **normalisation**.

La réduction de la redondance permet de :

* réduire l'espace de stockage utilisé ;
* éviter les incohérences ;
* limiter les anomalies lors des insertions, modifications ou suppressions.

#### c. Sécurité

Le SGBD permet de contrôler **l'accès aux données** et les opérations que chaque utilisateur est autorisé à effectuer.

Il permet notamment de gérer :

* l'authentification des utilisateurs ;
* les rôles et permissions ;
* les droits de lecture, insertion, modification et suppression ;
* la protection contre les accès non autorisés.

#### d. Intégrité des données

L'**intégrité des données** consiste à garantir que les données restent **valides, cohérentes et conformes aux règles définies**.

Exemples :

* une clé primaire doit être unique ;
* une clé étrangère doit respecter une relation avec une autre table ;
* une colonne définie comme `NOT NULL` ne peut pas contenir de valeur nulle ;
* une contrainte `CHECK` peut imposer une condition sur une valeur.

Les principales contraintes d'intégrité SQL sont :

`PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`.

#### e. Partage des données

Un SGBD permet à **plusieurs utilisateurs et applications d'accéder aux mêmes données**.

Il doit également gérer les accès concurrents afin d'éviter les incohérences lorsque plusieurs opérations sont exécutées simultanément.

Cette gestion repose notamment sur les **transactions** et les mécanismes de contrôle de la concurrence.

---

## 1.2. Architecture ANSI/SPARC

L'architecture **ANSI/SPARC** est un modèle d'architecture des SGBD basé sur **trois niveaux d'abstraction** :

1. **Niveau externe**
2. **Niveau conceptuel**
3. **Niveau interne**

L'objectif principal est de **séparer les différents niveaux de représentation des données** et de favoriser l'indépendance des données.

### 1.2.1. Niveau externe — Vue utilisateur

Le **niveau externe** correspond à la manière dont les données sont **présentées aux utilisateurs ou aux applications**.

Un même système peut proposer plusieurs vues différentes selon les besoins des utilisateurs.

**Exemple :**

Dans une université :

* un étudiant peut consulter ses informations et ses notes ;
* un professeur peut consulter les étudiants et leurs notes ;
* l'administration peut accéder à des informations supplémentaires.

Chaque utilisateur ne voit donc qu'une **vue adaptée à ses besoins**.

---

### 1.2.2. Niveau conceptuel — Schéma logique

Le **niveau conceptuel** décrit la **structure logique globale de la base de données**, indépendamment des détails physiques du stockage.

Il définit notamment :

* les tables ou entités ;
* les attributs ou colonnes ;
* les relations entre les tables ;
* les contraintes d'intégrité.

**Exemple :**

```text
ETUDIANT
---------
id_etudiant
nom
email

MODULE
------
id_module
nom_module

INSCRIPTION
-----------
id_etudiant
id_module
date_inscription
```

À ce niveau, on décrit **quelles données existent et comment elles sont liées**, sans préciser comment elles sont physiquement stockées.

---

### 1.2.3. Niveau interne — Stockage physique

Le **niveau interne** décrit la manière dont les données sont **physiquement stockées et organisées** par le SGBD.

Il concerne notamment :

* les fichiers de données ;
* les pages ou blocs de stockage ;
* les index ;
* les structures de stockage ;
* les méthodes d'accès aux données.

**Exemple :** un SGBD peut utiliser un **index B-tree** pour accélérer les recherches sur une colonne.

Ces détails sont généralement transparents pour l'utilisateur et le développeur.

---

### 1.2.4. Résumé des trois niveaux

| Niveau         | Description                                                |
| -------------- | ---------------------------------------------------------- |
| **Externe**    | Vues adaptées aux utilisateurs et aux applications         |
| **Conceptuel** | Structure logique globale : tables, relations, contraintes |
| **Interne**    | Organisation physique : stockage, fichiers, index          |

> **À retenir :**
>
> **Externe → ce que l'utilisateur voit**
> **Conceptuel → comment les données sont organisées logiquement**
> **Interne → comment les données sont stockées physiquement**

---

## 1.3. Les principaux rôles

### 1.3.1. Administrateur de bases de données (DBA)

Le **DBA (Database Administrator)** est responsable de l'**administration, de la sécurité, des performances et de la disponibilité** des bases de données.

Ses principales responsabilités sont :

* installer et configurer le SGBD ;
* créer et gérer les utilisateurs et les rôles ;
* gérer les permissions ;
* assurer la sécurité des données ;
* effectuer les sauvegardes et restaurations ;
* surveiller et optimiser les performances ;
* gérer la disponibilité de la base de données ;
* intervenir en cas de problème ou d'incident.

### 1.3.2. Développeur

Le **développeur** utilise le SGBD pour intégrer les données dans les applications.

Il peut notamment :

* concevoir ou utiliser le schéma de la base ;
* écrire des requêtes SQL ;
* effectuer des opérations CRUD ;
* utiliser des transactions ;
* connecter l'application au SGBD ;
* optimiser les requêtes utilisées par l'application.

**CRUD** signifie :

* **Create** → créer ;
* **Read** → lire ;
* **Update** → modifier ;
* **Delete** → supprimer.

### 1.3.3. Utilisateur

L'**utilisateur final** utilise les données à travers une application ou une interface.

Il n'a généralement pas besoin de connaître le fonctionnement interne du SGBD.

**Exemple :**

Un client consulte son solde bancaire depuis une application mobile. L'application interroge le SGBD, tandis que le client utilise simplement l'interface de l'application.

---

### 1.3.4. Résumé des rôles

| Rôle            | Responsabilité principale                                       |
| --------------- | --------------------------------------------------------------- |
| **DBA**         | Administrer, sécuriser, sauvegarder et optimiser la base        |
| **Développeur** | Développer les applications et les requêtes utilisant la base   |
| **Utilisateur** | Utiliser les données à travers une application ou une interface |

## 1.2. Typologie des Bases de Données

Les bases de données peuvent être classées selon leur **modèle de données**, leur structure et leur usage. On distingue principalement les **bases relationnelles**, les **bases non relationnelles (NoSQL)** et les **bases décisionnelles / entrepôts de données**.

### 1.2.1. Bases de données relationnelles (SGBDR / RDBMS)

Une **base de données relationnelle** organise les données sous forme de **tables** composées de lignes et de colonnes.

Les tables peuvent être liées entre elles à l'aide de **clés primaires** et de **clés étrangères**.

Les SGBDR utilisent principalement le langage **SQL (Structured Query Language)** pour créer, consulter et manipuler les données.

**Caractéristiques principales :**

* données organisées en tables ;
* schéma généralement défini à l'avance ;
* relations entre les tables ;
* utilisation de clés primaires et étrangères ;
* contraintes d'intégrité ;
* support des transactions ;
* utilisation du langage SQL.

**Exemples :**

* PostgreSQL ;
* MySQL ;
* Oracle Database ;
* Microsoft SQL Server.

**Exemple :**

```text
CLIENT
-------------------------
id_client | nom | email
-------------------------
1         | Ali | ali@mail.com
2         | Sara| sara@mail.com

COMMANDE
------------------------------
id_commande | id_client | montant
------------------------------
101         | 1         | 500
102         | 2         | 250
```

Ici, `id_client` dans la table `COMMANDE` peut être une **clé étrangère** faisant référence à `id_client` dans la table `CLIENT`.

---

### 1.2.2. Bases de données non relationnelles (NoSQL)

Les bases **NoSQL (Not Only SQL)** sont conçues pour stocker et manipuler des données qui ne suivent pas nécessairement le modèle relationnel traditionnel.

Elles sont particulièrement adaptées à certains systèmes nécessitant :

* une grande quantité de données ;
* une structure de données flexible ;
* une forte scalabilité ;
* une distribution des données sur plusieurs serveurs ;
* des accès rapides adaptés à des besoins spécifiques.

Il existe plusieurs grandes familles de bases NoSQL.

#### a. Bases orientées documents

Les données sont stockées sous forme de **documents**, généralement au format JSON ou dans un format similaire.

**Exemple : MongoDB**

```json
{
  "id": 1,
  "nom": "Ali",
  "email": "ali@mail.com",
  "ville": "Casablanca"
}
```

Contrairement à une table relationnelle, différents documents peuvent avoir des structures différentes.

#### b. Bases clé-valeur

Les données sont stockées sous la forme :

```text
clé → valeur
```

Elles sont particulièrement adaptées aux accès très rapides par clé.

**Exemple : Redis**

```text
"user:123" → "Ali"
```

#### c. Bases orientées colonnes

Les données sont organisées selon un modèle adapté au **stockage distribué et aux très grands volumes de données**.

**Exemple : Cassandra**

Elles sont utilisées notamment dans des systèmes nécessitant une forte disponibilité et une capacité à distribuer les données sur plusieurs machines.

#### d. Bases orientées graphes

Les données sont représentées sous forme de **nœuds et de relations**.

Elles sont particulièrement adaptées aux données où les relations entre les éléments sont importantes.

**Exemple : Neo4j**

```text
(Ali) ──[AMI_DE]──> (Sara)
```

**Exemples de SGBD NoSQL :**

* MongoDB → documents ;
* Redis → clé-valeur ;
* Cassandra → colonnes ;
* Neo4j → graphes.

> **À retenir :**
>
> **NoSQL ne signifie pas "sans SQL"**. Le terme est généralement interprété comme **"Not Only SQL"**, car ces systèmes proposent des modèles de données et des mécanismes d'accès différents du modèle relationnel traditionnel.

---

### 1.2.3. Bases de données décisionnelles et Entrepôts de données (Data Warehouse)

Un **Data Warehouse**, ou **entrepôt de données**, est un système conçu principalement pour **stocker et analyser de grandes quantités de données historiques provenant de différentes sources**.

Contrairement à une base de données transactionnelle utilisée quotidiennement par les applications, un Data Warehouse est principalement destiné à l'**analyse**, au **reporting** et à la **Business Intelligence (BI)**.

Les données peuvent provenir de plusieurs sources :

```text
Applications      Bases SQL       Fichiers
     │                │               │
     └────────────────┼───────────────┘
                      ▼
                 ETL / ELT
                      │
                      ▼
              ┌───────────────┐
              │ Data Warehouse│
              └───────────────┘
                      │
                      ▼
              BI / Reporting
```

**Caractéristiques principales :**

* stockage de données historiques ;
* intégration de données provenant de plusieurs sources ;
* optimisation pour les requêtes analytiques ;
* utilisation pour le reporting et la Business Intelligence ;
* traitement de volumes importants de données.

**Exemples :**

* Google BigQuery ;
* Snowflake.

### Base transactionnelle vs Data Warehouse

| Caractéristique | Base transactionnelle               | Data Warehouse                      |
| --------------- | ----------------------------------- | ----------------------------------- |
| Objectif        | Gérer les opérations quotidiennes   | Analyser les données                |
| Données         | Souvent opérationnelles et récentes | Principalement historiques          |
| Opérations      | INSERT, UPDATE, DELETE fréquents    | Requêtes analytiques principalement |
| Utilisation     | Applications métier                 | BI, reporting, analyse              |
| Exemple         | PostgreSQL, MySQL                   | BigQuery, Snowflake                 |

> **À retenir :**
>
> **Base relationnelle → gérer les données et les transactions**
> **NoSQL → modèles flexibles et besoins spécifiques de scalabilité ou de distribution**
> **Data Warehouse → analyser de grandes quantités de données historiques**

# 2. Conception et Modélisation des Données

## 2.1. Le Modèle Conceptuel des Données (MCD - Méthode MERISE)

Le **Modèle Conceptuel des Données (MCD)** est une représentation **abstraite et indépendante du système informatique** permettant de décrire les données d'un système d'information ainsi que les relations entre ces données.

Dans la méthode **MERISE**, le MCD permet de représenter principalement :

* les **entités** ;
* leurs **attributs** ;
* les **associations** entre les entités ;
* les **cardinalités** ;
* les **identifiants**.

L'objectif est de décrire **quelles données existent et quelles relations existent entre elles**, avant de passer à la conception logique puis physique de la base de données.

---

### 2.1.1. Entités

Une **entité** représente un objet ou un élément identifiable du système d'information sur lequel on souhaite conserver des informations.

Une entité peut représenter par exemple :

* un client ;
* un produit ;
* un étudiant ;
* un employé ;
* une commande ;
* un véhicule.

**Exemple :**

Dans une application de gestion d'une université, on peut avoir les entités :

```text
ETUDIANT
PROFESSEUR
MODULE
```

Chaque entité représente une catégorie d'objets du système.

---

### 2.1.2. Attributs

Un **attribut** est une propriété permettant de décrire une entité.

**Exemple :**

L'entité `ETUDIANT` peut posséder les attributs suivants :

```text
ETUDIANT
---------
id_etudiant
nom
prenom
email
date_naissance
```

Ici :

* `id_etudiant` identifie l'étudiant ;
* `nom` représente son nom ;
* `prenom` représente son prénom ;
* `email` représente son adresse électronique ;
* `date_naissance` représente sa date de naissance.

Un attribut doit représenter une **information élémentaire** concernant l'entité.

---

### 2.1.3. Associations

Une **association** représente un **lien entre une ou plusieurs entités**.

Elle permet de décrire une relation qui existe dans le système réel.

**Exemple :**

Un étudiant peut s'inscrire à plusieurs modules.

On peut donc avoir :

```text
ETUDIANT ───── S'INSCRIRE ───── MODULE
```

L'association `S'INSCRIRE` relie les entités `ETUDIANT` et `MODULE`.

Une association peut également posséder ses propres attributs.

**Exemple :**

La date à laquelle un étudiant s'inscrit à un module appartient à l'association :

```text
ETUDIANT ───── S'INSCRIRE ───── MODULE
                    |
                    └── date_inscription
```

`date_inscription` n'est pas une propriété de l'étudiant seul ni du module seul. Elle décrit **la relation entre un étudiant et un module**.

---

### 2.1.4. Cardinalités

La **cardinalité** indique le nombre **minimum et maximum de fois** qu'une occurrence d'une entité peut participer à une association.

Elle est généralement représentée sous la forme :

```text
(minimum, maximum)
```

Les cardinalités principales sont :

* **(0,1)** : participation facultative, au maximum une fois ;
* **(1,1)** : participation obligatoire, exactement une fois ;
* **(0,N)** : participation facultative, plusieurs fois possibles ;
* **(1,N)** : participation obligatoire, une ou plusieurs fois.

### Signification détaillée

| Cardinalité | Signification                      |
| ----------- | ---------------------------------- |
| **(0,1)**   | Zéro ou une occurrence             |
| **(1,1)**   | Exactement une occurrence          |
| **(0,N)**   | Zéro, une ou plusieurs occurrences |
| **(1,N)**   | Une ou plusieurs occurrences       |

---

### Exemple 1 : Client et Commande

Supposons qu'un client puisse passer plusieurs commandes, mais qu'une commande appartienne obligatoirement à un seul client.

```text
CLIENT ───── PASSER ───── COMMANDE

CLIENT      (0,N)
COMMANDE    (1,1)
```

Interprétation :

* Un **client** peut passer **zéro, une ou plusieurs commandes** → `(0,N)`.
* Une **commande** est passée par **exactement un client** → `(1,1)`.

---

### Exemple 2 : Employé et Bureau

Supposons qu'un employé puisse avoir au maximum un bureau et qu'un employé puisse également ne pas avoir de bureau.

```text
EMPLOYE ───── OCCUPER ───── BUREAU

EMPLOYE      (0,1)
BUREAU       (0,1)
```

Dans ce cas, la relation est facultative des deux côtés et chaque employé ou bureau peut être associé à au maximum une occurrence de l'autre côté.

---

### Exemple 3 : Étudiant et Module

Un étudiant peut s'inscrire à plusieurs modules et un module peut être suivi par plusieurs étudiants.

```text
ETUDIANT ───── S'INSCRIRE ───── MODULE

ETUDIANT      (0,N)
MODULE        (0,N)
```

Il s'agit d'une relation **plusieurs-à-plusieurs (N:N)**.

---

### 2.1.5. Identifiant

L'**identifiant** est un attribut, ou un ensemble d'attributs, permettant d'**identifier de manière unique chaque occurrence d'une entité**.

**Exemple :**

```text
ETUDIANT
---------
id_etudiant
nom
prenom
email
```

`id_etudiant` peut être utilisé comme identifiant de l'entité `ETUDIANT`.

Deux étudiants différents ne doivent pas avoir le même `id_etudiant`.

> Dans le modèle conceptuel, l'identifiant correspond à la notion qui deviendra généralement une **clé primaire** lors du passage au modèle relationnel.

### Exemple

```text
ETUDIANT
-------------------------------
# id_etudiant
  nom
  prenom
  email
```

L'identifiant est ici `id_etudiant`.

---

### 2.1.6. Exemple complet de MCD

Considérons une université dans laquelle :

* un étudiant peut s'inscrire à plusieurs modules ;
* un module peut être suivi par plusieurs étudiants ;
* chaque inscription possède une date.

On peut représenter le modèle conceptuel ainsi :

```text
                  (0,N)
ETUDIANT ─────── S'INSCRIRE ─────── MODULE
                  (0,N)
                       |
                       └── date_inscription
```

Avec :

**ETUDIANT**

```text
id_etudiant
nom
prenom
email
```

**MODULE**

```text
id_module
nom_module
coefficient
```

**Association S'INSCRIRE**

```text
date_inscription
```

L'association possède un attribut car la **date d'inscription dépend du couple étudiant-module**.

---

### 2.1.7. Résumé

| Élément         | Rôle                                                   |
| --------------- | ------------------------------------------------------ |
| **Entité**      | Représente un objet ou élément du système              |
| **Attribut**    | Décrit une propriété d'une entité                      |
| **Association** | Représente un lien entre des entités                   |
| **Cardinalité** | Indique le nombre minimum et maximum de participations |
| **Identifiant** | Permet d'identifier une occurrence de manière unique   |

> **À retenir :**
>
> **Entité → ce que l'on veut gérer**
> **Attribut → ce que l'on veut savoir sur l'entité**
> **Association → comment les entités sont liées**
> **Cardinalité → combien de fois elles peuvent être liées**
> **Identifiant → comment distinguer chaque occurrence**

## 2.2. Passage du MCD au MLD (Modèle Logique des Données / Schéma Relationnel)

Le **Modèle Logique des Données (MLD)** correspond à la transformation du **MCD** en une structure adaptée au modèle de données choisi.

Dans le cas d'un modèle relationnel, le MLD décrit les **tables, leurs colonnes, leurs clés primaires et leurs clés étrangères**.

L'objectif est de passer de :

> **MCD : entités + associations + cardinalités**

à :

> **MLD : tables + colonnes + PK + FK**

---

### 2.2.1. Transformation d'une entité en relation

Chaque **entité** du MCD devient généralement une **table** dans le MLD.

Les attributs de l'entité deviennent des **colonnes** et son identifiant devient la **clé primaire (PK)**.

**Exemple :**

MCD :

```text
ETUDIANT
---------
id_etudiant
nom
prenom
email
```

MLD :

```text
ETUDIANT(
    id_etudiant PK,
    nom,
    prenom,
    email
)
```

---

### 2.2.2. Transformation d'une association

La transformation d'une association dépend principalement de ses **cardinalités**.

Les principaux cas sont :

* relation **1:1** ;
* relation **1:N** ;
* relation **N:M**.

---

## 2.3. Gestion d'une relation 1:N

Dans une relation **1:N**, une occurrence de la première entité peut être associée à plusieurs occurrences de la deuxième entité.

**Exemple :**

Un client peut passer plusieurs commandes, mais une commande appartient à un seul client.

```text
CLIENT ───── PASSER ───── COMMANDE

CLIENT      (0,N)
COMMANDE    (1,1)
```

### Règle de transformation

Pour une relation **1:N**, la **clé primaire de l'entité du côté 1 est migrée vers la table située du côté N**.

Cette clé devient une **clé étrangère (FK)**.

```text
CLIENT(
    id_client PK,
    nom,
    email
)

COMMANDE(
    id_commande PK,
    date_commande,
    montant,
    id_client FK
)
```

La colonne `id_client` dans `COMMANDE` référence `CLIENT(id_client)`.

On obtient donc :

```text
CLIENT 1 ───────── N COMMANDE
   PK                  FK
id_client  ───────>  id_client
```

### Pourquoi ?

Une même valeur de `id_client` peut apparaître plusieurs fois dans `COMMANDE`, car un même client peut avoir plusieurs commandes.

En revanche, chaque commande possède un seul `id_client`.

---

## 2.4. Gestion d'une relation N:M

Une relation **N:M** signifie que plusieurs occurrences d'une entité peuvent être associées à plusieurs occurrences d'une autre entité.

**Exemple :**

Un étudiant peut suivre plusieurs modules et un module peut être suivi par plusieurs étudiants.

```text
ETUDIANT ───── SUIVRE ───── MODULE

ETUDIANT      (0,N)
MODULE        (0,N)
```

Une relation N:M **ne peut pas être représentée directement avec une seule clé étrangère** dans l'une des deux tables.

### Règle de transformation

On crée une **table d'association**, également appelée **table intermédiaire**.

Cette table contient :

* la clé primaire de la première table ;
* la clé primaire de la deuxième table ;
* éventuellement les attributs de l'association.

**MLD :**

```text
ETUDIANT(
    id_etudiant PK,
    nom,
    prenom
)

MODULE(
    id_module PK,
    nom_module
)

INSCRIPTION(
    id_etudiant PK, FK,
    id_module PK, FK,
    date_inscription
)
```

Ici, la table `INSCRIPTION` permet de représenter la relation entre les étudiants et les modules.

La clé primaire de `INSCRIPTION` peut être composée de :

```text
(id_etudiant, id_module)
```

Cette combinaison permet d'identifier de manière unique une inscription.

### Représentation

```text
ETUDIANT                 MODULE
   │                       │
   │ PK                    │ PK
   ▼                       ▼
id_etudiant             id_module
   │                       │
   └──────────┬────────────┘
              ▼
        INSCRIPTION
        ───────────
        id_etudiant FK
        id_module   FK
        date_inscription
```

> **À retenir :**
>
> **1:N → la PK du côté 1 devient une FK dans la table du côté N.**
>
> **N:M → création d'une table intermédiaire contenant les PK des deux tables comme FK.**

---

## 2.5. Gestion d'une relation 1:1

Dans une relation **1:1**, une occurrence d'une entité est associée à au maximum une occurrence de l'autre entité.

**Exemple :**

Une personne possède au maximum une carte d'identité et une carte d'identité appartient à une seule personne.

```text
PERSONNE ───── POSSEDER ───── CARTE_IDENTITE

PERSONNE          (0,1)
CARTE_IDENTITE    (1,1)
```

Dans le modèle relationnel, la clé primaire d'une table peut être utilisée comme **clé étrangère** dans l'autre table.

Par exemple :

```text
PERSONNE(
    id_personne PK,
    nom,
    prenom
)

CARTE_IDENTITE(
    id_carte PK,
    numero,
    id_personne FK UNIQUE
)
```

La contrainte `UNIQUE` sur `id_personne` permet d'empêcher qu'une même personne soit associée à plusieurs cartes dans ce modèle.

> Le choix de la table qui reçoit la clé étrangère dépend notamment des cardinalités et des contraintes du modèle.

---

## 2.6. Clé primaire (PK)

La **clé primaire (Primary Key ou PK)** est une colonne, ou un ensemble de colonnes, permettant d'**identifier de manière unique chaque ligne d'une table**.

Une clé primaire doit :

* être unique ;
* ne pas être `NULL` ;
* identifier une seule ligne.

**Exemple :**

```text
CLIENT(
    id_client PK,
    nom,
    email
)
```

Ici, `id_client` identifie chaque client de manière unique.

### Clé primaire composée

Une clé primaire peut être composée de plusieurs colonnes.

**Exemple :**

```text
INSCRIPTION(
    id_etudiant PK,
    id_module PK,
    date_inscription
)
```

La clé primaire est alors :

```text
(id_etudiant, id_module)
```

La combinaison des deux colonnes doit être unique.

---

## 2.7. Clé étrangère (FK)

Une **clé étrangère (Foreign Key ou FK)** est une colonne qui permet de créer une **référence entre deux tables**.

Elle fait généralement référence à la clé primaire d'une autre table.

**Exemple :**

```text
CLIENT(
    id_client PK,
    nom
)

COMMANDE(
    id_commande PK,
    date_commande,
    id_client FK
)
```

Ici :

```text
COMMANDE.id_client
        │
        ▼
CLIENT.id_client
```

La clé étrangère permet donc de relier chaque commande à son client.

Elle participe également au maintien de l'**intégrité référentielle** : une valeur de clé étrangère doit respecter les contraintes définies sur la table référencée.

---

## 2.8. Résumé des principales règles de transformation

| Relation dans le MCD | Transformation dans le MLD                                           |
| -------------------- | -------------------------------------------------------------------- |
| **Entité**           | Devient une table                                                    |
| **Attribut**         | Devient une colonne                                                  |
| **Identifiant**      | Devient une clé primaire (PK)                                        |
| **1:N**              | La PK du côté 1 devient une FK dans la table du côté N               |
| **N:M**              | Création d'une table d'association contenant les PK des deux entités |
| **1:1**              | Une PK est généralement propagée comme FK dans l'une des deux tables |

### Exemple global

MCD :

```text
CLIENT (1) ───── PASSER ───── (N) COMMANDE

ETUDIANT (N) ─── SUIVRE ───── (N) MODULE
```

MLD :

```text
CLIENT(
    id_client PK,
    nom
)

COMMANDE(
    id_commande PK,
    date_commande,
    montant,
    id_client FK
)

ETUDIANT(
    id_etudiant PK,
    nom
)

MODULE(
    id_module PK,
    nom_module
)

INSCRIPTION(
    id_etudiant PK, FK,
    id_module PK, FK,
    date_inscription
)
```

**Idée essentielle :**

> **Le MCD décrit les données et leurs relations de manière conceptuelle.**
>
> **Le MLD transforme cette description en tables, colonnes, clés primaires et clés étrangères.**

## 2.3. La Normalisation (Formes Normales)

La **normalisation** est une méthode de conception des bases de données relationnelles qui consiste à **organiser les données dans plusieurs tables de manière cohérente** afin de réduire la redondance et d'éviter les anomalies lors de la manipulation des données.

Elle repose sur plusieurs **formes normales (FN)**, qui définissent progressivement des règles de structuration des tables.

### Objectifs de la normalisation

La normalisation vise principalement à :

* réduire la redondance des données ;
* éviter les incohérences ;
* faciliter la maintenance de la base ;
* éviter les anomalies d'insertion ;
* éviter les anomalies de mise à jour ;
* éviter les anomalies de suppression.

---

### 2.3.1. Les anomalies liées à une mauvaise conception

Considérons la table suivante :

```text id="x6l1j2"
ETUDIANT_MODULE
------------------------------------------------
id_etudiant | nom | id_module | nom_module | prof
------------------------------------------------
1           | Ali | M01       | SQL        | Karim
2           | Sara| M01       | SQL        | Karim
3           | Omar| M02       | Python     | Nadia
```

Les informations sur le module `M01` sont répétées pour chaque étudiant inscrit.

Cela peut provoquer plusieurs problèmes.

#### Anomalie de mise à jour

Si le professeur du module `M01` change, il faut modifier plusieurs lignes.

Si une ligne n'est pas mise à jour, la base contient des informations contradictoires.

#### Anomalie d'insertion

Supposons qu'un nouveau module soit créé mais qu'aucun étudiant ne soit encore inscrit.

Avec cette structure, il peut être difficile d'enregistrer uniquement le module sans avoir également les informations d'un étudiant.

#### Anomalie de suppression

Si le dernier étudiant inscrit au module `M02` est supprimé, les informations concernant le module `M02` peuvent également disparaître.

La normalisation permet de séparer les informations qui ne dépendent pas directement les unes des autres.

---

## 2.3.2. Dépendance fonctionnelle

La notion de **dépendance fonctionnelle** est fondamentale pour comprendre les formes normales.

On dit qu'un attribut **B dépend fonctionnellement d'un attribut A** lorsque chaque valeur de A détermine une seule valeur de B.

On note :

```text id="0u7jib"
A → B
```

Cela signifie :

> La valeur de A permet de déterminer de manière unique la valeur de B.

**Exemple :**

Dans une table `ETUDIANT` :

```text id="1yq9p8"
id_etudiant → nom
id_etudiant → email
```

Un `id_etudiant` donné correspond à un seul étudiant, donc à un seul nom et à un seul email.

---

## 2.3.3. Première Forme Normale (1FN)

Une table est en **Première Forme Normale (1FN)** si ses attributs contiennent des **valeurs atomiques**, c'est-à-dire des valeurs qui ne sont pas constituées de plusieurs éléments regroupés dans une même cellule.

Chaque cellule doit contenir **une seule valeur**.

### Exemple non conforme à la 1FN

```text id="z9x9xl"
ETUDIANT
--------------------------------
id | nom | téléphones
--------------------------------
1  | Ali | 0611111111, 0622222222
```

La colonne `téléphones` contient plusieurs valeurs dans une même cellule.

### Transformation

On peut créer une structure permettant de stocker chaque numéro séparément :

```text id="exqzqn"
ETUDIANT
----------------
id | nom
----------------
1  | Ali

TELEPHONE
---------------------
id_etudiant | numero
---------------------
1           | 0611111111
1           | 0622222222
```

La table respecte ainsi le principe d'atomicité.

> **1FN = une cellule contient une seule valeur.**

---

## 2.3.4. Deuxième Forme Normale (2FN)

Une table est en **Deuxième Forme Normale (2FN)** si :

1. elle est en **1FN** ;
2. chaque attribut non-clé dépend **de toute la clé primaire**, et non seulement d'une partie de celle-ci.

Cette notion concerne principalement les tables possédant une **clé primaire composée de plusieurs attributs**.

### Exemple

Considérons :

```text id="km7owm"
INSCRIPTION
------------------------------------------------
id_etudiant | id_module | nom_etudiant | nom_module
------------------------------------------------
1           | M01       | Ali          | SQL
1           | M02       | Ali          | Python
2           | M01       | Sara         | SQL
```

Supposons que la clé primaire soit :

```text id="gqv9be"
(id_etudiant, id_module)
```

Les dépendances sont :

```text id="q5u1fd"
id_etudiant → nom_etudiant

id_module → nom_module
```

`nom_etudiant` dépend uniquement de `id_etudiant`, et `nom_module` dépend uniquement de `id_module`.

Ils ne dépendent donc pas de **toute la clé composée**.

La table n'est donc pas en 2FN.

### Décomposition

On peut séparer les informations :

```text id="6w6m4v"
ETUDIANT
--------------------
id_etudiant | nom
--------------------
1           | Ali
2           | Sara

MODULE
--------------------
id_module | nom_module
--------------------
M01       | SQL
M02       | Python

INSCRIPTION
-------------------------
id_etudiant | id_module
-------------------------
1           | M01
1           | M02
2           | M01
```

Les informations sur les étudiants et les modules ne sont plus répétées dans la table `INSCRIPTION`.

> **2FN = 1FN + aucun attribut non-clé ne dépend d'une partie de la clé primaire composée.**

---

## 2.3.5. Troisième Forme Normale (3FN)

Une table est en **Troisième Forme Normale (3FN)** si :

1. elle est en **2FN** ;
2. il n'existe pas de **dépendance fonctionnelle transitive** entre la clé primaire et un attribut non-clé.

Autrement dit, un attribut non-clé ne doit pas dépendre d'un autre attribut non-clé.

### Exemple

Considérons :

```text id="r7t6za"
EMPLOYE
------------------------------------------------
id_employe | nom | id_departement | nom_departement
------------------------------------------------
1          | Ali | D01            | Informatique
2          | Sara| D01            | Informatique
3          | Omar| D02            | Finance
```

On a les dépendances :

```text id="k0u1js"
id_employe → id_departement

id_departement → nom_departement
```

Donc :

```text id="3cykaw"
id_employe → id_departement → nom_departement
```

`nom_departement` dépend indirectement de `id_employe` à travers `id_departement`.

Il existe donc une **dépendance fonctionnelle transitive**.

### Décomposition

On peut séparer les deux informations :

```text id="l3tjck"
EMPLOYE
-----------------------------
id_employe | nom | id_departement
-----------------------------
1          | Ali | D01
2          | Sara| D01
3          | Omar| D02

DEPARTEMENT
----------------------------
id_departement | nom
----------------------------
D01            | Informatique
D02            | Finance
```

On élimine ainsi la dépendance transitive.

> **3FN = 2FN + aucun attribut non-clé ne dépend d'un autre attribut non-clé.**

---

## 2.3.6. Forme Normale de Boyce-Codd (BCNF)

La **BCNF (Boyce-Codd Normal Form)** est une forme normale plus stricte que la 3FN.

Une relation est en **BCNF** si, pour toute dépendance fonctionnelle :

```text id="3qg8qg"
A → B
```

`A` est une **super-clé**.

Autrement dit :

> Tout déterminant d'une dépendance fonctionnelle doit être une super-clé.

La BCNF élimine certains cas particuliers qui peuvent encore exister dans une table respectant la 3FN.

### Exemple conceptuel

Supposons une relation :

```text id="bd6l7b"
COURS
------------------------------------
etudiant | cours | professeur
```

avec les règles :

```text id="u1c5pp"
(etudiant, cours) → professeur

professeur → cours
```

Le déterminant `professeur` n'est pas nécessairement une super-clé de la relation.

La deuxième dépendance peut donc violer la **BCNF**, même si la relation peut satisfaire certaines conditions de la 3FN.

Dans la pratique, la BCNF conduit souvent à une **décomposition supplémentaire** des relations afin que chaque déterminant soit une super-clé.

---

## 2.3.7. Résumé des formes normales

| Forme normale | Condition principale                     |
| ------------- | ---------------------------------------- |
| **1FN**       | Les valeurs sont atomiques               |
| **2FN**       | 1FN + dépendance complète à toute la clé |
| **3FN**       | 2FN + absence de dépendance transitive   |
| **BCNF**      | Tout déterminant est une super-clé       |

### Progression à retenir

```text id="e9n3p5"
1FN
 │
 ├── Valeurs atomiques
 │
 ▼
2FN
 │
 ├── Pas de dépendance partielle
 │
 ▼
3FN
 │
 ├── Pas de dépendance transitive
 │
 ▼
BCNF
 │
 └── Tout déterminant est une super-clé
```

> **À retenir :**
>
> **1FN → Atomicité**
> **2FN → Dépendance à toute la clé**
> **3FN → Pas de dépendance transitive**
> **BCNF → Tout déterminant est une super-clé**

# 3. Le Langage SQL (Structured Query Language)

Le **SQL (Structured Query Language)** est un langage utilisé pour **définir, manipuler, interroger et contrôler les données** dans les bases de données relationnelles.

SQL permet notamment de :

* créer et modifier les structures des tables ;
* insérer, modifier et supprimer des données ;
* rechercher et analyser les données ;
* gérer les utilisateurs et leurs permissions.

Les principales catégories de commandes SQL sont :

| Catégorie     | Signification              | Principales commandes                 |
| ------------- | -------------------------- | ------------------------------------- |
| **DDL / LDD** | Data Definition Language   | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML / LMD** | Data Manipulation Language | `INSERT`, `UPDATE`, `DELETE`          |
| **DQL**       | Data Query Language        | `SELECT`                              |
| **DCL / LCD** | Data Control Language      | `GRANT`, `REVOKE`                     |

---

# 3.1. Langage de Définition de Données (LDD / DDL)

Le **DDL (Data Definition Language)** permet de **définir et modifier la structure** des objets de la base de données, notamment les tables.

Les principales commandes sont :

* `CREATE TABLE`
* `ALTER TABLE`
* `DROP TABLE`
* `TRUNCATE`

---

## 3.1.1. CREATE TABLE

La commande `CREATE TABLE` permet de créer une nouvelle table.

```sql
CREATE TABLE client (
    id_client INT PRIMARY KEY,
    nom VARCHAR(100),
    email VARCHAR(150)
);
```

Ici, la table `client` possède trois colonnes :

* `id_client` ;
* `nom` ;
* `email`.

---

## 3.1.2. ALTER TABLE

La commande `ALTER TABLE` permet de **modifier la structure d'une table existante**.

### Ajouter une colonne

```sql
ALTER TABLE client
ADD COLUMN telephone VARCHAR(20);
```

### Modifier la structure

La syntaxe exacte peut varier selon le SGBD.

Par exemple, PostgreSQL permet :

```sql
ALTER TABLE client
ALTER COLUMN nom TYPE VARCHAR(150);
```

### Supprimer une colonne

```sql
ALTER TABLE client
DROP COLUMN telephone;
```

---

## 3.1.3. DROP TABLE

La commande `DROP TABLE` permet de **supprimer une table ainsi que sa structure et ses données**.

```sql
DROP TABLE client;
```

Après cette opération, la table n'existe plus.

> **Attention :** `DROP TABLE` est une opération destructive. La table et ses données sont supprimées.

---

## 3.1.4. TRUNCATE

La commande `TRUNCATE` permet de **supprimer toutes les lignes d'une table tout en conservant sa structure**.

```sql
TRUNCATE TABLE client;
```

Après l'opération :

```text
Structure de la table → conservée
Données                → supprimées
```

### DROP vs TRUNCATE

| Commande     | Structure | Données    |
| ------------ | --------- | ---------- |
| `DROP TABLE` | Supprimée | Supprimées |
| `TRUNCATE`   | Conservée | Supprimées |

---

## 3.1.5. Contraintes d'intégrité

Les **contraintes** permettent de garantir la validité et la cohérence des données.

### PRIMARY KEY

La contrainte `PRIMARY KEY` identifie de manière unique chaque ligne d'une table.

```sql
CREATE TABLE client (
    id_client INT PRIMARY KEY,
    nom VARCHAR(100)
);
```

Une clé primaire :

* doit être unique ;
* ne peut pas contenir `NULL`.

---

### FOREIGN KEY

La contrainte `FOREIGN KEY` permet de créer une relation entre deux tables.

```sql
CREATE TABLE commande (
    id_commande INT PRIMARY KEY,
    date_commande DATE,
    id_client INT,
    FOREIGN KEY (id_client)
        REFERENCES client(id_client)
);
```

Ici, `id_client` dans `commande` référence `id_client` dans `client`.

---

### NOT NULL

`NOT NULL` interdit l'absence de valeur dans une colonne.

```sql
CREATE TABLE client (
    id_client INT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL
);
```

Le nom doit obligatoirement être renseigné.

---

### UNIQUE

`UNIQUE` garantit qu'une valeur ne peut pas être dupliquée dans une colonne.

```sql
CREATE TABLE client (
    id_client INT PRIMARY KEY,
    email VARCHAR(150) UNIQUE
);
```

Deux clients ne peuvent donc pas avoir la même valeur d'email.

---

### CHECK

`CHECK` permet d'imposer une condition sur les valeurs.

```sql
CREATE TABLE produit (
    id_produit INT PRIMARY KEY,
    prix DECIMAL(10,2) CHECK (prix >= 0)
);
```

Le prix ne peut pas être négatif.

---

### DEFAULT

`DEFAULT` permet de définir une valeur utilisée automatiquement lorsqu'aucune valeur n'est fournie.

```sql
CREATE TABLE client (
    id_client INT PRIMARY KEY,
    nom VARCHAR(100),
    ville VARCHAR(100) DEFAULT 'Casablanca'
);
```

Si aucune ville n'est indiquée, la valeur `Casablanca` sera utilisée.

---

# 3.2. Langage de Manipulation de Données (LMD / DML)

Le **DML (Data Manipulation Language)** permet de **manipuler les données contenues dans les tables**.

Les principales commandes sont :

* `INSERT`
* `UPDATE`
* `DELETE`

---

## 3.2.1. INSERT INTO

`INSERT INTO` permet d'ajouter des lignes dans une table.

```sql
INSERT INTO client (id_client, nom, email)
VALUES (1, 'Ali', 'ali@mail.com');
```

Il est également possible d'insérer plusieurs lignes :

```sql
INSERT INTO client (id_client, nom, email)
VALUES
    (1, 'Ali', 'ali@mail.com'),
    (2, 'Sara', 'sara@mail.com');
```

---

## 3.2.2. UPDATE

`UPDATE` permet de modifier des données existantes.

```sql
UPDATE client
SET email = 'ali@gmail.com'
WHERE id_client = 1;
```

La clause `WHERE` permet de déterminer quelles lignes doivent être modifiées.

> **Attention :** un `UPDATE` sans `WHERE` peut modifier toutes les lignes de la table.

```sql
UPDATE client
SET ville = 'Rabat';
```

Cette requête modifie la ville de **tous les clients**.

---

## 3.2.3. DELETE

`DELETE` permet de supprimer des lignes.

```sql
DELETE FROM client
WHERE id_client = 1;
```

Comme pour `UPDATE`, l'absence de `WHERE` peut avoir un impact important :

```sql
DELETE FROM client;
```

Cette requête supprime **toutes les lignes** de la table.

---

# 3.3. Langage de Requête de Données (DQL / SQL de consultation)

Le **DQL (Data Query Language)** concerne principalement la **consultation des données**, notamment avec la commande `SELECT`.

---

## 3.3.1. SELECT, FROM et WHERE

### SELECT

`SELECT` permet de choisir les colonnes à afficher.

```sql
SELECT nom, email
FROM client;
```

### FROM

`FROM` indique la table ou les tables à interroger.

### WHERE

`WHERE` permet de filtrer les lignes.

```sql
SELECT *
FROM client
WHERE ville = 'Casablanca';
```

La requête retourne uniquement les clients dont la ville est Casablanca.

---

## 3.3.2. Opérateurs de comparaison et logiques

Les principaux opérateurs de comparaison sont :

```text
=      égal
<>     différent
>      supérieur
<      inférieur
>=     supérieur ou égal
<=     inférieur ou égal
```

### AND

Toutes les conditions doivent être vraies.

```sql
SELECT *
FROM produit
WHERE prix > 100
  AND stock > 0;
```

### OR

Au moins une des conditions doit être vraie.

```sql
SELECT *
FROM client
WHERE ville = 'Casablanca'
   OR ville = 'Rabat';
```

### NOT

Inverse une condition.

```sql
SELECT *
FROM client
WHERE NOT ville = 'Casablanca';
```

---

## 3.3.3. LIKE

`LIKE` permet d'effectuer des recherches basées sur un motif.

Le caractère `%` représente zéro, un ou plusieurs caractères.

```sql
SELECT *
FROM client
WHERE nom LIKE 'A%';
```

Retourne les noms qui commencent par `A`.

Le caractère `_` représente exactement un caractère.

```sql
SELECT *
FROM client
WHERE nom LIKE 'A_i';
```

---

## 3.3.4. IN

`IN` permet de vérifier si une valeur appartient à une liste.

```sql
SELECT *
FROM client
WHERE ville IN ('Casablanca', 'Rabat', 'Fès');
```

Cette requête est équivalente à :

```sql
SELECT *
FROM client
WHERE ville = 'Casablanca'
   OR ville = 'Rabat'
   OR ville = 'Fès';
```

---

## 3.3.5. BETWEEN

`BETWEEN` permet de rechercher une valeur comprise dans un intervalle.

```sql
SELECT *
FROM produit
WHERE prix BETWEEN 100 AND 500;
```

---

## 3.3.6. ORDER BY

`ORDER BY` permet de trier les résultats.

### Ordre croissant

```sql
SELECT *
FROM produit
ORDER BY prix ASC;
```

### Ordre décroissant

```sql
SELECT *
FROM produit
ORDER BY prix DESC;
```

`ASC` est l'ordre croissant et `DESC` l'ordre décroissant.

---

## 3.3.7. LIMIT et OFFSET

`LIMIT` permet de limiter le nombre de lignes retournées.

```sql
SELECT *
FROM client
LIMIT 10;
```

`OFFSET` permet d'ignorer un certain nombre de lignes avant de retourner les résultats.

```sql
SELECT *
FROM client
LIMIT 10 OFFSET 20;
```

Cette requête récupère 10 lignes après avoir ignoré les 20 premières.

> La syntaxe et la disponibilité de `LIMIT` peuvent varier selon les SGBD. Par exemple, SQL Server utilise notamment `TOP` ou `OFFSET ... FETCH`.

---

# 3.3.8. Les jointures

Une **jointure (JOIN)** permet de combiner des données provenant de plusieurs tables en fonction d'une condition de correspondance.

Supposons les tables :

```text
CLIENT
-------------------
id_client | nom
-------------------
1         | Ali
2         | Sara

COMMANDE
----------------------------
id_commande | id_client | montant
----------------------------
101         | 1         | 500
102         | 1         | 250
103         | 2         | 300
```

---

## INNER JOIN

`INNER JOIN` retourne uniquement les lignes ayant une correspondance dans les deux tables.

```sql
SELECT c.nom, co.id_commande, co.montant
FROM client c
INNER JOIN commande co
    ON c.id_client = co.id_client;
```

Résultat :

```text
Ali  | 101 | 500
Ali  | 102 | 250
Sara | 103 | 300
```

---

## LEFT JOIN

`LEFT JOIN` retourne **toutes les lignes de la table de gauche**, même lorsqu'aucune correspondance n'existe dans la table de droite.

```sql
SELECT c.nom, co.id_commande
FROM client c
LEFT JOIN commande co
    ON c.id_client = co.id_client;
```

Si un client n'a aucune commande, il apparaîtra quand même dans le résultat avec des valeurs `NULL` pour les colonnes de `commande`.

---

## RIGHT JOIN

`RIGHT JOIN` retourne **toutes les lignes de la table de droite**, même lorsqu'aucune correspondance n'existe dans la table de gauche.

```sql
SELECT c.nom, co.id_commande
FROM client c
RIGHT JOIN commande co
    ON c.id_client = co.id_client;
```

Il est possible d'obtenir le même résultat en inversant les tables et en utilisant un `LEFT JOIN`.

---

## FULL OUTER JOIN

`FULL OUTER JOIN` retourne :

* les lignes correspondant aux deux tables ;
* les lignes uniquement présentes dans la table de gauche ;
* les lignes uniquement présentes dans la table de droite.

```sql
SELECT c.nom, co.id_commande
FROM client c
FULL OUTER JOIN commande co
    ON c.id_client = co.id_client;
```

Les valeurs sans correspondance apparaissent sous forme de `NULL`.

> `FULL OUTER JOIN` n'est pas disponible nativement dans tous les SGBD.

---

## SELF JOIN — Auto-jointure

Une **auto-jointure** consiste à joindre une table avec elle-même.

Elle est utile lorsqu'une table contient une relation entre ses propres lignes.

**Exemple :** un employé possède un responsable qui est lui-même un employé.

```sql
SELECT
    e.nom AS employe,
    r.nom AS responsable
FROM employe e
LEFT JOIN employe r
    ON e.id_responsable = r.id_employe;
```

Ici, la table `employe` est utilisée deux fois avec deux alias :

* `e` → employé ;
* `r` → responsable.

---

## CROSS JOIN — Produit cartésien

`CROSS JOIN` produit toutes les combinaisons possibles entre les lignes de deux tables.

```sql
SELECT *
FROM couleur
CROSS JOIN taille;
```

Si `couleur` contient 3 lignes et `taille` contient 4 lignes :

```text
3 × 4 = 12 combinaisons
```

Le produit cartésien doit donc être utilisé avec précaution lorsque les tables contiennent beaucoup de lignes.

---

# 3.3.9. Agrégation et regroupement

Les **fonctions d'agrégation** permettent de calculer une valeur à partir de plusieurs lignes.

Les principales fonctions sont :

| Fonction  | Rôle                       |
| --------- | -------------------------- |
| `COUNT()` | Compter                    |
| `SUM()`   | Calculer une somme         |
| `AVG()`   | Calculer une moyenne       |
| `MIN()`   | Trouver la valeur minimale |
| `MAX()`   | Trouver la valeur maximale |

### COUNT()

```sql
SELECT COUNT(*) AS nombre_clients
FROM client;
```

Compte le nombre de lignes.

### SUM()

```sql
SELECT SUM(montant) AS chiffre_affaires
FROM commande;
```

Calcule la somme des montants.

### AVG()

```sql
SELECT AVG(montant) AS montant_moyen
FROM commande;
```

Calcule le montant moyen.

### MIN() et MAX()

```sql
SELECT
    MIN(montant) AS montant_min,
    MAX(montant) AS montant_max
FROM commande;
```

---

## GROUP BY

`GROUP BY` permet de **regrouper les lignes selon une ou plusieurs colonnes** avant d'appliquer une fonction d'agrégation.

**Exemple :**

Calculer le chiffre d'affaires par client :

```sql
SELECT
    id_client,
    SUM(montant) AS total_commandes
FROM commande
GROUP BY id_client;
```

Le résultat contient une ligne par client.

---

## HAVING

`HAVING` permet de **filtrer les groupes après l'agrégation**.

**Exemple :**

Afficher uniquement les clients ayant dépensé plus de 1 000 :

```sql
SELECT
    id_client,
    SUM(montant) AS total_commandes
FROM commande
GROUP BY id_client
HAVING SUM(montant) > 1000;
```

### WHERE vs HAVING

La différence essentielle est :

* `WHERE` filtre les **lignes avant le regroupement** ;
* `HAVING` filtre les **groupes après le regroupement**.

```sql
SELECT
    id_client,
    SUM(montant) AS total
FROM commande
WHERE montant > 100
GROUP BY id_client
HAVING SUM(montant) > 1000;
```

---

# 3.3.10. Sous-requêtes

Une **sous-requête** est une requête SQL placée à l'intérieur d'une autre requête.

Elle permet notamment d'utiliser le résultat d'une requête comme entrée d'une autre.

---

## Sous-requête scalaire

Une sous-requête scalaire retourne **une seule valeur**.

**Exemple :**

Afficher les produits dont le prix est supérieur au prix moyen :

```sql
SELECT *
FROM produit
WHERE prix > (
    SELECT AVG(prix)
    FROM produit
);
```

La sous-requête :

```sql
SELECT AVG(prix)
FROM produit
```

retourne une seule valeur.

---

## Sous-requête avec IN

`IN` permet d'utiliser le résultat d'une sous-requête retournant plusieurs valeurs.

**Exemple :**

Afficher les clients ayant passé au moins une commande :

```sql
SELECT *
FROM client
WHERE id_client IN (
    SELECT id_client
    FROM commande
);
```

La sous-requête retourne plusieurs `id_client`.

---

## EXISTS

`EXISTS` vérifie si une sous-requête retourne **au moins une ligne**.

```sql
SELECT *
FROM client c
WHERE EXISTS (
    SELECT 1
    FROM commande co
    WHERE co.id_client = c.id_client
);
```

Cette requête retourne les clients pour lesquels au moins une commande existe.

---

## NOT EXISTS

`NOT EXISTS` vérifie qu'aucune ligne correspondante n'existe.

```sql
SELECT *
FROM client c
WHERE NOT EXISTS (
    SELECT 1
    FROM commande co
    WHERE co.id_client = c.id_client
);
```

Cette requête retourne les clients qui n'ont aucune commande.

---

## Requête corrélée

Une **sous-requête corrélée** dépend d'une valeur provenant de la requête externe.

Dans l'exemple précédent :

```sql
SELECT *
FROM client c
WHERE EXISTS (
    SELECT 1
    FROM commande co
    WHERE co.id_client = c.id_client
);
```

La sous-requête utilise :

```text
c.id_client
```

qui provient de la requête externe.

La sous-requête est donc **corrélée** à la requête principale.

> **À retenir :**
>
> Une sous-requête classique peut être exécutée indépendamment de la requête externe.
>
> Une sous-requête corrélée fait référence aux colonnes de la requête externe.

---

# 3.4. Langage de Contrôle de Données (LCD / DCL)

Le **DCL (Data Control Language)** permet de **gérer les droits d'accès aux données et aux objets de la base de données**.

Les principales commandes sont :

* `GRANT`
* `REVOKE`

---

## 3.4.1. GRANT

`GRANT` permet d'accorder des permissions à un utilisateur ou à un rôle.

**Exemple :**

```sql
GRANT SELECT
ON client
TO utilisateur1;
```

L'utilisateur `utilisateur1` peut maintenant effectuer des requêtes `SELECT` sur la table `client`.

On peut également accorder plusieurs permissions :

```sql
GRANT SELECT, INSERT, UPDATE
ON client
TO utilisateur1;
```

---

## 3.4.2. REVOKE

`REVOKE` permet de retirer une permission précédemment accordée.

```sql
REVOKE INSERT
ON client
FROM utilisateur1;
```

L'utilisateur conserve les autres permissions qui lui ont éventuellement été accordées.

---

## 3.4.3. Résumé des catégories SQL

| Catégorie     | Objectif              | Commandes principales                 |
| ------------- | --------------------- | ------------------------------------- |
| **DDL / LDD** | Définir la structure  | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML / LMD** | Modifier les données  | `INSERT`, `UPDATE`, `DELETE`          |
| **DQL**       | Consulter les données | `SELECT`                              |
| **DCL / LCD** | Gérer les permissions | `GRANT`, `REVOKE`                     |

> **À retenir :**
>
> **DDL → structure**
> **DML → données**
> **DQL → consultation**
> **DCL → droits d'accès**

# 4. Transactabilité, Concurrence et Sécurité

## 4.1. Gestion des Transactions

### 4.1.1. Notion de transaction

Une **transaction** est un ensemble d'opérations SQL qui sont exécutées comme une **unité logique de travail**.

Une transaction doit permettre de garantir qu'une opération complexe est soit **entièrement réalisée**, soit **annulée** en cas de problème.

**Exemple :** transfert de 500 DH du compte A vers le compte B.

L'opération nécessite deux modifications :

```text
1. Retirer 500 DH du compte A
2. Ajouter 500 DH au compte B
```

Ces deux opérations doivent être considérées comme une seule transaction.

Si le retrait est effectué mais que le dépôt échoue, la transaction doit pouvoir être annulée afin de revenir à l'état initial.

---

### 4.1.2. Principales commandes de transaction

#### BEGIN / START TRANSACTION

Permet de commencer une transaction.

```sql
BEGIN;
```

ou :

```sql
START TRANSACTION;
```

#### COMMIT

`COMMIT` valide définitivement les modifications effectuées pendant la transaction.

```sql
COMMIT;
```

Après un `COMMIT`, les changements sont normalement considérés comme validés.

#### ROLLBACK

`ROLLBACK` annule les modifications effectuées depuis le début de la transaction ou depuis un point de sauvegarde approprié.

```sql
ROLLBACK;
```

### Exemple

```sql
BEGIN;

UPDATE compte
SET solde = solde - 500
WHERE id_compte = 1;

UPDATE compte
SET solde = solde + 500
WHERE id_compte = 2;

COMMIT;
```

Si une erreur survient avant le `COMMIT`, on peut annuler les modifications :

```sql
ROLLBACK;
```

> **À retenir :**
>
> `BEGIN` → commencer la transaction
> `COMMIT` → valider les modifications
> `ROLLBACK` → annuler les modifications

---

# 4.1.3. Les propriétés ACID

Les transactions doivent respecter quatre propriétés fondamentales regroupées sous l'acronyme **ACID** :

* **A** → Atomicité ;
* **C** → Cohérence ;
* **I** → Isolation ;
* **D** → Durabilité.

---

### A — Atomicité

L'**atomicité** signifie qu'une transaction est exécutée selon le principe :

> **Tout ou rien.**

Toutes les opérations de la transaction doivent être validées, ou aucune ne doit l'être.

**Exemple :**

Lors d'un transfert :

```text
Compte A : -500 DH
Compte B : +500 DH
```

Si la deuxième opération échoue, la première doit également être annulée.

---

### C — Cohérence

La **cohérence** signifie qu'une transaction doit faire passer la base de données d'un **état valide à un autre état valide**.

Les contraintes d'intégrité doivent continuer à être respectées.

**Exemple :**

Si une colonne possède :

```sql
CHECK (solde >= 0)
```

une transaction ne doit pas laisser la base dans un état où cette contrainte est violée.

---

### I — Isolation

L'**isolation** garantit que les transactions exécutées simultanément ne doivent pas produire d'interactions incorrectes.

Chaque transaction doit avoir une vision des données conforme au **niveau d'isolation** configuré.

Elle permet notamment de contrôler les problèmes liés aux accès concurrents.

---

### D — Durabilité

La **durabilité** signifie qu'une fois qu'une transaction a été validée avec `COMMIT`, ses modifications doivent **persister**, notamment après une panne du système.

Les SGBD utilisent différents mécanismes, notamment les journaux de transactions, pour assurer cette propriété.

> **Résumé ACID :**
>
> **Atomicité → tout ou rien**
> **Cohérence → données toujours valides**
> **Isolation → transactions concurrentes isolées selon le niveau choisi**
> **Durabilité → changements validés conservés**

---

# 4.2. Concurrence d'accès et Verrouillage

## 4.2.1. Notion de concurrence

La **concurrence** correspond à la situation dans laquelle **plusieurs transactions accèdent simultanément aux mêmes données**.

Cette situation est normale dans les systèmes multi-utilisateurs.

**Exemple :**

Deux utilisateurs consultent et modifient simultanément le solde d'un même compte.

Sans mécanisme de contrôle de concurrence, ces opérations peuvent produire des résultats incorrects.

Le SGBD utilise notamment les **niveaux d'isolation**, les **verrous** et parfois le **contrôle de concurrence multiversion (MVCC)** pour gérer ces situations.

---

# 4.2.2. Lecture sale — Dirty Read

Une **lecture sale (Dirty Read)** se produit lorsqu'une transaction lit une donnée qui a été modifiée par une autre transaction mais **pas encore validée avec `COMMIT`**.

### Exemple

Transaction A :

```text
Solde = 1000
        ↓
Modification
        ↓
Solde = 500
```

Transaction B lit alors :

```text
Solde = 500
```

Mais la transaction A effectue finalement :

```text
ROLLBACK
```

Le solde réel revient à :

```text
1000
```

La transaction B avait donc lu une valeur qui n'a finalement jamais été validée.

> **Dirty Read = lire une donnée non validée.**

---

# 4.2.3. Lecture non répétable — Non-repeatable Read

Une **lecture non répétable** se produit lorsqu'une même transaction lit deux fois la même ligne et obtient **deux valeurs différentes**, car une autre transaction a modifié et validé cette ligne entre les deux lectures.

### Exemple

Transaction A :

```text
Première lecture → solde = 1000
```

Transaction B :

```text
UPDATE compte
SET solde = 500;
COMMIT;
```

Transaction A effectue ensuite une deuxième lecture :

```text
Deuxième lecture → solde = 500
```

La même requête effectuée dans la même transaction peut donc observer une valeur différente.

> **Non-repeatable Read = une même ligne change entre deux lectures.**

---

# 4.2.4. Lecture fantôme — Phantom Read

Une **lecture fantôme (Phantom Read)** se produit lorsqu'une transaction exécute deux fois une requête retournant un ensemble de lignes et constate que **des lignes ont été ajoutées ou supprimées** entre les deux lectures par une autre transaction.

### Exemple

Transaction A :

```sql
SELECT *
FROM client
WHERE ville = 'Casablanca';
```

Elle obtient :

```text
3 clients
```

Transaction B ajoute ensuite un nouveau client de Casablanca et valide :

```sql
INSERT INTO client (...)
VALUES (..., 'Casablanca');

COMMIT;
```

Transaction A exécute à nouveau la même requête :

```sql
SELECT *
FROM client
WHERE ville = 'Casablanca';
```

Elle obtient maintenant :

```text
4 clients
```

La nouvelle ligne constitue une **ligne fantôme**.

> **Phantom Read = l'ensemble des lignes correspondant à une requête change entre deux lectures.**

---

# 4.2.5. Comparaison des problèmes de concurrence

| Problème                | Description                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| **Dirty Read**          | Lecture d'une donnée non encore validée                                 |
| **Non-repeatable Read** | Une même ligne possède une valeur différente lors d'une seconde lecture |
| **Phantom Read**        | L'ensemble des lignes retournées par une requête change                 |

---

# 4.2.6. Niveaux d'isolation SQL

Les principaux niveaux d'isolation définis par le standard SQL sont :

1. `READ UNCOMMITTED`
2. `READ COMMITTED`
3. `REPEATABLE READ`
4. `SERIALIZABLE`

Plus le niveau d'isolation est élevé, plus les transactions sont isolées, mais cela peut généralement avoir un impact sur la **concurrence et les performances**.

---

### READ UNCOMMITTED

C'est le niveau d'isolation le plus faible.

Une transaction peut potentiellement lire des données modifiées par une autre transaction avant leur validation.

Il peut donc permettre des **Dirty Reads**.

```text
READ UNCOMMITTED
    ↓
Dirty Read possible
```

---

### READ COMMITTED

Une transaction ne lit normalement que des données **validées**.

Les Dirty Reads sont donc évitées.

Cependant, une même ligne peut changer entre deux lectures.

```text
READ COMMITTED
    ↓
Dirty Read            → évitée
Non-repeatable Read   → possible
Phantom Read          → possible
```

---

### REPEATABLE READ

Ce niveau garantit qu'une ligne déjà lue par une transaction ne change pas de manière visible pour cette transaction pendant sa durée, selon la sémantique du SGBD.

Il empêche les **Dirty Reads** et les **Non-repeatable Reads**.

Les Phantom Reads peuvent dépendre du SGBD et de son mécanisme de concurrence.

```text
REPEATABLE READ
    ↓
Dirty Read            → évitée
Non-repeatable Read   → évitée
Phantom Read          → dépend du SGBD
```

---

### SERIALIZABLE

`SERIALIZABLE` est le niveau d'isolation le plus élevé parmi les niveaux SQL standards.

L'objectif est que les transactions concurrentes produisent un résultat équivalent à une **exécution séquentielle** des transactions.

Il offre la plus forte isolation, mais peut réduire la concurrence et augmenter les risques d'attente ou de conflits.

```text
SERIALIZABLE
    ↓
Isolation maximale
    ↓
Concurrence généralement plus faible
```

---

### Résumé des niveaux d'isolation

| Niveau               | Dirty Read | Non-repeatable Read | Phantom Read   |
| -------------------- | ---------- | ------------------- | -------------- |
| **Read Uncommitted** | Possible   | Possible            | Possible       |
| **Read Committed**   | Évitée     | Possible            | Possible       |
| **Repeatable Read**  | Évitée     | Évitée              | Dépend du SGBD |
| **Serializable**     | Évitée     | Évitée              | Évitée         |

> Les comportements exacts peuvent varier selon le SGBD et son mécanisme de contrôle de concurrence.

---

# 4.2.7. Verrouillage

Le **verrouillage (locking)** est une technique utilisée par les SGBD pour contrôler les accès concurrents aux données.

Les deux principaux types de verrous sont :

* **verrou partagé (Shared Lock / S)** ;
* **verrou exclusif (Exclusive Lock / X)**.

---

## Verrou partagé (Shared Lock)

Un **verrou partagé** est généralement utilisé lors d'une opération de lecture.

Plusieurs transactions peuvent généralement détenir simultanément un verrou partagé sur la même donnée.

```text
Transaction A → lecture → Shared Lock
Transaction B → lecture → Shared Lock
```

Les lectures peuvent donc être concurrentes.

---

## Verrou exclusif (Exclusive Lock)

Un **verrou exclusif** est généralement utilisé lorsqu'une transaction modifie une donnée.

Pendant qu'un verrou exclusif est détenu, les autres transactions ne peuvent normalement pas effectuer des opérations incompatibles sur cette même donnée.

```text
Transaction A → modification → Exclusive Lock
                         ↓
              autres accès incompatibles
                         ↓
                      bloqués
```

### Compatibilité simplifiée

|                   |     Shared (S) |  Exclusive (X) |
| ----------------- | -------------: | -------------: |
| **Shared (S)**    |     Compatible | Non compatible |
| **Exclusive (X)** | Non compatible | Non compatible |

---

# 4.2.8. Verrouillage pessimiste

Le **verrouillage pessimiste** part du principe qu'un conflit est **possible ou probable**.

La transaction verrouille donc les données avant de les modifier ou de les utiliser dans une opération critique.

**Exemple :**

```sql
SELECT *
FROM compte
WHERE id_compte = 1
FOR UPDATE;
```

Le compte est verrouillé pour permettre une modification contrôlée par la transaction.

Cette approche peut être adaptée lorsque les conflits sont fréquents et qu'il est important d'empêcher les modifications concurrentes.

---

# 4.2.9. Verrouillage optimiste

Le **verrouillage optimiste** part du principe que les conflits sont relativement rares.

Au lieu de bloquer immédiatement les données, le système vérifie au moment de la modification que les données n'ont pas été modifiées entre-temps.

Une technique courante consiste à utiliser un **numéro de version**.

Exemple :

```text
id_compte | solde | version
---------------------------
1         | 1000  | 5
```

L'application lit la version `5`.

Lors de la mise à jour :

```sql
UPDATE compte
SET solde = 900,
    version = 6
WHERE id_compte = 1
  AND version = 5;
```

Si une autre transaction a déjà modifié la ligne et changé la version, la condition `version = 5` ne sera plus satisfaite.

L'application détecte alors un **conflit de concurrence** et peut demander une nouvelle lecture ou retenter l'opération.

---

## 4.2.10. Comparaison des stratégies de verrouillage

| Aspect       | Verrouillage pessimiste                        | Verrouillage optimiste                            |
| ------------ | ---------------------------------------------- | ------------------------------------------------- |
| Hypothèse    | Les conflits peuvent être fréquents            | Les conflits sont rares                           |
| Blocage      | Utilise des verrous pour prévenir les conflits | Évite généralement les verrous longs              |
| Détection    | Avant ou pendant l'accès                       | Lors de la validation de la modification          |
| Avantage     | Évite certains conflits en les bloquant        | Bonne concurrence lorsque les conflits sont rares |
| Inconvénient | Peut provoquer des attentes ou blocages        | Peut nécessiter de recommencer une opération      |

> **À retenir :**
>
> **Transaction → unité logique de travail**
> **ACID → propriétés garantissant la fiabilité des transactions**
> **Isolation → contrôle des interactions entre transactions concurrentes**
> **Verrou partagé → principalement utilisé pour la lecture**
> **Verrou exclusif → principalement utilisé pour la modification**
> **Pessimiste → on se protège contre le conflit à l'avance**
> **Optimiste → on vérifie l'existence d'un conflit au moment de la modification**

# 5. Optimisation, Indexation et Administration

## 5.1. Indexation

Un **index** est une structure de données associée à une table permettant au SGBD de **retrouver plus rapidement les lignes correspondant à une condition de recherche**, sans parcourir systématiquement toute la table.

### Rôle d'un index

Sans index, le SGBD peut être amené à effectuer un **Full Table Scan**, c'est-à-dire parcourir les lignes de la table une par une.

Avec un index approprié, il peut utiliser une structure spécialisée pour localiser plus rapidement les lignes recherchées.

Exemple :

```sql
SELECT *
FROM clients
WHERE email = 'client@example.com';
```

Un index sur `email` peut permettre au SGBD de retrouver directement la ligne correspondante au lieu de parcourir toute la table.

Cependant, les index ont également un **coût** :

* ils occupent de l'espace disque ;
* ils doivent être maintenus lors des `INSERT`, `UPDATE` et `DELETE` ;
* un nombre excessif d'index peut donc ralentir les opérations d'écriture.

### Création d'un index

```sql
CREATE INDEX idx_client_email
ON clients(email);
```

Pour supprimer un index :

```sql
DROP INDEX idx_client_email;
```

La syntaxe exacte peut varier selon le SGBD.

### Principales structures d'index

#### B-Tree / B+Tree

Les arbres **B-Tree** et **B+Tree** sont parmi les structures d'index les plus courantes dans les SGBD relationnels.

Ils sont particulièrement adaptés aux recherches :

* par égalité ;
* par intervalle (`>`, `<`, `BETWEEN`) ;
* avec des valeurs ordonnées.

Exemple :

```sql
CREATE INDEX idx_client_age
ON clients(age);
```

L'index peut être utile pour :

```sql
SELECT *
FROM clients
WHERE age BETWEEN 20 AND 30;
```

#### Hash Index

Un **Hash Index** utilise une fonction de hachage pour associer une valeur à une position dans la structure d'index.

Il est particulièrement adapté aux recherches par **égalité** :

```sql
WHERE id = 150
```

mais généralement moins adapté aux recherches par intervalle :

```sql
WHERE id BETWEEN 100 AND 200
```

#### Bitmap Index

Un **Bitmap Index** représente les valeurs sous forme de bitmaps.

Il peut être particulièrement efficace pour des colonnes ayant **peu de valeurs distinctes** (faible cardinalité), notamment dans certains systèmes orientés décisionnel/analytique.

Exemple de colonne à faible cardinalité :

```text
sexe      : F, M
statut    : Actif, Inactif
```

Les bitmap indexes sont notamment associés à certains SGBD et charges analytiques ; ils ne constituent pas le choix général pour les applications transactionnelles.

### Index unique

Un index peut également garantir l'unicité des valeurs :

```sql
CREATE UNIQUE INDEX idx_client_email
ON clients(email);
```

Deux clients ne pourront alors pas avoir la même adresse email, sous réserve des règles de gestion des valeurs `NULL` propres au SGBD.

### Index primaire, clustered et secondaire

Il faut distinguer **clé primaire**, **index clustered** et **index secondaire** : ces notions ne sont pas synonymes dans tous les SGBD.

#### Clé primaire (Primary Key)

La **clé primaire** est une contrainte permettant d'identifier chaque ligne de manière unique.

```sql
CREATE TABLE clients (
    id INT PRIMARY KEY,
    nom VARCHAR(100)
);
```

Un SGBD peut créer automatiquement un index pour prendre en charge cette contrainte, mais le type et l'organisation physique de cet index dépendent du SGBD.

#### Clustered Index

Un **clustered index** détermine généralement l'organisation physique des données selon la clé d'index.

Il ne peut donc généralement y avoir qu'un seul clustered index par table.

Par exemple, dans certains SGBD, les données peuvent être organisées selon :

```text
ID : 1 → 2 → 3 → 4 → 5 → ...
```

Cela facilite notamment certaines recherches et lectures par plages.

#### Non-clustered / Secondary Index

Un **index secondaire** possède une structure séparée permettant de retrouver les lignes de la table.

Une table peut généralement avoir plusieurs index secondaires.

Exemple :

```text
Table clients
     |
     +-- Index sur email
     +-- Index sur nom
     +-- Index sur ville
```

La distinction exacte entre **clustered** et **non-clustered** dépend toutefois du SGBD. Par exemple, PostgreSQL ne possède pas de clustered index permanent au même sens que SQL Server.

### Index composite

Un **index composite** porte sur plusieurs colonnes :

```sql
CREATE INDEX idx_client_ville_nom
ON clients(ville, nom);
```

L'ordre des colonnes est important.

Cet index peut être particulièrement utile pour des requêtes telles que :

```sql
SELECT *
FROM clients
WHERE ville = 'Casablanca'
AND nom = 'Ali';
```

Il faut donc choisir les colonnes et leur ordre en fonction des requêtes réellement exécutées.

### Quand utiliser un index ?

Les index sont particulièrement intéressants sur :

* les colonnes utilisées fréquemment dans `WHERE` ;
* les colonnes utilisées dans les `JOIN` ;
* certaines colonnes utilisées dans `ORDER BY` ;
* certaines colonnes utilisées dans `GROUP BY` ;
* les colonnes ayant une cardinalité adaptée au type de requête.

Il ne faut cependant pas indexer systématiquement toutes les colonnes.

---

## 5.2. Optimisation des Requêtes

L'**optimisation des requêtes** consiste à améliorer les performances d'exécution des requêtes SQL en réduisant notamment :

* le temps d'exécution ;
* les lectures disque ;
* l'utilisation de la mémoire ;
* la consommation CPU ;
* les opérations inutiles.

Le SGBD possède généralement un **optimiseur de requêtes (Query Optimizer)** qui choisit un plan d'exécution parmi plusieurs possibilités.

### Plan d'exécution

Un **plan d'exécution** décrit la manière dont le SGBD prévoit ou réalise l'exécution d'une requête.

Il peut notamment indiquer :

* les tables parcourues ;
* l'utilisation ou non des index ;
* le type de jointure utilisé ;
* le nombre de lignes estimé ou réellement traité ;
* le coût estimé de chaque opération.

### EXPLAIN

La commande `EXPLAIN` permet d'obtenir le plan d'exécution estimé d'une requête.

Exemple avec PostgreSQL :

```sql
EXPLAIN
SELECT *
FROM clients
WHERE email = 'client@example.com';
```

Le résultat permet notamment de voir si le SGBD envisage un **Index Scan** ou un **Sequential Scan**.

### EXPLAIN ANALYZE

`EXPLAIN ANALYZE` exécute réellement la requête et fournit des informations sur son exécution.

```sql
EXPLAIN ANALYZE
SELECT *
FROM clients
WHERE email = 'client@example.com';
```

Il permet notamment de comparer :

* le nombre de lignes estimé ;
* le nombre de lignes réellement obtenu ;
* le temps d'exécution ;
* les opérations effectivement réalisées.

> **Attention :** contrairement à `EXPLAIN`, `EXPLAIN ANALYZE` exécute réellement la requête. Il faut donc être prudent avec les requêtes `INSERT`, `UPDATE` ou `DELETE`.

### Quelques bonnes pratiques SQL

#### Éviter `SELECT *` lorsque toutes les colonnes ne sont pas nécessaires

Au lieu de :

```sql
SELECT *
FROM clients;
```

préférer :

```sql
SELECT id, nom, email
FROM clients;
```

Cela permet notamment de réduire la quantité de données transférées et traitées.

#### Filtrer les données le plus tôt possible

Au lieu de récupérer inutilement un grand volume de données :

```sql
SELECT *
FROM commandes;
```

on peut appliquer directement une condition :

```sql
SELECT id, montant
FROM commandes
WHERE montant > 1000;
```

#### Éviter les fonctions sur les colonnes indexées lorsque cela empêche l'utilisation efficace de l'index

Par exemple :

```sql
WHERE LOWER(email) = 'client@example.com'
```

peut empêcher l'utilisation d'un index classique sur `email` selon le SGBD.

Une solution peut être d'utiliser un **index fonctionnel** lorsque le SGBD le permet :

```sql
CREATE INDEX idx_email_lower
ON clients(LOWER(email));
```

#### Vérifier les jointures

Les colonnes utilisées pour les jointures doivent être correctement choisies et, lorsque cela est pertinent, indexées.

```sql
SELECT c.nom, co.montant
FROM clients c
JOIN commandes co
    ON c.id = co.client_id;
```

Un index sur `commandes(client_id)` peut être utile selon le volume de données et le plan choisi.

### Optimisation et statistiques

Le SGBD utilise des **statistiques** sur les données pour estimer le nombre de lignes correspondant à une condition et choisir un plan d'exécution.

Des statistiques obsolètes peuvent conduire à un mauvais choix de plan.

L'optimisation ne consiste donc pas simplement à « ajouter des index » : il faut analyser les requêtes, les données, les statistiques et les plans d'exécution.

---

## 5.3. Objets Programmables et Vues

Les SGBD proposent différents objets permettant de **réutiliser des requêtes, encapsuler de la logique métier ou automatiser certaines opérations**.

Les principaux sont :

* les vues ;
* les vues matérialisées ;
* les fonctions ;
* les procédures stockées ;
* les déclencheurs (triggers).

### 5.3.1. Vues (Views)

Une **vue** est une table virtuelle basée sur une requête SQL.

Elle ne stocke généralement pas elle-même les données résultantes ; elle stocke essentiellement la définition de la requête.

Exemple :

```sql
CREATE VIEW clients_actifs AS
SELECT id, nom, email
FROM clients
WHERE statut = 'ACTIF';
```

On peut ensuite utiliser la vue comme une table :

```sql
SELECT *
FROM clients_actifs;
```

#### Avantages des vues

Les vues peuvent permettre de :

* simplifier des requêtes complexes ;
* masquer certaines colonnes sensibles ;
* réutiliser une requête ;
* fournir une interface stable aux applications ;
* contrôler l'accès aux données.

### 5.3.2. Vues matérialisées

Une **vue matérialisée (Materialized View)** stocke physiquement le résultat de la requête.

Elle peut donc accélérer certaines requêtes coûteuses, notamment dans les environnements analytiques.

Exemple :

```sql
CREATE MATERIALIZED VIEW ventes_par_client AS
SELECT client_id, SUM(montant) AS total_ventes
FROM commandes
GROUP BY client_id;
```

Le résultat doit cependant être **actualisé** lorsque les données sources changent.

Dans PostgreSQL :

```sql
REFRESH MATERIALIZED VIEW ventes_par_client;
```

On a donc un compromis :

| Vue                                            | Vue matérialisée                            |
| ---------------------------------------------- | ------------------------------------------- |
| Résultat calculé lors de la consultation       | Résultat stocké                             |
| Données généralement à jour                    | Données potentiellement obsolètes           |
| Pas de stockage du résultat                    | Stockage du résultat                        |
| Moins de maintenance                           | Nécessite un rafraîchissement               |
| Peut être plus lente pour une requête complexe | Peut être beaucoup plus rapide à la lecture |

### 5.3.3. Fonctions et procédures stockées

Une **fonction stockée** est un programme enregistré dans le SGBD pouvant recevoir des paramètres, effectuer des opérations et retourner une valeur ou un ensemble de résultats selon le SGBD.

Une **procédure stockée** est également un programme exécuté côté serveur, mais sa sémantique et sa gestion du retour de valeurs dépendent du SGBD.

Les langages utilisés dépendent du système :

* **PL/SQL** : Oracle ;
* **PL/pgSQL** : PostgreSQL ;
* T-SQL : SQL Server.

Exemple simplifié en PostgreSQL :

```sql
CREATE FUNCTION calcul_ttc(prix NUMERIC)
RETURNS NUMERIC
AS $$
BEGIN
    RETURN prix * 1.20;
END;
$$ LANGUAGE plpgsql;
```

Utilisation :

```sql
SELECT calcul_ttc(100);
```

Les fonctions et procédures permettent notamment de :

* centraliser une logique métier ;
* réutiliser du code ;
* réduire certains traitements côté application ;
* exécuter des traitements directement sur le serveur de base de données.

### 5.3.4. Déclencheurs (Triggers)

Un **trigger** est un mécanisme qui déclenche automatiquement l'exécution d'une fonction ou d'une action lorsqu'un événement défini se produit sur une table ou un autre objet.

Les événements courants sont :

* `INSERT` ;
* `UPDATE` ;
* `DELETE`.

Les déclencheurs peuvent être exécutés notamment :

* **BEFORE** : avant l'opération ;
* **AFTER** : après l'opération.

Exemple conceptuel :

```text
INSERT d'un client
       ↓
   Trigger
       ↓
Enregistrement automatique
dans une table d'historique
```

Exemple simplifié :

```sql
CREATE TRIGGER log_client
AFTER INSERT ON clients
FOR EACH ROW
EXECUTE FUNCTION enregistrer_historique();
```

Les triggers peuvent être utilisés pour :

* enregistrer des modifications ;
* maintenir certaines données dérivées ;
* appliquer automatiquement certaines règles ;
* assurer une traçabilité (audit).

Cependant, une utilisation excessive des triggers peut rendre le comportement d'une base de données plus difficile à comprendre et à maintenir.

---

## À retenir

| Concept              | Rôle principal                                                           |
| -------------------- | ------------------------------------------------------------------------ |
| **Index**            | Accélérer certaines recherches                                           |
| **B-Tree / B+Tree**  | Index adapté notamment aux égalités et aux recherches par intervalle     |
| **Hash Index**       | Recherche efficace par égalité                                           |
| **Bitmap Index**     | Adapté à certains contextes analytiques et colonnes à faible cardinalité |
| **Index composite**  | Index basé sur plusieurs colonnes                                        |
| **EXPLAIN**          | Examiner le plan d'exécution estimé                                      |
| **EXPLAIN ANALYZE**  | Exécuter et analyser réellement la requête                               |
| **Vue**              | Requête enregistrée présentée comme une table virtuelle                  |
| **Vue matérialisée** | Résultat d'une requête stocké physiquement                               |
| **Fonction**         | Programme stocké pouvant retourner une valeur/résultat                   |
| **Procédure**        | Programme stocké exécutant un traitement                                 |
| **Trigger**          | Exécution automatique déclenchée par un événement                        |

### Points essentiels

* Un index **accélère certaines lectures mais ajoute un coût aux écritures et au stockage**.
* Il faut choisir les index en fonction des **requêtes réellement exécutées**.
* `EXPLAIN` et `EXPLAIN ANALYZE` sont essentiels pour comprendre les performances.
* L'optimisation ne consiste pas uniquement à créer des index : il faut également analyser les requêtes et les plans d'exécution.
* Une **vue** simplifie l'accès à des données calculées dynamiquement.
* Une **vue matérialisée** stocke le résultat et doit être rafraîchie.
* Les **fonctions, procédures et triggers** permettent d'exécuter de la logique directement dans le SGBD.
* Les détails d'implémentation des index et des objets programmables peuvent varier selon le SGBD.

# 6. Le Paradigme NoSQL et Big Data

## 6.1. Théorème de CAP (Brewer)

Le **théorème CAP**, formulé par Eric Brewer, concerne les systèmes distribués.

Il décrit un arbitrage entre trois propriétés :

* **C — Consistency (Cohérence)** : toutes les opérations de lecture voient une donnée cohérente selon le modèle de cohérence choisi.
* **A — Availability (Disponibilité)** : chaque requête reçue par un nœud disponible obtient une réponse, même en cas de problème sur une partie du système.
* **P — Partition Tolerance (Tolérance au partitionnement)** : le système continue à fonctionner malgré une rupture de communication entre certains nœuds du réseau.

### Le principe fondamental

Le théorème CAP ne signifie pas simplement qu'un système doit choisir **2 propriétés parmi 3**.

Dans un système distribué, une **partition réseau** peut se produire. Lorsqu'elle survient, le système doit alors faire un choix entre :

* maintenir la **cohérence (C)** ;
* maintenir la **disponibilité (A)**.

La **tolérance au partitionnement (P)** devient donc une nécessité pour les systèmes distribués qui doivent continuer à fonctionner malgré les problèmes réseau.

On peut représenter cette situation ainsi :

```text
                 Système distribué
                       |
              Partition réseau
                       |
              +--------+--------+
              |                 |
        Cohérence (C)      Disponibilité (A)
        privilégiée        privilégiée
```

### Exemple

Imaginons une base de données répliquée sur deux serveurs :

```text
Serveur A  <------ réseau ------>  Serveur B
```

Une partition réseau se produit :

```text
Serveur A      X      Serveur B
```

Les deux serveurs ne peuvent plus communiquer.

Supposons qu'une donnée possède la valeur :

```text
solde = 1000 DH
```

Une transaction sur le serveur A modifie cette valeur :

```text
solde = 800 DH
```

Le serveur B n'a pas encore reçu cette modification.

Le système doit alors gérer le conflit entre :

* **Cohérence** : empêcher certaines lectures/écritures tant que les serveurs ne peuvent pas se synchroniser ;
* **Disponibilité** : continuer à accepter les requêtes malgré l'absence de communication.

### CAP et systèmes NoSQL

Dans la pratique, les systèmes distribués font des choix différents concernant la cohérence et la disponibilité.

On parle souvent de systèmes :

* **CP** : privilégient la cohérence lors d'une partition ;
* **AP** : privilégient la disponibilité lors d'une partition.

Le comportement exact dépend cependant du SGBD, de sa configuration et du niveau de cohérence demandé.

> **À retenir :** CAP concerne principalement le comportement d'un système distribué **lorsqu'une partition réseau survient**. Il ne signifie pas qu'un système est simplement « C ou A ou P » dans toutes les situations.

---

## 6.2. Les Familles NoSQL

**NoSQL** signifie généralement **Not Only SQL**.

Les bases NoSQL ont été conçues notamment pour répondre à certains besoins liés :

* aux très grands volumes de données ;
* à la distribution sur plusieurs serveurs ;
* à la haute disponibilité ;
* à la scalabilité horizontale ;
* aux données semi-structurées ou non structurées.

Contrairement aux bases relationnelles, elles ne reposent pas nécessairement sur le modèle classique des tables, lignes et relations.

On distingue principalement quatre grandes familles :

1. Clé-Valeur ;
2. Orientée Document ;
3. Orientée Colonnes ;
4. Orientée Graphe.

---

### 6.2.1. Bases Clé-Valeur

Une base **clé-valeur (Key-Value)** associe une clé unique à une valeur.

```text
Clé             Valeur
------------------------------
user:1001       "Hamza"
user:1002       "Ahmed"
user:1003       "Sara"
```

La clé permet d'accéder directement à la valeur.

### Exemple

Avec Redis :

```text
SET user:1001 "Hamza"
GET user:1001
```

Résultat :

```text
"Hamza"
```

### Caractéristiques

* accès très rapide par clé ;
* modèle simple ;
* facilement distribuable ;
* particulièrement adapté au cache ;
* adapté aux sessions utilisateur et certaines données temporaires.

### Exemples

* **Redis**
* **Memcached**

> Redis offre cependant beaucoup plus de fonctionnalités qu'un simple stockage clé-valeur, notamment des structures de données comme les listes, ensembles, sorted sets et hashes.

---

### 6.2.2. Bases Orientées Document

Une base **orientée document** stocke les données sous forme de documents, généralement proches du format JSON.

Par exemple :

```json
{
  "id": 101,
  "nom": "Hamza",
  "ville": "Casablanca",
  "competences": [
    "Python",
    "SQL",
    "Machine Learning"
  ]
}
```

Contrairement à une table relationnelle où les colonnes sont généralement définies à l'avance, les documents peuvent avoir des structures différentes.

Exemple :

```json
{
  "id": 101,
  "nom": "Hamza"
}
```

et :

```json
{
  "id": 102,
  "nom": "Sara",
  "ville": "Rabat",
  "age": 25
}
```

peuvent coexister dans une même collection selon le système et ses règles de validation.

### Exemple : MongoDB

MongoDB utilise le format **BSON (Binary JSON)** pour représenter les documents.

Une collection peut être comparée conceptuellement à une table relationnelle :

```text
Base de données
      |
      +── Collection : clients
              |
              +── Document
              +── Document
              +── Document
```

### Caractéristiques

* schéma flexible ;
* représentation naturelle des données hiérarchiques ;
* bonne intégration avec les applications utilisant JSON ;
* possibilité de distribuer les données horizontalement.

### Exemples

* **MongoDB**
* **CouchDB**

---

### 6.2.3. Bases Orientées Colonnes

Les bases **orientées colonnes** sont conçues pour gérer de grandes quantités de données distribuées, avec notamment des charges importantes en écriture et des accès adaptés à certains traitements analytiques.

Exemples :

* **Apache Cassandra**
* **Apache HBase**

Il faut toutefois distinguer ces systèmes du **stockage en colonnes utilisé dans certains Data Warehouses** : les architectures et modèles de données ne sont pas identiques.

### Exemple conceptuel

Dans un modèle relationnel classique :

```text
Ligne 1 : ID | Nom    | Ville
Ligne 2 : ID | Nom    | Ville
Ligne 3 : ID | Nom    | Ville
```

Un système orienté colonnes organise les données de manière permettant de regrouper efficacement les valeurs associées aux colonnes ou familles de colonnes, selon le système.

### Cassandra

Cassandra est conçu pour :

* fonctionner sur plusieurs nœuds ;
* supporter de très grands volumes ;
* fournir une forte disponibilité ;
* supporter des débits d'écriture importants ;
* permettre une **scalabilité horizontale**.

Son modèle est basé sur des **tables**, mais sa conception et ses mécanismes internes sont différents d'un SGBD relationnel classique.

### HBase

HBase est une base distribuée construite au-dessus de l'écosystème Hadoop.

Elle est adaptée notamment aux très grands volumes de données distribuées.

---

### 6.2.4. Bases Orientées Graphe

Une base **orientée graphe** représente les données sous forme de :

* **nœuds (nodes)** ;
* **relations (edges)** ;
* **propriétés (properties)**.

Exemple :

```text
[Hamza]
   |
   | connaît
   ↓
[Ahmed]
   |
   | travaille_avec
   ↓
[Sara]
```

Chaque nœud peut posséder des propriétés :

```text
Personne
----------------
nom : Hamza
âge : 25
ville : Casablanca
```

Les relations peuvent également posséder des propriétés.

### Exemple : Neo4j

Neo4j est un système de gestion de bases de données orienté graphe.

Il peut être utilisé pour représenter :

* les réseaux sociaux ;
* les systèmes de recommandation ;
* les réseaux de transport ;
* les relations entre entreprises ;
* les systèmes de détection de fraude ;
* les dépendances entre objets.

Une requête Neo4j peut être écrite avec **Cypher** :

```cypher
MATCH (p:Personne)-[:CONNAIT]->(ami:Personne)
WHERE p.nom = 'Hamza'
RETURN ami;
```

Cette requête recherche les personnes connues par Hamza.

---

## 6.3. Comparaison des principales familles NoSQL

| Famille        | Structure                       | Exemple          | Cas d'utilisation typique                     |
| -------------- | ------------------------------- | ---------------- | --------------------------------------------- |
| **Clé-Valeur** | Clé → Valeur                    | Redis, Memcached | Cache, sessions, accès rapide                 |
| **Document**   | Documents JSON/BSON             | MongoDB, CouchDB | Applications web, données semi-structurées    |
| **Colonnes**   | Colonnes / familles de colonnes | Cassandra, HBase | Très grands volumes, systèmes distribués      |
| **Graphe**     | Nœuds + relations               | Neo4j            | Réseaux, recommandations, relations complexes |

---

## 6.4. NoSQL vs Bases Relationnelles

Le choix entre SQL et NoSQL dépend principalement des **besoins de l'application**.

| Critère                  | Relationnel                    | NoSQL                                |
| ------------------------ | ------------------------------ | ------------------------------------ |
| Modèle                   | Tables et relations            | Plusieurs modèles possibles          |
| Schéma                   | Généralement structuré         | Souvent plus flexible                |
| Transactions             | Très développées               | Dépendent du système                 |
| Relations complexes      | Très adaptées                  | Variable selon la famille            |
| Scalabilité horizontale  | Possible                       | Très courante                        |
| Cohérence                | Souvent forte                  | Variable selon le système            |
| Données semi-structurées | Possible                       | Souvent bien adaptée                 |
| Cas typique              | Applications transactionnelles | Systèmes distribués à grande échelle |

### Important

NoSQL ne signifie pas **« SQL est dépassé »**.

Les bases relationnelles restent particulièrement adaptées lorsque l'application nécessite :

* des transactions complexes ;
* une forte intégrité référentielle ;
* des relations nombreuses entre les données ;
* une structure de données relativement stable.

Les bases NoSQL sont particulièrement intéressantes lorsque l'on recherche, selon le système :

* une grande scalabilité horizontale ;
* une distribution sur plusieurs machines ;
* une haute disponibilité ;
* une grande flexibilité de modèle ;
* la gestion de volumes importants de données.

---

## À retenir

* **CAP** décrit un compromis entre **Cohérence, Disponibilité et Tolérance au partitionnement** dans les systèmes distribués.
* Lorsqu'une partition réseau survient, un système distribué doit arbitrer entre **Cohérence et Disponibilité**.
* **Key-Value** : accès rapide à partir d'une clé → Redis.
* **Document** : données semi-structurées sous forme de documents → MongoDB.
* **Colonnes** : grands volumes et systèmes distribués → Cassandra, HBase.
* **Graphe** : relations complexes entre entités → Neo4j.
* **NoSQL ne remplace pas systématiquement le relationnel** : le choix dépend des besoins fonctionnels et techniques.
