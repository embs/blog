---
layout: post
title: "Como Utilizar Issues do Github"
date: 2013-02-20 19:19:40 -0300
comments: true
categories: [github, issues, dica, pt_BR]
---

Pessoal,

o nosso repositório no Github possui uma seção muito importante em qualquer projeto de desenvolvimento de software: a seção de issues. Issues são, basicamente, questões do projeto que podem assumir dois estados: aberta (open) ou fechada (closed).

No Github, a cada issue são associadas labels que indicam do que ela trata. Por exemplo: uma issue com título "Corrigir estilo do botão de logar" pode ser associada com as labels "front-end" e "bug" -- já que, claramente, trata-se de um bug no front-end do projeto.

<!-- more -->

As labels são completamente customizáveis -- isto é, podemos criá-las, editá-las ou removê-las, além de associar uma cor a cada uma delas. Segue uma descrição de cada uma das labels existentes atualmente em nosso repositório:

* Bug: bug;
* Enhancement: melhoria. Rotula issues que se referem a funcionalidades que *já estão implementadas* mas podem ser melhoradas;
* Front-end: issues relacionados à implementação do front-end (HTML, CSS e Javascript);
* Back-end: issues relacionados à implementação do back-end (controladores, modelos e tudo o mais que for RubyOnRails-specific);
* Duplicate: usada para quando, por engano, issues são criadas para questões do projeto que já possuem issue;
* Feature: implementação de nova funcionalidade;
* Invalid: nunca usei. Deve ser pra quando um issue é criado por engano ou pra quando um issue é criado e depois se constata que não é uma questão do projeto válida (que deve ser levada em conta);
* Question: usada para issues referentes a dúvidas específicas sobre alguma coisa do projeto. Ex.: uma issue "Será que não deveríamos usar o MongoDB como nosso banco de dados?" pode ser rotulada com a label "question";
* Wontfix: rotula issues que não serão resolvidas;

Além disso, issues podem ser atribuídas a um colaborador do projeto (responsável por resolvê-la, isto é, fechá-la ou tratar dos meios para que ela seja fechada, vulgo mandar alguém fazer) e podem ser associadas a um milestone do projeto. Milestones são utilizados quando há prazos estimados para lançamento de versões -- algo que foge do escopo desta mensagem e que não utilizaremos ao menos por enquanto.

Estou criando issues à medida em que encontro possibilidades factíveis para tal. Quem quiser acompanhar e colaborar, basta fazer isso através da nossa seção de issues no Github.

Abraços!
