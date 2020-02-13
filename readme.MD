# Creating a configuration file.

In your last lesson we created **Webpack environment** which needed **no configuration**. In this lesson we are going to create a webpack configuration file which will **minify** and **write** out our HTML to the **dist folder**, in conjunction we will configure a dev server.

## Installing packages
The **html-webpack-plugin** plugin bundles html and writes it out to a dest folder. You can find more information about the plugin here: 

https://www.npmjs.com/package/html-webpack-plugin



The **html-loader** plugin converts HTML into string so JavaScript may parse it. Additional information can be found here:

https://www.npmjs.com/package/html-loader

While cd’ed into your project please run the following command:


**npm i -D html-webpack-plugin html-loader**

# Creating a webpack.config.js file

In the root of your folder create a file called **webpack.config.js.** We are going to configure the **plugins** which we just installed.

```javascript
const htmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    module: {
        rules: [
            {
                test: /\.html$/,
                use: [
                        {
                            loader: "html-loader",
                            options: { minimize: true } 
                        }
                ]
            }
        ]
    },
    plugins: [
        new htmlWebpackPlugin({
            template: './src/index.html',
            filename: './index.html'
        })
    ]
}
```

We require the **html-webpack-plugin**, we will configure this later. We create a **module and export** it so other parts of the application can use it. We will create an **object which will be configured** with certain keys and values.


The **rules key** takes an **array** as a value. The object inside the array configures the **html-loader plugin.** The **test key** uses regex to look for **all html files** inside our **src folder**.

The plugin will convert this to a **string.** The loader key is set to a value of html-loader plugin. We can also add options for this plugin. **In this case we will minify our HTML**, hence we set the minimize value to true.


## Configuring the plugins key

The plugins key will take in an **array** as a value. We configure an array because it is unlikely that we will only use one plugin. We create a **new instance** of the **html-webpack-plugin**. This takes an object as the argument. The template configuration takes a **path** in. This **path** tells webpack where to look for **html files**. The filename key lets webpack know what to name the file.

**Remove the following line of code from your index.html file:**

```html
<script src="./../dist/main.js"></script>
```

Run the command: **npm run build**

Look at the **index.html** file inside your dist folder. Although it is **minified**, you can see that it linked the **main.js** file from the **dist** inside your **html**.

##Installing a dev server

**Webpack** has a plugin which can create a **server** for us, it can also **hot-reload browsers** with code changes.

To install the plugin run the following command: **npm i -D webpack-dev-server**

## Configuring the package.json file to run a server

```json
{
  "name": "myFirstAutomatedProject",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "build": "webpack",
    "dev": "webpack-dev-server"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "webpack": "^4.41.6",
    "webpack-cli": "^3.3.11",
    "webpack-dev-server": "^3.10.3"
  }
}
```

In your **scripts object** create another key called **dev** and give it a value of **webpack-dev-server**. This script tells node, that if we run the command **npm run dev**  launch the **webpack-dev-server**.

Run the command: **npm run dev**
While you are cd’ed inside the myFirstAutomatedProject folder. Open the following URL: **http://localhost:8080/** in your browser.

Edit the **HTML and JS** and watch the plugin work. You have now configured webpack to create a dev server and work with HTML.
