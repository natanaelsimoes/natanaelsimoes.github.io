---
layout: post
title: "Instalação do TeX Live no Windows"
date: "2017-10-15 11:03:17 -0200"
categories: latex
---
TeX Live é uma das implementações de binários para o padrão LaTeX que permite a edição de documentos por marcação, tal como acontece com HTML. O objetivo é atribuir semântica ao conteúdo e então aplicar um template. Desta forma o autor não precisa se preocupar com regras de formatação, que constam no template, focando exclusivamente no conteúdo. O TeX Live fará a compilação do texto utilizando o template selecionado para gerar um PDF devidamente formatado.

### Faça o download do instalador

O instalador do TL para qualquer plataforma pode ser baixado na [página oficial][492365c6] do projeto. Especificamente para Windows, você pode [baixar aqui][3a48fa7f]!

### Execute o instalador

Depois de finalizada a instalação, execute o instalador `install-tl-windows.exe` onde quer que você tenha salvo em seu computador.

A seguinte janela deve aparecer com as opções:

{% include image.html description="Primeira tela do instalador TL" position="right" url="/images/2017/10/primeira-tela-do-instalador-tl.png" %}

- **Simple install (big)**: fará a instalação completa com todos os pacotes oficiais TeX. Pode levar muito tempo dependendo de sua conexão, pois somam-se quase **4 GB**.
- **Custom install**: permitirá que você selecione os pacotes que deseja instalar. Ideal para quem já tem experiência com TL e sabe que pacotes utiliza no dia-a-dia. Este tipo de instalação é bem mais rápida por baixar apenas o necessário.
- **Unpack only**: realizará o mesmo procedimento que a instalação completa, porém não fará o Windows reconhecer a instalação da distribuição TL (os executáveis não ficarão disponíveis para uso).

Selecione a primeira opção para uma instalação completa e clique em **Install**.

Aparecerá a seguinte tela de boas vindas, clique em **Próximo**.

{% include image.html description="Segunda tela do instalador TL" position="center" url="/images/2017/10/segunda-tela-do-instalador-tl.png" %}

O instalador questionará sobre o local de instalação do TL. Deixe como está ou troque para uma outra localização de sua escolha se achar necessário. Quando estiver tudo pronto, clique em **Próximo**.

{% include image.html description="Terceira tela do instalador TL" position="center" url="/images/2017/10/terceira-tela-do-instalador-tl.png" %}

Em seguida o instalador perguntará sobre o tamanho padrão de papel e opções para inclusão de uma nova entrada no Menu Iniciar e a instalação de um editor de documentos TeX chamado [TeXworks][903a7e11]. Eu particularmente não gosto muito desse editor, prefiro [TeXstudio][83e2e564]. Recentemente tenho experimentado [Atom][ce7c4583] que com o conjunto certo de plugins consegue fazer coisas mais surpreendentes que o TeXstudio.

Neste ponto da instalação deixe marcado **A4** como tamanho padrão, deixe marcado **Adicionar atalhos de menu**, __DESMARQUE__ o TeXworks e clique em **Próximo**.

{% include image.html description="Quarta tela do instalador TL" position="center" url="/images/2017/10/quarta-tela-do-instalador-tl.png" %}

A última tela de configuração do instalador mostrará um resumo das opções selecionadas. Basta clicar em **Instalar** e aguardar o download e instalação dos pacotes (pode levar horas).

### Informe ao Windows o caminho da instalação

Depois que a instalação terminar, verifique se o Windows "sabe" onde os programas do TL foram instalados. Para fazer isso:
- Abra o menu iniciar ou use a combinação `Windows + R` no seu teclado
- Digite `cmd` e aperte **Enter**
- Na tela preta, digite o comando `pdflatex`

Se aparecer **"This is pdfTeX, Version x.xxxxx-x.x-x.x (TeX Live xxxx/W32TeX)..."** a instalação está concluída e você pode pular direto para a [instalação de um editor de documentos TeX](#instale-um-editor-de-documentos-tex). Feche o prompt ou a combinação de teclas `Ctrl + C` para interromper o `pdflatex` e então `exit`.

{% include image.html description="Prompt exibindo com sucesso a execução do programa pdflatex" position="center" url="/images/2017/10/prompt-exibindo-com-sucesso-a-execucao-do-programa-pdflatex.png" %}

Entretanto, se aparecer a mensagem **"'pdflatex' não é reconhecido como um comando interno ou externo, um programa operável ou um arquivo em lotes"** é porque o Windows não sabe onde estão os binários do TL.

Abra o **Windows Explorer** pelo Menu Iniciar ou a combinação `Windows + E`, clique com o botão direito sobre **Meu Computador** e selecione **Propriedades**.

{% include image.html description="Seleção de Propriedades do Computador no Windows Explorer" position="center" url="/images/2017/10/selecao-de-propriedades-do-computador-no-windows-explorer.png" %}

Abrirá uma janela com as propriedades do computador contendo informações do Sistema Operacional, quantidade de memória RAM e outros. Neste caso, meu SO é o Windows 10, portanto os próximos passos serão específicos para ele. Se você usa alguma outra versão do Windows, procure por termos equivalentes.

Nas propriedades do computador selecione **Configurações avançadas do sistema** e então **Variáveis de Ambiente...*.

{% include image.html description="Propriedades do sistema no Windows 10" position="center" url="/images/2017/10/propriedades-do-sistema-no-windows-10.png" %}

{% include image.html description="Configurações avançadas do sistema no Windows 10" position="center" url="/images/2017/10/configuracoes-avancadas-do-sistema-no-windows-10.png" %}

Na janela de Variáveis de Ambiente selecione a entrada **Path** e clique em **Editar...**.

{% include image.html description="Janela de variáveis de ambiente no Windows 10" position="center" url="/images/2017/10/janela-de-variaveis-de-ambiente-no-windows-10.png" %}

Na edição de variáveis, clique em **Novo** para adicionar um novo caminho e então digite o `caminho de instalação do TeX Live + \bin\win32`. Se você instalou no diretório padrão do instalador então o caminho será `C:\texlive\2017\bin\win32`. Clique em **OK** para finalizar a configuração, e então **OK** em todas as outras janelas até chegar na tela de propriedades do sistema novamente.

{% include image.html description="Edição da variável Path no Windows 10" position="center" url="/images/2017/10/edicao-da-variavel-path-no-windows-10.png" %}

Agora [volte no início deste passo](#informe-o-windows-do-caminho-da-instalação) para verificar se o `pdflatex` é executado pelo `cmd` e então prossiga com a instalação do editor TeXstudio.

### Instale um editor de documentos TeX

Prossiga para o site do [TeXstudio][83e2e564] e faça o download do instalador. Em toda as etapas da instalação, avance até o final sem mudar qualquer propriedade.

Se por acaso o Windows não reconhecer a instalação do TL, ao abrir o TS será exibido um erro falando sobre isso. Caso esteja tudo certo, TS abrirá com uma página em branco aguardando seu comando.

{% include image.html description="TeXstudio aberto com página em branco" position="center" url="/images/2017/10/texstudio-aberto-com-pagina-em-branco.png" %}

Você agora está pronto para começar a desfrutar do LaTeX!

  [492365c6]: https://www.tug.org/texlive "Página oficial do Tex Live"
  [3a48fa7f]: http://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe "Instalador do Tex Live para Windows"
  [903a7e11]: https://www.tug.org/texworks/ "Página do TeXworks"
  [83e2e564]: https://www.texstudio.org "Página do TeXstudio"
  [ce7c4583]: https://atom.io "Página do Atom"
