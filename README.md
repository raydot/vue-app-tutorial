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

# Interesting things I learned!

A `.vue` file always consists of three things: 
    <ul>
        <li>`<template>`</li>
        <li>`<script>`</li>
        <li>`<style>`</li>
    </ul>

Example:

`<template></template>

<script>
    export default {
        name: 'component-name',
    }
</script>

<style scoped></style>
`

The data and logic for the component goes into `<script>` but only `name` is required.  The `<style>` tag is just CSS.  'scoped' means it only applys to this component and not globally.

