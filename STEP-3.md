## my notes:
It might seem strange that we have to add ANOTHER library before we’re even finished setting up the first library - but believe me, that’s how it goes. Babel itself is also not an easy tool to use necessarily, it requires a bit of setup but it is widely used throughout the javascript world to translate new ES syntax into vanilla js that can run on browsers etc. They describe their tool like this:

Babel is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments.

Once you have the hang of this setup, I have personally found it helpful to have babel even on projects that don’t have Webpack. Sometimes I’ll install it just for the convenience … like the convenience of no semicolons or being able to use import/export syntax.

First off, we need to install Babel via npm. Babel occasionally changes its install requirements, but at the moment these are the configurations that work and seem to be pretty stable:

    npm i -D @babel/core @babel/preset-env babel-loader

Remember that the -D will install these as development dependencies.

And now, just like webpack, babel also requires a config file. In this case, it is a fairly simple one.

Create a new file .babelrc in the root of the project. Fill it with this code:

    { ‘presets’: ['@babel/preset-env'] }

Now, we’re about to go through a whole rigamarole of settings, these aren’t the kind of settings I would commit to memory necessarily, but I will try to explain the steps as we go along.

First, we have both webpack and babel installed, now we have to get webpack to use babel. Doing that forces us to use a part of webpack we haven’t explained yet - we will explain them I promise - but that would jump us just a little ahead of where we are, so for now, you can copy and paste this part. We will observe what it does and then circle back around to explain it.

So, back we go to the webpack config, because we have some things to add.

First, we could specify the “output” of our webpack config, it would look something like this:

    output: { ...output options }

But at the moment, we don’t need to add any custom settings there. The default settings are good enough for us - creating a dist folder in the root of our project.

So, output is set, but there’s still the matter of getting webpack to use babel. For that we’ll use a webpack loader. Loaders are what we will circle back around to in a second, but for now, add this to your webpack config.

    module: {
            rules: [
                    {
                test: '/\.js$/',
                exclude: /node_modules/,
                loader: "babel-loader"
                    }
            ]
    }

Now, with that loader in place, we should be able to get going.

Go to your index.js file and import our two javascript files (also make sure you export them in the original files!). Then console log one of the functions. Here is an example:

    import { checkForName } from './js/nameChecker'
    import { handleSubmit } from './js/formHandler'
    
    console.log(checkForName);
    
    alert("I EXIST")

Really we don’t need the alert any more, but either way, delete the current distribution folder and rerun the build command. 

Babel is a javascript library that allows us to:

Use the latest version of javascript, even if our browser or runtime doesn't allow it

# Step 3 - Webpack Output

The “output” of webpack is the distribution folder. It is where webpack drops or “outputs” the neat bundles of assets it creates from the individual files we point it to.

We have setup webpack just enough to be performing the most basic function of webpack - creating a dist folder with a main.js file from our entry point. And all of that is great - but none of it is useful yet.

What’s wrong? Let’s take a look:

- The main.js file of our distribution folder contains none of the javascript or other assets we wrote for our webpage.
- The distribution folder has no connection whatsoever to our app. If you start the express server, our app is still functioning exactly the same way it did in part 0.

1. Add our client/js file contents into dist/main.js


2. Create a new index.js file at the address above. For now, it can be mostly empty, with just an alert.




**You have been successful when you see a dist folder in the root of your app**

*Some miscellanious notes:*

- If you run webpack build and in your text editor you see the dist folder, but nothing inside it - it might still be working. Some text editors will hide folders or folder contents like ```dist```. Yeah... that one didn't have me second guessing myself for like 20 min...


