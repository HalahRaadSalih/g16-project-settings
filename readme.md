## Project Settings

These are the steps for any serverside project with :

- NodeJS
- Express JS
- Knex
- EJS


## Table Of Contents

- [Git and Github](https://github.com/HalahRaadSalih/g16-project-settings#git-and-github)
- [MVC](https://github.com/HalahRaadSalih/g16-project-settings#mvc-and-folder-structure) 
- [NPM](https://github.com/HalahRaadSalih/g16-project-settings#npm)
- [KNEX](https://github.com/HalahRaadSalih/g16-project-settings#knex)
- [Migrations](https://github.com/HalahRaadSalih/g16-project-settings#migrations)
- [EJS](https://github.com/HalahRaadSalih/g16-project-settings#ejs)


### Git and Github

 In the case where you've forked a repo, all you have to do is clone it somewhere

```
	$ git clone [repo_url]
	$ cd [repo_name]
	
```

In the case where you're creating a new project 

- Make a new directory, duh!

	```
	$ mkdir [new_project_name]
	$ cd  [new_project_name]
	```
- If you're using [oh my zsh](http://ohmyz.sh/) then you can both create and cd into your new directory in one command:

	```
	$ take [new_project_name]
	```
	

Great now, you have a new folder and you're set for life, you can find a job, start a family .. 

wait .. What? 

- Create a repo 

	```
	$ git init
	```
-  Create a [markdown](https://guides.github.com/features/mastering-markdown/) readme file and add a nice description of what that repo is all about. Don't complain, and don't say 'nah, later ..'.

 They're MY instrutions, do as I say. >:-|

	```
	$ touch readme.md
	```
- Link your remote

	
	```
	$ git remote add origin [repo_url]
	$ git remote -v
	```
<br>

#### Now

<br>
![commit all things](http://i.imgur.com/dGidez2.jpg)

<br>

```
$ git status
$ git add readme.md
$ git commit -m "initial commit"
$ git push origin master
```

<br>

![](http://i.imgur.com/k0MjHQf.jpg)


I know, I know .. Me too. 

### MVC and Folder Structure

 - Create models, views, controllers folders
 - Create assets folder, with css, images and javascript subfolders.
 - Create server.js 
 - Cd into controllers folder and create router.js
 - Create db folder with knex.js file inside it
 - Your project after a `tree` command would look like this:

 ```
 	$ tree
 	├── assets
	│   ├── css
	│   ├── images
	│   └── javascript
	├── controllers
	│   └── router.js
	├── db
	│   └── knex.js
	├── models
	├── readme.md
	├── server.js
	└── views


 ```
 
 <br>
 
### NPM
 
- To create your `package.json` file, which will hold a reference to your project dependencies, use this command:
 
 ```
 	$ npm init
 ```
 
 A `package.json` file should be added to your project directory. 
 
- Install and save all the modules that you need to use in your project.  

	```
	$ npm install --save express ejs knex body-parser method-override morgan locus
	```
	![](http://img.pandawhale.com/post-38843-could-you-fucking-not-chloe-gi-QDAW.gif)
	<br>
	
	What do these modules do? .. 
	
	- [`express`](https://www.npmjs.com/package/express) If you're still wondering what this does, it's time for another career choice, bro. For the layman,  it is essentially a fancy minimalist NodeJS framework that spares the need to repeat sever code for web services.
	
	- [`ejs`] (https://www.npmjs.com/package/ejs) is a view engine that can be used with express.js, it stands for 'embeded javascript', which means that you can embed your javascript code with your html. Their are many options out in the wild, you can use [Jade](https://www.npmjs.com/package/jade) in place of ejs.
	- [`knex`](https://www.npmjs.com/package/knex) is a SQL schema and query builder with a javascript synax. I'd like to imagine it as a fancy wrapper around SQL. 
	- [`body-parser`](https://www.npmjs.com/package/body-parser) basically parses the form input fields for their values and places them into an object that you can be accessed with a server request.
		- For example, if I were to need the value of a text input, body-parser would place that text into an object that is held as the value of the **body** key that I could then access via a request: 

			```
			req.body
			```
		
	- [`method-override`](https://www.npmjs.com/package/method-override) to your own dismay and mine, HTML forms don't support request verbs PUT and DELETE, so we need the method-override module to give us that flexibility. 
	- [`morgan`](https://www.npmjs.com/package/morgan) logs into your terminal console every request that takes place. Good for debugging. 
	- [`locus`](https://www.npmjs.com/package/locus) opens a REPL during your program execution, allowing access to all variables. Again, amazing for debugging. 

<br>

- After the `npm install` command, a `node_modules` directory containing all these modules and any others you've installed, will be added to your project.
 
<br>
 
### KNEX
 
Now that you've just installed the [knex](http://knexjs.org/#Builder-update) module, what do we do with it? 
 
 <br>
 ![take over the world](http://s2.quickmeme.com/img/ca/ca1e82814fbabf4703590d43509c7f4c2c1ce2403a1e634162043cef0a894c7f.jpg)
 
- No, you can't do that; but here is what you can do with it:
 
 ```
 $ knex init
 ```
 
- After you enter the above command, a file called `knexfile.js` will be created. This file will contain all the database configuration settings. 
- Since we're still in the development environment open the `knexfile.js` file and head to the developement object. 
- Before we adjust anything in this file, we need to go back to the terminal and create a database:

	```
	$ createdb [database-name]
	```
- Now, let's head back to our `knexfile.js` file and take a look at that development object:
	- 	Change your client from `sqlite3` to `postgresql`
	-  Change the connection 'filename', to 'database'
	-  Make the [database-name] that you just created the value of the 'database' key for the connection object.
	-  Add a key called debug and set its value to `true`.
	-  Your development object should look like this:

	```
	development: {
		client: 'postgresql',
    	connection: {
      		database: '[database-name]'
    	},
    	debug: true
  	}
	```
 
- Wait, what about that `knex.js` file? What am I going to use that for? Well kids, you're going to use that to tell your knex model what environment you're actually in right now. We've set the development object in the `knexfile.js` file, but we haven't told knex that we're actually in development mode yet.. duh!
- So, how do we tell the knex module what environment we're using? Here is how:

	- open knex.js.
	- add this code:
		<br>

	```
	var env = process.env.NODE_ENV || 'development';
	var config = require('../knexfile')[env];

	module.exports = require('knex')(config);
	```
 
 
### Migrations

 For every table, you need a migration. In addition to this, if you're adding a new column to your table you will also need to make a new migration. 
 
 How do we make a new migration for table? 
 
 ```
 $ knex migrate: make [migration name]
 ```
 
 A new directory called `migrations` should be created in your project directory. `cd` and `tree` into the folder and check the file that has been created inside that migration ...wait, what's that weird number filled name?... 
 It's the exact date and time the migration had been created and the name is the migration name you've entered above. Open the file .. 
 
 ![Hmmm](http://i.imgur.com/eptUkTN.jpg)
 
 Me neither. 
 
- Assuming that this migration is for the author's table for the knex Library assignment, the code should look like this:

 ```
 exports.up = function(knex, Promise) {
  	return knex.schema.createTable('authors', 		function(table){
			table.increments(); // id serial primary key
			table.string('name');
	});
};
exports.down = function(knex, Promise) {
    return knex.schema.dropTable('authors');
};

 ```
 
- One more thing ... you need to run the migration by entering: 

 ```
 knex migrate: latest
 ```

- This command must be run after you `make`a migration ie. after you're done with creating all your migrations up to a certain point.

<br> 
 
### EJS
 
 For all those times when plain old html and javascript are just too easy.
 
Embedded javascript allows you to process your data server-side, and then send it to your ejs template to render in html. In your `routes.js` file, process all of the data you want to show in html into an object and render it. Your server-side code should look something like this:

 
 ```
 res.render('index', {someData: data});
 ```
 Where index is your `index.ejs` page and `{someData: data}` is the object you are rendering.
 
 Now for the fun part! ejs mosies over to your `index.ejs` page, and looks for anything inside the ejs tags that matches someData.
 
 - `<% %>` for regular javascript
 - `<%= %>` for where code is being turned into html
 
 The equivalent ejs code should look something like this:
 
 ```
 <% someData.forEach(function(data) { %> 
     <%= data.whatever %>     
 <% }); %>

 ```