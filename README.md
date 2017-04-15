Redux, React
---

This is my starter project based on:

* (Redux, React) https://github.com/verekia/js-stack-from-scratch tutorial by verekia.com

Note that I copied over the instructions so that I don't forget

# 01 - Node, Yarn, and `package.json`

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/01-node-yarn-package-json).

In this section we will set up Node, Yarn, a basic `package.json` file, and try a package.

## Node

> 💡 **[Node.js](https://nodejs.org/)** is a JavaScript runtime environment. It is mostly used for Back-End development, but also for general scripting. In the context of Front-End development, it can be used to perform a whole bunch of tasks like linting, testing, and assembling files.

We will use Node for basically everything in this tutorial, so you're going to need it. Head to the [download page](https://nodejs.org/en/download/current/) for **macOS** or **Windows** binaries, or the [package manager installations page](https://nodejs.org/en/download/package-manager/) for Linux distributions.

For instance, on **Ubuntu / Debian**, you would run the following commands to install Node:

```sh
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```

You want any version of Node > 6.5.0.

## Node Version Management Tools

If you need the flexibility to use multiple versions of Node, check out [NVM](https://github.com/creationix/nvm) or [tj/n](https://github.com/tj/n).

## NPM

NPM is the default package manager for Node. It is automatically installed alongside with Node. Package managers are used to install and manage packages (modules of code that you or someone else wrote). We are going to use a lot of packages in this tutorial, but we'll use Yarn, another package manager.

## Yarn

> 💡 **[Yarn](https://yarnpkg.com/)** is a Node.js package manager which is much faster than NPM, has offline support, and fetches dependencies [more predictably](https://yarnpkg.com/en/docs/yarn-lock).

Since it [came out](https://code.facebook.com/posts/1840075619545360) in October 2016, it received a very quick adoption and may soon become the package manager of choice of the JavaScript community. If you want to stick to NPM you can simply replace all `yarn add` and `yarn add --dev` commands of this tutorial by `npm install --save` and `npm install --save-dev`.

Install Yarn by following the [instructions](https://yarnpkg.com/en/docs/install) for your OS. I would recommend using the **Installation Script** from the *Alternatives* tab if you are on macOS or Unix, to [avoid](https://github.com/yarnpkg/yarn/issues/1505) relying on other package managers:

```sh
curl -o- -L https://yarnpkg.com/install.sh | bash
```

## `package.json`

> 💡 **[package.json](https://yarnpkg.com/en/docs/package-json)** is the file used to describe and configure your JavaScript project. It contains general information (your project name, version, contributors, license, etc), configuration options for tools you use, and even a section to run *tasks*.

- Create a new folder to work in, and `cd` in it.
- Run `yarn init` and answer the questions (`yarn init -y` to skip all questions), to generate a `package.json` file automatically.

Here is the basic `package.json` I'll use in this tutorial:

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "license": "MIT"
}
```

## Hello World

- Create an `index.js` file containing `console.log('Hello world')`

🏁 Run `node .` in this folder (`index.js` is the default file Node looks for in a folder). It should print "Hello world".

**Note**: See that 🏁 racing flag emoji? I will use it every time you reach a **checkpoint**. We are sometimes going to make a lot of changes in a row, and your code may not work until you reach the next checkpoint.

## `start` script

Running `node .` to execute our program is a bit too low-level. We are going to use an NPM/Yarn script to trigger the execution of that code instead. That will give us a nice abstraction to be able to always use `yarn start`, even when our program gets more complicated.

- In `package.json`, add a `scripts` object like so:

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "license": "MIT",
  "scripts": {
    "start": "node ."
  }
}
```

`start` is the name we give to the *task* that will run our program. We are going to create a lot of different tasks in this `scripts` object throughout this tutorial. `start` is typically the name given to the default task of an application. Some other standard task names are `stop` and `test`.

`package.json` must be a valid JSON file, which means that you cannot have trailing commas. So be careful when editing manually your `package.json` file.

🏁 Run `yarn start`. It should print `Hello world`.

## Git and `.gitignore`

- Initialize a Git repository with `git init`

- Create a `.gitignore` file and add the following to it:

```gitignore
.DS_Store
/*.log
```

`.DS_Store` files are auto-generated macOS files that you should never have in your repository.

`npm-debug.log` and `yarn-error.log` are files that are created when your package manager encounters an error, we don't want them versioned in our repository.

## Installing and using a package

In this section we will install and use a package. A "package" is simply a piece of code that someone else wrote, and that you can use in your own code. It can be anything. Here, we're going to try a package that helps you manipulate colors for instance.

- Install the community-made package called `color` by running `yarn add color`

Open `package.json` to see how Yarn automatically added `color` in  `dependencies`.

A `node_modules` folder has been created to store the package.

- Add `node_modules/` to your `.gitignore`

You will also notice that a `yarn.lock` file got generated by Yarn. You should commit this file to your repository, as it will ensure that everyone in your team uses the same version of your packages. If you're sticking to NPM instead of Yarn, the equivalent of this file is the *shrinkwrap*.

- Write the following to your `index.js` file:

```js
const color = require('color')

const redHexa = color({ r: 255, g: 0, b: 0 }).hex()

console.log(redHexa)
```

🏁 Run `yarn start`. It should print `#FF0000`.

Congratulations, you installed and used a package!

`color` is just used in this section to teach you how to use a simple package. We won't need it anymore, so you can uninstall it:

- Run `yarn remove color`

## Two kinds of dependencies

There are two kinds of package dependencies, `"dependencies"` and `"devDependencies"`:

**Dependencies** are libraries you need for your application to function (React, Redux, Lodash, jQuery, etc). You install them with `yarn add [package]`.

**Dev Dependencies** are libraries used during development or to build your application (Webpack, SASS, linters, testing frameworks, etc). You install those with `yarn add --dev [package]`.

Next section: [02 - Babel, ES6, ESLint, Flow, Jest, Husky](02-babel-es6-eslint-flow-jest-husky.md#readme)

Back to the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 02 - Babel, ES6, ESLint, Flow, Jest, and Husky

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/02-babel-es6-eslint-flow-jest-husky).

We're now going to use some ES6 syntax, which is a great improvement over the "old" ES5 syntax. All browsers and JS environments understand ES5 well, but not ES6. That's where a tool called Babel comes to the rescue!

## Babel

> 💡 **[Babel](https://babeljs.io/)** is a compiler that transforms ES6 code (and other things like React's JSX syntax) into ES5 code. It is very modular and can be used in tons of different [environments](https://babeljs.io/docs/setup/). It is by far the preferred ES5 compiler of the React community.

- Move your `index.js` into a new `src` folder. This is where you will write your ES6 code. Remove the previous `color`-related code in `index.js`, and replace it with a simple:

```js
const str = 'ES6'
console.log(`Hello ${str}`)
```

We're using a *template string* here, which is an ES6 feature that lets us inject variables directly inside the string without concatenation using `${}`. Note that template strings are created using **backquotes**.

- Run `yarn add --dev babel-cli` to install the CLI interface for Babel.

Babel CLI comes with [two executables](https://babeljs.io/docs/usage/cli/): `babel`, which compiles ES6 files into new ES5 files, and `babel-node`, which you can use to replace your call to the `node` binary and execute ES6 files directly on the fly. `babel-node` is great for development but it is heavy and not meant for production. In this chapter we are going to use `babel-node` to set up the development environment, and in the next one we'll use `babel` to build ES5 files for production.

- In `package.json`, in your `start` script, replace `node .` by `babel-node src` (`index.js` is the default file Node looks for, which is why we can omit `index.js`).

If you try to run `yarn start` now, it should print the correct output, but Babel is not actually doing anything. That's because we didn't give it any information about which transformations we want to apply. The only reason it prints the right output is because Node natively understands ES6 without Babel's help. Some browsers or older versions of Node would not be so successful though!

- Run `yarn add --dev babel-preset-env` to install a Babel preset package called `env`, which contains configurations for the most recent ECMAScript features supported by Babel.

- Create a `.babelrc` file at the root of your project, which is a JSON file for your Babel configuration. Write the following to it to make Babel use the `env` preset:

```json
{
  "presets": [
    "env"
  ]
}
```

🏁 `yarn start` should still work, but it's actually doing something now. We can't really tell if it is though, since we're using `babel-node` to interpret ES6 code on the fly. You'll soon have a proof that your ES6 code is actually transformed when you reach the [ES6 modules syntax](#the-es6-modules-syntax) section of this chapter.

## ES6

> 💡 **[ES6](http://es6-features.org/)**: The most significant improvement of the JavaScript language. There are too many ES6 features to list them here but typical ES6 code uses classes with `class`, `const` and `let`, template strings, and arrow functions (`(text) => { console.log(text) }`).

### Creating an ES6 class

- Create a new file, `src/dog.js`, containing the following ES6 class:

```js
class Dog {
  constructor(name) {
    this.name = name
  }

  bark() {
    return `Wah wah, I am ${this.name}`
  }
}

module.exports = Dog
```

It should not look surprising to you if you've done OOP in the past in any language. It's relatively recent for JavaScript though. The class is exposed to the outside world via the `module.exports` assignment.

In `src/index.js`, write the following:

```js
const Dog = require('./dog')

const toby = new Dog('Toby')

console.log(toby.bark())
```

As you can see, unlike the community-made package `color` that we used before, when we require one of our files, we use `./` in the `require()`.

🏁 Run `yarn start` and it should print "Wah wah, I am Toby".

### The ES6 modules syntax

Here we simply replace `const Dog = require('./dog')` by `import Dog from './dog'`, which is the newer ES6 modules syntax (as opposed to "CommonJS" modules syntax). It is currently not natively supported by NodeJS, so this is your proof that Babel processes those ES6 files correctly.

In `dog.js`, we also replace `module.exports = Dog` by `export default Dog`

🏁 `yarn start` should still print "Wah wah, I am Toby".

## ESLint

> 💡 **[ESLint](http://eslint.org)** is the linter of choice for ES6 code. A linter gives you recommendations about code formatting, which enforces style consistency in your code, and code you share with your team. It's also a great way to learn about JavaScript by making mistakes that ESLint will catch.

ESLint works with *rules*, and there are [many of them](http://eslint.org/docs/rules/). Instead of configuring the rules we want for our code ourselves, we will use the config created by Airbnb. This config uses a few plugins, so we need to install those as well.

Check out Airbnb's most recent [instructions](https://www.npmjs.com/package/eslint-config-airbnb) to install the config package and all its dependencies correctly. As of 2017-02-03, they recommend using the following command in your terminal:

```sh
npm info eslint-config-airbnb@latest peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs yarn add --dev eslint-config-airbnb@latest
```

It should install everything you need and add `eslint-config-airbnb`, `eslint-plugin-import`, `eslint-plugin-jsx-a11y`, and `eslint-plugin-react` to your `package.json` file automatically.

**Note**: I've replaced `npm install` by `yarn add` in this command. Also, this won't work on Windows, so take a look at the `package.json` file of this repository and just install all the ESLint-related dependencies manually using `yarn add --dev packagename@^#.#.#` with `#.#.#` being the versions given in `package.json` for each package.

- Create an `.eslintrc.json` file at the root of your project, just like we did for Babel, and write the following to it:

```json
{
  "extends": "airbnb"
}
```

We'll create an NPM/Yarn script to run ESLint. Let's install the `eslint` package to be able to use the `eslint` CLI:

- Run `yarn add --dev eslint`

Update the `scripts` of your `package.json` to include a new `test` task:

```json
"scripts": {
  "start": "babel-node src",
  "test": "eslint src"
},
```

Here we just tell ESLint that want to lint all JavaScript files under the `src` folder.

We will use this standard `test` task to run a chain of all the commands that validate our code, whether it's linting, type checking, or unit testing.

- Run `yarn test`, and you should see a whole bunch of errors for missing semicolons, and a warning for using `console.log()` in `index.js`. Add `/* eslint-disable no-console */` at the top of our `index.js` file to allow the use of `console` in this file.

**Note**: If you're on Windows, make sure you configure your editor and Git to use Unix LF line endings and not Windows CRLF. If your project is only used in Windows environments, you can add `"linebreak-style": [2, "windows"]` in ESLint's `rules` array (see the example below) to enforce CRLF instead.

### Semicolons

Alright, this is probably the most heated debate in the JavaScript community, let's talk about it for a minute. JavaScript has this thing called Automatic Semicolon Insertion, which allows you to write your code with or without semicolons. It really comes down to personal preference and there is no right and wrong on this topic. If you like the syntax of Python, Ruby, or Scala, you will probably enjoy omitting semicolons. If you prefer the syntax of Java, C#, or PHP, you will probably prefer using semicolons.

Most people write JavaScript with semicolons, out of habit. That was my case until I tried going semicolon-less after seeing code samples from the Redux documentation. At first it felt a bit weird, simply because I was not used to it. After just one day of writing code this way I could not see myself going back to using semicolons at all. They felt so cumbersome and unnecessary. A semicolon-less code is easier on the eyes in my opinion, and is faster to type.

I recommend reading the [ESLint documentation about semicolons](http://eslint.org/docs/rules/semi). As mentioned in this page, if you're going semicolon-less, there are some rather rare cases where semicolons are required. ESLint can protect you from such cases with the `no-unexpected-multiline` rule. Let's set up ESLint to safely go semicolon-less in `.eslintrc.json`:

```json
{
  "extends": "airbnb",
  "rules": {
    "semi": [2, "never"],
    "no-unexpected-multiline": 2
  }
}
```

🏁 Run `yarn test`, and it should now pass successfully. Try adding an unnecessary semicolon somewhere to make sure the rule is set up correctly.

I am aware that some of you will want to keep using semicolons, which will make the code provided in this tutorial inconvenient. If you are using this tutorial just for learning, I'm sure it will remain bearable to learn without semicolons, until going back to using them on your real projects. If you want to use the code provided in this tutorial as a boilerplate though, it will require a bit of rewriting, which should be pretty quick with ESLint set to enforce semicolons to guide you through the process. I apologize if you're in such case.

### Compat

[Compat](https://github.com/amilajack/eslint-plugin-compat) is a neat ESLint plugin that warns you if you use some JavaScript APIs that are not available in the browsers you need to support. It uses [Browserslist](https://github.com/ai/browserslist), which relies on [Can I Use](http://caniuse.com/).

- Run `yarn add --dev eslint-plugin-compat`

- Add the following to your `package.json`, to indicate that we want to support browsers that have more than 1% market share:

```json
"browserslist": ["> 1%"],
```

- Edit your `.eslintrc.json` file like so:

```json
{
  "extends": "airbnb",
  "plugins": [
    "compat"
  ],
  "rules": {
    "semi": [2, "never"],
    "no-unexpected-multiline": 2,
    "compat/compat": 2
  }
}
```

You can try the plugin by using `navigator.serviceWorker` or `fetch` in your code for instance, which should raise an ESLint warning.

### ESLint in your editor

This chapter set you up with ESLint in the terminal, which is great for catching errors at build time / before pushing, but you also probably want it integrated to your IDE for immediate feedback. Do NOT use your IDE's native ES6 linting. Configure it so the binary it uses for linting is the one in your `node_modules` folder instead. This way it can use all of your project's config, the Airbnb preset, etc. Otherwise you will just get some generic ES6 linting.

## Flow

> 💡 **[Flow](https://flowtype.org/)**: A static type checker by Facebook. It detects inconsistent types in your code. For instance, it will give you an error if you try to use a string where should be using a number.

Right now, our JavaScript code is valid ES6 code. Flow can analyze plain JavaScript to give us some insights, but in order to use its full power, we need to add type annotations in our code, which will make it non-standard. We need to teach Babel and ESLint what those type annotations are in order for these tools to not freak out when parsing our files.

- Run `yarn add --dev flow-bin babel-preset-flow babel-eslint eslint-plugin-flowtype`

`flow-bin` is the binary to run Flow in our `scripts` tasks, `babel-preset-flow` is the preset for Babel to understand Flow annotations, `babel-eslint` is a package to enable ESLint *to rely on Babel's parser* instead of its own, and `eslint-plugin-flowtype` is an ESLint plugin to lint Flow annotations. Phew.

- Update your `.babelrc` file like so:

```json
{
  "presets": [
    "env",
    "flow"
  ]
}
```

- And update `.eslintrc.json` as well:

```json
{
  "extends": [
    "airbnb",
    "plugin:flowtype/recommended"
  ],
  "plugins": [
    "flowtype",
    "compat"
  ],
  "rules": {
    "semi": [2, "never"],
    "no-unexpected-multiline": 2,
    "compat/compat": 2
  }
}
```

**Note**: The `plugin:flowtype/recommended` contains the instruction for ESLint to use Babel's parser. If you want to be more explicit, feel free to add `"parser": "babel-eslint"` in `.eslintrc.json`.

I know this is a lot to take in, so take a minute to think about it. I'm still amazed that it is even possible for ESLint to use Babel's parser to understand Flow annotations. These 2 tools are really incredible for being so modular.

- Chain `flow` to your `test` task:

```json
"scripts": {
  "start": "babel-node src",
  "test": "eslint src && flow"
},
```

- Create a `.flowconfig` file at the root of your project containing:

```flowconfig
[options]
suppress_comment= \\(.\\|\n\\)*\\flow-disable-next-line
```

This is a little utility that we set up to make Flow ignore any warning detected on the next line. You would use it like this, similarly to `eslint-disable`:

```js
// flow-disable-next-line
something.flow(doesnt.like).for.instance()
```

Alright, we should be all set for the configuration part.

- Add Flow annotations to `src/dog.js` like so:

```js
// @flow

class Dog {
  name: string

  constructor(name: string) {
    this.name = name
  }

  bark() {
    return `Wah wah, I am ${this.name}`
  }
}

export default Dog
```

The `// @flow` comment tells Flow that we want this file to be type-checked. For the rest, Flow annotations are typically a colon after a function parameter or a function name. Check out the [documentation](https://flowtype.org/docs/quick-reference.html) for more details.

- Add `// @flow` at the top of `index.js` as well.

`yarn test` should now both lint and type-check your code fine.

There are 2 things that I want you to try:

- In `dog.js`, replace `constructor(name: string)` by `constructor(name: number)`, and run `yarn test`. You should get a **Flow** error telling you that those types are incompatible. That means Flow is set up correctly.

- Now replace `constructor(name: string)` by `constructor(name:string)`, and run `yarn test`. You should get an **ESLint** error telling you that Flow annotations should have a space after the colon. That means the Flow plugin for ESLint is set up correctly.

🏁 If you got the 2 different errors working, you are all set with Flow and ESLint! Remember to put the missing space back in the Flow annotation.

### Flow in your editor

Just like with ESLint, you should spend some time configuring your editor / IDE to give you immediate feedback when Flow detects issues in your code.

## Jest

> 💡 **[Jest](https://facebook.github.io/jest/)**: A JavaScript testing library by Facebook. It is very simple to set up and provides everything you would need from a testing library right out of the box. It can also test React components.

- Run `yarn add --dev jest babel-jest` to install Jest and the package to make it use Babel.

- Add the following to your `.eslintrc.json` at the root of the object to allow the use of Jest's functions without having to import them in every test file:

```json
"env": {
  "jest": true
}
```

- Create a `src/dog.test.js` file containing:

```js
import Dog from './dog'

test('Dog.bark', () => {
  const testDog = new Dog('Test')
  expect(testDog.bark()).toBe('Wah wah, I am Test')
})
```

- Add `jest` to your `test` script:

```json
"scripts": {
  "start": "babel-node src",
  "test": "eslint src && flow && jest --coverage"
},
```

The `--coverage` flag makes Jest generate coverage data for your tests automatically. This is useful to see which parts of your codebase lack testing. It writes this data into a `coverage` folder.

- Add `/coverage/` to your `.gitignore`

🏁 Run `yarn test`. After linting and type checking, it should run Jest tests and show a coverage table. Everything should be green!

## Git Hooks with Husky

> 💡 **[Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)**: Scripts that are run when certain actions like a commit or a push occur.

Okay so we now have this neat `test` task that tells us if our code looks good or not. We're going to set up Git Hooks to automatically run this task before every `git commit` and `git push`, which will prevent us from pushing bad code to the repository if it doesn't pass the `test` task.

[Husky](https://github.com/typicode/husky) is a package that makes this very easy to set up Git Hooks.

- Run `yarn add --dev husky`

All we have to do is to create two new tasks in `scripts`, `precommit` and `prepush`:

```json
"scripts": {
  "start": "babel-node src",
  "test": "eslint src && flow && jest --coverage",
  "precommit": "yarn test",
  "prepush": "yarn test"
},
```

🏁 If you now try to commit or push your code, it should automatically run the `test` task.

If it does not work, it is possible that `yarn add --dev husky` did not install the Git Hooks properly. I never encountered this issue but it happens for some people. If that's your case, run `yarn add --dev husky --force`, and maybe post a note describing your situation in [this issue](https://github.com/typicode/husky/issues/84).

**Note**: If you are pushing right after a commit, you can use `git push --no-verify` to avoid running all the tests again.

Next section: [03 - Express, Nodemon, PM2](03-express-nodemon-pm2.md#readme)

Back to the [previous section](01-node-yarn-package-json.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 03 - Express, Nodemon, and PM2

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/03-express-nodemon-pm2).

In this section we are going to create the server that will render our web app. We will also set up a development mode and a production mode for this server.

## Express

> 💡 **[Express](http://expressjs.com/)** is by far the most popular web application framework for Node. It provides a very simple and minimal API, and its features can be extended with *middleware*.

Let's set up a minimal Express server to serve an HTML page with some CSS.

- Delete everything inside `src`

Create the following files and folders:

- Create a `public/css/style.css` file containing:

```css
body {
  width: 960px;
  margin: auto;
  font-family: sans-serif;
}

h1 {
  color: limegreen;
}
```

- Create an empty `src/client/` folder.

- Create an empty `src/shared/` folder.

This folder is where we put *isomorphic / universal* JavaScript code – files that are used by both the client and the server. A great use case of shared code is *routes*, as you will see later in this tutorial when we'll make an asynchronous call. Here we simply have some configuration constants as an example for now.

- Create a `src/shared/config.js` file, containing:

```js
// @flow

export const WEB_PORT = process.env.PORT || 8000
export const STATIC_PATH = '/static'
export const APP_NAME = 'Hello App'
```

If the Node process used to run your app has a `process.env.PORT` environment variable set (that's the case when you deploy to Heroku for instance), it will use this for the port. If there is none, we default to `8000`.

- Create a `src/shared/util.js` file containing:

```js
// @flow

// eslint-disable-next-line import/prefer-default-export
export const isProd = process.env.NODE_ENV === 'production'
```

That's a simple util to test if we are running in production mode or not. The `// eslint-disable-next-line import/prefer-default-export` comment is because we only have one named export here. You can remove it as you add other exports in this file.

- Run `yarn add express compression`

`compression` is an Express middleware to activate Gzip compression on the server.

- Create a `src/server/index.js` file containing:

```js
// @flow

import compression from 'compression'
import express from 'express'

import { APP_NAME, STATIC_PATH, WEB_PORT } from '../shared/config'
import { isProd } from '../shared/util'
import renderApp from './render-app'

const app = express()

app.use(compression())
app.use(STATIC_PATH, express.static('dist'))
app.use(STATIC_PATH, express.static('public'))

app.get('/', (req, res) => {
  res.send(renderApp(APP_NAME))
})

app.listen(WEB_PORT, () => {
  // eslint-disable-next-line no-console
  console.log(`Server running on port ${WEB_PORT} ${isProd ? '(production)' : '(development)'}.`)
})
```

Nothing fancy here, it's almost Express' Hello World tutorial with a few additional imports. We're using 2 different static file directories here. `dist` for generated files, `public` for declarative ones.

- Create a `src/server/render-app.js` file containing:

```js
// @flow

import { STATIC_PATH } from '../shared/config'

const renderApp = (title: string) =>
`<!doctype html>
<html>
  <head>
    <title>${title}</title>
    <link rel="stylesheet" href="${STATIC_PATH}/css/style.css">
  </head>
  <body>
    <h1>${title}</h1>
  </body>
</html>
`

export default renderApp
```

You know how you typically have *templating engines* on the back-end? Well these are pretty much obsolete now that JavaScript supports template strings. Here we create a function that takes a `title` as a parameter and injects it in both the `title` and `h1` tags of the page, returning the complete HTML string. We also use a `STATIC_PATH` constant as the base path for all our static assets.

### HTML template strings syntax highlighting in Atom (optional)

It might be possible to get syntax highlighting working for HTML code inside template strings depending on your editor. In Atom, if you prefix your template string with an `html` tag (or any tag that *ends* with `html`, like `ilovehtml`), it will automatically highlight the content of that string. I sometimes use the `html` tag of the `common-tags` library to take advantage of this:

```js
import { html } from `common-tags`

const template = html`
<div>Wow, colors!</div>
`
```

I did not include this trick in the boilerplate of this tutorial, since it seems to only work in Atom, and it's less than ideal. Some of you Atom users might find it useful though.

Anyway, back to business!

- In `package.json` change your `start` script like so: `"start": "babel-node src/server",`

🏁 Run `yarn start`, and hit `localhost:8000` in your browser. If everything works as expected you should see a blank page with "Hello App" written both on the tab title and as a green heading on the page.

**Note**: Some processes – typically processes that wait for things to happen, like a server for instance – will prevent you from entering commands in your terminal until they're done. To interrupt such processes and get your prompt back, press **Ctrl+C**. You can alternatively open a new terminal tab if you want to keep them running while being able to enter commands. You can also make these processes run in the background but that's out of the scope of this tutorial.

## Nodemon

> 💡 **[Nodemon](https://nodemon.io/)** is a utility to automatically restart your Node server when file changes happen in the directory.

We are going to use Nodemon whenever we are in **development** mode.

- Run `yarn add --dev nodemon`

- Change your `scripts` like so:

```json
"start": "yarn dev:start",
"dev:start": "nodemon --ignore lib --exec babel-node src/server",
```

`start` is now just a pointer to an other task, `dev:start`. That gives us a layer of abstraction to tweak what the default task is.

In `dev:start`, the `--ignore lib` flag is to *not* restart the server when changes happen in the `lib` directory. You don't have this directory yet, but we're going to generate it in the next section of this chapter, so it will soon make sense. Nodemon typically runs the `node` binary. In our case, since we're using Babel, we can tell Nodemon to use the `babel-node` binary instead. This way it will understand all the ES6/Flow code.

🏁 Run `yarn start` and open `localhost:8000`. Go ahead and change the `APP_NAME` constant in `src/shared/config.js`, which should trigger a restart of your server in the terminal. Refresh the page to see the updated title. Note that this automatic restart of the server is different from *Hot Module Replacement*, which is when components on the page update in real-time. Here we still need a manual refresh, but at least we don't need to kill the process and restart it manually to see changes. Hot Module Replacement will be introduced in the next chapter.

## PM2

> 💡 **[PM2](http://pm2.keymetrics.io/)** is a Process Manager for Node. It keeps your processes alive in production, and offers tons of features to manage them and monitor them.

We are going to use PM2 whenever we are in **production** mode.

- Run `yarn add --dev pm2`

In production, you want your server to be as performant as possible. `babel-node` triggers the whole Babel transpilation process for your files at each execution, which is not something you want in production. We need Babel to do all this work beforehand, and have our server serve plain old pre-compiled ES5 files.

One of the main features of Babel is to take a folder of ES6 code (usually named `src`) and transpile it into a folder of ES5 code (usually named `lib`).

This `lib` folder being auto-generated, it's a good practice to clean it up before a new build, since it may contain unwanted old files. A neat simple package to delete files with cross platform support is `rimraf`.

- Run `yarn add --dev rimraf`

Let's add the following `prod:build` task to our `package.json`:

```json
"prod:build": "rimraf lib && babel src -d lib --ignore .test.js",
```

- Run `yarn prod:build`, and it should generate a `lib` folder containing the transpiled code, except for files ending in `.test.js` (note that `.test.jsx` files are also ignored by this parameter).

- Add `/lib/` to your `.gitignore`

One last thing: We are going to pass a `NODE_ENV` environment variable to our PM2 binary. With Unix, you would do this by running `NODE_ENV=production pm2`, but Windows uses a different syntax. We're going to use a small package called `cross-env` to make this syntax work on Windows as well.

- Run `yarn add --dev cross-env`

Let's update our `package.json` like so:

```json
"scripts": {
  "start": "yarn dev:start",
  "dev:start": "nodemon --ignore lib --exec babel-node src/server",
  "prod:build": "rimraf lib && babel src -d lib --ignore .test.js",
  "prod:start": "cross-env NODE_ENV=production pm2 start lib/server && pm2 logs",
  "prod:stop": "pm2 delete server",
  "test": "eslint src && flow && jest --coverage",
  "precommit": "yarn test",
  "prepush": "yarn test"
},
```

🏁 Run `yarn prod:build`, then run `yarn prod:start`. PM2 should show an active process. Go to `http://localhost:8000/` in your browser and you should see your app. Your terminal should show the logs, which should be "Server running on port 8000 (production).". Note that with PM2, your processes are run in the background. If you press Ctrl+C, it will kill the `pm2 logs` command, which was the last command our our `prod:start` chain, but the server should still render the page. If you want to stop the server, run `yarn prod:stop`

Now that we have a `prod:build` task, it would be neat to make sure it works fine before pushing code to the repository. Since it is probably unnecessary to run it for every commit, I suggest adding it to the `prepush` task:

```json
"prepush": "yarn test && yarn prod:build"
```

🏁 Run `yarn prepush` or just push your files to trigger the process.

**Note**: We don't have any test here, so Jest will complain a bit. Ignore it for now.

Next section: [04 - Webpack, React, HMR](04-webpack-react-hmr.md#readme)

Back to the [previous section](02-babel-es6-eslint-flow-jest-husky.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 04 - Webpack, React, and Hot Module Replacement

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/04-webpack-react-hmr).

## Webpack

> 💡 **[Webpack](https://webpack.js.org/)** is a *module bundler*. It takes a whole bunch of various source files, processes them, and assembles them into one (usually) JavaScript file called a bundle, which is the only file your client will execute.

Let's create some very basic *hello world* and bundle it with Webpack.

- In `src/shared/config.js`, add the following constants:

```js
export const WDS_PORT = 7000

export const APP_CONTAINER_CLASS = 'js-app'
export const APP_CONTAINER_SELECTOR = `.${APP_CONTAINER_CLASS}`
```

- Create an `src/client/index.js` file containing:

```js
import 'babel-polyfill'

import { APP_CONTAINER_SELECTOR } from '../shared/config'

document.querySelector(APP_CONTAINER_SELECTOR).innerHTML = '<h1>Hello Webpack!</h1>'
```

If you want to use some of the most recent ES features in your client code, like `Promise`s, you need to include the [Babel Polyfill](https://babeljs.io/docs/usage/polyfill/) before anything else in your bundle.

- Run `yarn add babel-polyfill`

If you run ESLint on this file, it will complain about `document` being undefined.

- Add the following to `env` in your `.eslintrc.json` to allow the use of `window` and `document`:

```json
"env": {
  "browser": true,
  "jest": true
}
```

Alright, we now need to bundle this ES6 client app into an ES5 bundle.

- Create a `webpack.config.babel.js` file containing:

```js
// @flow

import path from 'path'

import { WDS_PORT } from './src/shared/config'
import { isProd } from './src/shared/util'

export default {
  entry: [
    './src/client',
  ],
  output: {
    filename: 'js/bundle.js',
    path: path.resolve(__dirname, 'dist'),
    publicPath: isProd ? '/static/' : `http://localhost:${WDS_PORT}/dist/`,
  },
  module: {
    rules: [
      { test: /\.(js|jsx)$/, use: 'babel-loader', exclude: /node_modules/ },
    ],
  },
  devtool: isProd ? false : 'source-map',
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  devServer: {
    port: WDS_PORT,
  },
}
```

This file is used to describe how our bundle should be assembled: `entry` is the starting point of our app, `output.filename` is the name of the bundle to generate, `output.path` and `output.publicPath` describe the destination folder and URL. We put the bundle in a `dist` folder, which will contain things that are generated automatically (unlike the declarative CSS we created earlier which lives in `public`). `module.rules` is where you tell Webpack to apply some treatment to some type of files. Here we say that we want all `.js` and `.jsx` (for React) files except the ones in `node_modules` to go through something called `babel-loader`. We also want these two extensions to be used to `resolve` modules when we `import` them. Finally, we declare a port for Webpack Dev Server.

**Note**: The `.babel.js` extension is a Webpack feature to apply our Babel transformations to this config file.

`babel-loader` is a plugin for Webpack that transpiles your code just like we've been doing since the beginning of this tutorial. The only difference is that this time, the code will end up running in the browser instead of your server.

- Run `yarn add --dev webpack webpack-dev-server babel-core babel-loader`

`babel-core` is a peer-dependency of `babel-loader`, so we installed it as well.

- Add `/dist/` to your `.gitignore`

### Tasks update

In development mode, we are going to use `webpack-dev-server` to take advantage of Hot Module Reloading (later in this chapter), and in production we'll simply use `webpack` to generate bundles. In both cases, the `--progress` flag is useful to display additional information when Webpack is compiling your files. In production, we'll also pass the `-p` flag to `webpack` to minify our code, and the `NODE_ENV` variable set to `production`.

Let's update our `scripts` to implement all this, and improve some other tasks as well:

```json
"scripts": {
  "start": "yarn dev:start",
  "dev:start": "nodemon -e js,jsx --ignore lib --ignore dist --exec babel-node src/server",
  "dev:wds": "webpack-dev-server --progress",
  "prod:build": "rimraf lib dist && babel src -d lib --ignore .test.js && cross-env NODE_ENV=production webpack -p --progress",
  "prod:start": "cross-env NODE_ENV=production pm2 start lib/server && pm2 logs",
  "prod:stop": "pm2 delete server",
  "lint": "eslint src webpack.config.babel.js --ext .js,.jsx",
  "test": "yarn lint && flow && jest --coverage",
  "precommit": "yarn test",
  "prepush": "yarn test && yarn prod:build"
},
```

In `dev:start` we explicitly declare file extensions to monitor, `.js` and `.jsx`, and add `dist` in the ignored directories.

We created a separate `lint` task and added `webpack.config.babel.js` to the files to lint.

- Next, let's create the container for our app in `src/server/render-app.js`, and include the bundle that will be generated:

```js
// @flow

import { APP_CONTAINER_CLASS, STATIC_PATH, WDS_PORT } from '../shared/config'
import { isProd } from '../shared/util'

const renderApp = (title: string) =>
`<!doctype html>
<html>
  <head>
    <title>${title}</title>
    <link rel="stylesheet" href="${STATIC_PATH}/css/style.css">
  </head>
  <body>
    <div class="${APP_CONTAINER_CLASS}"></div>
    <script src="${isProd ? STATIC_PATH : `http://localhost:${WDS_PORT}/dist`}/js/bundle.js"></script>
  </body>
</html>
`

export default renderApp
```

Depending on the environment we're in, we'll include either the Webpack Dev Server bundle, or the production bundle. Note that the path to Webpack Dev Server's bundle is *virtual*, `dist/js/bundle.js` is not actually read from your hard drive in development mode. It's also necessary to give Webpack Dev Server a different port than your main web port.

- Finally, in `src/server/index.js`, tweak your `console.log` message like so:

```js
console.log(`Server running on port ${WEB_PORT} ${isProd ? '(production)' :
  '(development).\nKeep "yarn dev:wds" running in an other terminal'}.`)
```

That will give other developers a hint about what to do if they try to just run `yarn start` without Webpack Dev Server.

Alright that was a lot of changes, let's see if everything works as expected:

🏁 Run `yarn start` in a terminal. Open an other terminal tab or window, and run `yarn dev:wds` in it. Once Webpack Dev Server is done generating the bundle and its sourcemaps (which should both be ~600kB files) and both processes hang in your terminals, open `http://localhost:8000/` and you should see "Hello Webpack!". Open your Chrome console, and under the Source tab, check which files are included. You should only see `static/css/style.css` under `localhost:8000/`, and have all your ES6 source files under `webpack://./src`. That means sourcemaps are working. In your editor, in `src/client/index.js`, try changing `Hello Webpack!` into any other string. As you save the file, Webpack Dev Server in your terminal should generate a new bundle and the Chrome tab should reload automatically.

- Kill the previous processes in your terminals with Ctrl+C, then run `yarn prod:build`, and then `yarn prod:start`. Open `http://localhost:8000/` and you should still see "Hello Webpack!". In the Source tab of the Chrome console, you should this time find `static/js/bundle.js` under `localhost:8000/`, but no `webpack://` sources. Click on `bundle.js` to make sure it is minified. Run `yarn prod:stop`.

Good job, I know this was quite dense. You deserve a break! The next section is easier.

**Note**: I would recommend to have at least 3 terminals open, one for your Express server, one for the Webpack Dev Server, and one for Git, tests, and general commands like installing packages with `yarn`. Ideally, you should split your terminal screen in multiple panes to see them all.

## React

> 💡 **[React](https://facebook.github.io/react/)** is a library for building user interfaces by Facebook. It uses the **[JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)** syntax to represent HTML elements and components while leveraging the power of JavaScript.

In this section we are going to render some text using React and JSX.

First, let's install React and ReactDOM:

- Run `yarn add react react-dom`

Rename your `src/client/index.js` file into `src/client/index.jsx` and write some React code in it:

```js
// @flow

import 'babel-polyfill'

import React from 'react'
import ReactDOM from 'react-dom'

import App from './app'
import { APP_CONTAINER_SELECTOR } from '../shared/config'

ReactDOM.render(<App />, document.querySelector(APP_CONTAINER_SELECTOR))
```

- Create a `src/client/app.jsx` file containing:

```js
// @flow

import React from 'react'

const App = () => <h1>Hello React!</h1>

export default App
```

Since we use the JSX syntax here, we have to tell Babel that it needs to transform it with the `babel-preset-react` preset. And while we're at it, we're also going to add a Babel plugin called `flow-react-proptypes` which automatically generates PropTypes from Flow annotations for your React components.

- Run `yarn add --dev babel-preset-react babel-plugin-flow-react-proptypes` and edit your `.babelrc` file like so:

```json
{
  "presets": [
    "env",
    "flow",
    "react"
  ],
  "plugins": [
    "flow-react-proptypes"
  ]
}
```

🏁 Run `yarn start` and `yarn dev:wds` and hit `http://localhost:8000`. You should see "Hello React!".

Now try changing the text in `src/client/app.jsx` to something else. Webpack Dev Server should reload the page automatically, which is pretty neat, but we are going to make it even better.

## Hot Module Replacement

> 💡 **[Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement/)** (*HMR*) is a powerful Webpack feature to replace a module on the fly without reloading the entire page.

To make HMR work with React, we are going to need to tweak a few things.

- Run `yarn add react-hot-loader@next`

- Edit your `webpack.config.babel.js` like so:

```js
import webpack from 'webpack'
// [...]
entry: [
  'react-hot-loader/patch',
  './src/client',
],
// [...]
devServer: {
  port: WDS_PORT,
  hot: true,
},
plugins: [
  new webpack.optimize.OccurrenceOrderPlugin(),
  new webpack.HotModuleReplacementPlugin(),
  new webpack.NamedModulesPlugin(),
  new webpack.NoEmitOnErrorsPlugin(),
],
```

- Edit your `src/client/index.jsx` file:

```js
// @flow

import 'babel-polyfill'

import React from 'react'
import ReactDOM from 'react-dom'
import { AppContainer } from 'react-hot-loader'

import App from './app'
import { APP_CONTAINER_SELECTOR } from '../shared/config'

const rootEl = document.querySelector(APP_CONTAINER_SELECTOR)

const wrapApp = AppComponent =>
  <AppContainer>
    <AppComponent />
  </AppContainer>

ReactDOM.render(wrapApp(App), rootEl)

if (module.hot) {
  // flow-disable-next-line
  module.hot.accept('./app', () => {
    // eslint-disable-next-line global-require
    const NextApp = require('./app').default
    ReactDOM.render(wrapApp(NextApp), rootEl)
  })
}
```

We need to make our `App` a child of `react-hot-loader`'s `AppContainer`, and we need to `require` the next version of our `App` when hot-reloading. To make this  process clean and DRY, we create a little `wrapApp` function that we use in both places it needs to render `App`. Feel free to move the `eslint-disable global-require` to the top of the file to make this more readable.

🏁 Restart your `yarn dev:wds` process if it was still running. Open `localhost:8000`. In the Console tab, you should see some logs about HMR. Go ahead and change something in `src/client/app.jsx` and your changes should be reflected in your browser after a few seconds, without any full-page reload!

Next section: [05 - Redux, Immutable, Fetch](05-redux-immutable-fetch.md#readme)

Back to the [previous section](03-express-nodemon-pm2.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 05 - Redux, Immutable, and Fetch

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/05-redux-immutable-fetch).

In this chapter we will hook up React and Redux to make a very simple app. The app will consist of a message and a button. The message changes when the user clicks the button.

Before we start, here is a very quick introduction to ImmutableJS, which is completely unrelated to React and Redux, but will be used in this chapter.

## ImmutableJS

> 💡 **[ImmutableJS](https://facebook.github.io/immutable-js/)** (or just Immutable) is a library by Facebook to manipulate immutable collections, like lists and maps. Any change made on an immutable object returns a new object without mutating the original object.

For instance, instead of doing:

```js
const obj = { a: 1 }
obj.a = 2 // Mutates `obj`
```

You would do:

```js
const obj = Immutable.Map({ a: 1 })
obj.set('a', 2) // Returns a new object without mutating `obj`
```

This approach follows the **functional programming** paradigm, which works really well with Redux.

When creating immutable collections, a very convenient method is `Immutable.fromJS()`, which takes any regular JS object or array and returns a deeply immutable version of it:

```js
const immutablePerson = Immutable.fromJS({
  name: 'Stan',
  friends: ['Kyle', 'Cartman', 'Kenny'],
})

console.log(immutablePerson)

/*
 *  Map {
 *    "name": "Stan",
 *    "friends": List [ "Kyle", "Cartman", "Kenny" ]
 *  }
 */
```

- Run `yarn add immutable@4.0.0-rc.2`

## Redux

> 💡 **[Redux](http://redux.js.org/)** is a library to handle the lifecycle of your application. It creates a *store*, which is the single source of truth of the state of your app at any given time.

Let's start with the easy part, declaring our Redux actions:

- Run `yarn add redux redux-actions`

- Create a `src/client/action/hello.js` file containing:

```js
// @flow

import { createAction } from 'redux-actions'

export const SAY_HELLO = 'SAY_HELLO'

export const sayHello = createAction(SAY_HELLO)
```

This file exposes an *action*, `SAY_HELLO`, and its *action creator*, `sayHello`, which is a function. We use [`redux-actions`](https://github.com/acdlite/redux-actions) to reduce the boilerplate associated with Redux actions. `redux-actions` implement the [Flux Standard Action](https://github.com/acdlite/flux-standard-action) model, which makes *action creators* return objects with the `type` and `payload` attributes.

- Create a `src/client/reducer/hello.js` file containing:

```js
// @flow

import Immutable from 'immutable'
import type { fromJS as Immut } from 'immutable'

import { SAY_HELLO } from '../action/hello'

const initialState = Immutable.fromJS({
  message: 'Initial reducer message',
})

const helloReducer = (state: Immut = initialState, action: { type: string, payload: any }) => {
  switch (action.type) {
    case SAY_HELLO:
      return state.set('message', action.payload)
    default:
      return state
  }
}

export default helloReducer
```

In this file we initialize the state of our reducer with an Immutable Map containing one property, `message`, set to `Initial reducer message`. The `helloReducer` handles `SAY_HELLO` actions by simply setting the new `message` with the action payload. The Flow annotation for `action` destructures it into a `type` and a `payload`. The `payload` can be of `any` type. It looks funky if you've never seen this before, but it remains pretty understandable. For the type of `state`, we use the `import type` Flow instruction to get the return type of `fromJS`. We rename it to `Immut` for clarity, because `state: fromJS` would be pretty confusing. The `import type` line will get stripped out like any other Flow annotation. Note the usage of `Immutable.fromJS()` and `set()` as seen before.

## React-Redux

> 💡 **[react-redux](https://github.com/reactjs/react-redux)** *connects* a Redux store with React components. With `react-redux`, when the Redux store changes, React components get automatically updated. They can also fire Redux actions.

- Run `yarn add react-redux`

In this section we are going to create *Components* and *Containers*.

**Components** are *dumb* React components, in a sense that they don't know anything about the Redux state. **Containers** are *smart* components that know about the state and that we are going to *connect* to our dumb components.

- Create a `src/client/component/button.jsx` file containing:

```js
// @flow

import React from 'react'

type Props = {
  label: string,
  handleClick: Function,
}

const Button = ({ label, handleClick }: Props) =>
  <button onClick={handleClick}>{label}</button>

export default Button
```

**Note**: You can see a case of Flow *type alias* here. We define the `Props` type before annotating our component's destructured `props` with it.

- Create a `src/client/component/message.jsx` file containing:

```js
// @flow

import React from 'react'

type Props = {
  message: string,
}

const Message = ({ message }: Props) =>
  <p>{message}</p>

export default Message
```

These are examples of *dumb* components. They are logic-less, and just show whatever they are asked to show via React **props**. The main difference between `button.jsx` and `message.jsx` is that `Button` contains a reference to an action dispatcher in its props, where `Message` just contains some data to show.

Again, *components* don't know anything about Redux **actions** or the **state** of our app, which is why we are going to create smart **containers** that will feed the proper action dispatchers and data to these 2 dumb components.

- Create a `src/client/container/hello-button.js` file containing:

```js
// @flow

import { connect } from 'react-redux'

import { sayHello } from '../action/hello'
import Button from '../component/button'

const mapStateToProps = () => ({
  label: 'Say hello',
})

const mapDispatchToProps = dispatch => ({
  handleClick: () => { dispatch(sayHello('Hello!')) },
})

export default connect(mapStateToProps, mapDispatchToProps)(Button)
```

This container hooks up the `Button` component with the `sayHello` action and Redux's `dispatch` method.

- Create a `src/client/container/message.js` file containing:

```js
// @flow

import { connect } from 'react-redux'

import Message from '../component/message'

const mapStateToProps = state => ({
  message: state.hello.get('message'),
})

export default connect(mapStateToProps)(Message)
```

This container hooks up the Redux's app state with the `Message` component. When the state changes, `Message` will now automatically re-render with the proper `message` prop. These connections are done via the `connect` function of `react-redux`.

- Update your `src/client/app.jsx` file like so:

```js
// @flow

import React from 'react'
import HelloButton from './container/hello-button'
import Message from './container/message'
import { APP_NAME } from '../shared/config'

const App = () =>
  <div>
    <h1>{APP_NAME}</h1>
    <Message />
    <HelloButton />
  </div>

export default App
```

We still haven't initialized the Redux store and haven't put the 2 containers anywhere in our app yet:

- Edit `src/client/index.jsx` like so:

```js
// @flow

import 'babel-polyfill'

import React from 'react'
import ReactDOM from 'react-dom'
import { AppContainer } from 'react-hot-loader'
import { Provider } from 'react-redux'
import { createStore, combineReducers } from 'redux'

import App from './app'
import helloReducer from './reducer/hello'
import { APP_CONTAINER_SELECTOR } from '../shared/config'
import { isProd } from '../shared/util'

const store = createStore(combineReducers({ hello: helloReducer }),
  // eslint-disable-next-line no-underscore-dangle
  isProd ? undefined : window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__())

const rootEl = document.querySelector(APP_CONTAINER_SELECTOR)

const wrapApp = (AppComponent, reduxStore) =>
  <Provider store={reduxStore}>
    <AppContainer>
      <AppComponent />
    </AppContainer>
  </Provider>

ReactDOM.render(wrapApp(App, store), rootEl)

if (module.hot) {
  // flow-disable-next-line
  module.hot.accept('./app', () => {
    // eslint-disable-next-line global-require
    const NextApp = require('./app').default
    ReactDOM.render(wrapApp(NextApp, store), rootEl)
  })
}
```

Let's take a moment to review this. First, we create a *store* with `createStore`. Stores are created by passing reducers to them. Here we only have one reducer, but for the sake of future scalability, we use `combineReducers` to group all of our reducers together. The last weird parameter of `createStore` is something to hook up Redux to browser [Devtools](https://github.com/zalmoxisus/redux-devtools-extension), which are incredibly useful when debugging. Since ESLint will complain about the underscores in `__REDUX_DEVTOOLS_EXTENSION__`, we disable this ESLint rule. Next, we conveniently wrap our entire app inside `react-redux`'s `Provider` component thanks to our `wrapApp` function, and pass our store to it.

🏁 You can now run `yarn start` and `yarn dev:wds` and hit `http://localhost:8000`. You should see "Initial reducer message" and a button. When you click the button, the message should change to "Hello!". If you installed the Redux Devtools in your browser, you should see the app state change over time as you click on the button.

Congratulations, we finally made an app that does something! Okay it's not a *super* impressive from the outside, but we all know that it is powered by one badass stack under the hood.

## Extending our app with an asynchronous call

We are now going to add a second button to our app, which will trigger an AJAX call to retrieve a message from the server. For the sake of demonstration, this call will also send some data, the hard-coded number `1234`.

### The server endpoint

- Create a `src/shared/routes.js` file containing:

```js
// @flow

// eslint-disable-next-line import/prefer-default-export
export const helloEndpointRoute = (num: ?number) => `/ajax/hello/${num || ':num'}`
```

This function is a little helper to produce the following:

```js
helloEndpointRoute()     // -> '/ajax/hello/:num' (for Express)
helloEndpointRoute(1234) // -> '/ajax/hello/1234' (for the actual call)
```

Let's actually create a test real quick to make sure this thing works well.

- Create a `src/shared/routes.test.js` containing:

```js
import { helloEndpointRoute } from './routes'

test('helloEndpointRoute', () => {
  expect(helloEndpointRoute()).toBe('/ajax/hello/:num')
  expect(helloEndpointRoute(123)).toBe('/ajax/hello/123')
})
```

- Run `yarn test` and it should pass successfully.

- In `src/server/index.js`, add the following:

```js
import { helloEndpointRoute } from '../shared/routes'

// [under app.get('/')...]

app.get(helloEndpointRoute(), (req, res) => {
  res.json({ serverMessage: `Hello from the server! (received ${req.params.num})` })
})
```

### New containers

- Create a `src/client/container/hello-async-button.js` file containing:

```js
// @flow

import { connect } from 'react-redux'

import { sayHelloAsync } from '../action/hello'
import Button from '../component/button'

const mapStateToProps = () => ({
  label: 'Say hello asynchronously and send 1234',
})

const mapDispatchToProps = dispatch => ({
  handleClick: () => { dispatch(sayHelloAsync(1234)) },
})

export default connect(mapStateToProps, mapDispatchToProps)(Button)
```

In order to demonstrate how you would pass a parameter to your asynchronous call and to keep things simple, I am hard-coding a `1234` value here. This value would typically come from a form field filled by the user.

- Create a `src/client/container/message-async.js` file containing:

```js
// @flow

import { connect } from 'react-redux'

import MessageAsync from '../component/message'

const mapStateToProps = state => ({
  message: state.hello.get('messageAsync'),
})

export default connect(mapStateToProps)(MessageAsync)
```

You can see that in this container, we are referring to a `messageAsync` property, which we're going to add to our reducer soon.

What we need now is to create the `sayHelloAsync` action.

### Fetch

> 💡 **[Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)** is a standardized JavaScript function to make asynchronous calls inspired by jQuery's AJAX methods.

We are going to use `fetch` to make calls to the server from the client. `fetch` is not supported by all browsers yet, so we are going to need a polyfill. `isomorphic-fetch` is a polyfill that makes it work cross-browsers and in Node too!

- Run `yarn add isomorphic-fetch`

Since we're using `eslint-plugin-compat`, we need to indicate that we are using a polyfill for `fetch` to not get warnings from using it.

- Add the following to your `.eslintrc.json` file:

```json
"settings": {
  "polyfills": ["fetch"]
},
```

### 3 asynchronous actions

`sayHelloAsync` is not going to be a regular action. Asynchronous actions are usually split into 3 actions, which trigger 3 different states: a *request* action (or "loading"), a *success* action, and a *failure* action.

- Edit `src/client/action/hello.js` like so:

```js
// @flow

import 'isomorphic-fetch'

import { createAction } from 'redux-actions'
import { helloEndpointRoute } from '../../shared/routes'

export const SAY_HELLO = 'SAY_HELLO'
export const SAY_HELLO_ASYNC_REQUEST = 'SAY_HELLO_ASYNC_REQUEST'
export const SAY_HELLO_ASYNC_SUCCESS = 'SAY_HELLO_ASYNC_SUCCESS'
export const SAY_HELLO_ASYNC_FAILURE = 'SAY_HELLO_ASYNC_FAILURE'

export const sayHello = createAction(SAY_HELLO)
export const sayHelloAsyncRequest = createAction(SAY_HELLO_ASYNC_REQUEST)
export const sayHelloAsyncSuccess = createAction(SAY_HELLO_ASYNC_SUCCESS)
export const sayHelloAsyncFailure = createAction(SAY_HELLO_ASYNC_FAILURE)

export const sayHelloAsync = (num: number) => (dispatch: Function) => {
  dispatch(sayHelloAsyncRequest())
  return fetch(helloEndpointRoute(num), { method: 'GET' })
    .then((res) => {
      if (!res.ok) throw Error(res.statusText)
      return res.json()
    })
    .then((data) => {
      if (!data.serverMessage) throw Error('No message received')
      dispatch(sayHelloAsyncSuccess(data.serverMessage))
    })
    .catch(() => {
      dispatch(sayHelloAsyncFailure())
    })
}
```

Instead of returning an action, `sayHelloAsync` returns a function which launches the `fetch` call. `fetch` returns a `Promise`, which we use to *dispatch* different actions depending on the current state of our asynchronous call.

### 3 asynchronous action handlers

Let's handle these different actions in `src/client/reducer/hello.js`:

```js
// @flow

import Immutable from 'immutable'
import type { fromJS as Immut } from 'immutable'

import {
  SAY_HELLO,
  SAY_HELLO_ASYNC_REQUEST,
  SAY_HELLO_ASYNC_SUCCESS,
  SAY_HELLO_ASYNC_FAILURE,
} from '../action/hello'

const initialState = Immutable.fromJS({
  message: 'Initial reducer message',
  messageAsync: 'Initial reducer message for async call',
})

const helloReducer = (state: Immut = initialState, action: { type: string, payload: any }) => {
  switch (action.type) {
    case SAY_HELLO:
      return state.set('message', action.payload)
    case SAY_HELLO_ASYNC_REQUEST:
      return state.set('messageAsync', 'Loading...')
    case SAY_HELLO_ASYNC_SUCCESS:
      return state.set('messageAsync', action.payload)
    case SAY_HELLO_ASYNC_FAILURE:
      return state.set('messageAsync', 'No message received, please check your connection')
    default:
      return state
  }
}

export default helloReducer
```

We added a new field to our store, `messageAsync`, and we update it with different messages depending on the action we receive. During `SAY_HELLO_ASYNC_REQUEST`, we show `Loading...`. `SAY_HELLO_ASYNC_SUCCESS` updates `messageAsync` similarly to how `SAY_HELLO` updates `message`. `SAY_HELLO_ASYNC_FAILURE` gives an error message.

### Redux-thunk

In `src/client/action/hello.js`, we made `sayHelloAsync`, an action creator that returns a function. This is actually not a feature that is natively supported by Redux. In order to perform these async actions, we need to extend Redux's functionality with the `redux-thunk` *middleware*.

- Run `yarn add redux-thunk`

- Update your `src/client/index.jsx` file like so:

```js
// @flow

import 'babel-polyfill'

import React from 'react'
import ReactDOM from 'react-dom'
import { AppContainer } from 'react-hot-loader'
import { Provider } from 'react-redux'
import { createStore, combineReducers, applyMiddleware, compose } from 'redux'
import thunkMiddleware from 'redux-thunk'

import App from './app'
import helloReducer from './reducer/hello'
import { APP_CONTAINER_SELECTOR } from '../shared/config'
import { isProd } from '../shared/util'

// eslint-disable-next-line no-underscore-dangle
const composeEnhancers = (isProd ? null : window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__) || compose

const store = createStore(combineReducers({ hello: helloReducer }),
  composeEnhancers(applyMiddleware(thunkMiddleware)))

const rootEl = document.querySelector(APP_CONTAINER_SELECTOR)

const wrapApp = (AppComponent, reduxStore) =>
  <Provider store={reduxStore}>
    <AppContainer>
      <AppComponent />
    </AppContainer>
  </Provider>

ReactDOM.render(wrapApp(App, store), rootEl)

if (module.hot) {
  // flow-disable-next-line
  module.hot.accept('./app', () => {
    // eslint-disable-next-line global-require
    const NextApp = require('./app').default
    ReactDOM.render(wrapApp(NextApp, store), rootEl)
  })
}
```

Here we pass `redux-thunk` to Redux's `applyMiddleware` function. In order for the Redux Devtools to keep working, we also need to use Redux's `compose` function. Don't worry too much about this part, just remember that we enhance Redux with `redux-thunk`.

- Update `src/client/app.jsx` like so:

```js
// @flow

import React from 'react'
import HelloButton from './container/hello-button'
import HelloAsyncButton from './container/hello-async-button'
import Message from './container/message'
import MessageAsync from './container/message-async'
import { APP_NAME } from '../shared/config'

const App = () =>
  <div>
    <h1>{APP_NAME}</h1>
    <Message />
    <HelloButton />
    <MessageAsync />
    <HelloAsyncButton />
  </div>

export default App
```

🏁 Run `yarn start` and `yarn dev:wds` and you should now be able to click the "Say hello asynchronously and send 1234" button and retrieve a corresponding message from the server! Since you're working locally, the call is instantaneous, but if you open the Redux Devtools, you will notice that each click triggers both `SAY_HELLO_ASYNC_REQUEST` and `SAY_HELLO_ASYNC_SUCCESS`, making the message go through the intermediate `Loading...` state as expected.

You can congratulate yourself, that was an intense section! Let's wrap it up with some testing.

## Testing

In this section, we are going to test our actions and reducer. Let's start with the actions.

In order to isolate the logic that is specific to `action/hello.js` we are going to need to *mock* things that don't concern it, and also mock that AJAX `fetch` request which should not trigger an actual AJAX in our tests.

- Run `yarn add --dev redux-mock-store fetch-mock`

- Create a `src/client/action/hello.test.js` file containing:

```js
import fetchMock from 'fetch-mock'
import configureMockStore from 'redux-mock-store'
import thunkMiddleware from 'redux-thunk'

import {
  sayHelloAsync,
  sayHelloAsyncRequest,
  sayHelloAsyncSuccess,
  sayHelloAsyncFailure,
} from './hello'

import { helloEndpointRoute } from '../../shared/routes'

const mockStore = configureMockStore([thunkMiddleware])

afterEach(() => {
  fetchMock.restore()
})

test('sayHelloAsync success', () => {
  fetchMock.get(helloEndpointRoute(666), { serverMessage: 'Async hello success' })
  const store = mockStore()
  return store.dispatch(sayHelloAsync(666))
    .then(() => {
      expect(store.getActions()).toEqual([
        sayHelloAsyncRequest(),
        sayHelloAsyncSuccess('Async hello success'),
      ])
    })
})

test('sayHelloAsync 404', () => {
  fetchMock.get(helloEndpointRoute(666), 404)
  const store = mockStore()
  return store.dispatch(sayHelloAsync(666))
    .then(() => {
      expect(store.getActions()).toEqual([
        sayHelloAsyncRequest(),
        sayHelloAsyncFailure(),
      ])
    })
})

test('sayHelloAsync data error', () => {
  fetchMock.get(helloEndpointRoute(666), {})
  const store = mockStore()
  return store.dispatch(sayHelloAsync(666))
    .then(() => {
      expect(store.getActions()).toEqual([
        sayHelloAsyncRequest(),
        sayHelloAsyncFailure(),
      ])
    })
})
```

Alright, Let's look at what's happening here. First we mock the Redux store using `const mockStore = configureMockStore([thunkMiddleware])`. By doing this we can dispatch actions without them triggering any reducer logic. For each test, we mock `fetch` using `fetchMock.get()` and make it return whatever we want. What we actually test using `expect()` is which series of actions have been dispatched by the store, thanks to the `store.getActions()` function from `redux-mock-store`. After each test we restore the normal behavior of `fetch` with `fetchMock.restore()`.

Let's now test our reducer, which is much easier.

- Create a `src/client/reducer/hello.test.js` file containing:

```js
import {
  sayHello,
  sayHelloAsyncRequest,
  sayHelloAsyncSuccess,
  sayHelloAsyncFailure,
} from '../action/hello'

import helloReducer from './hello'

let helloState

beforeEach(() => {
  helloState = helloReducer(undefined, {})
})

test('handle default', () => {
  expect(helloState.get('message')).toBe('Initial reducer message')
  expect(helloState.get('messageAsync')).toBe('Initial reducer message for async call')
})

test('handle SAY_HELLO', () => {
  helloState = helloReducer(helloState, sayHello('Test'))
  expect(helloState.get('message')).toBe('Test')
})

test('handle SAY_HELLO_ASYNC_REQUEST', () => {
  helloState = helloReducer(helloState, sayHelloAsyncRequest())
  expect(helloState.get('messageAsync')).toBe('Loading...')
})

test('handle SAY_HELLO_ASYNC_SUCCESS', () => {
  helloState = helloReducer(helloState, sayHelloAsyncSuccess('Test async'))
  expect(helloState.get('messageAsync')).toBe('Test async')
})

test('handle SAY_HELLO_ASYNC_FAILURE', () => {
  helloState = helloReducer(helloState, sayHelloAsyncFailure())
  expect(helloState.get('messageAsync')).toBe('No message received, please check your connection')
})
```

Before each test, we initialize `helloState` with the default result of our reducer (the `default` case of our `switch` statement in the reducer, which returns `initialState`). The tests are then very explicit, we just make sure the reducer updates `message` and `messageAsync` correctly depending on which action it received.

🏁 Run `yarn test`. It should be all green.

Next section: [06 - React Router, Server-Side Rendering, Helmet](06-react-router-ssr-helmet.md#readme)

Back to the [previous section](04-webpack-react-hmr.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 06 - React Router, Server-Side Rendering, and Helmet

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/06-react-router-ssr-helmet).

In this chapter we are going to create different pages for our app and make it possible to navigate between them.

## React Router

> 💡 **[React Router](https://reacttraining.com/react-router/)** is a library to navigate between pages in your React app. It can be used on both the client and the server.

React Router has received a major update with its v4 release which is still in beta. Since I want this tutorial to be future-proof, we'll be using v4.

- Run `yarn add react-router@next react-router-dom@next`

On the client side, we first need to wrap our app inside a `BrowserRouter` component.

- Update your `src/client/index.jsx` like so:

```js
// [...]
import { BrowserRouter } from 'react-router-dom'
// [...]
const wrapApp = (AppComponent, reduxStore) =>
  <Provider store={reduxStore}>
    <BrowserRouter>
      <AppContainer>
        <AppComponent />
      </AppContainer>
    </BrowserRouter>
  </Provider>
```

## Pages

Our app will have 4 pages:

- A Home page.
- A Hello page showing a button and message for the synchronous action.
- A Hello Async page showing a button and message for the asynchronous action.
- A 404 "Not Found" page.

- Create a `src/client/component/page/home.jsx` file containing:

```js
// @flow

import React from 'react'

const HomePage = () => <p>Home</p>

export default HomePage
```

- Create a `src/client/component/page/hello.jsx` file containing:

```js
// @flow

import React from 'react'

import HelloButton from '../../container/hello-button'
import Message from '../../container/message'

const HelloPage = () =>
  <div>
    <Message />
    <HelloButton />
  </div>

export default HelloPage

```

- Create a `src/client/component/page/hello-async.jsx` file containing:

```js
// @flow

import React from 'react'

import HelloAsyncButton from '../../container/hello-async-button'
import MessageAsync from '../../container/message-async'

const HelloAsyncPage = () =>
  <div>
    <MessageAsync />
    <HelloAsyncButton />
  </div>

export default HelloAsyncPage
```

- Create a `src/client/component/page/not-found.jsx` file containing:

```js
// @flow

import React from 'react'

const NotFoundPage = () => <p>Page not found</p>

export default NotFoundPage
```

## Navigation

Let's add some routes in the shared config file.

- Edit your `src/shared/routes.js` like so:

```js
// @flow

export const HOME_PAGE_ROUTE = '/'
export const HELLO_PAGE_ROUTE = '/hello'
export const HELLO_ASYNC_PAGE_ROUTE = '/hello-async'
export const NOT_FOUND_DEMO_PAGE_ROUTE = '/404'

export const helloEndpointRoute = (num: ?number) => `/ajax/hello/${num || ':num'}`
```

The `/404` route is just going to be used in a navigation link for the sake of demonstrating what happens when you click on a broken link.

- Create a `src/client/component/nav.jsx` file containing:

```js
// @flow

import React from 'react'
import { NavLink } from 'react-router-dom'
import {
  HOME_PAGE_ROUTE,
  HELLO_PAGE_ROUTE,
  HELLO_ASYNC_PAGE_ROUTE,
  NOT_FOUND_DEMO_PAGE_ROUTE,
} from '../../shared/routes'

const Nav = () =>
  <nav>
    <ul>
      {[
        { route: HOME_PAGE_ROUTE, label: 'Home' },
        { route: HELLO_PAGE_ROUTE, label: 'Say Hello' },
        { route: HELLO_ASYNC_PAGE_ROUTE, label: 'Say Hello Asynchronously' },
        { route: NOT_FOUND_DEMO_PAGE_ROUTE, label: '404 Demo' },
      ].map(link => (
        <li key={link.route}>
          <NavLink to={link.route} activeStyle={{ color: 'limegreen' }} exact>{link.label}</NavLink>
        </li>
      ))}
    </ul>
  </nav>

export default Nav
```

Here we simply create a bunch of `NavLink`s that use the previously declared routes.

- Finally, edit `src/client/app.jsx` like so:

```js
// @flow

import React from 'react'
import { Switch } from 'react-router'
import { Route } from 'react-router-dom'
import { APP_NAME } from '../shared/config'
import Nav from './component/nav'
import HomePage from './component/page/home'
import HelloPage from './component/page/hello'
import HelloAsyncPage from './component/page/hello-async'
import NotFoundPage from './component/page/not-found'
import {
  HOME_PAGE_ROUTE,
  HELLO_PAGE_ROUTE,
  HELLO_ASYNC_PAGE_ROUTE,
} from '../shared/routes'

const App = () =>
  <div>
    <h1>{APP_NAME}</h1>
    <Nav />
    <Switch>
      <Route exact path={HOME_PAGE_ROUTE} render={() => <HomePage />} />
      <Route path={HELLO_PAGE_ROUTE} render={() => <HelloPage />} />
      <Route path={HELLO_ASYNC_PAGE_ROUTE} render={() => <HelloAsyncPage />} />
      <Route component={NotFoundPage} />
    </Switch>
  </div>

export default App
```

🏁 Run `yarn start` and `yarn dev:wds`. Open `http://localhost:8000`, and click on the links to navigate between our different pages. You should see the URL changing dynamically. Switch between different pages and use the back button of your browser to see that the browsing history is working as expected.

Now, let's say you navigated to `http://localhost:8000/hello` this way. Hit the refresh button. You now get a 404, because our Express server only responds to `/`. As you navigated between pages, you were actually only doing it on the client-side. Let's add server-side rendering to the mix to get the expected behavior.

## Server-Side Rendering

> 💡 **Server-Side Rendering** means rendering your app at the initial load of the page instead of relying on JavaScript to render it in the client's browser.

SSR is essential for SEO and provides a better user experience by showing the app to your users right away.

The first thing we're going to do here is to migrate most of our client code to the shared / isomorphic / universal part of our codebase, since the server is now going to render our React app too.

### The big migration to `shared`

- Move all the files located under `client` to `shared`, except `src/client/index.jsx`.

We have to adjust a whole bunch of imports:

- In `src/client/index.jsx`, replace the 3 occurrences of `'./app'` by `'../shared/app'`, and `'./reducer/hello'` by `'../shared/reducer/hello'`

- In `src/shared/app.jsx`, replace `'../shared/routes'` by `'./routes'` and `'../shared/config'` by `'./config'`

- In `src/shared/component/nav.jsx`, replace `'../../shared/routes'` by `'../routes'`

### Server changes

- Create a `src/server/routing.js` file containing:

```js
// @flow

import {
  homePage,
  helloPage,
  helloAsyncPage,
  helloEndpoint,
} from './controller'

import {
  HOME_PAGE_ROUTE,
  HELLO_PAGE_ROUTE,
  HELLO_ASYNC_PAGE_ROUTE,
  helloEndpointRoute,
} from '../shared/routes'

import renderApp from './render-app'

export default (app: Object) => {
  app.get(HOME_PAGE_ROUTE, (req, res) => {
    res.send(renderApp(req.url, homePage()))
  })

  app.get(HELLO_PAGE_ROUTE, (req, res) => {
    res.send(renderApp(req.url, helloPage()))
  })

  app.get(HELLO_ASYNC_PAGE_ROUTE, (req, res) => {
    res.send(renderApp(req.url, helloAsyncPage()))
  })

  app.get(helloEndpointRoute(), (req, res) => {
    res.json(helloEndpoint(req.params.num))
  })

  app.get('/500', () => {
    throw Error('Fake Internal Server Error')
  })

  app.get('*', (req, res) => {
    res.status(404).send(renderApp(req.url))
  })

  // eslint-disable-next-line no-unused-vars
  app.use((err, req, res, next) => {
    // eslint-disable-next-line no-console
    console.error(err.stack)
    res.status(500).send('Something went wrong!')
  })
}
```

This file is where we deal with requests and responses. The calls to business logic are externalized to a different `controller` module.

**Note**: You will find a lot of React Router examples using `*` as the route on the server, leaving the entire routing handling to React Router. Since all requests go through the same function, that makes it inconvenient to implement MVC-style pages. Instead of doing that, we're here explicitly declaring the routes and their dedicated responses, to be able to fetch data from the database and pass it to a given page easily.

- Create a `src/server/controller.js` file containing:

```js
// @flow

export const homePage = () => null

export const helloPage = () => ({
  hello: { message: 'Server-side preloaded message' },
})

export const helloAsyncPage = () => ({
  hello: { messageAsync: 'Server-side preloaded message for async page' },
})

export const helloEndpoint = (num: number) => ({
  serverMessage: `Hello from the server! (received ${num})`,
})
```

Here is our controller. It would typically make business logic and database calls, but in our case we just hard-code some results. Those results are passed back to the `routing` module to be used to initialize our server-side Redux store.

- Create a `src/server/init-store.js` file containing:

```js
// @flow

import Immutable from 'immutable'
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunkMiddleware from 'redux-thunk'

import helloReducer from '../shared/reducer/hello'

const initStore = (plainPartialState: ?Object) => {
  const preloadedState = plainPartialState ? {} : undefined

  if (plainPartialState && plainPartialState.hello) {
    // flow-disable-next-line
    preloadedState.hello = helloReducer(undefined, {})
      .merge(Immutable.fromJS(plainPartialState.hello))
  }

  return createStore(combineReducers({ hello: helloReducer }),
    preloadedState, applyMiddleware(thunkMiddleware))
}

export default initStore
```

The only thing we do here, besides calling `createStore` and applying middleware, is to merge the plain JS object we received from the `controller` into a default Redux state containing Immutable objects.

- Edit `src/server/index.js` like so:

```js
// @flow

import compression from 'compression'
import express from 'express'

import routing from './routing'
import { WEB_PORT, STATIC_PATH } from '../shared/config'
import { isProd } from '../shared/util'

const app = express()

app.use(compression())
app.use(STATIC_PATH, express.static('dist'))
app.use(STATIC_PATH, express.static('public'))

routing(app)

app.listen(WEB_PORT, () => {
  // eslint-disable-next-line no-console
  console.log(`Server running on port ${WEB_PORT} ${isProd ? '(production)' :
    '(development).\nKeep "yarn dev:wds" running in an other terminal'}.`)
})
```

Nothing special here, we just call `routing(app)` instead of implementing routing in this file.

- Rename `src/server/render-app.js` to `src/server/render-app.jsx` and edit it like so:

```js
// @flow

import React from 'react'
import ReactDOMServer from 'react-dom/server'
import { Provider } from 'react-redux'
import { StaticRouter } from 'react-router'

import initStore from './init-store'
import App from './../shared/app'
import { APP_CONTAINER_CLASS, STATIC_PATH, WDS_PORT } from '../shared/config'
import { isProd } from '../shared/util'

const renderApp = (location: string, plainPartialState: ?Object, routerContext: ?Object = {}) => {
  const store = initStore(plainPartialState)
  const appHtml = ReactDOMServer.renderToString(
    <Provider store={store}>
      <StaticRouter location={location} context={routerContext}>
        <App />
      </StaticRouter>
    </Provider>)

  return (
    `<!doctype html>
    <html>
      <head>
        <title>FIX ME</title>
        <link rel="stylesheet" href="${STATIC_PATH}/css/style.css">
      </head>
      <body>
        <div class="${APP_CONTAINER_CLASS}">${appHtml}</div>
        <script>
          window.__PRELOADED_STATE__ = ${JSON.stringify(store.getState())}
        </script>
        <script src="${isProd ? STATIC_PATH : `http://localhost:${WDS_PORT}/dist`}/js/bundle.js"></script>
      </body>
    </html>`
  )
}

export default renderApp
```

`ReactDOMServer.renderToString` is where the magic happens. React will evaluate our entire `shared` `App`, and return a plain string of HTML elements. `Provider` works the same as on the client, but on the server, we wrap our app inside `StaticRouter` instead of `BrowserRouter`. In order to pass the Redux store from the server to the client, we pass it to `window.__PRELOADED_STATE__` which is just some arbitrary variable name.

**Note**: Immutable objects implement the `toJSON()` method which means you can use `JSON.stringify` to turn them into plain JSON strings.

- Edit `src/client/index.jsx` to use that preloaded state:

```js
import Immutable from 'immutable'
// [...]

/* eslint-disable no-underscore-dangle */
const composeEnhancers = (isProd ? null : window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__) || compose
const preloadedState = window.__PRELOADED_STATE__
/* eslint-enable no-underscore-dangle */

const store = createStore(combineReducers(
  { hello: helloReducer }),
  { hello: Immutable.fromJS(preloadedState.hello) },
  composeEnhancers(applyMiddleware(thunkMiddleware)))
```

Here with feed our client-side store with the `preloadedState` that was received from the server.

🏁 You can now run `yarn start` and `yarn dev:wds` and navigate between pages. Refreshing the page on `/hello`, `/hello-async`, and `/404` (or any other URI), should now work correctly. Notice how the `message` and `messageAsync` vary depending on if you navigated to that page from the client or if it comes from server-side rendering.

### React Helmet

> 💡 **[React Helmet](https://github.com/nfl/react-helmet)**: A library to inject content to the `head` of a React app, on both the client and the server.

I purposely made you write `FIX ME` in the title to highlight the fact that even though we are doing server-side rendering, we currently do not fill the `title` tag properly (or any of the tags in `head` that vary depending on the page you're on).

- Run `yarn add react-helmet`

- Edit `src/server/render-app.jsx` like so:

```js
import Helmet from 'react-helmet'
// [...]
const renderApp = (/* [...] */) => {
  // [...]
  const appHtml = ReactDOMServer.renderToString(/* [...] */)
  const head = Helmet.rewind()

  return (
    `<!doctype html>
    <html>
      <head>
        ${head.title}
        ${head.meta}
        <link rel="stylesheet" href="${STATIC_PATH}/css/style.css">
      </head>
    [...]
    `
  )
}
```

React Helmet uses [react-side-effect](https://github.com/gaearon/react-side-effect)'s `rewind` to pull out some data from the rendering of our app, which will soon contain some `<Helmet />` components. Those `<Helmet />` components are where we set the `title` and other `head` details for each page. Note that `Helmet.rewind()` *must* come after `ReactDOMServer.renderToString()`.

- Edit `src/shared/app.jsx` like so:

```js
import Helmet from 'react-helmet'
// [...]
const App = () =>
  <div>
    <Helmet titleTemplate={`%s | ${APP_NAME}`} defaultTitle={APP_NAME} />
    <Nav />
    // [...]
```

- Edit `src/shared/component/page/home.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import { APP_NAME } from '../../config'

const HomePage = () =>
  <div>
    <Helmet
      meta={[
        { name: 'description', content: 'Hello App is an app to say hello' },
        { property: 'og:title', content: APP_NAME },
      ]}
    />
    <h1>{APP_NAME}</h1>
  </div>

export default HomePage

```

- Edit `src/shared/component/page/hello.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import HelloButton from '../../container/hello-button'
import Message from '../../container/message'

const title = 'Hello Page'

const HelloPage = () =>
  <div>
    <Helmet
      title={title}
      meta={[
        { name: 'description', content: 'A page to say hello' },
        { property: 'og:title', content: title },
      ]}
    />
    <h1>{title}</h1>
    <Message />
    <HelloButton />
  </div>

export default HelloPage
```

- Edit `src/shared/component/page/hello-async.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import HelloAsyncButton from '../../container/hello-async-button'
import MessageAsync from '../../container/message-async'

const title = 'Async Hello Page'

const HelloAsyncPage = () =>
  <div>
    <Helmet
      title={title}
      meta={[
        { name: 'description', content: 'A page to say hello asynchronously' },
        { property: 'og:title', content: title },
      ]}
    />
    <h1>{title}</h1>
    <MessageAsync />
    <HelloAsyncButton />
  </div>

export default HelloAsyncPage

```

- Edit `src/shared/component/page/not-found.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

const title = 'Page Not Found'

const NotFoundPage = () =>
  <div>
    <Helmet
      title={title}
      meta={[
        { name: 'description', content: 'A page to say hello' },
        { property: 'og:title', content: title },
      ]}
    />
    <h1>{title}</h1>
  </div>

export default NotFoundPage
```

The `<Helmet>` component doesn't actually render anything, it just injects content in the `head` of your document and exposes the same data to the server.

🏁 Run `yarn start` and `yarn dev:wds` and navigate between pages. The title on your tab should change when you navigate, and it should also stay the same when you refresh the page. Show the source of the page to see how React Helmet sets the `title` and `meta` tags even for server-side rendering.

Next section: [07 - Socket.IO](07-socket-io.md#readme)

Back to the [previous section](05-redux-immutable-fetch.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 07 - Socket.IO

Code for this chapter available [here](https://github.com/verekia/js-stack-walkthrough/tree/master/07-socket-io).

> 💡 **[Socket.IO](https://github.com/socketio/socket.io)** is a library to easily deal with Websockets. It provides a convenient API and fallback for browsers that don't support Websockets.

In this chapter, we are going to set up a basic message exchange between the client and the server. In order to not add more pages and components – which would be unrelated to the core feature we're interested in here – we are going to make this exchange happen in the browser console. No UI stuff in this chapter.

- Run `yarn add socket.io socket.io-client`

## Server-side

- Edit your `src/server/index.js` like so:

```js
// @flow

import compression from 'compression'
import express from 'express'
import { Server } from 'http'
import socketIO from 'socket.io'

import routing from './routing'
import { WEB_PORT, STATIC_PATH } from '../shared/config'
import { isProd } from '../shared/util'
import setUpSocket from './socket'

const app = express()
// flow-disable-next-line
const http = Server(app)
const io = socketIO(http)
setUpSocket(io)

app.use(compression())
app.use(STATIC_PATH, express.static('dist'))
app.use(STATIC_PATH, express.static('public'))

routing(app)

http.listen(WEB_PORT, () => {
  // eslint-disable-next-line no-console
  console.log(`Server running on port ${WEB_PORT} ${isProd ? '(production)' :
    '(development).\nKeep "yarn dev:wds" running in an other terminal'}.`)
})
```

Note that in order for Socket.IO to work, you need to use `Server` from `http` to `listen` to incoming requests, and not the Express `app`. Fortunately, that doesn't change much of the code. All the Websocket details are externalized in a different file, called with `setUpSocket`.

- Add the following constants to `src/shared/config.js`:

```js
export const IO_CONNECT = 'connect'
export const IO_DISCONNECT = 'disconnect'
export const IO_CLIENT_HELLO = 'IO_CLIENT_HELLO'
export const IO_CLIENT_JOIN_ROOM = 'IO_CLIENT_JOIN_ROOM'
export const IO_SERVER_HELLO = 'IO_SERVER_HELLO'
```

These are the *type of messages* your client and your server will exchange. I suggest prefixing them with either `IO_CLIENT` or `IO_SERVER` to make it clearer *who* is sending the message. Otherwise, things can get pretty confusing when you have a lot of message types.

As you can see, we have a `IO_CLIENT_JOIN_ROOM`, because for the sake of demonstration, we are going to make clients join a room (like a chatroom). Rooms are useful to broadcast messages to specific groups of users.

- Create a `src/server/socket.js` file containing:

```js
// @flow

import {
  IO_CONNECT,
  IO_DISCONNECT,
  IO_CLIENT_JOIN_ROOM,
  IO_CLIENT_HELLO,
  IO_SERVER_HELLO,
} from '../shared/config'

/* eslint-disable no-console */
const setUpSocket = (io: Object) => {
  io.on(IO_CONNECT, (socket) => {
    console.log('[socket.io] A client connected.')

    socket.on(IO_CLIENT_JOIN_ROOM, (room) => {
      socket.join(room)
      console.log(`[socket.io] A client joined room ${room}.`)

      io.emit(IO_SERVER_HELLO, 'Hello everyone!')
      io.to(room).emit(IO_SERVER_HELLO, `Hello clients of room ${room}!`)
      socket.emit(IO_SERVER_HELLO, 'Hello you!')
    })

    socket.on(IO_CLIENT_HELLO, (clientMessage) => {
      console.log(`[socket.io] Client: ${clientMessage}`)
    })

    socket.on(IO_DISCONNECT, () => {
      console.log('[socket.io] A client disconnected.')
    })
  })
}
/* eslint-enable no-console */

export default setUpSocket
```

Okay, so in this file, we implement *how our server should react when clients connect and send messages to it*:

- When the client connects, we log it in the server console, and get access to the `socket` object, which we can use to communicate back with that client.
- When a client sends `IO_CLIENT_JOIN_ROOM`, we make it join the `room` it wants. Once it has joined a room, we send 3 demo messages: 1 message to every user, 1 message to users in that room, 1 message to that client only.
- When the client sends `IO_CLIENT_HELLO`, we log its message in the server console.
- When the client disconnects, we log it as well.

## Client-side

The client-side of things is going to look very similar.

- Edit `src/client/index.jsx` like so:

```js
// [...]
import setUpSocket from './socket'

// [at the very end of the file]
setUpSocket(store)
```

As you can see, we pass the Redux store to `setUpSocket`. This way whenever a Websocket message coming from the server should alter the client's Redux state, we can `dispatch` actions. We are not going to `dispatch` anything in this example though.

- Create a `src/client/socket.js` file containing:

```js
// @flow

import socketIOClient from 'socket.io-client'

import {
  IO_CONNECT,
  IO_DISCONNECT,
  IO_CLIENT_HELLO,
  IO_CLIENT_JOIN_ROOM,
  IO_SERVER_HELLO,
  } from '../shared/config'

const socket = socketIOClient(window.location.host)

/* eslint-disable no-console */
// eslint-disable-next-line no-unused-vars
const setUpSocket = (store: Object) => {
  socket.on(IO_CONNECT, () => {
    console.log('[socket.io] Connected.')
    socket.emit(IO_CLIENT_JOIN_ROOM, 'hello-1234')
    socket.emit(IO_CLIENT_HELLO, 'Hello!')
  })

  socket.on(IO_SERVER_HELLO, (serverMessage) => {
    console.log(`[socket.io] Server: ${serverMessage}`)
  })

  socket.on(IO_DISCONNECT, () => {
    console.log('[socket.io] Disconnected.')
  })
}
/* eslint-enable no-console */

export default setUpSocket
```

What happens here should not be surprising if you understood well what we did on the server:

- As soon as the client is connected, we log it in the browser console and join the room `hello-1234` with a `IO_CLIENT_JOIN_ROOM` message.
- We then send `Hello!` with a `IO_CLIENT_HELLO` message.
- If the server sends us a `IO_SERVER_HELLO` message, we log it in the browser console.
- We also log any disconnection.

🏁 Run `yarn start` and `yarn dev:wds`, open `http://localhost:8000`. Then, open your browser console, and also look at the terminal of your Express server. You should see the Websocket communication between your client and server.

Next section: [08 - Bootstrap, JSS](08-bootstrap-jss.md#readme)

Back to the [previous section](06-react-router-ssr-helmet.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 08 - Bootstrap and JSS

Code for this chapter available in the [`master-no-services`](https://github.com/verekia/js-stack-boilerplate/tree/master-no-services) branch of the [JS-Stack-Boilerplate repository](https://github.com/verekia/js-stack-boilerplate).

Alright! It's time to give our ugly app a facelift. We are going to use Twitter Bootstrap to give it some base styles. We'll then add a CSS-in-JS library to add some custom styles.

## Twitter Bootstrap

> 💡 **[Twitter Bootstrap](http://getbootstrap.com/)** is a library of UI components.

There are 2 options to integrate Bootstrap in a React app. Both have their pros and cons:

- Using the official release, **which uses jQuery and Tether** for the behavior of its components.
- Using a third-party library that re-implements all of Bootstrap's components in React, like [React-Bootstrap](https://react-bootstrap.github.io/) or [Reactstrap](https://reactstrap.github.io/).

Third-party libraries provide very convenient React components that dramatically reduce the code bloat compared to the official HTML components, and integrate greatly with your React codebase. That being said, I must say that I am quite reluctant to use them, because they will always be *behind* the official releases (sometimes potentially far behind). They also won't work with Bootstrap themes that implement their own JS. That's a pretty tough drawback considering that one major strength of Bootstrap is its huge community of designers who make beautiful themes.

For this reason, I'm going to make the tradeoff of integrating the official release, alongside with jQuery and Tether. One of the concerns of this approach is the file size of our bundle of course. For your information, the bundle weights about 200KB (Gzipped) with jQuery, Tether, and Bootstrap's JS included. I think that's reasonable, but if that's too much for you, you should probably consider an other option for Bootstrap, or even not using Bootstrap at all.

### Bootstrap's CSS

- Delete `public/css/style.css`

- Run `yarn add bootstrap@4.0.0-alpha.6`

- Copy `bootstrap.min.css` and `bootstrap.min.css.map` from `node_modules/bootstrap/dist/css` to your `public/css` folder.

- Edit `src/server/render-app.jsx` like so:

```html
<link rel="stylesheet" href="${STATIC_PATH}/css/bootstrap.min.css">
```

### Bootstrap's JS with jQuery and Tether

Now that we have Bootstrap's styles loaded on our page, we need the JavaScript behavior for the components.

- Run `yarn add jquery tether`

- Edit `src/client/index.jsx` like so:

```js
import $ from 'jquery'
import Tether from 'tether'

// [right after all your imports]

window.jQuery = $
window.Tether = Tether
require('bootstrap')
```

That will load Bootstrap's JavaScript code.

### Bootstrap Components

Alright, it's time for you to copy-paste a whole bunch of files.

- Edit `src/shared/component/page/hello-async.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import MessageAsync from '../../container/message-async'
import HelloAsyncButton from '../../container/hello-async-button'

const title = 'Async Hello Page'

const HelloAsyncPage = () =>
  <div className="container mt-4">
    <Helmet
      title={title}
      meta={[
        { name: 'description', content: 'A page to say hello asynchronously' },
        { property: 'og:title', content: title },
      ]}
    />
    <div className="row">
      <div className="col-12">
        <h1>{title}</h1>
        <MessageAsync />
        <HelloAsyncButton />
      </div>
    </div>
  </div>

export default HelloAsyncPage
```

- Edit `src/shared/component/page/hello.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import Message from '../../container/message'
import HelloButton from '../../container/hello-button'

const title = 'Hello Page'

const HelloPage = () =>
  <div className="container mt-4">
    <Helmet
      title={title}
      meta={[
        { name: 'description', content: 'A page to say hello' },
        { property: 'og:title', content: title },
      ]}
    />
    <div className="row">
      <div className="col-12">
        <h1>{title}</h1>
        <Message />
        <HelloButton />
      </div>
    </div>
  </div>

export default HelloPage
```

- Edit `src/shared/component/page/home.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'

import ModalExample from '../modal-example'
import { APP_NAME } from '../../config'

const HomePage = () =>
  <div>
    <Helmet
      meta={[
        { name: 'description', content: 'Hello App is an app to say hello' },
        { property: 'og:title', content: APP_NAME },
      ]}
    />
    <div className="jumbotron">
      <div className="container">
        <h1 className="display-3 mb-4">{APP_NAME}</h1>
      </div>
    </div>
    <div className="container">
      <div className="row">
        <div className="col-md-4 mb-4">
          <h3 className="mb-3">Bootstrap</h3>
          <p>
            <button type="button" role="button" data-toggle="modal" data-target=".js-modal-example" className="btn btn-primary">Open Modal</button>
          </p>
        </div>
        <div className="col-md-4 mb-4">
          <h3 className="mb-3">JSS (soon)</h3>
        </div>
        <div className="col-md-4 mb-4">
          <h3 className="mb-3">Websockets</h3>
          <p>Open your browser console.</p>
        </div>
      </div>
    </div>
    <ModalExample />
  </div>

export default HomePage
```

- Edit `src/shared/component/page/not-found.jsx` like so:

```js
// @flow

import React from 'react'
import Helmet from 'react-helmet'
import { Link } from 'react-router-dom'
import { HOME_PAGE_ROUTE } from '../../routes'

const title = 'Page Not Found!'

const NotFoundPage = () =>
  <div className="container mt-4">
    <Helmet title={title} />
    <div className="row">
      <div className="col-12">
        <h1>{title}</h1>
        <div><Link to={HOME_PAGE_ROUTE}>Go to the homepage</Link>.</div>
      </div>
    </div>
  </div>

export default NotFoundPage
```

- Edit `src/shared/component/button.jsx` like so:

```js
// [...]
<button
  onClick={handleClick}
  className="btn btn-primary"
  type="button"
  role="button"
>{label}</button>
// [...]
```

- Create a `src/shared/component/footer.jsx` file containing:

```js
// @flow

import React from 'react'
import { APP_NAME } from '../config'

const Footer = () =>
  <div className="container mt-5">
    <hr />
    <footer>
      <p>© {APP_NAME} 2017</p>
    </footer>
  </div>

export default Footer
```

- Create a `src/shared/component/modal-example.jsx` containing:

```js
// @flow

import React from 'react'

const ModalExample = () =>
  <div className="js-modal-example modal fade">
    <div className="modal-dialog">
      <div className="modal-content">
        <div className="modal-header">
          <h5 className="modal-title">Modal title</h5>
          <button type="button" className="close" data-dismiss="modal">×</button>
        </div>
        <div className="modal-body">
          This is a Bootstrap modal. It uses jQuery.
        </div>
        <div className="modal-footer">
          <button type="button" role="button" className="btn btn-primary" data-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>

export default ModalExample
```

- Edit `src/shared/app.jsx` like so:

```js
const App = () =>
  <div style={{ paddingTop: 54 }}>
```

This is an example of a *React inline style*.

This will translate into: `<div style="padding-top:54px;">` in your DOM. We need this style to push the content under the navigation bar, but that's what's important here. [React inline styles](https://speakerdeck.com/vjeux/react-css-in-js) are a great way to isolate your component's styles from the global CSS namespace, but it comes at a price: You cannot use some native CSS features like `:hover`, Media Queries, animations, or `font-face`. That's [one of the reasons](https://github.com/cssinjs/jss/blob/master/docs/benefits.md#compared-to-inline-styles) we're going to integrate a CSS-in-JS library, JSS, later in this chapter.

- Edit `src/shared/component/nav.jsx` like so:

```js
// @flow

import $ from 'jquery'
import React from 'react'
import { Link, NavLink } from 'react-router-dom'
import { APP_NAME } from '../config'
import {
  HOME_PAGE_ROUTE,
  HELLO_PAGE_ROUTE,
  HELLO_ASYNC_PAGE_ROUTE,
  NOT_FOUND_DEMO_PAGE_ROUTE,
} from '../routes'

const handleNavLinkClick = () => {
  $('body').scrollTop(0)
  $('.js-navbar-collapse').collapse('hide')
}

const Nav = () =>
  <nav className="navbar navbar-toggleable-md navbar-inverse fixed-top bg-inverse">
    <button className="navbar-toggler navbar-toggler-right" type="button" role="button" data-toggle="collapse" data-target=".js-navbar-collapse">
      <span className="navbar-toggler-icon" />
    </button>
    <Link to={HOME_PAGE_ROUTE} className="navbar-brand">{APP_NAME}</Link>
    <div className="js-navbar-collapse collapse navbar-collapse">
      <ul className="navbar-nav mr-auto">
        {[
          { route: HOME_PAGE_ROUTE, label: 'Home' },
          { route: HELLO_PAGE_ROUTE, label: 'Say Hello' },
          { route: HELLO_ASYNC_PAGE_ROUTE, label: 'Say Hello Asynchronously' },
          { route: NOT_FOUND_DEMO_PAGE_ROUTE, label: '404 Demo' },
        ].map(link => (
          <li className="nav-item" key={link.route}>
            <NavLink to={link.route} className="nav-link" activeStyle={{ color: 'white' }} exact onClick={handleNavLinkClick}>{link.label}</NavLink>
          </li>
        ))}
      </ul>
    </div>
  </nav>

export default Nav
```

There is something new here, `handleNavLinkClick`. One issue I encountered using Bootstrap's `navbar` in an SPA is that clicking on a link on mobile does not collapse the menu, and does not scroll back to the top of the page. This is a great opportunity to show you an example of how you would integrate some jQuery / Bootstrap-specific code in your app:

```js
import $ from 'jquery'
// [...]

const handleNavLinkClick = () => {
  $('body').scrollTop(0)
  $('.js-navbar-collapse').collapse('hide')
}

<NavLink /* [...] */ onClick={handleNavLinkClick}>
```

**Note**: I've removed accessibility-related attributes (like `aria` attributes) to make the code more readable *in the context of this tutorial*. **You should absolutely put them back**. Refer to Bootstrap's documentation and code samples to see how to use them.

🏁 Your app should now be entirely styled with Bootstrap.

## The current state of CSS

In 2016, the typical modern JavaScript stack settled. The different libraries and tools this tutorial made you set up are pretty much the *cutting-edge industry standard* (*cough – even though it could become completely outdated in a year from now – cough*). Yes, that's a complex stack to set up, but at least, most front-end devs agree that React-Redux-Webpack is the way to go. Now regarding CSS, I have some pretty bad news. Nothing settled, there is no standard way to go, no standard stack.

SASS, BEM, SMACSS, SUIT, Bass CSS, React Inline Styles, LESS, Styled Components, CSSX, JSS, Radium, Web Components, CSS Modules, OOCSS, Tachyons, Stylus, Atomic CSS, PostCSS, Aphrodite, React Native for Web, and many more that I forget are all different approaches or tools to get the job done. They all do it well, which is the problem, there is no clear winner, it's a big mess.

The cool React kids tend to favor React inline styles, CSS-in-JS, or CSS Modules approaches though, since they integrate really well with React and solve programmatically many [issues](https://speakerdeck.com/vjeux/react-css-in-js) that regular CSS approaches struggle with.

CSS Modules work well, but they don't leverage the power of JavaScript and its many features over CSS. They just provide encapsulation, which is fine, but React inline styles and CSS-in-JS take styling to an other level in my opinion. My personal suggestion would be to use React inline styles for common styles (that's also what you have to use for React Native), and use a CSS-in-JS library for things like `:hover` and media queries.

There are [tons of CSS-in-JS libraries](https://github.com/MicheleBertoli/css-in-js). JSS is a full-featured, well-rounded, and [performant](https://github.com/cssinjs/jss/blob/master/docs/performance.md) one.

## JSS

> 💡 **[JSS](http://cssinjs.org/)** is a CSS-in-JS library to write your styles in JavaScript and inject them into your app.

Now that we have some base template with Bootstrap, let's write some custom CSS. I mentioned earlier that React inline styles could not handle `:hover` and media queries, so we'll show a simple example of this on the homepage using JSS. JSS can be used via `react-jss`, a library that is convenient to use with React components.

- Run `yarn add react-jss`

Add the following to your `.flowconfig` file, as there is currently a Flow [issue](https://github.com/cssinjs/jss/issues/411) with JSS:

```flowconfig
[ignore]
.*/node_modules/jss/.*
```

### Server-side

JSS can render styles on the server for the initial rendering.

- Add the following constants to `src/shared/config.js`:

```js
export const JSS_SSR_CLASS = 'jss-ssr'
export const JSS_SSR_SELECTOR = `.${JSS_SSR_CLASS}`
```

- Edit `src/server/render-app.jsx` like so:

```js
import { SheetsRegistry, SheetsRegistryProvider } from 'react-jss'
// [...]
import { APP_CONTAINER_CLASS, JSS_SSR_CLASS, STATIC_PATH, WDS_PORT } from '../shared/config'
// [...]
const renderApp = (location: string, plainPartialState: ?Object, routerContext: ?Object = {}) => {
  const store = initStore(plainPartialState)
  const sheets = new SheetsRegistry()
  const appHtml = ReactDOMServer.renderToString(
    <Provider store={store}>
      <StaticRouter location={location} context={routerContext}>
        <SheetsRegistryProvider registry={sheets}>
          <App />
        </SheetsRegistryProvider>
      </StaticRouter>
    </Provider>)
  // [...]
      <link rel="stylesheet" href="${STATIC_PATH}/css/bootstrap.min.css">
      <style class="${JSS_SSR_CLASS}">${sheets.toString()}</style>
  // [...]
```

## Client-side

The first thing the client should do after rendering the app client-side, is to get rid of the server-generated JSS styles.

- Add the following to `src/client/index.jsx` after the `ReactDOM.render` calls (before `setUpSocket(store)` for instance):

```js
import { APP_CONTAINER_SELECTOR, JSS_SSR_SELECTOR } from '../shared/config'
// [...]

const jssServerSide = document.querySelector(JSS_SSR_SELECTOR)
// flow-disable-next-line
jssServerSide.parentNode.removeChild(jssServerSide)

setUpSocket(store)
```

Edit `src/shared/component/page/home.jsx` like so:

```js
import injectSheet from 'react-jss'
// [...]
const styles = {
  hoverMe: {
    '&:hover': {
      color: 'red',
    },
  },
  '@media (max-width: 800px)': {
    resizeMe: {
      color: 'red',
    },
  },
  specialButton: {
    composes: ['btn', 'btn-primary'],
    backgroundColor: 'limegreen',
  },
}

const HomePage = ({ classes }: { classes: Object }) =>
  // [...]
  <div className="col-md-4 mb-4">
    <h3 className="mb-3">JSS</h3>
    <p className={classes.hoverMe}>Hover me.</p>
    <p className={classes.resizeMe}>Resize the window.</p>
    <button className={classes.specialButton}>Composition</button>
  </div>
  // [...]

export default injectSheet(styles)(HomePage)
```

Unlike React inline styles, JSS uses classes. You pass styles to `injectSheet` and the CSS classes end up in the props of your component.

🏁 Run `yarn start` and `yarn dev:wds`. Open the homepage. Show the source of the page (not in the inspector) to see that the JSS styles are present in the DOM at the initial render in the `<style class="jss-ssr">` element (only on the Home page). They should be gone in the inspector, replaced by `<style type="text/css" data-jss data-meta="HomePage">`.

**Note**: In production mode, the `data-meta` is obfuscated. Sweet!

If you hover over the "Hover me" label, it should turn red. If you resize your browser window to be narrower than 800px, the "Resize your window" label should turn red. The green button is extending Bootstrap's CSS classes using JSS' `composes` property.

Next section: [09 - Travis, Coveralls, Heroku](09-travis-coveralls-heroku.md#readme)

Back to the [previous section](07-socket-io.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 09 - Travis, Coveralls, and Heroku

Code for this chapter available in the `master` branch of the [JS-Stack-Boilerplate repository](https://github.com/verekia/js-stack-boilerplate).

In this chapter, I integrate our app with third-party services. These services offer free and paid plans. It is a bit controversial to use such services in a tutorial that relies exclusively on community-driven and free open source tools, which is why I maintain 2 different branches of the [JS-Stack-Boilerplate repository](https://github.com/verekia/js-stack-boilerplate), `master` and `master-no-services`.

## Travis

> 💡 **[Travis CI](https://travis-ci.org/)** is a popular continuous integration platform, free for open source projects.

If your project is hosted publicly on Github, integrating Travis is very simple. First, authenticate with your Github account on Travis, and add your repository.

- Then, create a `.travis.yml` file containing:

```yaml
language: node_js
node_js: node
script: yarn test && yarn prod:build
```

Travis will detect automatically that you use Yarn because you have a `yarn.lock` file. Every time you push code to your Github repository, it will run `yarn test && yarn prod:build`. If nothing goes wrong, you should get a green build.

## Coveralls

> 💡 **[Coveralls](https://coveralls.io)** is a service that gives you a history and statistics of your test coverage.

If your project is open-source on Github and compatible with Coveralls' supported Continuous Integration services, the only thing you need to do is to pipe the coverage file generated by Jest to the `coveralls` binary.

- Run `yarn add --dev coveralls`

- Edit your `.travis.yml`'s `script` instruction like so:

```yaml
script: yarn test && yarn prod:build && cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js
```

Now, every time Travis will build, it will automatically submit your Jest test coverage data to Coveralls.

## Badges

Is everything green on Travis and Coveralls? Great, show it off to the world with shiny badges!

You can use the code provided by Travis or Coveralls directly, or use [shields.io](http://shields.io/) to homogenize or customize your badges. Let's use shields.io here.

- Create or edit your `README.md` like so:

```md
[![Build Status](https://img.shields.io/travis/GITHUB-USERNAME/GITHUB-REPO.svg?style=flat-square)](https://travis-ci.org/GITHUB-USERNAME/GITHUB-REPO)
[![Coverage Status](https://img.shields.io/coveralls/GITHUB-USERNAME/GITHUB-REPO.svg?style=flat-square)](https://coveralls.io/github/GITHUB-USERNAME/GITHUB-REPO?branch=master)
```

Of course, replace `GITHUB-USERNAME/GITHUB-REPO` by your actual Github username and repository name.

## Heroku

> 💡 **[Heroku](https://www.heroku.com/)** is a [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) to deploy to. It takes care of infrastructure details, so you can focus on developing your app without worrying about what happens behind the scenes.

This tutorial is not sponsored in any way by Heroku, but Heroku being one hell of a platform, I am going to show you how to deploy your app to it. Yep, that's the kind of free love you get when you build a great product.

**Note**: I might add an AWS section in this chapter later, but one thing at a time.

### Web setup

- If that's not done yet, install the [Heroku CLI](https://devcenter.heroku.com/articles/getting-started-with-nodejs) and log in.

- Go to your [Heroku Dashboard](https://dashboard.heroku.com/) and create 2 apps, one called `your-project` and one called `your-project-staging` for instance.

We are going to let Heroku take care of transpiling our ES6/Flow code with Babel, and generate client bundles with Webpack. But since these are `devDependencies`, Yarn won't install them in a production environment like Heroku. Let's change this behavior with the `NPM_CONFIG_PRODUCTION` env variable.

- In both apps, under Settings > Config Variables, add `NPM_CONFIG_PRODUCTION` set to `false`.

- Create a Pipeline, and grant Heroku access to your Github.

- Add both apps to the pipeline, make the staging one auto-deploy on changes in `master`, and enable Review Apps.

Alright, let's prepare our project for a deployment to Heroku.

### Running in production mode locally

- Create a `.env` file containing:

```.env
NODE_ENV='production'
PORT='8000'
```

That's in this file that you should put your local-only variables and secret variables. Don't commit it to a public repository if your project is private.

- Add `/.env` to your `.gitignore`

- Create a `Procfile` file containing:

```Procfile
web: node lib/server
```

That's where we specify the entry point of our server.

We are not going to use PM2 anymore, we'll use `heroku local` instead to run in production mode locally.

- Run `yarn remove pm2`

- Edit your `prod:start` script in `package.json`:

```json
"prod:start": "heroku local",
```

- Remove `prod:stop` from `package.json`. We don't need it anymore since `heroku local` is a hanging process that we can kill with Ctrl+C, unlike `pm2 start`.

🏁 Run `yarn prod:build` and `yarn prod:start`. It should start your server and show you the logs.

### Deploying to production

- Add the following line to your `scripts` in `package.json`:

```json
"heroku-postbuild": "yarn prod:build",
```

`heroku-postbuild` is a task that will be run every time you deploy an app to Heroku.

You will also probably want to specify a specific version of Node or Yarn for Heroku to use.

- Add this to your `package.json`:

```json
"engines": {
  "node": "7.x",
  "yarn": "0.20.3"
},
```

- Create an `app.json` file containing:

```json
{
  "env": {
    "NPM_CONFIG_PRODUCTION": "false"
  }
}
```

This is for your Review Apps to use.

You should now be all set to use Heroku Pipeline deployments.

🏁 Create a new git branch, make changes and open a Github Pull Request to instantiate a Review App. Check your changes on the Review App URL, and if everything looks good, merge your Pull Request with `master` on Github. A few minutes later, your staging app should have been automatically deployed. Check your changes on the staging app URL, and if everything still looks good, promote staging to production.

You are done! Congratulations if you finished this entire tutorial starting from scratch.

You deserve this emoji medal: 🏅

Back to the [previous section](08-bootstrap-jss.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).

# 09 - Travis, Coveralls, and Heroku

Code for this chapter available in the `master` branch of the [JS-Stack-Boilerplate repository](https://github.com/verekia/js-stack-boilerplate).

In this chapter, I integrate our app with third-party services. These services offer free and paid plans. It is a bit controversial to use such services in a tutorial that relies exclusively on community-driven and free open source tools, which is why I maintain 2 different branches of the [JS-Stack-Boilerplate repository](https://github.com/verekia/js-stack-boilerplate), `master` and `master-no-services`.

## Travis

> 💡 **[Travis CI](https://travis-ci.org/)** is a popular continuous integration platform, free for open source projects.

If your project is hosted publicly on Github, integrating Travis is very simple. First, authenticate with your Github account on Travis, and add your repository.

- Then, create a `.travis.yml` file containing:

```yaml
language: node_js
node_js: node
script: yarn test && yarn prod:build
```

Travis will detect automatically that you use Yarn because you have a `yarn.lock` file. Every time you push code to your Github repository, it will run `yarn test && yarn prod:build`. If nothing goes wrong, you should get a green build.

## Coveralls

> 💡 **[Coveralls](https://coveralls.io)** is a service that gives you a history and statistics of your test coverage.

If your project is open-source on Github and compatible with Coveralls' supported Continuous Integration services, the only thing you need to do is to pipe the coverage file generated by Jest to the `coveralls` binary.

- Run `yarn add --dev coveralls`

- Edit your `.travis.yml`'s `script` instruction like so:

```yaml
script: yarn test && yarn prod:build && cat ./coverage/lcov.info | ./node_modules/coveralls/bin/coveralls.js
```

Now, every time Travis will build, it will automatically submit your Jest test coverage data to Coveralls.

## Badges

Is everything green on Travis and Coveralls? Great, show it off to the world with shiny badges!

You can use the code provided by Travis or Coveralls directly, or use [shields.io](http://shields.io/) to homogenize or customize your badges. Let's use shields.io here.

- Create or edit your `README.md` like so:

```md
[![Build Status](https://img.shields.io/travis/GITHUB-USERNAME/GITHUB-REPO.svg?style=flat-square)](https://travis-ci.org/GITHUB-USERNAME/GITHUB-REPO)
[![Coverage Status](https://img.shields.io/coveralls/GITHUB-USERNAME/GITHUB-REPO.svg?style=flat-square)](https://coveralls.io/github/GITHUB-USERNAME/GITHUB-REPO?branch=master)
```

Of course, replace `GITHUB-USERNAME/GITHUB-REPO` by your actual Github username and repository name.

## Heroku

> 💡 **[Heroku](https://www.heroku.com/)** is a [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) to deploy to. It takes care of infrastructure details, so you can focus on developing your app without worrying about what happens behind the scenes.

This tutorial is not sponsored in any way by Heroku, but Heroku being one hell of a platform, I am going to show you how to deploy your app to it. Yep, that's the kind of free love you get when you build a great product.

**Note**: I might add an AWS section in this chapter later, but one thing at a time.

### Web setup

- If that's not done yet, install the [Heroku CLI](https://devcenter.heroku.com/articles/getting-started-with-nodejs) and log in.

- Go to your [Heroku Dashboard](https://dashboard.heroku.com/) and create 2 apps, one called `your-project` and one called `your-project-staging` for instance.

We are going to let Heroku take care of transpiling our ES6/Flow code with Babel, and generate client bundles with Webpack. But since these are `devDependencies`, Yarn won't install them in a production environment like Heroku. Let's change this behavior with the `NPM_CONFIG_PRODUCTION` env variable.

- In both apps, under Settings > Config Variables, add `NPM_CONFIG_PRODUCTION` set to `false`.

- Create a Pipeline, and grant Heroku access to your Github.

- Add both apps to the pipeline, make the staging one auto-deploy on changes in `master`, and enable Review Apps.

Alright, let's prepare our project for a deployment to Heroku.

### Running in production mode locally

- Create a `.env` file containing:

```.env
NODE_ENV='production'
PORT='8000'
```

That's in this file that you should put your local-only variables and secret variables. Don't commit it to a public repository if your project is private.

- Add `/.env` to your `.gitignore`

- Create a `Procfile` file containing:

```Procfile
web: node lib/server
```

That's where we specify the entry point of our server.

We are not going to use PM2 anymore, we'll use `heroku local` instead to run in production mode locally.

- Run `yarn remove pm2`

- Edit your `prod:start` script in `package.json`:

```json
"prod:start": "heroku local",
```

- Remove `prod:stop` from `package.json`. We don't need it anymore since `heroku local` is a hanging process that we can kill with Ctrl+C, unlike `pm2 start`.

🏁 Run `yarn prod:build` and `yarn prod:start`. It should start your server and show you the logs.

### Deploying to production

- Add the following line to your `scripts` in `package.json`:

```json
"heroku-postbuild": "yarn prod:build",
```

`heroku-postbuild` is a task that will be run every time you deploy an app to Heroku.

You will also probably want to specify a specific version of Node or Yarn for Heroku to use.

- Add this to your `package.json`:

```json
"engines": {
  "node": "7.x",
  "yarn": "0.20.3"
},
```

- Create an `app.json` file containing:

```json
{
  "env": {
    "NPM_CONFIG_PRODUCTION": "false"
  }
}
```

This is for your Review Apps to use.

You should now be all set to use Heroku Pipeline deployments.

🏁 Create a new git branch, make changes and open a Github Pull Request to instantiate a Review App. Check your changes on the Review App URL, and if everything looks good, merge your Pull Request with `master` on Github. A few minutes later, your staging app should have been automatically deployed. Check your changes on the staging app URL, and if everything still looks good, promote staging to production.

You are done! Congratulations if you finished this entire tutorial starting from scratch.

You deserve this emoji medal: 🏅

Back to the [previous section](08-bootstrap-jss.md#readme) or the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).
