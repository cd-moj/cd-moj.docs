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
- <s>enviar-uri.sh</s> **\[Depreciado\]** - Dentro desse script há funções responsáveis por fazer requisições para o antigo URI online judge, essas funções são: - **login-uri** - Realiza uma requisição e salva o cookie do login se a requisição for bem sucedida. - **enviar-uri** - Responsável por realizar uma requisição para a API do URI e enviar os dados da submissão com a solução do problema. - **pega-resultado-uri** - Responsável por recuperar a resposta do juiz online por uma requisição através do ID da submissão.
- **cdmoj-cgi.sh** - Script responsável por redirecionar para os problemas do cd-moj.
- **spoj-cgi.sh** - Script responsável por redirecionar para os problemas do spoj e spoj-br.
- <s>uri-cgi.sh</s> **\[Depreciado\]** - Script responsável por redirecionar para os problemas do URI.
- **oj-links.sh** - Script que o CGI deve originar para obter as funções do CGI.

**OBS:** Caso ocorra algum erro no envio da submissão para os respectivos sites, verifique a existência dos arquivos **$HOME/.cache/cookie-spoj-www** ou **$HOME/.cache/cookie-spoj-br**.

---

### Arquivos de configuração

Dentro do diretório **etc** são encontrados dois arquivos:

- **common.conf** - Declara variáveis contendo os caminhos para os diretórios utilizados pelo sistema cd-moj.
- **judge.conf** - Declara variáveis que contêm os dados para realizar requisições às APIs dos juízes.

---
