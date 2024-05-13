
# O que é 

- É um software que entrega uma VM (Virtual Machine) para programas isolados em **containers**.

## Desvantagens

- Em uma máquina virtual divide recursos de processador de sua máquina principal além de que você precisa **cuidar de dois sistemas completos** com dois kernels, uso de mais armazenamento de RAM.

- Esse cuidado é contra intuitivo, pois muitas vezes você só quer executar um programa o que faz ser eficiente utilizar o **Docker**.

## Vantagens

- Um container Docker consegue compartilhar recursos da própria máquina hospedeira, como o kernel dela. Evitando redundância, reduzindo recursos desnecessários

- Faz com que **uma unica só máquina consiga rodar varias aplicações diferentes** simultaneamente sem gastar tanto recurso de hardware

- Além da **segurança** de se ter recursos em VMs

- Te permite **backups**

# Comandos

## $`docker pull`

- Baixar um container Docker:

Exemplo:

`docker pull wordpress`

- Sempre ira baixar a ultima versão da imagem, se você quer uma versão especifica.

`docker pull IMAGEM:v1.0.0`


## $`docker images`

- Mostra **todas** as imagens em tabela.

## $`docker run`

- cria um container baseado em uma imagem baixada

Exemplo:

`docker run --name meu_wordpress -p 8080:80 -d wordpress`

### Argumentos

#### `--name NOME`

- Usar um nome para o container 

#### `-p 0000:00`

- Colocar uma porta que será usada pelo container

#### `-d IMAGEM`

- Colocar qual imagem baixada será usada pelo container 

#### `-i -t IMAGEM`

- `-i` permite nossa interação com o container

- `-t` alocar um pseudo-TTY (Pseudo Terminal)

## $`docker ps`

- Lista os **containers em execução**

### Argumentos

#### `-a`

- Listar tanto os  **containers em execução** quanto os **containers parados**

## $`docker stop`

- Para a execução de um container

Exemplo:
`docker stop wordpress`

## $`docker start`

- inicia um container

Exemplo:
`docker start wordpress`

## $`docker restart`

- Reinicializa um container

Exemplo:
`docker restart wordpress`

## $`docker rm`

- remove um container

- os containers precisa estar parados para ser removidos

- remove SÓ os containers as imagens ainda estão armazenadas

Exemplo:
`docker rm wordpress`
OU
`docker rm ID_DO_CONTAINER`

> `rmi` - Remove uma imagem de OS


