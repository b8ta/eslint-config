# eslint-config-b8ta

[Sharable ESlint config files](http://eslint.org/docs/developer-guide/shareable-configs) to "extends" in our projects. Do not extend the files from the "rules" folder directly.

# Configure Webpack Resolver for `eslint-plugin-import`

In projects that use special webpack resolve rules (such as `resolve.alias`), you will need to provide webpack config to allow `eslint-plugin-import` to resolve modules that it lints correctly.

**1. Install eslint-import-resolver-webpack**

```bash
yarn add -D eslint-import-resolver-webpack
```

Not every project needs this, so it is the consumer project's responsibility to manage the dependency. Recent working version tested was `eslint-import-resolver-webpack@0.8.1`.

**2. Update Settings of the project `.eslintrc` with `import/resolver`**

```json
{
  ...
  "settings": {
    "import/resolver": {
      "webpack": {
        "config": "./config/webpack.config.js"
      }
    }
  },
  ...
}
```

ESLint will find the config file using the path relative to the location of your `package.json`. If you want more power (e.g. using different webpack config for different builds), consider [using Javascript eslint config](http://eslint.org/docs/user-guide/configuring).

Do not use "babeled" webpack config file (or require modules that require to be transpiled). ESLint only loads standard Javascript that supports in the version of your runtime node.
