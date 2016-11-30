# Formulários HTML

- 20 minutos

## Definição

- podemos usar o node/express para servir páginas de internet também
- a coisa mais legal se ter em uma página é conteúdo
- a segunda coisa mais legal é ter uma forma de coletar os dados do visitante
- apresentaremos o html com um enfoque nos formulários para coletar dados e enviar ao express

## Aplicação

- receber dados de modo mais civilizado que digitar manualmente parâmetros na url do navegador
- poderia dizer mais coisas, mas é tudo derivado disso aí em cima

## Exemplo

- 15 minutos

### Preparação

- faça fork do projeto
- pelo terminal, crie uma pastas chamada appweb
- dentro da pasta crie o projeto node

```bash
mkdir appweb
cd appweb
npm init -y
```

- instale nossas dependências usuais
- crie o **index.js**

```bash
npm install express knex --save
touch index.js
```

- nosso **index.js** tem o mesmo aspecto do que fizemos antes

```javascript
// index.js
const express = require("express");
const app = express();

app.get("/hello", (req,res) => res.send("hello"));

app.listen(3000);
console.log("app online");
```

- vamos fazer as alterações para que o express possa **servir** páginas html
- crie uma pasta chamada **public** dentro da pasta **appweb**
- crie o documento html dentro dela

```bash
mkdir public
touch public/index.html
```

- adicione ao express o suporte a pasta estática

```javascript
// index.js
const express = require("express");
const app = express();

app.use(express.static("public"));

app.get("/hello", (req,res) => res.send("hello"));

app.listen(3000);
console.log("app online");
```

- vamos adicionar um conteúdo básico no documento html

```html
<!DOCTYPE html>
<html>
<head>
  <title>App web</title>
</head>
<body>
  <h1>App web</h1>
  <p>O documento html é voltado para a publicação na internet</p>
</body>
</html>
```

- o html é uma linguagem de marcação, é o payload mais comum em requisições HTTP
- podemos criar um formulário e usá-lo para enviar dados ao express
- por padrão, se nenhum documento é solicitado abertamente, o servidor HTTP deve retornar o **index.html**

```html
<!DOCTYPE html>
<html>
<head>
  <title>App web</title>
</head>
<body>
  <h1>App web</h1>
  <p>O documento html é voltado para a publicação na internet</p>
  <form action="dosave" method="GET">
    <label>Nome</label><br/>
    <input name="nome"/><br/>
    <label>Endereço</label><br/>
    <input name="endereco"/><br/>
    <label>Telefone</label><br/>
    <input name="telefone"/><br/>
    <input type="submit"/>
  </form>
</body>
</html>
```

- form precisa ter **action** (para onde enviar os dados) e **mehod** (qual verbo usar, GET ou POST).
- só esses dois verbos HTTP estão disponíveis para formulários HTML
- o código express deve ser modificado para receber este formulário

```javascript
// index.js
const express = require("express");
const app = express();

app.use(express.static("public"));

app.get("/dosave", (req,res) => {
  console.log("os dados recebidos do formulário são:");
  console.log(req.query);
  res.send("<h1>Sucesso!</h1><a href='index.html'>voltar</a>");
});

app.listen(3000);
console.log("app online");
```

## Exercício

- submeta diferentes valores no formulário criado
- comite o código para o seu projeto no github

[Voltar](../README.md)
