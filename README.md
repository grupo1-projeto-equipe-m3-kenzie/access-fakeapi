https://access-fakeapi-12yk.onrender.com

# ACCESS-FAKEPI

Este é o backend da aplicação Access, uma plataforma de viagens com o objetivo dos viajantes compartilharem experiências, informações sobre pontos turísticos e locais para visitar, estadias e rotas para passeios, além de poderem comentar nas publicações uns dos outros. 

# Endpoints:
A API tem um total de 10 endpoints, divididos entre posts e usuários: o usuário pode se cadastrar, cadastrar, ler e pesquisar posts, comentar nos mesmos e seguir outros usuários.

O URL base da API é https://access-fakeapi-12yk.onrender.com/

# Rotas que não precisam de autenticação

VISUALIZAR POSTS

Nessa aplicação, para os usuários visualizarem os posts cadastrados, não é necessário autenticação.

GET /posts - FORMATO DA RESPOSTA - STATUS 200

[
	{
		"title": "Viagem incrível para Gaspar/SC",
		"state": "SC",
		"city": "Gaspar",
		"country": "Brasil",
		"img": "",
		"description": "Nossa viagem foi sensacional! Ficamos na Cabanas Maktup, uma casinha no meio da mata que te traz uma sensação de paz, contato com a natureza, tranquilidade e paz. O lugar ideal para quem quer recarregar as energias e ficar alguns dias 'isolado' da socidade.",
		"userId": 1,
		"id": 1,
		"comments": []
	},
	{
		"title": "Caminhada na natureza",
		"state": "PR",
		"city": "São José dos Pinhais",
		"country": "Brasil",
		"img": "",
		"description": "Se você curte contato com a natureza, praticar atividade física e conhecer outras pessoas, o programa ideal é participar de uma caminhada na natureza. A 7a caminhada notura da Colônica Murici, em São José dos Pinhais, foi uma experiência incrível, com desafios de não cair /(sim, devido a chuva, o terreno estava super enlameado)/, acompanhada de uma lua cheia esplêndia. Caminhada super recomendada!",
		"userId": 1,
		"id": 2,
		"comments": []
	},
	{
		"title": "Pontos turísticos de Curitiba",
		"state": "PR",
		"city": "Curitiba",
		"country": "Brasil",
		"img": "",
		"description": "Curitiba, a capital do Paraná, é repleta de pontos turísticos. De parques, bosques, até uma vida noturna agitada, é uma cidade que vale a pena visitar.",
		"userId": 2,
		"id": 3
	}
]

CADASTRO DE NOVO USUÁRIO

POST /register - FORMATO DA REQUISIÇÃO
{
	"name": "Teste",
	"email": "teste@kenzie.com",
	"password": "123456",
	"img": "",
	"isAdm": "false",
	"following": [],
	"posts": []
}

Se o usuário for criado com sucesso, a resposta será no seguinte formato:

POST /register - FORMATO DA RESPOSTA - STATUS 201

{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlMkBrZW56aWUuY29tIiwiaWF0IjoxNjc4MDQ4MTk0LCJleHAiOjE2NzgwNTE3OTQsInN1YiI6IjMifQ.hRxe_29CR3YHN1Fct04aA8_rp0vkGow6fjo6n5Eid28",
	"user": {
		"email": "teste2@kenzie.com",
		"name": "Teste2",
		"img": "",
		"isAdm": "false",
		"following": [],
		"posts": [],
		"id": 3
	}
}

Possíveis erros: 
O email e a senha são campos obrigatórios.

POST /register - FORMATO DA RESPOSTA  - STATUS 400
"Email and password are required"

E-mail com formato inválido.

POST /register - FORMATO DA RESPOSTA  - STATUS 400
"Email format is invalid"

O e-mail já existe.

POST /register - FORMATO DA RESPOSTA  - STATUS 400
"Email already exists"

LOGIN

POST /login

{
	"email": "teste@kenzie.com",
	"password": "123456"
}

Se o login for realizado com sucesso, a resposta será no seguinte formato:

POST /login  - FORMATO DA RESPOSTA - STATUS 200

{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGtlbnppZS5jb20iLCJpYXQiOjE2NzgwNDg0MjAsImV4cCI6MTY3ODA1MjAyMCwic3ViIjoiMiJ9.qTD0EWOkCnqcLspTLCNCU-FdL4Wt26xXm72P4i1Dp3g",
	"user": {
		"email": "teste@kenzie.com",
		"name": "Teste",
		"img": "",
		"isAdm": "false",
		"id": 2
	}
}

Com essa resposta, vemos que temos duas informações: "user" e o "accessToken". Dessa forma, é possível armazenar o token e o usuário logado no "localStorage" para fazer a gestão do usuário no seu frontend.

POSTS DO USUÁRIO

Para retornar os posts de determinado usuário, será preciso informar o id do usuário.

GET /users/posts?userId={id}

[
	{
		"title": "Pontos turísticos de Curitiba",
		"state": "PR",
		"city": "Curitiba",
		"country": "Brasil",
		"img": "",
		"description": "Curitiba, a capital do Paraná, é repleta de pontos turísticos. De parques, bosques, até uma vida noturna agitada, é uma cidade que vale a pena visitar.",
		"userId": 2,
		"id": 3
	}
]

PESQUISAR POST

Para pesquisar post, será utilizado um query params "q" com o termo a ser pesquisado no conteúdo do post.

GET /posts/?q={termo de busca}

Se a requisição for bem-sucedida, a resposta será:

POST /posts  - FORMATO DA RESPOSTA - STATUS 200


# Rotas que precisam de autenticação

As rotas que precisam de autenticação precisam do respectivo token do usuário no cabeçalho da requisição no campo "Authorization", dessa forma:

Authorization: Bearer {token}

DADOS DO USUÁRIO

Será necessário informar o token e o id do usuário para que as informações do mesmo sejam apresentadas.

GET /users/:id

{
	"email": "teste@kenzie.com",
	"password": "$2a$10$arAElEH2dLw/WNR9YS7FvuN9SGWzOJKg8y4TdDv.yUFGL3SUAY0GW",
	"name": "Teste",
	"img": "",
	"isAdm": "false",
	"id": 2
}

Se a requisição for bem-sucedida, a resposta será:

POST /users  - FORMATO DA RESPOSTA - STATUS 200

CRIAR POST

{
	"title": "Pontos turísticos de Curitiba",
	"state": "PR",
	"city": "Curitiba",
	"country": "Brasil",
	"img": "",
	"description": "Curitiba, a capital do Paraná, é repleta de pontos turísticos. De parques, bosques, até uma vida noturna agitada, é uma cidade que vale a pena visitar.",
	"userId": 2,
	"comments": []
}

Se a requisição for bem sucedida, a resposta será:

POST /users  - FORMATO DA RESPOSTA - STATUS 201

DELETAR POST

Para deletar um post, o usuário precisa estar logado com um token gerado e informar no corpo da requisição, além de informar o id do post a ser deletado.

DELETE /posts/{id}

Se a requisição for bem-sucedida, a resposta será:

POST /users  - FORMATO DA RESPOSTA - STATUS 200







