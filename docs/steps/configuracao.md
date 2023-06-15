## Configurando apache cgi-bin

Primeiramente acesse o arquivo de configuração do apache:

```bash
$ sudo nano /etc/apache2/apache2.conf
```

Adicione as seguintes linhas no final do arquivo:

```apache
  <Directory /home/$USER/cdmoj/moj-pagina/>
      Options +ExecCGI
      AddHandler cgi-script .cgi .sh
  </Directory>
```

Execute o seguinte comando para permitir que o apache execute cgi:

```bash
$ sudo ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/cgi.load
```

Acesse o arquivo do servidor cgi-bin:

```bash
$ sudo nano /etc/apache2/conf-available/serve-cgi-bin.conf
```

Dentro desse arquivo há um trecho parecido com esse:

```apache
<IfModule mod_alias.c>
        <IfModule mod_cgi.c>
                Define ENABLE_USR_LIB_CGI_BIN
        </IfModule>

        <IfModule mod_cgid.c>
                Define ENABLE_USR_LIB_CGI_BIN
        </IfModule>

        <IfDefine ENABLE_USR_LIB_CGI_BIN>
                ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
                <Directory "/usr/lib/cgi-bin/">
                        AllowOverride None
                        Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
                        Require all granted
                </Directory>
        </IfDefine>
    </IfModule>
```

Modifique as seguintes linhas e salve o arquivo:

```apache
ScriptAlias /cgi-bin/  /home/$USER/cdmoj/moj-pagina/cgi-bin/
<Directory "/home/$USER/cdmoj/moj-pagina/cgi-bin/">
```

Crie um arquivo para o site cd-moj:

```bash
$ sudo nano /etc/apache2/sites-available/moj.conf
```

Esse arquivo deve se parecer com o seguinte:

```apache
<VirtualHost *:80>
        ServerName moj.com.br

        ServerAdmin webmaster@localhost
        DocumentRoot /home/$USER/cdmoj/moj-pagina/

        ErrorLog ${APACHE_LOG_DIR}/moj.com.br-error.log
        CustomLog ${APACHE_LOG_DIR}/moj.com.br-access.log combined

        Include conf-available/serve-cgi-bin.conf

        ScriptAlias /cgi-bin/ /home/$USER/cdmoj/moj-pagina/cgi-bin/
<Directory "/">
        Options Indexes FollowSymLinks MultiViews Includes
        Require all granted
</Directory>
</VirtualHost>
```

Desative o site padrão:

```bash
$ sudo a2dissite 000-default
```

Habilite o site do cd-moj:

```bash
$ sudo a2ensite moj
```

Reinicie o serviço apache:

```bash
$ sudo systemctl reload apache2
```

---

## Configurando do CD-MOJ

Edite o arquivo common.conf que está dentro do diretório moj-serverside:

```bash
$ sudo nano $HOME/cdmoj/moj-serverside/etc/common.conf
```

Esse arquivo deve se parecer com o seguinte:

```bash
CACHEDIR=$HOME/tmp
CONTESTSDIR=$HOME/cdmoj/contests
SUBMISSIONDIR=$HOME/cdmoj/submissions
BASEURL="http://localhost"
HTMLDIR=$HOME/cdmoj/moj-pagina
```

---

### Criando um administrador

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

---

## Erros Comuns

### Permissões

Abaixo seguem algumas permissões necessárias para que seja possível rodar o CD-MOJ com sucesso localmente.

```bash
cd cdmoj
chwon -R www-data:www-data ./contests
chwon -R user.user ./contest/
sudo chmod 777 submissions/
```
