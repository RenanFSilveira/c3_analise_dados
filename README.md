# 🏠 Análise e Predição de Preços de Imóveis nos EUA — Projeto Final (Desafio C3)

Projeto acadêmico de **Análise de Dados e Machine Learning** sobre a base
*House Prices - Advanced Regression Techniques* (Kaggle / Ames, Iowa).
Percorre todo o ciclo de um projeto de dados — da análise exploratória aos modelos
supervisionados e não supervisionados — com foco em **storytelling** e boas práticas.

> **Disciplina:** Análise de Dados e Machine Learning · **Instituição:** FAESA Centro Universitário

---

## 📂 Estrutura do repositório

```
projeto_final/
├── data/
│   └── train.csv                          # 1460 imóveis × 81 variáveis
├── notebooks/
│   ├── projeto_final_house_prices.ipynb   # notebook principal (executado, com gráficos)
│   └── projeto_final_house_prices.html    # versão HTML para leitura/apresentação
├── requirements.txt
└── README.md
```

## 🚀 Como executar

```bash
pip install -r requirements.txt
jupyter notebook notebooks/projeto_final_house_prices.ipynb
```

Para rodar tudo de uma vez (embute saídas e gráficos no arquivo):

```bash
python -m nbconvert --to notebook --execute --inplace notebooks/projeto_final_house_prices.ipynb
```

---

## 🧪 Metodologia (inspirada no CRISP-DM)

| # | Etapa | Técnicas |
|---|-------|----------|
| 1 | **Análise Exploratória (EDA)** | distribuição da target, faltantes, correlações, outliers |
| 2 | **Feature Engineering** | tratamento de NaN, novas features, **codificação híbrida** (ordinal + one-hot), `log1p` da target |
| 3 | **Regressão** | Linear Simples e Múltipla, Random Forest, Gradient Boosting |
| 4 | **Classificação** | Regressão Logística e Random Forest (caro × barato) |
| 5 | **Clusterização** | K-Means (cotovelo + silhouette) |
| 6 | **Redução de dimensionalidade** | PCA (variância + **loading plot**) e t-SNE |
| 7 | **Associação e Outliers** | Apriori (regras enxutas) e Local Outlier Factor (LOF) |
| 8 | **Comparação e conclusões** | painel-resumo, limitações e trabalhos futuros |

**Destaque técnico — codificação híbrida:** variáveis **ordinais** (qualidade, acabamento)
recebem mapeamento numérico que **preserva a ordem**, enquanto as **nominais** (bairro, tipo
de telhado) usam **one-hot encoding**. É a abordagem correta para este dataset.

---

## 📊 Principais resultados

**Regressão** (alvo = `log(SalePrice)`):

| Modelo | RMSE (log) | R² |
|---|---|---|
| **Gradient Boosting** 🏆 | ~0.125 | **~0.91** |
| Linear Múltipla | ~0.13 | ~0.90 |
| Random Forest | ~0.15 | ~0.87 |

**Classificação** (caro × barato, limiar = mediana ≈ US$ 163.000):
modelos atingem **F1 e AUC-ROC altos** (acurácia ~0,90).

**Não supervisionado:** K-Means revelou **4 perfis de imóveis**; PCA mostra que ~33
componentes explicam 90% da variância numérica; o loading plot evidencia que **área e
qualidade** dominam o 1º componente; o Apriori confirmou regras intuitivas
(*qualidade alta → preço alto*) e o LOF isolou **73 imóveis atípicos (5%)**.

---

## 🧠 Insights de negócio

- **Qualidade geral** (`OverallQual`) e **área total** (`TotalSF`) são os principais
  determinantes do preço.
- Variáveis criadas na engenharia de atributos (`TotalSF`, `HouseAge`, `TotalBath`)
  ficaram entre as mais importantes dos modelos.
- Modelos de *ensemble* explicam **~90% da variação** do preço, superando o modelo linear simples.

## ⚠️ Limitações e trabalhos futuros

- Base de uma **única cidade/período** → generalização limitada.
- Avaliação por *hold-out* 80/20, sem *k-fold* nem otimização de hiperparâmetros.
- **Próximos passos:** validação cruzada + *Grid/Random Search*, *boosting* avançado
  (XGBoost/LightGBM), *stacking* e enriquecimento com dados externos.

---

## 🛠️ Tecnologias

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · mlxtend (Apriori)
