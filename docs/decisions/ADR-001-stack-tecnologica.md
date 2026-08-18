# ADR-001 — Stack tecnológica

## Status

Accepted

## Contexto

O Clinic Workflow será uma plataforma de atendimento para clínicas,
com integração com WhatsApp, automações via n8n, processamento de
linguagem natural, painel web e banco de dados relacional.

O MVP possui como objetivo entregar uma primeira versão funcional
em aproximadamente um mês, mantendo uma arquitetura preparada
para evolução futura.

## Decisão

A stack inicial será:

- Frontend: Next.js + TypeScript
- UI: Tailwind CSS + shadcn/ui
- Backend: FastAPI + Python
- ORM: SQLAlchemy 2
- Migrations: Alembic
- Database: PostgreSQL
- Automação: n8n
- Containers: Docker
- CI/CD: GitHub Actions
- Testes backend: pytest
- Testes frontend: Vitest
- E2E: Playwright, posteriormente

A integração com WhatsApp será inicialmente planejada para a
Meta WhatsApp Cloud API, mas essa decisão ainda depende de
validação técnica e comercial.

A integração com LLM será realizada através de uma camada de
abstração, permitindo alterar o provedor futuramente.

## Motivações

### FastAPI

- API-first
- Baixa complexidade inicial
- Excelente integração com Python
- Bom suporte a aplicações assíncronas
- Boa integração com soluções de IA
- Familiaridade do desenvolvedor com a tecnologia

### Next.js

- Ecossistema React
- TypeScript
- Bom suporte para aplicações web modernas
- Adequado para construção do painel administrativo

### PostgreSQL

- Banco relacional robusto
- Excelente suporte a relacionamentos
- Transações
- Escalabilidade
- Open source

### n8n

Será utilizado como camada de automação e orquestração,
não como responsável pelas regras centrais de negócio.

## Alternativas consideradas

### Django

Foi considerado para o backend devido ao seu ecossistema,
autenticação e Django Admin.

Foi descartado para o MVP porque o sistema possui uma abordagem
mais orientada a API e integrações, e o painel administrativo
será desenvolvido separadamente em Next.js.

### MongoDB

Foi considerado, mas PostgreSQL foi escolhido devido à natureza
relacional do domínio.

### Redis

Não será utilizado inicialmente. Poderá ser introduzido
posteriormente caso surjam necessidades de cache, filas,
rate limiting ou estado temporário.

## Consequências

### Positivas

- Stack relativamente simples
- Boa separação entre frontend e backend
- Facilidade para integração com IA
- Baixo custo inicial
- Arquitetura preparada para evolução

### Negativas

- Autenticação e autorização precisarão ser implementadas
  no backend
- Algumas funcionalidades disponíveis nativamente no Django
  precisarão ser construídas
- Mais componentes precisam ser gerenciados separadamente

## Status da decisão

Aceita para o MVP.

A escolha do provedor de WhatsApp permanece pendente de
validação.
