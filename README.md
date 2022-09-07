# Projeto GO

Este repositório contem em sua raiz o link para outros repositórios assim como o docker-compose com todos os seus containers orquestrados.

**TL;DR:** Este projeto se trata de um gerenciador de eventos para usuários que buscam uma decisão rápida para onde ir, nele você podera identificar rapidamente algo que de match com seu gosto e poder verificar os principais detalhes do lugar.

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
  <img src="https://user-images.githubusercontent.com/48265863/188963337-19fc3528-b831-4b27-aab8-a3ff5984b118.png">
</p>

A arquitetura do MVP desse projeto possui em seu backend quatro microsserviços, dois bancos de dados sendo eles Mysql e MongoDB, uma api-gateway, uma exchange no RabbitMQ, e ainda faz o uso do Keycloak para autenticação e gerenciamento de usuários administradores. No frontend temos uma aplicativo desenvolvido com o SDK flutter(dart) e uma aplicação de backoffice desenvolvida em <angular ou vuejs>.

  Observações:
  1º Todo acesso via app irá ser filtrado por um WAF - Web Application Firewal nesse caso [Cloudflare](https://www.cloudflare.com/pt-br/).

* **Cloudflare** --> sua descrição
* **api-gateway** --> sua descrição
* **api-control(BFF)** --> sua descrição
* **Keycloak** --> sua descrição
* **api-business** --> sua descrição
* **api-listener** --> sua descrição
* **api-notification** --> sua descrição
* **Exchange RabbitMQ** --> sua descrição
* **MySQL** --> sua descrição
* **MongoDB** --> sua descrição
* **Dashboard Admin** --> sua descrição
* **GO App** --> sua descrição

  
