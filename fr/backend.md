# Dzconseil Software Engineer Challenge - Backend

## Introduction

En tant qu’ingénieur logiciel dans l’équipe **dzconseil**, vous devez fournir un système **fiable** aux utilisateurs. Votre tâche ici est d’implémenter quelques **endpoints** api pour : lister/créer/afficher un courriel

## Exigence

1. Nous valorisons une solution **propre**, **simple** et **efficace**.
2. La solution doit fonctionner sur Ubuntu (18.04 LTS or higher ).
3. Nous préférons [Laravel](https://laravel.com/), mais la solution peut aussi être écrite en php pur ou dans l'un des frameworks suivants: [slimframework](https://www.slimframework.com/) ou [lumen](https://lumen.laravel.com/).
4. La solution doit être prête pour la production.

## Remarques

- Le code source doit être stocké dans un dépôt git ( vous pouvez nous envoyer un lien vers un dépôt [Github](https://github.com/), [Bitbucket](https://bitbucket.com/) ou [Gitlab](https://gitlab.com/) )
  - Pour les dépôts publics:
    - La repository doit éviter de contenir des mots tels que `dzconseil` ou `challenge`.
    - Ne copiez-collez aucune partie de ce fichier. (tâche, documentation de l'API, etc.)
    - Cela est nécessaire pour empêcher d'autres candidats de trouver votre solution.
- Votre repo devrait être facile à installer avec des instructions claires.
- (Facultatif) Déployez en tant qu'API publique sur votre propre hôte.

## Expections

- Ce défi devrait durer environ 4 heures.
- Votre code doit être modulaire, chaque module doit se concentrer sur une chose à faire et bien le faire.
- Évitez le `over-engineering`.
- L'utilisation de packages third-party populaires est fortement recommandée.

## Problem Statement

1. Doit être une API HTTP **RESTful**
2. L'API doit implémenter 4 **endpoints** avec le chemin, la méthode, la requête et le corps de la réponse spécifiés
    - Une endpoint pour créer un nouveau courriel [voir example](#creer-un-nouveau-courriel)
        - pour créer un courriel, le client API doit fournir un sujet et un destinataire.
        - L'API répond avec un objet json pour le nouveau courriel créé.
    - Une endpoint pour Afficher un courriel [voir example](#afficher-un-courriel)
    - Une endpoint pour lister tous les courriels [voir example](#lister-les-courriels)
    -Une endpoint pour créer un nouveau message [voir example](#créer-un-nouveau-message)
        - Un message doit toujours appartenir à un courriel.
        - Une réponse d'erreur ne doit être envoyée que si un utilisateur tente de créer un message pour un courriel qui ne lui appartient pas.

3. Une base de données doit être utilisée ( chez **dzconseil**, nous utilisons principalement **MySQL**).
4. Toutes les réponses doivent être au format JSON, peu importe les situations de réussite ou d’échec.

## Exemple d'interface Api

### Créer un nouveau Courriel

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads)**
- la méthode : `POST`
- le chemin URL : `/api/v1/threads`
- le corps de la requête:
  
  ```json
  {
    "subject": "Team Metting!",
    "recipient": "example@dzconseil.com",
    "message": "hello, there is a meeting tommorw"
  }
  ```

- Réponse:

  Entête: `HTTP 200`

  Le corps de la réponse:

  ```json
  {
    "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "subject": "Team meeting!",
    "time": "2016-08-29T09:12:33.001Z",
    "read": true,
    "deleted": true,
    "creator": {
      "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
      "email": "admin@dzconseil.com",
      "username": "administrator"
    },
    "messages": [
      {
        "id": "d290f1ee-6c52-4b02-90e6-d701748f9854",
        "body": "Lorem ipsum dolor sit amet, consectetur adipiscing.",
        "time": "2016-08-29T09:12:33.001Z",
        "creator": {
          "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
          "email": "admin@dzconseil.com",
          "username": "administrator"
        }
      }
    ]
  }
  ```

  ou

  Entête: `HTTP 422`

  Le corps de la réponse:

  ```json
  {
    "message": "The given data was invalid.",
    "errors": [
        ...
    ]
  }
  ```

- Conseils:

  Le champ **ID** dans la reponse devrait être un **UUID**. Vous pouvez utiliser cette bibliothèque pour gérer la génération de **UUID's** [lien vers github!](https://github.com/ramsey/uuid).

  si vous trouvez ce format **json** étrange pour vous, lisez les spécifications des api json [lien vers jsonapi.org!](https://jsonapi.org).

**[⬆ retour au sommet](#problem-statement)**

### Afficher un courriel

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads__threadID_)**
- la méthode: `GET`
- le chemin URL: `/api/v1/threads/:uuid`

- Réponse:

  Entête: `HTTP 200`

  le corps de la réponse:

  ```json  
  {
    "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "subject": "meeting!",
    "time": "2016-08-29T09:12:33.001Z",
    "read": true,
    "deleted": true,
    "creator": {
      "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
      "email": "example@dzconseil.com",
      "username": "administrator"
    },
    "messages": [
      {
        "id": "d290f1ee-6c52-4b02-90e6-d701748f9854",
        "body": "Lorem ipsum dolor sit amet, consectetur.",
        "time": "2016-08-29T09:12:33.001Z",
        "creator": {
          "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
          "email": "example@dzconseil.com",
          "username": "administrator"
        }
      }
    ]
  }
  ```

**[⬆ back to top](#problem-statement)**

### lister les Courriels

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads)**
- la méthode: `GET`
- le chemin URL: `/api/v1/threads`

- Réponse:

  Entête: `HTTP 200`

  le corps de la réponse:

  ```json
  [
    {
      "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
      "subject": "meeting!",
      "time": "2016-08-29T09:12:33.001Z",
      "read": true,
      "deleted": true,
      "creator": {
        "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
        "email": "example@dzconseil.com",
        "username": "administrator"
      }
    },
    {
      "id": "d290f1ee-6c54-4251-1111-d701748f0164",
      "subject": "Second meeting!",
      "time": "2016-08-29T09:12:33.001Z",
      "read": false,
      "deleted": false,
      "creator": {
        "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
        "email": "example@dzconseil.com",
        "username": "administrator"
      }
    }
  ]
  ```

**[⬆ back to top](#problem-statement)**

### Créer un nouveau Message

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads__threadID_)**
- la méthode: `PUT`
- le chemin URL: `/api/v1/threads/:uuid`
- le corps de la requête:

  ```json
  {
    "message": "hello, there is a meeting tommorw",
    "creator": "admin@dzconseil.com"
  }
  ```

- Réponse:

  Entête: `HTTP 200`

  le corps de la réponse:

  ```json
  {
    "id": "d290f1ee-6c52-4b02-90e6-d701748f9854",
    "body": "hello, there is a meeting tommrow",
    "time": "2016-08-29T09:12:33.001Z",
    "creator": {
      "id": "d290f1ee-6c54-4b01-90b6-d701748f0851",
      "email": "example@dzconseil.com",
      "username": "administrator"
    }
  }
  ```

  or

  Header: `HTTP 422`
  le corps de la réponse:

  ```json
  {
    "message": "The given data was invalid.",
    "errors": [
        ...
    ]
  }
  ```

**[⬆ back to top](#problem-statement)**

**Des questions? Suggestions? Nous aimons répondre: <techchallenge@dzconseil.com>**
