# homework-13

## Server

The server starts requiring the modules necessary to run the application:
* express
* session
* internal config/passport: module used for authentication
* models: where we are handling our database connection and where the database inputs are defined.

After requiring modules, we set up the port number. In most of the cases, it's 8080. If no port is specified in the .env, the 8080 is utilized.

The next step is to Create the Express app and configure the middleware needed for authentication. Here it shows that the app uses a static hosting called public.

After that, the session middleware is set up:

Session keeps users logged in, popular known as cookies. 

"Cookies allow you to store a user's information inside a file on their browser. The browser then sends that info back on every request, allowing your application to identify the user and customize their experience. Which is objectively way better than asking for a username and password on every request."

The next piece of code is related to the routes—the server import the Html and API routes to the app.

And finally, the last piece of code is a promise that established the app has to run Sequelize, check and drop or create the table in the database before running anything else through the Port.

## Routes

### API Routes

This is the file that establishes the routes for the apis.

The apis routes saves and provides json format information that will be viewed the client (in case of get), and uses the other file to save information (post). It's also autheticating the information and giving back a response.

The server starts requiring two modules:
* internal config/passport: module used for authentication
* models: where we are handling our database connection and where the database inputs are defined.

The module exports a collection of routes. Based on the user request, it sends back the user information authenticated by the passport module.

#### app.post("/api/login")
Route for signing up a user. The user's password is automatically hashed and stored securely thanks to how we configured our Sequelize User Model. If the user is created successfully, proceed to log the user in, otherwise send back an error.

####  app.post("/api/signup")
Route for signing up a user. The user's password is automatically hashed and stored securely thanks to how we configured our Sequelize User Model. If the user is created successfully, proceed to log the user in, otherwise send back an error.

####  app.get("/logout")
Route for logging user out. When user click on log out anchior text, there is an href in the html file that drives the user to the page /Logout, which doesn not exists, but user ios redirected to the main page due to this route.

####  app.get("/api/user_data")
Route for getting some data about our user to be used client side. If the user is not logged in, it sends back an empty object, otherwise it sends back the user's email and id.

### HTML Routes

This file directs the user to member or login page if the user is authenticated or not by the middleware.

#### app.get("/")
If the user already has an account it sends them to the members page, otherwise the user stays in the main.

#### app.get("/login")
 If the user already has an account it redirects them to the members page, otherwise it stays in the login page.

#### app.get("/members")
This route establishes the members page route whner the user is already authenticated.

## Models

### User

Users.js uses sequelize to create the structure of MySql tables. In this case it's creating the table with user information, containing email information with:

 ```
 email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
      validate: {
        isEmail: true
      }
```

And the password table:    

```
password: {
      type: DataTypes.STRING,
      allowNull: false
    }
```

### Index

Index is importing a number of moduldes to be used in models files.

Then, it has a condition that states if the environment has connection information for sequelize, it will that infomration, otherwise it will use what's specified in the config.

The fs is importing all js files expect itself.


### Config

#### Cofig.JSON

It specifies information to be used to authenticate on MySql.


#### Is Autheticated

It's am idware to tracj if the user is logged in.

#### Passport

File contains a function that have conditional statements tom cehck if the username and password matches with the information in the database.


### Public

### Login

HTML / JS containing the structure of the website for logging in.

In the JS first function, it grabs information written on the form in the HTML file. It used val (value) method for it and  trimms it.

Im the second JS function, the password and usernmane information is being sent to the api rout using the post method.

### Members

It gets the information of the user data and and shows it on the html page using JQuery.

### Members

HTML / JS containing the structure of the website for signing up.

In the JS first function, it grabs information written on the form in the HTML file. It used val (value) method for it and  trimms it.

Next, if the sign up function runs successfully, it redirects the user to the members page, otherwise, it shows an error.
