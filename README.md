<div align="center">

<a href="https://www.fiap.com.br/">
  <img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Administração Paulista" width="300px">
</a>

</div>

<br>

# 🌾 AgroScore — Predição e Prevenção de Sinistros em Equipamentos Agrícolas

## Grupo [Nome do Grupo]

## 👨‍🎓 Integrantes

- Renan Chaves Bezerra (RM573532)
- Lucas Henrique Aparecido Gomes de Mello (RM569583)
- Clarice Oliveira Barreto (RM571269)
- Kevin de Freitas Minervino (RM570667)

## 👩‍🏫 Professores

### Tutor(a)
- Sabrina Otoni — Turma B

### Coordenador(a)
- André Godoi Chiovato

---

## 📜 Descrição

O **AgroScore** é um sistema de apoio à decisão que utiliza dados climáticos, geográficos e operacionais para identificar, prever e reduzir riscos operacionais no uso de equipamentos agrícolas. O projeto foi desenvolvido no **Enterprise Challenge — FIAP 2026** em parceria com a **Sompo Seguros**.

Equipamentos agrícolas operam sob condições variáveis como chuva, tipo de solo, relevo e proximidade de água. Atualmente, as decisões são tomadas de forma **reativa**, após o problema já ter ocorrido — gerando tombamentos, atolamentos, derrapagens e custos elevados de indenização (colheitadeiras podem ultrapassar R$ 80 mil por sinistro). Na Região Sul, o risco é ainda maior devido a chuvas frequentes, solo argiloso e relevo acidentado.

O AgroScore calcula um **score de risco de 0 a 100** para cada operação, classificando-o em Baixo, Médio ou Alto risco, e transforma esse dado em uma **recomendação prática** para o operador. Para a seguradora, o sistema oferece padrões de risco por região e apoio à subscrição e precificação. O modelo preditivo principal é o **Random Forest**, treinado para prever a variável `sinistro (0 ou 1)` com base em variáveis climáticas, geográficas e operacionais, avaliado por métricas como Recall, F1-score e AUC-ROC.

> 📽️ **Vídeo de Apresentação:** [Inserir link aqui] *(até 5 minutos)*

---

## 📁 Estrutura de Pastas

Dentre os arquivos e pastas presentes na raiz do projeto, definem-se:

- **.github**: arquivos de configuração específicos do GitHub para gerenciar e automatizar processos no repositório.
- **assets**: arquivos relacionados a elementos não-estruturados do repositório, como imagens e logotipos.
- **config**: arquivos de configuração utilizados para definir parâmetros e ajustes do projeto (ex.: hiperparâmetros do modelo preditivo).
- **document**: documentos do projeto solicitados pelas atividades. Na subpasta `other`, documentos complementares e menos importantes.
- **scripts**: scripts auxiliares para tarefas específicas, como coleta de dados climáticos via API INMET, dados hidrológicos via ANA e geração do dataset simulado.
- **src**: todo o código-fonte criado ao longo das sprints, organizado em subpastas: `data/` (pipelines de ingestão e tratamento), `models/` (modelos preditivos), `analysis/` (notebooks de EDA) e `dashboard/` (interface Streamlit).
- **README.md**: arquivo que serve como guia e explicação geral sobre o projeto (o mesmo que você está lendo agora).

---

## 🔧 Como Executar o Código

> ⚠️ **Sprint 1 — Fase de Proposta:** nesta etapa não há código funcional. As instruções abaixo descrevem o ambiente planejado para as próximas sprints.

### Pré-requisitos

- Python 3.10+
- Bibliotecas: `pandas`, `numpy`, `scikit-learn`, `streamlit`, `requests`, `geopandas`

### Instalação (Sprint 2 em diante)

**Fase 1 — Configuração:**
```bash
git clone *https://github.com/1RenanBezerra/AgroScore*
cd AgroScore
pip install -r requirements.txt
```

**Fase 2 — Coleta de dados:**
```bash
python scripts/coleta_inmet.py       # Dados climáticos via INMET
python scripts/coleta_ana.py         # Dados hidrológicos via ANA
python scripts/gerar_dataset.py      # Geração do dataset simulado
```

**Fase 3 — Treinamento do modelo:**
```bash
python src/models/train.py
```

**Fase 4 — Dashboard:**
```bash
streamlit run src/dashboard/app.py
```
---

## 🔴 Problema

Equipamentos agrícolas operam sob condições variáveis como chuva, tipo de solo, relevo e proximidade de água. Atualmente, as decisões são tomadas de forma reativa, após o problema já ter ocorrido.

**Consequências:**
- Tombamentos, atolamentos e derrapagens
- Alto custo de indenização — colheitadeiras podem ultrapassar R$ 80 mil por sinistro
- Baixa previsibilidade de risco
- Dificuldade de correlacionar fatores ambientais com sinistros

Na **Região Sul do Brasil**, o risco é amplificado por chuvas frequentes, solo predominantemente argiloso e relevo acidentado — fatores que tornam a análise preditiva especialmente relevante.

---

## 💡 Solução

O AgroScore calcula um **score de risco (0 a 100)** para cada operação e transforma esse dado em uma recomendação prática, entregando:

| Saída | Descrição |
|-------|-----------|
| 📊 Score de risco | Valor numérico de 0 a 100 |
| 🟢🟡🔴 Classificação | Baixo (0–40), Médio (41–70), Alto (71–100) |
| 🔍 Principais fatores | Variáveis que mais influenciaram o score |
| 💡 Recomendação de ação | Orientação prática para o operador |

**Exemplo de saída do sistema:**
```
Equipamento : Trator A12
Região      : Chapecó (SC)
Score       : 82 / 100  →  🔴 ALTO RISCO

Fatores     : chuva acumulada, solo saturado, declividade
Recomendação: adiar operação
```

### Valor da Solução

**Para a operação:**
- Redução de decisões baseadas em intuição
- Prevenção de danos e interrupções

**Para a seguradora (Sompo):**
- Redução da frequência de sinistros
- Apoio à subscrição
- Melhor precificação de risco

---

## 👥 Usuários (Personas)

### 🧑‍🌾 Operador
- Precisa decidir rapidamente se deve operar ou não
- Necessita de alertas simples e acionáveis em linguagem direta

### 👨‍💼 Gestor de Frota
- Precisa monitorar múltiplos equipamentos simultaneamente
- Quer identificar onde o risco está maior para priorizar ações

### 🏢 Seguradora (Sompo)
- Precisa entender padrões de risco por região e tipo de operação
- Quer apoiar decisões de subscrição e gestão de carteira com dados

---

## 📋 User Stories

### US-01 — Alerta para o operador
> **Como** operador, **quero** receber um alerta simples de risco antes de iniciar a operação, **para** decidir com segurança se devo ou não operar naquele momento.

**Critérios de aceite:**
- Alerta disparado automaticamente quando score > 70
- Exibe os principais fatores de risco em linguagem simples
- Apresenta uma recomendação prática (ex.: "adiar operação")

---

### US-02 — Dashboard para o gestor
> **Como** gestor de frota, **quero** visualizar o risco de cada equipamento em um painel centralizado, **para** priorizar ações preventivas e alocar recursos com eficiência.

**Critérios de aceite:**
- Exibe lista de equipamentos com score atual e classificação de risco
- Permite filtro por região e nível de risco
- Mostra histórico de alertas dos últimos 30 dias

---

### US-03 — Análise de padrões para a seguradora
> **Como** analista da Sompo, **quero** analisar padrões de risco por região e tipo de operação, **para** melhorar a precificação e embasar decisões de subscrição com dados reais.

**Critérios de aceite:**
- Consulta histórica de score por equipamento, data e localização
- Exportação dos dados em CSV para análise interna
- Visualização de correlação entre score e sinistros registrados

---

### US-04 — Explicabilidade do score

> **Como** operador ou gestor, **quero** entender quais fatores geraram o score de risco, **para** saber o que monitorar ou mitigar antes de iniciar a operação.

**Critérios de aceite:**

- Exibe os top 3 fatores que mais influenciaram o score
- Mostra o peso relativo de cada fator (ex.: "chuva acumulada contribuiu com 38% do risco")

---

## 📊 Dados

A solução integra diferentes fontes de dados estruturadas em quatro categorias:

### Variáveis Principais

**Clima:**
| Variável | Descrição |
|----------|-----------|
| `precipitacao_mm` | Precipitação no momento (mm) |
| `umidade_ar_pct` | Umidade do ar (%) |
| `temperatura_c` | Temperatura (°C) |
| `vento_kmh` | Velocidade do vento (km/h) |

**Solo:**
| Variável | Descrição |
|----------|-----------|
| `tipo_solo` | Tipo do solo (argiloso, arenoso, misto) |
| `umidade_solo_pct` | Umidade do solo (%) |

**Geografia:**
| Variável | Descrição |
|----------|-----------|
| `declividade_graus` | Declividade do terreno (graus) |
| `distancia_agua_m` | Proximidade de água (m) |
| `area_alagavel` | Se a área é mapeada como alagável (0/1) |

**Operação:**
| Variável | Descrição |
|----------|-----------|
| `tipo_operacao` | Campo ou Transporte |
| `tipo_equipamento` | Trator, Colheitadeira, Pulverizador |
| `sinistro` | **Variável-alvo** — 0 ou 1 |

### Exemplo de Dataset Simulado

| equipamento | chuva_mm | umidade_solo | declividade | dist_agua_m | tipo_solo | operacao | sinistro | tipo_sinistro | custo_brl |
|-------------|----------|-------------|-------------|-------------|-----------|----------|---------|--------------|-----------|
| Trator | 78 | 88% | 18° | 120 | Argiloso | Campo | 1 | Atolamento | R$ 32.000 |
| Colheitadeira | 22 | 42% | 5° | 800 | Arenoso | Campo | 0 | — | — |
| Trator | 55 | 95% | 22° | 50 | Encharcado | Campo | 1 | Tombamento | R$ 65.000 |
| Pulverizador | 8 | 60% | 6° | 500 | Argiloso | Campo | 0 | — | — |
| Trator | 0 | 48% | 2° | 1500 | Rochoso | Transporte | 0 | — | — |
| Colheitadeira | 41 | 85% | 14° | 95 | Argiloso | Campo | 1 | Atolamento | R$ 47.000 |

> O dataset completo terá **500+ registros simulados** cobrindo diferentes combinações de fatores dos estados do PR, SC e RS.

### Fontes de Dados

| Fonte | Dado fornecido |
|-------|---------------|
| [INMET](https://portal.inmet.gov.br) | Clima (temperatura, chuva, vento, umidade) |
| [CPTEC/INPE](https://www.cptec.inpe.br) | Previsão do tempo e alertas climáticos |
| [ANA HidroWeb](https://www.snirh.gov.br/hidroweb) | Hidrografia, vazão e chuva acumulada |
| [IBGE](https://servicodados.ibge.gov.br) | Território, municípios e malha viária |
| [SRTM/NASA](https://earthexplorer.usgs.gov) | Relevo e declividade do terreno |
| [MapBiomas](https://mapbiomas.org) | Uso do solo e áreas alagáveis |

---

## 🤖 Modelo Preditivo

**Objetivo:** prever a probabilidade de ocorrência de sinistro em uma operação agrícola.

| Componente | Definição |
|-----------|-----------|
| Variável alvo | `sinistro` — 0 (sem sinistro) ou 1 (com sinistro) |
| Modelo principal | **Random Forest** |
| Baseline de comparação | Regressão Logística |
| Saída | Probabilidade de sinistro → score de risco (0–100) |
| Métricas de avaliação | Recall, F1-score, AUC-ROC |

**Justificativa do Random Forest:** lida bem com variáveis mistas (numéricas e categóricas), é robusto a outliers e entrega nativamente a importância de cada variável (feature importance) — essencial para explicar o score gerado.

**Métricas priorizadas:** o **Recall** é a métrica mais crítica do projeto — minimizar falsos negativos (sinistros não detectados) é mais importante do que minimizar falsos positivos, dado o alto custo de um sinistro não previsto.

---

## 🏗️ Arquitetura da Solução

```
┌──────────────────────────────────────────────────────────────┐
│               FONTES DE DADOS (APIs e bases públicas)        │
│   INMET · CPTEC/INPE · ANA · IBGE · SRTM/NASA · MapBiomas  │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────┐
│                   COLETA E PROCESSAMENTO                     │
│      Python (requests, pandas) · Scripts de ETL             │
│      Limpeza · Normalização · Criação de variáveis          │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────┐
│                   FEATURE ENGINEERING                        │
│   Índices parciais: risco_chuva · risco_relevo · risco_agua │
│   União das bases: clima + solo + geografia + operação      │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────┐
│                   MODELO PREDITIVO                           │
│   Random Forest (scikit-learn) · Baseline: Reg. Logística   │
│   Entrada: variáveis climáticas, geográficas, operacionais  │
│   Saída: probabilidade de sinistro                          │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────┐
│                   SCORE DE RISCO                             │
│   Probabilidade → score 0–100 → Baixo / Médio / Alto       │
│   Feature importance → top 3 fatores → recomendação        │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────┐
│               ALERTAS E DASHBOARD (Streamlit)                │
│   Painel Operador · Dashboard Gestor · Painel Sompo         │
└──────────────────────────────────────────────────────────────┘
```

| Componente | Tecnologia |
|-----------|-----------|
| Coleta de dados | Python + `requests` |
| Processamento e ETL | Pandas + NumPy |
| Análise exploratória | Jupyter Notebook |
| Modelo preditivo | Scikit-learn (Random Forest) |
| Dashboard e alertas | Streamlit |
| Controle de versão | GitHub |

---

## 🖥️ Interface

- **Dashboard para gestores:** visão consolidada de todos os equipamentos com score, classificação e histórico de alertas
- **Alertas simples para operadores:** notificação direta com nível de risco e recomendação prática em linguagem acessível
- **Visualização por equipamento, região e nível de risco:** filtros e mapa geoespacial com marcadores coloridos por nível de risco

---

## 🔒 Segurança

| Princípio | Aplicação |
|-----------|-----------|
| Controle de acesso por perfil | Permissões distintas para operador, gestor e seguradora |
| Separação entre dados individuais e agregados | Dados por equipamento isolados de análises gerais da carteira |
| Dados anonimizados para a seguradora | Informações sensíveis do segurado protegidas na camada de relatórios |
| Integridade | Logs de inserção e modificação de dados com timestamp |
| Disponibilidade | Fallback para dados cacheados em caso de falha nas APIs externas |

---

## 🗃 Histórico de Lançamentos

- **0.1.0** — Sprint 1: Proposta técnica documentada (problema, solução, dados, arquitetura e modelo)
- **0.2.0** — Sprint 2: Coleta de dados reais/simulados e análise exploratória *(previsto)*
- **0.3.0** — Sprint 3: Modelo preditivo treinado e sistema de score funcional *(previsto)*
- **0.4.0** — Sprint 4: Dashboard Streamlit integrado com alertas *(previsto)*
- **0.5.0** — Sprint 5: MVP completo, testes e apresentação final *(previsto)*

---

## 📅 Planejamento das Próximas Etapas

### Sprint 2 — Dados e Análise Exploratória

| Tarefa | Responsável |
|--------|------------|
| Coleta de dados climáticos via INMET e CPTEC/INPE | [Integrante] |
| Coleta de dados de relevo e solo (SRTM/NASA + MapBiomas) | [Integrante] |
| Geração do dataset simulado com 500+ registros | [Integrante] |
| Análise exploratória: correlações e padrões por região | [Integrante] |
| Notebook de EDA documentado | [Integrante] |

### Sprint 3 — Modelagem Preditiva

| Tarefa | Responsável |
|--------|------------|
| Pré-processamento e feature engineering | [Integrante] |
| Treinamento do modelo Random Forest | [Integrante] |
| Avaliação de métricas (Recall, F1-score, AUC-ROC) | [Integrante] |
| Implementação do score de risco (0–100) | [Integrante] |
| Feature importance e explicabilidade do score | [Integrante] |

### Sprint 4 — Interface e Protótipo Funcional

| Tarefa | Responsável |
|--------|------------|
| Dashboard em Streamlit para gestores | [Integrante] |
| Painel de alerta para operadores | [Integrante] |
| Integração modelo preditivo + interface | [Integrante] |
| Mapa geoespacial com níveis de risco | [Integrante] |
| Testes com as personas e ajustes finais | Todos |

### Sprint 5 — MVP e Apresentação Final

| Tarefa | Responsável |
|--------|------------|
| Integração completa de todos os componentes | Todos |
| Testes de desempenho e validação do modelo | [Integrante] |
| Documentação final do repositório | [Integrante] |
| Gravação do vídeo de demonstração | Todos |

---

## 💻 Tecnologias

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 📋 Licença

<a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1">
  <img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" height="22">
  <img src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" height="22">
</a>

[MODELO GIT FIAP](https://github.com/agodoi/template) por [FIAP](https://fiap.com.br) está licenciado sob [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1).
