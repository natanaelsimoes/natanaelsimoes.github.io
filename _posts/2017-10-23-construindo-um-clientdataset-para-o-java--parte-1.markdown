---
layout: post
title: "Construindo um ClientDataSet para o Java - Parte 1"
date: "2017-10-23 09:12:28 -0400"
---
Depois de participar de uma oficina sobre personalização de componentes Java
com o colega Prof. Reinaldo do IFRO, Campus Ji-Paraná, durante o
[V CONPEX](https://eventos.pvhzonanorte.ifro.edu.br/painel/00339708239/), tive a
brilhante (acho que nem dá pra classificar como brilhante, já que é uma
adaptação bem caseira pra uma linguagem que já possui o poder do hibernate e outros de alto
calibre) de desenvolver um conjunto de componentes para Java que simulasse a estrutura do
[ClientDataSet](https://edn.embarcadero.com/article/28876) no Delphi.

{% include image.html url="/images/2017/10/hierarquia-de-implementacao-clientdataset-no-delphi.png" description="Hierarquia de implementação ClientDataSet no Delphi<br>Fonte: <a href='http://docs.embarcadero.com/products/rad_studio/delphiAndcpp2009/HelpUpdate2/EN/html/delphivclwin32/DBClient_TClientDataSet.html'>Embarcadero</a>" %}

### Objetivo do projeto

A solução que estou propondo deve descrever componentes de conexão, tabela,
consulta e os componentes visuais adaptados para essa tarefa tal como era no Delphi
com `TDBText`, `TDBComboBox` e o resto da turma.

### Metodologia

Pretendo ler a documentação oficial da Embarcadero que especifica um TDataSet para
trabalhar a interface de todos os tipos de conjunto de dados que serão abordados
por esta solução, delimitando-se inicialmente a uma estrutura para ligação direta
com uma tabela, semelhante ao `TSQLTable` e outra para consultas personalizadas
como um `TSQLQuery`.

{% include image.html url="/images/2017/10/exemplo-de-data-module-com-componentes-das-estrutura-requerida-por-um-clientdataset.png" description="Exemplo de Data Module com componentes das estrutura requerida por um ClientDataSet" cite="DelphiBR" cite_url="http://www.delphibr.com.br/artigos/clientdataseteibx/clientdataseteibx.htm" %}

Depois de especificadas as funções que devem ser implementadas, as classes concretas
serão criadas para ambos os tipos de estruturas pretendidos. Nos dois casos será
utilizado um objeto de `ResultSet` como base para a adaptação das funções do CDS.

Assim que uma estrutura funcional semelhante à do CDS for concluída, os componentes
visuais serão criados de forma que todos os componentes nativos do Swing terão sua
versão produzida para trabalhar com este plugin.

Todo o projeto ficará disponível publicamente através de [repositório no github](https://github.com/ifroariquemes/JSQL).
