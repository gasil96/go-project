# GO: Em qualquer lugar - [Acesse aqui.](http://goanywhere.app.br/)

Este repositório contem em sua raiz o link para outros repositórios assim como o docker-compose com todos os seus containers orquestrados.

**TL;DR:** Este projeto se trata de um gerenciador de eventos para usuários que buscam uma decisão rápida para onde ir, nele você podera
identificar rapidamente algo que de match com seu gosto e poder verificar os principais detalhes do lugar, adicionando a sua lista de eventos
curtidos, traçando rota, compartilhando o evento entre outras funcionalidades...

![MOCKUP-GO!](https://user-images.githubusercontent.com/48265863/226208324-e6bed131-b520-429c-895c-cd44a1ddfccf.png)

## Stacks e Serviços empregadas no projeto.

| Back-end | Front-end | Banco de Dados | DevOps/Cloud | Ferramentas |
|----------|-----------|----------------|--------------|-------------|
| Java 11 | Flutter 2.0 | MongoDB (Atlas) 6.0 | Docker 20.20.12 | Github Actions |
| Maven 3.8.1 | Dart 2.18 | MySQL 5.7 | Docker Compose 2.2.3 | Cloudflare |
| Spring Boot 2.6.1 | Figma | | Heroku | Kubernetes |
| Spring Cloud - Open Feign | | | AWS S3 Bucket e IAM | Nginx |
| Swagger | | | | Firebase |
| RabbitMQ 3.10.7 (CloudAMQP) | | | | Facebook Console |
| Keycloak 19.01 | | | | Google Console |
| | | | | XCode |
| | | | | Jira |
| | | | | Slack |
| | | | | Draw.io |

## [Arquitetura](https://app.diagrams.net/#G1C4F9m1qkxhmU36VOlm15OinctUIdHRtG)

<p align="center">
  <img src="https://user-images.githubusercontent.com/48265863/226204658-4d7e3af0-8abc-49ee-af5f-a29db5b35bf9.png">
</p>

A arquitetura da versão MVP (1.0.0 - Beta) deste projeto inclui quatro microsserviços em seu backend, dois bancos de dados MySQL em uma única
instância Amazon RDS e um banco NoSQL no MongoDB Atlas. Além disso, está alocada em um cluster Kubernetes na DigitalOcean, com um balanceador de
carga com NGINX e utiliza uma exchange no RabbitMQ via CloudAMQP. Para autenticação e gerenciamento de usuários administradores, o Keycloak é
utilizado. Para enriquecer o evento durante o processo de criação, há o acesso externo da API do Google Maps.

No frontend, o aplicativo foi desenvolvido com o SDK Flutter (Dart).

Também foi criada uma operação separada do cluster principal, onde há um job em Spring que captura e salva vários eventos listados em uma
planilha de uma só vez. Esse processo pode ser acionado manualmente com uma planilha local ou a cada X horas através de um scheduler que busca no
S3 Bucket.

### Descrição sobre suas funcionalidades

* **Cloudflare** - Usado como WAF, ou seja uma camada a mais de segurança na aplicação

* **Kubernetes** - Usado no projeto porque é uma plataforma confiável e eficiente para gerenciar e orquestrar contêineres em ambientes de nuvem.
  Ele oferece recursos como escalabilidade horizontal, alta disponibilidade, implantação e atualização de aplicativos simplificadas, e
  gerenciamento simplificado de infraestrutura. Essas vantagens tornam o Kubernetes uma escolha ideal para a criação de um ambiente altamente
  dinâmico e escalável para nossos aplicativos.
    - [Documentação oficial do Kubernetes](https://kubernetes.io/docs/home/)


* **Observabilidade (Grafana & Prometheus)** - Foi utilizado em cada microsserviço um apanhado de Actuator + Prometheus + Grafana para gerar
  insumos de dados a respeito dos usos de cada microsserviço.
    - [Documentação oficial do Grafana](https://grafana.com/docs/)
    - [Documentação oficial do Prometheus](https://prometheus.io/docs/introduction/overview/)


* **Nginx** - O Nginx foi usado como balanceador de carga round-robin no cluster Kubernetes. Ele é um servidor HTTP e proxy reverso que distribui
  as requisições para diferentes instâncias de um mesmo serviço de forma equilibrada. A vantagem de usar o Nginx como balanceador de carga é que
  ele ajuda a otimizar o tráfego da rede, garantindo uma melhor distribuição das requisições e evitando sobrecarga em uma única instância, o que
  resulta em maior disponibilidade e confiabilidade do serviço.
    - [Documentação oficial do Nginx](https://nginx.org/en/docs/)


* **api-control(BFF)** - API que funciona como BFF, centralizando os recursos de todos os outros serviços para ser acessivel facilmente através
  de uma única fonte. Também é responsável pelo gerenciamento de acesso a recursos, dividindo os perfis através de suas Roles de acesso.

* **api-business** - API que fica responsável por execução de scheduled e services com funcionalidades que atendem as regras de negócio como:
  Apagar usuários desabilitados, desabilitar automaticamente eventos que já encerraram, etc...


* **api-listener** - API CORE do projeto, centralizar por enquanto as principais funcionalidades, como gerenciamento de usuários com keycloak,
  gerenciamento de eventos, tambem assume as integrações com api externas que facilitam os workflows.


* **api-notification** - API que gerencia as notificações de PUSH e Message para o APP, monitoramento de ações dentro do sistema como: ao ser
  executado uma exclusão é disparado de forma assíncrona uma message com os valores de que realizou a ação e o payload excluido e movido para um
  banco de backup, garantindo economia de dados e rastreabildiade de negócio.


* **Github Actions** - O GitHub Actions foi utilizado nesse projeto para criar uma pipeline de deploy automatizada para o Kubernetes. Com passos
  para executar a pipeline, incluindo a criação de um novo container, o push desse container para o registro de container DigitalOcean, e o
  deployment desse container para o cluster do Kubernetes. O uso dessa pipeline automatizada oferece diversas vantagens, como a simplificação do
  processo de deploy e a melhoria na qualidade do software, garantindo que os testes sejam executados antes da implantação. Além disso, a
  pipeline garante maior segurança e consistência no deploy, reduzindo o risco de erros humanos e garantindo a integridade do sistema.
    - [Documentação oficial do Github Actions](https://docs.github.com/en/actions)


* **Keycloak** - O Keycloak foi utilizado como servidor de autenticação e gerenciamento de acesso no projeto. Ele permite a autenticação de
  usuários e fornece um controle de acesso baseado em roles, simplificando a implementação de políticas de segurança. Além disso, o Keycloak
  oferece recursos como integração com provedores de identidade externos e gerenciamento de usuários e permissões, o que o torna uma opção
  robusta e escalável para projetos que necessitam de controle de acesso e segurança.
    - [Documentação oficial do Keycloak](https://www.keycloak.org/documentation)


* **Exchange RabbitMQ (CloudAMQP)** - Servidor de fila em nuvem utilizado, para movimentação de notificações, processo esse que não precisa ser
  síncrono, a Stack foi RabbitMQ e o serviço em nuvem o CloudAMQP.
    - [Documentação oficial do RabbitMQ](https://www.rabbitmq.com/documentation.html)
    - [Documentação oficial do CloudAMQL](https://www.cloudamqp.com/docs/index.html)


* **MySQL (Babilonia)** - Banco de dados em uma instância no Amazon RDS que armazena todas tabelas de notificações. (Backup a cada 7 Dias)
    - [Documentação oficial do Amazon RDS](https://aws.amazon.com/rds/)
    - [Documentação oficial do MySQL](https://dev.mysql.com/doc/)


* **MySQL (Constantinopla)** - Banco de dados em uma instância no Amazon RDS que armazena todas tabelas de usuários e configurações do Keycloak (
  backup a cada 7 dias)
    - [Documentação oficial do Amazon RDS](https://aws.amazon.com/rds/)
    - [Documentação oficial do MySQL](https://dev.mysql.com/doc/)

* **MongoDB (Pompeia)** - Banco de dados que armazena todas informações de Eventos e Tags
    - [Documentação oficial do MongoDB](https://docs.mongodb.com/)


* **job-event-increment (event.list)** - Serviço em JOB que executa a leitura de uma planilha .xlsx e cadastra em massa todos os eventos nela
  contido. Esse processo roda fora do cluster e pode ser executado via schedulled ou localmente em qualquer máquina com Java.


* **Amazon S3 - Bucket** - Bucket na AWS que armazena as imagens utilizadas para eventos e usuários.
    - [Documentação oficial do Amazon S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html)


* **Google Map API** - API do Google Maps que preenche os dados de endereço de cada evento.
    - [Documentação oficial do Google Map API](https://developers.google.com/maps/documentation)


* **Wordpress/HostGator** - Foi usado uma combinação entre Wordpress & HostGator para que tenhamos um domínio próprio e uma área de gerenciamento
  para nossa Landing Page.
    - [Documentação oficial do WordPress](https://wordpress.org/support/)
    - [Documentação oficial do Hostgator](https://support.hostgator.com/)


* **GO: Em qualquer Lugar** - Aplicativo feito com Flutter SDK(Dart) e liberado na AppStore e Play Store, esse APP se conecta de forma
  autenticada com nosso serviço principal através da go-api-control. Também no app foi criado um gerenciamento de cache inteligente que mantem
  informações retidas na memória local do dipsositivo por um período de X horas de acordo com a necessidade do negócio.
    - [Documentação oficial do Flutter SDK](https://flutter.dev/docs)
    - [Documentação oficial do Dart](https://dart.dev/guides)
    - [Documentação oficial do Flutter Cache Manager](https://pub.dev/packages/flutter_cache_manager)
    - [Documentação oficial da App Store](https://developer.apple.com/documentation/appstore/)
    - [Documentação oficial da Play Store](https://developer.android.com/google/play)

## Banco de dados

### Amazon RDS (MySQL) - babilonia

Gerenciamento de Notificações
![BABILONIA!](https://user-images.githubusercontent.com/48265863/226209055-4729c6a5-dfbe-4831-9278-14916ed2f354.png)

### Amazon RDS (MySQL) - constantinopla

Gerenciamento de Usuários e Roles
![CONSTANTINOPLA!](https://user-images.githubusercontent.com/48265863/226209278-82f60a8f-e6d5-4d1e-97ce-3ec9499bfb0d.png)

### MongoDB Atlas (MongoDB) - pompeia

Gerenciametno de Eventos e Tags

![POMPEIA](https://user-images.githubusercontent.com/48265863/226209870-04ec0a50-5a3e-491b-b2e5-bed8be559989.png)

## Docker Compose

Docker Compose é uma ferramenta para definir e executar aplicativos Docker de vários contêineres. Ele permite definir toda a infraestrutura
necessária para o seu aplicativo em um único arquivo, facilitando o processo de configuração do ambiente local de desenvolvimento e evitando a
necessidade de executar vários comandos manualmente.

No projeto, o Docker Compose foi utilizado para orquestrar a execução dos serviços necessários, como o banco de dados, o servidor de aplicativos
e o servidor web, em contêineres separados e interligados. Isso simplificou o processo de configuração do ambiente de desenvolvimento local,
permitindo que a equipe de desenvolvimento trabalhasse de maneira mais eficiente e focada na criação do aplicativo. Além disso, o uso do Docker
Compose facilitou a reprodução do ambiente de desenvolvimento em diferentes máquinas e a implantação do aplicativo em ambientes de produção.

O arquivo de docker-compose se encontra na raiz desse repositório.

## Keycloak | Uso

O Keycloak foi utilizado no projeto como solução de gerenciamento de autenticação e autorização, seguindo alguns padrões de gerenciamento de
usuários.

Para isso, foi configurado um realm chamado "go-app-realm", que define um escopo de segurança, permitindo a definição de usuários, grupos e
clientes. Além disso, foi criado um cliente com o ID "go-app-client-id".

Também foram definidas roles tanto para o client quanto para o realm. No client, foram criadas as roles "PROFILE_XXXXXX_XXXXXX", "
PROFILE_XXXXXX_XXXXXX", "PROFILE_XXXXXX_XXXXXX", "PROFILE_XXXXXX_XXXXXX", "PROFILE_XXXXXX_XXXXXX" e "PROFILE_XXXXXX_XXXXXX". Já no realm, foram
criadas as roles "ADMIN", "MANAGER", "PARTNER" e "INFLUENCER".

Adicionalmente, foram criados três perfis de usuário que são definidos como roles do realm:

PERFIL MANAGER: possui todas as permissões. PERFIL PARTNER: possui as permissões "PROFILE_XXXXXX_XXXXXX", "PROFILE_XXXXXX_XXXXXX" e "
PROFILE_XXXXXX_XXXXXX". PERFIL INFLUENCER: possui as permissões "PROFILE_XXXXXX_XXXXXX" e "PROFILE_XXXXXX_XXXXXX". Por fim, foi criado um usuário
administrador com permissões de gerenciamento de tokens de autenticação.

# Apache Archetype

O Apache Archetype foi utilizado no projeto para padronizar a criação de microsserviços. Com isso, é possível reduzir o tempo e os custos de
desenvolvimento, além de facilitar a manutenção e evolução do sistema como um todo. Os arquétipos gerados seguem as melhores práticas e padrões
definidos pelo projeto principal, o que garante maior qualidade e consistência no código produzido.

O repositório do apache archetype é um repositório liberado na raiz desse projeto ou você pode
acessar [nesse link](https://github.com/gasil96/go-archetype-ms).

## **Heroku** x **AWS** x **Digital Ocean**

Durante o processo de desenvolvimento do MVP, foi decidido usar a Heroku como plataforma de hospedagem para os ambientes de teste. No entanto, ao
longo do tempo, foi se percebendo que o preço da Heroku não entregava a qualidade que se esperava comparado a outras plataformas. Então, se
iniciou o estudo sobre outras opções como a AWS, que é conhecida por sua confiabilidade e escalabilidade.

Após algumas tentativas, no final se optou pela DigitalOcean, que exigiu um pouco mais de configuração em comparação com a Heroku e a AWS, mas
entregava mais qualidade e um melhor custo-benefício. A plataforma se mostrou uma excelente escolha para hospedagem do MVP, pois permitia uma
fácil escalabilidade, além de fornecer recursos e ferramentas necessários para a manutenção e gerenciamento da aplicação.

Apesar de ter exigido mais tempo e esforço para configurar, o retorno foi satisfatório com a escolha da DigitalOcean, pois permitiu o
desenvolvimento do MVP com mais qualidade e eficiência. A plataforma se mostrou uma solução robusta e confiável para a hospedagem da aplicação,
além de ser uma opção mais acessível em termos de custo-benefício.

## Jira | Figma | Slack

Durante o processo de criação do MVP do aplicativo, foram utilizadas algumas ferramentas para ajudar a gerenciar o projeto de forma ágil e
colaborativa. O Jira foi usado como plataforma de gerenciamento de projetos, permitindo a criação e acompanhamento de tarefas e bugs, bem como a
definição de sprints e pontos de histórias.

O Figma foi utilizado para criar protótipos e wireframes do aplicativo, permitindo a colaboração entre designers e desenvolvedores e garantindo
uma visão clara do que seria desenvolvido. Isso facilitou a definição de prioridades e a implementação de mudanças no design do aplicativo.

O Slack foi usado para manter a comunicação em tempo real entre a equipe, permitindo que todos estivessem sempre atualizados sobre o andamento do
projeto e facilitando a organização de reuniões periódicas, como as daily scrums e as retrospectivas. Isso permitiu que a equipe trabalhasse de
forma mais colaborativa e eficiente, tornando o processo de desenvolvimento mais ágil e assertivo.

## Agradecimentos e Contato

Atualmente em Março de 2023 o GO é um projeto ativo e mantido de forma completamente independente. Caso deseje fazer uma parceria ou ter seu
evento em destaque no nosso APP, acesse o nosso [site](http://goanywhere.app.br) ou entre em contato via Whats APP: (91) 9 8217-9201 (Gabriel)

"Comece onde você está. Use o que você tem. Faça o que você pode." - Arthur Ashe

💚
