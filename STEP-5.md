# Step 5 - Webpack Mode

from class notes: 

Changes proposed for the Configuration Files

Create a copy of the webpack.config.js, and rename it as webpack.prod.js. This file should have mode: 'production' statement in module.exports.
Now, rename the webpack.config.js to webpack.dev.js. This file should have the following statements in module.exports

     mode: 'development',
     devtool: 'source-map',

Changes proposed for package.json

The statements added to the package.json for the configuration files of production and development modes separately in the "script" block are:

    "scripts": {
        "build-prod": "webpack --config webpack.prod.js",
        "build-dev": "webpack-dev-server  --config webpack.dev.js --open"
    },

Note that you should remove the "build": "webpack" script now from package.json, and only have the two related to build-dev and build-prod. This also means when you build your app with npm, you should use the correct script, e.g.

    npm run build-dev



In Webpack, there are two ways you can set the environment mode:

## #1. Through the CLI

```
webpack --mode=production
```

## #2. In the config

```
module.exports = {
  mode: 'production'
};
```

Projects will use either one. If using the CLI flag, you can create conditional statements in your webpack config that check the environment before adding a setting, like this:

```
if (argv.mode === 'development') {
    config.devtool = 'source-map';
  }
```

If you choose option 2 and declare mode in the webpack config, then you’ll have two webpack config files - one for dev and one for prod. 

From what I have seen, option 2 is a bit more common. And that is the way we’ll go.

Go ahead a rename the webpack config file we have to webpack.dev.js and create a new one, also at root, called webpack.prod.js. 

Add the correct mode flag to each one:

```
mode: "development"/"production"
```

We also have to edit our npm script to use the correct files we run npm build. Your scripts will look like this:

```
    "build-prod": "--config webpack.prod.js",
    "build-dev": "--config webpack.prod.js"
```

to build now you have to use: 

    npm run build-dev