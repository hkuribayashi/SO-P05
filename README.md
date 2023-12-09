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

4. Caso o comando anterior tenha falhado, verifique se a instalação do Docker Engine ocorreu com sucesso:

```
    $ sudo service docker start
```

## Reconhecendo o Terreno

Inicialmente vamos reconhecer o terrreno e entender nossos primeiros comandos. Começaremos com o comando 
docker run e entender seu funcionamento.

```
    $ sudo docker run hello-world
```
No comando acima, a instrução run serve para indicar que desejamos rodar uma imagem docker, neste caso a 
imagem **hello-world**, que é uma imagem que serve apenas para testar a instalação do Docker, como um Hello World.
Assim, este comando possui a seguinte estrutura:

```
    $ sudo docker run <imagem_docker>
```

Onde **<imagem_docker>** representa uma imagem docker que frequentemente não está disponível em seu Sistema Operacional,
e assim, o Docker Daemon realiza o download da imagem a partir de algum repositório Docker.

Após o comando anterior, execute o comando a seguir:

```
    $ sudo docker container ps
```

ou execute o comando equivalente abaixo:

```
    $ sudo docker container ps -a
```

O que aconteceu no comando anterior? Quantos containers foram listados? Quantas imagens foram listadas?

A partir do comando acima fica claro uma mesma imagem pode ser utilizada para rodar vários containers.

Cada container terá um nome único e aleatório e será criado a partir de uma imagem. 
 
Agora informe o seguinte comando para listas as imagens disponíveis no sitema:

```
    $ sudo docker image ls 
```

Após, vamos executar o seguinte comando abaixo:

```
    $ sudo docker container run ubuntu 
```

O que o comando acima produziu? O que acontece se ele for executado novamente?

Agora modifique o comando anterior para o seguinte formato:

```
    $ sudo docker container run -it ubuntu
```

Embora tenhamos executado uma imagem **ubuntu** em um container, esta imagem não 
é uma Máquina Virtual. A imagem possui apenas o Shell do Sistema Operacional, e não
possui Kernel. A imagem "acha" que possui o Kernel, mas este Kernel é o da Máquina Física.

Agora vamos fazer um novo teste com a imagem nginx que é uma aplicação de servidor web.

Execute o seguinte comando:

```
    $ sudo docker container run nginx
```

O que aconteceu? A imagem **nginx** foi utilizada para iniciar um novo container. É possível 
abrir uma nova aba no Terminal e executar o comando de listagem de containers. Neste caso é 
possível ver que há pelo menos uma imagem sendo utilizada por um container.

```
    $ sudo docker container ps -a
```

A imagem que está rodando em um container pode usar uma porta de comunicação para o estabelecimento
de conexões TCP/IP. Neste caso, o container que está em execução, está com a porta 80/TCP em uso, e
assim pode ser acessada por outros computadores:

![Imagem1](/imagens/imagem1.png)

Conforme pode ser observado na imagem acima, o container usa uma porta, mas esta porta de comunicação
é diferente da porta de comunicação usada pelo Sistema Operacional físico. É possível criar um mapeamento
entre a porta utilizada pelo SO e a porta utilizada pelo container da seguinte forma:

```
    $ sudo docker container run -p <porta_do_so>:<porta_do_container> nginx
```

onde, **<porta_do_so> deve ser substituído pela numeração de porta utilizada no SO, e o termo <porta_do_container>
deve ser substituído pela porta do container, conforme o exemplo abaixo:

```
    $ sudo docker container run -p 8080:80 nginx
```

No exemplo a seguir, a porta 80/TCP do container foi mapeada para a porta 8080/TCP do Sistema Operacional,
sendo, portanto, agora acessível por um navegador (Firefox, Chrome, etc.). Basta acessar o endereço abaixo:
```
    http://localhost:8080/
```
