### Instalando pré-requisitos

```bash
$ apt update
$ apt install gcc git apache2 rsync xclip curl default-jre default-jdk openjdk-17-jre openjdk-17-jdk
```

---

### Instalando CD-MOJ

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
