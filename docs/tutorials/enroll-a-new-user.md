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
last_updated: "2025-24-10"
# vale  on
# markdownlint-enable
---

# Tutorial: Enroll a new user

The To-Do Service is a task management system where users create and manage tasks. To use the service, you must first enroll as a user. This tutorial shows you how to enroll a new user by making a **POST** request to the Users endpoint. 

* [Command line tool: cURL](<https://curl.se/docs/tutorial.html>)
* [GUI tool: Postman](<https://learning.postman.com/docs/sending-requests/requests/>)

## What you'll learn in this tutorial

* The user resource schema and required fields
* How to make a **POST** request to create a new user using [Postman](https://learning.postman.com/docs/getting-started/overview/)
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

Complete the [Before you start a tutorial](../before-you-start-a-tutorial.md) topic on the development system you'll use for the tutorial.

## Tutorial summary steps

After completing the prerequisites, you'll undertake the following steps to complete the tutorial  
  **Step 1** Start the To-Do Service on your development desktop.  
**Step 3**

## Enroll a new user using Postman

Enrolling a new user in the service requires that you use the `POST` method to store the details of a new [`user`](../api/user.md) resource in the service.

### Step 1. Start the To-Do Service

* Open a terminal or command prompt
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

* Verify the To-Do-Service is running. It'll typically run on <http://localhost:3000>.  
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

### Step 2. Configure your Postman evironment
- Open the Postman app on your desktop
- Configure [postman environment](<https://learning.postman.com/docs/sending-requests/variables/managing-environments/>) to use your local host, /localhost:3000, as the base_url.
    
### Step 3. In the Postman app, create a new request with these values
* Click New in the top-left corner
* Select HTTP Request
* Configure the request with these settings
    * **METHOD**: POST
    * **URL**: `{{base_url}}/users`
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

4. In the Postman app, choose **Send** to make the request.
5. Review the response body, in the lower panel, which should look something like this. Note that the names should be the same as you used in your **Request body** and the response should include the new user's `id`.

    ```js
    {
        "lastName": "Jones",
        "firstName": "Jenny",
        "email": "jen.jones@example.com",
        "id": 5
    }
    ```
### Step 4: Verify the enrollment
To confirm the user was enrolled successfully, retrieve the user by their ID.
* Create a new request in Postman
* Set the method to GET
* Enter the URL: {{base_url}}/users/{id} (replace {id} with the ID from the previous response)
* Click Send
You should see the same user information returned, confirming the user exists in the service.

## Troubleshooting 
| Status Code              | Problem                                      | Solution                                                                                          |
|--------------------------|----------------------------------------------|---------------------------------------------------------------------------------------------------|
| 400 Bad Request          | Invalid JSON format or missing required fields | Verify your JSON syntax and ensure all required fields (firstName, lastName, email) are included |
| 409 Conflict             | Email address already exists                 | Use a different email address; each user must have a unique email                                 |
| 500 Internal Server Error | Service error                               | Check that the json-server is running and the database file is accessible                         |

After doing this tutorial in Postman, you might like to repeat it in
your favorite programming language. To do this, adapt the values from
the tutorial to the properties and arguments that the language uses to
make REST API calls.

## Next Steps ##
Now that you've enrolled a user, you can:
* Add a [task](add-a-new-task.md) for that user
* Retrieve [all users](<../api/users-get-all-users.md>)
* Retrieve [users by id](<../api/users-get-user-by-id.md>)