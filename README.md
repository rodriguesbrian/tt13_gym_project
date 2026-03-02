# Model Fitness – Predição de Rotatividade e Estratégia de Retenção

Este projeto analisa dados de clientes da rede **Model Fitness** para prever churn, identificar perfis comportamentais e desenvolver uma estratégia de retenção baseada em evidências.

A questão central é:

> Quem vai sair no próximo mês — e o que fazer antes que isso aconteça?

---

# 🎯 Objetivos

- Predizer a probabilidade de churn no próximo mês.
- Identificar segmentos comportamentais distintos.
- Determinar fatores mais associados à rotatividade.
- Formular recomendações práticas de retenção.

---

# 📂 Base de Dados

Arquivo:

`/datasets/gym_churn_us.csv`

Variável alvo:
- `Churn` — 1 = saiu; 0 = permaneceu

Principais variáveis:

**Perfil e histórico**
- gender
- Near_Location
- Partner
- Promo_friends
- Phone
- age
- Lifetime

**Contrato e comportamento**
- Contract_period
- Month_to_end_contract
- Group_visits
- Avg_class_frequency_total
- Avg_class_frequency_current_month
- Avg_additional_charges_total

---

# 1️⃣ Preparação dos Dados

- Verificação de valores ausentes
- Conversão de tipos
- Checagem de duplicatas
- Padronização de variáveis categóricas
- Análise inicial com `describe()`

Validação da distribuição da variável `Churn`.

---

# 2️⃣ Análise Exploratória (EDA)

---

## 📊 Estatísticas Descritivas

- Média e desvio padrão
- Comparação entre:
  - Clientes que ficaram
  - Clientes que saíram (`groupby(Churn)`)

Objetivo:
Identificar diferenças estruturais iniciais.

---

## 📊 Distribuições por Churn

Histogramas comparando:

- Frequência atual
- Frequência total
- Lifetime
- Idade
- Gastos adicionais

Padrões esperados:

- Frequência atual baixa → maior churn
- Lifetime curto → maior churn
- Contratos curtos → maior churn

---

## 🔗 Matriz de Correlação

Heatmap de correlação.

Objetivo:

- Identificar variáveis altamente correlacionadas
- Detectar redundâncias
- Observar associação com `Churn`

---

# 3️⃣ Modelo de Predição de Churn

Problema: classificação binária.

---

## 📌 Separação de Dados

- `train_test_split()`
- `random_state` fixado
- 70% treino / 30% validação

---

## 📌 Modelos Treinados

### 1. Regressão Logística
- Interpretação clara dos coeficientes
- Bom baseline

### 2. Random Forest
- Captura relações não lineares
- Robusto a interações complexas

---

## 📊 Métricas Avaliadas

- Acurácia
- Precisão
- Sensibilidade (Recall)

Comparação:

Qual modelo detecta melhor clientes que irão sair?

Em churn, recall costuma ser mais crítico que acurácia.

---

# 4️⃣ Segmentação de Clientes

Objetivo:
Identificar perfis comportamentais distintos.

---

## 📌 Padronização

Uso de `StandardScaler`.

---

## 📌 Dendrograma (linkage)

- Método hierárquico
- Estimativa visual do número ideal de clusters

---

## 📌 K-Means (n = 5)

- Treinamento
- Atribuição de cluster a cada cliente

---

## 📊 Análise dos Clusters

Para cada cluster:

- Média das variáveis
- Taxa de churn (`groupby(cluster).mean()`)

Perguntas-chave:

- Quais clusters têm churn alto?
- O que diferencia clientes leais?
- Existe cluster de alto valor com risco elevado?

---

# 📊 Padrões Comportamentais Observáveis

Exemplos típicos esperados:

- Cluster 1: Contratos longos, alta frequência, baixo churn
- Cluster 2: Contrato mensal, baixa frequência atual, alto churn
- Cluster 3: Alto gasto adicional, moderado churn
- Cluster 4: Novos clientes, alta incerteza
- Cluster 5: Parceiros corporativos, retenção alta

---

# 5️⃣ Fatores Mais Impactantes no Churn

Com base em:

- Coeficientes da regressão
- Importância de variáveis na Random Forest
- Diferenças entre clusters

Fatores geralmente críticos:

- Avg_class_frequency_current_month
- Contract_period
- Month_to_end_contract
- Lifetime

---

# 🧠 Conclusões Estratégicas

---

## 🎯 1. Identificação de Grupo de Risco

Clientes com:

- Frequência atual baixa
- Contrato curto
- Baixo tempo de casa

São candidatos prioritários para intervenção.

---

## 🎯 2. Incentivar Contratos Mais Longos

Contratos de 6 ou 12 meses apresentam churn significativamente menor.

Estratégia:
- Ofertas de upgrade antes do vencimento.

---

## 🎯 3. Intervenção Baseada em Queda de Frequência

Criar alerta automático:

Se frequência cair X% no mês → disparar ação:
- Contato personalizado
- Benefício temporário
- Sessão gratuita

---

## 🎯 4. Incentivar Engajamento Social

Clientes que participam de aulas em grupo tendem a permanecer mais.

Estratégia:
- Oferecer aulas gratuitas no primeiro mês.
- Criar eventos exclusivos para membros ativos.

---

# 📌 Resultado Final

Notebook estruturado contendo:

- Análise exploratória completa
- Modelos preditivos comparados
- Segmentação comportamental
- Taxa de churn por cluster
- Recomendações práticas de retenção

---

# 📦 Como Executar

1. Clone o repositório:

```bash
git clone https://github.com/rodriguesbrian/tt13_gym_project
cd tt13_gym_project