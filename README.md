# FreeKenzie API

Bem vindo, nessa API você poderá acessar usuários cadastrados e vagas de projetos disponíveis.

Base URL: https://freekenzie.onrender.com

## Endpoints

### Rotas que não precisam de autenticação 

#### Usuários para demonstração

`GET /free -  FORMATO DA RESPOSTA `

```json
 [
  {
    "id": 2,
    "name": "Gabriel Machado",
    "email": "gabriel@mail.com",
    "avatar": "",
    "description": "Desenvolvedor Front End, iniciando os estudos em Back End na Kenzie Academy Brazil.",
    "contact": "gabriel@mail.com"
    "type": "developer",
    "techs": [
      {
        "id": 1,
        "title": "Python"
        "level": "Iniciante"
      }
    ]
  }
```

#### Listando Vagas

`GET /jobs -  FORMATO DA RESPOSTA `

`GET /jobs/:id -  FORMATO DA RESPOSTA`

```json
[
	{
      "jobName": "Desenvolvedor Front End - JavaScript",
      "jobOwnerID": 1,
      "description": "Necessário desenvolvedor que possua conhecimento em React para ajudar na criação do projeto BaseESports",
      "devs": [],
      "id": 1
    }
]
```

### Cadastro

`POST /users - FORMATO DA REQUISIÇÃO`

```json
  {
    "email": "joaozinho@mail.com",
    "password": "batata1234",
    "avatar": "",
    "name": "Joao da Silva",
    "description": "",
    "contact": "",
    "type": "developer"
    "techs": []
  }
```

```json
  {
    "email": "maisDevs@mail.com",
    "password": "devs1234",
    "avatar": "",
    "name": "+Devs",
    "description": "",
    "contact": "",
    "type": "company"
  }
```

Caso dê tudo certo, a resposta será assim:

```json
  {
    "id": "35",
    "name": "Joao da Silva",
    "email": "joaozinho@mail.com",
    "avatar": "",
    "description": "",
    "contact": "",
    "type": "developer",
    "techs": []
  }
```

Possíveis erros:

```json
  {
    "status": "error",
    "message": "Email already exists"
  }
```

### Login

`POST /login - FORMATO DA REQUISIÇÃO` 

```json
  {
    "email": "johndoe@email.com",
    "password": "teste123456"
  }
```

Possíveis erros:

```json
  {
    "status": "error",
    "message": "Incorrect password"
  }

```
```json
  {
    "status": "error",
   "message": "Cannot find user"
  }

```


Caso dê tudo certo, a resposta será assim:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2MDcxODM3NzYsImV4cCI6MTYwNzQ0Mjk3Niwic3ViIjoiMmE3NWUxMmQtZmQxYy00ODFkLWJhODgtNGQ4YjE3MTAzYjJhIn0.UY67X23mPYAAzT43uFWZDHPUakd2STo5w4AuOcppkyQ"
  "user": {
    "id": "53",
    "name": "John Doe",
    "email": "johndoe@email.com",
    "avatar": "",
    "description": "",
    "contact": "johndoe@email.com"
    "type": "developer",
    "techs": []
  },
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o id logado no localStorage para fazer a gestão do usuário no seu frontend.

### Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

`Authorization: Bearer {token}`

#### Listando usuários

Nessa aplicação o usuário quando logado pode ver os usuários já cadastrados na plataforma.

`GET /users -  FORMATO DA RESPOSTA`

`GET /users/:user_id -  FORMATO DA RESPOSTA`

```json
 [
  {
      "email": "antonio@mail.com",
      "password": "$2a$10$GwpxDo70ZWpWLyLdq1UcT.E6rkBSOwZkD5PavX4Hpi057YkfArZJ.",
      "name": "Pedro Barros Silva",
      "type": "developer",
      "avatar": "",
      "description": "",
      "contact": "antonio@mail.com",
      "techs": [
        {
          "id": 1,
          "title": "JavaScript",
          "level": "Avançado"
        },
        {
          "id": 2,
          "title": "Git",
          "level": "Intermediário"
        }
      ],
      "id": 8
    },
  {
      "email": "maisDevs@mail.com",
      "password": "$2a$10$GwpxDo70ZWpWLyLdq1UcT.E6rkBSOwZkD5PavX4Hpi057YkfArZJ.",
      "name": "+Devs",
      "type": "company",
      "avatar": "",
      "description": "",
      "contact": "maisDevs@mail.com",
      "id": 12
    }
 ]
```

### Atualizar informações do seu perfil

Para adicionar, atualizar ou deletar tecnologias é necessário realizar uma atualização contendo os dados antigos + dados novos.

`PATCH /users/:id - FORMATO DA REQUISIÇÃO`

```json
  {
    "techs":[
      {
        "id": 0,
        "title": "Python",
        "level": "Iniciante"
      },
      {
        "id": 1,
        "title": "JavaScript",
        "level": "Avançado"
      }
    ]
  }
```
O campo level deve receber respectivamente os 3 níveis de habilidade:
<ul>
  <li>"Iniciante"</li>
  <li>"Intermediário"</li>
  <li>"Avançado"</li>
</ul>

### Criar vaga
 Somente para usuários do tipo company.

`POST /jobs - FORMATO DA REQUISIÇÃO`

```json
{
	"jobName": "Desenvolvedor Front End",
	"jobOwnerID": 3,
	"description":"Necessário desenvolver com conhecimento avançado em JavaScript para se unir a equipe no projeto BuscaPets",
	"devs": []
}
```


### Atualizar vaga
 Somente para usuários do tipo developer.
 
 Para se candidatar a vaga ou cancelar a candidatura é necessário realizar uma atualização contendo os dados antigos + dados novos.
 
 `PATCH /jobs/:id - FORMATO DA REQUISIÇÃO`
 
 ```json
{
	"devs": [
    {
      "name": "Pedro Barros da Silva",
      "id": "8",
      "techs":[
       {
        "id": 0,
        "title": "Python",
        "level": "Iniciante"
      },
      {
        "id": 1,
        "title": "JavaScript",
        "level": "Avançado"
      }
      ]
    }
  ]
}
```

### Deletar vaga
 Somente o dono da vaga pode deletá-la.
 
 `DELETE /jobs/:id - FORMATO DA RESPOSTA - status 200`
 
```json
{}
```
