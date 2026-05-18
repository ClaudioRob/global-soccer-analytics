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

# 🚀 Roadmap do Projeto

## 📌 Fase 1 — Foundation & Data Ingestion

Construção da base do projeto e pipelines iniciais de coleta.

### Atividades

* Descoberta de endpoints internos do Sofascore
* Estruturação inicial do repositório
* Construção do primeiro scraper (`matches_by_date`)
* Implementação da camada Bronze (RAW JSON)
* Padronização de armazenamento e particionamento
* Primeira tabela Silver (`silver_matches`)
* Setup do ambiente no Databricks

---

## 📌 Fase 2 — Analytics Engineering

Construção da camada analítica utilizando dbt.

### Atividades

* Configuração do DBT
* Criação de modelos staging
* Criação de modelos Gold
* Construção de KPIs
* Testes de qualidade
* Geração de documentação e lineage

---

## 📌 Fase 3 — Exploratory Analytics

Exploração dos dados e geração de insights analíticos.

### Atividades

* EDA (Exploratory Data Analysis)
* KPIs de performance
* Rankings ofensivos e defensivos
* Comparações entre ligas e clubes
* Visualizações analíticas

---

## 📌 Fase 4 — Expansão de Dados

Ampliação do escopo de coleta e granularidade.

### Novos datasets

* Estatísticas avançadas
* Eventos por partida
* Dados de jogadores
* xG, posse de bola, finalizações e cartões

---

## 📌 Fase 5 — Inteligência Artificial

Aplicação de Machine Learning e modelos preditivos.

### Possibilidades

* Predição de resultados
* Predição de gols
* Clusterização de times
* Identificação de padrões táticos

---

## 📌 Fase 6 — Produção & Orquestração

Automação e operacionalização da plataforma.

### Atividades

* Orquestração de pipelines
* Execuções agendadas
* Processamento incremental
* Monitoramento e observabilidade

---

# 🏗️ Arquitetura Geral

```text id="g2t54o"
Sofascore
    ↓
Python Scraper
    ↓
Bronze Layer (RAW JSON)
    ↓
Silver Layer (Spark / Delta)
    ↓
DBT Models (Gold)
    ↓
Databricks Analytics
```

---

# ⚽ Dataset Inicial Prioritário

## `matches_by_date`

Este dataset será a fundação do projeto e alimentará:

* KPIs
* Modelos DBT
* Analytics
* Machine Learning futuro
