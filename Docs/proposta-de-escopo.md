# 🧠 **Projeto: Global Football Analytics (via Web Scraping)**

## 🎯 Objetivo (atualizado)

Construir uma plataforma analítica baseada em dados de futebol global coletados via scraping do site Sofascore, permitindo:

* Coleta automatizada de dados
* Estruturação em modelo analítico
* Criação de KPIs avançados
* Análises exploratórias em notebooks
* Aplicação futura de IA

---

# ⚠️ **Observação importante (arquitetura realista)**

O Sofascore:

* NÃO é uma API pública oficial
* Usa chamadas internas (XHR / JSON)
* Possui proteção contra scraping agressivo

👉 **Boa notícia:**
É possível capturar dados estruturados via:

* Inspeção de requisições (Network tab)
* Endpoints JSON internos

👉 Isso evita scraping HTML pesado (melhor abordagem 👍)

---

# 🧱 **Arquitetura Geral (atualizada)**

```
[Sofascore]
     ↓
[Coleta - Scraper/API interna]
     ↓
[Bronze - JSON bruto]
     ↓
[Silver - dados tratados]
     ↓
[Gold - KPIs]
     ↓
[Databricks Notebook]
```

---

# 🧩 **Divisão por Módulos (estratégia do projeto)**

## 📦 Módulo 1 — Coleta de Dados (AGORA)

* Descobrir endpoints internos
* Construir scraper estruturado
* Salvar dados brutos

## 🧹 Módulo 2 — Transformação

* Normalizar dados
* Criar tabelas (matches, teams, stats)

## 📊 Módulo 3 — Análise

* KPIs
* EDA

## 🤖 Módulo 4 — IA (futuro)

* Previsões
* Clusterização

---

# 🚀 **MÓDULO 1 — ESCOPO DETALHADO (INICIAL)**

## 🎯 Objetivo

Construir pipeline de ingestão confiável a partir do Sofascore

---

## 🔍 1. Estratégia de Coleta

### ❌ NÃO fazer:

* Scraping direto de HTML (frágil e lento)

### ✅ FAZER:

Capturar endpoints internos JSON

Exemplo típico (descoberto via DevTools):

```
https://api.sofascore.com/api/v1/sport/football/events/live
```

Outros exemplos úteis:

* Jogos por data
* Estatísticas por jogo
* Times
* Rankings

---

## 🧪 2. Primeira coleta (MVP)

### 🎯 Caso inicial:

Coletar **jogos do dia**

---

## 🧾 Código inicial (Python)

```python
import requests
import json
from datetime import datetime

url = "https://api.sofascore.com/api/v1/sport/football/events/live"

headers = {
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(url, headers=headers)

data = response.json()

# salvar bronze
timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
file_name = f"bronze_live_matches_{timestamp}.json"

with open(file_name, "w") as f:
    json.dump(data, f)

print("Coleta concluída:", file_name)
```

---

# 🥉 **Camada Bronze (definição oficial)**

## 📁 Estrutura sugerida

```
/data/bronze/sofascore/
    /matches/
        /live/
        /by_date/
    /teams/
    /statistics/
```

---

# 🧹 **Preview da Transformação (Silver)**

Você vai extrair:

### 📊 Entidades principais:

* Match
* Team
* Tournament
* Score
* Status

---

## Exemplo de transformação:

```python
import pandas as pd

events = data.get("events", [])

rows = []

for e in events:
    rows.append({
        "match_id": e["id"],
        "tournament": e["tournament"]["name"],
        "home_team": e["homeTeam"]["name"],
        "away_team": e["awayTeam"]["name"],
        "home_score": e["homeScore"]["current"],
        "away_score": e["awayScore"]["current"],
        "status": e["status"]["type"]
    })

df = pd.DataFrame(rows)

df.head()
```

---

# ☁️ **Integração com Databricks**

## 🎯 Objetivo

Centralizar tudo em notebooks no Databricks

---

## Estrutura sugerida de notebooks:

### 📓 Notebook 1 — Ingestão

* scraping Sofascore
* salvar bronze

### 📓 Notebook 2 — Transformação

* parsing JSON
* gerar tabelas

### 📓 Notebook 3 — Análise

* KPIs
* visualizações

---

# 📊 **KPIs futuros (já preparando o terreno)**

* Win rate por time
* Média de gols
* Forma recente
* Ranking por performance
* Eficiência ofensiva/defensiva

---

# 🔒 **Boas práticas de scraping (importante)**

* Usar headers (User-Agent)
* Evitar muitas requisições simultâneas
* Implementar retry
* Implementar delay (`time.sleep`)

---

# 🧠 **Próximo passo recomendado (agora)**

Vamos evoluir de forma estruturada:

## 👉 Próxima etapa:

Escolher UM tipo de coleta inicial:

1. Jogos ao vivo (mais simples)
2. Jogos por data (melhor para histórico)
3. Detalhes de uma partida (mais rico)

---

💬 Me diga qual você prefere — eu posso:

* descobrir endpoints específicos
* montar scraper mais robusto
* já estruturar como pipeline (quase produção)

Se quiser um caminho ideal:
👉 recomendo começar com **jogos por data** (base histórica sólida)
