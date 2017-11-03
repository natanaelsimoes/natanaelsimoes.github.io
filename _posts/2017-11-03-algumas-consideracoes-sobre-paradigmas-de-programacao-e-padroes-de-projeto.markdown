---
layout: post
title: Algumas considerações sobre paradigmas de programação e padrões de projeto
date: '2017-11-03 10:28:43 -0400'
---

O cenário do Desenvolvimento de Software e suas Linguagens de Programação tem passado por profundas mudanças nesta última década. Tivemos um aumento repentino na popularidade da Programação Funcional em linguagens Web onde protagoniza atualmente em toda a sua glória o React, uma amostra de tendência de crescimento desse estilo de paradigma para os próximos anos. A dúvida que fica é: devo aderir a tendência e começar a estudar novos paradigmas ou devo me concentrar em me especializar no que é mainstream no mercado?

{% include image.html url="/images/2017/10/linguagens-mais-populares-de-2016-segundo-a-code-eval.png" description="Linguagens mais populares de 2016" cite="Code Eval" cite_url="<http://blog.codeeval.com/codeevalblog/2016/2/2/most-popular-coding-languages-of-2016>" %}

Há uns anos atrás eu programava para uma software house da minha cidade onde a linguagem principal era Delphi. Naquela época, em 2010, eu estava iniciando o sexto período de Sistemas de Informação e tinha alguma experiência com desenvolvimento de sites com PHP. Em contrapartida a linguagem ensinada da faculdade era C#. Notem a salada de letrinhas se formando.

Ao me deparar com Delphi pela primeira vez não me senti confortável: aquela sintaxe com cara de Pascal, o design do XE (que era a versão do editor da Emcarcadero na época) que não me agravada, aqueles `TForm` lotados de componentes que por vezes atrapalhava até a visão do formulário. **"Que bagunça!"** eu pensava.

E a **Orientação a Objetos** disso, cadê? Comecei a perceber que aqueles componentes matavam a OO fazendo a visão se conectar diretamente com o banco e ter a lógica de negócios implementada em cada botão. Novamente, **"que bagunça"**!

Respire um pouco pra ouvir o que vou dizer a seguir. Se você é novo no ramo, como eu era nos parágrafos acima, revoltado se algo estivesse fora dos "padrões" em que você foi doutrinado na academia, sinto lhe informar: **não há coisa alguma errada em programar daquela forma**.

Eu realmente perdia a cabeça quando via aquilo, tanto é que no começo eu só assumia projetos para internet, pois PHP que era minha praia (e continua firme e forte). Mas aos poucos fui ficando **tolarente** e aceitando o fato de que OO não é o único jeito de resolver os problemas da humanidade.

A frase no menu de navegação desse site (até este dia em que escrevo esta postagem, 03 nov 2017) é ["There is more than a way to do it"](https://en.wikipedia.org/wiki/There%27s_more_than_one_way_to_do_it) (Larry Walls) é um ditado popular de entre os programadores Perl que se espalhou nas comunidades de desenvolvimento. Minha tradução para o português dela é _"Há mais de um jeito de se fazer isso"_. Foi um dos primeiros conceitos que aprendi ainda estudando algoritmos na faculdade. É possível que exista solução ideal mas não significa que ela seja a única forma de resolver o problema.

{% include image.html url="/images/2017/10/mudancas-na-porcentagem-de-popularidade-das-linguagens-por-ano-segundo-a-code-eval.png" description="Mudanças na porcentagem de popularidade das linguagens por ano" cite="Code Eval" cite_url="<http://blog.codeeval.com/codeevalblog/2016/2/2/most-popular-coding-languages-of-2016>" %}

Portanto o fato de um formulário possuir um componente que faz com que um componente visual, como uma caixa de seleção, acesse quase que diretamente o banco de dados, seja para efeitos de pura pesquisa ou registro de dados, não invalida em nada a solução elaborada. Considere que se um recurso existe para a linguagem ele pode ser utilizado. Considere que o MVC é apenas uma das formas de resolver o problema e aqui não temos o cenário da View acessando o banco, pois **não é MVC**!

Desta forma, temos um paradigma que foi utilizado fortemente no passado e foi caindo em desuso com o tempo devido a popularização da OO: a [Programação Orientada a Eventos](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_orientada_a_eventos). É possível programar OO em Delphi, pois tem suporte. É possível programar OE em Java, pois tem suporte. A comunidade Delphi é acostumada a programar OE, quase um concenso, mas não impede de implementar tudo OO. Já a comunidade Java se apropriou da OO na sua mais pura forma, tanto que há uma necessidade quase que psicopatológica de deixar tudo de acordo com o design pattern escolhido (sem choro nem vela).

Eu não quero subir num palanque aqui e gritar aos sete ventos pra todo mundo se abraçar não importa em qual paradigma programa. Só que tem situações que o exagero de não permitir a flexibilização do desenvolvimento pode custar caro pra alguém. Vou elencar aqui dois personagens que podem ser afetados com esse tipo de comportamento: o desenvolvedor e o cliente.

# Implicações da (in)tolerância paradigmática para o desenvolvedor

Explorar outras formas de resolver o mesmo problema, mesmo que haja uma solução conhecida (na maioria dos casos é nativa da linguagem), faz com que o desenvolvedor adquira conhecimento mais profundo sobre o problema.

Se você se contenta com o que a linguagem possui e não busca entender os algoritmos por detrás das funções nativas, ou não explora outras maneiras de fazer aquilo, isso **pode custar tempo de desenvolvimento** caso você não possa usar essa linguagem em um outro projeto no futuro.

Mesmo que você não chegue a um lugar novo com a experiência da exploração, como se estivesse apenas andado em círculos numa floresta densa, você tem agora o conhecimento do que está a sua volta e se tornou mais apto para usar essa função, mesmo que nativa da linguagem! Vai **saber o momento certo** de utilizá-la quando ninguém mais lhe daria atenção. A equipe vai se levantar e dizer "eu nunca teria usado isso pra resolver esse problema".

Outro ponto a ser considerado é **saber o propósito de cada linguagem**. Virtualmente toda linguagem é capaz de resolver qualquer problema, de qualquer natureza. As diferenças estão na facilidade e tempo para se chegar à solução. É possível fazer um webservice só usando Assembly, mas quanto tempo e esforço isso vai requerer? É possível fazer uma aplicação desktop com PHP, mas quanto tempo e esforço isso vai requerer?

Estar disposto a conhecer um pouco de outras linguagens e por vezes ter de abrir mão dos padrões que você já está acostumado **pode te ajudar e muito a fazer seus projetos mais rápido**. Eu já tive muitas dificuldades por conta disso, em querer resolver todos os problemas usando a mesma linguagem. Apesar do que vou falar aqui, não posso esconder que há vantagens reais em se fechar num mundo de apenas uma linguagem: com o tempo você se torna mais eloquente, culto, experiente, um guru na linguagem, manjador dos paranauês. Entretanto, assim como no mundo real, a capacidade de falar outros idiomas pode abrir portas a oportunidades antes impossíveis.

Ter a habilidade de analisar um problema e decidir usar a "linguagem tal", não porque você a domina, mas porque o propósito dela é o que mais atende às demandas do projeto, sem sombra de dúvidas, é recompensador em todos os sentidos. Isso vai causar incômodo, principalmente com linguagens não tão frequentes no seu arcabouço, mas o resulto é simplesmente fantástico. No dia em que você retornar para sua linguagem de praxe, **novas ideias surgirão e você passará a fazer as coisas diferentemente, analisando de outras perspectivas** que você acabou de trazer de uma outra linguagem. É quase que a experiência de um intercâmbio internacional!

Passei por essa situação recentemente no mestrado. Comecei a desenvolver minha dissertação sobre Meteorologia Urbana onde acabei incluindo Sistemas de Aquisição Automática de Dados. Depois de muita pesquisa, descobri que toda a comunidade científica que trabalha com esses temas programa integralmente em Java. Torci o nariz. Na graduação tive aquela pincelada básica de Java, mas nada que pudesse me habilitar para algo no nível proposto para esse trabalho. Eu poderia ter imposto minha vontade, provavelmente ninguém se levantaria para me condenar por usar PHP naquele projeto, mas resolvi por conta própria produzir a solução usando a língua de quem já está no meio. [E funcionou!](https://github.com/natanaelsimoes/52n-sos-util) A comunidade rapidamente absorveu minha proposta e foi muito bem recebida.

E quando tive que programar comunicação serial com um carrinho Arduino através de bluetooth, a opção mais óbvia para o meu contexto pessoal era Java, devido a experiência recente no mestrado. Mas novamente observando tanto a comunidade quanto a facilidade de implementação, Python se mostrou mais aceitável para a missão. Aquele foi o [meu primeiro programa em Python](https://github.com/ifroariquemes/IFRC) (excluidos os tutoriais que usei para aprender a linguagem) e ainda rendeu um mestrado para um amigo que usou a solução para aprimorar a didática no ensino de movimento retilíneo nas aulas de física do ensino médio.

# Implicações da (in)tolerância paradigmática para o usuário

Pode não parecer mas o resultado de se viajar por outros mundos não afeta apenas o viajante mas todos a sua volta. Já ouvi boatos por ai de situações como "teria ficado muito melhor se eu tivesse feito em [coloque aqui sua linguagem de estimação]", e não posso discordar disso completamente. Seria o mesmo de tentar escrever um poema em outra lingua que não a nativa: geralmente possuímos maior desenvoltura e voculário mais rebuscado quando dominamos desde o berço.

Pense o seguinte sobre essa frase, teria ficado melhor para quem? Mais cômodo para quem escreveu? Que diferença faz a linguagem que você utilizou para o usuário se ele não sabe ler linguagem de alto nível? Bem, pode não fazer diferença assim diretamente, pois o que ele usa é o programa depois de interpretado/compilado e não em sua forma de texto plano. Portanto temos que manter em nossa mente que linguagens têm propósitos específicos, e por serem especializadas tornam-se mais eficientes em realizar os objetivos para os quais foram projetadas.

Assim temos que a exploração de outros jeitos de programar podem conduzir a escolhas de linguagens que entreguem ao usuário final velocidade de processamento e ROI.

**Maior velocidade no processamento de dados específicos**

Você ficaria abismado em saber como as linguagens utilizam os recursos do computador para fazer o que fazem. Quanto mais recursos uma linguagem possui, mais tempo ela leva para executar as coisas: não tem como fugir disso.

Para manter esse ar de super linguagem, elas precisam criar um monte de estruturas de controle envolta do seu código que por vezes nem você faz ideia de que estavam ali e portanto ficam ociosas o tempo inteiro, só esperando para serem utilizadas. Contudo estão ali gastando seu processador, sua memória, seu disco...

Antes prosseguir entre nesses dois sites de benckmark de linguagens:

- [AttractiveChaos](https://attractivechaos.github.io/plb/) para informações de tempos de execução e memória utilizados em algoritmos bem peculiares;
- [The Computer Language Benchmark Game](http://benchmarksgame.alioth.debian.org), e neste selecione sua linguagem favorita para vê-la comparada com outra (no fim da página tem links para controlar a outra linguagem com a qual será comparada, como por exemplo [neste link você pode ver PHP contra Java](http://benchmarksgame.alioth.debian.org/u64q/compare.php?lang=php&lang2=java)).

Algumas linguagens possuem sérios problemas de I/O, outras têm maior dificuldade no gerenciamento de memória. Há casos que processos [estocásticos](https://pt.wikipedia.org/wiki/Estocástico) podem produzir resultados bem catastróficos. Por isso a linguagem, seu propósito e o problema sendo analisado precisam estar de comum acordo, por questões de qualidade do produto final.

**Maior retorno sobre o investimento (ROI)**

Supondo que escolhendo uma linguagem que tem como propósito solucionar problemas relacionados com o do usuário, e supondo que o desenvolvedor consiga com a menor curva de aprendizagem possível chegar à solução, é altamente provável que o tempo de produção pode ser reduzido a tal ponto de permitir a entrega de partes funcionais do sistema com menos esforço braçal/cerebral. Isto quer dizer que o cliente terá diante de si um sistema funcional que faça valer o investimento realizado em menos tempo.

# Ainda temos muito que codar

Já estamos beirando os [70 anos de programação moderna](https://en.wikipedia.org/wiki/Timeline_of_programming_languages)
(com linguagens de alto nível) e em todo esse período as formas de pensar, o jeito de projetar, os objetivos
das linguagens, as demandas da sociedade, tudo mudou e tem caminhado ligeiramente
para novos patamares ainda não explorados.

Olhando para a história podemos afirmar que não existe solução definitiva. Acompanhe
esta analogia: se já existe fotografia da Torre Eiffel, por que tanta gente
tira fotos dela todos os dias? Observe essa [pesquisa no Google Imagens](https://www.google.com.br/search?q=torre+eiffel&tbm=isch) e perceba a
**diversidade de perspectivas e composições**. O objeto principal é o mesmo
mas cada solução traz informações distintas.

Assim também é a programação. São infinitos jeitos de codar. Cada um à sua
maneira. Tal como distingue a [Lei do Direito Autoral 9610/1998](http://www.planalto.gov.br/ccivil_03/leis/L9610.htm)
em seu Art. 7°, item XII, que define programas de computador como sendo criação do espírito humano.
Portanto todo código leva consigo a visão de mundo, os valores,
as crenças e as digitais de seu autor, configurando a identidade e unicidade da
obra.

Não somos robôs, não produzimos software em linha de produção (dá para usar
a mesma receita, mas cada problema tem seu próprio escopo). Usamos da criatividade
para propor novas soluções e não há livro, curso, academia ou professor que
possa/deva limitar nossa capacidade a um pensamento exclusivamente padronizado.

Não pense mal de mim, eu ADORO padrões. Eles são maravilhosos. Mas às vezes
pensar fora da caixinha pode possibilitar a criação de soluções muito mais efetivas
do que fazer as coisas da forma como a receita diz.
