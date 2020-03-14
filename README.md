[![Coverage Status](https://coveralls.io/repos/github/Deityhub/hb_backend/badge.svg?branch=master)](https://coveralls.io/github/Deityhub/hb_backend?branch=master) [![Build Status](https://travis-ci.org/Deityhub/hb_backend.svg?branch=master)](https://travis-ci.org/Deityhub/hb_backend)

# HackerBay Nodejs API task

A simple stateless microservice in Nodejs to implement authentication, json patching and image thumbnail generation.

## Getting Started

Follow the guidelines below to set up a copy of this project locally on your machine for development and testing purposes.

### First steps

To have a local copy of this project, you can:

- Clone the repository by using git clone command, or the download zip alternative provided on github

```
git clone https://github.com/Deityhub/hb_backend.git
```

To run the cloned version locally, `cd` into the root folder and run

```
npm install
```

or

```
yarn
```

to install required dependencies.

- Create a `.env` file which will be used for storing jwt secret for token generation and verification; with the following content.

```
JWT_SECRET="<secret>"
```

> The secret variable can be any text of your choice

### Testing

To test the application on your local machine, run

```
npm test
```

or

```
yarn test
```

A code coverage report will be seen on your console.

## API Endpoints

### Starting the Server

Before you start testing the endpoints with postman, you need to start the server with:

```
npm start
```

or

```
yarn start
```

### Swagger Documentation

- Request Method: GET
- URL: [https://localhost:3000](http://localhost:3000)

> Once your server is running, the url above is where the documentation on how to use the api endpoints resides, you can also run your test there without using postman

### Login

- Request Method: POST
- URL: [http://localhost:3000/api/v1/login](http://localhost:3000/api/v1/login)

Request body should contain username and password; the API will return a token for the user which will be used for future requests to the server.

- Sample Request: `{ "username": "any name", "password": "any password" }`
- Sample Response: `{ "status": "Success", "data": { "token": "\<token\>" } }`

> Any username/password combination is accepted, since this it just a mock authentication service

### JSON Patch

- Request Method: PATCH
- URL: [http://localhost:3000/api/v1/json](http://localhost:3000/api/v1/json)

> This endpoint accepts two parameters (document and patch) which are JSON objects.

- Sample Request: `{ "document": { "baz": "qux", "foo": "bar" }, "patch": [ { "op": "replace", "path": "/baz", "value": "eke" } ] }`
- Sample Response: `{ "success": true, "data": { "baz": "eke", "foo": "bar" } }`

> The **jwt token** required for authentication can be passed in the request headers [Authorization: Bearer \<token\>], request body [ { req.body.token: \<token\> } ] or request query [ ?token=\<token\> ]

### Thumbnail Generation

- Request Method: GET
- URL: [http://localhost:3000/api/v1/thumbnail?url=imageurl](http://localhost:3000/api/v1/thumbnail?url=imageurl)

This endpoint accepts an image url, generates a 50x50 thumbnail image and returns it to the user.

> The **jwt token** required for authentication can be passed in the request headers [Authorization: Bearer \<token\>], request body [ { req.body.token: \<token\> } ] or request query [ ?token=\<token\> ]

## Docker

This project was dockerised and hosted on [docker hub](https://hub.docker.com/repository/docker/deityhub/hb_backend). Use the following docker command

```
docker run -p 127.0.0.1:3000:3000 --env JWT_SECRET=anyrandomstuff deityhub/hb_backend
```

to run it on your machine.

## Author

**Ojini Chizoba Jude** [github](https://github.com/deityhub) [linkedin](https://www.linkedin.com/in/jude-ojini-5873a3159/)
