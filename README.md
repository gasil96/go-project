# Projeto GO

Este repositório contem em sua raiz o link para outros repositórios assim como o docker-compose com todos os seus containers orquestrados.

**TL;DR:** Este projeto se trata de um gerenciador de eventos para usuários que buscam uma decisão rápida para onde ir, nele você podera identificar rapidamente algo que de match com seu gosto e poder verificar os principais detalhes do lugar.

![MOCKUP-GO!](https://user-images.githubusercontent.com/48265863/192113098-bb60b60e-a6e7-4348-a6e7-900a27b0eec9.jpg)

## Stacks empregadas no projeto
* Java - 11
* Maven - 3.8.1
* Spring Boot - 2.6.1
* RabbitMQ - 3.10.7
* MongoDB - 6.0
* MySQL - 5.7
* Keycloak - 19.01
* Flutter - 2.0
* Dart - 2.18
* Docker - 20.20.12
* Docker Compose - 2.2.3
* Heroku
* AWS - S3 Bucket e IAM
* Cloudflare
* Figma
* Firebase
* Facebook Console
* Google Console
* XCode
* Jira Software

## [Arquitetura](https://app.diagrams.net/#G1C4F9m1qkxhmU36VOlm15OinctUIdHRtG)
<p align="center">
  <img src="https://user-images.githubusercontent.com/48265863/188970560-d7e0d148-a3ab-4069-b491-146c2ab327da.png">
</p>

A arquitetura do MVP desse projeto possui em seu backend quatro microsserviços, dois bancos de dados sendo eles Mysql e MongoDB, uma api-gateway, uma exchange no RabbitMQ, e ainda faz o uso do Keycloak para autenticação e gerenciamento de usuários administradores. No frontend temos uma aplicativo desenvolvido com o SDK flutter(dart) e uma aplicação de backoffice desenvolvida em <angular ou vuejs>.

  Observações:
  1º Todo acesso via app irá ser filtrado por um WAF - Web Application Firewal nesse caso [Cloudflare](https://www.cloudflare.com/pt-br/).

* **Cloudflare** --> a descrição vem aqui...
* **api-gateway** --> a descrição vem aqui...
* **api-control(BFF)** --> a descrição vem aqui...
* **Keycloak** --> a descrição vem aqui...
* **api-business** --> a descrição vem aqui...
* **api-listener** --> a descrição vem aqui...
* **api-notification** --> a descrição vem aqui...
* **Exchange RabbitMQ** --> a descrição vem aqui...
* **MySQL** --> a descrição vem aqui...
* **MongoDB** --> a descrição vem aqui...
* **Dashboard Admin** --> a descrição vem aqui...
* **Amazon S3 - Bucket** --> a descrição vem aqui...
* **GO App** --> a descrição vem aqui...

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
