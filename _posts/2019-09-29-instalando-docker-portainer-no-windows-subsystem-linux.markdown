---
layout: post
title: Instalando Docker e Portainer no Windows Subsystem Linux
date: '2019-09-29 21:56:28 -0400'
---

Este tutorial o guiará na instalação do Docker dentro de um Windows Subsystem Linux (WSL) para que você não tenha que usar VirtualBox ou Hyper-V para criar as máquinas. Eu mesmo tive muitos problemas ao tentar ativar os Containers Linux utilizando o Docker Desktop, e essa foi a solução mais efetiva que encontrei para contorná-los. Isso além de utilizar melhor os recursos de hardware já que a implementação deste Docker é nativo do Linux!

A containerização é parte integrante do dia-a-dia dos DevOps. É a melhor opção quando se tenta criar um ambiente seguro, replicável e escalável para se trabalhar com equipes de desenvolvimento de qualquer porte. O uso de container agiliza tanto o processo de criação de software, pela distribuição dos arquivos de configuração de um servidor compatível com as necessidade do software, quanto o processo de instalação e gerenciamento de um servidor de aplicação em produção.

Se você não sabe o que são essas coisas que falei até aqui, pare e leia agora sobre [WSL](https://medium.com/joaorobertopb/wsl-linux-nativo-no-windows-sem-vm-1cd6e352c995), 

### Pré-requisitos

Para iniciar você precisará dos seguintes softwares instalados:

- Windows 10, Versão 1803, Build 1734 e qualquer outro acima deste
- Ubuntu for WSL 16.0.4 LTS

Antes de iniciar, quero deixar bem claro que ainda não testei essas configurações em outros subsistemas, pois demorei um bom tempo para conseguir fazer tudo funcionar na versão. É importante que a versão do Windows seja esta ou superior por conta de uma alteração no kernel do WSL que habilita o uso de _cgroups_ que o Docker utiliza para gerenciar os recursos do seu sistema dentro dos containers.

### Instalação do Docker no WSL

Se você já tiver tentado instalar o Docker no WSL, livre-se dessa instalação. Para isto, abra o `bash` e execute:

```bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

Em seguida, faremos a instalação do **Docker Community Edition** através do `apt-get` para que seja instalada uma versão específica do Docker conhecida por rodar no WSL sem ter que compilar o código na mão.

```bash
# Comece atualizando seu apt
$ sudo apt-get update

# Instale os binários necessários para baixar outros repositórios
$ sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common

# Baixe o repositório do próprio site do Docker e adicione
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Atualize novamente agora com o repositório do Docker adicionado
$ sudo apt-get update
```

Depois disso você instalará a versão específica do Docker que precisamos:

```bash
$ sudo apt-get install docker-ce=17.09.0~ce-0~ubuntu
```

Caso você deseje testar se este procedimento funciona em outra Distro, rode o seguinte comando para verificar as versões do Docker disponíveis para ela:

```bash
$ apt list -a docker-ce
```

Feita a instalação, vamos adicionar seu usuário atual no grupo `docker` para que seja permitido utilizar o **Docker Engine** que estará rodando no sistema como _root_.

```bash
sudo usermod -aG docker $USER
```

### Inicializando o serviço do Docker com o Windows

A partir daqui vamos configurar seu computador para que toda vez que o Windows iniciar, o serviço do Docker será automaticamente executado dentro do WSL. Para que isto seja possível, será necessário executar uns comandos a partir de um shell com privilégios de administrador toda vez que o Windows arrancar. Então não é algo assim tão simples.

Crie um script em `/usr/local/sbin/`:

```bash
$ sudo nano /usr/local/sbin/start_docker.sh
```

que conterá os seguintes comandos para executar o serviço do Docker e desabilitar a verificação TLS no futuro quando partirmos para a configuração do Portainer:

```bash
#!/usr/bin/env bash

export DOCKER_TLS_VERIFY=1
sudo cgroupfs-mount
sudo dockerd -H tcp://0.0.0.0: -H unix:///var/run/docker.sock
```

Salve tudo, habilite a execução do script de inicialização e rode:

```bash
$ sudo chmod +x /usr/local/sbin/start_docker.sh
$ sudo chmod 755 /usr/local/sbin/start_docker.sh
$ /bin/sh /usr/local/sbin/start_docker.sh
```

Apesar de parecer estar tudo bem, o docker não foi iniciado por dois motivos:
1. Como há utilização de `sudo` dentro do script ele precisa ser executado como _root_ para funcionar corretamente. O problema é que se usarmos `sudo` o usuário teria de entrar com a senha toda vez a cada boot, e isso é chato demais.
2. O comando para montar o _cgroups_ precisa ser executado em um bash com privilégios de administrador, e isso só da pra fazer sem interação com o usuário se for através do **Gerenciador de Tarefas do Windows**.

Com isto em mente, vamos resolver esses dois problemas a seguir.

### Chamando o script de inicialização como root sem precisar de senha

No Linux, o arquivo `/etc/sudoers` controla quem pode executar o que como um super-usuário. Vamos então modificar esse arquivo para que possamos executar o script sem necessidade de entrar com a senha de usuário toda vez.

```bash
$ sudo nano /etc/sudoers
```

Adicione a seguinte linha no **final** do arquivo (tenha certeza de substituir **@SEU_USUARIO** pelo nome do seu usuário no WSL):

```
@SEU_USUARIO ALL=(ALL:ALL) NOPASSWD: /bin/sh /usr/local/sbin/start_docker.sh
```

Agora se você chamar o script ele nem vai mais te perguntar pela senha.

### Iniciando o Docker em um prompt elevado quando o Windows bootar

Depois de ativarmos o recurso para que o Docker seja inicializado através de um único comando não interativo, podemos faze-lo rodar como um administrador quando o sistema bootar.

Inicie o _Gerenciador de Tarefas_ do Windows, clique _Biblioteca do Agendador de Tarefas_ no painel esquerdo, e depois em _Criar Tarefa..._ no painel da direita.

{% include image.html description="Janela do Gerenciador de Tarefas" position="center" url="/images/2019/09/gerenciador-tarefas.png" %}

Uma nova janela se abrirá para que você insira os dados básicos da tarefa. Nomeie a tarefa de forma descritiva. Selecione **Executar estando o usuário contectado ou não** e marque a caixa **Executar com privilégios mais altos**. Configure para **Windows 10**.

Na aba **Disparadores** clique em _Novo..._ e selecione para que a tarefa seja iniciada **Ao fazer logon** usando o seu **Usuário específico** (esse usuário tem que ser administrador do Windows). Salve essas opções e retorne para a janela de configuração geral.

Na aba **Ações** clique em _Novo..._ e selecione a ação **Iniciar um programa** apontando para o executável `C:\Windows\System32\bash.exe`. **Adicione argumentos** a seguir: 
```
-c "sudo /bin/sh /usr/local/sbin/start_docker.sh"
```

Salve e vá para a aba **Condições**. Deixe todas as opções **desmarcadas**.

Na aba **Configurações** deixe apenas as seguintes opções **marcadas**:
- Permitir que a tarefa seja executada por demanda
- Executar a tarefa o mais cedo possível...
- Interromper tarefa se ele for executada...
- Se a tarefa em execução não parar ...

Salve as configurações da tarefa para finalizar sua criação. Na lista de tarefas do gerenciador selecione esta que você acabou de criar e clique em **Executar** no painel da direita.

### Teste se o Docker roda depois de um novo boot

Reinicie o computador, abra o `bash` e rode o seguinte:

```bash
$ docker run --rm hello-world
```

Se tudo estiver rodando perfeitamente, o Docker começará o download desta imagem de apresentação e vai exibir uma mensagem de boas-vindas. Isto quer dizer que o serviço do Docker está inicializando automaticamente dentro do WSL!

### Instalando o Portainer

Agora que o Docker funciona e temos certeza disso, vamos fazer o download da **versão standalone do Portainer** no nosso host Windows. Visite o site dos lançamentos do Portainer em [https://github.com/portainer/portainer/releases](https://github.com/portainer/portainer/releases) e baixe a versão mais atual da versão Windows. Descompacte em algum lugar em que você não vai mais mexer depois, já que precisaremos inicializar o Portainer também junto com o Docker.

Com a pasta aberta onde você descompactou o download, pressione `Shift` e aperte com o botão direito do mouse. No menu de contexto selecione **Abrir janela do PowerShell aqui**.

{% include image.html description="Janela do Gerenciador de Tarefas" position="center" url="/images/2019/09/power-shell.png" %}

No PowerShell execute o Portainer com o comando:

```posh
.\portainer.exe --template-file="./templates.json"
```

Com isto o Portainer deve ser executado e você poderá acessar pelo browser através do link `http://localhost:9000`. Ao abrir, o Portainer não localizará qualquer Endpoint, então clique em **Endpoint** no menu da esquerda, e depois em **Add endpoint**.

Deixe selecionado **Docker environment** como tipo de ambiente e dê um nome ao seu servidor. Em **Endpoint URL** insira `localhost:2375` e em **Public IP** entre com `localhost`. Deixe o **TLS desabilitado** e salve.

Você será redirecionado para a página inicial mostrando os Endpoints. Clique no seu servidor e comece a orquestrar seu containers WSL com Portainer.

### Não tente executar um bash

Se você tentar executar um bash seja via Portainer ou mesmo pelo próprio Docker do WSL você vai se deparar com um erro dizendo que não foi possível criar uma chave de sessão, já que esta não foi implementada no kernel do 16.04 LTS.

As duas forma de abrir um bash diretamente no container é por `attach`. 

- Via WSL rode o comando abaixo, e utilize a sequência de teclas `Ctrl+A, X` para liberar o container. Se você executar `exit` o container irá parar:

```bash
$ sudo docker attach --detach-keys="ctrl-a,x" nome_do_container
```

Incluí o parâmetro para personalização do _detach_, pois em meus testes não consegui executar a sequência padrão de liberação, que é `Ctrl+P, Ctrl+Q`. Portanto há essa adição ao `attach` tradicional por conta disso.

- Via Portainer, cliquem e **Containers**, selecione o container desejado e clique em **Attach**. Este com certeza é o jeito mais simples de executar comandos diretamente no container.

### Referências
1. Faun no Medium: [https://medium.com/faun/docker-running-seamlessly-in-windows-subsystem-linux-6ef8412377aa](https://medium.com/faun/docker-running-seamlessly-in-windows-subsystem-linux-6ef8412377aa)
2. Lord Loh no ServerFault: [https://serverfault.com/questions/843296/how-do-i-expose-the-docker-api-over-tcp](https://serverfault.com/questions/843296/how-do-i-expose-the-docker-api-over-tcp)
3. Documentação do Docker: [https://docs.docker.com/engine/security/https/](https://docs.docker.com/engine/security/https/)
4. Documentação do Portainer: [https://portainer.readthedocs.io/en/stable/deployment.html](https://portainer.readthedocs.io/en/stable/deployment.html)