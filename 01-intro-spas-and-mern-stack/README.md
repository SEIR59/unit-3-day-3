<img src="https://i.imgur.com/IKHxRMa.png">

# Intro to Single-Page Applications (SPAs) and the MERN-Stack

## Learning Objectives

|Students Will Be Able To:|
|---|
| Explain the difference between a SPA and a traditional multi-page web application |
| Identify the three development concepts that make SPAs possible |
| Structure a MERN-Stack Project |

## Road Map

- Intro to SPAs
- Intro to the MERN-Stack
- This Unit's Reference App: **SEI CAFE**
- Building a MERN-Stack's Infrastructure
- Let's Begin Building **mern-infrastructure**
- Configure React for Full-stack Development
- Further Study

## Intro to SPAs

### Review - What is a Single-Page App?

We've mentioned them previously - **what are they?**

<img src="https://i.imgur.com/m01TbLF.png">

In a traditional multi-page web app, if we click a link, submit data via a form, or type in the address bar and press [enter], **what happens?**

In a SPA, we still want to be able to access different functionality by clicking links, submitting data to the server, etc., however, we want the UI to update without triggering a full-page refresh.

There are three development concepts that make SPAs possible:

1. AJAX Communications between client and server
2. Client-Side Routing
3. Client-Side Rendering

### Concept 1: Client/Server Communication via AJAX

As you've seen, the `fetch` API, as well as utilities such as Axios & jQuery's AJAX methods can be used to send HTTP requests to a server using JavaScript instead of using forms and links in the page.

With AJAX, the server responds to an HTTP request with an HTTP response that usually contains a JSON payload in the response body.

Because the request was sent via code, and the response handled via code, the browser has no reason to reload the page!

### Concept 2: Client-Side Routing

When the users have interacted by clicking links and submitting forms in the traditional multi-page web apps we've built thus far, the server has responded with a new HTML document that the browser proceeds to replace the current page with.

In a SPA, we still need a way to switch to different "pages" of functionality (see diagram above) - but without replacing the entire HTML document that's currently loaded in the browser...

**Client-side routing** is what enables users of a SPA to navigate to different "pages" without triggering a full-page refresh. 

The users will still be clicking navigation "links" that cause the browser's address bar to change.  However, the client-side router intercepts the changes to the path by tapping into the browser's [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API). Intercepting the change to the path in the address bar prevents a request from ever being sent to the server. Instead, the SPA will react locally and this is why it's called client-side routing.

> Note that we will continue to define server-side routes, however, the vast majority of those routes will be API-type routes that are accessed via AJAX calls, perform CRUD and return data as JSON needed by the frontend.

Feel free to checkout the Further Study section to learn more about the History API and Hash URIs.

### Concept 3: Client-Side Rendering

So, assume a user clicks an **Add Comment** button in a SPA and expects to see the new comment show up in the list of comments...

This is a SPA, so you don't want the button to cause a full-page refresh!

In SPAs, you would send an AJAX request containing the data for the new comment to the server.

The server would update the database and send back a response (probably containing the updated list of comments).

However, to make the comment show up in the UI, it needs to be updated using JavaScript - a process we call **client-side rendering**.

<details><summary>Guess who the undisputed client-side rendering champion is...</summary>
<p><strong>The React Library - of course!</strong></p>
</details>

### ❓ Review Questions - SPAs

1. **What's the most significant difference between a traditional multi-page web app and a single-page app?**

2. **What three development concepts enable the creation of comprehensive single-page applications?**

## Intro to the MERN-Stack

A technology stack, also called a solutions stack, is a group of development tools/services used to build an application.

For example, the LAMP-Stack is a mature technology stack that uses:  Linux, Apache (web server), MySQL and PHP (web development programming language).

In the last unit, our stack consisted of Python, Django & PostgreSQL - sorry, no meaningful acronym in this case.

There are a few tech stacks that use MongoDB, Express & Node as their backend solutions. Then one of the following front-end solutions is added to the stack:

- [React](https://reactjs.org/) which results in the MERN-Stack
- [Angular](https://angular.io/) which results in the MEAN-Stack
- [Vue.js](https://vuejs.org/) which results in the MEVN-Stack

The MERN-Stack is by far the most popular tech stack currently and will remain so into the foreseeable future.

### Architecture of the MERN-Stack

The following depicts the overall architecture of a MERN-Stack app:

<img src="https://i.imgur.com/m87p4kN.png">

The flow is as follows:

1. When the user browses to the app's URL, the Express server always delivers the static **public/index.html** page.

    > Note that there are no EJS templates on the server - just the static index.html.  In fact, there's no reason to install the EJS template engine.

2. When the browser loads **index.html**, it will request the scripts that contain the React app - this is shown as the blue CLIENT/React app.

3. The code in the React app's **index.js** module runs, which causes the React app to render for the first time. During this initial rendering, the client-side routing library renders components based upon the path of the URL.

4. After the **index.html** has been loaded, all subsequent HTTP communications between the client and server will be via AJAX in order to avoid the page from being reloaded.

5. Certain components may want to CRUD data on the server. However, we won't litter components with the code responsible for CRUD. Instead, as a best practice, that code will be organized into **service/API** modules.

6. On the server, a single non-API "traditional" route will be defined with the purpose of delivering the static **index.html** file. We will refer to this route as the "catch all" route since it will match all `GET` requests that do not match any of the "API" routes...

7. Other than the single "catch all" route just mentioned, all other routes on the server will be defined to respond to AJAX requests with JSON. By convention, the endpoints of these routes with be prefaced with `/api`, e.g., `/api/cats`, `/api/login`, etc.

### How to Structure a MERN-Stack Project

Up until this point, we've taken for granted that full-stack apps, like your Express and Django projects, were single, integrated projects.

However, developing a MERN-stack project involves complexities such as tooling, React's integrated development server, etc.

Additionally, there are concerns in both **development and production** environments that have to be addressed.

#### During Development...

A React project uses a development server that compiles and serves the React app to the browser at `localhost:3000`.

<details>
<summary>❓ There's a conflict between React's development server and the Express applications we've built previously - what is it?</summary>
<p><strong>They both run on port 3000 by default.</strong></p>
</details>

Luckily, the React team recognized this conflict and has a solution which we'll see in a bit.

#### Production Environment Concerns

As we develop our React app locally, we're writing source code that React's dev server builds and runs automatically.  However, this is not production ready code because it has extra debugging logic, etc.

In a moment will see how to **build** the React app locally, however, this locally built code is git ignored thus it's important to ensure that whatever hosting service you deploy to is configured to **build** the React app in the cloud.

Luckily for us, beginning in 2019, Heroku started to automatically build React apps when they are deployed.

In addition to ensuring that the hosting service builds the React app, we will also need to code the Express app to serve the built production code.

#### Possible MERN-Stack Project Structures

There are two general architectures we could pursue:

1. Maintain **two** separate projects, one for the React app, the other for the Express backend.
2. Integrate the codebase for both the React frontend and the Express backend.

| Architecture | Pros | Cons |
| --- | --- | --- |
| Separate Projects | <ul><li>Better for when the backend services multiple frontend projects (web, native mobile, desktop).</li></ul> | <ul><li>Must manage two projects and git repos.</li><li>Must deploy to two separate projects.</li><li>The React project will require code and/or configuration to access the correct backend during development (localhost) and production (could be anywhere).</li><li>Must implement CORS.</li></ul> |
| Single Project | <ul><li>A single integrated project.</li><li>None of the above Cons.</li></ul> | <ul><li>Not the best project structure to re-use the same backend project to service multiple frontend projects, e.g., Web/Mobile/Desktop</li></ul> |

The single, integrated project approach looks to be a no-brainer. But, what does the structure of a single project look like?

Again, two options:

1. Start with an Express app, then generate the React app within it (naming it `client` or something similar). This approach will result in nested **package.json** files and **node_modules** folders requiring you to "know where you are" when installing additional Node modules. Also with this approach, Heroku will not "see" the React app and will not build it automatically.
2. Start with a React app, then add an Express **server.js** and other server related folders/files as necessary. This approach results in a single **package.json** file and **node_modules** folder.

The second option is "cleaner" and less error prone, so we'll opt for that approach.

Now that we've discussed how to structure a MERN-Stack app, let's take a look at the reference app we'll build together this unit...

## This Unit's Reference App: **SEI CAFE**

As you know, it's important to practice the individual skills we learn for a given technology by bringing them together to build a real-world working application.

This unit's reference app is a MERN-Stack online food ordering app called [SEI CAFE](https://sei-cafe.herokuapp.com/).

Be sure to sign-up:

<img src="https://i.imgur.com/ShSz0xE.png">

and place a couple of orders!

<img src="https://i.imgur.com/ZSsDUqk.png">

## Building a MERN-Stack's Infrastructure

We'll begin by building out the infrastructure (boilerplate) that every real-world MERN-Stack app starts with, including client-side routing and authentication.

After the infrastructure code is complete, we'll save the project to a separate repo that can be cloned to launch future MERN-Stack projects, including your capstone project at the end of this unit!

## Let's Begin Building **mern-infrastructure**

Here's the plan:

1. Generate the React app
2. Build the React app's production code
3. Code the skeleton Express app
4. Define the "catch all" route in the Express backend
5. Test the Express server

Let's do this!

### 1. Generate the React App

The **best** way to create a React project is by using the `create-react-app` script provided by the React team:

```
cd ~/code
npx create-react-app mern-infrastructure
```

> Note: A new folder will be created named **mern-infrastructure**. If you would like to generate a project in the future within an existing folder, you can use `.` in place of the project name.

Creating a new React app takes some time because `create-react-app` also installs the Node modules - and there's a ton of them!

Let's briefly review the outputted message:

```
Created git commit.

Success! Created mern-infrastructure at /Users/<your username>/code/mern-infrastructure
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd mern-infrastructure
  npm start

Happy hacking!
```

Now we can:

1. `cd mern-infrastructure`
2. Open the project in VS Code: `$ code .`
3. Open an integrated terminal in VS Code:  `control + backtick`
4. Spin up React's built-in development server: `npm start`, which automatically opens the app in a browser tab at `localhost:3000`:

    <img src="https://i.imgur.com/4ouH8bS.png" height="400">


The React development server automatically builds and reloads the app in the browser whenever changes are saved.

Within VS Code, we'll find a Node project's usual **package.json**, **node_modules**, etc.

The React project's source code lives within the **src** folder:

<img src="https://i.imgur.com/d9T3Vqw.png" height="400">

### 2. Building the React App's Production Code

We will soon be coding the Express server to serve the production **index.html** page. Thus, we need to build the React app's code locally into production code at least once so that the Express server does not raise an error.

The `create-react-app` CLI includes tooling and a **build** script in **package.json** that, when run, compiles the the code in the **src** and **public** folders of the React project into production code - placing it into a folder named **build**.

Let's run the build script:

```
npm run build
```

> Note: npm requires us to use the `run` command for scripts other than `start` and `test`.
 
After building, examining our project's structure reveals a new **build** folder containing production ready static assets including **index.html**, **static/css** & **static/js** folders, etc.  If this React app was a frontend only app, the assets in the build folder would be ready to be deployed to any static hosting service.

This **build** folder of production-ready goodness is ready to be served up by an Express backend...

### 3. Code the Skeleton Express App

Now with the React app up and running, we can start to code the Express backend.

We _could_ use Express generator if we save the existing React-oriented **package.json** file and merge it with the Express dependencies.

Instead we're going to code our own Express app from scratch because we won't need much middleware, etc. due to the fact that the Express backend simply needs to:

- Deliver the **production-ready** **index.html**, which will in turn request the **production-ready** scripts, etc.
- Respond to AJAX requests, performing any necessary CRUD, and finally respond with JSON.

#### Install the Modules for the Express Server

There's no problem with the Express project happily sharing that same **package.json** that `create-react-app` created.

For now, we're only going to install a minimal number of modules for the Express app:

```
npm i express morgan serve-favicon
```

> Again, we don't need a view engine because our server will be either serving static assets (index.html, CSS, JS, images, etc.) or responding to AJAX requests with JSON. There will be no EJS templates!

Later, we'll install additional modules, e.g., `mongoose`, `dotenv`, etc.

#### Create and Code the Express App (**server.js**)

Let's code our Express server:

1. Ensure that you're still in the root folder of the React project.

2. `touch server.js`

3. At the top of **server.js**, let's do all the familiar stuff: `require` the modules; create the Express app; and mount the `morgan` logging middleware and `express.json()` middleware that processes JSON data sent in the AJAX request and adds it to the `req.body`:

	```js
	const express = require('express');
	const path = require('path');
	const favicon = require('serve-favicon');
	const logger = require('morgan');
	
	const app = express();
	
	app.use(logger('dev'));
	app.use(express.json());
	```

	<details><summary>❓ Why don't we need to mount the <code>express.urlencoded()</code> middleware also?</summary><p><strong>Because <code>express.urlencoded</code> middleware is used to process data submitted by a form - and we don't submit forms in a SPA.</strong></p></details>

4. Mount and configure the `serve-favicon` & `static` middleware so that they serve from the **build** (production) folder:

	```js
	app.use(express.json());
	
	// Configure both serve-favicon & static middleware
	// to serve from the production 'build' folder
	app.use(favicon(path.join(__dirname, 'build', 'favicon.ico')));
	app.use(express.static(path.join(__dirname, 'build')));
	```

5. Set the port for development to use `3001` so that React's dev server can continue to use `3000` and finally, tell the Express app to listen for incoming requests:

	```js
	// Configure to use port 3001 instead of 3000 during
	// development to avoid collision with React's dev server
	const port = process.env.PORT || 3001;
	
	app.listen(port, function() {
	  console.log(`Express app running on port ${port}`)
	});
	```

### 4. Define the "Catch All" Route

A single "catch all" route is required to serve the **index.html** when any non-AJAX "API" request is received by the Express app:

```js
app.use(express.static(path.join(__dirname, 'build')));

// Put API routes here, before the "catch all" route

// The following "catch all" route (note the *) is necessary
// to return the index.html on all non-AJAX requests
app.get('/*', function(req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});
```

> Note: Since this route is a "catch all" that matches every `GET` request, be sure to mount API or other routes before it!

Now the "catch all" route will serve the **index.html** whenever:

- A user types a path into the address bar and presses enter.
- The user refreshes the browser.
- An "external" link in an email, included on another web page, etc. to the MERN-Stack app is clicked.

For example, if we slack the following link to a friend: `https://sei-cafe.herokuapp.com/orders/new`. The friend clicks on it, initiating an HTTP request to our server.

However, the `/orders/new` part of the URL is supposed to be for the client router - not the server!  But there it is, and the server has to deal with it...

The server deals with it by, thanks to the "catch all" route, sending back  **index.html** - which is what we want.

After **index.html** loads in the browser, the React app's client-side routing will render components based upon the `/orders/new` path in the address bar.

### 5. Test the Express Server

We should now be able to test the Express server.

However, please note that we can no longer just type `nodemon` because just typing `nodemon` relies on the `start` script in **package.json** to know what to run and that script is being used to start the React dev server instead.

Therefore, in the MERN-Stack development environment, it's important to start the Express server by typing:

```
nodemon server
```

As expected, the Express server will run on port 3001 instead of 3000 (which is where the React dev server runs).

Browsing to `localhost:3001` will display our React app!

### ❓ Review Questions - MERN-Stack Development

1. **Is the app we're currently viewing at `localhost:3001` the "production" version of the React app or the version within the `src` folder?**

2. **What command must be run to update the React app's production code?**

## Configure React for MERN-stack Development

Note how we're viewing the React app without the React development server running - as we just discussed, this is because we are viewing the built production code, not the code as it exists in the **src** folder.

> **IMPORTANT**: During development, you don't want to browse to `localhost:3001`! Instead, you want the browser to load the React app from React's dev server on `localhost:3000`. You should only browse to `localhost:3001` to check out how the production code will run when deployed, however, don't forget to build before doing so.

So, when you are hacking out code and nothing seems to be updating in the browser - be sure to verify that you are browsing `localhost:3000`!

### Running Both Express & React During Development

To develop a MERN-Stack app, you'll need two **separate** terminal sessions for running:

1. The Express backend

2. React's development server

<details><summary>❓ If we don't already have the Express server running, we start it with what command?</summary>
<p>

```
nodemon server
```

</p>
</details>

<details><summary>❓ Now let's open a second terminal session and start React's dev server using what command?</summary>
<p>

```
npm start
```

</p>
</details>

Now, browse to `localhost:3000` - not `3001`!

So far, so good, but there's an problem lurking...

### Ensuring that the React Dev Server Sends AJAX Calls to the Express Server

Let's think ahead to when we begin to make AJAX requests from the React app to our server using code like this:

```js
return fetch('/api/orders/history').then(res => res.json());
```

<details><summary>❓ Which host/server will that fetch request be sent to?</summary>
<p><strong>The same host as shown in the address bar: <code>localhost:3000</code></strong>
</p></details>

<details><summary>❓ Where do we actually need the fetch requests be sent to during development?</summary>
<p><strong>Our Express server that's listening for AJAX requests at <code>localhost:3001</code> !</strong>
</p></details>

BTW, this is only a problem **during development** - the deployed app will be just fine thanks to our chosen MERN-Stack structure that uses a single project for the frontend and backend.

Luckily, the React team has created an easy fix for this dilemma. The React development server allows us to configure a "proxy" which specifies the host to forward API/AJAX calls to.

The fix is to add a `"proxy"` key in the **TOP-LEVEL** of the **package.json**:

```
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "proxy": "http://localhost:3001"
}
```

> Note: The React dev server will NOT automatically restart when changes are made to the package.json file.

Now **during development**, the React SPA can make AJAX calls, such as `fetch('/api/todos')`, and the request will be "proxied" (forwarded) to `localhost:3001` instead of `localhost:3000`.

#### Welcome to the MERN-stack!

## ❓ Essential Questions

1. **What folder holds a React app's production-ready code?**

2. **What's the responsibility of the "catch all" route defined in the Express app?** 

3. **True or False: API routes will need to be defined in the Express app so that the React app can CRUD data, etc. on the server.**

4. **True or False: The React app should use a "service/api" module to communicate with the backend's API routes via AJAX.**

## Further Study

### HTML5's History API

Using HTML5's [History API](https://developer.mozilla.org/en-US/docs/Web/API/History), an application in the browser is able to manipulate the browser's current URL using JS and without triggering a server request.

Client-side router software can use the History API to perform client-side routing to load different "screens" of functionality and perform other magic without a causing a request to be sent to the server, thus there's no full-page refresh.

This approach works wonderfully when the client router is in charge and is the only thing manipulating the URL in the address bar. However, what about when a user enters a URL manually, or a link external to the client app is clicked? These cases require a small bit of configuration on the server - a simple "catch all" route that handles all requests that don't match requests for static assets, API routes, etc. The catch all route will then return the **index.html** and all is well.

Later in this unit you'll be introduced to the popular [React Router](https://github.com/ReactTraining/react-router), which uses the History API to perform client-side routing in React SPAs.

### Browser Hash Navigation

The HTML specification includes what is known as **Hash URIs**.

Hash URIs include a "hash" (`#`) in the URI, for example:<br>[https://facebook.github.io/react/docs/react-dom.html#reference](https://facebook.github.io/react/docs/react-dom.html#reference)  

If we browse to the above link, we will see that it takes us directly to the "Reference" section on the page.

Hovering over other titles/sub-titles on the page reveals other links that have their href's set to a value prefaced with a "#", for example:

```html
<a class="hash-link" href="#unmountcomponentatnode">#</a>
```

Notice that when we can click on these links, the address bar changes, but the browser does **not** make an HTTP request.

Today's client-side routers lean toward using the History API over Hash URIs due mainly to the fact that the URL's are "prettier" without the hash.

## References

[React Docs](https://facebook.github.io/react/)
