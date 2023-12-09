# Demonstração de Funcionamento do Docker

Este projeto é uma demonstração reproduzível do conceito de virtualização de containers,
para que você mesmo possa fazer o trabalho de criação de containers com Dockerfile ou por
meio do docker-compose.

Este projeto é para alunos da disciplina SI01033 (Sistemas Operacionais) do Curso de Sistemas 
de Informação da Unifesspa, que querem testar ferramentas de virtualização de containers.


## O que é o Docker?

É uma plataforma aberta para desenvolvimento, transporte e execução de aplicações utilizando 
conceitos de virtualização de containers.

## Instalação do Docker 

Para fazer a instalação do Docker é necessária a instalação do Docker Daemon, e sua instalação
varia de acordo com o Sistema Operacional. A seguir apresentamos um roteiro de instalação para
o SO Debian Linux. Para outros Sistemas Operacionais consultar: https://docs.docker.com/get-docker/ 

A abordagem recomendada de instalação do Docker Desktop em sistemas Linux Debian:

1. Instalar o repositório do Docker no sistemas APT do Debian

Podemos recuperar o cabeçalho deste arquivo fazendo:
```
    # Adicionar a chave do Repositório

    $ sudo apt update
    $ sudo apt install ca-certificates curl gnupg
    $ sudo install -m 0755 -d /etc/apt/keyrings
    $ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    $ sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Adicionar o repositório ao APT:
   
    $ echo \
  	"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  	$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  	sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    $ sudo apt update
```
2. Para instalar a última versão do Docker use o seguinte comando:
```
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3. Para verificar se a instalação ocorreu com sucesso rode o seguinte comando a seguir:
```
    $ sudo docker run hello-world
```

