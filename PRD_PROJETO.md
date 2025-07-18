# Product Requirements Document (PRD)
## Sistema de Controle de Diárias - FÁCIL

---

## Overview

O Sistema de Controle de Diárias - FÁCIL é uma solução digital desenvolvida para simplificar e automatizar o processo de gestão de diárias para profissionais que trabalham com deslocamentos e viagens a trabalho. O sistema resolve o problema da gestão manual e complexa de relatórios de diárias, oferecendo uma interface intuitiva e processos automatizados para controle de gastos, relatórios e aprovações.

**Problema que resolve:** Elimina a complexidade e erros manuais no controle de diárias, reduzindo tempo de processamento e aumentando a precisão dos relatórios.

**Público-alvo:** Engenheiros que precisam controlar diárias de forma digital, substituindo o uso de planilhas manuais.

**Valor:** Redução significativa no tempo de processamento de diárias, maior precisão no controle e facilidade de visualização comparado ao uso de planilhas.

---

## Core Features

### 1. Sistema de Autenticação
- **O que faz:** Sistema de login simples para o engenheiro
- **Importância:** Garante segurança e controle de acesso ao sistema
- **Funcionamento:** Login com credenciais únicas, acesso direto às funcionalidades de controle de diárias

### 2. Registro de Diárias
- **O que faz:** Interface para inserção de gastos diários com categorização automática
- **Importância:** Facilita o registro rápido e preciso de despesas
- **Funcionamento:** Formulário React Hook Form com validação Zod, campos para data, valor, categoria, descrição e comprovantes

### 3. Categorização Automática de Gastos
- **O que faz:** Classifica automaticamente os gastos em categorias predefinidas
- **Importância:** Padroniza relatórios e facilita análises
- **Funcionamento:** Algoritmo de reconhecimento baseado em descrições e valores

### 4. Controle e Validação
- **O que faz:** Sistema de validação e controle de dados inseridos
- **Importância:** Garante precisão e consistência dos dados
- **Funcionamento:** Validação automática com feedback imediato, controle de duplicatas

### 5. Geração de Relatórios
- **O que faz:** Cria relatórios detalhados e exportáveis
- **Importância:** Fornece visibilidade e dados para tomada de decisão
- **Funcionamento:** Templates configuráveis com exportação em múltiplos formatos

### 6. Dashboard e Analytics
- **O que faz:** Visualização de dados e métricas em tempo real
- **Importância:** Permite acompanhamento de gastos e identificação de tendências
- **Funcionamento:** Gráficos interativos e filtros dinâmicos

### 7. Cálculos Automáticos
- **O que faz:** Calcula automaticamente totais, médias e comparativos
- **Importância:** Fornece insights rápidos sobre gastos e produtividade
- **Funcionamento:** Cálculos em tempo real de dias de viagem, média por dia, comparativo com limites

### 8. Controle de Períodos de Trabalho
- **O que faz:** Define e controla períodos de trabalho durante viagens
- **Importância:** Permite análise de produtividade e custo-benefício
- **Funcionamento:** Registro de horas trabalhadas, diferenciação de dias úteis/finais de semana

### 9. Validações Avançadas
- **O que faz:** Valida gastos contra limites e regras de negócio
- **Importância:** Garante conformidade com políticas e orçamentos
- **Funcionamento:** Validação de limites por categoria, horários de trabalho, gastos por dia

### 10. Configurações do Sistema
- **O que faz:** Permite configurar parâmetros e limites do sistema
- **Importância:** Personaliza o sistema para necessidades específicas
- **Funcionamento:** Definição de limites de gastos, períodos de trabalho, categorias customizáveis

---

## User Experience

### User Personas

**João Silva - Engenheiro**
- 35 anos, engenheiro de campo
- Atualmente usa planilha Excel para controle de diárias
- Precisa registrar gastos de viagens a trabalho
- Quer substituir processo manual por sistema digital
- Usa desktop principalmente para trabalho

### Key User Flows

**Fluxo de Registro de Diária:**
1. Login no sistema
2. Seleção de "Nova Diária"
3. Preenchimento de dados (data, gastos, descrições)
4. Upload de comprovantes
5. Validação automática dos dados
6. Salvamento e confirmação

**Fluxo de Visualização e Controle:**
1. Acesso ao dashboard principal
2. Visualização de diárias registradas
3. Filtros por período, categoria, valor
4. Edição de registros quando necessário
5. Geração de relatórios

**Fluxo de Configuração:**
1. Acesso às configurações do sistema
2. Definição de limites por categoria
3. Configuração de períodos de trabalho
4. Personalização de categorias
5. Salvamento das configurações

**Fluxo de Análise:**
1. Visualização de métricas no dashboard
2. Análise de gastos por período
3. Comparativo com limites configurados
4. Geração de relatórios de produtividade
5. Exportação de dados para análise

### UI/UX Considerations
- Interface responsiva para mobile e desktop
- Design intuitivo com poucos cliques
- Feedback visual claro para ações
- Acessibilidade para diferentes usuários
- Cores e tipografia consistentes com identidade visual

---

## Technical Architecture

### System Components

**Frontend:**
- Interface web responsiva (React/TypeScript)
- Componentes modulares e reutilizáveis
- Sistema de design consistente
- Arquitetura baseada em hooks customizados
- Formulários com React Hook Form + Zod
- Validação de dados com Zod schemas

**Backend:**
- API RESTful (Fastify/TypeScript)
- Arquitetura MVC (Model-View-Controller)
- Autenticação JWT
- Banco de dados relacional (PostgreSQL)
- Sistema de cache (Redis)

**Infrastructure:**
- Servidor de aplicação configurável
- Sistema de backup
- Monitoramento e logs
- Configuração modular para diferentes ambientes

### Data Models

**Usuário:**
- ID, nome, email, senha_hash, data_criacao

**Diária:**
- ID, usuario_id, data_inicio, data_fim, valor_total, status, dias_viagem, media_dia

**Gasto:**
- ID, diaria_id, categoria, valor, descricao, comprovante_url, data_registro, data_gasto

**Categoria:**
- ID, nome, descricao, cor, limite_diario, limite_mensal

**Período de Trabalho:**
- ID, diaria_id, data, hora_inicio, hora_fim, horas_trabalhadas, tipo_dia (util/fim_semana)

**Configuração:**
- ID, usuario_id, categoria_id, limite_diario, limite_mensal, ativo

**Relatório:**
- ID, usuario_id, tipo_relatorio, periodo_inicio, periodo_fim, dados_json, data_geracao

### APIs and Integrations

**APIs Internas:**
- /api/auth (autenticação)
- /api/diarias (CRUD diárias)
- /api/gastos (CRUD gastos)
- /api/categorias (gestão categorias)
- /api/periodos-trabalho (CRUD períodos)
- /api/configuracoes (gestão configurações)
- /api/relatorios (geração relatórios)
- /api/calculos (cálculos automáticos)
- /api/validacoes (validações avançadas)

**Integrações Externas:**
- Sistema de pagamento
- Serviço de email
- Storage para arquivos
- Analytics

### Formulários e Validação

**React Hook Form:**
- Gerenciamento de estado de formulários performático
- Validação em tempo real
- Integração com Zod para type safety
- Componentes de formulário reutilizáveis
- Tratamento de erros consistente

**Validação Zod:**
- Schemas de validação type-safe
- Validação tanto no frontend quanto backend
- Mensagens de erro customizáveis
- Transformação de dados
- Validação de tipos complexos

**Componentes de Formulário:**
- Input, Select, TextArea reutilizáveis
- Integração automática com React Hook Form
- Validação visual e feedback de erros
- Acessibilidade integrada
- Temas consistentes

**Componentes de Cálculo:**
- Calculadora de dias de viagem
- Calculadora de médias por dia
- Comparativo com limites
- Indicadores de produtividade

**Componentes de Configuração:**
- Formulário de limites por categoria
- Configurador de períodos de trabalho
- Personalizador de categorias
- Validador de parâmetros

### Cálculos e Validações Específicas

**Cálculos Automáticos:**
- **Dias de Viagem:** Diferença entre data_inicio e data_fim
- **Média por Dia:** valor_total / dias_viagem
- **Subtotais por Categoria:** Soma de gastos por categoria
- **Comparativo com Limites:** Gastos vs limites configurados
- **Horas Trabalhadas:** Soma de horas por período
- **Produtividade:** Relação entre horas e gastos

**Validações Avançadas:**
- **Limite Diário:** Validação de gastos por categoria por dia
- **Limite Mensal:** Validação de gastos por categoria por mês
- **Horários de Trabalho:** Validação de períodos de trabalho
- **Dias Úteis:** Diferenciação entre dias úteis e finais de semana
- **Duplicatas:** Controle de gastos duplicados
- **Comprovantes:** Validação de upload de arquivos

### Arquitetura MVC Backend

**Model (Modelo):**
- Representação dos dados e regras de negócio
- Interação com banco de dados
- Validação de dados com Zod
- Queries otimizadas e type-safe

**View (Visão):**
- Respostas padronizadas da API
- Serialização de dados
- Tratamento de erros consistente
- Documentação automática (Swagger/OpenAPI)

**Controller (Controlador):**
- Recebimento de requisições
- Validação de entrada com Zod
- Orquestração de serviços
- Respostas padronizadas

**Benefícios da Arquitetura MVC:**
- Separação clara de responsabilidades
- Código mais testável e manutenível
- Reutilização de componentes
- Facilita implementação de testes
- Escalabilidade do código

### Arquitetura Modular e Boas Práticas

**Princípios de Desenvolvimento:**
- **DRY (Don't Repeat Yourself):** Componentes e funções reutilizáveis
- **Separação de Responsabilidades:** Lógica de negócio separada da apresentação
- **TypeScript Rigoroso:** Tipos específicos, evitando uso de 'any'
- **Componentes Atômicos:** Componentes pequenos e focados (< 250 linhas)
- **Hooks Customizados:** Lógica reutilizável extraída em hooks
- **Gerenciamento de Estado Eficiente:** Context API e composição de componentes
- **Tratamento de Erros:** Error boundaries e feedback ao usuário
- **Performance:** React.memo, useCallback, useMemo quando apropriado
- **Acessibilidade:** WCAG guidelines e navegação por teclado
- **Testes Abrangentes:** Jest para unit, integration e E2E tests
- **Formulários Modulares:** React Hook Form com validação Zod
- **Arquitetura MVC:** Separação clara no backend (Model-View-Controller)

**Estrutura de Pastas Frontend:**
```
src/
├── components/          # Componentes reutilizáveis
│   ├── ui/             # Componentes de UI básicos
│   ├── forms/          # Componentes de formulário reutilizáveis
│   ├── calculators/    # Componentes de cálculo
│   ├── config/         # Componentes de configuração
│   └── features/       # Componentes específicos de features
├── hooks/              # Hooks customizados
│   ├── forms/          # Hooks para formulários
│   ├── api/            # Hooks para APIs
│   ├── calculations/   # Hooks para cálculos
│   └── config/         # Hooks para configurações
├── services/           # Lógica de negócio e APIs
├── types/              # Definições de tipos TypeScript
├── schemas/            # Schemas de validação Zod
├── utils/              # Funções utilitárias
│   ├── calculations/   # Utilitários de cálculo
│   └── validations/    # Utilitários de validação
├── contexts/           # Context providers
├── pages/              # Componentes de página
└── tests/              # Arquivos de teste Jest
```

**Estrutura de Pastas Backend:**
```
src/
├── controllers/        # Controllers (lógica de negócio)
│   ├── diarias/       # Controllers de diárias
│   ├── gastos/        # Controllers de gastos
│   ├── calculos/      # Controllers de cálculos
│   ├── config/        # Controllers de configuração
│   └── relatorios/    # Controllers de relatórios
├── models/            # Models (interação com banco)
├── views/             # Views (respostas da API)
├── routes/            # Definição de rotas
├── middlewares/       # Middlewares customizados
├── services/          # Serviços de negócio
│   ├── calculations/  # Serviços de cálculo
│   ├── validations/   # Serviços de validação
│   └── reports/       # Serviços de relatórios
├── types/             # Definições de tipos TypeScript
├── schemas/           # Schemas de validação
├── utils/             # Funções utilitárias
│   ├── calculations/  # Utilitários de cálculo
│   └── validations/   # Utilitários de validação
├── config/            # Configurações
└── tests/             # Arquivos de teste Jest
```

---

## Development Roadmap

### Fase 1 - MVP (Minimum Viable Product)
**Objetivo:** Sistema básico funcional para substituir a planilha de controle de diárias

**Funcionalidades:**
- Sistema de autenticação simples
- Registro manual de diárias
- Visualização de diárias registradas
- Categorização básica de gastos
- Interface web responsiva
- Banco de dados básico

**Entregáveis:**
- Sistema de login/logout
- Formulário de registro de diárias
- Lista de diárias com filtros básicos
- Dashboard simples de visualização

### Fase 2 - Funcionalidades Core
**Objetivo:** Implementar funcionalidades essenciais de controle

**Funcionalidades:**
- Categorização automática de gastos
- Upload e gestão de comprovantes
- Validação avançada de dados
- Cálculos automáticos básicos
- Relatórios básicos
- Dashboard com métricas
- Filtros avançados

**Entregáveis:**
- Categorização inteligente
- Sistema de arquivos
- Cálculos de dias e médias
- Relatórios em PDF/Excel
- Dashboard interativo

### Fase 3 - Analytics e Otimizações
**Objetivo:** Adicionar insights e melhorar experiência

**Funcionalidades:**
- Dashboard avançado com gráficos
- Analytics e métricas
- Controle de períodos de trabalho
- Validações avançadas
- Configurações do sistema
- Filtros avançados
- Exportação de dados
- Otimizações de performance
- Testes Jest automatizados

**Entregáveis:**
- Dashboard interativo
- Sistema de métricas
- Controle de períodos
- Sistema de configurações
- API completa documentada
- Testes Jest (unit, integration, E2E)

### Fase 4 - Integrações e Expansão
**Objetivo:** Integrações externas e funcionalidades avançadas

**Funcionalidades:**
- Integração com sistemas ERP
- API pública para terceiros
- Funcionalidades avançadas
- Internacionalização
- Otimizações de performance

**Entregáveis:**
- Integrações com ERPs
- API pública documentada
- Sistema multilíngue
- Performance otimizada

---

## Logical Dependency Chain

### Ordem Lógica de Desenvolvimento

**1. Foundation (Base)**
- Sistema de autenticação
- Banco de dados e modelos
- API básica
- Interface web básica

**2. Core Features (Funcionalidades Essenciais)**
- CRUD de diárias
- Sistema de autenticação
- Upload de arquivos
- Interface responsiva

**3. Business Logic (Lógica de Negócio)**
- Categorização automática
- Validação de dados
- Cálculos automáticos
- Controle de períodos
- Relatórios básicos
- Controle de duplicatas

**4. Enhancement (Melhorias)**
- Dashboard avançado
- Analytics
- Validações avançadas
- Configurações
- Otimizações
- Testes

**5. Expansion (Expansão)**
- Integrações externas
- API pública
- Funcionalidades avançadas
- Otimizações finais

### Princípios de Desenvolvimento
- **Atomicidade:** Cada feature deve ser completa e funcional
- **Iterativo:** Construir sobre funcionalidades existentes
- **Testável:** Cada fase deve incluir testes
- **Escalável:** Arquitetura preparada para crescimento
- **Modular:** Componentes e funções reutilizáveis
- **TypeScript:** Tipos rigorosos e específicos
- **Performance:** Otimizações desde o início
- **Acessibilidade:** Inclusivo desde o design

---

## Risks and Mitigations

### Technical Challenges

**Risco:** Complexidade na categorização automática
**Mitigação:** Começar com categorização manual, implementar IA gradualmente

**Risco:** Performance com muitos usuários
**Mitigação:** Implementar cache, otimizar queries, componentes modulares otimizados

**Risco:** Segurança de dados
**Mitigação:** Criptografia, autenticação robusta, auditoria

### MVP Definition

**Risco:** Escopo muito amplo
**Mitigação:** Focar em funcionalidades essenciais, validar com usuários

**Risco:** Falta de validação de mercado
**Mitigação:** Testes com usuários reais, feedback contínuo

**Risco:** Complexidade técnica subestimada
**Mitigação:** Prototipagem rápida, validação técnica, arquitetura modular

**Risco:** Código duplicado e manutenibilidade
**Mitigação:** Componentes reutilizáveis, hooks customizados, revisão de código

### Resource Constraints

**Risco:** Limitação de recursos de desenvolvimento
**Mitigação:** Priorização rigorosa, desenvolvimento iterativo

**Risco:** Dependências externas
**Mitigação:** Identificar alternativas, planos de contingência

**Risco:** Mudanças de requisitos
**Mitigação:** Documentação clara, comunicação frequente

---

## Appendix

### Research Findings
- 85% dos engenheiros usam planilhas para controle de diárias
- 78% consideram processo manual propenso a erros
- 92% preferem solução digital a planilhas
- 88% valorizam visualização rápida e organizada
- 76% precisam de relatórios detalhados

### Technical Specifications
- **Frontend:** React 18+, TypeScript, Material-UI, React Hook Form, Zod
- **Backend:** Fastify, TypeScript, Arquitetura MVC
- **Database:** PostgreSQL 15+
- **Testing:** Jest (unit, integration, E2E)
- **CI/CD:** GitHub Actions
- **Code Quality:** ESLint, Prettier, Husky

### Performance Requirements
- **Tempo de resposta:** < 2 segundos
- **Disponibilidade:** 99.9%
- **Usuários simultâneos:** 1000+
- **Storage:** Escalável conforme necessidade

### Security Requirements
- **Autenticação:** JWT + refresh tokens
- **Criptografia:** AES-256 para dados sensíveis
- **Compliance:** LGPD, ISO 27001
- **Auditoria:** Logs completos de ações

### Testing Strategy

**Jest como Framework Principal:**
- **Unit Tests:** Componentes, hooks, utilitários
- **Integration Tests:** APIs, fluxos de usuário
- **E2E Tests:** Cenários completos de uso

**Cobertura de Testes:**
- **Frontend:** Componentes, hooks customizados, formulários, cálculos
- **Backend:** Controllers, models, services, validações
- **Validação:** Schemas Zod, regras de negócio, limites
- **APIs:** Endpoints, middlewares, autenticação
- **Cálculos:** Utilitários de cálculo, validações de limites
- **Configurações:** Parâmetros, limites, períodos de trabalho

**Estratégia de Testes:**
- Testes unitários para lógica de negócio
- Testes de integração para APIs
- Testes E2E para fluxos críticos
- Mocks para dependências externas
- Testes de acessibilidade