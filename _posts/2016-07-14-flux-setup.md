---
layout: post
title: "On my set up of Flux architecture"
date: 2016-07-14
author: Wu Lei
categories: Article
tags: JavaScript
---

### On my set up of Flux architecture

Since learning the React JS front-end library, having a good control of a web application on the data flow, especially when it becomes more and more complex is in demand. 

Even though there are many articles including the official document providing those tutorials on how to build this architecture for some specific application, I still find it a little difficult to follow most of them. Until I followed a [demo](https://www.youtube.com/watch?v=LCaH1siSzW4) of this on Youtube. 

Fortunately or not, this is the few if not only tutorial that actually works for me. I forked it [here](https://github.com/znss1989/template_flux), having it just touched up a bit on my own. It is the template project for a typical ReactJS project developed using the Flux architecture. Again, this whole thing is borrowed from bradtraversy/fluxboiler.

To use this template, 1. Clone to current project 2.  npm install  3.  gulp 

The package.json file is displayed here.

```
{
  "name": "learn-react-flux",
  "version": "1.0.0",
  "description": "Learn ReactJS with Flux architecture with production workflow.",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Wu Lei",
  "license": "ISC",
  "devDependencies": {
    "browserify": "*",
    "flux": "*",
    "gulp": "*",
    "reactify": "*",
    "vinyl-source-stream": "*",
    "object-assign": "*"
  },
  "dependencies": {
    "react": "^0.14.7",
    "react-dom": "^0.14.7"
  }
}
```

A little explaination goes here for the set up process. 

First, Browserify lets you require('modules') in the browser by bundling up all of your dependencies. Flux is included for the architecture, providing the dispatcher and something else. Then gulp is added as the task runner, which can be seen from the gulpfile.js file. Since most likely we are to use the so-called JSX syntax for a ReactJS component for a app, the module reactify is added for transforming the JSX into plain JavaScript format. The vinyl-source-stream transforms strings into data streams that gulp can handle for pipelining. Last, the object-assign are needed in the store portion of the architecture. 

React and React-dom are added for dependency then. That's done I suppose.

I heard that babelify is recommended over reactify now, maybe we should change for that later on then. 

