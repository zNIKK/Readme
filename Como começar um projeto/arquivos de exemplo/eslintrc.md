
## `files` e `ignores`

Você pode usar essa combinação para determinar qual configuração aplicará as regras e qual não aplicará.

```js
module.exports = {
        files: ["src/**/*.js"],
        rules: {
            semi: "error"
        }
    }
];
```

### `ignore` globalmente

pode ignorar arquivos globalmente

```js
module.exports = {
    {
        ignores: [".config/*"]
    }
};
```

## Configurando regras

## Arquivo de exemplo

```js
module.exports = {
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended"
  ],
  "overrides": [
    {
      "env": {
        "node": true
      },
      "files": [
        ".eslintrc.{js,cjs}"
      ],
      "parserOptions": {
        "sourceType": "script"
      }
    }
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "plugins": [
    "@typescript-eslint",
    "react"
  ],
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "rules": {
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    'react/react-in-jsx-scope': 'off'
  }
}
```
