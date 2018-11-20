# Projeto de deploy de Servidor Linux
Sexto projeto do curso nanodegree da Udacity de Desenvolvedor Full-stack. O projeto consiste em configurar um servidor remoto hospedado através do serviço da Amazon Lightsail. Nele, deve servir uma aplicação feita em Flask.

## Items obrigatórios

### i. Endereço de IP e porta SSH
- Endereço IP: 54.145.86.10
- Porta SSH utilizada: 2200

O login é feito através do comando: `ssh grader@54.145.86.10 -p 2200 -i ~/.ssh/grader`, sendo `~/.ssh/grader` a localização da chave privada.

### ii. URL da aplicação web
- http://54.145.86.10.xip.io/

Por conta da API do google de autenticação não permitir o uso de IPs públicos, foi necessário utilizar o serviço de xip.io.

### iii. Resumo do software instalado e mudanças feitas em configuração
Configuração do servidor:
- Amazon Lightsail
- Plataforma: Linux/UNIX
- SO: Ubuntu 16.04 LTS
- Plano de 512 MB RAM, 1 vCPU, 20 GB SSD

Configuração do Ubuntu:
- Atualização de pacotes feitas em 19/11/2018;
- Criação de um usuário chamado grader;
- Poderes de sudo foram cedidos ao grader copiando o arquivo `/etc/sudoers.d/ubuntu` e renomeando para grader dentro de seu conteúdo;
- Gerado o novo par de chaves localmente, copiando a chave pública e inserindo em `.ssh/authorized_keys` dentro de `/home/grader/`, com as devidas permissões (700 para `.ssh` e 600 para `.ssh/authorized_keys`);
- Desativa login via root editando `/etc/ssh/sshd_config` em:
```
PasswordAuthentication no
```

Configuração de rede:
- HTTP: 80 - TCP
- (Custom) NTP: 123 - UDP
- (Custom) SSH: 2200 - TCP

Configuração de `/etc/apache2/sites-enabled/000-default.conf` (sem os comentários):
```sh
<VirtualHost *:80>
        ServerAdmin gior.grs@gmail.com
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        WSGIDaemonProcess projeto-catalogo user=grader group=grader threads=5
        WSGIScriptAlias / /var/www/projeto-catalogo/webtool.wsgi

        <Directory /var/www/projeto-catalogo>
                WSGIProcessGroup projeto-catalogo
                WSGIApplicationGroup %{GLOBAL}
                Order deny,allow
                Allow from all
        </Directory>

        <Directorymatch "^/.*/\.git/">
                Order deny,allow
                Deny from all
        </Directorymatch>
</VirtualHost>
```

### iv. Lista de recursos de terceiros utilizados para completar o projeto
- [Slack do curso da Udacity](https://br-udacity-fullstack.slack.com/messages/C8E7UHPM5/)
- [mod_wsgi (Apache)](http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/)
- [How do I prevent apache from serving the .git directory?](https://serverfault.com/questions/128069/how-do-i-prevent-apache-from-serving-the-git-directory)
- [Target WSGI script cannot be loaded as Python module](https://stackoverflow.com/questions/6454564/target-wsgi-script-cannot-be-loaded-as-python-module)
- [How to correct TypeError: Unicode-objects must be encoded before hashing?](https://stackoverflow.com/questions/7585307/how-to-correct-typeerror-unicode-objects-must-be-encoded-before-hashing)
- [permission denied AWS EC2 file.save from Flask App](https://stackoverflow.com/questions/34320280/permission-denied-aws-ec2-file-save-from-flask-app)
- [TypeError: the JSON object must be str, not 'bytes'](https://stackoverflow.com/questions/42683478/typeerror-the-json-object-must-be-str-not-bytes)
