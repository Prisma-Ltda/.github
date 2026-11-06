<!-- BANNER PRINCIPAL -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:00C2CB,50:2A9D8F,100:1D3557&height=200&section=header&text=PRISMA&fontSize=50&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Ecossistema%20de%20Feedback,%20IA%20e%20Gestão%20Corporativa&descAlignY=55&descSize=16" alt="PRISMA Header Banner" />
</p>

<!-- BADGES -->
<p align="center">
  <img src="https://img.shields.io/badge/Status-Ativo-00C2CB?style=flat-square" alt="Status">
  <img src="https://img.shields.io/badge/Arquitetura-Hexagonal%20%7C%20Medallion-2A9D8F?style=flat-square" alt="Arquitetura">
  <img src="https://img.shields.io/badge/Segurança-OWASP%20Top%2010%20%7C%20MFA-1D3557?style=flat-square" alt="Segurança">
  <img src="https://img.shields.io/badge/Qualidade-SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white" alt="SonarQube">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Angular-21.2-DD0031?style=flat-square&logo=angular&logoColor=white" alt="Angular">
  <img src="https://img.shields.io/badge/TypeScript-5.9-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Tailwind_CSS-4.2-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white" alt="Tailwind CSS">
  <img src="https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java 21">
  <img src="https://img.shields.io/badge/Spring_Boot-3.x%20%2F%204.x-6DB33F?style=flat-square&logo=springboot&logoColor=white" alt="Spring Boot">
  <img src="https://img.shields.io/badge/Python-3.13-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Polars-0.20-CD792C?style=flat-square" alt="Polars">
  <img src="https://img.shields.io/badge/Prefect-Orchestration-024DFD?style=flat-square&logo=prefect&logoColor=white" alt="Prefect">
  <img src="https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Docker-Ready-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
</p>

---

## Visão Geral

O **PRISMA** é uma plataforma corporativa voltada para a gestão de clima organizacional, acompanhamento de desempenho e análise contínua de feedbacks internos. O sistema combina a metodologia **Net Promoter Score (NPS)** com **Inteligência Artificial (Processamento de Linguagem Natural)** para transformar avaliações qualitativas e quantitativas em indicadores acionáveis para lideranças e equipes de Recursos Humanos.

A solução opera de ponta a ponta: desde a coleta de avaliações em interface web com suporte a acessibilidade e autenticação segura (MFA), passando por regras de negócio centralizadas em arquitetura hexagonal, até a ingestão e enriquecimento dos dados em uma esteira analítica com processamento local de modelos de linguagem.

---

## Estrutura do Ecossistema

O ecossistema PRISMA é dividido em três serviços independentes:

| Repositório | Descrição | Tecnologias Principais |
| :--- | :--- | :--- |
| [**prisma-app**](https://github.com/Prisma-Ltda/prisma-app) | Interface web (SPA). Responsável pelos fluxos de coleta de feedback, visualização analítica, organograma hierárquico e governança de acessibilidade. | Angular 21, TypeScript, Tailwind CSS, D3.js, Storybook, Vitest, VLibras |
| [**prisma-api**](https://github.com/Prisma-Ltda/prisma-api) | API RESTful e núcleo transacional. Gerencia autenticação, controle de usuários, hierarquias organizacionais, equipes e permissões. | Java 21, Spring Boot, Spring Security, JWT, PostgreSQL, Flyway, Maven |
| [**prisma-elt**](https://github.com/Prisma-Ltda/prisma-elt) | Pipeline de dados e inteligência artificial. Realiza ingestão, tratamento, análise de sentimento com LLM local e consolidação de métricas. | Python 3.13, Prefect, Polars, dbt, Llama-cpp (GGUF), pytest |

---

## Arquitetura da Solução

O fluxo de dados e comunicação entre os componentes segue o modelo abaixo:

```text
[ Colaborador / Gestor ]
           │
           ▼
┌──────────────────────────────────────┐
│             prisma-app               │  SPA em Angular 21
│   - Interface de Feedback e PDI      │  - D3.js (Organograma)
│   - Autenticação com 2FA / TOTP      │  - Cloudflare Turnstile e VLibras
└──────────────────┬───────────────────┘
                   │
                   │ HTTPS / REST (JWT)
                   ▼
┌──────────────────────────────────────┐
│             prisma-api               │  Backend em Java 21 / Spring Boot
│   - Arquitetura Hexagonal            │  - Controle de Acesso (RBAC)
│   - Regras de Negócio e Serviços     │  - Migrations automáticas (Flyway)
└──────────────────┬───────────────────┘
                   │
                   │ Escrita e Leitura Transacional
                   ▼
┌──────────────────────────────────────┐
│        PostgreSQL (Database)         │  Schemas Operacionais
└──────────────────┬───────────────────┘
                   │
                   │ Ingestão / Extração Batch
                   ▼
┌──────────────────────────────────────┐
│             prisma-elt               │  Pipeline de Engenharia de Dados & IA
│   - Arquitetura Medallion            │  - Polars (Limpeza e Transformação)
│   - Ingestão Bronze / Silver / Gold  │  - Prefect (Orquestração)
│   - LLM Local (Llama-cpp / GGUF)     │  - Análise de Sentimento Privada
└──────────────────┬───────────────────┘
                   │
                   ▼
       [ Dashboards & Relatórios ]
```

---

## Principais Recursos

- **Dashboard Analítico**: Indicadores de eNPS, consolidação de promotores, neutros e detratores, além de gráficos de tendência de sentimento ao longo do tempo.
- **Organograma Hierárquico Interativo**: Renderização dinâmica em árvore utilizando D3.js, permitindo navegação, busca de colaboradores e visualização de estruturas departamentais.
- **Coleta de Feedback Estruturada**: Formulário em etapas com seleção de destinatário, nota NPS e justificativa descritiva, com mecanismo de persistência de rascunho em cache local.
- **Classificação de Sentimento com IA Privada**: Inferência automatizada via modelos de linguagem executados localmente (formato GGUF), garantindo privacidade dos dados internos sem envio a serviços terceiros.
- **Plano de Desenvolvimento Individual (PDI)**: Acompanhamento de metas individuais associadas aos pontos levantados nos ciclos de avaliação.
- **Gestão de Mudanças Organizacionais**: Módulo para requisição, aprovação e registro histórico de transferências de equipe e alterações de função.
- **Autenticação e Controle de Sessão**: Suporte a autenticação de dois fatores (2FA via TOTP/QRCode), tokens JWT assinados, e proteção contra abusos via Cloudflare Turnstile.
- **Acessibilidade Digital**: Navegação semântica e suporte integrado ao tradutor de Língua Brasileira de Sinais (VLibras).

---

## Pipeline de Dados (Arquitetura Medallion)

A esteira de dados em `prisma-elt` organiza o processamento de feedbacks em três camadas sequenciais:

1. **Camada Bronze (Raw)**: Ingestão de feedbacks e dados transacionais brutos extraídos do banco de dados operacional.
2. **Camada Silver (Trusted & Enriched)**:
   - Limpeza, tipagem e remoção de inconsistências com Polars.
   - Inferência de sentimento (positivo, neutro, negativo) por meio de modelo LLM executado localmente.
3. **Camada Gold (Aggregated & Analytics)**:
   - Modelagem dimensional e transformações analíticas via dbt.
   - Validações de integridade e consolidação de métricas para consumo dos painéis gerenciais.

---

## Práticas de Segurança e Qualidade de Código

A solução adota diretrizes de Shift-Left Security e conformidade com o padrão OWASP Top 10 em todos os componentes:

| Tipo | Finalidade | Ferramentas Utilizadas |
| :--- | :--- | :--- |
| **SCA** (Software Composition Analysis) | Identificação de dependências vulneráveis e desatualizadas (CVEs). | OWASP Dependency-Check, npm audit, pip-audit, Dependabot |
| **SAST** (Static Application Security Testing) | Análise estática de código-fonte para prevenção de falhas de segurança e injeções. | SpotBugs, FindSecBugs, Semgrep CE, SonarQube |
| **DAST** (Dynamic Application Security Testing) | Verificação dinâmica de vulnerabilidades em endpoints e cabeçalhos HTTP em tempo de execução. | OWASP ZAP (zap-api-scan e zap-baseline) |
| **Qualidade e Cobertura** | Controle de cobertura de testes, complexidade de código e dívida técnica. | JaCoCo (Java), Vitest (TypeScript), pytest-cov (Python), SonarQube |

---

## Matriz Tecnológica

| Camada | Tecnologias |
| :--- | :--- |
| **Frontend** | Angular 21, TypeScript 5.9, Tailwind CSS 4, D3.js, Ngx-Charts, Storybook 10, Vitest, Lucide Icons, VLibras |
| **Backend** | Java 21 LTS, Spring Boot 3/4, Spring Security, JWT, Flyway, Maven, OpenAPI / Swagger UI |
| **Dados e IA** | Python 3.13, Prefect, Polars, dbt-core, Llama-cpp (GGUF), pytest |
| **Banco de Dados** | PostgreSQL 16 (Schemas: public, bronze, silver, gold) |
| **Infraestrutura e QA** | Docker, Docker Compose, SonarQube, OWASP ZAP, GitHub Actions |

---

## Guia de Execução Local

### Pré-requisitos
- Git
- Docker e Docker Compose
- JDK 21 e Maven
- Node.js 22.x e npm
- Python 3.13

### 1. Clonar os Repositórios
```bash
# Repositório do Frontend
git clone https://github.com/Prisma-Ltda/prisma-app.git

# Repositório do Backend
git clone https://github.com/Prisma-Ltda/prisma-api.git

# Repositório de Dados e IA
git clone https://github.com/Prisma-Ltda/prisma-elt.git
```

### 2. Inicializar o Banco de Dados e Serviços
```bash
cd prisma-api
docker compose up -d
```

### 3. Iniciar o Backend
```bash
# Execução da API Spring Boot (disponível em http://localhost:8080)
./mvnw spring-boot:run
```

### 4. Iniciar o Frontend
```bash
cd ../prisma-app
npm install
npm start
# Aplicação disponível em http://localhost:4200
```

### 5. Executar o Pipeline de Dados
```bash
cd ../prisma-elt
python -m venv .venv
source .venv/bin/activate  # No Windows: .\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python -m poc.main
```

---

## Diretrizes de Contribuição

Para assegurar padronização entre as equipes de desenvolvimento:

### Padrão de Branches
- `feat/nome-da-feature`: Novas funcionalidades
- `fix/nome-do-bug`: Correções de defeitos
- `refactor/nome-da-melhoria`: Refatoração estrutural de código
- `chore/nome-da-tarefa`: Atualização de configurações, dependências ou documentação

### Padrão de Commits
Utilize o padrão Conventional Commits:
- `feat(app): adiciona filtro de periodo na tela de relatorios`
- `fix(api): corrige validacao de token jwt no endpoint de equipes`
- `perf(elt): otimiza processamento da camada silver com polars`
- `test(api): adiciona testes unitarios para criacao de usuarios`
- `docs(readme): atualiza documentacao de inicializacao do ambiente`

---

<!-- FOOTER -->
<p align="center">
  <b>PRISMA</b> — Gestão de Desempenho e Clima Organizacional
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1D3557,50:2A9D8F,100:00C2CB&height=100&section=footer" alt="PRISMA Footer Banner" />
</p>
