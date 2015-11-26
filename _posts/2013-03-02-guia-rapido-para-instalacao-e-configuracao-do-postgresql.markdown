---
layout: post
title: "Guia Rápido para Instalação e Configuração do PostgreSQL"
date: 2013-03-02 19:26:45 -0300
comments: true
categories: [banco de dados, tutorial, passo-a-passo, instalação, configuração, linux, postgresql, puppy, puppylinux, pt_BR]
---

### Um Pouco de Blábláblá

Ontem eu tive minha primeira experiência (pra valer) de utilização do PuppyLinux [1][2]. Quis experimentar o S.O. por que as máquinas do Centro de Informática tolhem completamente o usuário comum (leia-se aluno) quanto à instalação de ferramentas e, desenvolvendo um projeto RoR atualmente, preciso instalar várias delas.

A ideia inicial é, portanto, rodar um ambiente de desenvolvimento Ruby on Rails direto de um pendrive com o S.O. PuppyLinux. Nesta postagem não abordarei o processo completo de setup do ambiente (que me custou a tarde e a noite de ontem) mas apenas uma das partes -- supostamente -- mais laboriosas: a instalação (na mão, é claro) do PostgreSQL.

<!-- more -->

### 1º Passo: Download

A página de download do Postgres fornece binários pré-compilados para vários S.O.s. No meu caso, pra instalar no Puppy, baixei o fonte desta página. A versão que escolhi foi a 9.1.7 [3].

### 2º Passo: Compilar e instalar

Descompactação:
```bash
$ tar xvjf postgresql-9.1.7.tar.bz2
```
Mudar para o diretório novo:
```bash
$ cd postgresql-9.1.7/
```
Preparar instalação:
```bash
$ ./configure
```
e
```bash
$ gmake
```
Mudar para usuário super:
```bash
$ su
```
Instalar: asd
```bash
# gmake install
```

### 3º Passo: Configurar e rodar

Criar o usuário (no Linux) 'postgres':
```bash
# adduser postgres
```
Criar o diretório onde ficarão os arquivos do BD:
```bash
# mkdir /usr/local/pgsql/data
```
Dar permissão ao usuário postgres:
```bash
# chown postgres /usr/local/pgsql/data
```
Mudar para usuário postgres:
```bash
# su - postgres
```
Iniciar o banco:
```bash
# /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
```
Iniciar o processo do Postgres:
```bash
# /usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data >logfile 2>&1 &
```

### 4º Passo: Testar a criação de um banco

```bash
# /usr/local/pgsql/bin/createdb test
```
e, para acessar o banco:
```bash
# /usr/local/pgsql/bin/psql test
```

### 5º Post-Install: Linkar comandos e criar um outro usuário

Não sei se você percebeu mas, para rodar os comandos do postgres nas linhas de comando anteriores, precisamos utilizar o caminho completo para o diretório onde o comando se encontra. Isso é um saco. Pra resolver, criei links simbólicos para todos os comandos presentes em "/usr/local/psql/bin/psql". Assim:
```bash
# for f in $(ls -d /usr/local/pgsql/bin/*); do ln -s $f /usr/local/bin; done
```
Agora só falta uma coisa: criar um usuário do Postgres com o nome do seu usuário Linux. Saia do usuário super (com um simples 'exit') e comande:
```bash
$ sudo -u postgres createuser --superuser $USER
```
E finalmente, para configurar uma senha para seu novo usuário, acesse a ferramenta de linha de comando do Postgres:
```bash
$ sudo -u postgres psql
```
e (substitua $USER pelo nome de seu usuário Linux)
```bash
postgres=# \password $USER
```
Beleza. Agora você já pode acessar o Posgres com o seu usuário e, no caso de estar desenvolvendo um projeto Rails, configurar o database.yml com seus dados de usuário e senha.

### Referências

* [1] http://puppylinux.com
* [2] http://puppylinux.org
* [3] http://ftp.postgresql.org/pub/source/v9.1.7/postgresql-9.1.7.tar.bz2
* [4] http://www.postgresql.org/docs/9.0/static/install-short.html
* [5] http://www.commandlinefu.com/commands/view/1225/symlink-all-files-from-a-base-directory-to-a-target-directory
