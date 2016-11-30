# Introdução ao body-parser

- 40 minutos

- cada verbo HTTP tem características [documentadas](http://stackoverflow.com/questions/165779/are-the-put-delete-head-etc-methods-available-in-most-web-browsers)
- o GET e o DELETE, por exemplo, não tem corpo
- já o POST tem

```html
POST /dosave HTTP/1.1
Host: localhost:3000
Connection: keep-alive
(... removido por questão de legibilidade ...)
Cookie: io=SQH1r7gh1p2QHq-mAAAF

nome=maria&endereco=rua+2&telefone=12345
```

- a primeira parte é o que chamamos de **HTTP HEADER**
- a primeira linha é o verbo, a uri e a versão do protocolo
- o header é separado do corpo por uma linha em branco (**\r\n\r\n**)
- o problema é que o express delega para plugins resolver o corpo dos métodos, quando tem. 
- o plugin para isso é o **body-parser**

## Definição

- plugin do express
- suporte a corpo das requisições **(req.body)**

## Aplicação

- garantir que middlewares express que precisem tratar o corpo da requisição 

## Exemplo

- primeiro instale o plugin 

```bash
npm install body-parser --save
```

- agora altere o index.js para ficar de acordo

```javascript
// index.js
const express    = require("express");
const bodyParser = require("body-parser");
const app        = express();

app.use(express.static("public"));

app.use(bodyParser.urlencoded({extended:true}));

app.post("/dosave", (req,res) => {
  console.log("os dados recebidos do formulário são:");
  console.log(req.body);
  res.send("<h1>Sucesso!</h1><a href='index.html'>voltar</a>");
});

app.listen(3000);
console.log("app online");
```

- nossos dados estarão no *body* da requisição a partir de agora
- altere também o formulário para usar o POST

```html
<!DOCTYPE html>
<html>
<head>
  <title>App web</title>
</head>
<body>
  <h1>App web</h1>
  <p>O documento html é voltado para a publicação na internet</p>
  <form action="dosave" method="POST">
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

- *por que usar outros verbos além do GET? Já funcionava sem iso de POST!*
  - o GET tem limitação de ter apenas o cabeçalho, que é limitado a 512kb de tamanho
  - os verbos do HTTP foram adicionados ao protocolo para dar **semântica** à conexão
  - as respostas todas podem ter corpo
  - é útil ter um corpo na requisição, podemos mandar informação relevante lá   

## Exercício

- comite os exemplos para o github
- crie um documento html chamado **numero.html**
- deve ser parecido com o index.html, mas deve ter apenas um input
- o name do input deve ser **"numero"** (i.e. ```<input name="numero"/>```)
- o formulário deve usar **POST** e action deve ser **"adivinha"**. baseie-se pelo formulário do index.html
- no express, crie uma rota do tipo post para receber os dados deste formulário.
- devemos imprimir o **req.body**, conforme exemplo anterior
- o action deve oferecer um link para voltar para o documento numero.html
- lembre-se: documentos html e tudo mais que for ser consumido no lado do cliente fica dentro de **public**
- não deixe de comitar este novo exercício!

[Voltar](../README.md)
