# BobApp

Clone project:

> git clone XXXXX

## Front-end 

Go inside folder the front folder:

> cd front

Install dependencies:

> npm install

Launch Front-end:

> npm run start;

### Docker

Build the container:

> docker build -t bobapp-front .  

Start the container:

> docker run -p 8080:8080 --name bobapp-front -d bobapp-front

## Back-end

Go inside folder the back folder:

> cd back

Install dependencies:

> mvn clean install

Launch Back-end:

>  mvn spring-boot:run

Launch the tests:

> mvn clean install

### Docker

Build the container:

> docker build -t bobapp-back .  

Start the container:

> docker run -p 8080:8080 --name bobapp-back -d bobapp-back


### Workflow
# Workflow GitHub Action : Lancement des tests frontend en Angular avec couverture

## Description
Ce workflow GitHub Action est exécuté chaque fois qu'une **pull request** est créée sur la branche `main` ou lorsqu'il est déclenché manuellement via `workflow_dispatch`. Il a pour objectif de tester l'application frontend en Angular, de générer un rapport de couverture de code, et de stocker ce rapport pour une analyse ultérieure.

## Objectif
- Exécuter les tests unitaires sur le frontend en Angular.
- Générer et stocker un rapport de couverture de code pour analyser la qualité du code testé.

## Étapes du workflow

1. **Vérification du dépôt**
   - **Action utilisée** : `actions/checkout@v4`
   - **Objectif** : Récupérer le code source du repository pour l'exécution des tests.

2. **Configuration de Node.js**
   - **Action utilisée** : `actions/setup-node@v4`
   - **Objectif** : Installer et configurer la version 20 de Node.js pour l'exécution des commandes npm.

3. **Installation des dépendances**
   - **Commande** : `npm install --legacy-peer-deps`
   - **Objectif** : Installer les dépendances du projet Angular dans le dossier `front` en utilisant npm. L'option `--legacy-peer-deps` est utilisée pour résoudre des problèmes de compatibilité avec les dépendances peer.

4. **Installation d'Angular CLI**
   - **Commande** : `npm install -g @angular/cli@14`
   - **Objectif** : Installer globalement la version 14 d'Angular CLI pour permettre l'exécution de commandes Angular, notamment pour exécuter les tests.

5. **Installation de DevKit**
   - **Commande** : `npm install --save-dev @angular-devkit/build-angular@14`
   - **Objectif** : Installer le package `@angular-devkit/build-angular` en tant que dépendance de développement pour permettre la compilation et les tests dans Angular.

6. **Exécution des tests avec couverture**
   - **Commande** : `npm run test -- --watch=false --browsers=ChromeHeadless --code-coverage`
   - **Objectif** : Lancer les tests unitaires en mode tête sans surveillance (non interactif), utiliser le navigateur sans interface graphique (`ChromeHeadless`) et générer un rapport de couverture de code.

7. **Stockage du rapport de couverture**
   - **Action utilisée** : `actions/upload-artifact@v4`
   - **Objectif** : Télécharger et stocker le rapport de couverture généré dans le répertoire `front/coverage` comme un artefact pour une analyse ultérieure.

## KPIs Suivis

1. **Couverture de code minimale** : L'objectif est de maintenir une couverture de code d'au moins 80 %. Cela garantit que la majorité du code est testé, ce qui permet de détecter des erreurs potentielles plus tôt dans le processus de développement.

2. **Temps d'exécution des tests** : Le temps d'exécution des tests est une métrique importante pour s'assurer que le workflow fonctionne efficacement et rapidement.

## Résultats Attendus
Après l'exécution du workflow, voici ce que tu devrais observer :
- Les tests unitaires du frontend sont exécutés.
- Un rapport de couverture de code est généré et stocké en tant qu'artefact.
- La couverture de code actuelle et les résultats des tests sont disponibles pour consultation.

## Recommandations
- **Améliorer la couverture de code** : Si la couverture de code est en dessous du seuil minimal de 80 %, il est recommandé de rajouter des tests supplémentaires pour améliorer la couverture.
- **Optimiser les performances** : Si le temps d'exécution des tests dépasse un certain seuil (par exemple 5 minutes), il est conseillé d'examiner les tests pour voir s'il est possible de les paralléliser ou de les optimiser.

# Workflow GitHub Action : Lancement des tests backend en Java avec couverture

## Description
Ce workflow GitHub Action est exécuté chaque fois qu'une **pull request** est créée sur la branche `main` ou lorsqu'il est déclenché manuellement via `workflow_dispatch`. Il a pour objectif de tester l'application backend en Java, de générer un rapport de couverture de code via JaCoCo, et de stocker ce rapport pour une analyse ultérieure.

## Objectif
- Exécuter les tests unitaires sur le backend en Java.
- Générer et stocker un rapport de couverture de code pour analyser la qualité du code testé.

## Étapes du workflow

1. **Vérification du dépôt**
   - **Action utilisée** : `actions/checkout@v4`
   - **Objectif** : Récupérer le code source du repository pour l'exécution des tests.

2. **Configuration de JDK 11**
   - **Action utilisée** : `actions/setup-java@v4`
   - **Objectif** : Installer et configurer JDK 11 avec la distribution `temurin`. La configuration inclut également la mise en cache des dépendances Maven pour accélérer les builds suivants.

3. **Construction avec Maven**
   - **Commande** : `mvn clean install`
   - **Objectif** : Exécuter la commande Maven pour nettoyer le projet et installer les dépendances, tout en construisant le projet.

4. **Exécution des tests avec JaCoCo**
   - **Commande** : `mvn test jacoco:report`
   - **Objectif** : Lancer les tests unitaires en utilisant Maven et générer un rapport de couverture de code avec JaCoCo.

5. **Stockage du rapport JaCoCo**
   - **Action utilisée** : `actions/upload-artifact@v4`
   - **Objectif** : Télécharger et stocker le rapport JaCoCo généré dans le répertoire `back/target/site/jacoco` comme un artefact pour une analyse ultérieure.

## KPIs Suivis

1. **Couverture de code minimale** : L'objectif est de maintenir une couverture de code d'au moins 80 %. Cela garantit que la majorité du code est testé, ce qui permet de détecter des erreurs potentielles plus tôt dans le processus de développement.

2. **Temps d'exécution des tests** : Le temps d'exécution des tests est une métrique importante pour s'assurer que le workflow fonctionne efficacement et rapidement.

## Résultats Attendus
Après l'exécution du workflow, voici ce que tu devrais observer :
- Les tests unitaires du backend en Java sont exécutés.
- Un rapport de couverture de code est généré et stocké en tant qu'artefact.
- La couverture de code actuelle et les résultats des tests sont disponibles pour consultation.

## Recommandations
- **Améliorer la couverture de code** : Si la couverture de code est en dessous du seuil minimal de 80 %, il est recommandé de rajouter des tests supplémentaires pour améliorer la couverture.
- **Optimiser les performances** : Si le temps d'exécution des tests dépasse un certain seuil (par exemple 5 minutes), il est conseillé d'examiner les tests pour voir s'il est possible de les paralléliser ou de les optimiser.

  
# Workflow GitHub Action : Build and Analyze Frontend SonarQube

## Description
Ce workflow GitHub Action est exécuté chaque fois qu'une **pull request** est créée sur la branche `main` ou lorsqu'il est déclenché manuellement via `workflow_dispatch`. Il permet de construire l'application frontend et de l'analyser avec SonarQube pour détecter les problèmes de qualité du code, la couverture des tests et d'autres métriques.

## Objectif
- Construire l'application frontend.
- Analyser l'application avec SonarQube pour vérifier la qualité du code.
- Rapporter les résultats d'analyse à l'interface SonarQube.

## Étapes du workflow

1. **Vérification du dépôt**
   - **Action utilisée** : `actions/checkout@v4`
   - **Objectif** : Récupérer le code source du repository pour l'exécution des étapes suivantes.

2. **Configuration de Node.js**
   - **Action utilisée** : `actions/setup-node@v4`
   - **Objectif** : Configurer Node.js avec la version 20 et mettre en cache les dépendances à l'aide de `npm`.

3. **Installation des dépendances**
   - **Commande** : `npm install --legacy-peer-deps`
   - **Objectif** : Installer les dépendances du projet frontend à l'aide de `npm`.

4. **Test de connectivité avec SonarQube**
   - **Commande** : `curl -v "${{ secrets.SONAR_HOST_URL }}/api/server/version"`
   - **Objectif** : Tester la connectivité avec le serveur SonarQube pour s'assurer que la connexion est fonctionnelle avant d'analyser le code.

5. **Mise en cache des packages SonarQube**
   - **Action utilisée** : `actions/cache@v4`
   - **Objectif** : Mettre en cache les fichiers et dépendances SonarQube pour accélérer les exécutions futures du workflow.

6. **Analyse avec SonarQube**
   - **Commande** : `npx sonar-scanner`
   - **Objectif** : Lancer l'analyse de l'application frontend avec SonarQube, en spécifiant les clés du projet et l'URL du serveur SonarQube pour récupérer et analyser les métriques du code.
   - **Environnement** : Utilisation des secrets `SONARQUBE_FRONTEND_TOKEN` et `SONAR_HOST_URL` pour authentifier l'analyse.

## KPIs Suivis

1. **Couverture de code** : SonarQube fournit des métriques sur la couverture de code, ce qui permet de s'assurer que le code est bien testé. Il est recommandé d'avoir une couverture d'au moins 80 %.
   
2. **Bugs et vulnérabilités** : SonarQube analyse le code pour détecter les bugs, les vulnérabilités de sécurité et les mauvaises pratiques. L'objectif est de réduire leur nombre au minimum.

## Résultats Attendus
Après l'exécution du workflow, les résultats de l'analyse sont disponibles dans l'interface web de SonarQube. Ces résultats incluent :
- La couverture de code.
- La détection des bugs et vulnérabilités.
- L'indice de qualité du code (qualité globale).
  
### Accès aux résultats
Les résultats de l'analyse peuvent être consultés en vous rendant sur la page du projet dans SonarQube. Par défaut, SonarQube est accessible via l'URL suivante :  

**URL de SonarQube** : `http://localhost:9000`

Une fois connecté à l'interface de SonarQube :

1. **Connexion à SonarQube** :
   - Ouvre un navigateur et accède à l'URL `http://localhost:9000` (si tu utilises SonarQube en local).
   - Si tu utilises SonarQube sur un serveur distant, remplace `localhost` par l'adresse de ton serveur SonarQube.
   - Connecte-toi avec tes identifiants.

2. **Accéder au tableau de bord du projet** :
   - Après t'être connecté à SonarQube, dans le tableau de bord principal, recherche ou accède à ton projet : **BobAppFrontend**.
   - L'URL de ton projet SonarQube sera sous la forme suivante :
     ```
     http://localhost:9000/dashboard?id=BobAppFrontend
     ```

3. **Consulter les métriques** :
   - Sur le tableau de bord du projet **BobAppFrontend**, tu pourras voir les métriques d'analyse du code :
     - **Couverture de code**.
     - **Bugs et vulnérabilités**.
     - **Code Smells**.
     - **Complexité**.

   Ces informations seront mises à jour après chaque exécution du workflow GitHub Action.

## Recommandations
- **Améliorer la couverture de code** : Si la couverture de code est en dessous du seuil minimal de 80 %, il est recommandé de rajouter des tests supplémentaires pour améliorer la couverture.
- **Corriger les bugs critiques** : Si SonarQube détecte des bugs ou vulnérabilités critiques, il est essentiel de les résoudre pour garantir la stabilité et la sécurité de l'application.


# Workflow GitHub Action : Build and Analyze Backend SonarQube

## Description
Ce workflow GitHub Action est déclenché chaque fois qu'une **pull request** est créée sur la branche `main` ou lorsqu'il est lancé manuellement via `workflow_dispatch`. Il permet de construire l'application backend et de l'analyser avec SonarQube pour détecter les problèmes de qualité du code, la couverture des tests et d'autres métriques.

## Objectif
- Construire l'application backend.
- Analyser l'application avec SonarQube pour vérifier la qualité du code.
- Rapporter les résultats d'analyse à l'interface SonarQube.

## Étapes du workflow

1. **Vérification du dépôt**
   - **Action utilisée** : `actions/checkout@v4`
   - **Objectif** : Récupérer le code source du repository pour l'exécution des étapes suivantes.

2. **Configuration de JDK 11**
   - **Action utilisée** : `actions/setup-java@v4`
   - **Objectif** : Configurer JDK 11 à l'aide de la distribution `zulu`.

3. **Test de connectivité avec SonarQube**
   - **Commande** : `curl -v "${{ secrets.SONAR_HOST_URL }}/api/server/version"`
   - **Objectif** : Tester la connectivité avec le serveur SonarQube pour s'assurer que la connexion est fonctionnelle avant d'analyser le code.

4. **Mise en cache des packages SonarQube**
   - **Action utilisée** : `actions/cache@v4`
   - **Objectif** : Mettre en cache les fichiers et dépendances SonarQube pour accélérer les exécutions futures du workflow.

5. **Mise en cache des packages Maven**
   - **Action utilisée** : `actions/cache@v4`
   - **Objectif** : Mettre en cache les dépendances Maven pour accélérer la phase de construction des builds futurs.

6. **Construction et analyse avec SonarQube**
   - **Commande** : `mvn -B verify org.sonarsource.scanner.maven:sonar-maven-plugin:5.0.0.4389:sonar`
   - **Objectif** : Lancer l'analyse de l'application backend avec SonarQube en spécifiant les clés du projet et l'URL du serveur SonarQube pour récupérer et analyser les métriques du code.
   - **Environnement** : Utilisation des secrets `SONARQUBE_BACKEND_TOKEN` et `SONAR_HOST_URL` pour authentifier l'analyse.

## KPIs Suivis

1. **Couverture de code** : SonarQube fournit des métriques sur la couverture de code, ce qui permet de s'assurer que le code est bien testé. Il est recommandé d'avoir une couverture d'au moins 80 %.
   
2. **Bugs et vulnérabilités** : SonarQube analyse le code pour détecter les bugs, les vulnérabilités de sécurité et les mauvaises pratiques. L'objectif est de réduire leur nombre au minimum.

## Résultats Attendus
Après l'exécution du workflow, les résultats de l'analyse sont disponibles dans l'interface web de SonarQube. Ces résultats incluent :
- La couverture de code.
- La détection des bugs et vulnérabilités.
- L'indice de qualité du code (qualité globale).

### Accès aux résultats
Les résultats de l'analyse peuvent être consultés en vous rendant sur la page du projet dans SonarQube. Par défaut, SonarQube est accessible via l'URL suivante :  

**URL de SonarQube** : `http://localhost:9000`

Une fois connecté à l'interface de SonarQube :

1. **Connexion à SonarQube** :
   - Ouvre un navigateur et accède à l'URL `http://localhost:9000` (si tu utilises SonarQube en local).
   - Si tu utilises SonarQube sur un serveur distant, remplace `localhost` par l'adresse de ton serveur SonarQube.
   - Connecte-toi avec tes identifiants.

2. **Accéder au tableau de bord du projet** :
   - Après t'être connecté à SonarQube, dans le tableau de bord principal, recherche ou accède à ton projet : **BobAppBackend**.
   - L'URL de ton projet SonarQube sera sous la forme suivante :
     ```
     http://localhost:9000/dashboard?id=BobAppBackend
     ```

3. **Consulter les métriques** :
   - Sur le tableau de bord du projet **BobAppBackend**, tu pourras voir les métriques d'analyse du code :
     - **Couverture de code**.
     - **Bugs et vulnérabilités**.
     - **Code Smells**.
     - **Complexité**.

   Ces informations seront mises à jour après chaque exécution du workflow GitHub Action.

## Recommandations
- **Améliorer la couverture de code** : Si la couverture de code est en dessous du seuil minimal de 80 %, il est recommandé de rajouter des tests supplémentaires pour améliorer la couverture.
- **Corriger les bugs critiques** : Si SonarQube détecte des bugs ou vulnérabilités critiques, il est essentiel de les résoudre pour garantir la stabilité et la sécurité de l'application.


# Workflow GitHub Action : Java CI/CD avec Docker

## Description
Ce workflow CI/CD pour GitHub Actions est utilisé pour :
1. **Construire l'application Java** avec Maven.
2. **Créer une image Docker** du backend Java.
3. **Se connecter à Docker Hub**.
4. **Pousser l'image Docker vers Docker Hub**.
5. **Exécuter un conteneur Docker** à partir de l'image construite.

### Déclenchement
Le workflow est déclenché sur un **push vers la branche `main`**.

## Étapes du workflow

### 1. **Checkout du code**
   - **Action utilisée** : `actions/checkout@v2`
   - **Objectif** : Récupérer le code du repository afin d'exécuter les étapes suivantes.

### 2. **Configuration de JDK 11**
   - **Action utilisée** : `actions/setup-java@v2`
   - **Objectif** : Installer JDK 11 pour la construction de l'application Java.
   - **Distribution** : Utilisation de la distribution `adopt` de JDK.

### 3. **Construction du projet avec Maven**
   - **Commande** : `mvn clean install`
   - **Objectif** : Compiler et construire le projet Java.

### 4. **Création de l'image Docker**
   - **Commande** : `docker build -t elvis1971/bobapp-back .`
   - **Objectif** : Créer une image Docker à partir du Dockerfile dans le répertoire `back`.
   - Le tag `elvis1971/bobapp-back` est utilisé pour nommer l'image Docker.

### 5. **Connexion à Docker Hub**
   - **Commande** : `docker login --username $DOCKER_HUB_USERNAME --password-stdin`
   - **Objectif** : Se connecter à Docker Hub en utilisant les secrets GitHub définis (`DOCKER_HUB_USERNAME` et `DOCKER_HUB_ACCESS_TOKEN`).
   - Ces secrets sont stockés dans GitHub Secrets pour assurer la sécurité.

### 6. **Pousser l'image vers Docker Hub**
   - **Commande** : `docker push elvis1971/bobapp-back`
   - **Objectif** : Pousser l'image Docker créée sur Docker Hub pour la rendre accessible publiquement ou dans ton compte privé.

### 7. **Exécution du conteneur Docker**
   - **Commande** : `docker run -p 8080:8080 --name bobapp-back -d elvis1971/bobapp-back`
   - **Objectif** : Lancer le conteneur Docker en arrière-plan en exposant le port 8080.
   - Le nom du conteneur est `bobapp-back`.

### 8. **Ajout d'un résumé des actions à GitHub**
   - **Commande** : Ajout d'un résumé détaillant la procédure de création du token Docker et son ajout dans GitHub Secrets.
   - **Objectif** : Afficher un résumé dans l'interface GitHub pour guider l'utilisateur sur la création des secrets nécessaires.

## Configuration du Repository Docker Hub et des Secrets GitHub

### 1. **Création du repository sur Docker Hub**
   - Connecte-toi à [Docker Hub](https://hub.docker.com/).
   - Crée un nouveau repository :
     - Dans l'interface de Docker Hub, clique sur **"Create Repository"**.
     - Donne un nom à ton repository, par exemple `bobapp-back`.
     - Choisis si tu veux que ton repository soit public ou privé.
     - Clique sur **"Create"** pour terminer.

### 2. **Création du Token Docker Hub**
   - Accède à [Docker Hub Login](https://login.docker.com).
   - Clique sur ton nom d'utilisateur en haut à droite et sélectionne **"Account Settings"**.
   - Dans l'onglet **"Security"**, sous **Personal Access Tokens**, clique sur **"New Access Token"**.
   - Donne un nom à ton token, par exemple `"GitHub Actions Backend"`.
   - Choisis la durée de validité et les permissions nécessaires (par exemple, "write" pour permettre l'envoi d'images).
   - Clique sur **"Generate"**.
   - Copie ton token, car tu ne pourras plus le voir une fois la fenêtre fermée.

### 3. **Ajouter les Secrets Docker dans GitHub**
   - Accède à ton repository sur GitHub.
   - Clique sur **Settings** (paramètres).
   - Dans la barre latérale, sélectionne **Secrets** puis **New repository secret**.
   - Ajoute un secret appelé `DOCKER_HUB_USERNAME` avec la valeur de ton nom d'utilisateur Docker Hub.
   - Ajoute également un autre secret appelé `DOCKER_HUB_ACCESS_TOKEN` avec le token que tu as créé sur Docker Hub.

### 4. **Vérification de la configuration**
   - Après avoir configuré les secrets et créé le repository Docker Hub, assure-toi que le workflow GitHub Action fonctionne correctement.
   - Vérifie que l'image Docker est bien poussée vers ton repository Docker Hub et que le conteneur s'exécute correctement.

## Résultats Attendus
1. **Image Docker sur Docker Hub** : Après l'exécution du workflow, l'image Docker de ton backend Java sera disponible sur Docker Hub sous le nom `elvis1971/bobapp-back`.
   
2. **Conteneur Docker en exécution** : Le conteneur sera lancé sur le port 8080, accessible via le nom de l'image.

3. **Résumé GitHub** : Un résumé détaillant la procédure de création des secrets Docker sera ajouté à la section **GitHub Actions summary**.

### Remarques
- N'oublie pas de garder tes **secrets Docker Hub** confidentiels.
- Si le repository Docker est privé, assure-toi que tes credentials Docker Hub ont les bonnes permissions.



