---
# markdownlint-disable
# vale  off
layout: default
parent: Tutorials
nav_order: 2
# tags used by AI files
description: Add a `user` resource to the service
tags:
    - api
categories: 
    - tutorial
ai_relevance: high
importance: 6
prerequisites: 
    - /before-you-start-a-tutorial
    - /api/user
related_pages: []
examples: []
api_endpoints: 
    - POST /users
version: "v1.0"
last_updated: "2025-09-03"
# vale  on
# markdownlint-enable
---

# Tutorial: Enroll a new user

The To-Do Service is a task management system where users create and manage tasks.  
To use the service, you must first enroll as a user. This tutorial shows you how to enroll
a  
new user by making a **POST** request to the Users endpoint using  
[Postman](https://learning.postman.com/docs/sending-requests/requests).  

## What you'll learn in this tutorial

* The user resource schema and required fields
* How to make a **POST** request to create a new user using Postman
* How to verify that a user was successfully enrolled
* How to troubleshoot common enrollment errors
  
Expect this tutorial to take about 15 minutes to complete.

## About the user resource

The `user` resource describes someone registered in the To-Do Service and includes these properties:

* `firstName`: The user's first name, required
* `lastName`: The user's last name, required
* `email`: The user's email address, required & must be unique
* `id`: The To-Do Service assigns a unique identifier

## Tutorial prerequisites

Complete the [Before you start a tutorial](../before-you-start-a-tutorial.md) topic
on the development system you'll use for the tutorial.

## Tutorial summary steps

After completing the prerequisites, you'll undertake the following steps to complete the tutorial  

1. Start the To-Do Service on your development desktop.
2. Configure your Postman environment.
3. Create a new request in the Postman app.
4. Click **Send** to make the request.
5. Review the response body.

## Enroll a new user using Postman

Enrolling a new user in the service requires you to use the `POST` method
to store the details of a new [`user`](../api/user.md) resource in the service.

### Step 1. Start the To-Do Service

* Open a terminal or command prompt.
* Navigate to your local To-Do Service API directory.

  ```shell
    cd <your-github-workspace>/to-do-service/api
    ```

    Example:

* ```shell
   cd documents/GitHub/GitHubRepos/to-do-service-au25/api
   ```

* Enter the following command:
  
    ```shell
    r -w to-do-db-source.json
    ```

* Verify the To-Do-Service is running. It'll typically run on //localhost:3000.  
  Example expected output:

  ```shell
    \{^_^}/ hi!

  Loading to-do-db-source.json
  Done

  Resources
  http://localhost:3000/users
  http://localhost:3000/tasks

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database
  Watching...
  ```

### Step 2. Configure your postman environment

* Open the Postman app on your desktop.
* Configure [Postman environment](https://learning.postman.com/docs/sending-requests/variables/managing-environments/) to use your local host, /localhost:3000, as the base_url.

### Step 3. Create a new request in the Postman app

* Click **Post** from the left menu.
* Configure the request with these settings:
    * **METHOD**: POST
    * **URL**: `{base_url}/users`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as you'd like.

        ```js
        {
            "lastName": "Jones",
            "firstName": "Jenny",
            "email": "jen.jones@example.com"
        }
        ```

### Step 4. Click **Send** to make the request

### Step 5. Review the response body

Review the response body in the lower panel of Postman. Note that the names should match those used in your **Request body**, and the response should include the new user's `id`. The response should look something like this.

 ```json
{
    "lastName": "Jones",
    "firstName": "Jenny",
    "email": "jen.jones@example.com"
    "id": 5
}
```

### Step 6: Verify the enrollment

To confirm successful user enrollment, retrieve the user by their ID.

* Create a new request in Postman.
* Set the method to [GET](https://learning.postman.com/docs/getting-started/first-steps/sending-the-first-request/).
* Enter the URL: {{base_url}}/users/{id}. Note: as before, use the //localhost:3000 base URL,
* and replace {id} with the ID from the previous response.
* Click **Send**.
You should see the same user information returned, confirming the user exists in the service.

 ```json
{
    "lastName": "Jones",
    "firstName": "Jenny",
    "email": "jen.jones@example.com",
    "id": 5
}
```

## Troubleshooting

| Status Code               | Problem                                        | Solution                                                                                          |
|---------------------------|------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 400 Bad Request           | Invalid JSON format or missing required fields | Verify your JSON syntax is correct and you have included all required fields |
| 409 Conflict              | email address already exists                   | Use a different email address; each user must have a unique email                                 |
| 500 Internal Server Error | Service error                                  | Check that the json-server is running and the database file is accessible                         |

## Next steps

Now you are ready to explore more to-do-service tasks.

### - Perform more tasks  

* Add a [task](add-a-new-task.md) for that user
* Retrieve [all users](<../api/users-get-all-users.md>)
* Retrieve [users by id](<../api/users-get-user-by-id.md>)
  
### - Explore other utilities

Once you're comfortable with this tutorial, you can send the same request using programming code
 instead of Postman.
 Don't worry - the information you need: the URL, the POST method, and the user data stays the same.
 You're just using a different tool to send it.

Here is the cURL command to get you started:

```bash
curl -X POST http://localhost:3000/users \
  -H "Content-Type: application/json" \
  -d '{
    "lastName": "Jones",
    "firstName": "Jenny",
    "email": "jen.jones@example.com"
  }'
```

Here is the expected cURL **GET** response:

```bash
curl http://localhost:3000/users/5

{
  "lastName": "Jones",
  "firstName": "Jenny",
  "email": "jen.jones@example.com",
  "id": 5
}
```
