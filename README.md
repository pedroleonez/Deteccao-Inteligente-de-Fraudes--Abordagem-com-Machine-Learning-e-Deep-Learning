# Detecção Inteligente de Fraudes: Abordagem com Machine Learning e Deep Learning

Este projeto consiste em um pipeline completo de ciência de dados para a detecção de fraudes em transações de cartões de crédito. O desafio central é o desequilíbrio extremo das classes, onde apenas **0,172%** das transações são fraudulentas. A solução utiliza uma abordagem híbrida de **Ensemble Learning**, combinando **XGBoost** e **Redes Neurais**.

## 📊 Visão Geral do Projeto

A segurança financeira depende da identificação de anomalias em tempo real. Este projeto foca na maximização do **AUPRC** (Area Under the Precision-Recall Curve) e do **F1-Score**, garantindo que o sistema seja seguro para a instituição e fluido para o cliente legítimo.

### 🔗 Base de Dados
O dataset utilizado contém transações feitas por cartões de crédito em setembro de 2013 por titulares europeus. Devido a questões de confidencialidade, as variáveis passaram por uma transformação PCA.
- **Fonte:** [Kaggle - Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)

## 🛠️ Tecnologias e Ferramentas
- **Linguagem:** Python
- **Manipulação e Visualização:** Pandas, NumPy, Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn, XGBoost
- **Deep Learning:** TensorFlow, Keras
- **Processamento de Dados Desbalanceados:** Imbalanced-learn (SMOTE)

## 🚀 Metodologia

### 1. Pré-processamento e Escalonamento
Para lidar com *outliers* e escalas distintas nas variáveis `Time` e `Amount`, foi utilizado o **RobustScaler**, que baseia o escalonamento na mediana e nos quartis.

### 2. Tratamento de Desbalanceamento
Utilizamos a técnica **SMOTE** (*Synthetic Minority Over-sampling Technique*) apenas nos dados de treino para criar exemplos sintéticos da classe minoritária, permitindo que o modelo aprenda os padrões de fraude sem "decorar" os dados originais.

### 3. Modelagem Híbrida (Ensemble)
Foi implementado um **Ensemble de Média Ponderada**:
- **XGBoost (Peso 0.4):** Excelente na captura de relações tabulares e interações complexas.
- **Rede Neural MLP (Peso 0.6):** Alta capacidade de processamento não-linear e generalização.

A probabilidade final é calculada por:  
$$P_{\text{final}} = (P_{\text{XGBoost}} \times 0.4) + (P_{\text{RedeNeural}} \times 0.6)$$

### 4. Otimização de Limiar (Threshold)
O limiar de decisão foi elevado para **0.7**, focando em aumentar a confiança dos alertas e reduzir o número de clientes legítimos bloqueados injustamente.

## 📈 Resultados e Impacto no Negócio

O modelo final atingiu métricas de estado da arte para este dataset:

| Métrica | Resultado |
| :--- | :--- |
| **Precisão** | 65% |
| **Recall (Sensibilidade)** | 86% |
| **F1-Score** | 0.74 |

### Análise de ROI (Retorno sobre Investimento)
Considerando premissas de mercado (R$ 500 de economia por fraude detectada e R$ 10 de custo por falso alarme):
- **Fraudes bloqueadas:** 84
- **Alarmes falsos:** 45
- **Economia Líquida Gerada: R$ 41.550,00**

O sistema demonstrou ser altamente lucrativo, onde a economia gerada supera em quase **100 vezes** os custos operacionais.

## 📋 Como executar
1. Clone o repositório.
2. Certifique-se de ter as bibliotecas instaladas:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost tensorflow imbalanced-learn