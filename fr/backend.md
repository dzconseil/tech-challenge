# Dzconseil Software Engineer Challenge - Backend

## Introduction

En tant qu’ingénieur logiciel dans l’équipe **dzconseil**, vous devez fournir un système **fiable** aux utilisateurs. Votre tâche ici est d’implémenter quelques **endpoints** api pour : lister/créer/afficher un courriel

## Exigence

1. Nous valorisons une solution **propre**, **simple** et **efficace**.
2. La solution doit fonctionner sur Ubuntu (18.04 LTS or higher ).
3. Nous préférons [Laravel](https://laravel.com/), mais la solution peut aussi être écrite en php pur ou dans l'un des frameworks suivants: [slimframework](https://www.slimframework.com/) ou [lumen](https://lumen.laravel.com/).
4. La solution doit être prête pour la production.

## Remarques
- Le code source doit être stocké dans un dépôt git (vous pouvez nous envoyer un lien vers un dépôt github.com, bitbucket.com ou gitlab.com)
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
    - Une endpoint pour créer un nouveau courriel [voir example](#créer-un-nouveau-courriel)
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

#### Créer un nouveau Courriel

  - la méthode : `POST`
  - le chemin URL : `/api/v1/threads`
  - le corps de la requête:

    ```json
    {
      "subject": "SUJET_COURRIEL",
      "recipient": "E-MAIL_DESTINATAIRE",
      "message": "CONTENU_MESSAGE"
    }
    ```

  - Réponse:

    Entête: `HTTP 200`

    Le corps de la réponse:
    ```json
    {
      "data": {
        "type": "threads",
        "id": <ID_COURRIEL>,
        "attributes": {
          "subject": <SUJET_COURRIEL>,
          "creator": <CRÉATEUR_COURRIEL>,
          "time": <created_at>,
          "read" : <true|false>,
          "deleted": <true|false>
        }
      }
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

#### Afficher un courriel

  - la méthode: `GET`
  - le chemin URL: `/api/v1/threads/:uuid`

  - Réponse:

    Entête: `HTTP 200`

    le corps de la réponse:
    ```json
    {
      "data": {
        "type": "thread",
        "id": <ID_COURRIEL>,
        "attributes": {
          "subject": <SUJET_COURRIEL>,
          "creator": <CRÉATEUR_COURRIEL>,
          "time": <created_at>,
          "read" : <true|false>,
          "deleted": <true|false>,
          "messages": [
            {
              "id":<ID_MESSAGE>,
              "body": <CONTENU_MESSAGE>,
              "time": <created_at>,
              "creator": <CRÉATEUR_MESSAGE>
            }
            ...
          ]
        }
      }
    }
    ```
**[⬆ back to top](#problem-statement)**

#### lister les Courriels

  - la méthode: `GET`
  - le chemin URL: `/api/v1/threads`

  - Réponse:

    Entête: `HTTP 200`

    le corps de la réponse:
    ```json
    {
      "data": [ 
        {
          "type": "threads",
          "id": <ID_COURRIEL>,
          "attributes": {
            "subject": <SUJET_COURRIEL>,
            "creator": <CRÉATEUR_COURRIEL>,
            "time": <created_at>,
            "read" : <true|false>,
            "deleted": <true|false>
          }
        }
        ...
      ]
    }
    ```
**[⬆ back to top](#problem-statement)**

#### Créer un nouveau Message

  - la méthode: `PUT`
  - le chemin URL: `/api/v1/threads/:uuid`
  - le corps de la requête:
    ```json
    {
      "thread_id": "SUJET_COURRIEL",
      "message": "CONTENU_MESSAGE"
    }
    ```
  - Réponse:

    Entête: `HTTP 200`

    le corps de la réponse:
      ```json
      {
        "data": {
          "type": "messages",
          "id":<ID_MESSAGE>,
          "attributes": {
            "body": <CONTENU_MESSAGE>,
            "time": <created_at>,
            "creator": <CRÉATEUR_MESSAGE>
          }
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
