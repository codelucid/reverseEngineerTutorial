# Reverse Engineering Tutorial

## Inside the Config Folder

- config.json

    Following the MVC (model, view, controller) software pattern design, which divides the related program logic into three interconnected elements, the config.json file is created when the Sequelize dependency is installed.  With regards to MVC, this file correlates with the model and controller.  Sequelize is a promise based ORM for Node.js. ORM stands for "object relational mapping." First, Sequelize CLI needs to be installed, on the global level, by issuing "npm install -g sequelize-cli." This is considered a "sequelize application," similar to "bootstrap's" front-end, html, setup; however, this is for the back-end, server setup.  To dynamically create the config folder and config.json file, the "sequelize init:config" command is issued in the terminal.  The config.json file contains three different entries, "development," "test," and "production."  The "development" entry is for working on your applications locally, while the "production" entry is for when you have your application deployed on Heroku. 

    With regards to MVC(model, view, controller), this file represents the *model* and *controller.*  A good analogy is the process of making Thanksgiving Dinner.  The model is the refrigerator full of the necessary ingredients to make the meal.  The controller is the recipe(s) needed to actually construct the meal. The view represents the plates and silverware on the table. 

- passport.js

    The passport.js file requires the Passport Node Module, which is saved as the variable "passport."  The Passport Module is Express-compatible authentication middleware for Node.js. Passport's sole purpose is to authenticate requests, which it does through en extensible set of plugins, known as *strategies.*  Passport does not mount routes or assume any particular database schema, which maximizes flexibility and allows application-level decisions to be made by the developer. The API is simple: you provide Passport a request to authenticate, and Passport provides hooks for controlling what occurs when authentication succeeds or fails.  In short, Passport provides a comprehensive set of strategies to support authentication using a username and password.  This file is also requiring the "Passport-local" module, which is a plug-in to the Passport module, that allows *local* authentication to be unobtrusively integrated into the application.  This plug-in is being saved as the variable, "LocalStrategy," per line 2.  *Local authentication* is logging in with a username and password.  Line 7 is calling the passport variable, applying the method "use," and creating a new instance to the LocalStrategy variable.  Line 10 is dictating the use of an email as the login method, noted by a payload being created, with a key called, "usernameField."  The function, on lines 12-32, checks with the database, via Sequelize's *findOne* method, to match the supplied email and password.  The *.then*, on line 18, is using Sequelize's built in "promises" for the return of requested information, and proceeds to run through *if and else if statements* qualifying the email and password.  If the email and password are found in the database, or are valid, the *dbUser* is returned via Passport's *done* method.  Line 40, passport.serializeUser, is setting up the user's id as a cookie in the user's browser.  More specifically, the user's id property is saved to the session as *req.session.passport.user.*  Passport with use the id property to obtain the user object from the database.  Line 44, passport.deserializeUser, is obtaining the user's id from the previously setup cookie.  This allows the user to open multiple tabs and still be "signed-in," avoiding the need to go through the authentication process, again.  Line 49 is exporting the passport variable, which includes the authentication details. 

    Passport.js file is part of the *model* and *controller* of the MVC(model, view, controller).
    
    The *api-routes.js* file requires the passport module, from the *passport.js* file, and it will be saved as a variable, called "passport."

- middleware folder

### Inside the Middleware Folder

- isAuthenticated.js

    Middleware is software that is in the "middle" of an operating system and the applications working on it.  It permits communication and data management for distributed applications by operating as a hidden translation layer.  The *isAuthenticated.js* file is working with the database and the current session to make sure the user is "signed-in" and is allowed to proceed to restricted sites.  This middleware is working in tandem with the Passport and Passport-local modules, along with the database to verify the user's credentials, which allows the user to open multiple session tabs, in the browser, and still be authenticated.  In the *isAuthenticated.js* file, the *if statement* asks "if the request.user is truthy, return the *next function.* If faslsy, return the response.redirect method, with a parameter URL route that directs the user to the index, or *signup.html,*" according to the *html-routes.js* file.

    *isAuthenticated.js* file is part of the *model* and *controller* of the MVC(model, view, controller).

***

## Inside the Models Folder

- index.js

    The origination of the *index.js* file is very similar to the *config.json* file, found in the config folder.  Since Sequelize is an "out of the box" ORM that handles SQL statements for you, this file is part of the model and controller, of the MVC, just like the *config.json* file.  After the global Sequelize CLI command has been issued in the terminal, the "sequelize init: models" command can be issued, which dynamically creates the models folder and *index.js* file.  Sequelize allows you to create as many models files as you want, or need. It reads all of those files, and executes them all.  This process creates all your necessary models, and exports them all as one big object, all at once.  The *index.js* file works "as-is."

- user.js

    As described above, within the *index.js* description, Sequelize allows you to create as many model files as needed for the application.  This file, *user.js,* is a javascript object, or model, that has been created for Sequelize to access and read for setting up the mySQL table information, for the database. Specifically, this file is requiring "bcryptjs," which is a node module from Node Package Module(NPM).  It is a password hashing module, written in pure JavaScript, that securely stores passwords in databases. Bcryptjs includes a "salt" feature, which when added to a password, produces a secure unique hashed password.  Hashing algorithms turn data into a fixed-length "fingerprint" that cannot be reversed.  That is what is happening on line 28 in this file. By default, the number of "salt rounds" is 10, which is large enough to deter brute force attacks, and small enough to minimize the necessary time needed to create the hashed password. The salt is stored in the same string that contains the hash.  Salts only prevent rainbow table attacks. Lines 22 and 23 are comparing passwords, making sure the password is valid and comparing it to what is already stored in the database.  Line 5 is creating a "User" class, or model.  Lines 4 - 20 are creating the "User" table, along with generating the email and password columns.  Two flags are being used at the "top level" for the email column, the allowNull flag and the unique flag.  These are saying "there must be an email" and "it has to be unique."  A validation is being used, which checks for the correct email format.  The password column also has a flag, allowNull, which is communicating there must be a password.  Each column is expecting a string data type.  
    
    The *api-routes.js* file will require the entire models folder(index.js and user.js), and it will be saved into the variable called "db."
    The *passport.js* file will require the entire models folder(index.js and user.js), and it will be saved into the variable called "db."

    With regards to MVC(model, view, controller), this folder represents the *model.*  Per the Thanksgiving analogy, the model is the refrigerator full of the necessary ingredients to make the meal.  These are the "ingredients" to make the table in the database.

***

> The Node Modules Folder 

> Packages are dropped into the Node Modules folder. When installing locally, you can require the *package name* to load its main module.  The necessary modules, for an application, are referenced in the package.json file, as dependencies.   

***

## Inside the Public Folder
- login.html

    The *login.html* file contains the html syntax for displaying the "login page" of the application.  The setup of the syntax begins with the styling references linked between the head tags, towards the top of the file. The references for this html are linked with *Bootstrap* -the most popular CSS framework for developing responsive and mobile-first websites, and *CSS stylesheet*.  Working down the html document, between the body tags, we see how the page will be "contained" by a Bootstrap container.  A row, with a column, will detail the display information in a very orgainized manner.  The different elements are labeled by classes and ids, which can be referenced by JavaScript files and CSS files.  This html will contain different "form groups" for the user to submit their login information- their email address and password.  The button tag represents a simple "submit" button.  There is a link, inside a paragraph tag, connecting to the *signup.html* page.  More specifically, the */* href link is directing the link to the *html-routes.js* file, and the required *path* module is redirecting the user to the *signup.html* file.  JavaScript is found at the bottom of the html document, noted by a *script tag,* which links in the necessary JavaScript file. This file uses the *login.js* file.  This html is also using a JavaScript Library, called JQuery. 

    With regards to MVC(model, view, controller), this file represents the *view.*

- members.html

    The *members.html* file contains the html syntax for displaying the "membership page" of the application.  This file contains similar syntax as the *login.html,* with Bootstrap and CSS styling referenced between head tags, towards the top of the document.  The body tag contains a Bootstrap navigation bar, that will display at the top of the actual page, when viewed.  This navbar contains a "logout" href link, that will log the user out of the database.  More specifically, the */logout* href redirects to the *api-routes.js* file, which uses the *app.get* Express method, a *request.logout* method, followed by a *response.redirect* method to redirect the user to the *signup.html* page, or file.   This document includes a Bootstrap container, with a row and column, that will display a "Welcome *member name*," once the user has been authenticated.  JavaScript if found at the bottom of the html document, noted by a *script tag,* which links the necessary JavaScript file and JavaScript Libraries being used.  The document is linking to a js file, called *members.js,* and to a library called JQuery, via the script tags.

    With regards to MVC(model, view, controller), this file represents the *view.*

- signup.html

    The *signup.html* file contains the html syntax for displaying the "sign-up page" fo the application.  This file could also be called the *index.html* or the starting point of the application, as noted by the */* URL href reference path, in the login.html document, and by the */* in the html-routes.js's Express' *app.get* parameter.  The layout of this html document is very similar to the login.html document, but with a slight difference.  This document contains an "error display" div tag, which will display an alert message, if the user can't be authenticated.  More specifically, the alert banner will display if the user has already been created and the incorrect password is given.  Also, the alert banner will display if the user email is given, along with the *correct* password, because this is technically the "sign-up" page; hence, the user can't be created a second time.  There is a paragraph tag, with a */login* href link, which will redirect to the *login.html* file.  More specifically, this href link redirects to the *html-routes.js* file, which uses the *app.get* Express method, the *response.redirect* method, the *response.sendFile* method, and the *path* module to redirect towards the *login.html* page, or file.  The document is linking to a js file, called *signup.js,* and to a library called JQuery, via the script tags.

    With regards to MVC(model, view, controller), this file represents the *view.*

- js folder
- stylesheets folder

### Inside the JS Folder

- login.js

    The *login.js* file begins with the *$(document).ready(function(),* which coordinates  the JavaScript, inside the function, to be available after the DOM(document object model) has loaded.  The variables *loginForm, emailInput, and passwordInput* are using JQuery to reference the appropriate id fields for the respective forms and input areas.  The *preventDefault* method tells the user agent, the computer program representing a person, that if the event does not get explicitly handled, its default action should not be taken as it normally would be.  The *loginForm* function captures the user's inputs, for their email and password, validates the inputs as being present, trims the white spaces, to form a succinct submission, and creates a new payload that is saved as the variable *userData.*  The email and password properties are then qualified by an If statement, and if it is falsey, will return and stop the function from progressing further.  If, truthy, the function calls on the loginUser function, and passes these properties along as arguments, or parameters.  The *loginUser function* posts the email and password payload to the */api/login* route, associated with the *api-routes.js* file, which uses the *passport* module to authenticate the submitted information.  Through the use of *promises* the function continues with the *.then function,* if the user is authenticated, and updates the DOM's window.location by replacing the current document, from the session's history, with the *members.html.*  This is incordination with the *html-routes.js* file.  Finally, the *.catch* allows the programmer to create a block of code, in this case a function that will console.log an error, if an error occurs in the *.try block,* which, in this case, is the *loginUser function.* 

    With regards to MVC(model, view, controller), this file represents the *view* and *controller.*

- members.js

    The *members.js* file also uses the *document.ready(function(),* which coordinates the JavaScript, inside the function, to be available after the DOM(document object model) has loaded.  JQuery is using the *.get* method to request data from the server, with an HTTP GET request, and the */api/user_data* is referenced in the *api-routes.js* file.  From the *api-routes.js* file, Express is being used, along with the *.get* method, to request the data from the server.  The *if statement* asks if the *request.user* is falsy, and if that request is truthy, and empty json is sent as the response.  Otherwise, a json payload is sent back, as the response, containing the user's email and database id.  Using *promises,* the *.then function,* on the *members.js* file, displays the returned data as the apporpriate email, from the database, in the *members.html* file, according to the *member-name class,* assigned to the element in the html.

    With regards to MVC(model, view, controller), this file represents the *view* and *controller.*

- signup.js

    The *signup.js* file also utilizes the *document.ready(function(),* which coordinates the JavaScript, inside the function, to be available after the DOM(document object model) has loaded.  JQuery is used to reference the appropriate class and id names, that correspond to the appropriate elements, in the *signup.html* file, and these references are saved as variables.  The user will enter in their email and password, which is checked for an actual value, and trimmed to leave off any white space remaining in the input field.  This payload will be saved as the *userData* variable.  The *preventDefault* method tells the user agent, the computer program representing a person, that if the event does not get explicitly handled, its default action should not be taken as it normally would be.  The *userData* variable is passed down to a qualifying *if statement,* which checks the *userData's* email and password properties.  If the email and password properties are "truly not acceptable," a return is issued and the progression stops; otherwise, the progression continues and the *signUpUser* function is called, which is inside the scope of the original *signUpForm* "submit button" function, so the email and password properties are easily passed into the *signUpUser* function.  Once the *signUpUser* function is called, the email and password properties are passed into it, as parameters, that the function uses to conduct an HTTP POST method, which references the */api/signup* URL route, or parameter, that is located in the *api-routes.js* file.  In the *api-routes.js* file, Express issues the HTTP POST request to the database.  The *Sequelize create method* uses the specified payload to be passed into the database.  The *promise* setup is used, with a *.then function* to take the response and redirect it to the */api/login* Express HTTP POST method route, which authenticates the email and password, via the *passport* module. The 307 means to temporarily redirect(HTTP status code; look elsewhere on that request only), so the code is temporarily redirecting the response to be authenticated. A *.catch* code block is used to catch the response if the authentication status fails.  The 401 HTTP status code is an "unauthorized client error status response code." The request has not been applied because it lacks valid authentication credentials for the target resource.  If the request is valid, the *.then function,* back in the *signUpUser* function, in the *signup.js* file, replaces the current resource with the resource directed from the */members* URL parameter, that is referenced in the *html-routes.js* file.  There, Express is used with a HTTP GET method, along with the *isAuthenticated.js* middleware, to officially display the *members.html* file.  Back on the *signup.js* file, if the promise fails, or if the authentication fails, the *.catch code block* calls another function, called *handleLoginErr* which initiates the error response and displays a Bootstrap alert message in the *signup.html* file.  The alert will be displayed at the appropriate element, per the id and class references.  The 500 HTTP status code indicates the server encountered an unexpected condition that prevented it from fulfilling the request.
    Lines 20 and 21 are the initial *emailInput* and *passwordInput* variables, setup as an empty sting, waiting for the user's input values. 

    With regards to MVC(model, view, controller), this file represents the *view* and *controller.*

### Inside the Stylesheets Folder

- style.css

    Overall, the *style.css* file controls the "styling" of your page.  CSS stands for *cascading style sheets,* with an emphasis placed on "style"-page layouts, colors, and fonts.  CSS is independent of HTML and can be used with any XML-based markup language.  There are three types of CSS: In a separate file (external), at the top of a web page document (internal), and right next to the text if decorates (inline).  This *style.css* file is creating a "buffer" at the top of the page, via the styling command *margin-top: 50px.*  This is to insure the visibility of the signup form and the login form, in combination with the nav bar, at the top of the page. 

    With regards to MVC(model, view, controller), this file represents the *view.*

***

## Inside the Routes Folder

- api-routes.js

    The *api-routes.js* file is requiring the entire models folder, which was created when Sequelize was installed, and saving it in a variable, called *db.*  This variable represents the interaction with the database, like the table creation, via Sequelize.  The *passport.js* file is also being required, which was configured to use Sequelize, the Passport module, and the Passport-local module.  This combination works at creating the information for the database, while handling the interactions with the database.  Passport controls the user authentication information.  This file contains a function, with an Express *app* parameter being passed in, that is equal to *module.exports.*  *Module.exports,* or *exports,* is a special object which is included in every JavaScript file in the Node.js application, by default.  Specifically, *module* is a plain JavaScript object with an *exports* property.  *Exports* is a plain JavaScript variable that happens to be set to *module.exports*.  *Module.exports* is an object that the current module returns when it is "required" in another program, or module.  Inside this function, the first Express HTTP POST route is for logging into the database, via the */api/login* URL parameter.  The user credentials are authenticated by passport's local strategy, which was articulated in the *passport.js* file.  The */api/login* URL parameter is also being referenced in the *login.js* file, which creates the payload, based on the approved Passport authentication, and sends them to the */members* URL route, which is displayed by the *html-routes.js* file.  Similarly, the function contains an Express HTTP POST route for the signup process, but this incorporates the *db* and *User* class, or model, from the *user.js* file.  A payload is created, via the Sequelize method of "create," and is associated with the */api/signup* URL parameter, which is referenced in the *signup.js* file.  If the sign-up process is approved, the window is replaced by the *members.html.*  If the sign-up process fails, the failure is communicated back, via the use of promises, and the user is redirected to the */api/login* URL parameter, or route.   The 307 means to temporarily redirect(HTTP status code; look elsewhere on that request only), so the code is temporarily redirecting the response to be authenticated. A *.catch* code block is used to catch the response if the authentication status fails.  The 401 HTTP status code is an "unauthorized client error status response code."  When the user wants to logout, the Express HTTP GET request is used, along with the */logout* URL parameter.  The request is made with the logout method, and the response is to redirect the user to the index.html, or the *signup.html* file, per the */* URL parameter, which is displayed by the *html-routes.js* file.  The final Express HTTP GET request is retrieving the user's email and id to be sent to the *members.js* file, which will connect with the *members.html* file, where it will be displayed on the appropriate elements, via their "class" identification of "member-name."  

    The *api-routes.js* file's module.exports is being imported by the *server.js* file. 

    With regards to MVC(model, view, controller), this file represents the *controller.*

- html-routes.js

    The *html-routes.js* file is requiring the *path* module, that will allow the use of relative routes to connect with the necessary HTML files.  The *path* module is being saved in a variable, called "path."  The file is also requiring the *isAuthenticated.js* file, which is the middleware used to check if a user has been logged in.  If the user hasn't logged in, they will be redirected to the *signup.html* file.  This is being incorporated in the third Express HTTP GET request, when the user is redirected to the */members* URL parameter.  If they are authenticated the *members.html* file will display.  The *path* module helps to find the correct file directory path to display the HTML file.  The first Express HTTP GET request is for the index.html, or the *signup.html,* per the */* URL parameter route.  If the user is authenticated, they will be funneled to the */members* URL parameter route, but if not, they will be shown the *signup.html* file.  The same schematic applies with the second Express HTTP GET request, but for the */login* URL parameter.  If the user has been authenticated, they will be directed to the *members.html,* per the */members* URL parameter, but if not, they will be directed to the *login.html* file.  These three Express requests are exported in the *module.export* object.

    The *html-routes.js* file's module.exports is being imported by the *server.js* file.

    With regards to MVC(model, view, controller), this file represents the *view.*

***

> package.json

> All npm packages contain a file, usually in the project root, called *package.json*  This file holds various metadata relevant to the project.  The file is used to give information to npm that allows it to identify the project, and to handle the project's dependencies.  The dependencies for this application are *bcryptjs,* *express,* *express-session,* *mysql2,* *passport,* *passport-local,* and *sequelize.*

> package-lock.json

> The *package-lock.json* file is automatically generated for any operations where npm modifies either the node_modules tree, or *package.json.*  It describes the exact tree that was generated, such that subsequent installs are able to generate identical trees, regardless of intermediate dependency updates.

***

- server.js file

    The *server.js* file is requiring *Express module,* *Express-session module,* the *passport.js* file, the entire models folder setup by Sequelize, the *html-routes.js* file, and the *api-routes.js* file.  The *Express module* is saved as the variable "express." The *Express-session module* is saved as the variable "session." The *passport.js* file is saved as the variable passport, and includes the configurations in the original file.  The *Server.js* file setups the PORT for connection and sets up the Sequelize models folder, as variable "db."  *Express.urlencoded* and *Express.json* are needed for POST and PUT requests, becasue these requests are sending data(in the form of some data object) to the server and you are asking the server to accept, or store, that data(object), which is enclosed in the body of that request.  Express provides you with middleware to deal with the (incoming) data (object) in the body of the request.  *Express.json()* is a method inbuilt in express to recognize the incoming Request Object as a *JSON Object.* This method is called as middleware in your application using the code: app.use(express.json());  *Express.urlencoded()* is a method inbuilt in express to recognize the incoming Request Object as *strings* or *arrays.* This method is called as middleware in your application using the code: app.use(express.urlencoded());  *Express.static* is middleware designed to access static asset directories.  In this case, it is accessing the entire "public" folder for the *js,* *css,* and *html* files.  *Passport* uses sessions(idea of tracking a user from one request to another), so *Express-session* is middlesware that is setup to coincide with *Passport's* setup. Session data is not saved in the cookie itself, just the session ID. Session data is stored server-side.  Passport will maintain persistent login sessions. In order for persistent sessions to work, the authenticated user must be serialized to the session, and deserialized when subsequent requests are made, as coded in the *passport.js* file.  *Passport.initialize()* is middleware that initializes *Passport* for *Express'* use.  *Passport.session()* acts as middleware to alter the req object and change the 'user' value that is currently the session id (from the client cookie) into the true deserialized user object.  This combination allows the user to open mulitple browser tabs, without the need to reauthenticate.  Line 26 is using Sequelize to sync the database and to setup the connection on the specified PORT, in a listening state. 

***

- .gitignore file

    File used by Github, that ignores the specified files.  The entire *node modules* folder is included in this file.  This file is checked in at the root of your repository.  

***

- readme.md file

    File created upon the creation of a new repository.  The file is an effective way to describe the overall application. 

***

- Alternatives:

    Could design the HTML pages to revolve around the Handlebars template engine, which would simplify the HTML layout
