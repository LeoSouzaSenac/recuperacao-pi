# Recuperação do Projeto Integrador  
## Desenvolvimento de Sistema Full Stack

### IMPORTANTE: se for detectado o uso de IA para produzir o trabalho (salvo apenas para estudo), o aluno estará automaticamente reprovado.

### Material de estudo de backend: https://backend-game-ashy.vercel.app/

### Objetivo

Esta atividade de recuperação tem como objetivo verificar se o aluno desenvolveu os conhecimentos fundamentais trabalhados durante o curso nas áreas de:

- desenvolvimento de back-end;
- desenvolvimento de front-end;
- banco de dados;
- criação de APIs;
- autenticação;
- segurança de senhas;
- organização de projetos;
- integração entre sistemas;
- lógica de programação;
- leitura e compreensão de código.

A recuperação será composta por duas etapas:

1. **Desenvolvimento e apresentação de um projeto prático**
2. **Prova individual após a entrega do projeto**

O projeto deverá ser desenvolvido dentro do prazo de **1 semana**.

---

# 1. Projeto prático

O aluno deverá desenvolver individualmente um sistema web completo contendo:

- front-end;
- back-end;
- banco de dados;
- autenticação;
- CRUD completo;
- integração entre front-end e back-end.

O tema do sistema pode ser escolhido pelo aluno, desde que seja aprovado pelo professor e permita implementar todos os requisitos descritos neste documento.

Exemplos de sistemas possíveis:

- sistema de tarefas;

O sistema deve possuir obrigatoriamente pelo menos duas entidades principais:

- `User`
- `Tasks`

Exemplo:

```text
User
Task
```

---

# 2. Tecnologias obrigatórias

## Back-end

O back-end deverá utilizar obrigatoriamente:

- Node.js;
- TypeScript;
- Express;
- TypeORM;
- MySQL;
- JWT;
- bcrypt;
- dotenv.

Não serão aceitos projetos utilizando arrays ou objetos JavaScript como substituição do banco de dados.

Os dados deverão ser realmente persistidos no MySQL.

---

# 3. Estrutura obrigatória do back-end

O projeto deverá possuir uma organização em camadas.

Estrutura mínima esperada:

```text
src/
│
├── config/
│   └── database.ts
│
├── controllers/
│   ├── AuthController.ts
│   └── EntityController.ts
│
├── entities/
│   ├── User.ts
│   └── Entity.ts
│
├── repositories/
│   ├── UserRepository.ts
│   └── EntityRepository.ts
│
├── services/
│   ├── AuthService.ts
│   └── EntityService.ts
│
├── routes/
│   ├── authRoutes.ts
│   └── entityRoutes.ts
│
├── middlewares/
│   └── authMiddleware.ts
│
├── app.ts
│
└── server.ts
```

Outras pastas poderão ser criadas caso o aluno considere necessário.

---

# 4. Responsabilidade de cada camada

O aluno deverá compreender a função de cada camada utilizada no projeto.

## Config

Responsável pelas configurações gerais da aplicação.

Exemplo:

- conexão com banco;
- variáveis de ambiente;
- configuração do TypeORM.

---

## Entity

Responsável por representar as tabelas do banco de dados.

Exemplo:

```typescript
@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    email: string;

    @Column()
    password: string;
}
```

O aluno deverá compreender:

- `@Entity`;
- `@Column`;
- `@PrimaryGeneratedColumn`;
- tipos de dados;
- relacionamentos, caso sejam utilizados.

---

# 5. Repository

O Repository deverá concentrar o acesso ao banco de dados.

Ele será responsável por operações como:

- buscar registros;
- cadastrar;
- atualizar;
- excluir;
- consultar por ID;
- consultar por e-mail.

O aluno deverá compreender o funcionamento do Repository do TypeORM.

Exemplos:

```typescript
find()
```

```typescript
findOne()
```

```typescript
create()
```

```typescript
save()
```

```typescript
delete()
```

---

# 6. Service

O Service deverá concentrar as regras de negócio da aplicação.

Exemplos:

- verificar se um usuário já existe;
- validar dados;
- criptografar uma senha;
- verificar uma senha;
- criar um token;
- verificar se um registro existe antes de editar;
- impedir determinada operação quando necessário.

O Controller não deverá possuir toda a lógica diretamente.

---

# 7. Controller

O Controller deverá receber as requisições HTTP e utilizar os Services.

O aluno deverá compreender:

```typescript
req.params
```

```typescript
req.body
```

```typescript
req.query
```

```typescript
res.status()
```

```typescript
res.json()
```

Além disso, deverá saber explicar como uma requisição entra pela rota e chega até o banco de dados.

---

# 8. Routes

As rotas deverão ser separadas dos Controllers.

Exemplo:

```typescript
router.get("/tasks", taskController.list);
router.post("/tasks", taskController.create);
router.put("/tasks/:id", taskController.update);
router.delete("/tasks/:id", taskController.delete);
```

O aluno deverá compreender:

- GET;
- POST;
- PUT;
- DELETE;
- parâmetros de rota;
- corpo da requisição;
- códigos HTTP.

---

# 9. CRUD obrigatório

A entidade principal do sistema deverá possuir CRUD completo.

O sistema deverá permitir:

### CREATE

Cadastrar um novo registro.

```http
POST /entity
```

### READ

Listar registros.

```http
GET /entity
```

Consultar um registro específico.

```http
GET /entity/:id
```

### UPDATE

Editar um registro.

```http
PUT /entity/:id
```

### DELETE

Excluir um registro.

```http
DELETE /entity/:id
```

Todas essas operações deverão funcionar também através do front-end.

---

# 10. Cadastro de usuário

O projeto deverá possuir cadastro de usuário.

Exemplo:

```http
POST /auth/register
```

O usuário deverá possuir no mínimo:

```text
id
name
email
password
```

O sistema deverá verificar se o e-mail já está cadastrado.

---

# 11. bcrypt

A senha do usuário não poderá ser armazenada diretamente no banco de dados.

Será obrigatório utilizar `bcrypt`.

O aluno deverá implementar e compreender:

```typescript
bcrypt.hash()
```

e:

```typescript
bcrypt.compare()
```

O banco deverá armazenar apenas o hash da senha.

Durante a apresentação, o aluno deverá saber explicar:

- o que é hash;
- por que não se salva uma senha diretamente;
- para que serve o salt;
- como o bcrypt verifica uma senha.

---

# 12. Login

O sistema deverá possuir autenticação.

Exemplo:

```http
POST /auth/login
```

O login deverá:

1. receber e-mail e senha;
2. buscar o usuário no banco;
3. verificar a senha utilizando bcrypt;
4. gerar um JWT caso os dados estejam corretos.

---

# 13. JWT

O projeto deverá utilizar JSON Web Token.

O token deverá ser gerado utilizando uma chave armazenada no `.env`.

Exemplo:

```text
JWT_SECRET=minha_chave_secreta
```

O aluno deverá compreender:

- o que é JWT;
- para que ele é utilizado;
- como um token é criado;
- como um token é enviado;
- como um token é validado;
- o que significa um token expirar.

---

# 14. Middleware de autenticação

O projeto deverá possuir pelo menos um middleware responsável por verificar o JWT.

Exemplo:

```text
authMiddleware.ts
```

Este middleware deverá:

1. receber o token;
2. verificar se existe;
3. validar o token;
4. permitir ou impedir o acesso à rota.

Pelo menos uma rota do CRUD deverá ser protegida.

Preferencialmente, todas as rotas de criação, edição e exclusão deverão exigir autenticação.

---

# 15. Variáveis de ambiente

Informações sensíveis não poderão ficar diretamente no código.

O projeto deverá possuir `.env`.

Exemplo:

```text
DB_HOST=
DB_PORT=
DB_USER=
DB_PASSWORD=
DB_DATABASE=
JWT_SECRET=
PORT=
```

O `.env` não deverá ser enviado ao GitHub.

O projeto deverá possuir um arquivo:

```text
.env.example
```

sem senhas reais.

---

# 16. Tratamento de erros

O sistema deverá retornar respostas adequadas quando ocorrer algum problema.

Exemplos:

```text
Usuário não encontrado.
```

```text
E-mail já cadastrado.
```

```text
Senha incorreta.
```

```text
Token inválido.
```

```text
Registro não encontrado.
```

Também deverão ser utilizados códigos HTTP adequados.

Exemplos:

```text
200
201
400
401
404
500
```

---

# 17. Front-end

O front-end deverá ser desenvolvido utilizando qualquer tecnologia aprendida durante o curso.

O front-end deverá consumir a API criada pelo próprio aluno.

Pode ser utilizado:

```javascript
fetch()
```

ou:

```javascript
axios
```

---

# 18. Telas obrigatórias

O projeto deverá possuir no mínimo:

## Login

Tela para autenticação.

---

## Cadastro de usuário

Tela para criação da conta.

---

## Listagem

Tela mostrando os registros cadastrados.

---

## Cadastro

Formulário para criação de um novo registro.

---

## Edição

Tela ou formulário para editar um registro existente.

---

## Exclusão

O usuário deverá conseguir excluir um registro pelo front-end.

---

# 19. Integração front-end e back-end

O front-end deverá efetivamente consumir a API.

Exemplo:

```javascript
const response = await fetch("http://localhost:3000/tasks");
const data = await response.json();
```

Não será aceita uma interface com dados estáticos.

O aluno deverá explicar o fluxo completo:

```text
Usuário clica no botão
↓
React executa uma função
↓
Front-end faz uma requisição HTTP
↓
Rota do Express recebe a requisição
↓
Controller é executado
↓
Controller chama o Service
↓
Service executa a regra de negócio
↓
Repository acessa o banco
↓
TypeORM executa a operação
↓
Banco retorna os dados
↓
API devolve uma resposta
↓
Front-end recebe os dados
↓
Interface é atualizada
```

---

# 20. GitHub

O projeto deverá ser entregue através de um repositório GitHub.

O repositório deverá conter:

```text
/backend
/frontend

```



---

# 21. Apresentação

A apresentação será individual.

Mesmo que alunos tenham se ajudado durante o desenvolvimento, cada aluno deverá demonstrar domínio completo do próprio projeto.

O professor poderá selecionar qualquer arquivo, função ou trecho do código e solicitar uma explicação.

Exemplos de perguntas:

- Explique este arquivo.
- Para que serve esta função?
- De onde vêm esses dados?
- O que acontece nesta linha?
- Por que foi utilizado `async`?
- O que o `await` está aguardando?
- Onde esta função é chamada?
- Quem chama este Controller?
- Quem chama este Service?
- Onde o Repository acessa o banco?
- Qual tabela esta Entity representa?
- Como o TypeORM sabe qual tabela utilizar?
- Onde a senha é criptografada?
- Onde a senha é comparada?
- Onde o JWT é criado?
- Onde o JWT é validado?
- O que acontece se o token for inválido?
- Qual endpoint o front-end está chamando?
- O que significa este código HTTP?
- Qual a diferença entre POST e PUT?
- Por que existe um `.env`?
- O que aconteceria se esta linha fosse removida?

O professor poderá solicitar pequenas alterações durante a apresentação.

Exemplos:

- adicionar um novo campo;
- alterar uma validação;
- modificar uma rota;
- criar um filtro;
- mudar um endpoint;
- adicionar uma nova informação na tela;
- modificar uma consulta.

O objetivo dessas alterações será verificar se o aluno compreende o código desenvolvido.

---

# 22. Uso de inteligência artificial

Ferramentas de inteligência artificial poderão ser utilizadas como apoio durante os estudos e desenvolvimento.

Porém, o aluno deverá compreender integralmente o código entregue.

Não será considerada suficiente a entrega de um sistema funcionando caso o aluno não consiga explicar o seu funcionamento.

Códigos gerados por inteligência artificial resultarão  na reprovação do aluno.

---

# 23. Prova individual

Após a entrega e apresentação do projeto será realizada uma prova individual.

A prova terá como objetivo verificar se o aluno realmente compreendeu os conteúdos utilizados no desenvolvimento.

As questões poderão envolver:

- interpretação de código;
- correção de código;
- escrita de pequenos trechos de código;
- explicação de conceitos;
- análise do fluxo de uma aplicação;
- banco de dados;
- APIs;
- TypeORM;
- autenticação;
- JWT;
- bcrypt;
- React;
- integração front-end/back-end.

O projeto e a prova serão considerados em conjunto na recuperação.

---

# Conteúdos que devem ser estudados

Os conteúdos abaixo estão organizados na ordem recomendada de estudo.

## 1. Fundamentos de JavaScript e TypeScript

Estudar:

- variáveis;
- `let` e `const`;
- tipos;
- operadores;
- condicionais;
- `if`;
- `else`;
- funções;
- parâmetros;
- retorno;
- arrays;
- objetos;
- métodos de arrays;
- destructuring;
- spread operator;
- módulos;
- `import`;
- `export`.

Também revisar TypeScript:

```typescript
string
number
boolean
```

Interfaces e tipos:

```typescript
interface User {
    id: number;
    name: string;
}
```

---

## 2. Programação assíncrona

Estudar:

- código síncrono e assíncrono;
- Promise;
- `async`;
- `await`;
- `try`;
- `catch`.

Exemplo:

```typescript
async function listUsers() {
    try {
        const users = await repository.find();
        return users;
    } catch (error) {
        throw error;
    }
}
```

---

## 3. Node.js

Estudar:

- o que é Node.js;
- `package.json`;
- npm;
- instalação de dependências;
- dependências e devDependencies;
- scripts do npm.

Exemplo:

```text
npm install
npm run dev
```

---

## 4. Express

Estudar:

- criação do servidor;
- `express()`;
- `app.use`;
- `express.json()`;
- rotas;
- Router;
- request;
- response.

---

## 5. HTTP e API REST

Estudar:

### Métodos

```text
GET
POST
PUT
DELETE
```

### Status HTTP

```text
200 OK
201 Created
400 Bad Request
401 Unauthorized
404 Not Found
500 Internal Server Error
```

Também estudar:

- endpoint;
- request;
- response;
- JSON;
- parâmetros;
- body;
- query;
- headers.

---

## 6. Banco de dados MySQL

Estudar:

- banco de dados;
- tabela;
- coluna;
- registro;
- chave primária;
- chave estrangeira;
- tipos de dados.

Revisar SQL:

```sql
SELECT
INSERT
UPDATE
DELETE
```

Também revisar:

```sql
WHERE
```

---

## 7. ORM

Estudar o conceito de ORM.

Compreender a relação:

```text
Objeto TypeScript
↓
ORM
↓
Tabela do banco
```

---

## 8. TypeORM

Estudar:

- DataSource;
- Entity;
- Repository;
- decorators;
- `@Entity`;
- `@Column`;
- `@PrimaryGeneratedColumn`.

Operações:

```typescript
find()
findOne()
create()
save()
delete()
```

---

## 9. Arquitetura em camadas

Estudar muito bem a responsabilidade de:

```text
Route
Controller
Service
Repository
Entity
Config
Middleware
```

O aluno deverá conseguir explicar o fluxo entre todas essas camadas.

---

## 10. CRUD

Compreender completamente:

```text
CREATE
READ
UPDATE
DELETE
```

Relacionando com:

```text
POST
GET
PUT
DELETE
```

---

## 11. Senhas e bcrypt

Estudar:

- segurança de senha;
- hash;
- salt;
- bcrypt;
- `bcrypt.hash`;
- `bcrypt.compare`.

Compreender por que a senha original não deve ser armazenada.

---

## 12. Autenticação

Estudar:

- cadastro;
- login;
- autenticação;
- autorização;
- usuário autenticado;
- credenciais.

Compreender a diferença entre:

```text
Autenticação
```

e:

```text
Autorização
```

---

## 13. JWT

Estudar:

- JSON Web Token;
- geração do token;
- assinatura;
- chave secreta;
- payload;
- expiração;
- validação.

Conhecer:

```typescript
jwt.sign()
```

```typescript
jwt.verify()
```

---

## 14. Middleware

Estudar:

- conceito de middleware;
- `req`;
- `res`;
- `next`;
- middleware de autenticação;
- proteção de rotas.

---

## 15. Variáveis de ambiente

Estudar:

- `.env`;
- `process.env`;
- dotenv;
- informações sensíveis;
- `.gitignore`;
- `.env.example`.

---

## 16. React

Estudar:

- componentes;
- JSX;
- props;
- estado;
- eventos;
- formulários.

Principalmente:

```javascript
useState
```

e:

```javascript
useEffect
```

---

## 17. Requisições no front-end

Estudar:

```javascript
fetch
```

ou:

```javascript
axios
```

Compreender:

- requisição GET;
- requisição POST;
- requisição PUT;
- requisição DELETE;
- envio de JSON;
- recebimento de JSON.

---

## 18. Formulários no React

Estudar:

- inputs controlados;
- `value`;
- `onChange`;
- submit;
- `preventDefault`.

---

## 19. Integração completa

Esta é uma das partes mais importantes da prova.

O aluno deverá compreender completamente o fluxo:

```text
React
↓
HTTP
↓
Route
↓
Controller
↓
Service
↓
Repository
↓
TypeORM
↓
MySQL
```

E o caminho de volta:

```text
MySQL
↓
TypeORM
↓
Repository
↓
Service
↓
Controller
↓
Response HTTP
↓
React
↓
Tela
```

---

# Prioridade de estudo

Caso o aluno tenha pouco tempo, a prioridade deverá ser:

### Prioridade máxima

1. CRUD
2. HTTP
3. API REST
4. Express
5. Controller
6. Service
7. Repository
8. Entity
9. TypeORM
10. MySQL
11. async/await
12. integração front-end/back-end

### Depois

13. bcrypt
14. login
15. JWT
16. middleware
17. `.env`

### Front-end

18. React
19. `useState`
20. `useEffect`
21. formulários
22. fetch/axios

---

# Condição fundamental da recuperação

O sistema funcionar será apenas uma parte da avaliação.

O aluno deverá demonstrar que compreende o código que entregou.

O aluno deve ser capaz de explicar:

```text
o que o código faz;
por que ele existe;
onde ele é utilizado;
o que ele recebe;
o que ele retorna;
qual outra parte do sistema chama esse código;
o que aconteceria caso aquele código fosse alterado.
```

A apresentação e a prova individual serão utilizadas para verificar esses conhecimentos.
