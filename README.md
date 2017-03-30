# JWT_JavaScript

This is a (very) small project to play with using JSON Web Tokens (JWT) as a lightweight authentication sysem. This project is written in JavaScript and uses Node.  The first thing to do is ensure you have Node and npm installed.
Type `node -v` to see if Node is installed; if it is, then the version number will be displayed. If it's not installed then install it using Homebrew or some
other means. I personally like using Homebrew and (assuming you have brew installed) all you need to do to install node is type `brew install node` from the 
bash command line. 

The next step is to install the packages we will need to run our application so once again we turn to our friendly bash shell:  `npm install express body-parser morgan mongoose jsonwebtoken --save` where


1. express is the popular Node framework
2.  mongoose is how we interact with our MongoDB database
3.  morgan will log requests to the console so we can see what is happening
4.  body-parser will let us get parameters from our POST requests
5.  jsonwebtoken is how we create and verify our JSON Web Tokens


Use nodemon to have your server restart on file changes. Install nodemon using `sudo npm install -g nodemon`. Then start your server with `nodemon server.js`
or `node server.js`. 

This app has several routes:

1.  /api: Our api root; simply returns a message to the browser
2.  /setup: Simple API to create a user in our Mongo database
3.  /users:  Returns all users
4.  /authenticate: Accepts a username and password and generates a JWT if the username/password are valid

We have chosen to restrict access to the /setup and /users APIs by implementing a "use" method. The important thing to remember is that ordering is important! The /setup and /users APIs are defined AFTER the use method.

An instance of a router is defined in server.js:  `var apiRoutes = express.Router();` The post and get methods or our API endpoints are defined using the apiRoutes variable. We instruct the node server to apply routes to the application with a prefix of /api by adding the following line:  `app.use('/api', apiRoutes); 

Retrieving users or creating a new user requires a token. The token can be generated using the /authenticate endpoint which can then be passed in one of two ways:

1.  Browser:  http://localhost:8080/api/setup?token=MySuperLongToken
2.  Postman:  Adding a header of "x-access-token" with the value being the token
