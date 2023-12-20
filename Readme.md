# Baiscs (Node JS & npm) 

Understanding Node-Js & npm is very important for backend development.
## What is Node Js?
**"** Node-Js is a just an enviroment to run JavaScript without browser. **"** 

JavaScript was originally created to handle browser functions and was unable for any tasks outside browser environment.\
Here Node-Js comes that give you power to run JavaScript outside browser.\
*(It's like a compiler of JavaScript)*

Visit `nodejs.org` to download Node-Js, simple next-next and installed.\
To check Is Node-Js installed? run
```
node -v
```
## Some Important Terms

#### **Package**:
 A Package is a bundled collection of *(pre-written)* code and files. 
#### **Library**:
 A Library is set of pre-written functions and routines, that developers use and reuse in their projects, saving time and effort. 
#### **Framework**:
 A Framework is like a structured blueprint, that provides a starter for building software applications. It offers a set of rules and tools for development. 
#### **Module**:
 A Module is a self-contained piece of code that performs a specific task in a larger program. 
#### **Dependency**:
 A piece of software that a program needs to function correctly. 
#### **API (Application Programming Interface)**:
 An API, is set of rules and tools that enable different software applications to communicate with each other. 

---
## What is npm ?
npm is *Node Package Manager*.

As names says **"** It manages node-js packages. **"**

It add or remove packages from your project. It cames with Node-Js by default, means when you install Node-js npm is also Installed.

To Check Is npm Installed? run
```
npm -v
```
---
To **Install a Package**
```
npm install package_name  
```
OR
```
npm i package_name  
```
---
To **Uninstall a Package**
```
npm uninstall package_name  
```
OR
```
npm un package_name  
```
---
To **Check *Latest version* of a Package**
```
npm outdated package_name  
```
To Check *Latest version of **All Packages*** (Installed in Project)
```
npm outdated
```
---
To ***Update a Package***
```
npm update package_name  
```
To *Update **All Packages*** (Installed in Project)
```
npm update
```
---

## Understanding **package.json**

**"** `package.json` is a configuration file used in Node.js projects to define various aspects of the project.**"**

It includes metadata, dependencies, and scripts. It provides essential information for Node.js & npm to manage the project.

To Start a Node Project, run
```
npm init -y
```
You can also use `npm init` and customize Options according to you.\
A file named `package.json` will generated, That looks like:
```
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```
All fields are clearly discibing itself,\
Here `main`, `scripts` and a missing field `dependencies` are important.