# Judge

Esse guia explica o funcionamento da parte principal do cd-moj que se trata dos juízes online.

---

### Daemons

O sistema do CD-MOJ é baseado em dois principais daemons, responsáveis por se comunicar com as APIs dos juízes online, processar os resultados das submissões e coordenar as ações.

> Daemons são processos executados em segundo plano que observam eventos do sistema ou fornecem funcionalidades a outros processos.

**executar-corretor.sh** e **executar-julgador.sh** são os dois daemons que executam os módulos de correção e julgador, a partir do momento em que são identificados novos arquivos no diretório de submissões que é o **$SUBMISSIONDIR** é disparado o script **julgador.sh** e quando uma submissão é repassada para o diretorio **$SUBMISSIONDIR-enviaroj** o script corrige.sh é disparado pelo **executar-corretor.sh**

---

### Módulo de correção

O módulo de correção disponibilizado pelo arquivo **corrigir.sh** é responsável por monitorar o diretório **/submissions-enviaroj** e capturar os dados da submissão, incluindo:

- **ARQ** - Arquivo submetido pelo participante do contest
- **SITE** - Site de origem do problema
- **IDSITE** - Identificador do problema
- **LING** - Linguagem utilizada para resolver o problema
- **COMANDO** - São diversos comandos responsáveis por acionar ações executadas pelos módulos do CD-MOJ

Antes de submeter esse problema para o site do juiz online responsável pelo problema, é necessário realizar o login para armazenar o cookie do site. O login é realizado pela função **login-$SITE** especifica para cada juiz. Após essa etapa, a submissão é feita através da função **enviar-$SITE**, que recebe os parâmetros **$SITE**, **$ARQ**, **$IDSITE** e **$LING**.

O módulo também é responsável por obter as submissões pendentes, de onde é extraído o seguinte dado:

- **CODIGOSUBMISSAO** - Código retornado pela função **enviar-$SITE**

O resultado da submissão é retornado pela função **pega-resultado-$SITE**, onde tem como parâmetro o **$CODIGOSUBMISSAO** e retornar uma resposta da API do juiz.

---

### Módulo Julgador

O módulo de julgamento é disponibilizado pelo arquivo **julgador.sh** é responsável por monitorar o diretório **$SUBMISSIONDIR** e acionar a maioria dos comandos disponíveis no CD-MOJ. Assim como no módulo de correção, ele captura dados como:

- **CONTEST** - O nome do contest do qual o participante fez a submissão
- **ID** - Identificador da submissão
- **LOGIN** - Usuário que fez a submissão
- **COMANDO** - Comando que será executado
- **PROBID** - Identificador do problema
- **LING** - Linguagem utilizada para resolver o problema
- **RESP** - Resposta da submissão enviada

Os comando aceitos pelo CD-MOJ são:

- **newcontest** - A partir desse comando é disparada a ação para criar um contest.
- **login** - A partir desse comando é disparada a ação para realizar o login no contest.
- **adduser** - Comando utlizado para adicionar um novo usuário ao contest com **"mojinho:abc"** e a flag ALLOWLATEUSER, essa ação é realizada pelo bot do telegram **mojinho**.
- **passwd** - A partir desse comando é disparada a ação para trocar a senha do participante do contest.
- **rejulgado** - A partir desse comando é disparada a ação para computar o novo score da submissão que foi rejulgada.
- **corrigido** - A partir desse comando é disparada a ação para computar o score da submissão que foi julgada.
- **rejulgar** - A partir desse comando é disparada a ação para colocar a submissão na fila para ser rejulgada.
- **answer** - A partir desse comando é disparada a ação para adicionar uma mensagem geral para o contest.
- **submit** - A partir dese comando é disparada a ação para copiar os arquivos das submissões para as respectivas pastas.
