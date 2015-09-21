# jmBoilerplate [![Dependency Status](https://www.versioneye.com/user/projects/55f92f283ed89400170006fb/badge.svg?style=flat)](https://www.versioneye.com/user/projects/55f92f283ed89400170006fb)

**Table of Contents**

1. [What's inside](#1-whats-inside)
2. [Getting started](#2-getting-started)
3. [Project structure](#3-project-structure)
4. [Build](#4-build)
   1. [Development](#41-development)
   2. [Production](#42-production)
5. [How-tos](#5-how-tos)
   1. [How to configure routing](#51-how-to-configure-routing)
   2. [How to create a controller](#52-how-to-create-a-controller)


## 1. What's inside
jmBoilerplate is an HTML5 framework that includes all the functionalities a web project needs so you can concentrate on the actual functionality and design of your app. It includes:
 - Modular JavaScript architecture with dependency management (RequireJS, Bower)
 - AngularJS including frequently used services like routing, translation, configuration, mediator (can be deactivated)
 - A build process for development and production including:
     - Optimizing and minification of your JavaScript
	 - Compiling your SCSS styles (with Compass) including needed vendor libraries loaded with Bower
	 - HTML-code minification
	 - Sprites generation, to reduce the amount of image-requests
 - Also it comes with Fontawesome and angular ui-notification (both can be deactivated).
	 - Fontawesome is used as a loading spinner if the route changes
	 - ui-notification is used when the app crashes and a unhandled exception is thrown.
	   It will be shown to the user. But ui-notification can also be used to show
	   custom messages from inside your controller
	
## 2. Getting started
Requirements for development: NodeJS with npm and Bower installed.
NodeJS is required for the build process (Grunt) and Bower for all the dependencies your application needs (like jQuery, AngularJS, ...)

**Instructions**

1. Download this repository (with ``$ git clone`` or download it with click on "__Download ZIP__")
2. In the project directory run ``$ npm install``.
3. After that run ``$ bower install``
4. Make sure you have installed [Compass](http://compass-style.org/install/) (which requires Ruby and SASS)
5. Finally, run ``$ grunt dev``

And you are done and can start developing your application! Simply open the 
included index.html or open your browser and type in http://localhost:8000 (if you have
not disabled the server - see below).

## 3. Project structure
The structure is easy to understand:
```
jmBoilerplate/
|-- src/
|   |-- app/
|   |   |-- controllers/
|   |   |-- directives/
|   |   |-- factories/
|   |   |-- filters/
|   |   |-- services/
|   |   |-- providers/
|   |   |-- app.js
|   |   |-- config.js
|   |   |-- main.js
|   |   |-- routes.js
|   |-- assets/
|   |   |-- images/
|   |   |-- fonts/
|   |-- resources/
|   |-- styles/
|       |-- _base.scss
|       |-- _functions.scss
|       |-- _mixins.scss
|       |-- _settings.scss
|       |-- _sprites.scss
|       |-- app.scss
|-- node_modules/
|-- vendor/
|-- .bowerrc
|-- bower.json
|-- Gruntfile.js
|-- index.html
|-- jmBoilerplate.version
|-- package.json
|-- README.md
```
Step by step:
- src/
  - This is were your applications source code lives
- src/app
  - Define your business logic here. This includes controllers,
    routing, configuration and anything else that is JS-based. Have a look
	at the containing files to see how they are working.
	
	Note: The structure is up to you. If you want to use module-folders
	instead of functionality-folders nobody keeps you from. But for the most
	projects using folders like
	```
	src/app/
	|-- controllers/
	|-- directives/
	|-- ...
	```
	is enough and less comlicated than
	```
	src/app/
	|-- module1
		|-- controllers/
		|-- filters/
		|-- ...
	|-- module2
		|-- controllers/
		|-- filters/
		|-- ...
	```
	If you want to change this structure just change the file
	location in "main.js".
- src/assets
  - Your static assets live here. You can use them in the styles.
- src/resources
  - This is optionally and may be needed in some applications.
    Normally this includes all application based resources
	that are not assets, like translation-files or database
	files that will be used from inside the app.
- src/styles
  - Your styling will go into here. The main file that will
    be compiled from the build process is "app.scss". This file
	includes the "_base.scss" (Note: all include files will start
	with an underscore. This is a SCSS convention). The "_base.scss"
	imports all dependencies including the settings, functions, mixins
	and maybe vendor css/scss.
	The "_sprites.scss" will be generated by the build process and is
	only necessary to include from the "_base.scss".
	
	If you are interested in the files in detail, look at the files comments.
- node_modules/
  - Contains all modules that are necessary for the build process. Therefore
    it is only necessary for development purposes.
- vendor/
  - Contains your vendor libraries like jQuery, RequireJS, AngularJS, ...! They
    will be loaded into this directory with "Bower" (``$ bower install`` or ``$ bower update``).
	Add dependencies into "bower.json"!
- .bowerrc
  - Just a internal file to configure Bower.
- bower.json
  - This file is necessary to work with Bower. Also it contains all the
    metadata of your project if you want to publish and register it to the
	Bower database.
- Gruntfile.js
  - This is the build process.
- index.html
  - The applications index file.
- jmBoilerplate.version
  - This file gives you information about the installed jmBoilerplate
    version. If you want to update jmBoilerplate you can check the version inside this file
    against the current version.
- package.json
  - Necessary for the build process. Also it contains
    all the metadata of your project (like "bower.json"). Note: All
	the contributors that are listed in here will be included in the
	banner (copyrigt header) in your compiled js, css and html files.
- README.md
  - Describe your project here
  
## 4. Build
The build is the largest component of jmBoilerplate. It generates the files
you need to develop and to distribute your app.

How does this work? Well, it's pretty simple.
### 4.1 Development
If you want to develop your app simply run ``$ grunt dev``. In the background a folder "/build" will be created.
It will contain a subfolder "css" with your "app.css" inside. This is the compiled file
of your styles, without minification and with debug hints. Also it will track
any changes to your style-files and will re-run the compiling task on each file change. Cool, isn't it?
On top this will generate sprites for you. You can use for example retina sprites with
```scss
@include retina-sprite($my-icon);
```
Have a look at "_sprites.scss" inside "src/styles" for detailed usage informations.
If you want to prevent sprite generation you can call the development build with ``$ grunt dev --sprites=false``.

Also the development build creates a server so that you can run your application and debug
it (e.g. with Chrome or Safari) on your mobile devices. The server can be disabled with
```$ grunt dev --server=false```. By default it will run under port 8000, which you can change with
```$ grunt dev --port=1234```.

At least the development build includes livereload. This means, that if you have not disabled
the server and also not the livereload the webpage will be automatically reloaded
on file changes. You can also disable this feature by calling the build with ``$ grunt dev --livereload=false``.
To change the default livereload port (35729) call it with ``$ grunt dev --livereloadPort=1234```.

###4.2 Production
In production all JavaScript files will be combined and compressed in a single "app.min.js"-file. For this the
"RequireJS Optimizer" will be used. Also it will compile your styles and generate sprites (see [Development](#41-development) how to disable it).
Your production app will be generated with all assets, resources, js and css into "/dist" (will be created if it does not exist). On top the output will be zipped into "/dist". You can prevent this if you want with
calling `$ grunt prod --zip=false`.

## 5. How-tos
### 5.1 How to configure routing
Insisde your project there is a file called "routes.js" located inside "src/app". This file contains your routing
configuration. Each route needs to have at least a ``title`` (for the browser window), a ``file`` to load when the route
is called and of course a ``route``. Additionally you can add a ``primaryRoute`` (boolean) element to define that this route
should be loaded when your app loads.

You need to define at least one "/404"-route and a route with ``primaryRoute`` set to true.

### 5.2 How to create a controller
To create a new controller simply clone the file "HomeCtrl" located inside src/app.
Note: Alle Controllers must start with a CamelCase filename.

To connect your controller with a template, open your "index.html". In the correct place create
an element and assign your controller to it
```html
<div data-ng-controller="MyController as ctrl">
    <!-- Your controller logic comes here -->
</div>
```



































