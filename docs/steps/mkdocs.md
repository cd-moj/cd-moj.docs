## Contribuição

Para contribuir com a documentação do CD-MOJ leia esse arquivo para entender o funcionamento da tecnologia utilizada, que é o Mkdocs.

---

### Mkdocs

O MkDocs utiliza o Markdown, uma linguagem de marcação leve, como formato principal para escrever a documentação. O Markdown oferece uma sintaxe simples que é fácil de ler e escrever, tornando-o acessível tanto para usuários técnicos quanto não técnicos. Com o MkDocs, você pode escrever o conteúdo da sua documentação em arquivos Markdown e, em seguida, gerar um site estático a partir desses arquivos.

---

### Começando
Faça o clone do repositorio de documentação com o comando:

```
git clone https://github.com/cd-moj/cd-moj.docs
git switch main
```
Note que a temos duas branchs **gh-deploy** onde estão os arquivos de deploy, a aplicação após o build e **main** onde estão os arquivos source. Assim, as alterações devem ser feitas na branch **main**. para mais informaçẽos acesse a documentação do [Mkdocs](https://www.mkdocs.org/user-guide/deploying-your-docs/)

### mkdocs serve

Para subir localmente a aplicação use o comando

```
mkdocs serve
```

---

### mkdocs build

Para buildar e gerar os html's automaticamente utilize o comando

```
mkdocs build
```

---

### mkdocs gh-deploy

Para realizar o deploy utilize o comando

```
mkdocs gh-deploy
```
Importante verificar as alterações feitas nos documentos de antemão usando os comandos **build** ou **serve**.