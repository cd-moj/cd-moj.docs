
### Instalando CD-MOJ

A correta instalação deve ser feita ao utilizar o Makefile disponibilizado no repositório do CD-MOJ. Siga os passos abaixo:

```bash
$ git clone https://github.com/cd-moj/cdmoj.git
$ cd cdmoj
$ sudo make SERVERDIR=$HOME/test/server HTMLDIR=$HOME/test/client
```

Caso algum problema ocorra, utilize os passos contidos abaixo e na configuração:
### Instalando pré-requisitos

```bash
$ apt update
$ apt install gcc git apache2 rsync xclip curl default-jre default-jdk openjdk-17-jre openjdk-17-jdk
```
---

```bash
$ mkdir $HOME/cdmoj
$ mkdir $HOME/cdmoj/moj
$ mkdir $HOME/cdmoj/tmp
```

```bash
$ git clone https://github.com/cd-moj/cdmoj.git
$ cd cdmoj
$ chmod +x install.sh
$ bash install.sh $HOME/cdmoj/moj-serverside $HOME/cdmoj/moj-pagina
```
