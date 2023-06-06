# Guia para subir contest 

## Daemons
O primeiro passo é importante já subir ambos daemons, executar-corretor.sh e executar-julgador.sh, e se certificar de que ambos estão conversando entre si corretamente. Os comandos para subir ambos daemons são: `bash executar-julgador.sh` e `bash executar-corretor.sh`

## Exercícios 
É possível que você não tenha acesso nas máquinas do Ribas que corrigem os exercícios, logo é interessante que se utilize exercícios listados no Spoj e é necessário que você tenha uma conta criada no mesmo e cadastrada no arquivo judge.conf.

## Contest
O arquivo contest-description.txt deve estar corretamente preenchido e precisa obrigatoriamente estar compactado no formato .tar. 

## Passo a passo para subir o contest
1. É necessário entrar no link [localhost admin](http://localhost/cgi-bin/admin.sh) e realizar o login;
2. Clicar na aba Old School; 
3. Adicionar o arquivo contest-description.tar na opção "Envie novo contest" e clicar em submit;
4. Conferir se o contest foi criado com sucesso observando o Log disponibilizado logo abaixo da aba Old School;

## Passo a passo para entrar no contest
1. É necessário entrar no link [localhost contest](http://localhost/cgi-bin/index.sh);
2. Realizar o login com a conta e nível desejado;

## Possíveis erros
Veja se os steps foram seguidos corretamente (Daemons, Exercícios e Contest). Para mais informações entrar no root do seu pc utilizando o comando `sudo -i` e dentro do root usar o comando `tail -f /var/log/apache2/*.log`
