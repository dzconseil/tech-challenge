# Dzconseil Software Engineer Challenge - Backend

## Introduction

As a software engineer in **dzconseil** team, you have to provide a reliable **backend** system to clients. Your task here is to implement few endpoints to `list/show/create` **threads**.

## Requirement

1. We value a **clean**, **simple** working solution.
2. Solution must work on Ubuntu (18.04 LTS or higher ).
3. We prefer [Laravel](https://laravel.com/), but the solution can also be written in pure php or one of the following frameworks: [slimframework](https://www.slimframework.com/) or [lumen](https://lumen.laravel.com/).
4. The solution must be production ready.

## Notes

- Source code must be stored in a git repository ( you can send us a link to a [Github](https://github.com/), [Bitbucket](https://bitbucket.com/) or [Gitlab](https://gitlab.com/) repo )
  - For public repos:
    - Repository must avoid containing words like `dzconseil` and `challenge`.
    - Do not copy-paste any part of this file. (task, API documentation, etc.)
    - This is needed to prevent other candidates from finding your solution.
- Your repo should be easy to setup with clear instruction.
- (Optional) Deploy as a public api to your own host.

## Expectations

- This challenge should take around 4 hours to complete.
- Your code should be modular, each module should focus on doing one thing and do it well.
- Avoid over-engineering.
- Use of popular third-party packages is strongly recommended.

## Problem Statement

1. Must be a **RESTful** HTTP API
2. The API must implement 4 endpoints with path, method, request and response body as specified
    - One endpoint to create a new thread [see sample](#create-a-new-thread)
        - To create a thread , the API client must provide a subject and a recipient.
        - The API responds with an object for the newly created thread
    - One endpoint to show a thread [see sample](#show-thread)
    - One endpoint to list all threads [see sample](#list-threads)
    - One endpoint to create a new message [see sample](#create-a-new-message)
        - A message should always belong to a thread.
        - An error response should be sent only if a user tries to create a message for a thread that doesn't belong to him.

3. A Database must be used ( at **dzconseil** we use mostly **MySQL**).
4. All responses should be in json format no matter in success or failure situations.

## Api interface example

### Create a new Thread

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads)**
- Method: `POST`
- URL path: `/api/v1/threads`
- Request body:

  ```json
  {
    "subject": "Team Metting!",
    "recipient": "example@dzconseil.com",
    "message": "hello, there is a meeting tommorw"
  }
  ```

- Response:

  Header: `HTTP 200`
  Body:

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

  or

  Header: `HTTP 422`
  Body:

  ```json
  {
    "message": "The given data was invalid!",
    "errors": [
      ...
    ]
  }
  ```

- Tips:

  **ID** field in reponse should be a **UUID** you can use a this library to handle generating **UUID's** [link to github!](https://github.com/ramsey/uuid).

  if you find this **json** format strange to you, read about json api specs 
  [link to jsonapi.org!](https://jsonapi.org).

**[⬆ back to top](#problem-statement)**

### Show Thread

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads__threadID_)**
- Method: `GET`
- URL path: `/api/v1/threads/:uuid`

- Response:

  Header: `HTTP 200`
  Body:

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

### List Threads

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/get_threads)**
- Method: `GET`
- URL path: `/api/v1/threads`

- Response:

  Header: `HTTP 200`
  Body:

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

### Create a new Message

- **[Check Docs](https://app.swaggerhub.com/apis-docs/dzconseil/challenge/1.0.0#/default/post_threads__threadID_)**
- Method: `POST`
- URL path: `/api/v1/threads/:uuid`
- Request body:

  ```json
  {
    "message": "hello, there is a meeting tommorw",
    "creator": "admin@dzconseil.com"
  }
  ```

- Response:
  Header: `HTTP 200`
  Body:

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
  Body:

  ```json
  {
    "message": "The given data was invalid.",
    "errors": [
        ...
    ]
  }
  ```

**[⬆ back to top](#problem-statement)**

**Questions? Suggestions? We love to hear from you: <techchallenge@dzconseil.com>**
