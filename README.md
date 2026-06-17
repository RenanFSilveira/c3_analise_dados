# Análise e predição de preços de imóveis nos EUA (Desafio C3)

Projeto acadêmico de Análise de Dados e Machine Learning sobre a base
*House Prices - Advanced Regression Techniques* (Kaggle / Ames, Iowa). O trabalho
percorre todo o ciclo de um projeto de dados, da análise exploratória aos modelos
supervisionados e não supervisionados.

**Integrantes:** Renan Fortunato Silveira e Thiago Rosetti Miranda
**Instituição:** FAESA Centro Universitário

## Estrutura do repositório

```
projeto_final/
├── data/
│   └── train.csv                          # 1460 imóveis x 81 variáveis
├── notebooks/
│   ├── projeto_final_house_prices.ipynb   # notebook principal (executado, com gráficos)
│   └── projeto_final_house_prices.html    # versão HTML para leitura e apresentação
├── requirements.txt
└── README.md
```

## Como executar

```bash
pip install -r requirements.txt
jupyter notebook notebooks/projeto_final_house_prices.ipynb
```

Para rodar tudo de uma vez e embutir as saídas e os gráficos no arquivo:

```bash
python -m nbconvert --to notebook --execute --inplace notebooks/projeto_final_house_prices.ipynb
```

## Metodologia

O projeto segue um fluxo inspirado no CRISP-DM:

| # | Etapa | Técnicas |
|---|-------|----------|
| 1 | Análise exploratória (EDA) | distribuição da variável-alvo, faltantes, correlações, outliers |
| 2 | Feature engineering | tratamento de NaN, novas variáveis, codificação híbrida (ordinal e one-hot), `log1p` da target |
| 3 | Regressão | Linear simples e múltipla, Random Forest, Gradient Boosting |
| 4 | Classificação | Regressão Logística e Random Forest (caro ou barato) |
| 5 | Clusterização | K-Means (cotovelo e silhouette) |
| 6 | Redução de dimensionalidade | PCA (variância e loading plot) e t-SNE |
| 7 | Associação e outliers | Apriori (regras enxutas) e Local Outlier Factor (LOF) |
| 8 | Comparação e conclusões | painel-resumo, limitações e trabalhos futuros |

Sobre a codificação híbrida: as variáveis ordinais (qualidade, acabamento) recebem um
mapeamento numérico que preserva a ordem, enquanto as nominais (bairro, tipo de telhado)
recebem one-hot encoding. É a abordagem adequada para este dataset.

## Principais resultados

Regressão (alvo = `log(SalePrice)`):

| Modelo | RMSE (log) | R² |
|---|---|---|
| Gradient Boosting | ~0.125 | ~0.91 |
| Linear múltipla | ~0.13 | ~0.90 |
| Random Forest | ~0.15 | ~0.87 |

Na classificação (caro ou barato, limiar igual à mediana de cerca de US$ 163.000), os
modelos chegaram a F1 e AUC-ROC altos, com acurácia em torno de 0,90.

Nos métodos não supervisionados, o K-Means revelou 4 perfis de imóveis. No PCA, cerca de
33 componentes explicam 90% da variância numérica, e o loading plot evidencia que área e
qualidade dominam o primeiro componente. O Apriori confirmou regras intuitivas, como
qualidade alta associada a preço alto, e o LOF isolou 73 imóveis atípicos (5%).

## Insights de negócio

Qualidade geral (`OverallQual`) e área total (`TotalSF`) são os principais fatores que
determinam o preço. As variáveis criadas na engenharia de atributos (`TotalSF`, `HouseAge`,
`TotalBath`) ficaram entre as mais importantes dos modelos. Os modelos de *ensemble*
explicam cerca de 90% da variação do preço e superam o modelo linear simples.

## Limitações e trabalhos futuros

A base é de uma única cidade e período, o que limita a generalização. A avaliação usou
apenas *hold-out* 80/20, sem validação cruzada *k-fold* nem otimização de hiperparâmetros.
Como próximos passos: validação cruzada com *Grid* ou *Random Search*, boosting mais
avançado (XGBoost, LightGBM), *stacking* de modelos e enriquecimento com dados externos.

## Tecnologias

Python, pandas, NumPy, scikit-learn, matplotlib, seaborn e mlxtend (Apriori).
