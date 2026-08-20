# ADR-002 — Arquitetura do Sistema

- **Status:** Aceito
- **Data:** 19/08/2026
- **Decisão:** Modular Monolith com princípios de Hexagonal Architecture
- **Issue:** #2 — Definir arquitetura do sistema

## Contexto

O Clinic Workflow será uma plataforma de atendimento automatizado para clínicas, utilizando o WhatsApp como principal canal de comunicação.

O sistema deverá integrar atendimento automatizado, inteligência artificial, agendamento, atendimento humano, métricas, autenticação e integrações externas.

Como o projeto está em fase de MVP, a arquitetura deve priorizar simplicidade, baixo custo e velocidade de desenvolvimento, sem comprometer a possibilidade de evolução futura.

Também foi definido que o backend será responsável pelas regras de negócio, enquanto o n8n será utilizado como camada de automação e orquestração.

## Alternativas consideradas

### Monólito tradicional

Uma única aplicação contendo todas as funcionalidades, organizada principalmente por camadas técnicas.

**Vantagens:**

- Simplicidade de desenvolvimento;
- Baixo custo operacional;
- Fácil execução e deploy;
- Adequado para o tamanho inicial do projeto.

**Desvantagens:**

- Pode gerar alto acoplamento entre funcionalidades;
- Fronteiras entre módulos podem se tornar pouco claras;
- Dificulta a evolução independente das partes do sistema.

### Modular Monolith

Uma única aplicação e um único deploy, porém organizada em módulos independentes por responsabilidade de negócio.

**Vantagens:**

- Mantém a simplicidade de um monólito;
- Reduz o acoplamento entre funcionalidades;
- Facilita manutenção e testes;
- Permite estabelecer limites claros entre domínios;
- Possibilita futura extração de módulos caso exista necessidade real.

**Desvantagens:**

- Exige disciplina para manter as fronteiras entre módulos;
- Continua compartilhando o mesmo processo e infraestrutura;
- Não possui o isolamento operacional de microsserviços.

### Microsserviços

Separação das funcionalidades em aplicações independentes.

**Vantagens:**

- Deploy independente;
- Escalabilidade independente;
- Isolamento entre serviços;
- Adequado para sistemas de maior escala e complexidade.

**Desvantagens:**

- Maior complexidade operacional;
- Mais infraestrutura;
- Comunicação distribuída;
- Maior dificuldade de desenvolvimento e debugging;
- Complexidade desnecessária para o MVP.

## Decisão

O Clinic Workflow será desenvolvido inicialmente como um **Modular Monolith**.

O backend será uma única aplicação FastAPI, responsável pelas regras de negócio e pelo estado do sistema.

Internamente, a aplicação será dividida em módulos relacionados às principais responsabilidades do domínio.

Cada módulo deverá possuir responsabilidades bem definidas e baixo acoplamento com os demais.

A organização interna utilizará princípios de **Hexagonal Architecture (Ports & Adapters)**, especialmente para separar regras de negócio de frameworks, banco de dados e integrações externas.

A arquitetura não será uma implementação rígida ou dogmática de Clean Architecture. As abstrações deverão ser utilizadas quando trouxerem benefício real ao projeto.

## Módulos iniciais

Os principais módulos previstos são:

- `auth` — autenticação e controle de acesso;
- `users` — gerenciamento de usuários e perfis;
- `conversations` — gerenciamento das conversas e seus estados;
- `messaging` — recebimento e envio de mensagens;
- `appointments` — agendamento, remarcação e cancelamento;
- `patients` — dados necessários dos pacientes;
- `ai` — integração e abstração dos provedores de IA;
- `automation` — automações e integração com o n8n;
- `metrics` — métricas do atendimento;
- `audit` — logs e auditoria.

Os módulos poderão ser revisados conforme os requisitos forem validados.

## Responsabilidade do backend

O backend será a fonte de verdade das regras de negócio.

O n8n não deverá implementar regras essenciais do domínio.

Por exemplo, decisões como disponibilidade para agendamento, regras de cancelamento, estado de uma conversa e transferência para atendimento humano deverão ser determinadas pelo backend.

O n8n será responsável principalmente pela orquestração de eventos e integrações externas.

## Responsabilidade da IA

A inteligência artificial será utilizada principalmente para interpretação de linguagem natural, classificação de intenção e extração de informações.

A IA não será responsável por executar diretamente regras de negócio.

O fluxo esperado é:

```text
Mensagem do paciente
        ↓
Interpretação pela IA
        ↓
Intenção + dados estruturados
        ↓
Caso de uso do backend
        ↓
Regras de negócio
        ↓
Resultado
```

Essa separação reduz a dependência do comportamento probabilístico do modelo e mantém as regras críticas sob controle determinístico do backend.

## Evolução futura

A arquitetura deverá permitir que um módulo seja posteriormente extraído para um serviço independente caso exista uma necessidade concreta de:

- escalabilidade independente;
- isolamento operacional;
- deploy independente;
- requisitos específicos de infraestrutura;
- crescimento significativo de determinada funcionalidade.

Entretanto, microsserviços não serão introduzidos antecipadamente.

O princípio adotado é:

> **Projetar para modularidade, não para distribuição.**

## Consequências

### Positivas

- Menor complexidade inicial;
- Desenvolvimento mais rápido;
- Menor custo de infraestrutura;
- Facilidade de desenvolvimento e debugging;
- Separação clara das responsabilidades;
- Possibilidade de evolução futura.

### Negativas

- Todos os módulos continuam compartilhando a mesma aplicação;
- Mudanças podem afetar diferentes módulos;
- Será necessário manter disciplina arquitetural;
- A extração futura de módulos exigirá trabalho adicional.

## Resultado esperado

A arquitetura escolhida deverá permitir que o MVP seja desenvolvido de forma simples e sustentável, mantendo uma estrutura suficientemente organizada para suportar a evolução do Clinic Workflow para uma solução de produção e, futuramente, para um produto comercial.
