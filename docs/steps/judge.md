# Judge

Esse guia explica o funcionamento da parte principal do cd-moj que se trata dos juízes online.

---

### Daemons

O sistema do CD-MOJ é baseado em dois principais daemons, responsáveis por se comunicar com as APIs dos juízes online, processar os resultados das submissões e coordenar as ações.

> Daemons são processos executados em segundo plano que observam eventos do sistema ou fornecem funcionalidades a outros processos.

executar-corretor.sh e executar-julgador.sh são os dois daemons que executam os módulos de correção e julgador.

Quando o usuário submete um problema, a submissão é salva dentro do diretório submissions-enviaroj especificado pelo script responsável por tratar das submissões dentro do CD-MOJ. O daemon que executa o corretor fica observando o diretório até que uma submissão seja realizada. Quando uma submissão é identificada, o daemon aciona o script corrige.sh. As validações e verificações dos dados são realizadas e se todas forem aceitas, o problema é enviado para a API específica. Ao retornar com o resultado, o mesmo é devolvido e salvo no database. Essa sequência é demonstrada pelo diagrama:

![corretor](/cd-moj.docs/assets/images/corretor.png)

O daemon responsável por executar o julgador fica esperando os resultados serem salvos e, após esse processo, é acionado o script julgador.sh. Ocorrerão validações e verificações para identificar os fluxos representados na Figura 7, e tais fluxos podem ter a possibilidade de adicionar um novo usuário pelo bot mojinho, realizar um login, criar um contest, rejulgar um problema, além de gravar soluções no database e computar as pontuações das listas, provas ou contests. Esses passos são demonstrados pelo diagrama:

![julgador](/cd-moj.docs/assets/images/julgador.png)


---

### Módulo de correção

O módulo de correção disponibilizado pelo arquivo corrigir.sh é responsável por monitorar o diretório /submissions-enviaroj e capturar os dados da submissão, incluindo:

- **ARQ** - Arquivo submetido pelo participante do contest
- **SITE** - Site de origem do problema
- **IDSITE** - Identificador do problema
- **LING** - Linguagem utilizada para resolver o problema
- **COMANDO** - São diversos comandos responsáveis por acionar ações executadas pelos módulos do CD-MOJ

Antes de submeter esse problema para o site do juiz online responsável pelo problema, é necessário realizar o login para armazenar o cookie do site. O login é realizado pela função login-$SITE especifica para cada juiz. Após essa etapa, a submissão é feita através da função enviar-$SITE, que recebe os parâmetros $SITE, $ARQ, $IDSITE e $LING.

O módulo também é responsável por obter as submissões pendentes, de onde é extraído o seguinte dado:

- **CODIGOSUBMISSAO** - Código retornado pela função enviar-$SITE

O resultado da submissão é retornado pela função pega-resultado-$SITE, onde tem como parâmetro o $CODIGOSUBMISSAO e retornar uma resposta da API do juiz.

---

### Módulo Julgador

O módulo de julgamento é disponibilizado pelo arquivo julgador.sh é responsável por monitorar o diretório $SUBMISSIONDIR e acionar a maioria dos comandos disponíveis no CD-MOJ. Assim como no módulo de correção, ele captura dados como:

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
- **adduser** - Comando utlizado para adicionar um novo usuário ao contest com "mojinho:abc" e a flag ALLOWLATEUSER, essa ação é realizada pelo bot do telegram mojinho.
- **passwd** - A partir desse comando é disparada a ação para trocar a senha do participante do contest.
- **rejulgado** - A partir desse comando é disparada a ação para computar o novo score da submissão que foi rejulgada.
- **corrigido** - A partir desse comando é disparada a ação para computar o score da submissão que foi julgada.
- **rejulgar** - A partir desse comando é disparada a ação para colocar a submissão na fila para ser rejulgada.
- **answer** - A partir desse comando é disparada a ação para adicionar uma mensagem geral para o contest.
- **submit** - A partir dese comando é disparada a ação para copiar os arquivos das submissões para as respectivas pastas.
