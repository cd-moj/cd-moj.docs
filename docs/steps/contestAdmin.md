# Guia para subir contest

## Daemons

O primeiro passo é importante se você esta rodanto uma instância local é subir ambos daemons, executar-corretor.sh e executar-julgador.sh, e se certificar de que ambos estão conversando entre si corretamente. Os comandos para subir ambos daemons são: `bash executar-julgador.sh` e `bash executar-corretor.sh`

---

## Exercícios

É possível que você não tenha acesso nas máquinas do Ribas que corrigem os exercícios, logo é interessante que se utilize exercícios listados no Spoj e é necessário que você tenha uma conta criada no mesmo e cadastrada no arquivo judge.conf.

---

## Contest

O arquivo contest-description.txt deve estar corretamente preenchido e precisa obrigatoriamente estar compactado no formato **.tar** seguindo o exemplo abaixo:

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

## Passo a passo para criar um contest

1. É necessário entrar no link de [administrador](https://moj.naquadah.com.br/cgi-bin/admin.sh) e realizar o login;
2. Clicar na aba Old School;
3. Adicionar o arquivo contest-description.tar na opção "Envie novo contest" e clicar em submit;
4. Conferir se o contest foi criado com sucesso observando o Log disponibilizado logo abaixo da aba Old School;

---

### Formulário

Você tambem pode criar um contest por meio de um formulário, segue os mesmos padrões dos dados explicados em [contest-description](#contest-descriptiontxt).

![form](/steps/assets/form_create_contest.jpg)

---

## Passo a passo para entrar no contest

1. É necessário entrar no link [localhost contest](http://localhost/cgi-bin/index.sh);
2. Realizar o login com a conta e nível desejado;

---

## Possíveis erros

Se houve algum erro ao criar um contest em uma instância local certifique se os steps foram seguidos corretamente [Daemons](#daemons), [Exercícios](#exercicios) e [Contest](#contest). Para mais informações entrar no root do seu pc utilizando os comandos abaixo:

```
sudo -i
tail -f /var/log/apache2/*.log

```
