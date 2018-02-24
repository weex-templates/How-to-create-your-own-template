# How-to-create-your-own-template

This document will introduce how to create your template and how to be work with the `weex-toolktit`.

## Examples

[1] [weex-templates/webpack](https://github.com/weex-templates/webpack)

The `weex-toolkit` will call flowing command while using the corresponding command:

![weex-toolkit](https://img.alicdn.com/tfs/TB1Rso6awmTBuNjy1XbXXaMrVXa-1169-599.png)

If you want to get the best experience, it is best to implement these commands

| Command | Description|
| -------- | -------- |
|npm run dev|This command need to compile the source on watch mode and put the production into the `dist` folder |
|npm run serve|This command need to open a web browser for developer to preview their page on web|
|npm run build:plugin|This command need to merge the plugins into `plugins/plugins.js` file which can be include into the entry file. |
|npm run build:prod|This command need to compiler source with production mode and put the file into the `dist` folder|
|npm run pack:web|The `pack:web` command need to transform `.vue` file into a `.html` file, such as `index.html` with `.js` files.|

## Necessary structure

``` bash
.
├── template/                   # folder for [ios|android] project
│   └── configs                 # webpack config files
│   │   └── ...
│   └── platforms
│   │   └── platforms.json      # file for storing platform version
│   │   └── ...
│   └── plugins
│   │   └── plugins.json        # file for storing plugin version
│   └── src/                    # source code
│   │   └── ...
│   └── test/                   # test code
│   │   └── ...
│   └── android.config.json     # android config file for `weex-toolkit`
│   └── ios.config.json         # ios config file for `weex-toolkit`
│   └── package.json            # build scripts and dependencies
│   └── README.md               # Default README file
├── package.json
└── meta.js                     # you can config prompts、filters、helpers、complete function while render the template
```

## Develop

In your template, the creater is using [handlebars](https://www.npmjs.com/package/handlebars) to render the template, so you can use `{{}}` such as `{{name}}` to binding data into your template, the data can be modify in the `meta.js` file and you can wrote some rules to using some conditional statement, suce as `{{#if_eq babel "stage-0"}}...some code{{/if_eq}}`.
More detail you can see the document here [handlebars helpers](http://handlebarsjs.com/#helpers), you can register helpers on `meta.js` file and here are several built-in conditional statement:

### #if_eq
```
{{#if_eq lintConfig "airbnb"}}
while the lintConfig === "airbnb", this line will be show
{{else}}
else this line will be show
{{/if_eq}}
```

### #unless_eq
```
{{#unless_eq lintConfig "airbnb"}}
while the lintConfig !== "airbnb", this line will be show
{{else}}
else this line will be show
{{/unless_eq}}
```

### #unless
```
{{#router}}
while the router is true, this line will be show
{{/router}}

{{#unless router}}
while the router is false, this line will be show
{{/unless}}
```

## Usage
```
$ weex create <template> [project-name] [options]
```

1. Create a new project with an official template, if the `<template>` has no slash, it will search template from `https://github.com/weex-templates` and the default template is `https://github.com/weex-templates/webpack`.
```
$ weex create my-project
$ weex create webpack my-project
```

2. create a new project straight from a github or other remote template.

- GitHub - github:owner/name or simply owner/name
- GitLab - gitlab:owner/name
- Bitbucket - bitbucket:owner/name

```
$ weex create username/repo my-project . #github
$ weex create gitlab:username/repo my-project . #gitlab
$ weex create bitbucket:username/repo my-project . #bitbucket
```


If you have any questions, please create a issue to me.

