# Especificação Inicial — Plataforma de Atendimento para Clínica

**Versão:** 0.1
**Status:** Levantamento inicial de requisitos
**Objetivo:** Definir o escopo inicial de uma plataforma de atendimento automatizado via WhatsApp, com painel administrativo para gestão das conversas, automações e métricas da clínica.

---

## 1. Visão geral

O projeto consiste no desenvolvimento de uma plataforma de atendimento para uma clínica com atuação nas áreas de Dermatologia e Ginecologia.

A plataforma terá o WhatsApp como principal canal de comunicação com os pacientes, utilizando automações e inteligência artificial de forma controlada para interpretar solicitações, direcionar fluxos e responder dúvidas frequentes.

Além do atendimento automatizado, o sistema contará com um painel web para que as secretárias e demais usuários autorizados possam acompanhar e assumir conversas, configurar informações e visualizar métricas.

O sistema será desenvolvido inicialmente para a clínica atual, mas sua arquitetura deverá permitir evolução para novas especialidades, profissionais, unidades e funcionalidades.

---

# 2. Objetivos

## 2.1 Objetivo principal

Reduzir o trabalho manual das secretárias em atividades repetitivas de atendimento, mantendo a possibilidade de intervenção humana sempre que necessário.

## 2.2 Objetivos específicos

- Automatizar dúvidas frequentes dos pacientes.
- Auxiliar no processo de agendamento, remarcação e cancelamento.
- Encaminhar situações não resolvidas para uma secretária.
- Permitir que uma secretária assuma uma conversa manualmente.
- Enviar lembretes automáticos de consultas.
- Coletar avaliações dos pacientes.
- Disponibilizar métricas sobre o atendimento.
- Centralizar o gerenciamento do atendimento em um painel web.
- Manter separação adequada entre informações operacionais e informações sensíveis.
- Criar uma arquitetura preparada para futuras expansões.

---

# 3. Escopo inicial

O MVP deverá contemplar:

- Integração com WhatsApp.
- Recebimento e envio de mensagens.
- Fluxos automatizados de atendimento.
- Identificação de intenções do paciente.
- Respostas para perguntas frequentes.
- Agendamento ou coleta de informações para agendamento.
- Remarcação.
- Cancelamento.
- Encaminhamento para atendimento humano.
- Painel web de atendimento.
- Autenticação.
- Controle de permissões.
- Cadastro básico de informações da clínica.
- Lembretes configuráveis.
- Coleta de avaliações.
- Dashboard básico de métricas.
- Registro de eventos e erros.

Funcionalidades como estoque, financeiro, prontuário, prescrição e gestão completa de pacientes ficam fora do MVP.

---

# 4. Stakeholders

## 4.1 Clínica

Responsável pela utilização e validação do sistema.

## 4.2 Secretárias

Usuárias responsáveis pelo atendimento humano e gerenciamento das conversas.

## 4.3 Médicas

Usuárias com acesso a informações e funcionalidades pertinentes às suas atividades.

## 4.4 Administrador

Responsável pela configuração geral da plataforma e gerenciamento dos usuários.

## 4.5 Pacientes

Usuários externos que utilizarão o WhatsApp para interagir com a clínica.

## 4.6 Equipe de desenvolvimento

Responsável pela implementação, manutenção e evolução da plataforma.

---

# 5. Usuários e permissões

O sistema deverá possuir, inicialmente, três níveis de acesso.

## 5.1 Administrador

Poderá:

- Gerenciar usuários.
- Gerenciar permissões.
- Configurar informações da clínica.
- Configurar automações.
- Visualizar conversas.
- Assumir conversas.
- Visualizar métricas.
- Gerenciar configurações do sistema.

## 5.2 Secretária

Poderá:

- Visualizar conversas.
- Assumir conversas.
- Enviar mensagens.
- Encerrar atendimentos.
- Consultar informações necessárias ao atendimento.
- Visualizar agenda, caso integrada.
- Consultar avaliações.

Não deverá possuir acesso às configurações administrativas críticas.

## 5.3 Médica

Poderá:

- Visualizar informações pertinentes aos seus atendimentos.
- Consultar sua agenda.
- Visualizar métricas autorizadas.
- Consultar informações necessárias para suas atividades.

O modelo deverá permitir futuramente restringir o acesso por profissional e especialidade.

---

# 6. Requisitos funcionais

## RF01 — Receber mensagens

O sistema deverá receber mensagens enviadas pelos pacientes através do WhatsApp.

## RF02 — Enviar mensagens

O sistema deverá enviar respostas automáticas e mensagens iniciadas pelo atendimento humano.

## RF03 — Identificar intenção

O sistema deverá identificar a intenção principal de uma mensagem recebida.

Exemplos:

- AGENDAMENTO
- REMARCACAO
- CANCELAMENTO
- INFORMACAO
- ATENDENTE
- AVALIACAO

## RF04 — Atendimento por fluxo

O sistema deverá conduzir o paciente por fluxos previamente definidos.

## RF05 — FAQ

O sistema deverá responder perguntas frequentes utilizando informações previamente cadastradas pela clínica.

## RF06 — Atendimento em linguagem natural

O sistema deverá permitir que o paciente utilize linguagem natural para solicitar serviços.

Exemplo:

> "Queria marcar uma consulta de ginecologia para sexta-feira."

A mensagem deverá ser interpretada e direcionada para o fluxo correspondente.

## RF07 — Agendamento

O sistema deverá permitir iniciar um processo de agendamento.

A implementação deverá depender da forma como a clínica disponibiliza sua agenda atualmente.

## RF08 — Remarcação

O sistema deverá permitir iniciar um processo de remarcação.

## RF09 — Cancelamento

O sistema deverá permitir iniciar um processo de cancelamento.

## RF10 — Transferência para humano

O sistema deverá encaminhar a conversa para uma secretária quando não conseguir resolver a solicitação ou quando o paciente solicitar atendimento humano.

## RF11 — Controle de atendimento humano

Quando uma secretária assumir uma conversa, o bot deverá deixar de responder automaticamente naquela conversa até que o atendimento seja encerrado ou devolvido ao fluxo automatizado.

## RF12 — Painel de conversas

O sistema deverá disponibilizar uma interface para visualização das conversas.

## RF13 — Status da conversa

Cada conversa deverá possuir um estado.

Exemplos:

- BOT
- AGUARDANDO HUMANO
- EM ATENDIMENTO
- FINALIZADA

## RF14 — Identificação do atendente

O sistema deverá registrar qual usuário assumiu uma conversa.

## RF15 — Lembretes

O sistema deverá permitir o envio automático de lembretes relacionados a consultas.

O período de antecedência deverá ser configurável.

## RF16 — Avaliações

O sistema deverá permitir solicitar uma avaliação após o atendimento.

A avaliação poderá incluir:

- Nota.
- Comentário opcional.

## RF17 — Métricas

O sistema deverá apresentar métricas relacionadas ao atendimento.

Exemplos:

- Número de conversas.
- Conversas resolvidas pelo bot.
- Conversas transferidas.
- Tempo médio de atendimento.
- Quantidade de avaliações.
- Nota média.

## RF18 — Configuração de informações

Usuários autorizados deverão poder alterar informações utilizadas pelo bot, como:

- Endereço.
- Horários.
- Convênios.
- Serviços.
- Informações institucionais.
- Perguntas frequentes.

## RF19 — Autenticação

O sistema deverá exigir autenticação para acesso ao painel administrativo.

## RF20 — Controle de acesso

O sistema deverá restringir funcionalidades de acordo com o nível de acesso do usuário.

## RF21 — Registro de eventos

O sistema deverá registrar eventos importantes para auditoria e diagnóstico.

---

# 7. Inteligência artificial

A inteligência artificial não deverá ser responsável por conduzir livremente o atendimento.

Sua função inicial será auxiliar o sistema na interpretação das mensagens.

Arquitetura conceitual:

```text
Mensagem do paciente
        ↓
LLM
        ↓
Intenção + informações extraídas
        ↓
Backend
        ↓
Fluxo determinístico
        ↓
Resposta
```

Exemplo:

```text
"Queria marcar ginecologista para sexta à tarde"

            ↓

{
  intent: "AGENDAMENTO",
  especialidade: "GINECOLOGIA",
  periodo: "SEXTA_TARDE"
}

            ↓

Fluxo de agendamento
```

A aplicação deverá validar as informações fornecidas pela IA antes de executar qualquer ação.

A IA não deverá:

- Diagnosticar pacientes.
- Interpretar exames.
- Prescrever medicamentos.
- Recomendar tratamentos.
- Tomar decisões médicas.
- Executar operações críticas sem validação do sistema.

---

# 8. Regras de negócio

## RN01 — Encaminhamento humano

Caso o bot não consiga identificar ou resolver uma solicitação, deverá encaminhá-la para atendimento humano.

## RN02 — Solicitação explícita

O paciente poderá solicitar atendimento humano a qualquer momento.

## RN03 — Atendimento humano

Enquanto uma conversa estiver sob responsabilidade de uma secretária, o fluxo automatizado não deverá enviar respostas conflitantes.

## RN04 — Informações médicas

Solicitações que envolvam diagnóstico, tratamento, medicamentos ou outras orientações médicas deverão ser encaminhadas para atendimento humano.

## RN05 — Informações confiáveis

Respostas institucionais deverão utilizar informações cadastradas pela clínica, evitando que a IA invente informações.

## RN06 — Agenda

O sistema não deverá confirmar um horário sem que exista confirmação de disponibilidade através da fonte oficial da agenda.

## RN07 — Permissões

Usuários somente poderão acessar informações e funcionalidades compatíveis com suas permissões.

## RN08 — Especialidades

Especialidades deverão ser entidades configuráveis do sistema, não estruturas fixas no código.

Atualmente:

- Dermatologia.
- Ginecologia.

O sistema deverá permitir adicionar novas especialidades posteriormente.

## RN09 — Profissionais

Profissionais deverão ser entidades independentes das especialidades, permitindo que o sistema seja expandido futuramente.

## RN10 — Dados sensíveis

O bot deverá possuir acesso somente aos dados necessários para realizar sua função.

Informações médicas sensíveis não deverão ser disponibilizadas ao bot sem necessidade.

---

# 9. Fluxos principais

## 9.1 Atendimento inicial

```text
Paciente
   ↓
WhatsApp
   ↓
Bot
   ↓
Identificação da intenção
   ↓
Fluxo correspondente
```

## 9.2 Agendamento

```text
Paciente
   ↓
"Quero marcar uma consulta"
   ↓
Identificação da intenção
   ↓
Especialidade
   ↓
Preferência de data/horário
   ↓
Consulta de disponibilidade
   ↓
Confirmação
   ↓
Agendamento
```

Caso não exista integração com a agenda:

```text
Preferências do paciente
        ↓
Encaminhamento para secretária
        ↓
Agendamento manual
```

## 9.3 Atendimento humano

```text
Paciente
   ↓
Solicitação
   ↓
Bot não consegue resolver
   ↓
Transferência
   ↓
Fila de atendimento
   ↓
Secretária assume
   ↓
Atendimento
   ↓
Finalização
```

## 9.4 Lembrete

```text
Consulta próxima
      ↓
Worker/automação
      ↓
Mensagem WhatsApp
      ↓
Paciente
      ↓
Confirmar / solicitar alteração
```

## 9.5 Avaliação

```text
Atendimento finalizado
        ↓
Solicitação de avaliação
        ↓
Nota
        ↓
Comentário opcional
        ↓
Armazenamento
        ↓
Dashboard
```

---

# 10. Requisitos não funcionais

## RNF01 — Segurança

O sistema deverá utilizar autenticação e autorização para proteger o painel administrativo.

## RNF02 — Disponibilidade

O serviço de atendimento deverá permanecer disponível continuamente, considerando as limitações dos serviços externos utilizados.

## RNF03 — Escalabilidade

A arquitetura deverá permitir a inclusão de:

- Novos profissionais.
- Novas especialidades.
- Novos fluxos.
- Novos números de WhatsApp.
- Novas unidades.
- Novas integrações.

## RNF04 — Manutenibilidade

O sistema deverá possuir arquitetura modular, separando responsabilidades entre atendimento, IA, agenda, usuários, avaliações e integrações.

## RNF05 — Observabilidade

Erros e eventos importantes deverão ser registrados para permitir diagnóstico.

## RNF06 — Performance

O sistema deverá minimizar o tempo entre o recebimento de uma mensagem e o envio da resposta.

## RNF07 — Privacidade

O armazenamento e tratamento de dados deverão considerar os princípios aplicáveis da LGPD.

---

# 11. Integrações

As integrações previstas são:

### Obrigatória para o MVP

- WhatsApp.

### Possíveis

- Sistema de agenda da clínica.
- Google Calendar.
- Provedor de IA.
- Serviço de envio de notificações.
- Sistema existente da clínica.

Antes da implementação da agenda, deverá ser identificado qual sistema a clínica utiliza atualmente e se existe API disponível.

---

# 12. Dados principais

O modelo deverá considerar inicialmente entidades semelhantes a:

```text
User
Role
Permission

Patient
Conversation
Message

Specialty
Professional
Service

Appointment

FAQ
ClinicInformation

Automation
Evaluation

AuditLog
```

O modelo definitivo será elaborado posteriormente.

---

# 13. Arquitetura conceitual

A arquitetura inicial deverá seguir uma separação semelhante a:

```text
                    WhatsApp
                       │
                       ▼
                 Webhook/API
                       │
                       ▼
                     n8n
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
         Backend                 LLM
             │
      ┌──────┼──────┐
      ▼      ▼      ▼
   Agenda  Bot    Users
      │      │      │
      └──────┼──────┘
             ▼
         PostgreSQL
             ▲
             │
        Painel Web
```

Essa arquitetura ainda deverá ser validada tecnicamente antes da implementação.

---

# 14. Escopo do MVP — primeiro mês

## Atendimento

- Receber mensagens.
- Enviar mensagens.
- Fluxo inicial.
- FAQ.
- Identificação de intenção.
- Agendamento.
- Remarcação.
- Cancelamento.
- Transferência para humano.

## Painel

- Login.
- Controle de acesso.
- Lista de conversas.
- Visualização de mensagens.
- Assumir conversa.
- Encerrar conversa.
- Configurações básicas.

## Automação

- Lembretes.
- Avaliações.

## Gestão

- Informações básicas da clínica.
- FAQ.
- Métricas básicas.

## Infraestrutura

- Banco de dados.
- Logs.
- Tratamento de erros.
- Deploy.
- Documentação.

---

# 15. Fora do MVP

Inicialmente não serão implementados:

- Prontuário eletrônico.
- Prescrição.
- Diagnóstico automatizado.
- Gestão financeira.
- Estoque.
- Aplicativo mobile.
- CRM completo.
- Gestão completa de pacientes.
- IA médica.
- Suporte a múltiplas clínicas.
- Integração com múltiplos provedores de WhatsApp.
- Recursos avançados de BI.

Esses itens poderão entrar posteriormente no roadmap.

---

# 16. Pontos que precisam ser investigados

Pontos a validar futuramente:

1. Qual sistema de WhatsApp é utilizado atualmente?
2. O número atual utiliza WhatsApp Business ou WhatsApp Business Platform?
3. Qual provedor/API está sendo utilizado?
4. Qual sistema de agenda a clínica utiliza?
5. O sistema de agenda possui API?
6. Existe banco de dados ou sistema administrativo atual?
7. O bot atual utiliza n8n?
8. Qual é a arquitetura do bot atual?
9. Quais são os principais problemas percebidos pelas secretárias?
10. Quais perguntas os pacientes fazem com maior frequência?
11. Quais processos atualmente consomem mais tempo das secretárias?
12. Como funciona o agendamento atualmente?
13. Como são enviados os lembretes?
14. Quais informações a clínica gostaria que fossem automatizadas?
15. Quais informações não podem ser acessadas pelo bot?
16. Quais usuários precisam de acesso ao painel?
17. Quais métricas a clínica gostaria de acompanhar?

Essas respostas poderão alterar significativamente a arquitetura.

---

# 17. Roadmap futuro

Após o MVP, o sistema poderá evoluir para:

### Fase 2

- Agenda completa.
- Cadastro de pacientes.
- Histórico de atendimentos.
- Mais automações.
- Relatórios avançados.
- Integração com sistemas externos.

### Fase 3

- Gestão de estoque.
- Gestão financeira.
- Gestão de procedimentos.
- Dashboard operacional completo.

### Fase 4

- Multiunidade.
- Multiempresa.
- Múltiplos números de WhatsApp.
- Marketplace de integrações.
- Plataforma SaaS.

---

# 18. Critério de sucesso do MVP

O MVP será considerado bem-sucedido quando a clínica conseguir utilizar o sistema em atendimento real e:

- O paciente conseguir iniciar atendimento pelo WhatsApp.
- O bot resolver dúvidas frequentes.
- O bot direcionar corretamente solicitações comuns.
- A secretária conseguir assumir conversas.
- O sistema não interferir em conversas humanas.
- Os lembretes funcionarem corretamente.
- As avaliações serem registradas.
- A equipe conseguir visualizar métricas básicas.
- O sistema funcionar de maneira estável em produção.

O principal indicador não será a quantidade de funcionalidades, mas a capacidade de **reduzir trabalho manual sem prejudicar a experiência do paciente**.
