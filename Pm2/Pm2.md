
# O que é?

- PM2 é um gerenciador de processos que ajuda a gerenciar e manter suas aplicações online. Com ele você pode gerenciar mais de uma aplicações NPM em um servidor só

# Instalação

```bash
sudo npm i -g pm2
```

para começar uma aplicação deve se dar um caminho de entrada ou seja o caminho que você inicia a aplicação.

```bash
pm2 start /home/<usuario>/projeto/projeto.js
```

> o parâmetro `--name <nome>` seleciona um nome para sua aplicação

# Comandos

## `pm2 list`

lista todos os aplicativos que foram carregados pelo pm2

## `pm2 stop <projeto>`

para o atual aplicativo