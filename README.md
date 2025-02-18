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






