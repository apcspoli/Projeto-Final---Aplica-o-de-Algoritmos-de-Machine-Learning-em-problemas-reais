# Projeto-Final---Aplica-o-de-Algoritmos-de-Machine-Learning-em-problemas-reais

# 🌧️ Previsão de Chuva com Machine Learning – weatherAUS

Este projeto tem como objetivo construir e comparar modelos de aprendizado supervisionado para prever se **vai chover amanhã** (`RainTomorrow`) com base em variáveis meteorológicas históricas fornecidas no dataset `weatherAUS.csv`.

---

## 📁 Dataset

- **Fonte:** [Kaggle - Weather Dataset - Rattle Package](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package)
- **Descrição:** Dados climáticos de estações meteorológicas australianas contendo informações como temperatura, umidade, vento, pressão, evaporação e precipitação.
- **Tarefa:** Classificação binária (`RainTomorrow`: Yes ou No)

---

## 🎯 Objetivo

> Desenvolver um modelo preditivo que, com base em condições climáticas observadas até o dia atual, estime se irá chover no próximo dia.

---

## 🧪 Algoritmos Utilizados

- 🌲 **Random Forest (com ajuste de hiperparâmetros)**
- ⚡ **XGBoost**
- 📍 **K-Nearest Neighbors (KNN)**

---

## 🔍 Etapas do Pipeline

1. **Carregamento do Dataset**
   - Leitura do arquivo CSV
2. **Análise Exploratória**
   - Gráficos, boxplots, heatmaps de correlação
   - Identificação de valores ausentes e outliers
3. **Pré-processamento**
   - Remoção de colunas com mais de 30% de valores ausentes
   - Preenchimento de valores nulos (mediana/mode)
   - Extração de `Month` e `Year` da data
   - One-Hot Encoding em variáveis categóricas
   - Detecção e possível remoção de outliers com IQR
4. **Divisão dos Dados**
   - Treino e teste com `train_test_split`
   - Normalização **apenas para o KNN**
5. **Modelagem**
   - **Random Forest:** ajuste fino com `GridSearchCV`
   - **XGBoost:** treinamento direto sem redução de dimensionalidade
   - **KNN:** aplicado com dados normalizados
6. **Avaliação dos Modelos**
   - Matriz de confusão
   - Precision, Recall, F1-score
   - Curva ROC e AUC
7. **Comparação Final**
   - Análise dos trade-offs entre os modelos para aplicação real

---

## 📊 Principais Resultados

| Modelo         | Recall (Chuva) | F1-score (Chuva) | Observação                        |
|----------------|----------------|------------------|-----------------------------------|
| Random Forest  | 0.49           | 0.60             | Conservador (erra menos alarmes) |
| **XGBoost**    | **0.55**       | **0.63**         | **Melhor para prever chuva**     |
| KNN            | 0.31           | 0.42             | Desempenho fraco, não recomendado|

---

## 🌾 Aplicação na Agricultura

- O **recall da classe positiva ("True")** foi usado como critério principal para escolha do modelo mais apropriado.
- O **XGBoost** foi o mais indicado, pois consegue **detectar mais dias em que realmente chove**, mesmo gerando alguns falsos alarmes, o que é preferível em contextos agrícolas.

---

## 📌 Conclusões

- ❌ Reduções de dimensionalidade como **PCA** ou **LDA** **pioraram o desempenho**, pois XGBoost já lida bem com dados brutos.
- ✅ A aplicação de **validação cruzada com `GridSearchCV` no Random Forest** trouxe melhorias moderadas.
- ✅ A **normalização foi aplicada apenas no KNN**, que é sensível à escala.
- 🔍 Métricas como **Recall** e **F1-score** foram priorizadas em vez da acurácia, devido ao desbalanceamento entre as classes.

---

## 🚀 Possíveis Extensões

- Aplicar **SMOTE** para balancear as classes
- Ajustar o **threshold de decisão** do XGBoost para priorizar recall
- Exportar o modelo final (`joblib`, `pickle`) para uso em APIs
- Deploy com **Streamlit**, **Flask** ou **FastAPI**

---

## 🧠 Autor

**Adriano Pedro Couto dos Santos**  
Estudo de previsão climática com aplicação em ciência de dados.  
Orientado a aplicações reais como agricultura e tomada de decisão estratégica.

---

## 📎 Licença

Este projeto é livre para uso educacional e pessoal. Para usos comerciais, entre em contato.

