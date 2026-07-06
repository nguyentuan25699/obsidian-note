
## 1. Introduction to npm
- npm manage downloads of dependencies of project
- How to use:

	Installing all dependencies
```sh
npm install  //node_modules folder is created
npm update  //updating packages for newer version
```

	Installing single dependencies
```sh
npm install <package-name>
```

- npm manage versioning: specify any specify version of a package, or require version higher or lower than what you need
- Running tasks
	- The package.json file support a format for specifying command line tasks that can be run by using
```sh
npm run <task-name>

//Example
{
	"script": {
		"start-dev": "node lib/server-development", //npm run start-dev
		"start": "node lib/server-production" //npm run start
	}
}
```

- Two type of installation
	- A local install: local package
	- A global install: global package
```sh
npm install <package-name> //the package installed in the current file tree, under the node_modules subfolder

npm install -g <package-name> //npm wont install the package under the local folder, it will use global location

npm root -g //this command tell you where exact localtion is on your machine. For example: on macOS or linux this location could be `/user/local/lib/node_modules`
```


## 2. package.json and package-lock.json file
### package.json file
- Is kind of a manifest for project, it can do a lot of things, completely unrelated. It's a central repository of configuration for tools.
	- File structure
```json
Example 1: package.json is empty
{}

Example 2: package.json defines a `name` property which tells the name of the app, or package
{
	"name": "test-project"
}
```

There are a lot of properties in this file
- **version**: indicate the current version
- **name**: sets the application/package name
- **description**: is a brief description of the app/package
- **main**: set the entry point for the application
- **private**: if set to true prevents the app/package to be accidentally published on npm
- **script**: defines a set of node script you can run
- **dependencies**: sets a list of npm packages installed as dependencies
- **devDependencies**: sets a list of npm packages installed as development dependencies
- **engines**: sets which versions of Node.js this package/app works on.
- ..etc..

Example of package.json file
```json
{
	"name": "local-facebook-content-scheduler-api",
	"version": "0.1.0",
	"private": true,
	"type": "module",
	"scripts": {
		"dev": "tsx watch src/index.ts",
		"build": "tsc",
		"start": "node dist/index.js"
	},
	"dependencies": {
		"cors": "^2.8.5",
		"express": "^4.19.2"
	},
	"devDependencies": {
		"@types/cors": "^2.8.17",
		"@types/express": "^4.17.21",
		"@types/node": "^22.5.4",
		"tsx": "^4.19.0",
		"typescript": "^5.5.4"
	},
	"engines": {
		"node": ">=22"
	}
}
```


### package-lock.json
- Is to keep track of the exact version of every package
- This solves a very specific problem that package.json left unsolved
	- package-lock.json sets your currently installed version of each package in stone, and npm will use those exact version when running `npm install`
	- package-lock.json file needs to be committed to your Git respository, so it can be fetched by another people
	- The dependencies version will be updated in the package-lock.json file when you run `npm update`
