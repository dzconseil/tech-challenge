# dzconseil Software Engineer Challenge - Frontend <!-- omit in toc -->

- [Introduction](#introduction)
- [Requirement](#requirement)
- [Notes](#notes)
- [Expectations](#expectations)
- [Problem Statement](#problem-statement)
  - [Interface](#interface)
- [API interface](#api-interface)
  - [Obtenir des informations sur le listing](#obtenir-des-informations-sur-le-listing)
  - [Calculer le coût de la réservation](#calculer-le-co%c3%bbt-de-la-r%c3%a9servation)
  - [Confirmer la réservation](#confirmer-la-r%c3%a9servation)

## Introduction

En tant qu’ingénieur logiciel dans l’équipe **dzconseil**, vous devez fournir une application **frontend** fiable aux clients.
Votre tâche ici est de mettre en place une page de paiement pour une petite api rest comme **Airbnb**.

## Requirement

1. Nous valorisons une solution **propre**, **simple** et efficace.
2. La solution doit fonctionner sur tous les navigateurs modernes (sauf IE).
3. La solution doit être écrite en [React](https://reactjs.org/).
4. La solution doit être prête pour la production.
5. Bonne compréhension du fonctionnement de **GIT**.
6. Bonne compréhension des **API REST** et **Clients HTTP**.

## Notes

- Le code source doit être inséré en tant que branche git dans le repository de projet fourni. ( pour ce défi nous avons utilisé une repository [Gitlab](https://gitlab.com/dzconseil/frontend-challenge) ) et [Create React App Starter](https://github.com/facebook/create-react-app)
- Votre nom de branche devrait suivre ce schéma `challenge/lastname-firstname`.
- (Facultatif) Déployez en tant qu'API publique sur votre propre hôte..

## Expectations

- Ce défi devrait durer environ **4** à **6** heures.
- Votre code doit être modulaire, chaque module doit se concentrer sur une chose à faire et bien le faire.
- Évitez l'ingénierie excessive.
- Méfiez-vous des bibliothèques **Third-party**. (N'incluez pas une bibliothèque de 300 Ko pour une seul fonction)

## Problem Statement

Le Web évolue rapidement et la plupart des entreprises transfèrent leurs projets d'applications **jQuery** à des applications SPA **React**.
chez **dzconseil**, nous travaillons beaucoup avec des clients de type **nous voulons migrer**.

En tant qu’ingénieur frontend **Votre mission, si vous choisissez de l’accepter** 💻 consiste à créer une page de paiement,
avec au plus 4 composants pour un site **comme Airbnb**, où les hôtes peuvent lister leurs maisons à louer.
et les clients plus tard peuvent visiter notre site Web et réserver ces maisons pour une durée spécifique appelée **Durée du voyage**. [Voir wireframe](#interface)

### Interface

_Pour référence seulement, vous pouvez être créatif avec les fonctionnalités de design et UI / UX._

![Interface Review](../assets/review_tab.png)
![Interface Confirmation](../assets/confirmation_tab.png)

Suite à cette image wireframe, nous souhaitons implémenter cette page de paiement comme suit:

1. **Doit** être une application à une seul page (SPA).
2. **Doit** implémenter 3 composants comme spécifié dans la wireframe.

   - Un composant pour la barre de navigation.
     - Ce composant **doit** fournir un élément de menu d'onglet pour basculer entre les onglets "révision" et "confirmation".
   - Un composant pour afficher les informations de liste et les informations de réservation.
     - Ce composant **doit** fournir un div pour afficher toutes les informations relatives à la réservation "durée, invités".
     - Ce composant **doit** fournir un élément textarea permettant à l'utilisateur de saisir un message d'accueil pour l'hôte.
     - Ce composant **doit** fournir un bouton **Continuer** lorsque vous cliquez dessus, vous devriez aller à l'onglet suivant "confirmation".
     - Ce composant **doit** fournir un bouton **Confirmer** lorsque vous cliquez dessus, il devrait envoyer le payload au backend.
   - Un composant pour calculer le coût de la réservation.
     - Ce composant **doit** fournir un sélecteur de date pour sélectionner les dates d'arrivée et de départ avec range.
     - Ce composant **doit** fournir un élément de compteur simple pour incrémenter ou décrémenter le nombre d'invités.
     - Ce composant **doit** fournir un élément de compteur simple pour incrémenter ou décrémenter le nombre d'enfants.
     - Ce composant **doit** fournir un Toggle-Switch pour laisser les utilisateurs décider s'ils incluent l'animal ou non.
     - Ce composant **doit** fournir un div pour afficher le coût de la réservation lorsque l'utilisateur modifie l'une des entrées ci-dessus.

**[⬆ retour au sommet](#introduction)**

## API interface

### Obtenir des informations sur le listing

- Méthode: `GET`
- Chemin de l'URL: `/api/listings/:uuid`
- Réponse:
  Entête: `HTTP 200`
  Corps:

  ```json
  {
    "id": "28eed9aa-c27d-4217-ab21-ad65ead3a2aa",
    "owner_id": "59f6d752-97cf-414e-a794-42794ac7511a",
    "name": "Warner",
    "slug": "revolutionize-warner",
    "description": "Maecenas ut massa quis augue luctus tincidunt.",
    "adults": 10,
    "children": 2,
    "is_pets_allowed": true,
    "base_price": 95.38,
    "cleaning_fee": 4.33,
    "image_url": "http://dummyimage.com/241x240.jpg/ff4444/ffffff",
    "weekly_discount": 0.13,
    "monthly_discount": 0.23,
    "special_prices": [
      {
        "date": "2019-10-12",
        "base_price": 40.51
      },
      {
        "date": "2019-10-13",
        "base_price": 80
      }
    ]
  }
  ```

**[⬆ retour au sommet](#introduction)**

### Calculer le coût de la réservation

- Méthode: `POST`
- Chemin de l'URL: `/api/listings/:uuid/reservation-cost`

- Corps de la requette:

  ```json
  {
    "checkin": "2019-12-06",
    "checkout": "2019-12-10",
    "adults": 2,
    "children": 1,
    "pets": false
  }
  ```

- Réponse:
  Entête: `HTTP 200`
  Corps:

  ```json
  {
    "nights_count": 4,
    "nights_cost": 95.82,
    "discount": 13.82,
    "cleaning_fee": 3.82,
    "total": 112.95
  }
  ```

### Confirmer la réservation

- Méthode: `POST`
- Chemin de l'URL: `/api/listings/:uuid/confirm-reservation`

- Corps de la requette:

  ```json
  {
    "checkin": "2019-12-06",
    "checkout": "2019-12-10",
    "adults": 2,
    "children": 1,
    "pets": false,
    "message": "Hello Host!"
  }
  ```

- Réponse:
  Entête: `HTTP 200`
  Corps:

  ```json
  {
    "message": "success! thanks for your reservation"
  }
  ```

**[⬆ retour au sommet](#introduction)**

**Des questions? Suggestions? Nous aimons répondre: <techchallenge@dzconseil.com>**
