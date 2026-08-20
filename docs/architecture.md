# Arquitetura do Sistema

## Visão geral

O Clinic Workflow utiliza uma arquitetura de **Modular Monolith**, com o backend como núcleo da aplicação e o n8n atuando como camada de automação e orquestração.

A arquitetura foi escolhida para manter o MVP simples de desenvolver e operar, enquanto mantém separação clara entre responsabilidades e permite evolução futura.

```text
                        ┌──────────────┐
                        │   WhatsApp   │
                        └──────┬───────┘
                               │
                               ▼
                        ┌──────────────┐
                        │     n8n      │
                        │ Orquestração │
                        └──────┬───────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │       FastAPI       │
                    │   Modular Monolith  │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
          ▼                    ▼                    ▼
   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
   │ PostgreSQL  │      │     LLM     │      │ Integrações │
   │             │      │             │      │   externas  │
   └─────────────┘      └─────────────┘      └─────────────┘

                    ┌─────────────────────┐
                    │      Next.js        │
                    │       Frontend      │
                    └─────────────────────┘
```

## Componentes

### WhatsApp

Principal canal de comunicação com os pacientes.

É responsável pelo recebimento e envio das mensagens.

A integração inicialmente considerada é a Meta WhatsApp Cloud API, cuja decisão definitiva será validada posteriormente.

### n8n

Responsável pela orquestração de automações e integrações.

O n8n não deverá ser responsável pelas regras centrais do domínio.

Sua função principal será conectar eventos externos ao backend e executar fluxos de automação.

### Backend

O backend será desenvolvido utilizando FastAPI e será responsável por:

- regras de negócio;
- gerenciamento de conversas;
- processamento de mensagens;
- agendamentos;
- usuários e permissões;
- integração com IA;
- atendimento humano;
- métricas;
- auditoria;
- comunicação com serviços externos.

O backend será a fonte de verdade do sistema.

### PostgreSQL

Banco de dados principal da aplicação.

Será responsável pela persistência dos dados necessários para o funcionamento do sistema.

### LLM

A IA será utilizada principalmente para:

- classificação de intenção;
- interpretação de mensagens;
- extração de entidades e informações;
- geração de respostas quando apropriado.

O provedor de IA será abstraído para permitir substituição futura.

### Frontend

Aplicação web desenvolvida com Next.js.

Será utilizada pelas secretárias, médicas e administradores para:

- acompanhar conversas;
- assumir atendimentos;
- visualizar informações autorizadas;
- configurar o sistema;
- visualizar métricas;
- gerenciar usuários e permissões.

## Organização do Backend

O backend será organizado por módulos de negócio:

```text
app/
├── modules/
│   ├── auth/
│   ├── users/
│   ├── conversations/
│   ├── messaging/
│   ├── appointments/
│   ├── patients/
│   ├── ai/
│   ├── automation/
│   ├── metrics/
│   └── audit/
│
├── shared/
│   ├── database/
│   ├── config/
│   ├── exceptions/
│   └── logging/
│
└── main.py
```

Cada módulo deverá possuir responsabilidades bem definidas.

Quando necessário, os módulos poderão utilizar uma estrutura baseada em:

```text
module/
├── domain/
├── application/
├── infrastructure/
└── api/
```

## Fluxo de mensagens

O fluxo básico de uma mensagem será:

```text
Paciente
   ↓
WhatsApp
   ↓
n8n
   ↓
Backend
   ↓
Identificação da conversa
   ↓
Persistência da mensagem
   ↓
Processamento da intenção
   ↓
Execução do caso de uso
   ↓
Regra de negócio
   ↓
Resposta
   ↓
n8n
   ↓
WhatsApp
   ↓
Paciente
```

O backend poderá interromper o fluxo automatizado quando a conversa estiver sob atendimento humano.

## Atendimento humano

Quando uma secretária assumir uma conversa, o backend deverá registrar o estado da conversa como atendimento humano.

Enquanto esse estado estiver ativo, o fluxo automatizado não deverá interferir na conversa.

Quando o atendimento humano for finalizado ou devolvido ao fluxo automatizado, a conversa poderá retornar ao processamento automático.

## Princípios arquiteturais

### Backend como fonte de verdade

Regras de negócio devem permanecer no backend.

### n8n como orquestrador

O n8n deverá executar automações e integrações, evitando concentrar regras de negócio.

### IA como componente de interpretação

A IA interpreta linguagem natural, mas não deve controlar diretamente as regras do sistema.

### Baixo acoplamento

Os módulos deverão possuir responsabilidades claras e depender de contratos bem definidos.

### Segurança por padrão

O sistema deverá limitar o acesso a dados conforme a necessidade de cada componente e usuário.

### Evolução incremental

Novas tecnologias e componentes de infraestrutura somente deverão ser adicionados quando houver necessidade concreta.

### Modularidade antes de distribuição

O sistema deverá ser organizado para permitir evolução futura, mas não será distribuído em múltiplos serviços sem justificativa técnica.

## Decisões relacionadas

- ADR-001 — Stack Tecnológica
- ADR-002 — Arquitetura do Sistema
