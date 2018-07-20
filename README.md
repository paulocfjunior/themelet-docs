# Themelet Docs

A brief summary of why and how to use Liferay Themelets.

## Table of contents
- [Why use themelets?](#why-use-themelets)
- [How to create themelets?](#how-to-create-themelets)
    - [Preparing the environment](#preparing-the-environment)
    - [Creating themelets](#creating-themelets)
    - [Installing themelets locally for testing](#installing-themelets-locally-for-testing)
- [How to publish themelets to npm?](#how-to-publish-themelets-to-npm)
- [How to install a published themelet into the theme?](#how-to-install-a-published-themelet-into-the-theme)
    - [Under the hood](#under-the-hood)
- [Conclusion](#conclusion)

## Why use themelets?
Themelets are small pieces of code, designed to provide additional styles or functionalities to your Liferay Theme, so you can search, choose the themelets you want to use, and extend your theme with them.

## How to create themelets?

#### Preparing the environment
The process to create a themelet is pretty simple by using the Yeoman Liferay Theme Generator.
But before, you should have installed `node` and `npm` on your pc, if you don't have yet, you could follow [these steps](https://www.liquidweb.com/kb/how-to-install-nvm-node-version-manager-for-node-js-on-ubuntu-12-04-lts/) to setup the environment (Ubuntu).

Then you should make sure to have Gulp, Yeoman and the Liferay Theme generator installed on your machine, you could install them by using npm:
```
npm install -g yo gulp generator-liferay-theme
```
> _Probably you should run this as root._

#### Creating themelets
As the prerequisites were supplied, you should be able to use the generator. You can run this in any folder on your pc, it shouldn't be created inside your theme or your bundle:
```
yo liferay-theme:themelet
```
It will ask you for some information about the themelet before creating it, like the name, identifier, and which version of the Liferay Portal you intend to use. Also, it's possible to create one to be compatible with all versions of Liferay.
> If you set it to be compatible with a specific version of Liferay Portal, it won't even appear in the searches performed by themes in other versions, it is to avoid an unexpected behavior.

#### Installing themelets locally for testing
Before you publish your themelet you should want to test it on your development environment. To do this you should install your themelet on your local repository globally, so navigate to the **_themelet_** folder and run the command:
```
/path/to/your/themelet$ npm install -g .
```
After that you should be able to extend your theme with your themelet, to do this you should go to the **_theme_** folder and run the command:
```
/path/to/your/theme$ gulp extend
```
And then it will show you a prompt, choose **Themelet**:
```
? What kind of theme asset would you like to extend?
  Base theme
❯ Themelet
```

Then it will ask you if you want to search on your machine or on the npm public registry, for testing, choose the first one:
```
? Where would you like to search for themelets? (Use arrow keys)
❯ Search globally installed npm modules (development purposes only)
  Search npm registry (published modules)
```
> Note it is recommended for development purposes only.

Then it will look for all themelets globally installed on your machine and show to you to choose the ones you want:
```
? Select a themelet
❯ ◉ demo-themelet
  ◯ another-demo-themelet
  ◯ yet-another-demo-themelet
```
> Use space to select the themelets you want, you can select multiple at once, and deselect the ones you don't want on your theme anymore.

After you confirm that, it will process your request and then the themelet will be added to your `node_modules` folder, and your theme's `package.json` file should be updated to describe which themelets are installed.
> If you deploy this to a production server, the themelet won't work, once the themelet isn't installed on the global `node_modules` there.

## How to publish themelets to npm?
First, you need to create and login to an npm account on your terminal. To do that you can run `npm adduser` and fill the credentials. It would create an account in the npm registry if you didn't have one yet. If you want to test it worked, you can run the `npm whoami` command, it should return your npm username. You should be able to login on the [npmjs site](https://www.npmjs.com) also.
> `npm login` is an alias to `npm adduser` and behaves exactly the same way. 

Then, to publish the package, you should execute the `npm publish` command. After that, your package should be available in the public npm registry to everyone who wanted to use it.

If you need to make changes to your themelet, you could publish it again, but before you will need to increment the version because it's not possible to publish the same package with the same version twice. For this you should use semantic versioning, it's an npm CLI command that will automatically update your metadata to the next major, minor or patch version.
> For more information about npm packages and to understand how the semantic versioning works, you could check [here](https://docs.npmjs.com/getting-started/publishing-npm-packages).

## How to install a published themelet into the theme?
Once you have a themelet published to npm, it's ready to extend your theme.

So, as you did for testing, you should go to your **theme** directory and run `gulp extend` command. You follow the steps and when it ask you like to search, you choose npm registry. 
```
? Where would you like to search for themelets? (Use arrow keys)
  Search globally installed npm modules (development purposes only)
❯ Search npm registry (published modules)
```
> This method is indicated for **_production_** environments.

You could do a search by name or you could just give a brief description of what you want, the extend task will search for the packages that match the most with your terms and show you a list. Then you could select the ones you want and proceed to the installation.

> The search considers only the packages that have **'liferay-theme'** included on their keywords. Your themelet's `package.json` file contains the keywords key, it accepts an array of strings, you can change that directly.

After that, the themelet will be added to your `node_modules` folder, and your theme's `package.json` file will be modified to describe which themelets are installed.

#### Under the hood
There is a difference between running `npm install` and `gulp extend` on the theme to _install_ your themelet. During the _extend_ process, although your themelet is installed via npm, your `package.json`'s themelet dependencies are changed too, this couple things are required to the themelet works.

## Conclusion
Then you should run `gulp deploy` in your theme to generate the build files and the dist war file, and you can also deploy it to your production server, it should work painless.