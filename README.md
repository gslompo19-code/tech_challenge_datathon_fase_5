# 💬 Análise de Sentimentos em Reclamações Financeiras com Deep Learning

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Deep%20Learning-orange)
![NLP](https://img.shields.io/badge/NLP-Text%20Classification-green)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-success)
![License](https://img.shields.io/badge/License-Acad%C3%AAmico-lightgrey)

Projeto desenvolvido para o **Datathon – Fase 5**, com foco em **Processamento de Linguagem Natural (PLN)** e **Deep Learning** para classificar narrativas de consumidores do setor financeiro em duas classes de sentimento:

- **Negativa**
- **Positiva**

Além da classificação, o projeto identifica as **principais dores dos clientes por categoria de produto**, transformando texto em insights de negócio.

---

## 🎯 Objetivo

Construir uma solução capaz de:

- tratar e preparar textos de reclamações
- criar uma variável alvo de sentimento
- treinar um modelo de **Deep Learning**
- avaliar o desempenho com métricas de classificação
- identificar os principais temas de insatisfação dos clientes

---

## 🧭 Definição das Classes

### 🔴 Negativa
Representa casos de **forte insatisfação do cliente**, geralmente associados a:

- cobranças indevidas
- fraude
- erro persistente
- ausência de resposta
- falhas não resolvidas
- prejuízo financeiro
- atendimento insatisfatório

### 🟢 Positiva
Neste projeto, a classe **Positiva não significa necessariamente elogio ou felicidade plena**.

Ela representa casos **não-negativos**, como:

- pedidos de esclarecimento
- dúvidas
- solicitações
- revisões administrativas
- relatos sem forte evidência de insatisfação intensa

Ou seja, a classe positiva foi tratada como **ausência de forte negatividade**, e não como entusiasmo explícito.

---

## 🛠️ Pipeline do Projeto

### 1. Pré-processamento textual
- remoção de ruídos, URLs, números e pontuação
- remoção seletiva de stopwords
- lematização
- preservação de palavras de negação (`not`, `no`, `never`)

### 2. Rotulagem heurística
Criação da coluna `sentimento` com base em:
- palavras-chave
- padrões linguísticos
- polaridade com **VADER**

### 3. Amostragem estratificada
Garante representatividade entre:
- categorias de produto
- classes de sentimento

### 4. Vetorização textual
- `Tokenizer`
- `pad_sequences`
- uso complementar de **TF-IDF** e **CountVectorizer** nas análises exploratórias

### 5. Tratamento do desbalanceamento
- **oversampling apenas no conjunto de treino**

### 6. Modelagem
- rede neural **BiLSTM**
- camada de embedding
- dropout
- saída sigmoide para classificação binária

### 7. Ajuste de threshold
- teste de diferentes limiares para melhorar o equilíbrio entre **precision**, **recall** e **F1-score**

---

## 🧠 Modelo Utilizado

A arquitetura principal foi uma **BiLSTM (Bidirectional LSTM)**, adequada para classificação de textos por capturar contexto em ambas as direções da sequência.

**Fluxo do modelo:**

`Texto tratado → Tokenização → Padding → Embedding → BiLSTM → Dropout → Dense → Saída Sigmoide`

---

## 📊 Resultados

### Resultado final do modelo
- **Accuracy:** `0.8988`
- **Precision:** `0.7553`
- **Recall:** `0.7117`
- **F1-score:** `0.7328`

### Relatório por classe
- **Negativa:** precision `0.93` | recall `0.94` | f1-score `0.94`
- **Positiva:** precision `0.76` | recall `0.71` | f1-score `0.73`

✅ Após os ajustes de pré-processamento e balanceamento, houve melhora importante na **precisão da classe positiva**, que era o principal ponto de atenção.

---

## 🔎 Principais Insights

A análise das reclamações negativas mostrou quatro grandes eixos de dor do cliente:

- **prejuízo financeiro percebido**
- **erros cadastrais ou informacionais**
- **falhas de atendimento e resolução**
- **desgaste relacional com a instituição**

### Exemplos por categoria
- **Cartão de crédito:** fraudes, cobranças indevidas, juros, bloqueios
- **Credit reporting:** dados incorretos, contas desconhecidas, score
- **Debt collection:** assédio, insistência, cobrança contestada
- **Hipotecas e empréstimos:** atraso, renegociação, falhas operacionais
- **Banco de varejo:** bloqueio de conta, erro em transações, suporte deficiente

---

## 📁 Estrutura do Repositório

```bash
.
├── data/
│   └── complaints_processed.csv
├── notebooks/
│   └── analise_sentimentos_fase5.ipynb
├── outputs/
│   ├── modelo/
│   │   ├── modelo_bilstm_sentimento.h5
│   │   └── tokenizer.pkl
│   └── graficos/
├── README.md
└── requirements.txt    '''

---

