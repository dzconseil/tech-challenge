# Dzconseil Software Engineer Challenge - Frontend

## Introduction

En tant qu’ingénieur logiciel dans l’équipe **dzconseil**, vous devez fournir une application **frontend** fiable aux clients. Votre tâche ici est de développer une boîte de réception pour
`lister/créer/afficher` des **courriels**.

## Requirement

1. Nous valorisons une solution **propre**, **simple** et **efficace**.
2. La solution doit fonctionner sur tous les navigateurs modernes (IE exclu).
3. Nous préférons [React](https://reactjs.org/), mais la solution peut également être écrite en javascript pur ou dans l’une des bibliothèques suivantes: [vuejs](https://vuejs.org/) ou [preactjs](https://preactjs.com/) mais n'hésitez pas à utiliser d'autres technologies si vous préférez.
4. La solution doit être prête pour la production.

## Remarques

- Le code source doit être stocké dans un dépôt git ( vous pouvez nous envoyer un lien vers un dépôt [Github](https://github.com/), [Bitbucket](https://bitbucket.com/) ou [Gitlab](https://gitlab.com/) )
  - Pour les dépôts publics:
    - La repository doit éviter de contenir des mots tels que `dzconseil` ou `challenge`.
    - Ne copiez-collez aucune partie de ce fichier. (tâche, documentation de l'API, etc.)
    - Cela est nécessaire pour empêcher d'autres candidats de trouver votre solution.
- Votre repo devrait être facile à installer avec des instructions claires.
- (Facultatif) Déployez en tant que site public sur votre propre hôte.
  
## Expections

- Ce défi devrait durer environ 4 heures.
- Votre code doit être modulaire, chaque module doit se concentrer sur une chose à faire et bien le faire.
- Évitez le `over-engineering`.
- Méfiez-vous de l'utilisation des bibliothèques third-party. (N'incluez pas une bibliothèque de 300 Ko seulement pour une fonction d'assistance)

## Déclaration du problème

Nous basculons la plupart de nos projets de jQuery à React. Nous visons des composants réutilisables et une base de code maintenable lors de l'expansion, votre tâche aujourd'hui en tant qu'ingénieur **front-end** consiste à créer une boîte de réception d'une seule page `SPA`.

1. Doit être une application à page unique (SPA) [voir exemple](#interface)
2. Doit implémenter 4 composants comme spécifié dans la structure wireframe.
    - Un composant pour créer un nouveau courriel
        - Pour créer un courriel, l'interface doit fournir les entrées sujet et destinataire. ainsi qu'une zone de texte de message de courriel.
    - Un composant pour montrer un courriel.
    - Un composant pour lister tous les threads.
    - Un composant pour créer un nouveau message.
        - Un message doit toujours appartenir à un courriel.

## Interface

*Pour référence uniquement, vous pouvez être créatif avec le design et les fonctionnalités UI/UX.*

![Interface](../assets/inbox.jpg)

## Mock Api interface

### Create a new Thread

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads)**
- Méthode: `POST`
- le chemin URL: `https://virtserver.swaggerhub.com/dzconseil/challenge/1.0.0/threads/`
- le corps de la requête:

  ```json
  {
    "subject": "Team Metting!",
    "recipient": "example@dzconseil.com",
    "message": "hello, there is a meeting tommorw"
  }
  ```

**[⬆ back to top](#problem-statement)**

### Show Thread

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads__threadID_)**
- Méthode: `GET`
- le chemin URL: `https://virtserver.swaggerhub.com/dzconseil/challenge/1.0.0/threads/{uuid}`

**[⬆ back to top](#problem-statement)**

### List Threads

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads)**
- Méthode: `GET`
- le chemin URL: `https://virtserver.swaggerhub.com/dzconseil/challenge/1.0.0/threads/`

**[⬆ back to top](#problem-statement)**

### Create a new Message

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads__threadID_)**
- Méthode: `POST`
- le chemin URL: `https://virtserver.swaggerhub.com/dzconseil/challenge/1.0.0/threads/{uuid}`
- le corps de la requête:

  ```json
  {
    "message": "hello, there is a meeting tommorw",
    "creator": "admin@dzconseil.com"
  }
  ```

**[⬆ back to top](#problem-statement)**

**Questions? Suggestions? We love to hear from you: <techchallenge@dzconseil.com>**