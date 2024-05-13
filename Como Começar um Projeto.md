
# instalação e configuração

## Instalando Npm:

`npm init -y`

## Instalando React.js (opcional):

`npm install react --save`

Crie um projeto em React:

`npx create-react-app meu-app`

## Instalando Eslint:

inicie o Eslint e responda as perguntas:

`npx eslint --init`

instalar a biblioteca `eslint-import-resolver-typescript` que permite importar arquivos `.ts/.tsx` e algumas outras funcionalidades dentro do nosso projeto:

`npm install -D eslint-plugin-import @typescript-eslint/parser eslint-import-resolver-typescript`

E em seguida devemos atualizar nosso arquivo `.eslintrc`, é só adicionar uma configuração à chave `rules` e uma à chave `settings` (caso não exista é só criar abaixo da última chave):  

```json
"rules": {
  ...
  "import/no-unresolved": "error"
},
"settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
}
```

## instalando Prettier

para instalar o Prettier devemos usar:

`npm install -D prettier eslint-config-prettier eslint-plugin-prettier`

Agora iremos atualizar nosso arquivo `.eslintrc` novamente, basta adicionar uma linha à nossa chave `extends` e uma à nossa chave `plugins`:  

```json
"extends": [
  ...
  "plugin:prettier/recommended"
],
"plugins": [
  ...
  "react-hooks",
  "prettier"
]
```

## Adicionando projeto ao repositório do GitHub (Opcional):

Conecte o repositório local ao remoto:

`git remote add origin git@github.com:USER_NAME/REPO_NAME.git`

Crie uma branch principal (Main Branch):

`git branch -M main`

Por ultimo subimos para o repositório remoto:

`git push -u origin main`

## Instalando TypeScript e os Tipos

Para instalar o Typescript devemos usar:

`npm install -g typescript`


`npm install --save-dev @types/react@latest @types/react-dom@latest`