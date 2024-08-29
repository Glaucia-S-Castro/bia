# Bootcamp Imersão AWS 

***Detalhes do evento:*** Período: 05 a 11 de Agosto/2024 (Online e ao Vivo às 20h) [>> Página de Inscrição do evento](https://org.imersaoaws.com.br/github/readme)

Participei do evento e entreguei os desafios mostrados e detalhados aqui.

###
----
# Pré-requisitos

- Ter uma conta cadastrada na AWS com permissão para provisionar e configurar os serviços;
- Conhecimentos básicos dos serviços AWS a serem utilizados no projeto;
- Conhecimentos em servidores Linux em nuvem;
- Conhecimentos em scrips de automação de tarefas em shell;
- Conhecimentos em Docker e Docker Compose;
------

# Instalação

```bash
# Clone o repositório:
git clone git@github.com:Glaucia-S-Castro/bia.git

# Entre no diretório:  
cd /bia

# Para subir os containers da aplicação e do banco de dados:
docker compose up -d

# Para rodar as migrations do BD no container 
docker compose exec server bash -c 'npx sequelize db:migrate'
```

### ATENÇÃO:

Os projetos práticos detalhados a seguir podem gerar custos pelo uso de alguns dos serviços AWS!

É necessário entender sobre AWS, pois, nem todos os serviços usados nestes projetos estão na camada free tier (nível gratuito) e muitos fatores podem interferir no custo total por exemplo: o tempo de cadastro da sua conta, os limites de uso dos serviços já feitos, o tempo que a aplicação vai ficar no ar e os serviços vão ficar ligados, entre outros. No meu caso o projeto teve um custo de menos de U$$ 2,00 (dois dólares) com a aplicação ficando no ar por 6 dias ( cerca de 144 horas) tendo minha conta tem menos de 12 meses.

------


# 1º Projeto prático: Levantando um ambiente na nuvem pra trabalhar com Docker

Nesse primeiro desafio tivemos como tarefa levantar um ambiente de trabalho na nuvem para trabalhar com Docker. 

Utilizamos conexão segura com SSM para acessar o ambiente via CloudShell e utilizamos algumas automações em shell para as configurações e criações de Roles no IAM. Além disso, foi apresentado a arquitetura em Alta Disponibilidade na AWS do projeto que iremos construir durante todo o Bootcamp

Abaixo alguns vídeos com as etapas que cumpri desse primeiro desafio:

--------
### Passo 1:

- Criação do Security Group na VPc default

<img src="img/Projeto1/Criação do Security Group na VPC default.gif"><br>

------
### Passo 2:

- Clonando o projeto usando Cloudshell, rodando automações em scripts shell para criar a Role no IAM e validar os recursos do nosso ambiente

<img src="img/Projeto1/Criação Role IAM com acesso SSM e validação dos recursos via scripts.gif"><br>

------
### Passo 3:

- Lançando maquina de trabalho: uma instância EC2 com imagem Linux configurada pra conexão ssm, instalando dependências via automação

<img src="img/Projeto1/Lançando maquina de trabalho instancia EC2 usando conexão ssm .gif"><br>

------
### Passo 4:

- Conectando a instância e clonando o projeto nela, gerando a imagem docker com o Dockerfile e subindo os containers com o docker compose

<img src="img/Projeto1/Conectando a instancia e subindo os containers.gif">

------
### Passo 5: 

- Adicionando mais polices a role do IAM pra comunicação com outros serviços, testando as permissões e vendo a aplicação no ar rodando.

<img src="img/Projeto1/Adicionando polices a role ssm testando e vendo aplicação rodar.gif">

-------
# 2º Projeto prático: Migrando a app Bia para o ECS 

Nesse segundo desafio tivemos como tarefa a criar um cluster no ECS, o principal serviço de gerenciamento de container da AWS.

Alocamos também um banco no RDS, rodamos as migrates para criar a estrutura relacional, configuramos os security groups e começamos o desmembramento da nossa aplicação dentro da nuvem.    

Aprendi também a fazer o envio da nossa imagem Docker para o ECR e fazer deploy via script para o ECS.

---------
### Passo 1:

Preparação pra criação do Cluster no ECS : 

- Nesta etapa foi necessário corrigir o ip no Dockerfile

<img src="img/Projeto2/1-corrigindo ip dockerfile pra persistencia.gif"><br>

- Testando e corrigindo a persistencia de dados no banco, (aqui ele ainda esta local só migramos pro RDS no passo 2)

<img src="img/Projeto2/2-corrigindo ip dockerfile pra persistencia.gif"><br>

- Criar os segurity groups (3 no total), e configura-los pra que se comunicassem no cluster internamente e habilitassem a comunicação externa apenas para a aplicação.

*obs.: No vídeo existe um erro que foi corrigido logo depois, mas acabei não gravando a correção. Na parte de criação das rules do grupo postgres-db cometi um erro inserindo como outbound rules o que devia ser incluso nas inbound rules, ficando as outbound apenas com o que ja vem default.*

<img src="img/Projeto2/3-criando security groups pra comunicação do cluster.gif"><br>

-------
### Passo 2:

Criação do Banco no RDS e do cluster no ECS, configurando tasks definitions e service: 

- Criando um banco PostregSQL no RDS e subindo a nossa imagem no ECR via automação em script

<img src="img/Projeto2/4-criando RDS do DB e subindo nossa imagem pro ECR via automacao.gif"><br>

- Criando o cluster no ECS e configurando as task definitions

<img src="img/Projeto2/5-criando o cluster no ECS e Task definitions.gif"><br>

- Criação do service e ajuste do dockerfile pra agora apontar pro DB no RDS 

<img src="img/Projeto2/6-criando o service e ajustando app pra apontar pro RDS.gif"><br>

-------
### Passo 3:

Simulando necessidade de alteração mudando a cor de um botão da página e executando o deploy:

- Alterando cor do botão no código e rodando deploy

<img src="img/Projeto2/7- mudando cor e botão e rodando o deploy.gif"><br>

-------
### Passo 4:

Preparação das questões de domínio e certificado https e configuração do CNAME que serão utilizados no próximo projeto:

- Inserindo dominio no Route 53 e requisitando certificado no ACM (Certificate Manager)

<img src="img/Projeto2/8- Inserindo Dominio no Route 53 e requisitando certificado no Certificate Manager-ACM.gif"><br>


- Finalizando CNAME cadastrando no Route53 recebendo certificado ACM

<img src="img/Projeto2/9-Finalizando CNAME cadastrando no Route53 recebendo certificado ACM.gif"><br>

-------

# 3º Projeto prático: Configurando deploy sem downtime, trabalhando com Load Balancer e inserindo a app em um dominio https personalizado

Nesse terceiro desafio aprendi a rodar uma aplicação (app bia) em Node com React em Alta disponibilidade e a realizar deploy sem downtime na AWS usando o ECS.

Trabalhei também com Application Load Balancer e Target Group.

Para fechar com chave de ouro, colocamos nossa aplicação para rodar com domínio personalizado e https configurado.

--------
### Passo 1:

- Ajustando os Security Groups: 

<img src="img/Projeto3/1- Ajustando Security Groups.gif"><br>

--------
### Passo 2:

- Criando o ELB (Elastic Load Balancer) com Target Group 

<img src="img/Projeto3/2- criação do ALB com Target Group.gif"><br>

--------
### Passo 3:

- Excluindo o cluster antigo e criando novo cluster apontando pro ALB

<img src="img/Projeto3/3- Exclusão do cluster antigo e criação do novo cluster ALB part1 .gif"><br>

- Reconfigurando as tasks definitions

<img src="img/Projeto3/4- criação do novo cluster ALB - terminando as tasks part2 .gif"><br>

--------
### Passo 4:

- Testando Deploy sem downtime 

<img src="img/Projeto3/5- testando deploy sem down time.gif"><br>

--------
### Passo 5:

- Configurando dominio com HTTPS e deploy com ajustes no Dockerfile

<img src="img/Projeto3/6- Configurando dominio com HTTPS e deploy com ajustes no Dockerfile.gif"><br>

-------

# 4º Projeto prático: Configurando deploy sem downtime, trabalhando com Load Balancer e inserindo a app em um dominio https personalizado

...



## Autor

Glaucia Castro - glauciacastro.dev@gmail.com