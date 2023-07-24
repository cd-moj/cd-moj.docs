## Daemons

O primeiro passo é importante se você esta rodanto uma instância local é subir ambos daemons, executar-corretor.sh e executar-julgador.sh, e se certificar de que ambos estão conversando entre si corretamente. Os comandos para subir ambos daemons são: `bash executar-julgador.sh` e `bash executar-corretor.sh`

---

## Simular Login

Para simular o login em contests siga os passos abaixo:

```bash
$ cp <path para pasta com os arquivos de login>/*:login:* <path para pasta submissions do CD-MOJ>

``` 
Ao copiar os arquivos de login para a pasta **cd-moj/submissions** o daemon **julgador.sh** fará com que ele percorra seu caminho natural pelo sistema.

**Ex.: **
```bash
$ cp ~/Downloads/login-subs/*:login:* ~/cd-moj/submissions

``` 

___


## Simular Submissão

Para simular submissões em contests siga os passos abaixo:

```bash
$ cp <path para pasta com os arquivos de submissão>/*:submit:* <path para pasta submissions do CD-MOJ>

```
Ao copiar os arquivos de submissão para a pasta **cd-moj/submissions** o daemon **julgador.sh** fará com que ele percorra seu caminho natural pelo sistema.

**Ex.: **
```bash
$ cp ~/Downloads/submit-subs/*:login:* ~/cd-moj/submissions

```

___

## Simular Correção

Para simular resposta do corretor em contests siga os passos abaixo, isso pode ser necessario devido a falto de acesso aos servidores de correção quando se esta desenvolvendo.

```bash
$ cp <path para pasta com os arquivos de correção>/*:corrigido:* <path para pasta submissions do CD-MOJ>

``` 
Ao copiar os arquivos de corerção para a pasta **cd-moj/submissions** o daemon **julgador.sh** fará com que ele percorra seu caminho natural pelo sistema.

**Ex.: **
```bash
$ cp ~/Downloads/corr-subs/*:login:* ~/cd-moj/submissions

``` 