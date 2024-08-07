# Bootcamp Imersão AWS

***Detalhes do evento:*** Período: 05 a 11 de Agosto/2024 (Online e ao Vivo às 20h) [>> Página de Inscrição do evento](https://org.imersaoaws.com.br/github/readme)

#### Para rodar as migrations no container ####
```
docker compose exec server bash -c 'npx sequelize db:migrate'
```

----



## Projeto prático da aula 1 do Bootcamp:

Entreguei o projeto prático da aula 1 do Bootcamp Imersão AWS do Henrylle Maia. 

Nesse primeiro desafio aprendi como levantar um ambiente de trabalho na nuvem para trabalhar com Docker. Utilizamos conexão segura com SSM para acessar o ambiente via CloudShell e utilizamos algumas automações em shell para as configurações e criações de Roles no IAM.

Além disso, foi apresentado a arquitetura em Alta Disponibilidade na AWS do projeto que iremos construir durante todo o Bootcamp

Abaixo alguns vídeos com as etapas que cumpri desse primeiro desafio:

### 1º passo:
Criação do Security Group na VPc default

<img src="img/Criação do Security Group na VPC default.gif">

------
### 2º passo:

Clonando o projeto usando Cloudshell, rodando automações em scripts shell para criar a Role no IAM e validar os recursos do nosso ambiente

<img src="img/Criação Role IAM com acesso SSM e validação dos recursos via scripts.gif">

------
### 3º passo:

 Lançando maquina de trabalho: uma instância EC2 com imagem Linux configurada pra conexão ssm, instalando dependências via automação

<img src="img/Lançando maquina de trabalho instancia EC2 usando conexão ssm .gif">

------
### 4º passo:

Conectando a instância e clonando o projeto nela, gerando a imagem docker com o Dockerfile e subindo os containers com o docker compose

<img src="img/Conectando a instancia e subindo os containers.gif">

------
### 5º passo: 

Adicionando mais polices a role do IAM pra comunicação com outros serviços, testando as permissões e vendo a aplicação no ar rodando.

<img src="img/Adicionando polices a role ssm testando e vendo aplicação rodar.gif">

