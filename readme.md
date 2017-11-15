# Express Convention Router

This module provides a simple way to define convention-based routes in a Node.js application. I originally got the idea from how ASP.NET MVC (as well as other MVC frameworks)and KrakenJS
s  (http://krakenjs.com) routes work. These frameworks automate the process of creating routes (which I've always liked) so I decided to do something similar with `express-convention-router`.

`express-convention-router` creates routes automatically by parsing a folder structure such as the one below. This allows you to easily create new routes without having to write any code to define the individual routes.

```
-controllers
    -customers
        -customers.controller.js
    -api
        -cart
            -cart.controller.js
    -index.controller.js
```

The previous folder structure would cause `express-convention-router` to create following routes:

```
/customers
/api/cart
/
```

Each folder contains a "controller" file that defines the functionality to run for the given route. For example, if you want a root route you'd add a file into the root `controllers` folder (`index.controller.js` for example). If you want an `api/cart` route you'd create that folder structure under the `controllers` folder (see the folder example above) and add a "controller" file such as `cart.controller.js` into the `api/cart` folder.

To get started perform the following steps:

1. Install the `express-convention-router` package locally (note that the package hasn't been published yet - coming soon!!)

    `npm install express-convention-router --save`

1. Create a `controllers` folder at the root of your Express project.

1. Add an `index.controller.js` file into the folder (you can name the file whatever you'd like). Put the following code into the file:

    ```JavaScript

    module.exports = function (router) {

        router.get('/', function (req, res) {

            res.end('Hello from the router');

        });
    };

    ```

1. To create a `/customers` route, create a subfolder under `controllers` named `customers`.

1. Add a `customers.controller.js` file into the `customers` folder (you can name the file anything you'd like):

    ```JavaScript

    module.exports = function (router) {

        router.get('/', function (req, res) {

            res.end('Hello from the customers route');

        });
    };

    ```

1. Once the routing folder structure is created, add the following code into your express server code (index.js, server.js, etc.) to load the routes automatically based on the
folder structure in the "controllers" folder when the Express server starts:

    ```JavaScript

    const router = require('express-convention-router');

    ...

    router.load(app);

    ```

    The `app` object represents the Express instance.

    If you want to define the folder where your routes are, log created routes to the console, 
    and even change the root folder where the routes folder lives you can do the following:

    ```JavaScript

    router.load(app, {
        //Defaults to "./controllers" but showing for example
        routesDirectory: './controllers', 

        //Defined since "controllers" isn't at the root of the project
        //and is in "examples" for this particular example
        rootDirectory: './examples/',
        
        //Do you want the created routes to be shown in the console?
        logRoutes: true, 
    });

    ```


1. Try out the included sample app by running the following commands:
* `npm install`
* `npm start`