# AppSec — 90 Dias

Este repositório documenta minha jornada intensiva de 90 dias de preparação para uma oportunidade profissional em Application Security (AppSec), com foco em segurança de aplicações web e APIs.

## Objetivos

- Dominar os fundamentos de segurança HTTP e APIs REST.
- Estudar OWASP Top 10 e OWASP API Security Top 10.
- Praticar testes de segurança em ambientes autorizados.
- Aprender a identificar, documentar e corrigir vulnerabilidades.
- Construir projetos práticos com Java, APIs e ferramentas de AppSec.

## Ferramentas

Burp Suite, Postman, Chrome DevTools, Java, Git e GitHub.

## Progresso

**Semana 1 — Fundamentos de segurança web**

- [x] Dia 1 — Fundamentos HTTP, headers, status e análise de APIs (simulado final: **8,6/10**) — [relatório técnico](semana-01/dia-01/relatorio-http.md)
- [ ] Dia 2 — Burp Suite e interceptação de requisições
- [x] Dia 3 — Requisições HTTP, autorização e laboratório PortSwigger de IDOR/BOLA — [relatório em inglês](reports/dia-03-broken-object-level-authorization.md)

### Aprendizados do Dia 1

- Inspeção de requisições e respostas HTTP no DevTools.
- Diferenciação entre método, URL, headers e corpo JSON.
- Distinção entre autenticação, autorização e CORS.
- Introdução a BOLA/IDOR e documentação de resultados sem afirmar vulnerabilidades não comprovadas.
- **Próximo ponto de melhoria:** reunir evidências suficientes para comprovar falhas de controle de acesso.

### Aprendizados do Dia 3

- Comparei o acesso legítimo à conta de teste `wiener` com uma requisição alterada para `carlos`.
- A aplicação retornou `200 OK` e os dados de outra conta na mesma sessão, confirmando a falha no laboratório.
- Reforcei que a autorização deve ser verificada no servidor para cada objeto solicitado.
- Registrei evidências, impacto, correção recomendada e testes de regressão no [relatório em inglês](reports/dia-03-broken-object-level-authorization.md).

## Laboratórios

Os exercícios são realizados em aplicações próprias, ambientes educacionais e sistemas com autorização explícita.

## Objetivo profissional

Transição de Analista de Sistemas/Sustentação para Analista de Segurança de Aplicações (AppSec).
