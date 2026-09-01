# Clinic Workflow

> Plataforma de atendimento e automação de fluxos para clínicas, com o WhatsApp como principal canal de comunicação.

[Português](README.md) | [English](README.en.md)

---

## Sobre o projeto

**Clinic Workflow** é uma plataforma de atendimento automatizado para clínicas, criada para centralizar e organizar a comunicação entre pacientes, secretárias e profissionais.

O WhatsApp será utilizado como principal canal de atendimento, enquanto um painel web permitirá acompanhar conversas, assumir atendimentos humanos, configurar automações e visualizar métricas.

O projeto está sendo desenvolvido inicialmente como um **MVP**, mas sua arquitetura está sendo planejada para permitir evolução futura para um produto utilizado em ambientes reais.

Atualmente, os requisitos relacionados ao funcionamento de clínicas são considerados hipóteses de produto e ainda deverão ser validados antes de uma eventual utilização em produção.

---

## Objetivos

A plataforma deverá permitir:

* responder perguntas frequentes;
* interpretar mensagens em linguagem natural;
* conduzir fluxos determinísticos de atendimento;
* auxiliar em agendamentos;
* auxiliar em remarcações;
* auxiliar em cancelamentos;
* transferir conversas para atendimento humano;
* permitir que secretárias assumam conversas;
* enviar lembretes;
* coletar avaliações;
* acompanhar métricas de atendimento;
* registrar eventos relevantes para auditoria.

A IA será utilizada principalmente para **interpretar intenção e extrair informações das mensagens**.

As regras de negócio e operações críticas permanecerão sob responsabilidade do backend.

A IA **não deverá diagnosticar, prescrever medicamentos ou tomar decisões médicas**.

---

## Arquitetura

A arquitetura segue o princípio de manter as regras de negócio concentradas no backend.

O **n8n** será utilizado como camada de automação e orquestração, sem se tornar o núcleo da aplicação.

```text
WhatsApp
    │
    ▼
Webhook
    │
    ▼
n8n
    │
    ▼
Backend
 ├── PostgreSQL
 ├── LLM
 └── Agenda / Integrações
    │
    ▼
Frontend
```

A aplicação será inicialmente desenvolvida como um **monólito modular**, permitindo separar responsabilidades por domínio sem introduzir a complexidade operacional de microsserviços prematuramente.

---

## Stack tecnológica

### Frontend

* Next.js
* TypeScript
* Tailwind CSS
* shadcn/ui

### Backend

* Python
* FastAPI
* SQLAlchemy 2
* Alembic

### Banco de dados

* PostgreSQL

### Automação

* n8n

### Infraestrutura

* Docker
* Docker Compose

### CI/CD

* GitHub Actions

### Testes

* pytest
* Vitest
* Playwright posteriormente

### Inteligência Artificial

A integração com modelos de linguagem será realizada através de uma camada de abstração, evitando dependência direta de um único provedor.

---

## WhatsApp

A **Meta WhatsApp Cloud API** é atualmente a principal opção considerada para integração com o WhatsApp.

A decisão ainda deverá ser validada antes da implementação definitiva da integração.

---

## Atendimento humano

O bot deverá permitir que uma conversa seja transferida para uma secretária.

Quando uma secretária assumir o atendimento:

```text
Bot ativo
    │
    ▼
Transferência
    │
    ▼
Atendimento humano
    │
    ├── Secretária conduz a conversa
    │
    └── Bot permanece inativo
              │
              ▼
       Atendimento finalizado
              │
              ▼
       Bot pode ser reativado
```

O bot não deverá responder enquanto o atendimento estiver sob controle humano.

---

## Usuários e permissões

Inicialmente, o sistema deverá suportar pelo menos:

* Administrador
* Secretária
* Médica

A arquitetura deverá permitir expansão futura para múltiplos profissionais e especialidades.

As primeiras especialidades consideradas para o projeto são:

* Dermatologia
* Ginecologia

---

## Painel Web

O painel administrativo deverá permitir:

* acompanhar conversas;
* visualizar o estado de cada atendimento;
* assumir conversas;
* devolver conversas para automação;
* visualizar informações autorizadas;
* configurar informações utilizadas pelo bot;
* configurar automações;
* visualizar métricas;
* gerenciar usuários;
* gerenciar permissões.

---

## Segurança e privacidade

Como a plataforma poderá trabalhar com informações relacionadas a pacientes, segurança e privacidade são requisitos fundamentais desde o início do projeto.

O sistema deverá considerar:

* LGPD;
* autenticação;
* autorização;
* princípio do menor privilégio;
* separação de responsabilidades;
* logs;
* auditoria;
* proteção de dados sensíveis;
* controle de acesso aos dados.

O bot deverá receber apenas os dados necessários para executar sua função.

Informações médicas sensíveis não deverão ser disponibilizadas desnecessariamente ao modelo de IA.

---

## Estrutura do repositório

O projeto utiliza uma estrutura **monorepo**:

```text
clinic-workflow/
├── .github/
├── apps/
│   ├── backend/
│   └── frontend/
├── workflows/
├── docs/
│   ├── requirements.md
│   ├── architecture.md
│   ├── database.md
│   └── decisions/
├── docker/
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

### Diretórios principais

`apps/backend`

API, regras de negócio, persistência, autenticação e integrações da aplicação.

`apps/frontend`

Painel web utilizado pelos usuários internos da plataforma.

`workflows`

Workflows e automações executadas pelo n8n.

`docs`

Documentação técnica, requisitos, arquitetura, banco de dados e registros de decisões arquiteturais.

`docs/decisions`

Architecture Decision Records (ADRs) utilizados para documentar decisões importantes do projeto.

---

## Desenvolvimento

O desenvolvimento está sendo conduzido de maneira incremental.

Antes de implementar funcionalidades maiores, as principais decisões são analisadas e documentadas.

Fluxo utilizado:

```text
Analisar alternativas
        ↓
Comparar vantagens e desvantagens
        ↓
Tomar uma decisão
        ↓
Documentar
        ↓
Atualizar Issues
        ↓
Implementar
```

Tecnologias e infraestrutura adicionais não serão introduzidas sem uma necessidade concreta.

As principais prioridades são:

* simplicidade;
* manutenibilidade;
* segurança;
* baixo custo;
* escalabilidade;
* qualidade arquitetural.

---

## Status atual

O projeto encontra-se na fase de definição da fundação técnica do sistema.

| Etapa                         | Status       |
| ----------------------------- | ------------ |
| Stack tecnológica             | Concluída    |
| Arquitetura do sistema        | Concluída    |
| Modelagem do banco de dados   | Em andamento |
| Fluxos de atendimento         | Pendente     |
| Estrutura inicial do monorepo | Pendente     |
| Implementação do backend      | Pendente     |
| Implementação do frontend     | Pendente     |
| Integração com WhatsApp       | Pendente     |
| MVP                           | Pendente     |

O foco atual está na **modelagem do banco de dados e definição das entidades e relacionamentos do sistema**.

---

## Roadmap

### Fundação

* [x] Definir stack tecnológica
* [x] Definir arquitetura do sistema
* [ ] Modelar banco de dados
* [ ] Definir fluxos do atendimento

### Estrutura inicial

* [ ] Criar estrutura inicial do monorepo
* [ ] Configurar ambiente Docker
* [ ] Configurar PostgreSQL
* [ ] Inicializar backend
* [ ] Inicializar frontend

### Core da aplicação

* [ ] Configurar autenticação e autorização
* [ ] Implementar modelo de conversas
* [ ] Implementar recebimento de mensagens
* [ ] Implementar envio de mensagens
* [ ] Implementar máquina de estados da conversa
* [ ] Implementar classificação de intenção
* [ ] Implementar fluxos do bot
* [ ] Implementar transferência para atendimento humano

### Painel

* [ ] Interface de conversas
* [ ] Interface de atendimento humano
* [ ] Dashboard
* [ ] Interface de configuração de FAQ
* [ ] Configuração de automações

### Automação e métricas

* [ ] Implementar lembretes
* [ ] Implementar avaliações
* [ ] Implementar métricas
* [ ] Implementar logs e auditoria

### Qualidade e entrega

* [ ] Testes
* [ ] CI/CD
* [ ] Configurar ambiente de produção
* [ ] Documentação
* [ ] Preparar MVP para demonstração

---

## Decisões arquiteturais

Decisões relevantes são documentadas utilizando **Architecture Decision Records (ADR)**.

Exemplos:

```text
docs/decisions/
├── ADR-001-stack-tecnologica.md
└── ADR-002-arquitetura.md
```

Esse processo ajuda a registrar não apenas **qual decisão foi tomada**, mas também **por que ela foi tomada** e quais alternativas foram consideradas.

---

## Branches

O projeto utiliza a branch:

```text
main
```

Branches de desenvolvimento seguem os padrões:

```text
feature/*
fix/*
refactor/*
docs/*
```

Exemplos:

```text
feature/whatsapp-integration
feature/authentication
fix/duplicate-messages
refactor/auth-service
docs/update-architecture
```

---

## Commits

Os commits seguem a especificação **Conventional Commits**:

```text
feat:
fix:
docs:
refactor:
test:
chore:
ci:
build:
```

Exemplo:

```text
feat: add conversation state model
```

---

## Gestão do projeto

O desenvolvimento é acompanhado através de GitHub Issues e GitHub Projects.

Fluxo Kanban utilizado:

```text
Backlog
   ↓
Todo
   ↓
In Progress
   ↓
Review
   ↓
Done
```

---

## Estado do projeto

Este projeto está atualmente em desenvolvimento.

Funcionalidades, integrações e decisões arquiteturais podem ser alteradas à medida que novos requisitos forem validados.

---
