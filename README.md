# JWT_JavaScript

This is a (very) small project to play with using JSON Web Tokens (JWT) as a lightweight authentication sysem. This project is written in JavaScript and uses node. To start the local server type `node server.js1` or `nodemon server.js`. We are using morgan which allows console logging for helping the development process.

This app has several routes:

1.  /api: Our api root; simply returns a message to the browser
2.  /setup: Simple API to create a user in our Mongo database
3.  /users:  Returns all users
4.  /authenticate: Accepts a username and password and generates a JWT if the username/password are valid

We have chosen to restrict access to the /setup and /users APIs by implementing a "use" method. The important thing to remember is that ordering is important! The /setup and /users APIs are defined AFTER the use method.

An instance of a router is defined in server.js:  `var apiRoutes = express.Router();` The post and get methods or our API endpoints are defined using the apiRoutes variable. We instruct the node server to apply routes to the application with a prefix of /api by adding the following line:  `app.use('/api', apiRoutes); 

Retrieving users or creating a new user requires a token. The token can be generated using the /authenticate endpoint which can then be passed in one of two ways:

Browser:  http://localhost:8080/api/setup?token=MySuperLongToken
Postman:  Adding a header of "x-access-token" with the value being the token
