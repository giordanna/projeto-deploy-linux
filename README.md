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
- TODO

### iv. Lista de recursos de terceiros utilizados para completar o projeto
- [mod_wsgi (Apache)](http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/)
- [Target WSGI script cannot be loaded as Python module](https://stackoverflow.com/questions/6454564/target-wsgi-script-cannot-be-loaded-as-python-module)
- [How to correct TypeError: Unicode-objects must be encoded before hashing?](https://stackoverflow.com/questions/7585307/how-to-correct-typeerror-unicode-objects-must-be-encoded-before-hashing)
- [permission denied AWS EC2 file.save from Flask App](https://stackoverflow.com/questions/34320280/permission-denied-aws-ec2-file-save-from-flask-app)
- [TypeError: the JSON object must be str, not 'bytes'](https://stackoverflow.com/questions/42683478/typeerror-the-json-object-must-be-str-not-bytes)
