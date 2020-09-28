# React + Express Starter Pack

## A minimal (but still batteries included) React starter setup for building web apps that require a Node/Express backend

### Latest Version 1.1.0

Added ability to make https requests in development

Added clean-webpack-plugin

### We’ll first add Babel 7 to the project, and the presets that we’ll need for ES6 and JSX.

`yarn add @babel/core @babel/preset-react @babel/preset-env` After we installed babel, we may need
to add basic configuration for it in .babelrc file (in our root folder)

`// .babelrc { "presets": ["@babel/preset-react", "@babel/preset-env"] }`

Now that we have our transpiler for JavaScript and React, we are able to add Webpack. It’s a module
bundler that will basically create a dependency graph in the project and spit a packaged JavaScript
file that we’ll attach to our index html.
`yarn add webpack webpack-cli babel-loader webpack-dev-server`

We will also add all of the bits we need for Webpack to be able to different file types:
`yarn add --dev css-loader style-loader file-loader html-webpack-plugin clean-webpack-plugin`

We installed Webpack and some dependencies we’ll need for building our React app. Babel-loader is
basically a bridge between webpack and babel and webpack dev server is a helpful plugin for creating
dev bundles really quick.

### Configuring webpack

As we made with babel, we need to create a configuration file. In most mature projects I’ve seen,
more than one webpack configuration is needed (for dev and for production). This is because
production bundles are normally optimized bundles that are hard to read and dev bundles can be read
by developers. The following code snipper was created in the root folder with the name
webpack.config.js

If you run npm run build or yarn build, you’ll see that there’s a production bundle made in dist
folder. If you run `npm run start` or `yarn start`, a server will be created for serving our files.
The ‘hot’ flag (which can be seen in the "scripts" in **package.json** indicate that the bundle will
be autogenerated after we change something in our app. ‘Open’ flag will automatically open a browser
tab in localhost:8080 which is the default webpack dev host and port.

### Using CSS-In-JS

We have opted for @emotion/core here as it has a smaller footprint than styled-components and I
prefer the syntax it uses. As well as installing it with `yarn add @emotion/core`, we also need to
`yarn add "@emotion/babel-preset-css-prop"` in order for emotion's jsx calls to be handled properly.
Once installed, we then need to update our **.babelrc** file, which should now look like this:

```
// .babelrc
{
  "presets": ["@babel/preset-react", "@babel/preset-env", "@emotion/babel-preset-css-prop"]
}
```

See https://emotion.sh/docs/css-prop for more info.

### Production

Run `yarn build` to create a production build of your app. This will automatically bundle everything
and save it to a 'build' folder in the root of your project.

### Express/Node additions inspired by/lifted from https://github.com/crsandeep/simple-react-full-stack

### Enabling https when working locally

Inside of src/server/index.js, there's a bunch of things going on (and also a step you need to take
to get everything working). You'll notice in there a link to letsencrypt. You don't need to visit
the site but further instructions/explanation is available there if so required. You'll see in the
file that there's a chunk of text commented out. You need to open up a terminal inside the root of
your project directory and simply copy and paste all of that code. It'll create two files in the
root of your directory. These are basically certificates in order to be able to make https requests
locally. These should not be included in your repo if you decide to upload anything to GitHub ot
elsewhere. Therefore, the default names are inside of .gitignore, and you will have to create them
if you decide to pull the repo down again. You should also not aim to keep a copy of those files
anywhere where access could be jeopardised. Everything else is set up to make use of them with their
existing names.
