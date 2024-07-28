
## Ubuntu server 
### Instalação

Baixe a iso no site oficial: https://ubuntu.com/download/server

Em um pendrive bootavel, siga as instruções de instalação abaixo:

```html
01. Try or Install Ubuntu Server
<Enter>


02. Use UP, DOWN and ENTER keys to select your language
	English (recomendado utilizar sempre a opção em Inglês)
<Enter>

03. Keyboard configuration
	Layout: [English (US)] ou [Portuguese (Brazil)] (altere conforme a sua necessidade)
	Variant: [English (US)] ou [Portuguese (Brazil)] (altere conforme a sua necessidade)
<Done>

04. Choose type of install
	(X) Ubuntu Server (DEFAULT - Selecionado)
	( ) Ubuntu Server (minimized)
	Additional options
		[ ] Search for third-party drivers
<Done>

05. Network connections
	enp0s3 eth (o nome lógico da placa de rede muda de equipamento para equipamento)
	DHCPv4 172.16.1.XXX/24 (altere conforme a sua necessidade)
	OBSERVAÇÃO IMPORTANTE: VERIFICAR O ENDEREÇO IPv4 QUE VOCÊ ESTÁ USANDO NA SUA REDE 
	INTERNA PARA ADAPTAR NO SEU CENÁRIO.
<Done>

06. Configure proxy
	Proxy address: (Default)
<Done>

07. Configure Ubuntu archive mirror
	Mirror: http://br.archive.ubuntu.com/ubuntu
	OBSERVAÇÃO IMPORTANTE: CASO QUEIRA TROCAR O MIRROR DO UBUNTU DO BRASIL PARA O
	OFICIAL NO US, SUBSTITUA A URL DE: http://br.archive.ubuntu.com/ubuntu PARA A
	URL: http://us.archive.ubuntu.com/ubuntu
<Done>

08. 

09. Guided storage configuration
	(X) Use an entire disk (Default)
		[VBOX_HARDISK local disk 50.000G]
		(X) Set up this disk as an LVM group (Default)
<Done>

10. Storage configuration
	USED DEVICES
		ubuntu-lv	new, to be formatted as ext4, mounted at /	24G <Enter>
			Edit <Enter>
				Name: ubuntu-lv
				Size (max 47.996G): 47.996G
				Format: ext4
				Mount: /
			<Save>
<Done>
	Confirm destructive action
<Continue>

11. Profile setup
	OBSERVAÇÃO: ALTERAR OS DADOS DO NOME DO SERVIDOR, USUÁRIO E SENHA PARA O SEU CENÁRIO.
	Your name: Seu Nome e Sobrenome <Tab>
	Your server's name: wsvaamonde <Tab>
	Pick a username: vaamonde <Tab>
	Choose a passwords: pti@2018 <Tab>
	Confirm your passwords: pti@2018
<Done>

12. Upgrade to Ubuntu Pro
	(X) Skip Ubuntu Pro setup for now
<Continue>

13. SSH Setup
	Install OpenSSH server: ON (Habilitar) <Space>
	Import SSH identity: No (Default)
<Done>

14. Featured Server Snaps
<Done>

15. Install complete!
<Reboot Now>

16. Please remove the installation medium, then press ENTER:
<Enter>
```

## Primeiros passos

### Testar internet

#### `$ ping 8.8.8.8`

verificar se a parte de roteamento, regras de firewall, etc... está saindo da minha rede e está acessando.

#### `$ ping google.com`

verificar se o serviço de **dns** está funcionando

### Atualizar

#### `$ sudo apt update`

Atualizando as Listas sources.list do Apt ou Apt-Get no Ubuntu Server

#### `$ sudo apt list --upgradable`

Verificando todos os pacotes a serem utilizados no Ubuntu Server

#### `$ sudo apt upgrade`

Atualizando todos os software no Ubuntu Server

##### `$ sudo apt full-upgrade`

 executa a função de atualização, mas removerá os pacotes atualmente instalados se isso for necessário para atualizar o sistema como um todo

##### `$ sudo apt dist-upgrade`

Força atualizações completa de todos os softwares, dependências, além de atualizações de kernel e de softwares

#### `sudo apt autoremove`

Remove pacotes desnecessários como memória em cache ou dependências inutilizáveis.

#### `$ sudo apt autoclean`

Limpar repositórios locais e pacotes desnecessários no Ubuntu Server

#### `$ sudo apt clean`

Limpando o cache local do sources.list no Ubuntu Server

# Configurando Hosts e Netplan

### Editando arquivo de configuração do Hostname

- `$ sudo vim /etc/hostname`

adicionar o nome de domínio na linha 1:
`tsukasa.pti.intra`

> salvar e sair do arquivo
> `ESC + : + x`

### editando o arquivo de configuração do Hosts

- `$ sudo vim /etc/hosts`

```
127.0.0.1    localhost.localdomain  localhost
127.0.1.1    tsukasa.pti.intra      tsukasa
192.168.1.6  tsukasa.pti.intra      tsukasa
```

### Instalando os principais software de rede no Ubuntu Server

atualizando as lista do sources.list e instalando os pacotes e ferramentas de rede

```bash
sudo apt update
sudo apt install bridge-utils ifenslave net-tools
```

### Verificando informações do Hardware de Rede no Ubuntu Server

```bash
sudo lspci -v | grep -i ethernet
```

verificando os detalhes do hardware de Placa de Rede instalada

```bash
sudo lshw -class network
```

### Verificando as informações de Endereços IPv4 no Ubuntu Server

verificando as configurações de endereçamento IP da Placa de Rede instalada

```bash
# opção do comando ifconfig: -a (all)

sudo ifconfig -a
sudo ip address show
```

verificando as informações de cache dos Servidores DNS (resolução de nomes)

```bash
sudo resolvectl
```

### verificando as configurações de Gateway (route)

opção do comando route: -n (number)

```bash
sudo route -n
sudo ip route
```

### listando o conteúdo do diretório do Netplan

Listando o conteúdo do diretório do Netplan

```bash
ls -lh /etc/netplan/
```

Fazendo o backup do arquivo de configuração original do Netplan

```bash
sudo cp -v /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.old
```

```c
#bloco de configuração da rede
network:
  #bloco de configuração do protocolo Ethernet
  ethernets:
    #configuração da Interface Física (Nome Lógico)
    enp0s3:
    #desabilitando o suporte ao DHCP Client
    dhcp4: false
    #desativando o suporte ao IPv6
    #OBSERVAÇÃO IMPORTANTE: utilizar essa opção somente se você não está usando
    #na sua rede o recurso do IPv6
    link-local: []
    #alterar o endereço IPv4 para o seu cenário
    #OBSERVAÇÃO IMPORTANTE: configuração do Endereço IPv4 dentro de Colchetes
    addresses: [172.16.1.20/24]
    #alterar o gateway padrão para o seu cenário
    #OBSERVAÇÃO IMPORTANTE: a opção de Gateway4 foi descontinuada, recomendo
    #utilizar as opções de Routes do Netplan para configurar o Gateway padrão
    #gateway4: 172.16.1.254
    routes:
      #configuração da rota padrão (cuidado com o traço antes do to)
      - to: default
        #configuração do endereço IPv4 do Gateway
        via: 172.16.1.254
    #configuração dos servidores de DNS Preferencial e Alternativo
    nameservers:
      #alterar os servidores DNS para o seu cenário
      #OBSERVAÇÃO: configuração do Endereço IPv4 dentro de Colchetes e separados
      #por vírgula, recomendo pelo menos dois DNS Server serem configurados ou 
	  #somente o endereço do Servidor de DNS Local d Rede.
      addresses: [8.8.8.8, 8.8.4.4]
      #alterar a pesquisa de domínio para o seu cenário
      #OBSERVAÇÃO: configuração da pesquisa de Domínio dentro de Colchetes
      search: [pti.intra]
  #fim do bloco de configuração do protocolo Ethernet versão 2
  version: 2
```

## Redimensionamento de discos

### LVM

- O LVM cria um grande "disco virtual" formado por discos físicos, permitindo o gerenciamento de volumes lógicos.

```
/ -> /var -> /home -> /tmp
```

#### Vantagens 

A grande vantagem do uso do LVM é permitir o re
## Configurações principais

### Personalizar a tela inicial do linux

1. Em ``/etc`` use o comando ``ls issue*``
2. Em seguida use ``cat issue``
3. Faça um backup dos arquivos `ìssues`, ou algum arquivo de configuração com o comando `cp issues issues.bkp`
4. faça as devidas alterações em `issues` e divirta-se


# Dicas

## Como resetar a senha do root no Servidor Linux

**É necessário que você tenha contato físico com o servidor**

1. Entre no grub e aperte o botão E

2. vai até a linha que está escrito linux e localize as letras "ro" atrás do "quiet"

>Esse "ro" significa "read only"

3. delete o "ro" e o "quiet" e deixe como "rw init=/bin/bash"

> Isso irá especificar para o grub iniciar o linux como terminal

4. depois que o sistema entrar como terminal, mude a senha com o seguinte comando `passwd`, coloque a sua senha e você acaba de mudar a senha do servidor

