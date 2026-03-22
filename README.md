# 📊 Análise de Qualidade de Dados – Churn Dataset

## 🎯 Objetivo
Demonstrar a importância da análise de dados nulos (`null`) e como sua interpretação correta impacta diretamente a confiabilidade das análises no Power BI.

---

## 🧠 Problema Identificado

Durante a análise dos dados, foi identificado que a coluna **TotalCharges** apresentava valores nulos.

<img width="1474" height="436" alt="null-analysis png" src="https://github.com/user-attachments/assets/aa7c0e05-a87c-4e49-abbd-3e9a09109f82" />

---

## 🔍 Análise Crítica

Nem todo valor nulo representa erro.

### ✅ Quando o `null` é CORRETO
- Clientes com `tenure = 0`
- Indica que o cliente é novo
- Ainda não houve cobrança acumulada

👉 Nesse caso, o `TotalCharges` nulo faz sentido do ponto de vista de negócio.

---

### ⚠️ Quando o `null` é PROBLEMA
- Clientes com `tenure > 0`
- Indica falha no dado

👉 Aqui o dado precisa ser tratado, pois impacta métricas como:
- Receita total
- Ticket médio
- Análise de churn

---

## 🛠️ Solução Aplicada

Foi realizada uma abordagem baseada em contexto:

- Validação dos dados
- Identificação de inconsistências
- Tratamento condicional dos valores nulos

### Exemplo de regra aplicada:

Se TotalCharges for null e tenure = 0 → manter como válido
Se TotalCharges for null e tenure > 0 → tratar/reconstruir

---

## 🛠️ Estratégia de Tratamento de Dados

O tratamento dos valores nulos na coluna **TotalCharges** foi realizado com base no contexto de negócio, evitando substituições genéricas.

### 📌 Regras Aplicadas

- Se `TotalCharges` for null e `tenure = 0`  
  → Considerado **válido** (cliente novo, sem cobrança acumulada)

- Se `TotalCharges` for null e `tenure > 0`  
  → Considerado **problema de qualidade de dados**, sendo necessário tratamento ou reconstrução

---

### 💻 Lógica Aplicada (DAX)

```DAX
TotalCharges_Ajustado = 
IF(
    ISBLANK('Tabela'[TotalCharges]) && 'Tabela'[tenure] = 0,
    0,
    IF(
        ISBLANK('Tabela'[TotalCharges]) && 'Tabela'[tenure] > 0,
        'Tabela'[MonthlyCharges] * 'Tabela'[tenure],
        'Tabela'[TotalCharges]
    )
)

💡 Insight Principal



```
---

## 📊 Impacto no Negócio

Após o tratamento:

- Dados mais confiáveis
- KPIs corrigidos
- Melhor tomada de decisão

---

## 🚀 Tecnologias Utilizadas

- Power BI
- Power Query
- DAX

---

## 💡 Insight Principal

> Nem todo dado nulo é um erro.  
> A interpretação correta depende do contexto de negócio.

---

## 👨‍💻 Autor

Daniel Caldeirão


