<h1 align="center">
  <img alt="KenzieHub" title="KenzieHub" src="https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=640&q=75" width="100px" />
</h1>

<h1 align="center">
  Portify - API
</h1>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

A API tem um total de 13 endpoints, sendo em volta principalmente do usuário (dev) - podendo cadastrar seu perfil, tecnologias que estuda e trabalhos realizados. <br/>

A url base da API é https://kenzie-portify-api.onrender.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Buscar portfólio por usuário </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os produtos já cadastrados na plataforma, na API podemos acessar a lista dessa forma:

`GET /portfolios?_embed=projects&userId=:userId - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "userId": 1,
    "color": "claro",
    "position": "Tech Lead",
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer pulvinar urna ante, nec dapibus leo semper nec. Vivamus aliquet nibh nec urna accumsan, eget euismod magna fringilla. Nam condimentum, enim ut rhoncus sagittis, tellus mi sodales erat, nec ornare nunc nisi sed tortor.",
    "projects": [
       {
        "id": 1,
        "portfolioId": 1,
        "name": "tsunodeverso",
        "repository": "https://github.com/tsunode/tsunode-verso-react",
        "link": "https://verso.tsunode.com.br",
        "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
        "coverUrl": "https://www.codingdojo.com/blog/wp-content/uploads/react.jpg"
      }
    ]
  }
]
```

<h2 align ='center'> Buscar portfólio por id </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os produtos já cadastrados na plataforma, na API podemos acessar a lista dessa forma:

`GET /portfolios/:idPortfolio?_embed=projects&_expand=user - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "id": 1,
  "userId": 1,
  "color": "claro",
  "position": "Tech Lead",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer pulvinar urna ante, nec dapibus leo semper nec. Vivamus aliquet nibh nec urna accumsan, eget euismod magna fringilla. Nam condimentum, enim ut rhoncus sagittis, tellus mi sodales erat, nec ornare nunc nisi sed tortor.",
  "projects": [
    {
      "id": 1,
      "portfolioId": 1,
      "name": "tsunodeverso",
      "repository": "https://github.com/tsunode/tsunode-verso-react",
      "link": "https://verso.tsunode.com.br/"
    },
    {
      "portfolioId": 1,
      "name": "teste3",
      "repository": "https://github.com/tsunode/tsunode-verso-react",
      "link": "ricardo.rufino/",
      "id": 4
    }
  ],
  "user": {
    "email": "kenzinho@mail.com",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "name": "Kenzinho",
    "age": 38,
    "id": 1
  }
}
```



<h2 align ='center'> Criação de usuário </h2>

`POST /users - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456",
  "name": "John Doe",
}
```

Caso dê tudo certo, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAZW1haWwuY29tIiwiaWF0IjoxNjg3ODA4MTYzLCJleHAiOjE2ODc4MTE3NjMsInN1YiI6IjMifQ.nWj1gqD4t3x00UTQvfFiK-PQjcgSpzbGeHknpncgC9E",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "id": 3
  }
}
```


<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAZW1haWwuY29tIiwiaWF0IjoxNjg3ODA4MTYzLCJleHAiOjE2ODc4MTE3NjMsInN1YiI6IjMifQ.nWj1gqD4t3x00UTQvfFiK-PQjcgSpzbGeHknpncgC9E",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "id": 3
  }
}
```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}


<h2 align ='center'> Buscar usuario </h2>

`GET /users/:idUser - FORMATO DA REQUISIÇÃO` - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "johndoe@email.com",
  "name": "John Doe",
  "id": 3
}
```



<h2 align ='center'> Criar Portifólio </h2>

`POST /portfolios - FORMATO DA REQUISIÇÃO`

```json
{
  "userId": 1,
  "color": "claro",
  "position": "Tech Lead",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer pulvinar urna ante, nec dapibus leo semper nec. Vivamus aliquet nibh nec urna accumsan, eget euismod magna fringilla. Nam condimentum, enim ut rhoncus sagittis, tellus mi sodales erat, nec ornare nunc nisi sed tortor."
}
```

<h2 align ='center'> Atualizar Portifólio </h2>

`PATCH /portfolios/:idPortfolio - FORMATO DA REQUISIÇÃO`

```json
{
  "color": "claro",
  "position": "Tech Lead",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer pulvinar urna ante, nec dapibus leo semper nec. Vivamus aliquet nibh nec urna accumsan, eget euismod magna fringilla. Nam condimentum, enim ut rhoncus sagittis, tellus mi sodales erat, nec ornare nunc nisi sed tortor."
}
```

<h2 align ='center'> Adicionar Projeto ao portfólio  </h2>

`POST /projects - FORMATO DA REQUISIÇÃO`

```json
{
  "portfolioId": 1,
  "name": "tsunodeverso",
  "repository": "https://github.com/tsunode/tsunode-verso-react",
  "link": "https://verso.tsunode.com.br/",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
  "coverUrl": "https://www.codingdojo.com/blog/wp-content/uploads/react.jpg"
}
```

<h2 align ='center'> Atualizar Projeto do portfólio  </h2>

`PUT /projects/:idProject - FORMATO DA REQUISIÇÃO`

```json
{
  "name:": "tsunodeverso",
  "repository": "https://github.com/tsunode/tsunode-verso-react",
  "link": "https://verso.tsunode.com.br/",
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
  "coverUrl": "https://www.codingdojo.com/blog/wp-content/uploads/react.jpg"
}
```
<h2 align ='center'> Deletar Projeto do portfólio  </h2>

`DELETE /projects/:id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Buscar Apenas Projetos do portfólio  </h2>

`GET /portfolios/:idPortfolio/projects/ - FORMATO DA RESPOSTA - STATUS 200`

```json
[
   {
    "id": 1,
    "portfolioId": 1,
    "name": "tsunodeverso",
    "repository": "https://github.com/tsunode/tsunode-verso-react",
    "link": "https://verso.tsunode.com.br",
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
    "coverUrl": "https://www.codingdojo.com/blog/wp-content/uploads/react.jpg"
  }
]
```
