# Step 6 - Adding Convenience in Webpack

my notes:

hard reloading

    npm i -D webpack-dev-server
    
we changed the `package.json` and `webpack.dev.js` which are already reflected in the code

then we run 

    npm run build-dev


Up next, have you noticed how we often have to remove the dist folder manually before re-running the build script? From what I have seen, when you rebuild, new code will be added to the bundled files, but if there was old code that you got rid of, webpack build does not remove the old stuff. So, we have been removing the dist folder via the terminal and before rebuilding.

Really though, that is an extra and unnecessary step. If we wanted to go really low tech, we could just edit our build script:

rm -rf dist && webpack-dev-server  --config webpack.dev.js --open

And there’s really nothing wrong with that. Honestly, being comfortable customizing your npm scripts will make so many things easier. But, it is doing a little bit of extra work. That script blindly deletes everything and then rebuilds it, even if 99% of the code remained the same.

To be a little more efficient, there is a webpack plugin called Clean. From its documentation:

    By default, this plugin will remove all files inside webpack's output.path directory, as well as all unused webpack assets after every successful rebuild.

Now, some people will choose to go with the simpler blanket dist folder delete, but just to try it, lets install the clean plugin.

npm i -D clean-webpack-plugin

Then, as we learned before, to make webpack use a plugin, we have to do two things:

Add a require statement to the top of the webpack config file:

const { CleanWebpackPlugin } = require('clean-webpack-plugin');

Add the plugin to Plugins array in the module.exports. The clean plugin is a good example of a plugin that allows for various options. Take a look at this:

We could use CleanWebpackPlugin like this:

    new CleanWebpackPlugin()

And the above would function. When there are no options passed in, a plugin will run all the default settings, but we can also pass in our custom selections of the various plugin options, like this:

        new CleanWebpackPlugin({
                // Simulate the removal of files
                dry: true,
                // Write Logs to Console
                verbose: true,
                // Automatically remove all unused webpack assets on rebuild
                cleanStaleWebpackAssets: true,
                protectWebpackAssets: false
        })

You can’t know what options a plugin allows without reading the documentation for that plugin.

Add that code to your wepack.dev.js file and rerun the build script, now you’ll see a few lines added to the webpack output that tell you the clean plugin is functioning.


i also tried 

    npm install --save-dev webpack-bundle-analyzer  


This section has three commits, they add the following webpack tools and configurations for a better development environment:

- The webpack dev server (commit 1)
- The Clean webpack plugin (commit 2)
- Light intro to Webpack Debugging tools (commit 3)

## IMPORTANT
**Please note that checking out the code at commit 3 will have errors in it. Errors were intentionally added for commit 3 to play around with various debugging settings.**
