---
layout: post
title: "Configurando Ambiente de Desenvolvimento Rails e Criando um Novo Projeto"
date: 2013-02-06 18:49:36 -0300
comments: true
categories: [rails, ror, ruby, tutorial, passo-a-passo, pt_BR]
---

Pessoal,

vou aproveitar que meu Linux aqui tá zerado pra fazer o que fizemos no
treinamento de hoje: configurar o ambiente para desenvolvimento e criação de um
novo projeto Rails.

Pra começo de conversa, basta acessar um terminal no Linux. Estou usando o Linux
Mint, que é baseado no Ubuntu. (clique com o botão direito e -> abrir em nova aba
/ janela para ver a imagem em seu tamanho original)

<!-- more -->

![uname -a](http://i1.minus.com/iNdaUrlsb96ra.png)

Beleza... a despeito do que dizem por aí sobre rodar um projeto Rails em 20
minutos no Windows (hauhauhauhua), agora temos um terminal (um dos dois únicos
programas que vamos, essencialmente, precisar para desenvolver) num sistema
operacional que fornece tudo o que precisamos para trabalhar de forma ágil. Não
é que não encontraremos problemas -- isto sempre acontece -- mas certamente
poderemos solucioná-los de maneira fácil. O outro programa que precisamos para
desenvolver é um editor de texto -- que você pode escolher à sua preferência, eu
gosto do Sublime Text.

O segundo passo é instalar o RVM. "Tá certo, Matheus. Você é um barbudo escroto
mas o quê diabos é RVM?". RVM é uma ferramenta que separa diferentes ambientes
de desenvolvimento para a linguagem Ruby. Um exemplo: você é um desenvolvedor
fuderoso que está atualmente trabalhando em dois grandes projetos open-source
feitos em Ruby on Rails (RoR). Um deles, o Unsocial, é uma rede social para
nerds que têm número de amigos negativo, podem dar "hate!" no que os outros
compartilham e excluir postagens do mural dos outros. O projeto Unsocial utiliza
muitas e muitas gems (como são conhecidas as bibliotecas Ruby) para:
autenticação de usuário, rating de postagens, amizade entre os usuários e outras
bibliotecas relacionadas. O segundo projeto, o MathOnRails, é uma ferramenta web
para execução de cálculos avançados que utiliza muitas e muitas gems também --
poucas em comum com o primeiro projeto. Já deu, intuitivamente, pra perceber que
ter todas as bibliotecas num único lugar para os dois projetos não é lá muito bom?
Não é bom mesmo, não. Uma das desvantagens é que o tempo necessário para iniciar
o ambiente de desenvolvimento (rodar servidor ou console localmente, por exemplo)
vai ser muito maior se as gems dos dois projetos tiverem que ser carregadas.

Antes de instalar o RVM, precisamos instalar algumas dependências. No Mint (ou
Ubuntu ou Debian) é fácil fazer isso utilizando o gerenciador de pacotes (vulgo
apt-get). Basta rodar o comando:
```bash
$ sudo apt-get install libssl-dev libreadline6-dev zlib1g-dev curl
```
O resultado aqui foi o seguinte:
![Inline image 2](http://i6.minus.com/itjOb5yY2PsW2.png)

Pra instalar o RVM:
```bash
$ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
```
Depois é necessário carregar o comando do diretório onde o RVM foi instalado:
```bash
$ source ~/.bash_profile
```
E então testar se a instalação deu certo (chamando o comando 'rvm' com o parâmetro
'-v' para mostrar a versão do RVM):
```bash
$ rvm -v
```
O resultado aqui foi o seguinte:
![Inline image 3](http://i4.minus.com/iApYQDwKRdObW.png)
(o que significa que deu tudo certo)

Beleza. Próximo passo: instalar o Ruby através do RVM (não é a toa que RVM = Ruby
Version Manager, isto é, além de separar as bibliotecas de diferentes projetos,
ele permite utilizar facilmente diferentes versões do Ruby). Como no nosso projeto
utilizaremos a versão 1.9.3 (que é a versão estável mais recente), vamos instalá-la:
```bash
$ rvm install 1.9.3
```
Só pra testar, do mesmo jeito que fizemos com o RVM:
```bash
$ ruby -v
```
Se o comando acima der algum erro, tente selecionar explicitamente a versão do
Ruby que deve ser usada:
```bash
$ rvm use 1.9.3
```
Obtive o seguinte resultado:
![Inline image 4](http://i4.minus.com/iHlXuLWZzFN4g.png)

Ok! Estamos nos aproximando do tão esperado momento de rodar um projeto Rails --
o próximo passo, inclusive, é justamente instalar o framework para desenvolvimento
web. O famigerado Rails nada mais é que uma biblioteca Ruby. Então é isso mesmo:
basta instalar um gem (chamado Rails) pra poder desenvolver usando esse negócio
tão famoso (utilizado por outras ferramentas tão foda quanto a nossa -- a exemplo
do próprio Github). Antes de executar o comando que irá executar a instalação,
vamos esclarecer algumas coisas: o tal do RVM serve pra separar os ambientes de
desenvolvimento, correto? Sim! Como é que a gente faz isso? Com gemsets! Massa.
Então vamos lá. Primeiro, listamos todos os gemsets que temos:
```bash
$ rvm gemset list
```
Isso deve exibir a lista de gemsets existentes e uma setinha '=>' apontando para
o gemset que está sendo usado atualmente. Legal. Mas peraí: já existem bibliotecas
(ou gems) nesse gemset? Sei lá. Vamos descobrir:
```bash
$ gem list
```
Esse comando lista todos os gems instalados no gemset (já que estamos usando RVM
para separá-los). Como deve ter aparecido, já existem alguns gems instalados por
padrão. Vamos ao que interessa: criar um gemset que abrigue os gems de nosso
projeto (que chamarei de quince mas você pode chamar do que quiser -- afinal, só
quem vai ter acesso a isso é você, na sua máquina, no seu ambiente de desenvolvimento).
```bash
$ rvm gemset create quince
```
Gemset criado! Agora, vamos dizer ao RVM que queremos trabalhar com esse gemset:
```bash
$ rvm gemset use quince
```
Eu não sei aí, mas aqui deu merda. "RVM is not a function".
![Inline image 5](http://i4.minus.com/iJl2isdjsqPo4.png)

Ok, shit happens. Resolver isso não é muito complicado. Basta ir em Edit > Profile
Preferences, escolher a aba Title and Command e checar a opção "Run command as a
login shell".
![Inline image 6](http://i3.minus.com/i3y580N5ZjaQc.png)

Depois de setar essa configuração é necessário reiniciar o terminal (fechar e
abrir ou abrir uma nova aba). Tentai aí selecionar o gemset de novo pra ver se
funciona. Se funcionar (e eu espero que sim), lista aí os gems instalados pra
ver se tem diferença em relação aos instalados no gemset padrão. Tem? Outro
comando legal do RVM é o que indica a versão do Ruby e o gemset que estão sendo
usados:
```bash
$ rvm current
```
Se isso der como saída algo do tipo "ruby-1.9.3@quince", então estamos prontos
para instalar o Rails (no gemset correto):
```bash
$ gem install rails --version 3.2.11 --no-ri --no-rdoc
```
Os parâmetros que passamos são os seguintes:
--version: versão do Rails que utilizaremos no projeto
--no-ri e --no-rdoc: informa que a documentação do Rails não deve ser instalada
junto com o gem. Escolhi esses parâmetros por que torna a instalação mais rápida
e evita utilizar espaço desnecessário -- já que utilizo http://railsapi.com/ para
acessar a documentação quando quero consultar algo. Se você quiser ter a
documentação localmente, basta não utilizar esses parâmetros.
A saída aqui foi assim:
![Inline image 7](http://i4.minus.com/iyG9y4BaY6JE4.png)

Se quiser, liste os gems novamente para checar que a lista aumentou
consideravelmente. Isso se deve ao fato de que Rails depende de outros gems (que
também foram instalados). Então é isso, já podemos usufruir de tudo que Rails
oferece? Já. Como? Criando um novo projeto Rails (que, aqui, chamei de jardas):
```bash
$ rails new jardas
```
Isso cria um novo diretório (chamado jardas) no diretório atual e adivinha só:
esse novo diretório é um projeto Rails! Perceba que a saída do comando é uma lista
de 'create' (Rails já cria uma porrada de arquivos) seguida por um linha 'run
bundle install'. Bundle é uma ferramenta importantíssima que gerencia dependências
do projeto. O comando 'bundle install' instala os gems definidos no arquivo Gemfile
(se notarmos bem, uma das primeiras linhas da série 'create' é 'create Gemfile').
Curioso? É só abrir o Gemfile no seu editor de texto pra ver quais gems são
adicionados por default a um novo projeto Rails.
O bundle install aqui deu em merda.
![Inline image 8](http://i5.minus.com/iq4ugI2eFBnoG.png)

Olhando rapidamente o texto bizarro e colorido desse erro dá pra ver 'sqlite3' em
algum lugar. Opa! Não tenho o sqlite instalado aqui. :B Então deve ser isso.
```bash
$ sudo apt-get install libsqlite3-dev
```
Para executar o bundle install novamente (não esqueça de mudar pro diretório do
projeto -- isto é, dar um 'cd jardas/'):
```bash
$ bundle install
```
Agora funcionou. Maravilha! Então já temos um projeto Rails com todas as suas
dependências instaladas? Temos. Será que essa joça funciona mesmo? Sei lá. Só
testando pra ver...
```
$ rails s
```
Funciona não. Deu um pau muito louco.
![Inline image 9](http://i7.minus.com/ibiELe2Znyba1q.png)

Bem... independentemente do resto da mensagem (que parece incompreensível mesmo),
tem um trecho que diz
```
"Could not find a JavaScript runtime. See https://github.com/sstephenson/execjs for a list of available runtimes."
```
De fato, a url indicada possui uma lista de bibliotecas que parecem ser o que eu
preciso (além disso, ainda explica do que é que se trata, o que torna o erro
ocorrido mais compreensível). É algo relacionado a executar código JavaScript
dentro de código Ruby. Escolhi o primeiro da lista -- um tal de therubyracer.
Legal. E agora? Como é que faz pra instalar isso aí? Ué, do mesmo jeito que
fazemos pra instalar qualquer outro gem: indicando a dependência através do
Gemfile e rodando bundle install.

![Inline image 10](http://i2.minus.com/igKjxhShquGbQ.png)

Oh, fuck! Another problem. O bundle install deu pau de novo.
![Inline image 11](http://i4.minus.com/ibnFLRCe0dNn2L.png)

Agora parece que é algo relacionado a um tal de g++ (UM TAL DE G++? MOTHER FUCKER).
Ah, é. Também não tenho instalado no meu Linux recém instalado. :B
```bash
$ sudo apt-get install g++
```
Agora é só rodar bundle install de novo e correr pro abraço. Dá um 'rails s' aí
pra ver se funciona agora. Se sim, o servidor é iniciado na porta 3000 (padrão do
Rails). Pra ver sua aplicação Rails rodando, é só visitar http://localhost:3000.

No treinamento, hoje, a gente ainda deu uma olhada básica na estrutura do projeto
Rails e começamos a desenvolver alguma coisa. Deixarei isso para uma outra ocasião
por que esta mensagem já está assaz comprida.
