# 📘 Global Football Analytics Platform

## 🎯 Visão Geral

O projeto tem como objetivo construir uma plataforma moderna de engenharia e análise de dados focada em futebol global, utilizando dados coletados do portal [Sofascore](https://www.sofascore.com/?utm_source=chatgpt.com) através de técnicas de web scraping e consumo de endpoints JSON internos.

A plataforma será construída de forma modular, utilizando arquitetura Lakehouse, notebooks analíticos no Databricks e transformação analítica com dbt.
# ⚽ Objetivos do Projeto

A solução permitirá:

* Coleta automatizada de dados de futebol global
* Armazenamento de dados brutos (raw)
* Transformação e normalização de dados
* Construção de métricas e KPIs
* Análises exploratórias em notebooks
* Estruturação de pipeline moderno de dados
* Evolução futura para Machine Learning e IA

# 🗺️ Roadmap — Passo a Passo

Abaixo está a sequência ideal das atividades para construir o projeto de forma profissional, modular e evolutiva.

## 🚀 FASE 1 — Foundation & Data Ingestion

## ✅ Atividade 1 — Descoberta de Endpoints

## Status

⬅️ Atual

## Objetivo

Mapear endpoints JSON internos do [Sofascore](https://www.sofascore.com/?utm_source=chatgpt.com).

## Entregáveis

* Inventário de endpoints
* Notebook de testes
* Primeiras requisições funcionando

---

## ✅ Atividade 2 — Estrutura Inicial do Projeto

## Objetivo

Criar a fundação do repositório.

## Tarefas

* Criar estrutura de diretórios
* Configurar Git
* Criar `requirements.txt`
* Criar notebooks iniciais
* Criar README inicial

---

## Estrutura

```text id="mjlwmz"
/global-football-analytics
│
├── /notebooks
├── /scraper
├── /configs
├── /data
│   ├── /bronze
│   ├── /silver
│   └── /gold
│
├── /dbt
├── requirements.txt
└── README.md
```

---

## ✅ Atividade 3 — Primeiro Scraper Oficial

## Objetivo

Construir o primeiro pipeline de ingestão.

## Dataset inicial

### `matches_by_date`

---

## Tarefas

* Criar request HTTP
* Adicionar headers
* Implementar retries
* Implementar timeout
* Salvar JSON Bronze

---

## Entregáveis

* Arquivos JSON salvos
* Estrutura Bronze criada
* Pipeline executando

---

## ✅ Atividade 4 — Padronização da Camada Bronze

## Objetivo

Criar padrão de armazenamento.

---

## Tarefas

* Definir convenção de nomes
* Criar particionamento por data
* Estruturar diretórios

---

## Estrutura sugerida

```text id="tvjg0o"
/bronze/sofascore/matches/year=2026/month=05/day=18/
```

---

# ✅ Atividade 5 — Criação da Primeira Silver Table

## Objetivo

Transformar JSON bruto em tabela estruturada.

---

## Tarefas

* Ler JSON
* Flatten do schema
* Padronizar colunas
* Criar DataFrame Spark
* Persistir Delta Table

---

## Primeira tabela

### `silver_matches`

Campos:

| Campo      | Tipo      |
| ---------- | --------- |
| match_id   | bigint    |
| match_date | timestamp |
| home_team  | string    |
| away_team  | string    |
| home_score | integer   |
| away_score | integer   |
| tournament | string    |

---

# ✅ Atividade 6 — Setup do Databricks

## Objetivo

Preparar ambiente analítico.

---

## Tarefas

* Criar workspace
* Configurar cluster
* Configurar DBFS
* Subir notebooks
* Configurar Delta Lake

---

# ✅ Atividade 7 — Setup do DBT

## Objetivo

Preparar camada de Analytics Engineering.

---

## Tarefas

* Instalar dbt
* Configurar adapter Databricks
* Criar projeto DBT
* Configurar profiles.yml

---

## Estrutura

```text id="0i7h7f"
/dbt
    /models
    /staging
    /marts
    /tests
    /snapshots
```

---

# 🚀 FASE 2 — Analytics Engineering

---

# ✅ Atividade 8 — Modelos Staging (DBT)

## Objetivo

Padronizar dados Silver.

---

## Tarefas

Criar:

* `stg_matches`
* `stg_teams`
* `stg_tournaments`

---

## Responsabilidades

* casts
* aliases
* limpeza
* normalização

---

# ✅ Atividade 9 — Modelos Mart / Gold

## Objetivo

Criar KPIs e métricas.

---

## Primeiros modelos

### `gold_team_performance`

KPIs:

* vitórias
* derrotas
* média de gols
* aproveitamento

---

### `gold_recent_form`

KPIs:

* últimos 5 jogos
* streak
* forma recente

---

# ✅ Atividade 10 — Testes DBT

## Objetivo

Garantir qualidade dos dados.

---

## Testes

* unique
* not null
* accepted values

---

# ✅ Atividade 11 — Documentação DBT

## Objetivo

Gerar lineage e documentação automática.

---

## Entregáveis

* DAG de modelos
* documentação HTML
* rastreabilidade

---

# 🚀 FASE 3 — Exploratory Analytics

---

# ✅ Atividade 12 — Notebook de EDA

## Objetivo

Explorar comportamento dos dados.

---

## Análises

* distribuição de gols
* mandante vs visitante
* ligas mais ofensivas
* frequência de empates

---

# ✅ Atividade 13 — KPIs Visuais

## Objetivo

Construir análises executivas.

---

## Visualizações

* ranking ofensivo
* ranking defensivo
* forma recente
* eficiência ofensiva

---

# 🚀 FASE 4 — Expansão de Dados

---

# ✅ Atividade 14 — Coleta de Estatísticas Avançadas

## Novos datasets

* player stats
* shots
* possession
* xG
* cards
* substitutions

---

# ✅ Atividade 15 — Event-Level Data

## Objetivo

Capturar granularidade por evento.

---

## Eventos

* gols
* faltas
* cartões
* substituições

---

# 🚀 FASE 5 — IA & Machine Learning

---

# ✅ Atividade 16 — Feature Engineering

## Objetivo

Criar variáveis preditivas.

---

## Features

* forma recente
* média gols
* desempenho casa/fora
* ranking ofensivo

---

# ✅ Atividade 17 — Predição de Resultados

## Modelos

* classificação
* regressão
* previsão de gols

---

# ✅ Atividade 18 — Clusterização de Times

## Objetivo

Descobrir estilos de jogo.

---

## Possibilidades

* ofensivo
* defensivo
* posse
* transição rápida

---

# 🚀 FASE 6 — Produção & Orquestração

---

# ✅ Atividade 19 — Orquestração

## Tecnologias

* Apache Airflow
  ou
* Prefect

---

# ✅ Atividade 20 — Pipeline Completa

## Fluxo final

```text id="2jlwm5"
Scraper
   ↓
Bronze
   ↓
Silver
   ↓
DBT
   ↓
Gold
   ↓
Analytics
```

---

# 🎯 Ordem Recomendada REAL

## Faça exatamente nesta sequência:

1. Endpoint discovery
2. Primeiro scraper
3. Bronze
4. Silver
5. Databricks
6. DBT
7. Gold KPIs
8. Analytics
9. Expansão de datasets
10. IA

---

# 🧠 Recomendação importante

## NÃO tente:

* coletar tudo no início
* modelar tudo
* prever jogos cedo demais

## Foque primeiro:

### `matches_by_date`

Essa será:

* sua tabela fato central
* a fundação do DBT
* a base dos KPIs
* a base futura de IA
