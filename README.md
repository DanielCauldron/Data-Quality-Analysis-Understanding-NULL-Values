# 📊 Análise de Qualidade de Dados — Churn Dataset

## 📌 Sobre o Projeto

Este projeto tem como foco a análise de qualidade de dados em um dataset de churn, com ênfase na identificação e interpretação de valores nulos (`NULL`) e seu impacto na confiabilidade das análises.

## 🎯 Objetivo

Demonstrar como a análise correta de valores nulos pode influenciar diretamente a qualidade dos dados e, consequentemente, a tomada de decisão em um contexto de negócio.

---

## 🧠 Problema Identificado

Durante a análise dos dados, foi identificado que a coluna **TotalCharges** apresentava valores nulos.

![Análise de valores nulos](https://github.com/user-attachments/assets/aa7c0e05-a87c-4e49-abbd-3e9a09109f82)

---

## 🔍 Análise Crítica

Nem todo valor nulo representa erro — a interpretação depende do contexto de negócio.

### ✅ Quando o `NULL` é válido

* Clientes com `tenure = 0`
* Indica que o cliente é novo
* Ainda não houve cobrança acumulada

📌 Neste cenário, o valor nulo é coerente e não deve ser tratado como erro.

---

### ⚠️ Quando o `NULL` é problema

* Clientes com `tenure > 0`
* Indica inconsistência nos dados

📌 Neste caso, o valor nulo compromete métricas importantes, como:

* Receita total
* Ticket médio
* Análise de churn

---

## 🛠️ Estratégia de Tratamento

Foi aplicada uma abordagem baseada em contexto de negócio, evitando substituições genéricas e garantindo maior confiabilidade dos dados.

### 📌 Regras Aplicadas

* Se `TotalCharges` for NULL e `tenure = 0`
  → Considerado **válido** (cliente novo)

* Se `TotalCharges` for NULL e `tenure > 0`
  → Considerado **problema de qualidade de dados**, sendo necessário tratamento

---

## 💻 Lógica Aplicada (DAX)

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
```

---

## 📊 Impacto no Negócio

Após o tratamento dos dados:

* Aumento da confiabilidade das informações
* Correção de KPIs relacionados à receita
* Melhoria na qualidade das análises de churn
* Apoio mais consistente à tomada de decisão

---

## 📈 Insights

* A presença de valores nulos nem sempre indica erro
* A interpretação correta depende do contexto de negócio
* A qualidade dos dados impacta diretamente a análise e os resultados

---

## 🚀 Tecnologias Utilizadas

* Power BI
* Power Query
* DAX

---

## 💡 Insight Principal

> Nem todo dado nulo é um erro.
> A interpretação correta depende do contexto de negócio.

---

## 👨‍💻 Autor

Daniel Caldeirão
