# 📘 Documentação do Projeto — Global Football Analytics Platform

## 🎯 Visão Geral

O projeto tem como objetivo construir uma plataforma moderna de engenharia e análise de dados focada em futebol global, utilizando dados coletados do portal [Sofascore](https://www.sofascore.com/?utm_source=chatgpt.com) através de técnicas de web scraping e consumo de endpoints JSON internos.

A plataforma será construída de forma modular, utilizando arquitetura Lakehouse, notebooks analíticos no Databricks e transformação analítica com dbt.

---

# ⚽ Objetivos do Projeto

A solução permitirá:

* Coleta automatizada de dados de futebol global
* Armazenamento de dados brutos (raw)
* Transformação e normalização de dados
* Construção de métricas e KPIs
* Análises exploratórias em notebooks
* Estruturação de pipeline moderno de dados
* Evolução futura para Machine Learning e IA

---

# 🧠 Escopo Atual

## 📦 Módulo 1 — Ingestão de Dados

Responsável pela coleta de dados do Sofascore.

### Objetivos:

* Descoberta de endpoints internos JSON
* Extração automatizada de dados
* Armazenamento da camada Bronze
* Construção de pipelines iniciais

### Tecnologias:

* Python
* requests
* Databricks Notebook

---

## 🧹 Módulo 2 — Transformação (Silver Layer)

Responsável pelo tratamento e estruturação dos dados.

### Objetivos:

* Parsing de JSON
* Flatten de estruturas aninhadas
* Padronização de schemas
* Criação de tabelas Delta

### Tecnologias:

* PySpark
* Delta Lake
* Databricks

---

## 📊 Módulo 3 — Analytics Engineering (DBT)

Responsável pela modelagem analítica e KPIs.

### Objetivos:

* Construção de modelos analíticos
* Criação de métricas
* Testes de qualidade
* Lineage
* Documentação automática

### Tecnologias:

* dbt
* Databricks SQL
* Delta Tables

---

## 📈 Módulo 4 — Analytics & Exploration

Responsável pela análise exploratória e geração de insights.

### Objetivos:

* EDA (Exploratory Data Analysis)
* Criação de KPIs
* Visualizações
* Estudos comparativos entre ligas e clubes

### Tecnologias:

* Databricks Notebook
* Python
* Pandas
* Matplotlib / Plotly

---

## 🤖 Módulo 5 — Inteligência Artificial (Futuro)

Responsável por análises preditivas e modelos avançados.

### Possibilidades:

* Predição de resultados
* Predição de gols
* Clusterização de times
* Detecção de padrões táticos
* Ranking global de clubes

---

# 🏗️ Arquitetura da Plataforma

```text
                ┌──────────────────┐
                │    Sofascore     │
                └────────┬─────────┘
                         │
                         ▼
              ┌────────────────────┐
              │ Python Scraper/API │
              └────────┬───────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ Bronze Layer (RAW) │
              │ JSON Files         │
              └────────┬───────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ Silver Layer       │
              │ Spark Transform    │
              └────────┬───────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ DBT Models         │
              │ Gold Layer         │
              └────────┬───────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ Databricks         │
              │ Analytics          │
              └────────────────────┘
```

---

# ☁️ Stack Tecnológica

| Camada                | Tecnologia        |
| --------------------- | ----------------- |
| Coleta                | Python + requests |
| Processamento         | PySpark           |
| Lakehouse             | Delta Lake        |
| Orquestração (futuro) | Apache Airflow    |
| Analytics Engineering | dbt               |
| Analytics             | Databricks        |
| Armazenamento         | DBFS / S3 / ADLS  |

---

# 🥉 Bronze Layer (RAW)

## Objetivo

Armazenar dados brutos exatamente como recebidos.

## Formato

* JSON

## Estrutura sugerida

```text
/data/bronze/sofascore/
    /matches/
        /live/
        /by_date/
    /teams/
    /statistics/
```

---

# 🥈 Silver Layer

## Objetivo

Estruturar e normalizar os dados.

## Entidades iniciais

### `silver_matches`

* match_id
* match_date
* tournament
* season
* home_team
* away_team
* home_score
* away_score
* status

---

### `silver_teams`

* team_id
* team_name
* country
* tournament

---

### `silver_tournaments`

* tournament_id
* tournament_name
* country

---

# 🥇 Gold Layer (DBT)

## Objetivo

Criar modelos analíticos e KPIs.

## Exemplos de modelos

### `gold_team_performance`

* partidas
* vitórias
* derrotas
* média de gols

---

### `gold_recent_form`

* desempenho últimos 5 jogos
* sequência de vitórias
* aproveitamento recente

---

### `gold_scoring_efficiency`

* gols por finalização
* eficiência ofensiva

---

# 🧪 Qualidade e Governança

## Estratégia

Utilizar testes no DBT para garantir consistência.

## Exemplos

* `match_id` unique
* scores >= 0
* times não nulos

---

# 📚 Documentação e Lineage

O DBT será utilizado para:

* geração automática de documentação
* lineage de tabelas
* rastreabilidade de transformações

---

# 📓 Estrutura de Notebooks

## Notebook 01 — Ingestão

Responsável pelo scraping e carga Bronze.

---

## Notebook 02 — Silver Processing

Responsável pela transformação e normalização.

---

## Notebook 03 — DBT Analytics

Responsável pelos modelos analíticos.

---

## Notebook 04 — Exploratory Analytics

Responsável pelas análises e visualizações.

---

# 📊 KPIs Planejados

## Times

* Win rate
* Média de gols
* Aproveitamento
* Forma recente

---

## Campeonatos

* Média de gols por liga
* Competitividade
* Eficiência ofensiva

---

## Jogadores (futuro)

* Participação em gols
* Eficiência ofensiva
* Performance por posição

---

# 🔒 Boas Práticas

## Scraping

* Uso de User-Agent
* Retry strategy
* Controle de rate limit
* Delay entre requests

---

## Engenharia

* Separação Bronze/Silver/Gold
* Versionamento Git
* Modelagem incremental
* Pipelines idempotentes

---

# 🚀 Próximo Passo do Projeto

## Fase Atual

### Descoberta e construção da primeira ingestão:

* Jogos por data (`matches_by_date`)

## Próximas entregas

1. Descobrir endpoints Sofascore
2. Criar scraper robusto
3. Estruturar camada Bronze
4. Construir primeira tabela Silver
5. Configurar DBT no Databricks
6. Criar primeiros KPIs analíticos
