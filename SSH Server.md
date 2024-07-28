# O que é 

Ferramenta poderosa e versátil que permite a administração e gerenciamento remoto de servidores e outros dispositivos de forma segura.

# Como usar

Para se conectar a um servidor SSH, você pode usar o seguinte comando no terminal:

```sh
ssh usuario@servidor_ip
```

Para criar uma key precisa, guardar a key publica em um bloco de notas em `~/ssh/authorized_keys` e cole a chave publica nesse arquivo 

```sh
ssh-keygen -f ~/.ssh/key -t rsa -b 4096 -C "your_email@example.com"
```

Para copiar um arquivo para o servidor:

```sh
scp arquivo_local usuario@servidor_ip:/caminho/destino
```

## **Túnel SSH (SSH Tunneling)**

- **Port Forwarding:** Criar túneis SSH para redirecionar tráfego de uma porta local para uma porta remota, ou vice-versa. Isso é útil para acessar serviços que estão atrás de firewalls.
- **Acesso Seguro a Redes Privadas:** Usar túnel SSH para acessar redes internas de maneira segura através de uma máquina intermediária.

Para criar um túnel SSH para encaminhar a porta 8080 no servidor remoto para a porta 8080 na máquina local:

```sh
ssh -L 8080:localhost:8080 usuario@servidor_ip
```

## Montar Sistemas de Arquivos Remotamente

**SSHFS (SSH Filesystem):**

- Permite montar um sistema de arquivos remoto via SSH como se fosse local.

```sh
sshfs usuario@servidor_ip:/caminho/remoto /ponto/de/montagem/local
```

Para usar, você precisa ter o pacote `sshfs` instalado. Em sistemas baseados em Debian/Ubuntu, você pode instalá-lo com:


```sh
sudo apt-get install sshfs
```

## Forwarding de Agente SSH

**Encaminhamento de Chave SSH:**

- Encaminha sua chave SSH para permitir que você se conecte a outros servidores a partir da máquina remota sem precisar transferir sua chave privada.


```sh
ssh -A usuario@servidor_ip
```

## Gestão de Portas e Redes

**Reverse Port Forwarding:**

- Redireciona uma porta de um servidor remoto para uma porta local, útil para acessar serviços locais de fora da rede.


```sh
ssh -R porta_remota:localhost:porta_local usuario@servidor_ip
```

## Controle e Monitoramento Remoto de Aplicações

**Screen/Tmux:**

- Utiliza ferramentas como Screen ou Tmux para manter sessões SSH persistentes, permitindo que você desconecte e reconecte a sessões de terminal sem interromper as tarefas em execução.


```sh
screen -S nome_da_sessao
tmux new -s nome_da_sessao
```

## Segurança e Controle de Acesso

**Firewall via SSH:**

- Configurar regras de firewall (iptables) remotamente para proteger o servidor e gerenciar o tráfego de rede.

**Fail2Ban:**

- Integrar Fail2Ban para proteger contra tentativas de login de força bruta, bloqueando IPs suspeitos automaticamente.

## Sincronização de Arquivos e Backups

**Rsync via SSH:**

- Sincronizar diretórios e realizar backups incrementais de forma segura usando rsync.


```sh
rsync -avz -e ssh /diretorio/origem usuario@servidor_ip:/diretorio/destino
```

## Auditoria e Logs

**Monitoramento de Acessos:**

- Configurar e revisar logs de acesso SSH (/var/log/auth.log) para monitorar tentativas de login e atividades dos usuários.

**OSSEC:**

- Utilizar ferramentas de detecção de intrusão como OSSEC para monitorar e alertar sobre atividades suspeitas.

## Proxy de HTTP/HTTPS

**Proxy HTTP/HTTPS:**

- Configurar o SSH para funcionar como um proxy SOCKS, permitindo rotear tráfego web através do servidor SSH para navegar de forma segura e privada.


```sh
ssh -D 8080 usuario@servidor_ip
```

Em seguida, configurar o navegador para usar localhost:8080 como proxy SOCKS.

## Serviços de Autenticação

**LDAP via SSH:**

- Proteger serviços de autenticação LDAP através de túneis SSH.

**Kerberos via SSH:**

- Integrar SSH com sistemas de autenticação Kerberos para melhorar a segurança.

## Gestão de Configurações e Implantação de Software

**Chef/Puppet/Ansible:**

- Utilizar ferramentas de gestão de configuração para automatizar a instalação, configuração e manutenção de software em vários servidores.

**Capistrano:**

- Automação de deploy de aplicações, frequentemente utilizado em ambientes de desenvolvimento web.

## Controle de Acesso Detalhado

**Match Blocks:**

- Usar blocos de configuração “Match” no sshd_config para aplicar regras de controle de acesso específicas com base no usuário, IP de origem, etc.

## Comando Forçado

**Comandos Restritos:**

- Configurar comandos específicos que um usuário pode executar automaticamente ao se conectar, útil para restrição de tarefas específicas.