## CD-MOJ

O CD-MOJ é um juiz online direcionado a concursos com exercícios de programação que despacha os códigos para outro juiz online ao invés de executar e verificar a correção da solução. O sistema facilita muito a criação de concursos e sua correção, permitindo uma maior autonomia aos estudantes.

O sistema é dividido em 4 partes para o usuário final: 

- Contest - Visualizar as questões do concurso com seu enunciado e realizar o envio da tentativa de resposta; 
- Score - Visualizar o placar atualizado da competição contendo todos os participantes;
- Trocar senha - Trocar a senha de login;
- Logout - Encerrar a sessão.

Utilizando essas funcionalidades, o CD-MOJ funciona da seguinte maneira: os usuários recebem um login e senha, que são únicos para cada concurso distinto, e acessam o site. Após realizado o login, entram diretamente na página de Contest e tem acesso as questões do concurso vendo seu enunciado e exemplos de casos de teste. Na mesma página é possível realizar a submissão e verificar o código de status retornado pelo juiz online, que pode ser aceito ou recusado, e caso seja recusado pode ser por erro de compilação, erro de execução ou tempo limite excedido.

A execução do fluxograma do processo de julgamento automático do sistema de juiz online é realizada da maneira mostrada na figura abaixo:

![fluxograma](/cd-moj.docs/assets/images/fluxo.png)

O processo de julgamento automático do sistema começa quando o participante realiza uma submissão, onde as informações dessa submissão são salvas através de um arquivo criado no diretório submissions, esse diretório é observado pelo daemon do julgador que irá identificar o arquivo criado e verificar as informações contidas e a partir desse momento identificar que se trata de uma submissão, o arquivo da solução é salvo dentro do diretório submissions-enviaroj observado pelo outro daemon responsável pelo corretor. As informações da submissão são identificadas pelo corretor e uma requisição é disparada para o juiz online identificado. A submissão pode ser redirecionada para dois juízes online que são: o SPOJ e o próprio módulo de correção do CD-MOJ que é chamado de mojtools.

Para o SPOJ é realizada uma requisição para a API na qual vai ser realizada os processos para avaliação da submissão e após isso o resultado será retornado para que o cálculo da pontuação seja feito e as informações da submissão sejam atualizadas para serem entregues ao participante.

Para o mojtools são enviados os dados da submissão e logo após é feita a compilação do código-fonte enviado como solução, se a compilação for concluída com sucesso a solução é executada com casos de teste de entrada e após a execução a saída dessa solução é salva, assim como se houver erro de compilação também é salvo e retornado como um resultado da submissão. Quando o resultado da análise de algum juiz online é retornado, será feito o cálculo da pontuação e as informações da submissão são atualizadas para serem apresentadas ao participante.

## Estrutura

Common Gateway Interface(CGI) é um mecanismo padrão de serviço de invocação que os servidores Web suportam para fornecer conteúdo dinâmico, páginas HTML criadas dinamicamente para responder a consultas/solicitações de usuários ou para executar scripts em segundo plano. Aplicações CGI adicionam ao servidor padrão Web um serviço de acesso à página HTML com um conjunto de funções do site.

A estrutura do CD-MOJ se baseia no CGI, onde o usuário realiza uma requisição através de um browser para o servidor, onde será executado um script. Terminada a execução, os dados são retornados ao servidor e servidos ao browser. Essa estrutura é demonstrada na figura abaixo.

![cgi](/cd-moj.docs/assets/images/cgi.png)

As interações e dependências entre cada um dos scripts são descritas na figura:

![componentes](/cd-moj.docs/assets/images/componentes.png)

Para uma melhor descrição dos scripts acesse as paginas [Judge](judge.md) e [Contesto](contesto.md).