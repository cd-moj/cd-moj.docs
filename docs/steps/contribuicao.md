# Guia de contribuição

## 1. Introdução

**Como contribuir para o projeto CD-MOJ ?**

Siga as diretrizes abaixo.

___
## 2. Diretrizes para contribuir


### 2.1 Politica de branches

A politica de branchs adotada é realizar todas as mudanças diretamente na main.

#### OBS.: Repositório de documentação
Note que a temos duas branchs gh-deploy onde estão os arquivos de deploy, a aplicação após o build e main onde estão os arquivos source. Assim, as alterações devem ser feitas na branch main.

___
### 2.2 Politica de Issues

A criação de novas _issues_ deverá seguir um dos padrões estabelecidos abaixo:

- [_Bug_](https://github.com/cd-moj/cd-moj.docs/blob/main/.github/ISSUE_TEMPLATE/relat%C3%B3rio-de-bug.md): para relatar problemas, erros, defeitos ou falhas;

- [_Fix_](https://github.com/cd-moj/cd-moj.docs/blob/main/.github/ISSUE_TEMPLATE/relat%C3%B3rio-de-conserto.md): quando for descrever funcionalidades que precisam de revisão;

- [Doc](https://github.com/cd-moj/cd-moj.docs/blob/main/.github/ISSUE_TEMPLATE/relat%C3%B3rio-de-documenta%C3%A7%C3%A3o.md): utilizado para criar ou alterar a documentação;

- [Feat](https://github.com/cd-moj/cd-moj.docs/blob/main/.github/ISSUE_TEMPLATE/relat%C3%B3rio-de-funcionalidade.md): quando for descrever funcionalidades que precisam sem implementadas.


___
### 2.3 Política de Commit

Os _commits_ deverão seguir o padrão proposto a seguir:

- A descrição de um _commit_ deve ser escrita em Português;

- Um _commit_ deve referenciar o caminho do principal arquivo alterado;

- Um _commit_ deve representar uma unidade de trabalho. Por exemplo: não adicionar arquivos relacionados a _issues_ diferentes no mesmo _commit_;

- Um _commit_ deve ser significativo, ou seja, deve explicar as alterações realizadas.

Exemplo: **Issue 1: \[Feat\]: Botão que muda senha**

```
git commit -m "<path do arquivo>: <descrição significativa>"
```

___
### 2.4 Pareamento

Para tarefas realizadas em pares, os _commits_ precisam seguir o seguinte padrão:

```
Descrição do commit

Signed-off-by: Nome do responsável <nome@gmail.com>
Co-authored-by: Nome de quem auxiliou <auxiliador@gmail.com>
```

Obs.: o email PRECISA ser o mesmo que está vinculado à conta do Github.

- **'Signed-off-by: '** deve ser preenchido pelo responsável pelo código;

- **'Co-authored-by:'** deve ser preenchido por quem prestou auxílio durante a tarefa.
