# RayCo

Consiste em desenvolver uma plataforma de avaliações e busca de universidades.

## 📑 Sumário

- [🧱 Arquitetura](#arquitetura)
- [🛠️ Tecnologias](#tecnologias)
- [📌 Regras de Negócio](#regras-de-negocio)
- [🚀 Como rodar o projeto](#como-rodar-o-projeto)
- [🔧 Pontos de melhoria](#pontos-de-melhoria)

<a id="arquitetura"></a>
## 🧱 Arquitetura
  Para a estrutura macro do projeto,  tomei como base o Clean Architecture, separando minha aplicação por 
  domínios, aplicando esse conceito na divisão dos arquivos. A imagem abaixo é para demonstrar os principais
  domínios que mapeei.

![image](https://github.com/user-attachments/assets/187380f1-372f-4db3-8783-3befa890d815)

Essa é uma representa a estrutura de pastas seguindo esse viés 
```text
Src/
├── Application/
│   ├── Client/
│   ├── Exceptions/
│   ├── Middleware/
│   └── Service/
├── Domain/
│   ├── Entity/
│   └── Enums/
├── Infrastructure/
│   └── Configuration/
│      
└── Presentation/
    ├── Controller/
    ├── DTO/
    └── Mapper/
```
  
O domínio da minha aplicação é composto por 3 principais entidades **User**, **University** e **Course**
A imagem abaixo representa o relacionamento entre elas

![image](https://github.com/user-attachments/assets/97ff11dd-2a41-43a3-9d50-50a5deb9d69b)

<a id="tecnologias"></a>
## 🛠️ Tecnologias
- Java com SpringBoot
- Keycloak (para o gerenciamento de usuários)

  - Keycloak é uma ferramenta de autenticação e autorização de código aberto, desenvolvida
    originalmente pela Red Hat, que permite adicionar facilmente funcionalidades de login,
    controle de acesso e gerenciamento de usuários em aplicações modernas.

    ⚙️ Casos de uso comuns:

    Proteger APIs REST (com tokens JWT)

    Aplicações web com login via Keycloak

    Microserviços que precisam compartilhar autenticação centralizada

    Portais com vários sistemas acessados via login único (SSO)
- Docker
- PostgreSQL
- React Native
<a id="regras-de-negocio"></a>
## 📌 Regras de Negócio
Nesta seção vou elucidar as principais regras de negócio da aplicação
- Usuários só podem ser criados por usuários **ADMIN**
  - O usuário ADMIN default da aplicação tem as credenciais email: **admin@provider.com** senha: **admin**
    a partir dele você pode criar outros usuarios. No endpoint de criação basta colocar qual o tipo de usuário
    **"userType": "ADMIN"** ou **"userType": "USER"**
    
- Apenas usuários administradores podem adicionar saldo na carteira de outros usuários,
  isso impede que usuários adicionem saldo a sua própria carteira.
  
- Apenas usuários administradores podem listar todos os usuários da aplicação

- Todo usuário inicialmente cadastrado, para a massa de testes, tem a senha de login
como o nome que está antes do @ no email, exemplo: usuário **admin@provider.com** senha: **admin**

- Quando um usuário é cadastrado na aplicação, as suas informações de Nome, Email e Id são salvas na base de dados da aplicação.
  E esse usuário terá um registro espelhado no Keycloak, porém o provider ficará responsável por gerenciar as informação de
  Password, Groups e Roles. 
  
<a id="como-rodar-o-projeto"></a>
## 🚀 Como rodar o projeto
Requisitos:
  
  Ter o docker instalado na maquina

Passo a passo:

1. Clonar repositórios rayco-api e rayco-mobile
2. Abrir um terminal na pasta `PASTA_PESSOAL/rayco-api`
3. Executar o comando `docker-compose up -d`
4. Após executar todos os comandos espere uns 40s para que o keycloak possa se configurar totalmente
5. Rodar o backend a partir de comando ou pela IDE
6. Abrir um terminal na pasta `PASTA_PESSOAL/rayco-mobile`
7. Executar o comando npm install e depois npm start
8. Ler o QR code com seu celular, lembrando que o ExpoGo deve estar instalado
9. Por fim, basta logar com o usuário email: **admin@provider.com** senha: **admin** e realizar as operações

<a id="pontos-de-melhoria"></a>
## 🔧 Pontos de melhoria
- Criar testes automatizados
- Melhorar o retorna dos erros na response dos enpoints
- Criar logica de avaliar e média de preços para o front
