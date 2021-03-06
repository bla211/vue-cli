# CLI Service

## Using the Binary

Inside a Vue CLI project, `@vue/cli-service` installs a binary named `vue-cli-service`. You can access the binary directly as `vue-cli-service` in npm scripts, or as `./node_modules/.bin/vue-cli-service` from the terminal.

This is what you will see in the `package.json` of a project using the default preset:

``` json
{
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build"
  }
}
```

You can invoke these scripts using either npm or Yarn:

``` bash
npm run serve
# OR
yarn serve
```

If you have [npx](https://github.com/zkat/npx) available (should be bundled with an update-to-date version of npm), you can also invoke the binary directly with:

``` bash
npx vue-cli-service serve
```

## vue-cli-service serve

```
Usage: vue-cli-service serve [options]

Options:

  --open    open browser on server start
  --copy    copy url to clipboard on server start
  --mode    specify env mode (default: development)
  --host    specify host (default: 0.0.0.0)
  --port    specify port (default: 8080)
  --https   use https (default: false)
```

The `serve` command starts a dev server (based on [webpack-dev-server](https://github.com/webpack/webpack-dev-server)) that comes with Hot-Module-Replacement (HMR) working out of the box.

In addition to the command line flags, you can also configure the dev server using the [devServer](../config/#devserver) field in `vue.config.js`.

## vue-cli-service build

```
Usage: vue-cli-service build [options] [entry|pattern]

Options:

  --mode    specify env mode (default: production)
  --dest    specify output directory (default: dist)
  --target  app | lib | wc | wc-async (default: app)
  --name    name for lib or web-component mode (default: "name" in package.json or entry filename)
  --watch   watch for changes
```

`vue-cli-service build` produces a production-ready bundle in the `dist/` directory, with minification for JS/CSS/HTML and auto vendor chunk splitting for better caching. The chunk manifest is inlined into the HTML.

It is also possible to build any component(s) inside your project as a library or as web components. See [Build Targets](./build-targets.md) for more details.

## vue-cli-service inspect

```
Usage: vue-cli-service inspect [options] [...paths]

Options:

  --mode    specify env mode (default: development)
```

You can use `vue-cli-service inspect` to inspect the webpack config inside a Vue CLI project. See [Inspecting Webpack Config](../config/#inspecting-the-project-s-webpack-config) for more details.

## Checking All Available Commands

Some CLI plugins  will inject additional commands to `vue-cli-service`. For example, `@vue/cli-plugin-eslint` injects the `vue-cli-service lint` command. You can see all injected commands by running:

``` bash
npx vue-cli-service help
```

You can also learn about the available options of each command with:

``` bash
npx vue-cli-service help [command]
```

## Caching and Parallelization

- `cache-loader` is enabled for Vue/Babel/TypeScript compilations by default. Files are cached inside `node_modules/.cache` - if running into compilation issues, always try deleting the cache directory first.

- `thread-loader` will be enabled for Babel/TypeScript transpilation when the machine has more than 1 CPU cores.

## Git Hooks

When installed, `@vue/cli-service` also installs [yorkie](https://github.com/yyx990803/yorkie), which allows you to easily specify Git hooks using the `gitHooks` field in your `package.json`:

``` json
{
  "gitHooks": {
    "pre-commit": "lint-staged"
  }
}
```

::: warning
`yorkie` is a fork of [`husky`](https://github.com/typicode/husky) and is not compatible with the latter.
:::

## Configuration without Ejecting

Projects created via `vue create` are ready to go without the need for additional configuration. The plugins are designed to work with one another so in most cases, all you need to do is pick the features you want during the interactive prompts.

However, we also understand that it's impossible to cater to every possible need, and the need of a project may also change over time. Projects created by Vue CLI allows you to configure almost every aspect of the tooling without ever needing to eject. Check out the [Config Reference](../config/) for more details.
