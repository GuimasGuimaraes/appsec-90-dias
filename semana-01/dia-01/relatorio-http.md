# Relatório Técnico 001 — Análise de Requisições HTTP

**Aplicação:** JSONPlaceholder  
**Tipo de teste:** Análise introdutória de comportamento HTTP  
**Método utilizado:** GET  
**Ferramenta:** Chrome DevTools — Network

## 1. Objetivo

Analisar as requisições HTTP de uma API pública, identificando os códigos de resposta, os dados retornados e o comportamento da aplicação ao consultar diferentes identificadores.

## 2. Endpoints analisados

URL base: `https://jsonplaceholder.typicode.com`

| Endpoint | Método | Status observado |
|---|---|---|
| `/todos/1` | GET | 200 OK |
| `/todos/2` | GET | 200 OK |
| `/todos/999999` | GET | 404 Not Found |

Os resultados foram registrados durante os exercícios práticos.

## 3. Dados retornados

A requisição `GET /todos/1` retornou:

```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

Foram identificados os campos `userId`, `id`, `title` e `completed`.

## 4. Headers observados

Durante a inspeção no DevTools, foram identificados os seguintes exemplos de cabeçalhos HTTP.

**Request Headers (enviados pelo navegador):**

- `Accept`: apresentou formatos aceitos como `text/html`, `application/xhtml+xml`, `application/xml;q=0.9` e `*/*;q=0.8`.
- `Cache-Control: no-cache`: solicita que uma resposta armazenada seja revalidada antes do uso.

**Response Headers (retornados pelo servidor):**

- `Content-Type: application/json; charset=utf-8`: identifica o corpo da resposta como JSON em UTF-8.
- `Date: Tue, 13 Oct 2026 19:24:31 GMT`: data e hora informadas no cabeçalho da resposta.
- `Access-Control-Allow-Credentials: true`: header de CORS observado na etapa anterior; **não significa** que a API tenha autenticado ou autorizado o cliente.

O JSON da seção 3 é o **corpo da resposta (Response Body)**, e não um Response Header. A presença de um header CORS não comprova uma vulnerabilidade.

## 5. Análise de segurança

Foi observado que a API permite consultar diferentes recursos alterando o identificador na URL.

Esse comportamento não caracteriza, isoladamente, uma vulnerabilidade.

Para identificar uma possível falha BOLA/IDOR, seria necessário conhecer as regras de autorização da aplicação e verificar, em ambiente autorizado, se um usuário consegue acessar recursos de outros usuários sem permissão.

Como a API analisada é pública e destinada a demonstrações, os testes realizados não comprovam falha de autorização.

## 6. Conclusão

As requisições apresentaram comportamentos HTTP compatíveis com os resultados observados: códigos `200` para os recursos encontrados e `404` para o identificador inexistente.

**Vulnerabilidades confirmadas:** Nenhuma.

**Limitações:** Não foram realizados testes de autorização entre usuários com permissões distintas.

**Recomendação:** Em futuras análises, utilizar uma aplicação de laboratório com autenticação e regras de acesso definidas para avaliar possíveis falhas de autorização no nível do objeto.

