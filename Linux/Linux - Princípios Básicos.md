
## O que é

Linux é um componente de um sistema operacional chamado Kernel

### Kernel

- parte responsável por gerenciar o Hardware

- é o núcleo do sistema operacional

- exemplo: Graças ao kernel que o sistema operacional consegue reproduzir musicas

#### `uname -r` 

Ver a versão do Kernel atual

#### `mhwd-kernel`

Instala e remove um novo kernel. Mostra todos os kernels instalados e os disponíveis

##### Parâmetros

###### `-i`

- instala um novo kernel

###### `-l`

- Lista todos os kernels disponíveis

###### `-li`

- Lista todos os kernels instalados

###### `-r`

- remove um kernel

## Comandos principais


### Dicas

- Você pode juntar parâmetros, exemplo:


```shell
ls -l -a
# simplificado:
ls -la
```

### $`whoami` 

- Comando para saber que usuário está na máquina

### $`hostname`

- Comando para saber o nome da máquina

#### Parâmetros

##### `-I`

- Mostra todas as interfaces de IPs na máquina

### $`chown` (Change Owner)

- Muda o dono da máquina

### $`pwd` (Print Working Directory)

- Exibe o diretório atual completo

### $`ls` (List)

- Lista informações sobre os ARQUIVOs (no diretório atual por padrão).

#### Parâmetros

##### `-l/--long`

- Listagem mais completa de um diretório contendo quantas pastas possui, usuário proprietário do arquivo e de quando foi criado.

##### `-h`

- Usado para exemplificar os bytes de um arquivo.

##### `-a/--all`

- Usado para mostrar TODAS as pastas inclusive as ocultas.

### $`lscpu`(List CPU)

- Lista as informações da processador da maquina de uma forma mais amigável

### $`clear` (Limpar)

- limpa o terminal

> CTRL + L

### $`cd` (Change Directory)

- navega pelos diretórios

#### Variáveis

##### `~` (Tilde Expansion)

- vai para o HOME

##### `/` (root)

- vai para o diretório raiz

###### `..`

- volta um diretório



### $`rmdir` (Remove Diretory)

- Remove um diretório

### $`touch`

- cria um arquivo, porem se o arquivo já existe ele vai atualizar o acesso a modificação da hora atual sem mudar seu conteúdo. 

- Exemplo, Criar um arquivo **.txt** com touch:

```shell
touch texto.txt
```

### $`echo`

- Este comando mostra texto na saída padrão seguido por uma nova linha.

#### Parâmetros

##### `texto > file.txt`

- Adiciona texto dentro do arquivo porem substitui

##### `texto >> file.txt`

- Concatena texto dentro do arquivo

### Manipulação de Arquivos

#### $`mkdir` (Make Directory)

- Cria um arquivo

#### $`cp`(Copy)

- Copia o arquivo para outra pasta ou diretório

#### $`mv` (Move)

- move um arquivo de um diretório para o outro 

- Troca o nome do arquivo

#### $`rm` (Remove)

- remove arquivo

##### Parâmetros 

###### `-i`

- Bash vai te perguntar se você quer mesmo apagar.

###### `-I`

- Bash vai te perguntar se você quer mesmo apagar. Somente quando 4 ou mais arquivos forem apagados

###### `-r`

- Apaga arquivos recursivamente.

###### `-f`

- Apaga um arquivo ou diretório mesmo se conter arquivos dentro dele

- **Cuidado** - Ele força a apaga TODOS OS ARQUIVOS


#### $`cat`

- Coloca na tela o conteúdo de um arquivo

- Feito para arquivos menores

- Pode ser usado `tac` para formatar o texto de baixo pra cima

### Editores e Paginadores

#### $`nano`

- usado para editar um arquivo **.txt** em um editor de texto

#### $`more`

- coloca na tela o conteúdo de um arquivo 

- feito para arquivos maiores

- (Comando Primitivo) - Usamos `less` ao invés desse

#### $`less`

- coloca na tela o conteúdo de um arquivo 

- feito para arquivos maiores

- ele faz isso em "Streams"

- permite usar **comandos dos editores de navegação tipo VI**

> j = para baixo
> k = para cima
> gg = pro topo
> (numero) e j = descer um numero de linhas para baixo
> (numero) e k = subir um numero de linhas para cima
> / e palavra = para procurar uma palavra, descer usando "n"
> q = parar

#### $`head`

- Ver as primeiras linhas

#### $`tail`

- Ver as ultimas linhas

##### Parâmetros

###### `-(números)`

- Ver as ultimas linhas que o número corresponde

###### `-f`

- Ver as ultimas linhas em produção

### $`ps`

- lista processos do sistema

#### Parâmetros

##### `aux`

- inclui os processos que não foram iniciados pelo usuário

### $`ln`

- Este comando cria ligações (_links_) entre **arquivos**. Há dois conceitos de _ligação_ em sistemas Unix:

- **Ligação direta** – define mais um nome para um arquivo (um arquivo pode ter diversos nomes). O arquivo será removido  do disco quando o último nome for removido. Não há algo como um nome original, todos os nomes tem o mesmo _status_.

- **Ligação simbólica** ou **dymlink** – define um caminho para um arquivo. Ligações simbólicas podem apontar para arquivos em diferentes sistemas de arquivo e não necessitam apontar para arquivos que realmente existem.

#### Parâmetros

##### `-d`(Hard Link)

- cria uma ligação direta, **é o padrão**.

##### `-L/--logical`

- cria uma ligação para um link simbólico.

##### `-s`(Soft Link)

- cria uma ligação simbólica.

##### `-v`

- mostra o nome de cada arquivo antes de criar o link.

### $`grep`(Globally Search a Regular Expression and Print)

- Localizar a palavra no arquivo

- Usado com expressões regulares

- Exemplo:  `ps aux | grep bash`
- localiza a palavra "bash" nos processos

- (Comando Primitivo) - Usamos o `ag` ao invés desse

### $`Find`

- Encontra arquivos dentro de diretórios

#### Parâmetros

 `.`

- Encontra arquivos a partir da pasta atual

`-name arquivo`

- Nome do arquivo que você quer procurar

### $`awk`

- Linguagem de programação interpretada voltada a processar dados e textos

### $`service service_name command`(systemctl)

- Usado para iniciar, parar ou ver um banco de dados em serviço

- Exemplo: `sudo service postgresql start`
- iniciar o postgresql

## Referência global

### `*x*`

- seleciona em uma pasta só os arquivos que tenham essa **x** ***na frente, atrás ou ambos.***

- Exemplo. No diretório /etc/ tem muitos arquivos **.conf** de nomes diferentes, para ler os arquivos. Usamos:

```bash
# na pasta etc/ coloque em lista só os arquivos .conf
ls /etc/*.conf

RETORNO

/etc/cpufreq-bench.conf  /etc/nfs.conf
/etc/dhcpcd.conf         /etc/nfsmount.conf
/etc/dnsmasq.conf        /etc/nftables.conf
/etc/e2scrub.conf        /etc/nsswitch.conf
/etc/fprintd.conf        /etc/openswap.conf
/etc/fuse.conf           /etc/ostree-mkinitcpio.conf
/etc/gai.conf            /etc/pacman.conf
/etc/healthd.conf        /etc/pacman-mirrors.conf
/etc/host.conf           /etc/pamac.conf
/etc/idmapd.conf         /etc/passim.conf
/etc/inxi.conf           /etc/request-key.conf
/etc/ipsec.conf          /etc/resolv.conf
/etc/krb5.conf           /etc/resolvconf.conf
/etc/ld.so.conf          /etc/rsyncd.conf
/etc/libaudit.conf       /etc/rygel.conf
/etc/libva.conf          /etc/sensors3.conf
/etc/locale.conf         /etc/strongswan.conf
/etc/logrotate.conf      /etc/sudo.conf
/etc/makepkg.conf        /etc/sudo_logsrvd.conf
/etc/man_db.conf         /etc/timeshift-autosnap.conf
/etc/mdadm.conf          /etc/ts.conf
/etc/mhwd-x86_64.conf    /etc/usb_modeswitch.conf
/etc/mke2fs.conf         /etc/vconsole.conf
/etc/mkinitcpio.conf     /etc/xattr.conf

```

### `?x`

- arquivos que tenham **x** de ***segunda letra***

- Exemplo. Eu quero selecionar só arquivos que tenham na segunda e terceira letra **as** e qualquer coisa depois, dentro de etc/

```bash
# lista palavras que tem "as" na segunda e terceira letra
ls /etc/?as*

RETORNO

/etc/bash.bash_logout  /etc/passim.conf  /etc/passwd-
/etc/bash.bashrc       /etc/passwd

/etc/sasl2:
libvirt.conf  qemu.conf

```

> Posso colocar "?" para aumentar a posição da letra. Exemplo:
> ls /etc/???a* - lista "a" na **quarta posição**

### `[a-e]`

- Faixa de caracteres aonde vária entre **a** ***até o*** **e**

- Exemplo. Eu quero lista só arquivos em /etc/ que tenha f na primeira letra e qualquer letra entre **a** até **o** no nome

```bash
ls /etc/f[a-o]*

RETORNO

/etc/flatpak:
remotes.d

/etc/fonts:
conf.d  fonts.conf

```

### `[a,e]`

- Faixa de caracteres aonde vária entre **a** ***ou*** **e**

- Exemplo. Eu quero lista só arquivos em /etc/ que tenha f na primeira letra e qualquer letra entre **a** ou **o** no nome

```bash
ls /etc/f[a,o]*

RETORNO

conf.d  fonts.conf

```

### `{tab,swd}`

- Busca arquivos ***terminados*** por **tab** ou **swd**

- Exemplo. Quero uma lista de arquivos em /etc/ que terminam com **tab** e **swd**. NÃO É A EXTENSÃO DO ARQUIVO.

```bash
ls /etc/*{tab,swd}*

RETORNO

/etc/anacrontab  /etc/crypttab  /etc/mtab           /etc/passwd
/etc/crontab     /etc/fstab     /etc/nftables.conf  /etc/passwd-

/etc/iptables:
empty.rules  ip6tables.rules  iptables.rules  simple_firewall.rules
```

## Diretórios da raiz

### /Dev (device)

- Ficam de todos os dispositivos na máquina

- Você nunca vai mexer em nesses dispositivos porque eles ainda não estão montados

- Dispositivos montados são no diretório: */media* ou */amt*

> Para poder gravar ou ler esses dispositivos precisamos "montar" eles com um sistema de arquivos como exFAT ou NTFS (se for de WINDOWS), ou HFS (se for de MAC), ou EXT4 (se for de LINUX)

### /Sbin

- Ficam os binários da máquina ou seja os *programas do sistema operacional*

### /Bin

- Ficam outros programas do sistema mais simples como o `cd` e `ls`

### /Usr (Unix System Resources)

- Ficam os programas de usuário como o "firefox" e "VScode"

#### /lib

- Bibliotecas de dependências dos programas

#### /src

- Se instalar um código fonte junto fica aqui
#### /include

- Se instalar os pacotes em `-dev` para quando precisar copiar dependências

### /Etc (Etcetera)

- Se instalar os pacotes de configuração

### /Var

- Contêm dados variáveis

#### Diretórios

##### /spool

- Bobina de impressão quando usa a impressora 

##### /mail

- para email

##### /log

- Todos os logs do sistema

##### /run

- Tem PID(Process ID) IDs dos processos sendo executados

##### /cache

- Caches do sistemas

### /Proc (Process)

- Processos do sistema que estão em execução

> Comandos: `ps` - Lista os processos em execução

#### Diretórios

##### /cpuinfo

- Lista informações sobre o processador

- É um arquivo .TXT

> Comandos: `lscpu` - Lista as informações da processador da maquina

### /Tmp (Temp)

- Diretório de coisas temporárias que o sistema não garante que elas vão estar lá depois do próximo boot

### /Home

- Diretório do usuário da maquina, aonde tem as pastas de Download, documentos entre outros.
 
## Expressão regulares - |

- Concatena códigos executando eles juntos

- Exemplo: `ps aux | less`
- usa o `ps aux` que pega todos os processos em execução e coloca esses TXTs no `less`

## Alias

- Alias é um apelido já pre-definido para um comando.

- Exemplo, posso colocar por padrão um comando toda vez que eu executar:

```bash
rm -I
# pergunta se você realmente deseja apagar
alias rm="rm -I"
# por padrão agora quando eu executar "rm" ele usará o parâmetro -I 
```


## Atalhos

### setas

- Navega pelo histórico do bash

> Usa `history` Listar o histórico de comandos 
> `! + numero_do_comando` = selecionar comando desejado
### CTRL + R

- Procura um comando no histórico por texto

### CTRL + L

- limpa o terminal

## Regras de permissão

### `chmod +x "script.exe"`

- Todo binário ou script para ser executado precisa de permissão

## Distribuições  linux (distros)

é o resultado do esforço de uma empresa ou comunidade de programadores. São sistemas operacionais que usam o linux como Kernel

### Interfaces gráficas (DE)

#### Gnome

O Gnome é um dos DE’s mais populares de todos os tempos, não se restringindo somente à interface, mas aos diversos aplicativos que o compõem, como o seu gerenciador de arquivos o Nautilus.

- Desenvolvido para ser fácil de usar tanto em dispositivos móveis com telas sensíveis ao toque, quanto em desktops

- Traz consigo um fluxo de trabalho dinâmico e flexível, considerado intuitivo por muitas pessoas.

![[Pasted image 20231124153053.png]]
#### KDE

O KDE também é um projeto grande, utilizado por milhares de pessoas ao redor do mundo,sua interface gráfica é o Plasma. O projeto KDE tem um conjunto de programas para diversas funções como, por exemplo, o KDE Connect, usado para integrar smartphones com o sistema Linux.

- Considerado um dos DEs mais personalizáveis (às vezes, até “demais”) para um usuário iniciantes.

- É leve em recursos. Está presente ou é o ambiente padrão de inúmeras distribuições Linux, seu gerenciador de arquivos padrão é o “Dolphin”.

![[Pasted image 20231124153646.png]]
#### Cinnamon

O Cinnamon é um projeto mais recente, criado como um fork do Gnome 3, conta com uma série de aplicativos próprios. 

- A possibilidade de customização e as semelhanças da sua interface, elegante e polida, o torna amigável aos usuários que vem do Windows.

- ainda que os desenvolvedores trabalhem para ser mais leve e intuitivo.

- É o ambiente padrão do Linux Mint 

- pode ser instalado em várias outras distribuições. O gerenciador de arquivos é o Nemo, um fork do “Nautilus”.

![[Pasted image 20231124154221.png]]
#### MATE

O MATE começou como um fork do Gnome 2, a preferência de muitas pessoas por um desktop tradicional manteve vibrante o projeto, que incorporou muitas melhorias e otimizações.

- Um DE simples, leve e personalizável, que vem com uma boa seleção de aplicativos básicos e ferramentas úteis. 

- Várias distribuições trazem o MATE como uma das suas opções de ambiente gráfico. O gestor de arquivos do MATE é o “Caja”.

![[Pasted image 20231124154431.png]]
#### XFCE

Amado pelos que gostam de simplicidade mesclada com leveza e personalização, o XFCE usa as ferramentas GTK, mas não é um fork do Gnome. A sua modularidade faz com que seja adotado por inúmeras distribuições e os seus aplicativos também são úteis aos usuários dos gerenciadores de janelas (tiling).

- Não usa animações, mas não se deixe levar pela aparência “out-of-the-box”, pois o XFCE é bastante leve e a sua aparência pode ser bem diferente dependendo da distribuição. 

- O seu gerenciador de arquivos padrão é o “Thunar”.

![[Pasted image 20231124154732.png]]
#### Budgie

O projeto Budgie começou a ser desenvolvido na distribuição Solus e utiliza várias tecnologias do projeto Gnome como, por exemplo, o código GTK. Mesclando uma interface moderna e, simultaneamente, atraente ao usuário tradicional de desktops, ele não é pesado, mas também não é um dos ambientes mais leves.

- Destaca-se pelo Raven, um menu lateral “tudo-em-um” para acessar as notificações, o calendário, controlar o volume dos aplicativos de áudio e vídeo.

- Apenas algumas distribuições trazem o Budgie pronto para usar, como a Solus e o Ubuntu Budgie, mas ele pode ser manualmente instalado em várias outras. 

- Assim como o Gnome, usa o “Nautilus” como o seu gerenciador de arquivos padrão.

![[Pasted image 20231124154914.png]]
#### LXQt

O LXQt é um DE muito leve, com a aparência semelhante ao KDE Plasma, é composto de elementos modulares e flexíveis: muitos usuários consideram que a sua experiência de uso é melhor que a do ambiente LXDE do Lubuntu. Ainda que não esteja presente nas principais distribuições Linux, pode ser instalado manualmente.

- Se você dá preferência ao desempenho e à simplicidade frente à aparência e à customização, o LXQt é uma boa escolha. 

- Ele usa o Openbox como gerenciador de janelas padrão e o “PCManFM” como gerenciador de arquivos.

![[Pasted image 20231124154956.png]]
#### Deepin

O Deepin Desktop Enviroment (DDE) passou por muitas transformações ao longo dos anos. Começou sendo uma modificação do Gnome, mas já possui aplicativos próprios para quase todas as funcionalidades. Sua interface e animações são semelhantes às do macOS.

- Não é leve e pode ser lento, especialmente em computadores mais limitados. O seu gerenciador de arquivos é o “Deepin File Manager”.

![[Pasted image 20231124155042.png]]
#### Pantheon

O Pantheon surgiu com o projeto elementary OS, uma distribuição focada no design e na elegância, apreciado pelos usuários do macOS que desejam migrar para o Linux. Permite organizar o seu fluxo de trabalho em vários espaços, sempre com um painel (dock) na parte inferior.

![[Pasted image 20231124155130.png]]

### Gerenciadores de Empacotamento

 Cada distribuição linux tem um gerenciador de empacotamento próprio, eles servem como compilador de programas muitos desses programas precisam cumprir algumas dependências, ai que entra os gerenciadores aonde eles instalam tudo do que precisa para instalar um programa


#### APT (Advanced Packing Tool)

O APT, Ferramenta de Empacotamento Avançada, é o conjunto de ferramentas que são utilizadas pelas distribuições **Debian/Ubuntu** e derivações para administrar os pacotes, por exemplo, **.deb** de maneira automática, como já explicado anteriormente. O APT é utilizado via linha de comandos, sim, isso significa usar o Terminal!
##### Comandos do APT

> usa-se **apt** antes de qualquer comando

`autoclean` - Apaga arquivos antigos baixados para instalação;

`check` - Verifica se não há dependências quebradas;  

`clean` - Apaga arquivos baixados para instalação;  

`dist-upgrade` - Atualiza a distribuição;  

`update` - Adquire novas listas de pacotes;  

`upgrade` - Faz uma atualização;  

`install` - Instala novos pacotes, especificar o pacote no próximo comando; 

`remove` - Remove um pacote, especificar o pacote no próximo comando;  

`source` - Faz o download de arquivos fonte;  

`build-dep` - Configura as dependências de compilação de pacotes fonte.


#### Yum (Yellow dog Updater Modified)

Assim como o **APT**, o **Yum** é o gerenciador de pacotes de distribuições baseadas em Red Hat/Fedora que utilizam o sistema **RPM** (**R**ed Hat **P**ackage **M**anager), os pacotes são conhecidos pela extensão **.rpm**. O funcionamento é semelhante ao do APT.  
##### Comandos do Yum

> usa-se **yum** antes de qualquer comando

`check-update` - Apenas exibe novas atualizações de pacotes.  

`update` - Exibe e sugere a instalação das novas atualizações.

`list`

 - Lista as informações sobre os pacotes, é complementado com um dos comando abaixo: 
       `available` - Pacotes disponíveis;  
       `extras` - Exibe todos os pacotes instalados no seu sistema que não estão disponíveis nos repositórios listados pelo Yum;  
       `installed` - Exibe os pacotes instalados atualmente no seu computador;  
       `obsoletes` - Exibe os pacotes instalados não utilizados por algum repositório;  
       `updates` - Exibe os pacotes que podem ser atualizados.  

`install` - Assim como no APT, instala uma aplicação com todas dependências;  

`remove` - Desinstala uma aplicação (pacote); 

`search` - Busca pacotes com os termos requisitados.

#### Pacman(PACkage MANager)

É um gerenciador de pacotes popular e poderoso, porém simples, para **Arch Linux** e algumas distribuições Linux pouco conhecidas. 

Mas, de forma mais eficaz, é construído para ser simples para facilitar o gerenciamento de pacotes pelos usuários do Arch. Você pode ler esta visão geral do Pacman que explica em detalhes algumas de suas funções mencionadas acima.
##### comandos do Pacman

> usa-se **pacman** antes de qualquer comando

`-Sy` - sincroniza com os repositórios;

`-Su` - atualiza a distribuição;

`-S pacote` - instala um pacote;

`-R pacote` - remove um pacote;

`-Rs pacote` - remove o pacote junto com as dependências não usadas por outros pacotes;

`-Ss pacote` - procura por um pacote;

`-Sw pacote` - apenas baixa o pacote e não o instala;

`-Si pacote` - mostra informações de um pacote não instalado;

`-Qi pacote` - mostra informações do pacote já instalado;

`-Se pacote` - instala apenas as dependências;

`-Ql pacote` - mostra todos os arquivos pertencentes ao pacote;

`-Qu` - mostra os pacotes que serão atualizados;

`-Q` - lista todos os pacotes instalados;

`-Qo arquivo` - mostra a qual pacote aquele arquivo pertence;

`-Sc` - deleta do cache todos os pacotes antigos ;

`-A arquivo.pkg.tar.gz` - instala um pacote local;

`-Scc` - limpa o cache, removendo todos os pacotes existentes no 
/var/cache/pacman/pkg/.

#### Pamac

O Pamac é o gerenciador de pacotes do **Manjaro**, e também pode ser instalado no **Arch Linux** e seus derivados através do **AUR**. Não sendo apenas mais um nome na lista ao lado do **DNF Dragora** e do **Synaptic**

O Pamac traz diferenciais que fazem com que ele seja até melhor do que muitas lojas de aplicativos distros afora.

##### comandos do Pamac

> usa-se **pamac** antes de qualquer comando

`search` - Procurar por pacotes ou arquivos, pode ser especificado mais de um termo para pesquisa

`list` - Listar pacotes, grupos, repositórios ou arquivos

`info` - Mostrar detalhes dos pacotes, pode ser especificado mais de um pacote

`install` - Instale pacotes a partir de repositórios, local ou URL

`reinstall` - Reinstalar pacotes

`remove` - Remover pacotes

`checkupdates` - Checar de forma segura por atualizações sem modificar as bases de dados.  

`update/upgrade`(Os dois tem a mesma função) - Atualize seu sistema

`clone pacote` - Clonar ou sincronizar arquivos de pacotes de construção do AUR

`build` - Construir pacotes a partir do AUR e os instalar com suas dependências.

`clean` - Limpar o cache de pacotes ou arquivos de compilação

#### Zypper

O **zypper** e **YaST** são os gerenciadores de pacotes padrão para o **OpenSUSE Linux** , que permite instalar pacotes **RPM**. 

O YaST que representa a interface gráfica para manipulação de pacotes. 

Já o zypper é a interface de linha de comando para gerenciar pacotes (instalar, remover e atualizar) no OpenSUSE.
##### comandos do Zypper

> usa-se **zypper** antes de qualquer comando

`repos/lr` -Listar todos os repositórios  

`addrepo/ar`  - Adicionar um novo repositório  

`removerepo/rr` - Remover o repositório especificado  

`refresh/ref` - Atualizar todos os repositórios  

`clean/cc` - Limpar caches dos repositórios 

`install/in` - Instalar pacotes  

`remove/rm` - Remover pacotes  

`remove -u/rm -u` - Remover pacotes + Dependências desnecessárias

`verify/ve` - Verificar a integridade das dependências dos pacotes  

`update/up` - Atualizar os pacotes instalados com versões mais recentes

`list-updates/lu` - Listar as atualizações disponíveis

`sudo patch` - Instalar as correções necessárias  

`list-patches/lp` - Listar as correções disponíveis  

`patch-check/pchk` - Verificar por correções  

`search/se` - Pesquisar por pacotes

`info` - Exibir todas as informações dos pacotes especificados  

`packages/pa` - Exibir todos os pacotes disponíveis

`patterns/pt` - Exibir todos os padrões disponíveis

`products/pd` - Exibir todos os produtos disponíveis  

#### Portage

É um gerenciador de pacotes para o **Gentoo**, uma distribuição Linux menos popular no momento, mas isso não o limita como um dos melhores gerenciadores de pacotes do Linux.

O principal objetivo do projeto Portage é criar um sistema de gerenciamento de pacotes simples e sem problemas para incluir funcionalidades como compatibilidade com versões anteriores, automação e muito mais.

O Portage é similar ao **ports**, o sistema gestor de pacotes do **BSD**, na verdade ele foi desenhado com o ports do **FreeBSD** em mente.

> Portage não usa o modelo convencional como os outros, antes de um comando 
> usa-se **emerge**
##### comandos do Portage

`emerge --sync` - Para sincronizar o portage do Gentoo, que é a "árvore" de pacotes do portage

`emerge-webrsync` - Caso em sua rede, aja um firewall bloqueando o funcionamento do rsync, ainda assim é possível atualizar

`emerge --search pacote` - Se você deseja instalar um pacote no Gentoo, mas não lembra o nome

`emerge --searchdesc pacote` - Para buscar pelo pacote também nas descrições

`emerge pacote` - Para instalar um pacote

`emerge --pretend pacote` - Caso queira saber de forma antecipada quais dependências serão instalados

`emerge --fetchonly pacote` - Caso queira baixar algum pacote, mas não queira instalar

`emerge -unmerge pacote` - Para remover pacotes

`emerge --update world` - Para manter o portage atualizado

`emerge --update --deep world` - Para chegar atualizações das depêndencias

`rc-update add serviço/pacote default` - Para inserir pacote instalado na inicialização do Gentoo

