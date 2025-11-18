# Previsão do Consumo de Combustível de Aeronaves - Aerometrics ✈️

## 📘 Descrição Geral
Este projeto foi desenvolvido como parte da disciplina **TRA 48 - Inteligência Analítica: Dados, Modelos e Decisões** do **Instituto Tecnológico de Aeronáutica (ITA)**.

O objetivo é aplicar métodos de **aprendizado de máquina supervisionado** para construir um **modelo preditivo de consumo de combustível (`fuel_burn`)** de aeronaves, com base em dados operacionais de voos simulados pela empresa **Aerometrics**.

O desafio consiste em treinar e combinar modelos no conjunto de dados `data_project_train.Rda` para prever o consumo de combustível para os voos do conjunto `data_project_test.Rda`.

As previsões são avaliadas pela métrica **RMSE Relativo (Relative Root Mean Square Error)**, visando a otimização da precisão percentual.

---

## 📂 Estrutura do Projeto
├── data_project_train.Rda # Base de treinamento (dados históricos) <br>
├── data_project_test.Rda # Base de teste (a ser prevista) <br>
├── **data_project_test_aerometrics.Rda** # Arquivo final de submissão com previsões <br>
├── **project.Rmd** # Notebook R Markdown com pipeline completo (EDA, Modelagem, Ensemble) <br>
├── **presentation.Rmd** # Apresentação de slides da disciplina <br>
└── README.md # Este arquivo

---

## ⚙️ Pipeline de Desenvolvimento

### 1. Pré-processamento e Feature Engineering
Foram criadas **variáveis derivadas** cruciais para capturar a eficiência e a característica do voo:

* `avg_speed` – Velocidade média (NM/h).
* `total_ineff` – Índice total de ineficiência operacional (Decolagem + Pouso).
* `flight_range` – Classificação categórica da rota (`Curto`, `Médio`, `Longo`).
* `dep_period` – Período do dia (`Manhã`, `Tarde`, `Noite`).

### 2. Análise Exploratória (EDA)
Análise visual da distribuição das variáveis chave:
* **`flight_duration`** (tempo de voo) e **`flown_distance_enr`** (distância).
* **`dep_hour`** (hora de partida) para identificar padrões operacionais.
* Distribuição de **`fuel_burn`** e sua dispersão por **`aircraft_type`**.

### 3. Modelagem e Ensemble 🧠🌳
Foram treinados e combinados dois modelos de aprendizado de máquina para aproveitar seus pontos fortes:

1.  **Rede Neural (NN):** Utilizada com as **três primeiras componentes principais (PCA)** das variáveis de ineficiência, para estabilidade e redução de dimensionalidade.
2.  **Árvore de Decisão (DT):** Utilizada por sua capacidade de capturar relações não lineares e interações entre variáveis operacionais e categóricas.
3.  **Ensemble Linear:** As previsões do NN e do DT foram combinadas em um modelo de regressão linear simples (`lm(fuel_burn ~ nn + dt)`), permitindo que o modelo aprenda o peso ótimo de cada previsão.

### 4. Avaliação e Submissão
* **Métrica:** RMSE Relativo (Relative RMSE) no conjunto de treinamento.
* **Previsão Final:** O modelo *Ensemble* foi aplicado à base de teste, e as previsões foram salvas no arquivo `data_project_test_aerometrics.Rda`.

---

## 🧰 Principais Bibliotecas Utilizadas
* `tidyverse` – Manipulação de dados e **Feature Engineering**.
* `lubridate` – Tratamento de datas e extração de variáveis temporais.
* `e1071` e `neuralnet` – Modelagem de **Rede Neural** (NN).
* `tree` e `caret` – Modelagem de **Árvore de Decisão** (DT) e validação.

---

## 📊 Insights Chave do Modelo Ensemble
* O **Ensemble** obteve o menor RMSE relativo no conjunto de treinamento.
* O uso do **PCA** na Rede Neural melhorou o desempenho ao focar nas dimensões mais explicativas das ineficiências.
* A inclusão de variáveis de **Feature Engineering** (e.g., `flight_range`, `total_ineff`) foi essencial para capturar variações no consumo que as variáveis brutas não conseguiam explicar sozinhas.

---

## 👥 Autores
Projeto desenvolvido por:
* Levi Gurgel de Lima
* Yves Gabriel Queiroz de Sousa
* Marco Aurélio Costa Risardi

para o curso **TRA-48 – Inteligência Analítica: Dados, Modelos e Decisões (ITA, 2025)**.
