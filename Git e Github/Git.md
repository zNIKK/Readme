
# Instalando

`sudo pacman -Sy git`

# Usando uma pasta git

Dentro da pasta para se cadastrar, use:
```bash
git config --global user.email "nicolas.gandolfi11@gmail.com"
git config --global user.name "zNIKK"
```

Depois disso precisa criar um arquivo `.git` em sua pasta para fazer a versatilidade:

```bash
git init
```


## `git add .`

Usando esse comando os arquivos são mandados para a pasta git.

> o `.` significa que é a pasta atual

## git commit -m "MSG"

Usando esse comando git criara uma nova versão para o seus arquivos com o argumento `-m` para mandar mensagens personalizadas ou atualizando do que mudou. 


lembrar da sua conta toda vez que fizer [push]
```bash
git config --global credential.helper store
```
