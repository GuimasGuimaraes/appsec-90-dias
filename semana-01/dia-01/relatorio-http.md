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

## 4. Análise de segurança

Foi observado que a API permite consultar diferentes recursos alterando o identificador na URL.

Esse comportamento não caracteriza, isoladamente, uma vulnerabilidade.

Para identificar uma possível falha BOLA/IDOR, seria necessário conhecer as regras de autorização da aplicação e verificar, em ambiente autorizado, se um usuário consegue acessar recursos de outros usuários sem permissão.

Como a API analisada é pública e destinada a demonstrações, os testes realizados não comprovam falha de autorização.

## 5. Conclusão

As requisições apresentaram comportamentos HTTP compatíveis com os resultados observados: códigos `200` para os recursos encontrados e `404` para o identificador inexistente.

**Vulnerabilidades confirmadas:** Nenhuma.

**Limitações:** Não foram realizados testes de autorização entre usuários com permissões distintas.

**Recomendação:** Em futuras análises, utilizar uma aplicação de laboratório com autenticação e regras de acesso definidas para avaliar possíveis falhas de autorização no nível do objeto.

