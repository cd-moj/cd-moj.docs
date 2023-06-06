### Script de criação de contest

Dentro do diretório **bin** é disponibilizado o script **cria-contest.sh** responsável por configurar toda a estrutura do contest.

---

### Scripts de API

A seguir, são descritos os scripts que se comunicam com as APIs dos juízes online e com o próprio juiz do cd-moj. São duas APIs que são utilizadas, além da própria API do cd-moj.

- **enviar-cdmoj.sh** - Dentro desse script há 3 funções:
  - **login-cdmoj** - Responsável por enviar os dados da submissão ao juiz.
  - **enviar-cdmoj** - Responsável por submeter ao juiz os dados da submissão.
  - **pega-resultado-cdmoj** - Responsável por obter o resultado da submissão retornado pelo juiz.
- **enviar-spoj.sh** - Este script disponibiliza oito funções que englobam tanto o spoj oficial quanto o spoj-br:
  - **enviar-spoj** - Realiza uma requisição à API do SPOJ e envia os dados da submissão com a solução do problema.
  - **pega-resultado-spoj** - Recupera a resposta do juiz online por meio de uma requisição.
  - **login-spoj-br** - Realiza uma requisição e salva o cookie do login spoj-br se a requisição for bem-sucedida.
  - **login-spoj-www** - Realiza uma requisição e salva o cookie do login spoj-www se a requisição for bem-sucedida.
- ~~enviar-uri.sh~~ **[Depreciado]** - Dentro desse script há funções responsáveis por fazer requisições para o antigo URI online judge, essas funções são: - **login-uri** - Realiza uma requisição e salva o cookie do login se a requisição for bem sucedida. - **enviar-uri** - Responsável por realizar uma requisição para a API do URI e enviar os dados da submissão com a solução do problema. - **pega-resultado-uri** - Responsável por recuperar a resposta do juiz online por uma requisição através do ID da submissão.
- **cdmoj-cgi.sh** - Script responsável por redirecionar para os problemas do cd-moj.
- **spoj-cgi.sh** - Script responsável por redirecionar para os problemas do spoj e spoj-br.
- ~~uri-cgi.sh~~ **[Depreciado]** - Script responsável por redirecionar para os problemas do URI.
- **oj-links.sh** - Script que o CGI deve originar para obter as funções do CGI.

**OBS:** Caso ocorra algum erro no envio da submissão para os respectivos sites, verifique a existência dos arquivos **$HOME/.cache/cookie-spoj-www** ou **$HOME/.cache/cookie-spoj-br**.

---

### Arquivos de configuração

Dentro do diretório **etc** são encontrados dois arquivos:

- **common.conf** - Declara variáveis contendo os caminhos para os diretórios utilizados pelo sistema cd-moj.
- **judge.conf** - Declara variáveis que contêm os dados para realizar requisições às APIs dos juízes.

---

### Formato de arquivo com contest

O cd-moj disponibiliza dois meios para criação de contest, o primeiro por meio do envio de um arquivo contento os arquivos necessários para o sistema carregar o contest e o segundo através do formulário presente dentro da [área do administrador](#administrador).

---

### contest-description.txt

Dentro de um arquivo de contest deve conter um arquivo chamado **contest-description.txt** e uma pasta chamada **enunciados** e dentro dela deve conter todos os arquivos dos problemas que estarão presentes no contest.

O arquivo responsável pela criação dos contests deve seguir um modelo específico

```
ID_PADRAO_UNIX
"Nome Completo do Contest"
Data e hora de inicio em segundos
Data e hora de termino em segundos
Quantidade problemas
SITE ID "Nome Completo" item_contest link-enunciado
Numero-de-usuarios
login:senha:Nome Completo
login.admin:senha:Usuario do Tipo Administrador
login.mon:senha:Usuario do Tipo Monitor
Diretivas
```

- **ID_PADRAO_UNIX** - Um identificador único para o contest, não deve haver espaços.
- **Data e hora de início e fim** - Podem ser geradas pelo comando:
  `date --date="15:00:00 today" +%s`
- **Quantidade de problemas** - Deve ser um número inteiro.
- **SITE** - Identificador para o site de origem do problema, podendo ser spoj-br ou spoj-www.
- **ID** - É o ID do problema no SITE
- **Nome completo** - É o nome completo do problema, deve estar entre aspas.
- **item_contest** - É o item do problema dentro do contest, numérico ou alfanumérico. É recomendável, que sejam colocados em ordem.
- **link-enunciado** - São os endereços responsáveis por redirecionar para cada um dos problemas em seus respectivos sites, há três tipos:
  - **site** - Redireciona para o site, que deve ser um link inciando por http://.
  - **sitepdf** - Redireciona para o pdf do site.
  - **nome** - O nome do arquivo que pode está dentro do diretório de enunciados(Se a extensão do arquivo for omitida é utilizado todos os arquivos).
  - **none** - Para não ter um enunciado.
- **Número de usuários** - Deve ser um número inteiro designando o total de usuários no contest.
- **Diretivas** - Diretivas são algumas flags dentro do sistema do cd-moj que fornecem permissão a certas funcionalidades, são elas:
  - **LANGUAGES** - Define quais linguagens são aceitas pelo contest.
  - **PASSWD** - Define se a troca de senhas no contest é permitida. Se PASSWD=1 essa troca é permitida.
  - **PENALTYCOST** - PENALTYCOST=n implica uma penalidade de n minutos por submissão errada (n inteiro).
  - **PARTIALSTATISTIC** - Quando 1 permite acesso público às estatísticas durante a execução do contest (padrão = 0).
  - **STATISTICS** - Quando 0 não permite acesso público às estatísticas após o encerramento do contest (padrão = 1).
  - **ALLOWLATEUSER** - Quando y permite cadastro posterior de usuário por interação com o bot do telegram **@mojinho** (padrão = n).
  - **SHOWCODE** - Quando 1 mostra o código da submissão. (padrão = 0).
  - **CLARIFICATION** - Quando 1 permite acesso as abas de clarification. (padrão = 0).

Segue um exemplo de um arquivo preenchido

```
doc_cdmoj
"Documentação CD-MOJ"
1627804800
2227420800
4
spoj-br PLACAR "Quem vai ser reprovado?" A reprovado.txt
cdmoj cartasfora "Jogando Cartas Fora" B jogando-cartas-fora.pdf
spoj-www TEST "Life, the Universe, and Everything" C https://www.spoj.com/problems/TEST/
spoj-br CONTAGEM "Não é Mais um Joguinho Canadense" D contagem.txt
4
winchester.admin:senhasecretaADMIN:Dean winchester Administrador
luffy.mon:senhasecretaMon:Monkey D. luffy Monitor
ribas:fiesta:Bruno Ribas
ricardo:busao:Ricardo Oliveira
CLARIFICATION=1
SHOWCODE=1
```

---

### Formulário

O formulário segue os mesmos padrões dos dados explicados em [contest-description.txt](#contest-descriptiontxt).

![form](../../assets/images/form_create_contest.jpg)

---

### Administrador

Para criar um contest é necessário um usuário administrador para poder enviar um arquivo com contest ou submeter um formulário com os dados necessários. Para isso é preciso criar um diretório dentro do caminho **/moj/contests/** chamado admin, logo após crie dois arquivos chamados **conf** e **passwd**. Segue o exemplo dos arquivos:

#### conf

```
CONTEST_ID="admin"
CONTEST_NAME="admin"
CONTEST_START=Gere uma data de inicio utilizando o comando "date --date="15:00:00 today" +%s"
CONTEST_END=Gere uma data de termino utilizando o comando "date --date="15:00:00 today" +%s"
```

#### passwd

```
usuario.admin:senhaAdmin:Usuario Administrador
```
