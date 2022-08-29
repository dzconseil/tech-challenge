# Défis Tech DZConseil - Backend <!-- omit in toc -->

- [Introduction](#introduction)
- [Exigences](#exigences)
- [Remarques](#remarques)
- [Attentes](#attentes)
- [Énonce du problème](#nonc-du-problme)
- [Configuration du projet](#configuration-du-projet)
- [Endpoints](#endpoints)
    - [Afficher toutes les maisons](#afficher-toutes-les-maisons)
    - [Afficher une maison](#afficher-une-maison)
    - [Créer une nouvelle maison](#crer-une-nouvelle-maison)
    - [Mettre à jour une maison](#mettre--jour-une-maison)
    - [Supprimer une maison](#supprimer-une-maison)

## Introduction

En tant qu’ingénieur logiciel dans l'équipe **DZConseil**, vous devez fournir une solution **backend** fiable à nos
clients.
Votre tâche ici est d'implémenter quelques fonctionnalités pour une api rest comme **Airbnb**.

## Exigences

- Nous valorisons une solution **propre**, **simple** et efficace.
- La solution doit être réalisée avec la dernière version de [Laravel](https://laravel.com/)
  et [PHP](https://www.php.net/).
- Bonne compréhension du fonctionnement du git.
- Bonne compréhension des **API REST**.
- Aucun package ne doit être ajouté au code fourni.

## Remarques

- Le code source doit être poussé en tant qu'une branche git dans ce [project](https://github.com/dzconseil/backend-challenge).
- Votre nom de branche devrait suivre cette forme `challenge/nom-prénom`.

## Attentes

- Ce défi devrait durer environ 4 à 5 heures.
- Tous les tests dans votre branche doivent réussir.
- Éviter le over-engineering.
- Toutes les réponses doivent être en format **JSON**.

## Énoncé du problème

![Diagramme UML](../assets/uml.png)

- En suivant ce diagramme, nous souhaitons mettre en place une API que nos utilisateurs peuvent utiliser.
- Cette API restfull devrait nous permettre de [lister](#afficher-toutes-les-maisons), [voir](#afficher-une-maison), [créer](#crer-une-nouvelle-maison), [mettre à jour](#mettre--jour-une-maison) et [supprimer](#supprimer-une-maison) une maison.
- Les methods qui calcule de couts de réservation `calculateCost()` & `calculateDiscount()` devrons être implémentées au niveau du model `Listing`.

## Configuration du projet

Pour obtenir une copie de ce projet sur votre machine, vous devez exécuter la commande suivante :

```bash
git clone git@github.com:dzconseil/backend-challenge.git dzconseil-challenge
```

Vous obtiendrez une copie de ce projet dans un dossier nommé `dzconseil-challenge`

Maintenant, vous devez créer une nouvelle branche pour commencer à travailler, exécutez la commande suivante :

```bash
git checkout -b challenge/nom-prénom challenge
```

Vous remarquerez que nous vous avons fourni le squelette du projet avec presque tout, y compris (`routes`, `models`
, `migration`, `factories`, `controllers`, `requests`, `resources`, `tests`)
tout ce que vous avez à faire est de remplir la logique manquante et d'exécuter les tests.

Tous les tests de ce projet doivent réussir avant que vous poussiez votre code.

## Endpoints

### Afficher toutes les maisons

- **Requête**
    - URI : `/api/listings`
    - Méthode : `GET`

- **Réponse**
    - Statut : `200`
    - Corps :

      ```json
      {
        "data": [
          {
            "id": "28eed9aa-c27d-4217-ab21-ad65ead3a2aa",
            "owner_id": "59f6d752-97cf-414e-a794-42794ac7511a",
            "name": "Warner",
            "slug": "warner",
            "description": "Maecenas ut massa quis augue luctus tincidunt.",
            "adults": 10,
            "children": 2,
            "is_pets_allowed": true,
            "base_price": 95.38,
            "cleaning_fee": 4.33,
            "image_url": null,
            "weekly_discount": 0.13,
            "monthly_discount": 0.23
          },
          {
            "id": "b3a6e269-d0fa-4408-89b1-fe2e48963177",
            "owner_id": "e0b227da-dc6e-402c-8172-9d950ece4707",
            "name": "Burrows White",
            "slug": "burrows-white",
            "description": "Phasellus in felis. Donec semper sapien a libero. Nam dui. ",
            "adults": 9,
            "children": 2,
            "is_pets_allowed": false,
            "base_price": 160.51,
            "cleaning_fee": 31.45,
            "image_url": "storage/1/image.png",
            "weekly_discount": 0.77,
            "monthly_discount": 0.36
          }
        ]
      }
      ```

**[⬆ retour au sommet](#introduction)**

### Afficher une maison

- **Requête**
    - URI : `/api/listings/:uuid`
    - Méthode : `GET`

- **Réponse**
    - Statut : `200`
    - Corps :

      ```json
      {
        "data": {
          "id": "b3a6e269-d0fa-4408-89b1-fe2e48963177",
          "owner_id": "e0b227da-dc6e-402c-8172-9d950ece4707",
          "name": "Burrows White",
          "slug": "burrows-white",
          "description": "Phasellus in felis. Donec semper sapien a libero. Nam dui. ",
          "adults": 9,
          "children": 2,
          "is_pets_allowed": false,
          "base_price": 160.51,
          "cleaning_fee": 31.45,
          "image_url": "storage/1/image.png",
          "weekly_discount": 0.77,
          "monthly_discount": 0.36,
          "special_prices": [
            {
              "id" : "b7b81974-51b7-4989-bd8d-28450c8466d1",
              "date": "2019-10-12",
              "price": 40.51
            },
            {
              "id" : "d3f39186-319a-4099-988c-a713c09d72b8",
              "date": "2019-10-13",
              "price": 80
            }
          ]
        }
      }
      ```

**[⬆ retour au sommet](#introduction)**

### Créer une nouvelle maison

- **Requête**
    - URI : `/api/listings`
    - Méthode : `POST`
    - Corps :

      ```json
      {
        "name": "Black Raven",
        "description": "Morbi porttitor lorem id ligula. Suspendisse ornare consequat lectus. In est risus, auctor sed.",
        "adults": 3,
        "children": 2,
        "is_pets_allowed": 1,
        "base_price": 195.62,
        "cleaning_fee": 95.82,
        "image": <file>,
        "weekly_discount": 0.77,
        "monthly_discount": 0.61
      }
      ```

- **Réponse**
    - Statut : `201`
    - Corps :

      ```json
      {
        "data": {
          "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
          "owner_id": "d701748f-6c54-4b01-90e6-d701748f0822",
          "name": "Black Raven",
          "slug": "black-raven",
          "description": "Morbi porttitor lorem id ligula. Suspendisse ornare consequat lectus. In est risus, auctor sed.",
          "adults": 3,
          "children": 2,
          "is_pets_allowed": true,
          "base_price": 195.62,
          "cleaning_fee": 95.82,
          "image_url": "storage/2/black-raven.jpg",
          "weekly_discount": 0.77,
          "monthly_discount": 0.61
        }
      }
      ```

**[⬆ retour au sommet](#introduction)**

### Mettre à jour une maison

- **Requête**
    - URI : `/api/listings/:uuid`
    - Méthode : `PUT`
    - Corps :

      ```json
      {
        "name": "White Raven",
        "description": "Morbi porttitor lorem id ligula",
        "adults": 3,
        "children": 2,
        "is_pets_allowed": true,
        "base_price": 195.62,
        "cleaning_fee": 95.82,
        "image": null,
        "weekly_discount": 0,
        "monthly_discount": 0.61
      }
      ```

- **Réponse**

    - Statut : `200`
    - Corps :

      ```json
      {
        "data": {
          "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
          "owner_id": "d701748f-6c54-4b01-90e6-d701748f0822",
          "name": "White Raven",
          "slug": "white-raven",
          "description": "Morbi porttitor lorem id ligula. Suspendisse ornare consequat lectus. In est risus, auctor sed.",
          "adults": 3,
          "children": 2,
          "is_pets_allowed": true,
          "base_price": 195.62,
          "cleaning_fee": 95.82,
          "image_url": "storage/2/black-raven.jpg",
          "weekly_discount": 0.77,
          "monthly_discount": 0.61
        }
      }
      ```

**[⬆ retour au sommet](#introduction)**

### Supprimer une maison

- **Requête**
    - URI : `/api/listings/:uuid`
    - Méthode : `DELETE`

- **Réponse**
    - Statut : `200`
    - Corps :

      ```json
      {
        "id": "d290f1ee-6c54-4b01-90e6-d701748f0851"
      }
      ```

**[⬆ retour au sommet](#introduction)**

**Des questions ? Suggestions ? Nous aimons vous répondre : <techchallenge@dzconseil.com>**

