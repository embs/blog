---
layout: post
title: "Pro Inferno com Configuração de Ambiente de Desenvolvimento!"
date: 2014-01-21 20:03:45 -0300
comments: true
categories: [nitrous, dica, tutorial, passo-a-passo, pt_BR]
---

**TL;DR** http://nitrous.io

A labuta pra configurar um ambiente de desenvolvimento RoR com sucesso não é de
hoje: [gist](https://gist.github.com/guiocavalcanti/1600711) de [Guila](https://github.com/guiocavalcanti),
[gist meu](https://gist.github.com/embs/3614398) (forkado do de Guila :B),
[postagem em blog](/2013/02/06/configurando-ambiente-de-desenvolvimento-rails-e-criando-um-novo-projeto/)
e tudo o mais. Recentemente eu quebrei a cabeça com utilização de máquinas
virtuais (o que **demora pra caralho**) e tentativas frustradas de usar um HD
externo pra bootar nas máquinas do CIn/UFPE.

![nitrous](http://i.minus.com/ibov54MlubiLia.png)

Hoje o [Nitrous](http://nitrous.io) salvou a minha pele. Se você tem alguma
proficiência com a utilização de aplicações web, vá lá e faça seu nome. Se não,
continue a leitura e acompanhe um passo-a-passo pra rodar uma aplicação RoR na
nuvem em **pouquíssimo** tempo.

<!-- more -->

Antes de qualquer coisa, você precisa de uma conta para utilizar o serviço: dá
pra criar na [home](http://nitrous.io) ou se cadastrar usando o [Github](https://www.nitrous.io/users/auth/github),
[Google+](https://www.nitrous.io/users/auth/google_oauth2) ou [Linkedin](https://www.nitrous.io/users/auth/linkedin).
(Eita! Não tem FB. :D)

Uma vez autenticado, é só clicar em `New Box`. A tela pra criação de um novo "box"
é bastante simples e intuitiva (+1 pra galera do Nitrous). Aqui, deixei o nome
da app que eles sugeriram (inspirados em Game of Thrones :D) e selecionei a região
"South America". Acho que não dá pra melhorar as specs da máquina virtual no plano
gratuito mas pela experiência que tive com esse plano, tudo rodou **muito** rápido
e eficientemente. Aliás, não dá pra reclamar de uma máquina com 384Mb de ram e
750MB de armazenamento em massa se você não pretende jogar GTA V nela (e, basicamente,
rodar só o terminal).

![create-box](http://i.minus.com/ib2vdoCif32F5l.png)

`Create Box` e:

![provisioning](http://i.minus.com/iGeyT4i1ZXK8o.png)

Na página de visualização de seus boxes, selecione o box recém-criado e clique
em `IDE`. A tela que você deve ver é uma como a que segue:

![IDE](http://i.minus.com/i8a2bakwQNj7m.png)

Ou seja: um editor de texto muito parecido com o Sublime Text e um console --
tudo o que precisamos para começar a desenvolver! \o/ Rodei alguns comandos
pra dar uma mostra do que temos ao nosso dispor:

```bash
$ cd workspace
$ ruby -v
$ rails -v
$ rvm -v
```

Mas não vamos começar do zero. Clone o código do [BDance](https://github.com/embs/bdance)
-- projeto que deve ser assunto de uma postagem em breve.

```bash
$ git clone https://github.com/embs/bdance.git # o git também já está instalado
```

Fiz o clone via HTTPS mas dá pra configurar chaves SSH no Nitrous pra permitir
o clone via SSH (não testei isso ainda). Dê um `cd` para o diretório criado pelo
comando `git clone` e bote o negócio pra rodar!

```bash
$ bundle                # instala dependências
$ rake db:create:all       # cria bases de dados
$ rake db:migrate          # cria tabelas
$ rake bootstrap:all    # povoa base de dados com informações fakes (ou quase isso)
$ rails s
```

Não encane se o `rake bootstrap:all` não rolar. Fiz isso hoje e não sei qual
será o seu futuro... Uma vez que o servidor Rails estiver rodando, clique (lá
no menu do topo da página) em `Preview` e selecione `Port 3000` (que é a porta
utilizada pelo servidor Rails por padrão).

Agora é só brincar com a aplicação Rails hosteada no Nitrous e descobrir outros
serviços que a plataforma oferece. Pense num negócio arretado!
