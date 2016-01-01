### Project Settings

These are the steps for any serverside project

#### In case you're forked an repo, all you have to do is clone it somewhere

	```
	$ git clone [repo_url]
	$ cd [reop_name]
	```

#### In case you're creating a new porject 

- Make a new directory, duh.

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