# Dzconseil Software Engineer Challenge - Backend

## Introduction

As a software engineer in **dzconseil** team, you have to provide a reliable **backend** system to clients. Your task here is to implement few endpoints to 
list/show/create **threads**. 

## Requirement

1. We value a **clean**, **simple** working solution.
2. Solution must work on Ubuntu (18.04 LTS or higher ).
3. We prefer [Laravel](https://laravel.com/), but the solution can also be written in pure php or one of the following frameworks: [slimframework](https://www.slimframework.com/) or [lumen](https://lumen.laravel.com/).
4. The solution must be production ready.

## Notes
- Source code must be stored in a git repository (you can send us a link to a github.com or bitbucket.com or gitlab.com repo)
  - For public repos:
	  - Repository must avoid containing words like `dzconseil` and `challenge`.
	  - Do not copy-paste any part of this file. (task, API documentation, etc.)
	  - This is needed to prevent other candidates from finding your solution.
- Your repo should be easy to setup with clear instruction.
- (Optional) Deploy as a public api to your own host.

## Expection
- This challange should take around 4 hours to complete.
- Your code should be modular, each module should focus on doing one thing and do it well.
- Avoid over-engineering.
- Use of popular third-party packages is strongly recommended.

## Problem Statement

1. Must be a **RESTful** HTTP API
2. The API must implement 4 endpoints with path, method, request and response body as specified
    - One endpoint to create a new thread [see sample](#create-a-new-thread)
        - To create a thread , the API client must provide a subject and a recipent 
        - The API responds an object for the newly created thread the thread UUID 
    - One endpoint to show a thread [see sample](#show-thread)
    - One endpoint to list all threads [see sample](#list-threads)
    - One endpoint to create a new message [see sample](#create-a-new-message)
        - A message should always belong to a thread.
        - An error response should be sent only if a user tries to create a message for a thread that doesn't belong to him.

3. A Database must be used ( at **dzconseil** we use mostly **MySQL**).
4. All responses should be in json format no matter in success or failure situations.


## Api interface example

#### Create a new Thread

  - Method: `POST`
  - URL path: `/api/v1/threads`
  - Request body:

    ```json
    {
      "subject": "THREAD_SUBJECT",
      "recipient": "RECIPIENT_EMAIL",
      "message": "THREAD_MESSAGE"
    }
    ```

  - Response:

    Header: `HTTP 200`
    Body:
    ```json
    {
      "data": {
        "type": "threads",
        "id": <thread_id>,
        "attributes": {
          "subject": <thread_subject>,
          "creator": <thread_creator>,
          "time": <created_at>,
          "read" : <true|false>,
          "deleted": <true|false>
        }
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

  - Tips:

    **ID** field in reponse should be a **UUID** you can use a this library to handle generating **UUID's** [link to github!](https://github.com/ramsey/uuid).

    if you find this **json** format strange to you, read about json api specs 
    [link to jsonapi.org!](https://jsonapi.org).

**[⬆ back to top](#problem-statement)**

#### Show Thread

  - Method: `GET`
  - URL path: `/api/v1/threads/:uuid`

  - Response:

    Header: `HTTP 200`
    Body:
    ```json
    {
      "data": {
        "type": "thread",
        "id": <thread_id>,
        "attributes": {
          "subject": <thread_subject>,
          "creator": <thread_creator>,
          "time": <created_at>,
          "read" : <true|false>,
          "deleted": <true|false>,
          "messages": [
            {
              "id":<message_id>,
              "body": <message_body>,
              "time": <created_at>,
              "creator": <message_creator>
            }
            ...
          ]
        }
      }
    }
    ```
**[⬆ back to top](#problem-statement)**

#### List Threads

  - Method: `GET`
  - URL path: `/api/v1/threads`

  - Response:

    Header: `HTTP 200`
    Body:
    ```json
    {
      "data": [ 
        {
          "type": "threads",
          "id": <thread_id>,
          "attributes": {
            "subject": <thread_subject>,
            "creator": <thread_creator>,
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
#### Create a new Message

  - Method: `PUT`
  - URL path: `/api/v1/threads/:uuid`
  - Request body:
    ```json
    {
      "thread_id": "THREAD_ID",
      "message": "THREAD_MESSAGE"
    }
    ```
  - Response:
    Header: `HTTP 200`
    Body:
      ```json
      {
        "data": {
          "type": "messages",
          "id": <message_id>,
          "attributes": {
              "body": <message_body>,
              "time": <created_at>,
              "creator": <message_creator>
          }
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
