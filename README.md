# Overview

This guide explains how to initialize this Full Stack application locally with a Shopify Hydrogen frontend + NodeJS microservice.

# Requirements

- Docker 24.0.2 or docker-compose 2.19.1
- NodeJS 20.11.0

# Getting started

## Environment Variables

You don't need to worry about environment variables. Both projects employ `dotenv` package. So, they were set up through `.env` and `.env.test` files in each application (client & server). Therefore, you don't have to add new ones to the services.

## Types

Both applications (client & server) have a stage `postinstall` which will execute after you install the packages. It will generate the types that you need to work with typescript. Nevertheless, some of them were committed.

## Run Mongo service

You must run a MongoDB service on your local machine. Here, it will run it through Docker. You must run the command below

```bash
docker-compose -f docker-compose-mongo.yml up -d
```

The filename has a different filename standard because it clarifies that the manifest constains just the Mongo service. Therefore, you must add the flag `-f` to `docker-compose` command to point the filename out.

## NodeJS microservice - server end

Firstly, this project looks like a mono-repo where you can look at the `/server` and `/client`. You will begin initializing first the NodeJS microservice. Therefore, you must move to `/server` folder

```bash
cd server
```

Here, you could employ a Node Version Manager (NVM) to select the NodeJS version declared from `.nvmrc` file through:

```bash
nvm use
```

Don't worry, if you don't have Node Package Manager installed, you could set up the NodeJS version declared `.nvmrc` with your favorite method from the terminal manually. The version of NodeJS employed here was `20.11.0`

Next, you must install the packages. You can use `yarn` or `npm`

```bash
yarn install
```

or

```bash
npm install
```

Finally, you can run the server from any commands shown below

```bash
yarn dev
```

or

```bash
npm run dev
```

You will observe the next log from the terminal. Now, your server will be running by default `http://localhost:4000/`

```bash
🚀  Server is running!
📭  Query at http://localhost:4000/
```

## Shopify Hydrogen - client end

Now, you will have to move to `/client` folder. First, you must open a new tab terminal and copy the commands below.

```bash
cd ../
cd client
```

Make sure that your last location had been from the `/server` folder. Otherwise, you don't need to come back. Only move to the client folder `cd client` or to the root folder where the project was cloned.

Once here, you must choose the NodeJS version proper. Here, it worked with `20.11.0`. It was the same employed for the server end. Nevertheless, you will have the command for Node Version Manager (nvm) package below

```bash
nvm use
```

Then, you will have to install the packages here as well. You can employ `yarn` or `npm`

```bash
yarn install
```

or

```bash
npm install
```

Finally, you can run the client end using any of the commands below

```bash
yarn dev
```

or

```bash
npm run dev
```

You look at the next log. This will be a good signal which declares that client is running in `http://localhost:3000/`

```bash
$ shopify hydrogen dev --codegen

Environment variables injected into MiniOxygen:
SESSION_SECRET        from local .env
PUBLIC_STORE_DOMAIN   from local .env
FAVORITES_API_TOKEN   from local .env
➜  Local:   http://localhost:3000/
➜  Network: use --host to expose
➜  press h + enter to show help

success
View Hydrogen app: http://localhost:3000/ [1]
```

## How to access to Favorites Products List Page

You can access to favorites list page by typing in the browser address bar `http://localhost:3000/favorites`. Also, you can access directly from the website, there is a navigation button to go to the Favorites List page directly.

## How to run the unit tests

You can run the test from both projects with any of the commands bellow

```bash
yarn test
```
or

```bash
npm run test
```

## Technologies employed

### GraphQL

It employs Apollo Server and Graphql technologies to build the interface of communication between the client and server. It has whopping powerful tools to reduce the latency of the application, cache of the requests, and save the number of requests through tools such as aliases or connections. Besides, tools like Graphql Codegen and Mock Schemas give you some advatanges. Some of them, for instance, keep up your types based on the schema. Another one, provide to frontend application an initial and predictable data which you can start to work quickly.

### Express

This employs Express through the Apollo Sserver framework. Under this layer, functions as `startStandaloneServer` use Apollo Server 4's Express integration. Therefore, it will allow you to build and launch an API faster with low complexity of configuration. Apart from that, if you need to add some processing before or after, you would have to switch to employ `expressMiddleware`. This was not the use case.

### Mongoose

It employs MongoDB, which is a NoSQL database for storing the product. Actually, you could use both type of database (SQL and NoSQL). However, we decided due to the simplicity and configuration of the model.

### Linting

It employs ESLint to organize the code properly

### Jest

It employs Jest for testing the backend side. This has enough tools to allow you to test your application, you don't need to install too many external packages to test the main methods and functions of your application.

### Docker

It employs docker-compose and docker to deploy a Mongo service. It will avoid installing third-party packages directly on your local machine and set up them. From Docker, you can manage an image that will host your service from a simple manifest file.

### Vitest

It employs `@testing-library/react`, `@remix-run/testing`, and `vitest` as main tools to create unit test cases in some Remix components. Vitest employs Jest assertions and it can run natively ESM and NodeJS modules without needing transformers. Furthermore, Shopify Hydrogen project works with ESM instead of CommonJS. It causes that some testing frameworks as Jest requests complex configuration files and low probability of success for running the unit tests properly
