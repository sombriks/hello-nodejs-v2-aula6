# Requisição via javascript

- formulário é bacana, *mas*
- mas é muito "anos 90"
- subentende a completa perda do documento (eu 'naveguei' de um canto para outro)
- entra o [XMLHTTPRequest](https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHttpRequest)

## Definição

- aplicativos modernos fazem muitas requisições a partir do javascrit e não do html (forms)
- a vantagem é não perder o **estado** atual do aplicativo

## Aplicação

- aplicações modernas para a internet
- comunicação em tempo real ou quase real
- troca de mensagens de alto nível entre cliente e servidor

## Exemplo

- modifique o index.js e adicione a rota **convidados**, um get simples
- ative também o modo json do bodyParser

```javascript
// index.js
const express    = require("express");
const bodyParser = require("body-parser");
const app        = express();
app.use(express.static("public"));
app.use(bodyParser.urlencoded({extended:true}));
app.use(bodyParser.json());
app.post("/dosave", (req,res) => {
  console.log("os dados recebidos do formulário são:");
  console.log(req.body);
  res.send("<h1>Sucesso!</h1><a href='index.html'>voltar</a>");
});
app.post("/adivinha", (req,res) => {
  if(req.body && req.body.numero == 7)
    res.send("<h1>Acertou!</h1><a href='numero.html'>voltar</a>");
  else
    res.send("<h1>Errou!</h1><a href='numero.html'>voltar</a>");
});
app.get("/convidados", (req,res) => {
  var convs = [{nomeconvidado:"Maria"},{nomeconvidado:"João"}];
  res.send(convs);
});
app.listen(3000);
console.log("app online");
```

- prepare um novo documento html chamado **moderno.html**. Ele deve ser salvo dentro da pasta **public**

```html
<!DOCTYPE html>
<!-- moderno.html -->
<html>
<head>
  <title>App web moderno</title>
  <script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
</head>
<body>
  <h1>App web moderno</h1>
  <button id="solicita">Solicitar convidados</button>
  <div id="ret"></div>
  <script>
    $("#solicita").click( () => {
      $.getJSON( "convidados", ( data ) => {
        $.map(data, (e) => {
          $("#ret").append($("<p>").text(e.nomeconvidado));
        });
      });
    });
  </script>
</body>
</html>
```

- os dados são recebidos pelo javascript e no javascript processados
- em vez de darmos forma à resposta no lado do servidor, deixamos esse trabalho para o cliente
- o [jQery](http://jquery.com/) (estrelando o bloco de script acima) foi a primeira forma decente de fazer esse tipo de operação
- atualmente temos [dezenas](https://en.wikipedia.org/wiki/List_of_Ajax_frameworks#JavaScript) de bibliotecas que fazem trabalho similar
- o exemplo abaixo mostra o mesmo resultado com outra biblioteca (mais) moderna

```html
<!DOCTYPE html>
<!-- moderno2.html -->
<html>
<head>
  <title>App web moderno</title>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>
<body>
  <h1>App web moderno</h1>
  <button id="solicita" onclick="dosol()">Solicitar convidados</button>
  <div id="ret"></div>
  <script>
    function dosol(){
      var ret = document.getElementById("ret");
      axios.get("convidados").then((res) => {
        res.data.map( (e) => ret.innerHTML += `<p>${e.nomeconvidado}</p>`);
      });
    }
  </script>
</body>
</html>
```

- o [axios](https://github.com/mzabriskie/axios#example) tem uma api baseada em promessas, que nem o knex
- similar à api fetch que virá nos navegadores do futuro
- para trocar o jQuery pelo axios foi preciso mudar **zero linhas** do lado do servidor

## Exercício

- comitar os exercícios mostrados até agora
- estudar os verbos HTTP

[Voltar](../README.md)
