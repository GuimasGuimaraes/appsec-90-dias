# PortSwigger Lab — User ID controlled by request parameter

**Categoria:** Controle de acesso — IDOR/BOLA  
**Ambiente:** PortSwigger Web Security Academy (laboratório autorizado)  
**Status:** Solved

## Objetivo

Verificar se um usuário autenticado consegue acessar dados de outra conta ao alterar um identificador controlado pelo cliente.

## Procedimento e evidências

1. Autentiquei no laboratório com a conta de teste `wiener`.
2. Observei a requisição legítima:

   ```http
   GET /my-account?id=wiener
   ```

   Resultado: `200 OK`, com os dados da conta `wiener`.

3. Mantendo a mesma sessão, alterei o parâmetro para solicitar a conta de `carlos`:

   ```http
   GET /my-account?id=carlos
   ```

   Resultado: `200 OK`, com os dados da conta `carlos`.

4. O laboratório confirmou a conclusão com a mensagem **Solved**.

Não foram incluídos cookies, tokens, chaves de API ou URLs únicos da instância.

## Análise

A aplicação aceitou o identificador informado na URL e retornou os dados de outra conta sem aplicar uma verificação de autorização adequada. A identidade autenticada (`wiener`) não deveria, por si só, permitir acesso ao recurso pertencente a `carlos`.

Isso caracteriza uma falha de autorização no nível do objeto, conhecida como **IDOR** (*Insecure Direct Object Reference*) ou **BOLA** (*Broken Object Level Authorization*).

## Impacto

Em uma aplicação real, essa falha poderia permitir que usuários autenticados consultassem dados de outras pessoas, conforme os recursos e informações expostos pelo endpoint.

## Correção recomendada

- Obter a identidade do usuário a partir da sessão ou do token validado no servidor.
- Verificar no backend se essa identidade pode executar a ação sobre o objeto solicitado.
- Sempre que possível, restringir a busca ao usuário autorizado, em vez de buscar o objeto somente pelo ID recebido do cliente.
- Retornar uma resposta controlada sem incluir dados protegidos quando o acesso for negado.

## Testes de regressão

- A conta autenticada consegue acessar os próprios dados.
- Ao solicitar a conta de outro usuário, a aplicação bloqueia o acesso e não inclui dados protegidos no corpo da resposta.
- IDs inexistentes e acessos não autorizados são tratados de forma consistente com o contrato da API.

## Aprendizado

**Autenticação** responde “quem está fazendo a requisição?”. **Autorização** responde “essa pessoa pode acessar este objeto?”. A autorização precisa ser verificada no servidor para cada objeto solicitado; confiar no ID da URL não é suficiente.

## Referência

[PortSwigger Web Security Academy — User ID controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)
