---
layout: post
title: "Tutorial: Pull Request através de branches distintos num mesmo repositório"
date: 2013-02-08 19:09:45 -0300
comments: true
categories: [git, rails, ror, ruby, github, passo-a-passo, tutorial, pt_BR]
---

Pessoal,

terminei de implementar a funcionalidade que escolhi (Autenticação com Facebook) e vou aproveitar minhas modificações para dar um exemplo de como é aquele fluxo de criação de novo branch e pull request usando o git e o Github. Segui o algoritmo e, no momento, eu deveria estar no passo 6 (abra a imagem em uma nova aba ou janela para ver em seu tamanho original)
![Inline Image](http://i.minus.com/ill0y8RRJeriz.png)

Acontece que eu esqueci de executar o passo 4 (afinal, estava com muito sono), o que não é de todo ruim por que serve para mostrar o que fazer no caso de acontecer o mesmo com algum de vocês.

<!-- more -->

Mas atenção: se você fez o que o passo 4 diz (criou e utilizou um novo branch para a inclusão das modificações), pode pular isso que vou fazer agora e passar direto para a etapa de criação do commit. Executando um simples
```bash
$ git status
```
é isso que obtenho como resultado:
![Inline Image](http://i.minus.com/itqnNxt69zTSo.png)

Passando as Modificações para o Branch Correto

Observem que estou no branch master e tenho vários arquivos modificados e untracked. Não era bem isso que eu queria. Queria ter todos esses arquivos modificados e untracked em outro branch para que eu pudesse, então, usar 'git add' e criar um commit com todas essas modificações. Como resolver essa bronca? Bem.. há algumas maneiras diferentes de se fazer isso e eu optei por uma que considero bastante simples: 'git stash'.

Antes usar o comando stash do git, preciso adicionar tudo como se fosse criar um commit. O stash é mais ou menos um commit que não vai pra lugar nenhum. Adicionando todas as minhas modificações:
```bash
$ git add .
```
Chamando 'git status' novamente, vejo os arquivos que foram adicionados ao index e estão prontos para entrar num novo commit:
![Inline Image](http://i.minus.com/iBdt6ThpNFmXt.png)

O status mostra que há um arquivo no status 'deleted'. Para efetivar essa modificação no git é necessário executar
```bash
$ git rm spec/controllers/games_controller_controller_spec.rb
```
Depois disso, executando 'git status' novamente, vejo que todas as modificações (inclusive novos arquivos e arquivos removidos) foram inseridas ao index e estão prontas para ser commitadas (aparecem em verde). Agora, pra fazer o stash entrar em ação:
```bash
$ git stash
```
O comando dá como saída uma mensagem informando que as modificações foram salvas no stash e que o HEAD agora está no último commit. O stash funciona em regime de pilha. Se eu continuasse fazendo modificações, adicionasse com 'git add' e chamasse 'git stash' de novo, essas novas modificações seriam empilhadas sobre o último stash. O comando para listar tudo o que há na pilha de stash é
```bash
$ git stash list
```
Depois de salvar as modificações no stash, o 'git status' fica limpo novamente (sem aquele monte de arquivos modificados e untrackeds resultantes da minha implementação).
![Inline Image](http://i.minus.com/iiceUtgqKUzWx.png)

Percebam que o arquivo '.rvmrc' está na seção untracked (o que não acontecia antes) por que o arquivo .gitignore que informava ao git para ignorar o .rvmrc foi mandado pro stash. De qualquer maneira, não há problemas em que ele permaneça aí por que a seção untracked (como já deve ser sabido) exibe arquivos que não estão sendo versionados com o git.

Beleza. Agora que já tenho todas as minha modificações em um lugar que posso recuperar depois e meu branch master voltou a ser o que era antes de eu começar a implementação, meu próximo passo é criar meu novo branch e dar um checkout pra ele (isto é, informar ao git que quero trabalhar nesse branch). Para criar um novo branch a partir do branch em que estou atualmente (no caso, estou no branch master), basta executar
```bash
$ git branch fb-connect
```
em que 'fb-connect' é o nome do meu branch (escolhido arbitrariamente por mim). Isso cria o branch mas não o seleciona. Para mudar para o branch:
```bash
$ git checkout fb-connect
```
Agora, sim, estamos trabalhando no branch recém-criado. Git oferece uma maneira de encurtar o caminho para criar um novo branch e dar checkout nele com um comando só, que é o seguinte:
```bash
$ git checkout -b fb-connect
```
O argumento '-b' informa que o branch para o qual se está dando checkout é um novo branch. Para confirmar que de fato estamos trabalhando num novo branch podemos rodar o popular 'git status' ou
```bash
$ git branch
```
que lista todos os branches no repositório local ou
```bash
$ git branch -a
```
que lista todos os branches -- tanto no repositório local quanto nos remotos (a stands for all).
![Inline Image](http://i.minus.com/ibpwfGJQg0wD3N.png)

Estamos preparados para remover aquelas modificações colocadas no stash e aplicá-las no novo branch! Para fazer isso:
```bash
$ git stash pop
```
Isso aplica as mudanças, já adicionando os novos arquivos ao stage -- isto é, prontos para ser commitados. Arquivos modificados e removidos vão para a seção de not staged, de acordo com a comparação com o último commit da árvore de commits do branch (que é onde o HEAD se encontra).
![Inline Image](http://i.minus.com/ibuvZnHpXlqYc3.png)

Criando e Enviando o Novo Commit ao Repositório Remoto

Para adicionar tudo ao commit que iremos criar, já sabe, né? 'git add .' e 'git rm <caminho/para/o/nome do arquivo a ser removido>...'. Depois de fazer isso, todas as modificações aparecem em verde ao dar um novo 'git status' -- o que significa que serão adicionadas ao novo commit, que criaremos com:
```bash
$ git commit -m "Introduz funcionalidade de login com conta do Facebook"
```
Se dermos um 'git status' novamente, veremos que nosso diretório de trabalho está limpo (nada pra commitar) e executando
```bash
$ git log
```
podemos listar todos os commits.
![Inline Image](http://i.minus.com/i9EylLqwxG1bM.png)

Atente para o fato de que o último commit ("Introduz funcionalidade[...]") só existe no branch em que estamos atualmente! Se dermos 'git checkout master' e 'git log' ele não ira aparecer. O commit também não existe no repositório remoto. Na verdade, o branch que criamos ainda não existe no remoto também. Para subir nosso código para o repositório remoto (hosteado pelo Github), precisamos rodar o comando
```bash
$ git push origin fb-connect
```
em que origin é o nome do remoto (você pode ver os nomes e os endereços dos remotos cadastrados no seu repositório local através de 'git remote -v') e fb-connect é o nome do branch para o qual o push será feito.
![Inline Image](http://i.minus.com/ivF35JHY3ZLa4.png)

Criando o Pull Request

Agora o nosso novo branch (com o commit que possui as modificações) já está no repositório remoto e pode ser visualizado através da interface web do Github (https://github.com/embs/gaming/tree/fb-connect). É justamente de lá que iremos realizar o pull request para solicitar que o código adicionado e modificado seja integrado ao branch principal (master). Isso é bem fácil de fazer (nem precisa de linha de comando -- pra ser sincero, não sei como fazer por linha de comando nem se há como fazer por linha de comando): basta clicar no botão bonito (Pull Request) do Github. :)
![Inline Image](http://i.minus.com/ipN3MizF4CLOd.png)

Depois aparece um formulário em que você pode dar mais detalhes (além do texto da mensagem do último commit) sobre o que você fez nesse novo branch. Ah! outra coisa importante nessa tela é a informação de qual pra qual branch o pull request está sendo feito. Nesse caso, estou solicitando para que o código do fb-connect vá para o master.
![Inline Image](http://i.minus.com/ib2xwxNGb0RXhF.png)

E aí é só "Send pull request".
![Inline Image](http://i.minus.com/iA4gdblA4YL7o.png)

E correr pro abraço! Ou melhor... ir para o passo 7 do passo-a-passo. :/
