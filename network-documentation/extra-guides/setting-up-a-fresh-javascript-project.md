---
description: >-
  This guide explains how to set up a new project directory for working with
  example JavaScript code
---

# Setting up a fresh JavaScript Project with dotenv

{% embed url="https://youtu.be/o8m5NYBZFe4" caption="So fresh and so clean!" %}

## Make sure Node.js is installed

_If you are installing Node.js on WSL_, you can [follow this guide](https://docs.microsoft.com/en-ca/windows/dev-environment/javascript/nodejs-on-wsl). 

Official releases of Node.js can be [downloaded from the official site](https://nodejs.org/en/download/).

Once the installation is complete, or if you already have Node.js installed, type the command `node -v` inside a terminal window \(such as `bash`, `zsh`, `cmd.exe` or PowerShell\) to check the currently installed version.

Most modern JavaScript APIs will target Node.js v12+. Using a version manager such as ****[**nvm**](https://github.com/nvm-sh/nvm) or [**fnm**](https://github.com/Schniz/fnm) is strongly encouraged, as it allows developers to quickly switch between Node.js versions as needed.

## Initialize the project directory

{% tabs %}
{% tab title="Enter these commands into a terminal" %}
```text
mkdir samplecode
cd samplecode
npm init -y
npm install --save dotenv
```
{% endtab %}
{% endtabs %}

These commands accomplish the following :

* `mkdir` creates our project directory, the directory name can be changed to anything suitable - it does not need to remain `samplecode`.
*  The `cd` command changes into the newly created directory \(making it the working directory\).
*  Run the node package manager - `npm` , optionally with the `-y` flag to skip the prompts and generate a default `package.json` .
*  Install the ****[**dotenv**](https://www.npmjs.com/package/dotenv) package, which will allow us to access environmental variables in our code.   Assuming no errors during the installation of dotenv, the project directory will now contain these files and directories in the following structure :

{% tabs %}
{% tab title="Directory structure" %}
```text
+-- /samplecode
    |
    +-- package.json
    |
    +-- package-lock.json
    |
    +-- /node_modules
        |  
        +-- /dotenv
```
{% endtab %}
{% endtabs %}

Since we used the `--save` flag when installing, it will be much easier to see which dependencies are installed by looking inside the `package.json` :

```text
{
  "name": "samplecode",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "dotenv": "^9.0.2"
  }
}
```

For anybody unfamiliar with environment variables, refer to our guide on ****[**dotenv and .env**](dotenv-and-.env.md) at this point to understand the package and what it is used for.

* _**If we are choosing to use the more modern**_ ****[**ES6 `import` syntax**](https://www.digitalocean.com/community/tutorials/js-modules-es6)_,_ when developing we will need to add a line to our `package.json` in order to prevent a`SyntaxError: Cannot use import statement outside a module` .  The `import` keyword was introduced in Node.js v12, a language feature to simplify the use of modules. Alternatively, we could use an `.mjs` file extension for all of our JavaScript files, however adding this line to `package.json` enables us to keep the `.js` file extension and saves a lot of  hassle with configuration : 

{% tabs %}
{% tab title="Type or paste this key:value pair into package.json if using ES6 import syntax" %}
```javascript
"type": "module",
```
{% endtab %}
{% endtabs %}

* _**If we are choosing to use the older, slightly more common**_ **`require()`** _**syntax**_, then it is unnecessary to add this line to `package.json` . 

With these steps completed, we now have a project directory that is prepared to have other dependencies installed into it using `npm install` or `yarn add` .  
This basic setup is a sufficient start to be able to write and execute further JavaScript code using Node.js, the next step being to install whichever dependencies we would like to learn about. This is a good way to experiment and become familiar with particular JavaScript libraries.

## References

{% embed url="https://www.digitalocean.com/community/tutorials/js-modules-es6" %}



