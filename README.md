# Criação de Lead com Crawler — Testes de API

Testes automatizados (Postman/Newman) da API de criação de leads via Crawler.

## Dashboard

[Ver dashboard de qualidade](https://websupply.github.io/CONNECTCRAWLERQA/)

O dashboard mostra a taxa de sucesso, resultado por requisição, detalhamento de falhas e histórico das últimas execuções.

## Como funciona a pipeline

- Roda automaticamente toda segunda-feira às 08:00 (horário de Brasília).
- Também roda a cada `push`/`pull request` na branch principal.
- Pode ser disparada manualmente em Actions → **Run Postman API Tests - Crawler** → Run workflow.
- Se algum teste falhar, um e-mail de alerta é enviado automaticamente para os destinatários configurados.
- O dashboard é publicado automaticamente no GitHub Pages a cada execução.

## Estrutura

```
.
├── .github/workflows/          # Workflow do GitHub Actions
├── scripts/
│   ├── generate-dashboard.js   # Gera o dashboard HTML
│   └── email-report.js         # Gera o e-mail de alerta
├── [QA] Testes - Crawler.postman_collection.json
└── package.json
```

## Rodando localmente

```
npm install
npx newman run "[QA] Testes - Crawler.postman_collection.json" --env-var "x-api-key=SUA_CHAVE"
```

## Secrets necessários (GitHub Actions)

| Secret | Descrição |
|---|---|
| `MAIL_USERNAME` | Conta Gmail usada para enviar os alertas |
| `MAIL_PASSWORD` | Senha de app do Gmail |
| `MAIL_TO` | E-mail(s) de destino dos alertas (separados por vírgula) |
| `CRAWLER_API_KEY` | Chave de API usada nos testes (header `x-api-key`) |
