# 🌐 HTTP

O **módulo HTTP** do Node.js permite a criação de servidores web e clientes HTTP de forma simples e eficiente.

## 🚀 Criando um Servidor HTTP

Para criar um servidor básico que responde "Olá, mundo!" em qualquer requisição:

```js
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Olá, mundo!');
});

server.listen(3000, () => {
    console.log('Servidor rodando em http://localhost:3000');
});
````

📌 O servidor escuta na porta **3000** e responde a todas as requisições com "Olá, mundo!".

💡Para visualizar o servidor abre ele como **localhost:3000** ou se preferir use **curl** para visualizar no console. Você pode usar o [**HTTPie**](https://httpie.io/) para melhor formatação

## 🛤️ Criando Rotas no Servidor HTTP

Podemos criar diferentes respostas para URLs específicas:

```js
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });

    if (req.url === '/') {
        res.end(JSON.stringify({ mensagem: 'Bem-vindo ao servidor!' }));
    } else if (req.url === '/sobre') {
        res.end(JSON.stringify({ mensagem: 'Esta é a página sobre.' }));
    } else {
        res.writeHead(404, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ erro: 'Página não encontrada' }));
    }
});

server.listen(3000, () => {
    console.log('Servidor rodando em http://localhost:3000');
});
```

🔹 Se acessar http://localhost:3000/, retorna:

```json
{ "mensagem": "Bem-vindo ao servidor!" }
```

🔹 Se acessar http://localhost:3000/sobre, retorna:

```json
{ "mensagem": "Esta é a página sobre." }
```

🔹 Qualquer outra rota retorna um erro 404.

---

## 📡 Fazendo Requisições HTTP

O módulo HTTP também permite enviar requisições para outros servidores.

### 🔹 Requisição GET (Buscar dados):

```js
const http = require('http');

const server = http.createServer((request, response) => {
    const {method, url} = request

    if (method === 'GET' && url === '/users') {
        return response.end('Listagem de usuários')
    }
})

server.listen(3333)
```

📌 Faz uma **requisição GET** para `localhost:3333/users` e exibe a resposta no console.

### 🔹 Requisição POST (Enviar dados)

```js
const http = require('http');

const server = http.createServer((request, response) => {
    const {method, url} = request

    if (method === 'POST' && url === '/users') {
        return response.end('Criação de usuário')
    }
})

server.listen(3333)
```

📌 Envia uma **requisição POST** com um JSON para `localhost:3333/users`.


📌 **Os mais usados em APIs REST:**
- **`GET`** → Buscar dados  
- **`POST`** → Criar novos recursos  
- **`PUT` / `PATCH`** → Atualizar recursos  
- **`DELETE`** → Remover recursos  


💡 **Dica:** Use `POST` para criar e `PUT` para substituir um recurso inteiro. Use `PATCH` quando for atualizar **apenas parte** do recurso.  

---

## 🔍 Métodos Úteis
---

## 📜 Métodos e Propriedades do HTTP

### 🔹 `req` (Request - Requisição)

O objeto `req` contém informações sobre a requisição do cliente, como **URL, método e cabeçalhos**.

| 🛠️ Propriedade / Método  | 📜 Descrição |
|--------------------------|-------------|
| `req.method`            | Retorna o método HTTP (`GET`, `POST`, etc.). |
| `req.url`               | Retorna a URL requisitada pelo cliente. |
| `req.headers`           | Retorna um objeto com os cabeçalhos da requisição. |
| `req.rawHeaders`        | Retorna os cabeçalhos em um array (pares chave-valor). |
| `req.httpVersion`       | Indica a versão do HTTP usada (`1.1`, `2.0`, etc.). |
| `req.socket`            | Retorna o **socket** associado à requisição. |
| `req.connection`        | Similar ao `req.socket`, mas considerado obsoleto. |
| `req.getHeader(name)`   | Obtém um cabeçalho específico da requisição. |
| `req.setTimeout(ms, cb)`| Define um timeout para a requisição. |
| `req.on('data', cb)`    | Lê os dados do corpo da requisição (para `POST`, `PUT`). |
| `req.on('end', cb)`     | Indica o fim da transmissão de dados da requisição. |

---

### 🔹 `res` (Response - Resposta)

O objeto `res` permite enviar uma resposta ao cliente, incluindo **status, cabeçalhos e corpo da resposta**.

| 🛠️ Método / Propriedade  | 📜 Descrição |
|-------------------------|-------------|
| `res.writeHead(status, headers)` | Define o status e os cabeçalhos da resposta. |
| `res.setHeader(name, value)` | Define um cabeçalho específico na resposta. |
| `res.getHeader(name)` | Retorna o valor de um cabeçalho definido. |
| `res.removeHeader(name)` | Remove um cabeçalho da resposta. |
| `res.write(chunk)` | Escreve um pedaço de dados no corpo da resposta. |
| `res.end([data])` | Finaliza a resposta e pode enviar dados finais. |
| `res.statusCode` | Define ou retorna o código de status da resposta. |
| `res.statusMessage` | Define ou retorna a mensagem de status (ex: `"OK"`). |
| `res.headersSent` | Retorna `true` se os cabeçalhos já foram enviados. |
| `res.writeContinue()` | Envia um status `100 Continue` para o cliente. |
| `res.setTimeout(ms, cb)` | Define um timeout para a resposta. |

---

## 🚀 **Dicas Rápidas**
> 💡 **`req.on('data', cb)`** é essencial para capturar o corpo da requisição (`POST`, `PUT`).  
> 🛠️ **Sempre finalize** a resposta com `res.end()`, ou a conexão pode ficar aberta.  
> 🔄 **Use `res.writeHead(200, { 'Content-Type': 'text/html' })`** para definir status e cabeçalhos antes de enviar uma resposta.  

---



---

## 🎯 Conclusão

O módulo **HTTP** é a base para construir servidores e APIs no Node.js. Para projetos mais complexos, frameworks como **Express.js** podem ser utilizados para facilitar o desenvolvimento.

✅ Criar servidores HTTP  
✅ Manipular rotas e URLs  
✅ Enviar requisições HTTP  
✅ Construir APIs básicas

💡 **Dica:** Se precisar de mais controle sobre requisições e respostas, combine o módulo HTTP com **streams** e **eventos** do Node.js!

