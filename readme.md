### Project Settings

These are the steps for any serverside project with :

- NodeJS
- Express JS
- Knex
- ejs


#### In the case where you've forked a repo, all you have to do is clone it somewhere

```
	$ git clone [repo_url]
	$ cd [reop_name]
	
```

#### In the case where you're creating a new porject 

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
 - Cd into contollers folder and create router.js
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
	$ npm install --save express ejs knex body-parser 	method-override morgan locus
	```
<br>
 A `node_modules` directory containing all the modules you've just installed will be added to your project.
 
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

		- open `knex.js`.
		- add this code:
		

		```
		var env = process.env.NODE_ENV || 'development';
		var config = require('../knexfile')[env];

		module.exports = require('knex')(config);
		```
 
 