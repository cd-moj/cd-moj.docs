# Judge

> Esse guia explica o funcionamento da parte principal do cd-moj que se trata dos juízes online.

## Daemons

> O funcionamento do sistema do cd-moj se baseia em dois principais módulos que são os daemons responsáveis por comunicar com as APIs dos juízes online, computar os dados dos resultados das submissões e centralizar ações.
>
> Daemons são processos executados em segundo plano e ficam observando alguma ação do sistema ou fornecem funcionalidades a outros processos.

**executar-corretor.sh** e **executar-julgador.sh** são os dois daemons que executam os módulos de correção e julgador, a partir do momento em que são identificados novos arquivos no diretório de submissões que é o $SUBMISSIONDIR é disparado o script **julgador.sh** e quando uma submissão é repassada para o diretorio $SUBMISSIONDIR-enviaroj o script **corrige.sh** é disparado pelo **executar-corretor**.

### Módulo de correção

O módulo de correção disponibilizado pelo arquivo **corrigir.sh** é o responsável por ficar escutando o diretorio **/submissions-enviaroj** onde os dados da submissão são capturados, alguns desses dados são:

*       **ARQ** - Arquivo submetido pelo participante do contest
*       **SITE** - Site de origem do problema
*       **IDSITE** - Identificador do problema
*       **LING** - Linguagem utilizada para resolver o problema
*       **COMANDO** - São diversos comandos responsáveis por identificar ações que serão executadas pelos módulos do cd-moj

Antes de submeter esse problema para o site do juiz online responsável pelo problema é necessário realizar o login para armazenar o cookie do site, esse login é realizado pela função login-**$SITE** especifica para cada juiz. Após essa etapa é realizado a submissão, onde é executada através da função enviar-**$SITE**, essa função tem como parâmetros $SITE, $ARQ, $IDSITE, $LING.

Também responsável por pegar as submissões pendentes, dessas submissões pendentes o seguinte dado é extraido:

*       CODIGOSUBMISSAO -  Código retornado pela função enviar-**$SITE**

O resultado da submissão é retornado pela função pega-resultado-**$SITE**, onde tem como parâmetro o $CODIGOSUBMISSAO e retornar uma resposta da API do juiz.


### Módulo Julgador

O módulo de julgamento é disponibilizado pelo arquivo **julgador.sh** é o responsável por ficar escutando o diretorio $SUBMISSIONDIR e por disparar a maioria dos comandos de ações disponíveis dentro do cd-moj, também são capturados dados igualmente ao módulo de correção, esses dados são:

*       **CONTEST** - O nome do contest do qual o participante fez a submissão
*       **ID** - Identificador da submissão
*       **LOGIN** - Usuário que fez a submissão
*       **COMANDO** - Comando que será executado
*       **PROBID** - Identificador do problema
*       **LING** - Linguagem utilizada para resolver o problema
*       **RESP** - Resposta da submissão enviada

Os comando aceitos pelo cd-moj são:

1.      **newcontest** - A partir desse comando é disparada a ação para criar um contest.
2.      **login** - A partir desse comando é disparada a ação para realizar o login no contest.
3.      **adduser** - Comando utlizado para adicionar um novo usuário ao contest com **"mojinho:abc"** e a flag ALLOWLATEUSER, essa ação é realizada pelo bot do telegram **mojinho**.
4.      **passwd** - A partir desse comando é disparada a ação para trocar a senha do participante do contest.
5.      **rejulgado** - A partir desse comando é disparada a ação para computar o novo score da submissão que foi rejulgada.
6.      **corrigido** - A partir desse comando é disparada a ação para computar o score da submissão que foi julgada.
7.      **rejulgar** - A partir desse comando é disparada a ação para colocar a submissão na fila para ser rejulgada.
8.      **answer** - A partir desse comando é disparada a ação para adicionar uma mensagem geral para o contest.
9.      **submit** - A partir dese comando é disparada a ação para copiar os arquivos das submissões para as respectivas pastas.