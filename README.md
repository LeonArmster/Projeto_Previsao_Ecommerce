# Projeto -- Previsão de Compras em E-Commerce

Autor: Leonardo Souza
Data Criação: 07/03

## 1. Visão Geral

Este projeto tem como objetivo analisar o comportamento de usuários em
sessões de um site de comércio eletrônico e construir um **modelo
preditivo capaz de estimar a probabilidade de um visitante realizar uma
compra**.

A análise foi realizada utilizando o dataset **Online Shoppers
Purchasing Intention Dataset**, que contém informações sobre **12.330
sessões de navegação**, com atributos comportamentais e técnicos
coletados durante a navegação.

O projeto inclui:

-   Análise exploratória de dados
-   Engenharia de atributos
-   Balanceamento de classes
-   Treinamento de modelos de Machine Learning
-   Otimização de hiperparâmetros
-   Avaliação de desempenho
-   Identificação das variáveis mais importantes para a previsão de
    compra

------------------------------------------------------------------------

# 2. Objetivo do Projeto

O objetivo deste projeto é:

1.  **Identificar os três atributos que mais influenciam a decisão de
    compra de um usuário.**
2.  **Construir um modelo preditivo capaz de prever se uma sessão
    resultará em compra.**
3.  **Comparar diferentes configurações de modelos para validar a
    robustez da solução.**

Como solicitado pelo responsável pelo projeto, foi construída **uma
tabela comparativa com múltiplos testes de modelos**, permitindo validar
o desempenho obtido.

------------------------------------------------------------------------

# 3. Fonte dos Dados

Dataset utilizado:

Online Shoppers Purchasing Intention Dataset

Fonte:
https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset

O conjunto de dados contém **12.330 sessões de navegação**, cada uma
pertencente a um usuário diferente ao longo de **um período de 1 ano**.

Essa estrutura foi projetada para evitar viés relacionado a:

-   campanhas específicas
-   datas promocionais
-   comportamento recorrente do mesmo usuário

------------------------------------------------------------------------

# 4. Estrutura dos Dados

O dataset possui:

-   **10 variáveis numéricas**
-   **8 variáveis categóricas**
-   **1 variável alvo**

Variável alvo:

**Revenue**

-   True → sessão gerou compra
-   False → sessão não gerou compra

------------------------------------------------------------------------

# 5. Dicionário de Dados

## Métricas de Navegação

  -----------------------------------------------------------------------
  Variável                            Descrição
  ----------------------------------- -----------------------------------
  Administrative                      Número de páginas administrativas
                                      visitadas

  Administrative_Duration             Tempo total gasto em páginas
                                      administrativas

  Informational                       Número de páginas informativas
                                      visitadas

  Informational_Duration              Tempo gasto em páginas informativas

  ProductRelated                      Número de páginas de produto
                                      visitadas

  ProductRelated_Duration             Tempo gasto em páginas de produto
  -----------------------------------------------------------------------

## Métricas de Comportamento

  Variável      Descrição
  ------------- ---------------------------------------------------------
  BounceRates   Percentual de visitantes que saem sem interagir
  ExitRates     Percentual de sessões em que aquela página foi a última
  PageValues    Valor médio da página antes da conversão

## Variáveis de Contexto

  Variável           Descrição
  ------------------ -----------------------------------------------
  SpecialDay         Proximidade com datas especiais
  OperatingSystems   Sistema operacional do visitante
  Browser            Navegador utilizado
  Region             Região do visitante
  TrafficType        Origem do tráfego
  VisitorType        Novo visitante ou visitante recorrente
  Weekend            Indica se a visita ocorreu em final de semana
  Month              Mês da visita

------------------------------------------------------------------------

# 6. Tecnologias Utilizadas

## Linguagem

-   Python

## Bibliotecas de Análise

-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn

## Machine Learning

-   Scikit-learn
-   Imbalanced-Learn

## Técnicas utilizadas

-   SMOTE (balanceamento de classes)
-   GridSearchCV (otimização de hiperparâmetros)
-   Permutation Importance (importância das variáveis)

------------------------------------------------------------------------

# 7. Pipeline do Projeto

## 1. Coleta de Dados

Carregamento do dataset em formato CSV utilizando Pandas.

## 2. Análise Exploratória

Foram realizadas análises para compreender o comportamento dos dados:

-   Distribuição das variáveis
-   Identificação de outliers
-   Histogramas
-   Boxplots
-   Análise da variável alvo

## 3. Tratamento dos Dados

Etapas aplicadas:

-   Remoção de valores nulos
-   Separação entre variáveis contínuas e categóricas
-   Transformação de distribuição utilizando **QuantileTransformer**

Essa técnica foi utilizada para:

-   reduzir impacto de outliers
-   aproximar a distribuição dos dados de uma distribuição normal

## 4. Codificação de Variáveis Categóricas

### Ordinal Encoding

Aplicado na variável:

-   Month

### One Hot Encoding

Aplicado nas variáveis:

-   VisitorType
-   Weekend

## 5. Balanceamento de Classes

O dataset apresentou **desbalanceamento na variável alvo**.

Foi utilizado:

**SMOTE (Synthetic Minority Over-sampling Technique)**

Objetivo:

-   gerar novos exemplos sintéticos da classe minoritária
-   equilibrar o dataset

## 6. Divisão Treino/Teste

Divisão dos dados:

-   70% treino
-   30% teste

------------------------------------------------------------------------

# 8. Modelagem

Foram testadas **quatro versões do modelo SVM**.

## Modelo 1 --- SVM Linear

Treinamento utilizando kernel linear sem padronização dos dados.

## Modelo 2 --- SVM Linear com Padronização

Aplicação de **StandardScaler** antes do treinamento.

## Modelo 3 --- SVM com Kernel RBF

Aplicação de **GridSearchCV** para encontrar os melhores
hiperparâmetros.

Parâmetros otimizados:

-   C
-   Gamma

## Modelo 4 --- SVM Polinomial

Também foi aplicado **GridSearchCV** para otimização dos parâmetros:

-   Degree
-   Gamma
-   Coef0

------------------------------------------------------------------------

# 9. Métricas de Avaliação

Os modelos foram avaliados utilizando:

  Métrica     Descrição
  ----------- -------------------------------------------
  Acurácia    Percentual de previsões corretas
  Precision   Proporção de previsões positivas corretas
  Recall      Capacidade de identificar casos positivos
  F1 Score    Média harmônica entre precisão e recall
  AUC         Área sob a curva ROC

------------------------------------------------------------------------

# 10. Comparação entre Modelos

Foi criada uma tabela consolidando o desempenho de todos os modelos
testados.

  Modelo   Kernel               Precision   Recall   F1 Score   Acurácia   AUC
  -------- -------------------- ----------- -------- ---------- ---------- -----
  SVM v1   Linear               \-          \-       \-         \-         \-
  SVM v2   Linear Padronizado   \-          \-       \-         \-         \-
  SVM v3   RBF                  \-          \-       \-         \-         \-
  SVM v4   Polinomial           \-          \-       \-         \-         \-

------------------------------------------------------------------------

# 11. Importância das Variáveis

Foi utilizada a técnica **Permutation Importance** para identificar
quais variáveis possuem maior impacto na previsão do modelo.

Essa abordagem mede quanto a performance do modelo cai quando os valores
de uma variável são embaralhados.

Dessa forma foi possível identificar **os fatores que mais influenciam a
decisão de compra do usuário**.

------------------------------------------------------------------------

# 12. Resultados do Projeto

Principais entregas:

-   Construção de múltiplos modelos de Machine Learning
-   Comparação entre diferentes configurações de SVM
-   Identificação das variáveis mais relevantes
-   Pipeline completo de preparação de dados

Aplicações práticas:

-   recomendação de produtos
-   otimização de campanhas de marketing
-   identificação de usuários com alta probabilidade de compra
-   personalização da experiência do cliente

------------------------------------------------------------------------

# 13. Estrutura do Projeto

Sugestão de estrutura do repositório:

    projeto_previsao_vendas_ecommerce

    data/
        online_shoppers_intention.csv

    imagens/
        boxplot.png
        histplot.png

    notebooks/
        analise_modelagem.ipynb

    src/
        config.py

    README.md
