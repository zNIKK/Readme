
## Dependências de desenvolvimento de sistemas

### build-essential

- Tem todo o essencial para fazer "Builds"

### default-jdk

- Instala a "jvm" como compilador do JAVA mais novo

### libssl-dev

- Parte da implementação do projeto OpenSSL dos protocolos criptográficos SSL e TLS para comunicação segura pela Internet.

### exuberant-ctags

- um clone ctags que é consideravelmente mais capaz que os ctags Unix. Ele produz um formato de arquivo de tags estendido que torna o processo de pesquisa e correspondência de tags mais flexível e poderoso.

### ncurses-term

- é uma biblioteca de programação que fornece uma interface de programação de aplicativo (API) que permite ao programador escrever interfaces de usuário baseadas em texto (TUI) de maneira independente do terminal.

### ack-grep

- Ack foi projetado como um substituto para 99% dos usos do grep. Ack pesquisa nos ARQUIVOS de entrada nomeados (ou na entrada padrão se nenhum arquivo for nomeado, ou o nome do arquivo - for fornecido) por linhas que contenham uma correspondência com o PATTERN fornecido.

### silversearcher-ag

- É uma ferramenta de pesquisa baseada em linha de comando super rápida. Basta executar `ag "termo de pesquisa"` para pesquisar seu termo de pesquisa. Isto irá listar cada linha de cada arquivo em qualquer diretório em seu diretório de trabalho atual que contenha uma correspondência

### fontconfig

- É uma biblioteca de programas livre projetada para fornecer configuração, enumeração e substituição de fontes para outros programas.

### imagemagick

- É uma suite de aplicativos para edição não interativa de imagens, ou seja, com ele é possível editar, converter, combinar etc. imagens de dezenas de tipos.

### libmagickwand-dev

- Este é um pacote de transição para ajudar a migrar sistemas para a nova ABI dos arquivos de desenvolvimento libmagickwand-6 para profundidade de canal padrão.

### software-properties-common

 - Este software fornece uma abstração dos repositórios apt usados. Ele permite que você gerencie facilmente sua distribuição e fontes de software de fornecedores de software independentes.

### git

- Usado para controle de versões e para registro de histórico das edições de qualquer tipo de arquivo.

### vim-gtk3

- É um editor de texto poderoso, popular entre os desenvolvedores. É baseado em atalhos, chamados de linguagem Vim, que podem tornar a codificação e a escrita mais rápidas e eficientes.


### curl

- É uma ferramenta de linha de comando para transferir dados usando vários protocolos.

```shell
sudo apt install build-essential default-jdk libssl-dev exuberant-ctags ncurses-term ack-grep silversearcher-ag fontconfig imagemagick libmagickwand-dev software-properties-common git vim-gtk3 curl -y
```

## Serviços para instalar

```shell
sudo apt -y install postgresql postgresql-contrib postgresql-server-dev redis-server libhiredis-dev memcached libmemcached-dev
```

## SSH(Secure SHell)

**SSH** é um protocolo de rede que permite dois computadores se comuniquem, ou seja você abra um terminal de outro computador no seu.

abrir um servidor usa-se:

```shell
ssh usuario@ip_do_servidor
/// Exemplo:
ssh ubuntu@10.234.190.66
```

### Chave SSH

para criar uma chave usa-se:

`ssh-keygen -f ~/.ssh/nomedachave -t rsa -b 4096`