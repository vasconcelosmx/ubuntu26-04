Autor: Daniel Vasconcelos<br>
DVCONNECT: http://dvconnect.com.br<br>
Instagram DVCONNECT: https://www.instagram.com/dv.connect<br>
Blog DVCONNECT: https://dvconnect.com.br/blog/<br>
LinkedIn Daniel Vasconcelos: https://br.linkedin.com/in/vasconcelosdaniel<br>
Github Daniel Vasconcelos: https://github.com/vasconcelosmx<br>
Data de criação: 20/06/2026<br>
Testado, validado e homologado no GNU/Linux Ubuntu Server 26.04.x LTS

Release Ubuntu Server 26.04: https://ubuntu.com/blog/canonical-releases-ubuntu-26-04-lts-resolute-raccoon

Conteúdo abordado neste procedimento:<br>
#01_ Download da ISO do Ubuntu Server 26.04.x LTS<br>
#02_ Criação da Máquina Virtual utilizando Oracle VirtualBOX<br>
#03_ Ajustes e Configurações da Máquina Virtual DockerUbuntu<br>
#04_ Inicialização da Instalação do Ubuntu Server 26.04.x LTS (seleção da ISO)<br>
#05_ Processo de Instalação e Configuração do Ubuntu Server 26.04.x LTS<br>
#06_ Primeiro acesso ao Ubuntu Server<br>

**Sites de IA (Inteligência Artificial) recomendados para os desafios**<br>
OpenAI ChatGPT: https://chatgpt.com<br>
Microsoft Copilot: https://copilot.microsoft.com<br>
Google Gemini: https://gemini.google.com<br>

**PERGUNTA PARA A IA**

```bash
Prompt-01: qual sistema operacional que mais se destacada em serviços para Container
Local (on-premises) e Cloud (nuvem) no Brasil e no Mundo, por que ele é o mais usado?
```

```bash
Prompt-02: qual distribuição GNU/Linux lidera o mercado de servidores locais (on-premises)
e nuvem (cloud) no Brasil e no mundo? por que essas distribuições são as mais usadas?
```

```bash
Prompt-03: quais as principais Big Techs no Brasil e no mundo que utiliza o GNU/Linux?
```

```bash
Prompt-04: quais as principais Big Techs no Brasil e no mundo utiliza Container?
```

**O QUE É E PARA QUE SERVE O ON-PREMISES:** O termo "on-premises" define uma infraestrutura de TI instalada fisicamente dentro da organização. Nesse modelo, servidores, bancos de dados, aplicações e demais recursos tecnológicos permanecem hospedados, administrados e mantidos pela própria equipe interna, em vez de serem executados em plataformas de nuvem pública como AWS, Azure ou Google Cloud.

**O QUE É E PARA QUE SERVE O CLOUD:** Cloud Computing (Computação em Nuvem) é um modelo de tecnologia que possibilita o acesso remoto a servidores, armazenamento, bancos de dados, redes e aplicações por meio da internet. Ao invés de manter toda a infraestrutura física localmente (on-premises), os recursos ficam hospedados em datacenters de provedores especializados, como AWS, Microsoft Azure e Google Cloud.

**O QUE É E PARA QUE SERVE A CANONICAL:** A Canonical Ltd. é uma empresa britânica de tecnologia fundada por Mark Shuttleworth em 2004. Sua principal atuação está relacionada ao desenvolvimento e suporte do Ubuntu, uma das distribuições Linux mais utilizadas mundialmente.

**O QUE É E PARA QUE SERVE O UBUNTU SERVER:** O Ubuntu Server é uma edição do Ubuntu desenvolvida especificamente para ambientes de servidores. Baseado no Debian, destaca-se pela estabilidade, segurança, ampla compatibilidade e facilidade de administração, sendo uma das distribuições Linux mais adotadas em datacenters e ambientes corporativos.

**O QUE É E PARA QUE SERVE O LTS:** LTS significa Long-Term Support (Suporte de Longa Duração). Trata-se de uma modalidade de versão que recebe correções, atualizações de segurança e suporte por um período prolongado, normalmente entre 5 e 10 anos, dependendo da política do projeto.

**O QUE É E PARA QUE SERVE O UBUNTU SERVER MINIMAL:** O Ubuntu Server Minimal é uma versão reduzida do Ubuntu Server, criada para disponibilizar apenas os componentes essenciais do sistema operacional. Essa abordagem permite maior personalização do ambiente, com a instalação apenas dos pacotes e serviços realmente necessários para cada cenário.

## 01_ Download da ISO do Ubuntu Server 26.04.x LTS

Link para download do Ubuntu Server: https://releases.ubuntu.com/26.04/

1. Versão da imagem ISO: ubuntu-26.04-server-amd64.iso<br>
2. Arquitetura utilizada: AMD64 (64-bit)<br>
3. Método de instalação: DVD Image (ISO) Installer<br>

## 02_ Criação da Máquina Virtual no Oracle VirtualBOX

1. Download do Oracle VirtualBOX: https://www.virtualbox.org/wiki/Downloads<br>

**OBSERVAÇÃO:** Recomenda-se utilizar o Oracle VirtualBOX Gerenciador versão 7.x ou superior.

## 04_ Iniciando a Instalação do Ubuntu Server 26.04.x LTS (localizando a ISO) no Oracle VirtualBOX

```bash
01) Selecionar a Máquina Virtual: DockerUbuntu
<Iniciar>

02) VirtualBOX VM
    DVD: <Outro>

    #LOCALIZE E SELECIONE A IMAGEM ISO DO UBUNTU SERVER 26.04.x LTS

<Montar e Tentar Novo Boot>
```

## 05_ Instalação e Configuração do Ubuntu Server 26.04.x LTS

Link Oficial da Documentação de Instalação do Ubuntu Server:
https://ubuntu.com/server/docs/installation

**OBSERVAÇÃO IMPORTANTE:** O processo inicial de boot do Ubuntu Server leva aproximadamente **`30 (trinta) segundos`** para iniciar automaticamente a instalação padrão, caso nenhuma opção seja alterada.

**OBSERVAÇÃO:** Para interromper o *Boot Inicial do Ubuntu Server*, pressione a tecla **`<Seta para Baixo>`**.

**DICA:** Conhecendo as opções de inicialização disponíveis no Ubuntu Server.

| Opção de Boot                         | Descrição                                                                                                                     |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Try or Install Ubuntu Server**      | Executa o instalador padrão do Ubuntu Server. Recomendado para a maioria dos cenários.                                        |
| **Ubuntu Server with the HWE kernel** | Realiza a instalação utilizando o kernel HWE (Hardware Enablement), oferecendo suporte ampliado para hardwares mais recentes. |
| **Test memory**                       | Inicia o Memtest86+ para validação e testes da memória RAM do equipamento.                                                    |

```bash
05) Network connections
    enp0s3 eth - (a identificação lógica da interface de rede pode variar conforme o equipamento)

    DHCPv4 10.133.44.XXX/24 (adequar ao seu ambiente)

    #OBSERVAÇÃO IMPORTANTE: CONFIRA O ENDEREÇO IPv4 UTILIZADO EM SUA REDE
    #LOCAL PARA AJUSTAR AS CONFIGURAÇÕES DE ACORDO COM O SEU CENÁRIO.
```

```bash
07) Configure Ubuntu archive mirror
    Mirror: http://archive.ubuntu.com/ubuntu

    #OBSERVAÇÃO IMPORTANTE: CASO DESEJE UTILIZAR O REPOSITÓRIO OFICIAL DOS
    #ESTADOS UNIDOS, SUBSTITUA A URL:
    #http://br.archive.ubuntu.com/ubuntu
    #POR:
    #http://us.archive.ubuntu.com/ubuntu
```

```bash
09) Storage configuration

    USED DEVICES

    #SELECIONE O LV (LOGICAL VOLUME) DA PARTIÇÃO RAIZ (/)
    #PARA AJUSTAR O TAMANHO DO VOLUME LÓGICO.

    ubuntu-lv new, to be formatted as ext4, mounted at / 24G <Enter>
```

```bash
10) Profile setup

    #OBSERVAÇÃO: PERSONALIZE AS INFORMAÇÕES DE HOSTNAME,
    #USUÁRIO E SENHA CONFORME O SEU AMBIENTE.

    Your name: Seu Nome e Sobrenome
    Your servers name: ctnseunome
    Pick a username: seu_usuario
    Choose a passwords: sua_senha
    Confirm your passwords: sua_senha
```

## 06_ Acessando o Ubuntu Server pela primeira vez via Terminal

**OBSERVAÇÃO:** AGUARDE A CONCLUSÃO TOTAL DA INICIALIZAÇÃO DO UBUNTU SERVER. DURANTE O PRIMEIRO BOOT SERÃO GERADAS AS CHAVES DE AUTENTICAÇÃO DO SSH SERVER. APÓS O PROCESSO, PRESSIONE <ENTER> PARA EXIBIR A TELA DE LOGIN.

```bash
01) Tela de Login do Ubuntu Server

    Ubuntu 26.04.3 LTS ctnseunome tty1

      ctnseunome login: seu_usuario <Enter>
      Password: sua_senha <Enter>

    seu_usuario@ctnseunome:~$

    #PRIMEIRO ACESSO AO TERMINAL DO UBUNTU SERVER
```
