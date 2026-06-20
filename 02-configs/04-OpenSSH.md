Autor: Daniel Vasconcelos<br>
DVCONNECT: http://dvconnect.com.br<br>
Instagram DVCONNECT: https://www.instagram.com/dv.connect<br>
Blog DVCONNECT: https://dvconnect.com.br/blog/<br>
LinkedIn Daniel Vasconcelos: https://br.linkedin.com/in/vasconcelosdaniel<br>
Github Daniel Vasconcelos: https://github.com/vasconcelosmx<br>
Data de criação: 20/06/2026<br>
Testado, validado e homologado no GNU/Linux Ubuntu Server 26.04.x LTS

Release Ubuntu Server 26.04: https://ubuntu.com/blog/canonical-releases-ubuntu-26-04-lts-resolute-raccoon

Conteúdo estudado nessa configuração:<br>
#01_ Instalado o OpenSSH no Ubuntu Server;<br>
#02_ Verificando os Status do Serviço do OpenSSH;<br>
#03_ Verificando a Versão do OpenSSH Server e Client;<br>
#04_ Verificando a Porta de Conexão do OpenSSH Server;<br>
#05_ Diretórios e Arquivos de Configuração do OpenSSH;<br>
#06_ Segurança do Arquivo Hosts.Deny do TCPWrappers;<br>
#07_ Segurança do Arquivo Hosts.Allow do TCPWrappers;<br>
#08_ Configuração do Arquivo sshd_config do OpenSSH;<br>
#09_ Configuração do Arquivo issue.net (Banner Login);<br>
#10_ Acessando Remoto via Powershell, PuTTY e Terminal.

Site Oficial do OpenSSH: https://www.openssh.com/<br>
Site Oficial do OpenSSL: https://www.openssl.org/<br>
Site Oficial do PuTTY: https://www.putty.org/

**O QUE É E PARA QUE SERVER O OPENSSH:** O *OpenSSH (Open Secure Shell)* é um conjunto de ferramentas que disponibiliza recursos para comunicação segura em ambientes de rede. Ele implementa o *Protocolo SSH (Secure Shell)*, possibilitando conexões criptografadas e protegidas entre computadores em redes públicas ou privadas. É amplamente empregado em sistemas Linux e Unix, mas também está disponível para outros sistemas operacionais, como o Windows.

**O QUE É E PARA QUE SERVER O OPENSSL:** O *OpenSSL* é uma biblioteca open source amplamente utilizada para segurança e criptografia, fornecendo ferramentas para comunicação segura através do *Protocolo TLS/SSL (Transport Layer Security/Secure Sockets Layer)*. Ele é essencial para a criação, gerenciamento e uso de certificados digitais, chaves criptográficas e conexões seguras em servidores, aplicações e redes.

**O QUE É E PARA QUE SERVER O TCP WRAPPERS:** O *TCP Wrappers* é uma recurso de segurança utilizado em sistemas Unix/Linux para controlar o acesso a serviços de rede. Ele permite *Restringir ou Permitir* conexões com base no endereço IPv4/IPv6 do cliente, hostname ou outras regras definidas pelo administrador.

**O QUE É E PARA QUE SERVER O ARQUIVO /ETC/ISSUE:** O /etc/issue é um arquivo de texto simples utilizado em sistemas Linux/Unix. Ele contém uma mensagem de boas-vindas ou aviso exibida antes do prompt de login em terminais locais (TTYs). Quem mostra o conteúdo é o agetty (o programa responsável por gerenciar logins nos consoles locais)..

**O QUE É E PARA QUE SERVER O ARQUIVO /ETC/ISSUE.NET:** O /etc/issue.net é semelhante ao /etc/issue, porém destinado a acessos remotos. Ele contém uma mensagem de identificação, aviso ou banner legal, exibida antes do login remoto via SSH, Telnet, etc. Diferente do /etc/issue, ele não interpreta sequências de escape (\n, \s, \d, etc.) → só mostra texto puro.

**O QUE É E PARA QUE SERVER O BLUE TEAM:** Blue Team é o time de *Defesa em Cibersegurança*. Trata-se da equipe responsável por: *proteger, monitorar e responder a ataques cibernéticos* dentro de uma organização. Eles trabalham de forma **Proativa e Reativa**, com foco total na segurança defensiva.

**O QUE É E PARA QUE SERVER O RED TEAM:** Red Team é o time de *Ataque em Cibersegurança*. Sua principal missão é *simular ataques reais contra a infraestrutura da empresa* para encontrar **Falhas** e testar a eficácia das *defesas (Blue Team)*. Eles são os __`"hackers éticos ofensivos"`__ dentro da organização — tudo é feito com autorização e objetivo de melhorar a segurança.



## 01_ Instalando o OpenSSH Server e Client no Ubuntu Server

**OBSERVAÇÃO IMPORTANTE:** realizar a instalação apenas se durante o processo de instalação o Ubuntu Server não marcou a opção: *Install OpenSSH*, caso contrário o mesmo já está instalado e pré-configurado.

```bash
#atualizando as listas do Apt
#opção do comando apt: update (Resynchronize the package index files from their sources)
sudo apt update

#instalando o OpenSSH Server e Client
#opção do comando apt: install (install is followed by one or more package names)
sudo apt install openssh-server openssh-client openssl lsof
```

## 02_ Verificando o Serviço e Versão do OpenSSH Server e Client no Ubuntu Server
```bash
#consultando o status do OpenSSH Server
#opções do comando systemctl: status (runtime status information), restart (Stop and then start one or more units),
#stop (Stop (deactivate) one or more units), start (Start (activate) one or more units)
sudo systemctl status ssh
sudo systemctl restart ssh
sudo systemctl stop ssh
sudo systemctl start ssh

#analisando logs e mensagens de erro do Servidor do OpenSSH 
#opção do comando journalctl: x (catalog), e (pager-end), u (unit)
sudo journalctl -xeu ssh
```

**OBSERVAÇÃO IMPORTANTE:** Por que sempre é necessário verificar a versão do serviço de rede que você está implementando ou configurando no Servidor Ubuntu Server, devido as famosas falhas de segurança chamadas de: *CVE (Common Vulnerabilities and Exposures)*, com base na versão utilizada podemos pesquisar no site do **Ubuntu Security CVE Reports:** https://ubuntu.com/security/cves as falhas de segurança encontradas e corrigidas da versão do nosso aplicativo, o que ela afeta, se foi corrigida e como aplicar a correção.

```bash
#verificando as versões do OpenSSH Server e Client
#opção do comando sshd e ssh: -V (version)
sudo sshd -V
sudo ssh -V
```

## 03_ Verificando a Porta de Conexão do OpenSSH Server

**OBSERVAÇÃO IMPORTANTE:** no Ubuntu Server as Regras de Firewall utilizando o comando: __` iptables `__ ou: __` ufw `__ está desabilitado por padrão **(INACTIVE)**, caso você tenha habilitado algum recurso de Firewall é necessário fazer a liberação do *Fluxo de Entrada (INPUT), Porta (PORT) e Protocolo (PROTOCOL) TCP* do Serviço corresponde nas tabelas do firewall e testar a conexão.

```bash
#validando a porta padrão TCP-22 do OpenSSH Server
#opção do comando lsof: -n (network number), -P (port number), -i (list IP Address), -s (alone directs)
sudo lsof -nP -iTCP:'22' -sTCP:LISTEN
```

## 04_ Principais Arquivos e Diretórios de Configuração do OpenSSH Server
```bash
/etc/ssh/             <-- Diretório de configuração do OpenSSH Server e Client
/etc/ssh/sshd_config  <-- Arquivo de configuração do OpenSSH Server
/etc/ssh/ssh_config   <-- Arquivo de configuração do OpenSSH Client
/etc/hosts.deny       <-- Arquivo de configuração do Firewall de Aplicação TCPWrappers Deny
/etc/hosts.allow      <-- Arquivo de configuração do Firewall de Aplicação TCPWrappers Allow
/etc/issue.net        <-- Arquivo de configuração do Banner do Ubuntu Server para acesso remoto
/var/log/             <-- Diretório de Logs do Sistema Operacional Ubuntu Server
/var/log/syslog       <-- Log principal do Sistema Operacional Ubuntu Server
/var/log/auth.log     <-- Log principal das autenticações do Sistema Operacional Ubuntu Server
```

## 05_ Aplicando controles de segurança de acesso ao OpenSSH Server
```bash
#abrindo o arquivo de configuração de Negação de Serviço e Host
sudo vim /etc/hosts.deny

#mostrando o número de linha do arquivo hosts.deny
ESC SHIFT :set number <Enter>

#entrando no modo de edição do editor de texto VIM
INSERT
```
```bash
#inserir as informações na linha: 17
#lista de serviço: lista de hosts: comando
#OBSERVAÇÃO: A OPÇÃO ALL: ALL BLOQUEIA TODOS OS SERVIÇOS (DAEMONS) E REDE/HOSTS.
#mais informações veja a documentação oficial em: https://linux.die.net/man/5/hosts.deny
ALL: ALL
```
```bash
#salvar e sair do arquivo
ESC SHIFT :x <Enter>

#abrindo o arquivo de configuração de Liberação de Serviço e Host
sudo vim /etc/hosts.allow

#mostrando o número de linha do arquivo hosts.allow
ESC SHIFT :set number <Enter>

#entrando no modo de edição do editor de texto VIM
INSERT
```
```bash
#inserir as informações na linha: 10
#lista de serviço: lista de hosts: comando
#OBSERVAÇÃO: ALTERAR A REDE OU ENDEREÇO IPv4 CONFORME A SUA NECESSIDADE
#mais informações veja a documentação oficial em: https://linux.die.net/man/5/hosts.allow
sshd: ENDEREÇO_DA_SUA_SUB-REDE/SEU_CIDR
```
```bash
#salvar e sair do arquivo
ESC SHIFT :x <Enter>
```


## 06_ Acessando remotamente o OpenSSH Server via Powershell e pelo software PuTTY
```bash
#acessando o OpenSSH via Powershell
Windows
  Pesquisa do Windows
    Powershell
      ssh seu_usuário@ENDEREÇO_IPV4_SERVIDOR (alterar para o endereço IPv4 do seu servidor)

#acessando o OpenSSH via PuTTY
Windows
  Pesquisa do Windows
    PuTTY

Category
  Session
    Host Name (or IP address): seu_usuário@ENDEREÇO_IPV4_SERVIDOR (alterar para o endereço IPv4 do seu servidor)
    Port: 22
    SSH: On
<Open>

#acessando o OpenSSH via Git Bash no Windows
Windows
  Git Bash
    ssh seu_usuário@ENDEREÇO_IPV4_SERVIDOR (alterar o usuário e endereço IPv4 do seu servidor)

#acessando o OpenSSH via Terminal no Linux Mint
Linux
  Terminal: Ctrl + Alt + T
    ssh seu_usuário@ENDEREÇO_IPV4_SERVIDOR (alterar o usuário e endereço IPv4 do seu servidor)
```

```bash
#consultando informações detalhadas dos usuários logados no Ubuntu Server
sudo w
```

**OBSERVAÇÃO IMPORTANTE 01:** no comando: __`w`__ ele mostra na primeira linha as informações de:<br>
14:28:13   up 16 min,   1 user,   load average: 0,00, 0,00, 0,00<br>

| Valores | Descrição |
|---------|-----------|
| 14:28:13 | Data e Hora Atual do Sistema; |
| up 16 min | Período de Tempo Ativo; |
| 1 user | Número de Usuários Logados; |
| load average: 0,00, 0,00, 0,00 | Médias de Cargas do Sistema (1, 5 e 15 minutos). |

**OBSERVAÇÃO IMPORTANTE 02:** no comando: __`w`__ ele mostra as informações separadas por colunas:<br>
USER   TTY   FROM   LOGIN@   IDLE   JCPU   PCPU   WHAT<br>

| Colunas | Descrição | 
|---------|-----------|
| USER | usuário logado; |
| TTY | terminal do usuário |
| FROM | origem da conexão; |
| LOGIN@ | hora do login do usuário; |
| IDLE | tempo ocioso do usuário; |
| JCPU | tempo de CPU dos processos do TTY; |
| PCPU | tempo de CPU do processo do último comando o usuário; |
| WHAT | processo atual do usuário. |

```bash
#identificando os usuários conectados remotamente no Ubuntu Server
#opção do comando who: -H (heading), -a (all)
sudo who -Ha
```

**OBSERVAÇÃO IMPORTANTE:** no comando: __`who`__ ele mostra as informações separadas por colunas:<br>
NAME   LINE   TIME   IDLE   PID COMMENT   EXIT<br>

| Colunas | Descrição | 
|---------|-----------|
| NAME | usuário logado; |
| LINE | terminal do usuário; |
| TIME | data e hora do login do usuário; |
| IDLE | tempo ocioso do usuário; |
| PID | identificação do processo; |
| COMMENT | origem da conexão do usuário; |
| EXIT | saída do processo. |

```bash
#identificando os usuários conectados no Ubuntu Server
users
```