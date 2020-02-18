# Hi ! 🚀

# Goal and about

**Currently**, this is a simple cli tool for generating web app projects like using MERN stack based on a few questions and some build and development-related questions as well as preferred bundler and all.

**Goal**. What I want to achieve is a tool that will eliminate the requirement of adding boilerplates manually. the goal extends to a point where I whole adding of boilerplates should be flexible and customizable. As a user I would like to have more options on my bundler or on my styling options, I want a plugin to update my `webpack.config.js` when I am changing my style loaders or changing my scss to postcss or similar and many other use cases. _It will be used as a pair programmer rather than a project generator._

The most important thing about this project will be how plugins are integrating and how they will work. and I consider this as most challenging thing of this project. Plugins will load more than 70% work of using this package. And writing plugins should be simple.

# :mega: Re-Written of the CLI

> ## Not a new version, its gonna be a new package.

## Current Implementation

Currently, the cli is using templates architecture where it is being shipped of the templates while installing which can increase the bundle size of the project and also increase the install time.
We have Three templates right now and have a plane to increase them to more number in future as **the goal** of this CLI is to **`become a single app generator for all kind, type, the stack of the project`**.

## New Architecture plan

#### 1. No templates packages in the project core:

- In order to reduce the size and time, no templates are gonna live inside the core package and also not in this repo.
- We are going to adopt the cloning mechanism, and more details about the clone flow will be discussed below or in a separate issue
- Like how `gatsby-cli` does.

#### 2. Plugin Architecture _Most Exciting Plan_:

- I have an on-going plan to make it pluggable. These plugins are gonna be separate packages. And each plugin will do a particular set of work.
- Small work like database managing and connecting plugin, Styling managing and creating a plugin, adding `passportjs` in your project plugin, etc.
- More about these plugin types and how this will be implemented will be discussed in a separate issue.

#### 3. Config file :

- Surely gonna have this config file thing for using the cli as an one more option to use the package.
- A **Global Config File** system, which is going to have a config file and whenever the cli is running it will load this if CLI finds it!

#### 4. Monorepo:

- The whole project will be a mono repo based project with the core cli logic in the `core` package. Also, there will core plugins and utility methods in this repo as monorepo.
- Future plans for the GUI version of the cli will be added as monorepo too. _Although not sure about this just a thought_.

#### 5. Anything to make it **FAST**:

- This is going to be our main priority. I am ready to compromise additional features in order to make it awesomely fast.
- Planning to have a `caching` system in order to cache the plugins, packages and also the **user's interactions**

# Working flow _not final yet_:

1. When starting the cli, you can either pass the Github link to the boilerplate you want to use or the CLI will prompt to ask for it.

   - It will first check for some specific files in the boilerplate project and if it finds it okay to make it customizable and pluggable. then it will install it and will do further work

   - If not, then it will scan the github keywords used in that project and will recommend you based on that keywords. It will try to recommend any default or official boilerplates.

   - command will look similar like this : - if passing the boilerplater then may like `-b [URL]` or if not passing the boilerplate , just
     simply running the CLI , it will start an interactive prompt

2)  Work of the **Interactive prompt**:

    - used will be asked some basic questions like, is it a website with or without server, _(basic)_
    - then if with the server then chained of questions like server framework or raw? , need a database? if yes then type and preferred ORM for it?. _(an advance question which may not be required to answer)_
    - Then question for frontends framework, _(basic)_
    - need state management if supported?, then need SSR if supported?
    - Then language type like TS or JS _(an advance question which may not be required to answer)_
    - Preferred bundlers, styling thing. _(an advance question which may not be required to answer)_

    - PWA ? or need minimal alternatives to framework like Preact for react etc._(an advance question which may not be required to answer)_ ,

3)  Using the config file, :

    - May be using flags like `-c [path]` it will look for global config file if the `path` is not passed else it will load the config file mentioned in the `path`
    - then it will use this config file to create the project.

4)  Where plugin will come?

          - there will be some default plugins that will be used during the build time like, webpack plugin, or postcss plugin which will be used based on selecting the stack or framework preference. , Like when we select PWA, a PWA managing plugin will be run to handle it.
         - We can say like this. **Based on these basic question, the boilerplate project will be selected** and **Based on the advance question, the plugin will be selected to customize those boilerplates**
         - And there will be plugins, which we can add using similar commands like `--plugin <plguin-name>` inside our project structure and then it will create config file inside the project if not present already, and it will add this plugin name to that config file and then running command like `make` will run that plugin and also we can prefined plugin(s) in that config file and will run those plugins.

    > the config file inside the project folder and config file located globally will be different and even with different name ! will have to think about this in details

## This is what I got till now !
