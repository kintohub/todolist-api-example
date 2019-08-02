# Todo List (example app) – Backend API

*Backend API for the Todo List example app.*

> 👋 Welcome! This example app is part of [this article in the docs for KintoHub][doc] to show how you can build cloud native apps in seconds. Head over there to read the guided steps to use this project.

## Project structure

This [Node.js] based backend API app has a dependency on a [MongoDB] database. It's meant to be used with the [Frontend app].

The app uses the [hapi framework] for handling API routes. It exposes a REST API for persisting Todo items, since the frontend app is based on [TodoMVC] and relies on this backend for storing the todos.

The REST API has [apiDoc] annotations, refer to those for usage in [`app/index.js`](./app/index.js).

For the purpose of easy debugging, the app logs to the console all API calls and related output.

## Configuration

The only thing you must specify is the environment variable that has a connection string to point to the MongoDB database.

### Environment variables
1. `MONGODB_CONNECTION_STRING` **(required)**  – MongoDB connection string, e.g. `mongodb://<user_name>:<password>@localhost:27017/<db_name>?authSource=<auth_db_name>`
2. `SERVER_HOST` (optional) – host where the server is bound to. Defaults to `0.0.0.0` (all available network interfaces) if undefined.
3. `SERVER_PORT` (optional) – port where the server listens on. Defaults to `8000` if undefined.

## Usage

### Developling locally

You'll need to have a MongoDB database. You could [install MongoDB], or if you have [Docker Desktop] installed, you can spin up a temporary one quickly.

#### MongoDB with Docker

1. Once Docker Desktop is installed, you can open create a new MongoDB container:  
   ```sh
   docker run --name todolist-mongo -d -p 27017:27017 mongo:4.0
   ```
   It will run (detached) a MongoDB 4.0 container `todolist-mongo` and exposes the default MongoDB port on your localhost.
2. To confirm whether the container is running, run:
   ```sh
   docker ps
   ```
3. Once you're done, you can quit Docker Desktop or run:
   ```sh
   docker stop todolist-mongo
   ```
4. When you get going again, start up Docker Desktop and run:
   ```sh
   docker start todolist-mongo
   ```

#### Configure environment

To make it easier to specify environment variables for local development, the app uses the [dotenv] node module to load environment variables from file. You can refer to the example file [`.env.example`](./.env.example), and copy it to a new `.env` file in the root folder. It's ignored in git.

If you use the MongoDB with Docker method, set your `.env` file like this:

```:.env
MONGODB_CONNECTION_STRING=mongodb://localhost:27017/todolist
```

#### Run the development server

1. Install dependencies:  
   ```sh
   npm install
   ```
2. Start in debugging mode:  
   ```sh
   npm start
   ```

### Serve in production

For running MongoDB in production, check out the [related KintoHub docs article][doc] how you can quickly get a cluster going with [Helm charts], so it has automatic failover built-in. (you shouldn't run just a single MongoDB instance in a container for production workloads)

#### Configure environment

Ensure the environment variable `MONGODB_CONNECTION_STRING` is set, and point to your production grade MongoDB cluster.

You may also want to set the correct `SERVER_PORT` for exposing the service.

#### Run the production server

1. Build the code for a production release:  
   ```sh
   npm run build
   ```
2. Serve the built application:  
   ```sh
   npm run serve
   ```

---

> 🚀 **Deploying on KintoHub**  
>
> Thank you for checking out this example app. KintoHub makes it super easy to build, deploy, manage and operate your cloud native apps, like this one.
>
> Find out more at www.kintohub.com.

  [doc]: https://docs.kintohub.com
  [Frontend app]: https://github.com/kintohub/todolist-api-example
  [Node.js]: https://nodejs.org
  [MongoDB]: https://www.mongodb.com
  [install MongoDB]: https://docs.mongodb.com/manual/installation/#tutorial-installation
  [Docker Desktop]: https://www.docker.com/products/docker-desktop
  [Helm charts]: https://helm.sh
  [hapi framework]: https://hapijs.com
  [apiDoc]: http://apidocjs.com
  [TodoMVC]: http://todomvc.com
  [dotenv]: https://www.npmjs.com/package/dotenv