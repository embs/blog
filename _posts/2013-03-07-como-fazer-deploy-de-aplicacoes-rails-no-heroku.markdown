---
layout: post
title: "Como Fazer Deploy de Aplicações Rails no Heroku"
date: 2013-03-07 19:37:13 -0300
comments: true
categories: [deploy, heroku, rails, tutorial, passo-a-passo, pt_BR]
---

Você vai precisar de:

* Conta no [Heroku](http://www.heroku.com/);
* [Ambiente preparado](http://naofalacomputa.blogspot.com.br/2013/02/configurando-ambiente-de.html) para criação de app Rails;

Vamos, primeiro, criar a aplicação Rails:
```bash
$ rails new hello_heroku
```
Já temos uma aplicação Rails pronta para ser mandada ao ambiente de produção do Heroku, certo? Certo. Mas vamos fazer uma modificação mínima para que a aplicação não fique apenas na tela de boas vindas do Rails. Remova o arquivo public/index.html e adicione uma nova rota ao config/routes.rb
```ruby
# routes.rb
HelloHeroku::Application.routes.draw do
  root to: 'welcome#index'
  # ou root :to => 'welcome#index' se você estiver usando uma versão do ruby < 1.9
end
```

<!-- more -->

Isso fará com que qualquer requisição get à raiz da nossa aplicação seja direcionado para a action index do nosso controlador WelcomeController (que, por sinal, ainda não temos) -- como podemos ver ao executar 'rake routes':

![img](http://i.minus.com/ibkNUWUx72wCGL.png)

O próximo passo é óbvio: criar o WelcomeController. Para evitar qualquer arquivo desnecessário que o generator do Rails pode, eventualmente, criar, façamos isso na mão. Basta criar um arquivo chamado welcome_controller.rb no diretório app/controllers/ com uma única action vazia index:
```ruby
# app/controllers/welcome_controller.rb
class WelcomeController < ApplicationController
  def index
  end
end
```
Como não fazemos nada na action index, ela simplesmente irá renderizar a view index.html.erb que deve estar presente em app/views/welcome/:
```erb
<%# app/views/welcome/index.html.erb %>
<b>Hello, Heroku!</b><br />
<%= l Time.now, format: :short %>
```
Pronto. Nossa prolífica aplicação Rails está pronta para ir pra produção! Se tiver dado tudo certo até aqui, você deve visualizar algo parecido com a imagem abaixo ao rodar o servidor (rails s) e acessar 'localhost:3000':

![img](http://i.minus.com/iZZAZSDzx9co5.png)

O próximo passo é criar a aplicação no Heroku. Para isso, é necessário que você disponha do ToolBelt do Heroku -- uma espécie de kit de ferramentas composto por comandos que tornam a tarefa de deploy (e outras) trivial. O ToolBelt pode ser instalado facilmente e as instruções para instalação são encontradas no próprio sítio do Heorku. Em sistemas Debian-like, é feito com um único passo:
```bash
$ wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```
ToolBelt instalado, é hora de autenticar com a conta do Heroku (com o comando 'heroku login'). Por exemplo:

![img](http://i.minus.com/ibkG6ZxcMa4eUd.png)

Depois basta criar a app no Heroku usando o comando heroku apps:create (seja mais criativo que eu e escolha um nome que ainda não exista entre as apps cadastradas no Heroku):

![img](http://i.minus.com/i8Lx4s1ryZRgi.png)

Pra terminar, vamos dar o deploy -- que é tão fácil quanto dar um push usando o Git. Na verdade, é um push usando o Git. "Mas, peraí, você não disse nada de Git e agora vem com essa história aí... vou ter que saber usar essa parada pra poder dar o deploy, pensei que fosse fácil, não vale a pena usar isso, não, é melhor pagar por uma solução mais fácil ou já sei: vou pagar pra alguém fazer isso pra mim" é o que você vai pensar se souber usar vírgulas no pensamento. Pois é. Continue chorando ou instale e configure o Git (se você estiver usando Windows, sugiro que continue chorando).

O Github possui artigos muito bons que ajudam pra caralho quando se encontra algum problema relacionado ao Git. Problemas com chaves, por exemplo: https://help.github.com/articles/generating-ssh-keys. É só procurar. https://help.github.com :)

Agora que você já deu a última soluçada do pranto e decidiu não mudar de aba me xingando, vamos adicionar o remoto que o Heroku dispõe para toda app que é hosteada lá e que pode ser encontrado clicando nos links no Heroku: Apps >> NomeDeSuaApp >> Settings

![img](http://i.minus.com/irxiP8YXet3R5.png)

Aí está: git@heroku.com:hello-heroku-naofalacomputa.git. Dava até pra ter inferido. Enfim...

![img](http://i.minus.com/iOWRWpFtvp0Fn.png)

Ah, gordo escroto, não dá pra copiar e colar da imagem. Vou quebrar teu galho...
```bash
# inicia repositório git
$ git init

# adiciona remote do heroku
$ git remote add heroku SUA_URL_GIT

# lista seus remotos
$ git remote -v
```
Agora, sim, é só dar o push!
```
# não sem antes criar o commit, claro :)
$ git add . # adiciona tudo

$ git commit -m "Primeiro commit" # cria o commit

$ git push heroku master # deploy!
```
O resultado do push pro Heroku é assaz comprido. Divirta-se com a leitura. Se você não fez nenhuma merda e for um bom aprendiz, deve ver a aplicação rodando na URL da app no Heroku:

![img](http://i.minus.com/ibabshYbOOa6iB.png)

### Observação Importante e Bastante Pertinente

O Rails, por default, utiliza a gem do sqlite. O Heroku, compulsoriamente, utiliza um BD Postgres. Se você tentar dar deploy de uma app Rails com a gem do sqlite listada no seu Gemfile, vai dar merda. Remova ou comente a linha que especifica essa gem, adicione uma linha especificando a gem do Postgres ("gem 'pg'") e não esqueça de rodar o bundle antes de criar o novo commit para o push correto pro Heroku.

### Observação Pertinente mas de Pouca Importância

Não, eu não estou às 3h da matina do dia 07 de Março escrevendo um tutorial de como fazer deploy de aplicações Rails no Heroku. A hora apareceu assim deturpada por conta da configuração da localização da app Rails. Mas isso fica pra uma próxima...
