# @9x3l6/eslint-config

[![npm](https://img.shields.io/npm/v/@9x3l6/eslint-config?color=a1b858&label=)](https://npmjs.com/package/@9x3l6/eslint-config)

Fork of @antfu/eslint-config, I originally made my own repo overriding some eslint rules but then ran into some issues when I wanted to use the git commit hooks in my projects. This fork was created to solve some of those issues with out of date packages as well as many of the other changes I made along the way to the @anfu/eslint-config code for use in my own projects.

- Single quotes, no semi; **not anymore** since many projects use a different style I turned this off
- Auto fix for formatting (aimed to be used standalone **without** Prettier)
- Designed to work with TypeScript, Vue out-of-box
- Lint also for json, yaml, markdown
- Sorted imports, dangling commas
- Reasonable defaults, best practices, only one-line of config
- **Style principle**: Minimal for reading, stable for diff

### Overriding rules in place

```js
  "rules": {
    "vue/prefer-separate-static-class": "off",
    "vue/html-self-closing": "off",
    "vue/html-end-tags": "off",
    "vue/html-indent": "off",

    "9x3l6/if-newline": "off",

    "@typescript-eslint/quotes": "off",
    "@typescript-eslint/semi": "off"
  }
```

## Usage

### Install

```bash
pnpm add -D eslint @9x3l6/eslint-config
```

### Config `.eslintrc`

```json
{
  "extends": "@9x3l6"
}
```

> You don't need `.eslintignore` normally as it has been provided by the preset.

### Add script for package.json

For example:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

### VS Code support (auto fix)

Install [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Add the following settings to your `settings.json`:

```jsonc
{
  "prettier.enable": false,
  "editor.formatOnSave": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": false,

    // The following is optional.
    // It's better to put under project setting `.vscode/settings.json`
    // to avoid conflicts with working with different eslint configs
    // that does not support all formats.
    "eslint.validate": [
      "javascript",
      "javascriptreact",
      "typescript",
      "typescriptreact",
      "vue",
      "html",
      "markdown",
      "json",
      "jsonc",
      "yaml"
    ]
  }
}
```

### TypeScript Aware Rules

Type aware rules are enabled when a `tsconfig.eslint.json` is found in the project root, which will introduce some stricter rules into your project. If you want to enable it while have no `tsconfig.eslint.json` in the project root, you can change tsconfig name by modifying `ESLINT_TSCONFIG` env.

```js
// .eslintrc.js
process.env.ESLINT_TSCONFIG = 'tsconfig.json'

module.exports = {
  extends: '@9x3l6'
}
```

### Lint Staged

If you want to apply lint and auto-fix before every commit, you can add the following to your `package.json`:

```json
{
  "simple-git-hooks": {
    "pre-commit": "pnpm lint-staged"
  },
  "lint-staged": {
    "*": "eslint --fix"
  }
}
```

and then

```bash
npm i -D lint-staged simple-git-hooks
```

## FAQ

### Antfu on why not use Prettier

[Why I don't use Prettier](https://antfu.me/posts/why-not-prettier)

### How to lint CSS?

This config does NOT lint CSS. I personally use [UnoCSS](https://github.com/unocss/unocss) so I don't write CSS. If you still prefer CSS, you can use [stylelint](https://stylelint.io/) for CSS linting.

### I prefer XXX...

Sure, you can override the rules in your `.eslintrc` file.

<!-- eslint-skip -->

```jsonc
{
  "extends": "@9x3l6",
  "rules": {
    // your rules...
  }
}
```

Or you can always fork this repo and make your own.

## Check Also

- [antfu/dotfiles](https://github.com/antfu/dotfiles) - My dotfiles
- [antfu/vscode-settings](https://github.com/antfu/vscode-settings) - My VS Code settings
- [antfu/ts-starter](https://github.com/antfu/ts-starter) - My starter template for TypeScript library

## Dev

### Update

```bash
npm i -g @antfu/ni
pnpm -r update
```

## License

- [MIT](./LICENSE) License &copy; 2019-PRESENT [Anthony Fu](https://github.com/antfu)
- [MIT](./LICENSE) License &copy; 2023-PRESENT [Alex Goretoy](https://github.com/9x3l6)