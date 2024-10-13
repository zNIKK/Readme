## Comandos principais

### Informações

#### $`pwd` (Print Working Directory)

```bash
/home/usuario
```

- Exibe o diretório atual completo

#### $`ls` (List)

- Lista informações sobre os ARQUIVOs (no diretório atual por padrão).

#### Algumas opções do comando

- **-l/--long** : Listagem mais completa de um diretório contendo quantas pastas possui, usuário proprietário do arquivo e de quando foi criado.
- **-h** : Usado para exemplificar os bytes de um arquivo.
- **-a/--all** : Usado para mostrar TODAS as pastas inclusive as ocultas.


#### $``lsb_release``(Linux Standard Base)
```bash
lsb_release [opções]
```

Este comando exibe informações sobre a **distribuição** Linux usada

##### Algumas opções do comando

- **-a** ou **−−all** : exibe todas as informações disponíveis.
- **-h** ou **−−help** : exibe as opções do comando.
- **-i** ou **−−id** : identifica a distribuição.
- **-c** ou **−−codename** : exibe o nome de código da distribuição.
- **-d** ou **−−description** : descreve a distribuição instalada.
- **-r** ou **−−release** : informa o número da versão instalada.
- **-v** ou **−−version** : mostra a versão do aplicativo.

#### $``lsusb``(Universal Serial Bus)

```bash
lsusb [opções]
```

Este comando exibe informações sobre dispositivos USB

##### Algumas opções do comando

- **-v, −−verbose** : mostra informações detalhadas.
- **-D device** : exibe informações apenas do dispositivo especificado.
- **-V, −−version** : exibe informações sobre o aplicativo.
- **-h** ou **−−help** : exibe informações sobre o comando.

#### lsscsi

```
lsscsi [opções]
```

Este comando lista os dispositivos scsi.

##### Algumas opções do comando

- **-l** ou **−−long** : exibe informação adicional para cada dispositivo SCSI.
- **-L** ou **−−list** : exibe informação adicional nos pares _=_.
- **-p** ou **−−protection** : exibe informação adicional sobre a integridade dos dados.
- **-v** ou **−−verbose** : exibe o nome dos diretórios de onde as informações foram retiradas.
- **-h** ou **−−help** : exibe informações sobre o comando.
- **-V** ou **−−version** : exibe  a versão do aplicativo.

#### lscpu

```
lscpu [opções]
```

Este comando exibe informações sobre a arquitetura da CPU.

##### Algumas opções do comando

- **-x** ou **–parse** : usa máscara hexadecimal para exibir as CPUs.
- **-h** ou **−−help** : exibe informações sobre o comando.
- **-V** ou **−−version** : exibe  a versão do aplicativo.

#### lsblk
```
lsblk [opções] [dispositivo]
```

Este comando exibe informações sobre as partições do HD e outros dispositivos de armazenamento como pen drives e CDs em formato de árvore.

##### Algumas opções do comando

- **-a** ou **−−all** : lista também dispositivos vazios (que por padrão não são exibidos).
- **-i** ou **−−ascii** : usa caracteres ASCII para a formatação da árvore.
- **-l** ou **−−list** : produz a saída em formato de lista.
- **-S** ou **−−scsi** : considera apenas os dispositivos SCSI.
- **-h** ou **−−help** : exibe informações sobre o comando.
- **-V** ou **−−version** : exibe  a versão do aplicativo.
#### lshw

```
lshw [opções]
```


Este comando exibe informações sobre o hardware.

##### Algumas opções do comando

- **-version** : exibe a versão do aplicativo.
- **-help** : exibe as opções do aplicativo.
- **-businfo** : mostra informações sobre barramento, detalhando endereços SCSI, USB, IDE e PCI.

#### ``lsmod``(list module)

Este comando lista os **módulos** do **kernel** que estão carregados na memória.

#### $``lsof``(list open files)

```
lsof [opções]
```
Este aplicativo lista os **arquivos** abertos (em uso) pelos **processos.**

##### Algumas opções do comando

- **−−help** : mostra as opções do aplicativo.
- ``-i [endereço] [tipo]`` : mostra a lista dos arquivos abertos que estão associados ao endereço de Internet especificado. Se nenhum endereço é especificado, o comando fornece a lista todos os arquivos abertos associados aos endereços de internet. Pode-se também definir um tipo de comunicação como porta,  protocolos IPv4 e IPv6 e tipo de socket.    
- **-s** : mostra o tamanho do arquivo.
- **-p PID** : mostra os arquivos abertos do processo com o [**PID**](https://guialinux.uniriotec.br/pid/) informado.
- **-u usuário** : mostra apenas informações de um determinado usuário.
- **-U** : lista os sockets Unix.
- 
#### $`whoami` 

- Comando para saber que usuário está na máquina

Retorno:
```
user
```

#### $`hostname`

- Comando para saber o nome da máquina

Retorno:
```bash
ubuntu
```
##### Algumas opções do comando

- **-I** : Mostra todas as interfaces de IPs na máquina

### $`chown` (Change Owner)

Este comando permite alterar o nome do dono e/ou do grupo de **arquivos**

##### Algumas opções do comando

- **-c** : informa quais arquivos estão sendo alterados.
- **-h** : altera o link, não o arquivo apontado pelo link.
- **-v** : informa quais arquivos estão sendo processados (não necessariamente alterados).
- **-R** : altera, recursivamente, dono e/ou grupo de arquivos.
- **−−help** : exibe opções do comando.
- **−−version** : exibe informações sobre o aplicativo.

### $`mhwd-kernel`

```bash
mhwd-kernel [opções] [kernel]
```

Instala e remove um novo kernel. Mostra todos os kernels instalados e os disponíveis

#### Parâmetros

##### `-i`

- instala um novo kernel

##### `-l`

- Lista todos os kernels disponíveis

##### `-li`

- Lista todos os kernels instalados

##### `-r`

- remove um kernel

### $`clear` (Limpar)

- limpa o terminal

> CTRL + L

### $`cd` (Change Directory)

```
cd [options] [directory]
```
- navega pelos diretórios

#### Variáveis

- **~ (Tilde Expansion)** : vai para o HOME
- **/ (root)** : vai para o diretório raiz
- **..** : volta um diretório

### $`echo`

- Este comando mostra texto na saída padrão seguido por uma nova linha.

##### Algumas opções do comando

- **-n** : não adiciona uma nova linha após mostrar os argumentos.
- **-e** : habilita interpretação dos códigos de escape após barra invertida.
- **-E** : suprime explicitamente a interpretação de códigos de escape após barra invertida.

São exemplos de códigos de escape:

- **\a** : alerta (Sino).
- **\b** : retroceder.
- **\c** : suprime próxima saída.
- **\e** : caractere de escape.
- **\f** : alimentação de página (FF).
- **\n** : nova linha (NL).
- **\r** : retorno de carro (CR).
- **\t** : tabulação horizontal.
- **\v** : tabulação vertical.

#### Exemplos

```bash
echo teste
```  
apenas mostra a palavra “teste” na saída padrão, enquanto o comando

```bash
echo
```
mostra uma linha em branco.
  
- Este comando pode ser usado para exibir todos os nomes de arquivos de um diretório em ordem alfabética. Por exemplo,
```bash
echo /*
```

- lista o conteúdo do diretório **raiz**.
```bash
echo -e /etc/* “\n” /*
```
mostra o conteúdo do diretório **/etc**, define uma nova linha com o código de escape **“\n”** e, em seguida, mostra o conteúdo diretório **raiz**.

> Este comando pode também ser utilizado na programação **shell** para escrever mensagens na saída padrão. Por exemplo,
```bash
echo ‘erro de execução’
```
mostra a mensagem definida entre aspas simples no terminal do usuário.
 
- Para verificar o conteúdo da **variável de ambiente(PATH)**, basta digitar na linha de comando
```bash
echo “$PATH”
```

### Manipulação de Arquivos

#### $`rmdir` (Remove Diretory)

- Remove um diretório

#### $`mkdir` (Make Directory)

- Cria um arquivo

#### $`touch`

```shell
touch [opções] arquivo
```

- cria um arquivo, porem se o arquivo já existe ele vai atualizar o acesso a modificação da hora atual sem mudar seu conteúdo. 

##### Algumas opções do comando

- **-a** : altera apenas a data do último acesso.
- **-c, −−no-create** : não cria qualquer arquivo.
- **-m** : altera apenas a data de modificação do arquivo.
- **-t [[CC]YY]MMDDhhmm[.ss]** : define o tempo a ser usado pelo utilitário ao invés do tempo atual.
- **−−help** : exibe as opções do utilitário.
- **−−version** : mostra informações sobre o arquivo.
##### Exemplos

- Se o arquivo _teste_ não existe, o comando
```bash
touch teste
```
cria um arquivo vazio.

- Para alterar as datas de modificação e de acesso do arquivo _teste_ para 12:31 do dia 01/05 do ano corrente, digite

```bash
touch -t 05011231 teste
```


- Para atualizar as datas de todos os arquivos do diretório corrente, digite
```bash
touch *
```


##### Observações

- Se as opções não especificarem qual data deve ser alterada, o utilitário altera as duas datas do arquivo: acesso e modificação.
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

### $`ps`(process)

- lista processos do sistema

> ESSE COMANDO PODE SER SUBSTITUIDO POR: `htop` ou `bashtop`


#### Parâmetros

##### `aux`

- inclui os processos que não foram iniciados pelo usuário

### $``df``(disk free)

```bash
df [opções]
```

- Este comando exibe informações sobre espaço, livre e ocupado, das partições do sistema.

##### Algumas opções do comando

- **-a** : inclui também na listagem os sistemas de arquivos com zero blocos.
- **−−help** : exibe as opções do comando.
- **-i** ou **−−inodes** : exibe informações sobre [**inode**](https://guialinux.uniriotec.br/inode/).
- **-k** : lista o tamanho dos blocos em kbytes.
- **-m** : lista o tamanho dos blocos em Mbytes.
- **-t tipo** : especifica o tipo dos sistemas de arquivos a serem listados.
- **-T** : exibe o tipo dos sistemas de arquivos listados.
- **-x tipo** : especifica o tipo dos sistemas de arquivos que não deve ser listado.
- **−−version** : exibe informações sobre o aplicativo.

> ESSE COMANDO ESTÁ DEFASADO USE O COMANDO: `ncdu`


### $`ln`(link)

```bash
ln [opções] origem destino
```
- Este comando cria ligações (_links_) entre **arquivos**. Há dois conceitos de _ligação_ em sistemas Unix:

- **Ligação direta** – define mais um nome para um arquivo (um arquivo pode ter diversos nomes). O arquivo será removido  do disco quando o último nome for removido. Não há algo como um nome original, todos os nomes tem o mesmo _status_.

- **Ligação simbólica** ou **dymlink** – define um caminho para um arquivo. Ligações simbólicas podem apontar para arquivos em diferentes sistemas de arquivo e não necessitam apontar para arquivos que realmente existem.

#### Algumas opções do comando

- **-d** : cria uma ligação direta (_hard link_), é o padrão.
- **-L** ou **−−logical** : cria uma ligação para um link simbólico.
- **-s** : cria uma ligação simbólica (_soft link_). Um atalho para o arquivo original
- **-v** : mostra o nome de cada arquivo antes de criar o link.

#### Exemplos

- O comando abaixo cria, no diretório _teste_, ligação direta para os arquivos do diretório atual cujos nomes começam por _aula_. Isto significa que cada arquivo terá dois nomes: um fica no diretório atual e o outro no diretório _teste_. As alterações feitas usando um dos nomes serão vistas quando se acessar o arquivo usando o outro nome. Se um dos nomes for apagado, o arquivo continuará existindo com o outro nome.

```shell
ln aula* teste/.
```
Quando dois nomes representam o mesmo arquivo, eles possuem o mesmo **inode**. Para ver os inodes dos arquivos de um diretório, basta digitar

```bash
ls -i
```

- Para criar, no diretório atual, um _link_ simbólico chamado _teste_ para o arquivo _/etc/passwd_, basta digitar

```bash
ln -s /etc/passwd teste
```


É possível então usar o comando **ls -l** para ver as características do arquivo criado.

```bash
lrwxrwxrwx 1 aluno aluno 11 Dez 31 16:17 teste -> /etc/passwd
```

Note que temos duas indicações de que se trata de um _link_ simbólico: o primeiro caractere das permissões é “l” e o arquivo _teste_ aponta para o arquivo _/etc/passwd_.

### $``alias``

```bash
alias [comando_novo]='[comando_original]'
```

- Abrevia comandos longos e complexos, para um comando da sua escolha

- esse tipo de alias só funciona uma vez por terminal para que podemos deixar os alias permanentes precisamos editar o arquivo `~/.bash_aliases` ou o arquivo `~/.bashrc`. 

- Meu arquivo de alias: [[bashrc]]

- depois use o comando `source ~/.bash_aliases`
### $`grep`(Globally Search a Regular Expression and Print)

- Localizar a palavra no arquivo

- Usado com expressões regulares

- Exemplo:  `ps aux | grep bash`
- localiza a palavra "bash" nos processos

- (Comando Primitivo) - Usamos o `ag` ao invés desse

### $`Find`

```bash
find [caminho] [expressão]
```
Este comando pesquisa **arquivos** em uma hierarquia de diretórios.

#### Algumas Opções

- **.** : Encontra arquivos a partir da pasta atual
- **-name arquivo** : Nome do arquivo que você quer procurar
- **-daystart** : medem o tempo do início do dia ou de até 24 horas atrás.
- **-depth** : processa o conteúdo de cada diretório antes do diretório em si.
- **-follow** : resolve as ligações simbólicas.
- **-help**: imprime um resumo do uso das linhas de comando de _find_ e finaliza.
- **-inum n** : acha arquivo com **inode** _n_.
- **-maxdepth n** : desce no máximo em _n_ níveis (um inteiro não negativo) de diretórios sob os argumentos da linha de comando. A opção “_-maxdepth 0_” significa a aplicação dos testes e ações somente nos argumentos da linha de comandos.
- **-mindepth n** : não aplica qualquer teste ou ação a níveis menores que _n_ níveis (um inteiro não negativo). A opção “_-mindepth 1_” significa testar todos os arquivos exceto os argumentos da linha de comandos.
- **-version** : lista o número da versão do comando _find_ e finaliza.
- **-xdev** : não desce diretórios em outros sistema de arquivos.

### $`awk`

- Linguagem de programação interpretada voltada a processar dados e textos

### $systemctl

```bash
systemctl [status] [service]
```
- Usado para iniciar, parar ou ver um banco de dados em serviço

- Exemplo: `sudo systemctl start postgresql`
- iniciar o postgresql

Usado também para "resetar", "startar" ou ver um status do aplicativo linux

```sh
sudo systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
```

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

# Melhores programas



