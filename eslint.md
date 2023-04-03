#  **what is ESLint**

[ESLint](https://www.npmjs.com/package/eslint) is a popular open-source tool for JavaScript code analysis that helps developers identify and fix issues in their code. It works by analyzing code syntax, detecting potential errors, and enforcing coding standards and best practices.

# **Install and setup ESLint**

React Native 0.63.4 (at the moment of this writing) comes with a predefined eslint config, but we'll remove that package because we'll create our own config.

`` 
npm uninstall @react-native-community/eslint-config 
``

React Native 0.63.4 (at the moment of this writing) doesn't come with the latest eslint version, so we'll simply uninstall it and then install it again to pull the latest version.

<pre>
 npm uninstall eslint
</pre>
install the latest eslint package version.

<pre> npm install eslint --save-dev </pre>

set up a configuration file for eslint. This command will ask you a few questions. Here's a list of them, and the answers we'll need to choose (✔ and ❯ symbols indicate the selected answers)

<pre> npx eslint --init </pre>

# **Question 1:**

   ``` How would you like to use ESLint? ``` <Br> 
    To check syntax only <Br>
     To check syntax and find problems <Br> 
    **❯To check syntax, find problems, and enforce code style**


# **question 2:**

```What type of modules does your project use?``` <Br>

**❯JavaScript modules (import/export)<Br>**
  CommonJS (require/exports)<Br>
  None of these

# **question 3:**

```Which framework does your project use?```<Br>
**❯ React** <Br>
Vue.js <Br>
None of thes <Br>

# **question 4**

```Does your project use TypeScript?```<Br>
No /**❯Yes**

(if you want to add typescript in your project then select YES else NO):

# ***question 5:***

``` Where does your code run?```<Br>
Browser<Br>
**✔ Node**
# **question 6:**
```How would you like to define a style for your project?```

**❯ Use a popular style guide**<Br>
Answer questions about your style<Br>
Inspect your JavaScript file(s)<Br>

# **question 7 (we'll rely on Airbnb's JavaScript style guide here):**

```Which style guide do you want to follow?```<Br>
❯ [Airbnb](https://github.com/airbnb/javascript)<Br>
[Standard](https://github.com/standard/standard)<Br>
[Google](https://github.com/google/eslint-config-google)

# **question 8:**

```What format do you want your config file to be in?```

JavaScript<Br>
YAML<Br>
❯ **JSON**

### **The final prompt here is where eslint will ask you if you want to install all the necessary dependencies. Select "Yes" and hit enter:**

```Would you like to install them now with npm?```<Br>
No / **›Yes**

As a result, you'll end up having a ```.eslintrc.json``` file in the root of your project, which looks like so (we'll modify it a little bit later on):

<pre> 
{
    "env": {
        "es2021": true,
        "node": true,
    },
    "extends": [
        "plugin:react/recommended",
        "airbnb"
    ],
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "plugins": [
        "react"
    ],
    "rules": {
    }
}

</pre>

 NOTE: 
 ```+ React Native comes (at the moment of this writing) with a .eslintrc.js config, and if that's still the case for you, then simply remove it, since we'll use the JSON format of that config.```

 [React Hooks](https://legacy.reactjs.org/docs/hooks-intro.html) are pretty popular at this point and most likely every new React Native project will make use of them, so let's add the recommended ESLint rules for hooks. For that, update the extends section of your .eslintrc.json file like so:

 <pre>
 {
    //...
    "extends": [
        "plugin:react/recommended",
        "airbnb",
        "airbnb/hooks"
    ],
    //...
}
</pre>

```npm install --save-dev eslint-plugin-react-native``` - add support for [React Native specific ESLint rules.](https://www.npmjs.com/package/eslint-plugin-react-native#list-of-supported-rules) After installing this package, update the plugins section of your .```eslintrc.json``` file like so:

```{
    //...
    "plugins": [
        "react",
        "react-native"
    ],
    //...
}

```
Create a ```.eslintignore``` file in the root on your project to tell ESLint to ignore specific files and directories, and then add the following contents:

<pre>node_modules/ </pre>

In our case, we simply want to ignore the node_modules folder from being linted.
Last step here, is to configure your code editor to lint the code for you. If you're a [VS Code](https://code.visualstudio.com/) user, simply install the [ESLint VS Code extension.](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) .The only ESLint configuration you need to add to your VS Code settings is the following:

<pre>
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
</pre>

NOTE:
```+ You may want to add these VS Code settings as  Workspace settings instead of User settings, meaning that they will only apply to this specific project and not to any project  you'll open in VS Code. Read more on the VS  Code Documentation page.```<Br>
[VS Code Documentation](https://code.visualstudio.com/docs/getstarted/settings)

# **Steps** 

You can add this configuration in VS Code by following these steps:

Open VS Code
Press ```Ctrl + ,``` or click on the gear icon at the bottom of the left-hand side bar to open the Settings menu.
In the search bar at the top of the Settings menu, type **"codeActionsOnSave"** to find the relevant setting.
Click on ```Edit in settings.json``` to open your VS Code settings file.


Overall, this configuration file helps ensure that your code adheres to best practices and avoids common issues.

**Now let's break down each part of this configuration file:**

 <pre>
  {
  "env": {
    "es2021": true,
    "node": true,
    "react-native/react-native": true
    },
 </pre>



This section specifies the environment in which the code will run. It declares that the code will run on ES2021, Node.js, and React Native.

<pre>
  "globals": {
    "JSX": "readonly"
  },
  </pre>

  This section specifies global variables that are used throughout the code, such as JSX. By setting "readonly", it prevents these global variables from being reassigned

  <pre>
   "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "prettier",
    "plugin:react-native/all",
    "plugin:@typescript-eslint/recommended",
    "airbnb",
    "airbnb/hooks"
  ],
  </pre>
  <Br>

This section extends the default rules provided by ESLint and adds additional rules from various plugins. The eslint:recommended and plugin:react/recommended rules provide recommended rules for JavaScript and React, respectively. The prettier rule configures ESLint to work well with the Prettier code formatting tool. The plugin:react-native/all rule provides recommended rules for React Native development. The plugin:@typescript-eslint/recommended rule provides recommended rules for TypeScript development. Finally, the airbnb and airbnb/hooks rules provide a set of opinionated rules for code style.
<Br>

<pre>
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
</pre>
<Br>

This section specifies the parser options for ESLint. It enables JSX parsing, sets the ECMAScript version to 12, and specifies that the code is written in modules.

<pre>
  "plugins": ["react", "react-native", "@typescript-eslint"],
  </pre>

  This section specifies the plugins to be used with ESLint. The react, react-native, and @typescript-eslint plugins are included.

  <pre>

    "settings": {
    "react": {
      "version": "detect"
    }
  },
  </pre>

  This section specifies settings for the react plugin. It tells ESLint to detect the version of React being used in the code.

  <pre>
   "rules": {
    "semi": ["error", "always"],
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx", ".ts", ".tsx"] }],
    "no-use-before-define": ["error", { "variables": false }],
    "react/prop-types": ["error", { "ignore": ["navigation", "navigation.navigate"] }]
  }
}</pre>

This section specifies the rules that ESLint will enforce. For example, the semi rule enforces the use of semicolons at the end of each statement, and the react/jsx-filename-extension rule enforces the use of .js, .jsx, .ts, or .tsx file extensions for files that contain JSX code. The no-use-before-define rule prevents the use of variables before they are defined, and the react/prop-types rule enforces the use of propTypes for React components, except for the navigation and navigation.navigate props.


# **What mean by propTypes for React components**

<pre>
import React from 'react';
import PropTypes from 'prop-types';

function Greeting(props) {
  return console.log(Hello, {props.name}!);
}

Greeting.propTypes = {
  name: PropTypes.string.isRequired
};

export default Greeting;</pre>

In this example, we have a simple component called Greeting that takes a name prop and displays a greeting message. We import the PropTypes library and then use it to define the expected type of the name prop. The PropTypes.string tells React that we expect the name prop to be a string, and the isRequired property specifies that the name prop is mandatory.

# **Install and setup Prettier**

```npm install --save-dev --save-exact prettier``` add the prettier package as a dev dependency to your project. We'll also install and use the [Prettier VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) later on, which already comes with Prettier package bundled in, but in general it's a good practice to add the npm package to your project directly as well, just in case some people won't use VS Code as their code editor of choice.

```npm install --save-dev eslint-config-prettier``` we'll use Prettier for code formatting concerns, and ESLint for code-quality concerns, so we need to turns off all ESLint rules that are unnecessary or might conflict with Prettier. Once the package has been installed, we need to update the extends section of your .eslintrc.json file like so:

<pre>
{
    //...
    "extends": [
        "plugin:react/recommended",
        "airbnb",
        "airbnb/hooks",
        "prettier",
        "prettier/react"
    ],
    //...
}
</pre>

Create a ```.prettierrc.json``` configuration file in the root of your project with the following options:

<pre>
{
    "arrowParens": "always",
    "bracketSpacing": true,
    "jsxBracketSameLine": false,
    "jsxSingleQuote": false,
    "quoteProps": "as-needed",
    "singleQuote": true,
    "semi": true,
    "printWidth": 100,
    "useTabs": false,
    "tabWidth": 2,
    "trailingComma": "es5"
}
</pre>

For more Prettier configuration options and an explanation of what each option does, see Prettier [Documentation](https://prettier.io/docs/en/options.html).

## **NOTE**:

```+ React Native comes (at the moment of this writing) with a .prettierrc config already, and if that's still the case for you, then you can still use that config file instead of creating a new .prettierrc.json one. They both use the JSON format for specifying configuration options. ```

Last step here, is to configure your code editor to format your code using Prettier. If you're a VS Code user, simply install the [Prettier VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode). After the extension has been installed, add the following settings to your VS Code JSON config:

<pre>
{
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
}
</pre>

# **same Steps we done before**

You can add this configuration in VS Code by following these steps:

Open VS Code
Press ```Ctrl + ,``` or click on the gear icon at the bottom of the left-hand side bar to open the Settings menu.
In the search bar at the top of the Settings menu, type "**codeActionsOnSave**" to find the relevant setting.
Click on "```Edit in settings.json```" to open your VS Code settings file.






