### Project Settings

These are the steps for any serverside project with :

- NodeJS
- Express JS
- Knex
- ejs


#### In the case where you've forked a repo, all you have to do is clone it somewhere

```
	$ git clone [repo_url]
	$ cd [repo_name]
	
```

#### In the case where you're creating a new project 

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

- create a repo 

	```
	$ git init
	```
-  create a [markdown](https://guides.github.com/features/mastering-markdown/) readme file and add a nice description of what that repo is all about. Don't complain, and don't say 'nah, later ..'.

 They're MY instrutions, do as I say. 

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

### Folder Structure
 - Create models,views, controllers folders
 - Create assets folder, with css,images and javascript subfolders.
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
	
	What do these modules do? .. 
	
	- [`express`](https://www.npmjs.com/package/express)? If you're still wondering what does this do, time for another career path, bro. Also, express is a fancy nodeJS framework that spares the need to repeat some nodeJS code to do web services.
	
	- [`ejs`] (https://www.npmjs.com/package/ejs) it is a view engine that can be used with express js. ejs stands for embeded javascript, which really really means that you can embed javascript in your html code. 
	- [`knex`](https://www.npmjs.com/package/knex) it is a SQL schema and query builder with a javascript synax. I'd like to imagine it as fancy wrapper around SQL. 
	- [`body-parser`](https://www.npmjs.com/package/body-parser) how I've used it so far, it basically parses the form input fields with their values into an object that you can access from a server request property called body.

		```
		req.body
		```
		
	- [`method-override`](https://www.npmjs.com/package/method-override) to your own dismay and mine, HTML forms doesn't support request verbs PUT and DELETE, so we need the method-override module to that for us. 
	- [`morgan`](https://www.npmjs.com/package/morgan) this one logs to your console what ever request that took place.
	- [`locus`](https://www.npmjs.com/package/locus) the website says it allows to open a REPL during your program execution, with access to all variables, and that's exactly what locus do.

<br>

- A `node_modules` directory containing all the modules you've just installed will be added to your project after that `npm install` command.
 
<br>
 
### KNEX
 
Now that you've just installed [knex](http://knexjs.org/#Builder-update) module, what can we do with it? 
 
 <br>
 ![take over the world](http://s2.quickmeme.com/img/ca/ca1e82814fbabf4703590d43509c7f4c2c1ce2403a1e634162043cef0a894c7f.jpg)
 
- No, you can't do that; but here is what you can do with it:
 
 ```
 $ knex init
 ```
 
- After you enter the above command, a file called `knexfile.js` will be created. This file will contain all database configuration settings. 
- Since, we're still in development environment open the `knexfile.js` file and head to the developement object. 
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
 
- Wait, what about that `knex.js` file? What am I going to use that for? Well kids, you're going to use that to tell your knex model what environment you're actually in right now. We've set the development object on `knexfile.js`, but we haven't told knex what that we're actually in development mode yet.. duh!
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
 For every table, you need a migration. If you're adding a new column to your table, then you need to make a new migration. How do we make a migration for table? 
 
 ```
 $ knex migrate: make [migration name]
 ```
 
 A new directory called `migrations` should be created in your project directory. `cd` and `tree` into the folder and check the file that has been created inside that migration .. what's that weird name, huh? 
 It's the exact date and time the migration has been created and the name is the migration name you've entered above. Open the file .. 
 
 ![Hmmm](http://i.imgur.com/eptUkTN.jpg)
 
 Me neither. 
 
- Assuming that this migration is for authors table, the code should look like this:

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
 
 ### ejs
 
 For all those times when plain old html and javascript are just too easy.
 
 Embedded javascript allows you to process your data server-side, and then send it to your ejs templet to render in html. In your routes file, process all of the data you want to show in html into an object and render it. Your server-side code should look something like this:
 
 ```
 res.render('index', {someData: data});
 ```
 Where index is your index.ejs page and {someData: data} is the object you are rendering.
 
 Now for the fun part! ejs mosies along over to your index.ejs page, and looks for anything inside the ejs tags that matches someData.
 - <% %> for regular javascript
 - <%= %> for where code is being turned into html
 
 Your equivalent ejs code should look something like this:
 
 ```
 <% someData.forEach(function(data) { %> 
     <%= data.whatever %>     
<% }); %>

 ```