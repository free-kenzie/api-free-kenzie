# FreeKenzie API

## Endpoints

### Rotas que não precisam de autenticação 

#### Listando usuários

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os devs já cadastrados na plataforma, na API podemos acessar a lista dessa forma: Aqui conseguimos ver os usuários, seus dados e suas tecnologias cadastradas.

`GET /users -  FORMATO DA RESPOSTA`

`GET /users/:user_id -  FORMATO DA RESPOSTA`

```json
 [
  {
    "id": 72,
    "name": "Teste",
    "email": "teste@mail.com",
    "avatar": null,
    "description": "Algum texto aqui",
    "type": "developer",
    "techs": [
      {
        "id": 1,
        "title": "Python"
        "level": "Iniciante"
      }
    ]
  },
  {
    "id": 158,
    "name": ,
    "email": ,
    "avatar": ,
    "description": ,
    "type": "company"
  }
 ]
```

#### Listando Vagas

`GET /jobs -  FORMATO DA RESPOSTA `

`GET /jobs/:id -  FORMATO DA RESPOSTA`

```json
[
	{
		"jobName": "Primeiro teste",
		"jobOwnerID": 3,
		"status": "open",
		"description": "",
		"devs": [],
		"id": 1
	}
]
```

### Cadastro
`POST /users - FORMATO DA REQUISIÇÃO`

```json
  {
    "email": "teste@mail.com",
    "password": "teste1234",
    "avatar": null,
    "name": "John Doe",
    "description": "",
    "contact": "",
    "type": "developer"
    "techs": []
  }
```

```json
  {
    "email": "teste@mail.com",
    "password": "teste1234",
    "avatar": null,
    "name": "John Doe",
    "description": "",
    "contact": "",
    "type": "company"
  }
```

Caso dê tudo certo, a resposta será assim:

```json
  {
    "id": "35",
    "name": "John Doe",
    "email": "teste@mail.com",
    "avatar": null,
    "description": "",
    "contact": "",
    "type": "developer",
    "techs": []
  }
```

Possíveis erros

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

Possíveis erros

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
    "id": "2",
    "name": "John Doe",
    "email": "johndoe@email.com",
    "avatar": null,
    "description": ""
    "type": "developer",
    "techs": []
  },
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.


### Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

`Authorization: Bearer {token}`

### Atualizar informações do seu perfil

`PATCH /users/:id - FORMATO DA REQUISIÇÃO`

```json
  {
    "techs":[
      {
        "id": 0,
        "title": "Python",
        "level": "Iniciante"
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
 Somente para usuários do tipo company

`POST /jobs - FORMATO DA REQUISIÇÃO`

```json
{
	"jobName": "Desenvolvedor Front End",
	"jobOwnerID": 3,
	"description":"",
	"devs": []
}
```


### Atualizar vaga
 Somente para usuários do tipo developer
 
 `PATCH /jobs/:id - FORMATO DA REQUISIÇÃO`
 
 ```json
{
	"devs": [
    {
      "name": "",
      "id": "",
      "techs":[]
    }
  ]
}
```

### Deletar vaga
 Somente para usuários do tipo company
 
 `DELETE /jobs/:id - FORMATO DA RESPOSTA - status 200`
 
```json
{}
```
