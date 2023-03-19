# Projeto GO

Este repositório contem em sua raiz o link para outros repositórios assim como o docker-compose com todos os seus containers orquestrados.

**TL;DR:** Este projeto se trata de um gerenciador de eventos para usuários que buscam uma decisão rápida para onde ir, nele você podera 
identificar rapidamente algo que de match com seu gosto e poder verificar os principais detalhes do lugar, adicionando a sua lista de eventos 
curtidos, traçando rota, compartilhando o evento entre outras funcionalidades...

![MOCKUP-GO!](https://user-images.githubusercontent.com/48265863/192113098-bb60b60e-a6e7-4348-a6e7-900a27b0eec9.jpg)

## Stacks/Serviços empregadas no projeto (como um todo)

Backend
* Java - 11
* Maven - 3.8.1
* Spring Boot - 2.6.1
* Spring Cloud - Open Feign 
* Swagger
* RabbitMQ - 3.10.7 (CloudAMQP)
* Apache Archetype
* MongoDB (Atlas) - 6.0
* MySQL - 5.7
* Keycloak - 19.01
* Flutter - 2.0
* Dart - 2.18
* One Signal
* Docker - 20.20.12
* Docker Compose - 2.2.3
* Heroku (Inicialmente)
* AWS - S3 Bucket e IAM
* Cloudflare 
* Kubernetes
* Nginx 
* Figma
* Wordpress
* Miro
* Firebase
* Facebook Console
* Google Console
* XCode
* Jira

## [Arquitetura](https://app.diagrams.net/#G1C4F9m1qkxhmU36VOlm15OinctUIdHRtG)
<p align="center">
  <img src="https://user-images.githubusercontent.com/48265863/226160076-20c715da-8ec0-430a-800a-777843b35cd1.png">
</p>

A arquitetura do MVP (1.0.0 - Beta) desse projeto possui em seu backend quatro microsserviços, dois bancos de 
dados Mysql em uma mesma instância Amazon RDS e um banco NoSQL no MongoDB Atlas. Além de
ser alocado em um clsuter kubernetes na DigitalOcean com um LoadBalance com NGinx, tem uma exchange no RabbitMQ via CloudAMQP, e ainda faz o 
uso do Keycloak para autenticação e gerenciamento de usuários administradores. em acesso externo temos a api google maps para enriquecer o 
nosso evento durante o processo de criação. 

No frontend temos 
uma aplicativo desenvolvido com o SDK Flutter(Dart).

Vale ressltar que tambem foi criado uma operação apartarda do Cluster principal, onde temos um job em Spring que ao rodar, captura e salva de 
uma vez só varios eventos listados em uma planilha, processo esse que pode ser acionado manualmente com uma planilha local ou a cada X horas 
através de um scheduller que busca no S3 Bucket.

Observações:
1 - Todo acesso via app é filtrado por um WAF - Web Application Firewal nesse caso [Cloudflare](https://www.cloudflare.com/pt-br/).

* **Cloudflare** --> a descrição vem aqui...
* **Kubernetes** --> a descrição vem aqui...
* **api-control(BFF)** --> a descrição vem aqui...
* **Keycloak** --> a descrição vem aqui...
* **api-business** --> a descrição vem aqui...
* **api-listener** --> a descrição vem aqui...
* **api-notification** --> a descrição vem aqui...
* **Exchange RabbitMQ** --> a descrição vem aqui...
* **MySQL (Babilonia)** --> a descrição vem aqui...
* **MySQL (Constantinopla)** --> a descrição vem aqui...
* **MongoDB (Pompeia)** --> a descrição vem aqui...
* **job-event-increment (event.list)** --> a descrição vem aqui...
* **Amazon S3 - Bucket** --> a descrição vem aqui...
* **Google Map API** --> a descrição vem aqui...
* **GO: Em qualquer Lugar** --> a descrição vem aqui...

## Banco de dados

  TODO - explicar os bancos e os motivos da escolha aqui...
  
## Microsserviços
  
  TODO - explicar cada microsserviço suas principais responsabilidades e documentação de endpoints com openAPI

## Keycloak
  
  TODO - explicar no que usamos keycloak (autenticação e criação de usuários/roles)
 
## Amazon S3 - Bucket
  
  TODO - explicar o uso do s3-bucket
  
## Cloudflare , API-GATEWAY
  
  TODO - explicar sobre a escolha da cloudflare e suas ações, tambem explicar oque faz a api-gateway.
  
## Observabilidade
  
  TODO - IPC, precisa aplica observabilidade nas APIS

## Figma
  
  TODO - explicar como utilizamos o Figma para projetar as telas a serem desenvolvidas
  
## Flutter| Aplicação Mobile
  
  TODO - explicar como foi usado o flutter pra criação de aplicação

## **Heroku** e Consoles utilizados
 
  TODO - explicar tudo sob a heroku, facebeok console, firebase etc...
  
## Jira Software | Documentação
  
  TODO - explicar como usamos o Jira e documentamos os passos através do SCRUM
  
## How To Local
  
  TODO - como rodar todo o projeto localmente com docker-compose e flutter 
  
## Agradecimentos e Contato
  
  TODO - agradecimentos e contatos de todos os envolvidos no projeto. 
