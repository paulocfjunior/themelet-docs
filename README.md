# Themelet Docs

A brief summary of why and how to use Liferay Themelets.

## Why use themelets?
Themelets are small pieces of code, designed to provide additional styles or functionalities to your Liferay Theme, so you can search, choose the themelets you want to use, and extend your theme with them.

## How to create themelets?
The process to create a themelet is pretty simple by using the Yeoman Liferay Theme Generator by the command:
```
yo liferay-theme:themelet
```
It will ask you for some information about the themelet before creating it, like the name, identifier, and which version of the Liferay Portal you intend to use. Also, it's possible to create one to be compatible with all versions of Liferay.
> If you set it to be compatible with a specific version of Liferay Portal, it won't even appear in the searches performed by themes in other versions, it's necessary to avoid an unexpected behavior.

## How to publish themelets to npm?
First, you need to create and login to an npm account on your terminal. To do that you can run `npm adduser` and fill the credentials. It would create an account in the npm registry if you didn't have one yet. If you want to test it worked, you can run the `npm whoami` command, it should return your npm username. You should be able to login on the [npmjs site](https://www.npmjs.com) also.
> `npm login` is an alias to `npm adduser` and behaves exactly the same way. 

Then, to publish the package, you should execute the `npm publish` command. After that, your package should be available in the public npm registry to everyone who wanted to use it.

If you need to make changes to your themelet, you could publish it again, but before you will need to increment the version because it's not possible to publish the same package with the same version twice. For this you should use semantic versioning, it's an npm CLI command that will automatically update your metadata to the next major, minor or patch version.
> For more information about npm packages and to understand how the semantic versioning works, you could check [here](https://docs.npmjs.com/getting-started/publishing-npm-packages).

## How to install a themelet on the theme?
Once you have a themelet published to npm, it's ready to extend your theme, and Liferay Theme Tasks have a gulp task for that.

So you should go to your theme directory and run `gulp extend` command, it will start an assistant to guide you through the import, then you should follow the steps and fill the required information.

There are two ways to import themelets, the first one is indicated to **_development_** environments, it searches your local npm repository and list all the themelets you have globally installed on your machine, then you could choose the ones you want to install and the tool will install them for you.

On the other hand, we can perform searches directly from npm, and find themelets created by anyone there. This method is indicated for **_production_** environments. You could do a search by name or you could just give a brief description of what you want, the extend task will search for the packages that match the most with your terms and show you a list. Then you could select the ones you want and proceed to the installation.

> The search considers only the packages that have **'liferay-theme'** included on their keywords.

After that, the themelet will be added to your `node_modules` folder, and your theme's `package.json` file will be modified to describe which themelets are installed.