# vue-app-tutorial

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Run your tests
```
yarn run test
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# Following Tutorial
[Getting Started With Vue](https://www.taniarascia.com/getting-started-with-vue/) by Tania Rascia

# Interesting things I learned!

A `.vue` file always consists of three things: 
    <ul>
        <li>`<template>`</li>
        <li>`<script>`</li>
        <li>`<style>`</li>
    </ul>

Example:

    <template></template>
    
    <script>
	    export  default {
		    name:  'component-name',
        }
    </script>
    
     <style scoped></style>

The data and logic for the component goes into `<script>` but only `name` is required.  The `<style>` tag is just CSS.  'scoped' means it only applys to this component and not globally.

# Verdict
Success!  I wish all tutorials were like this one.  Easy to follow, and works 100% without my having to spend two hours on Stack trying to figure out why nothing works.

