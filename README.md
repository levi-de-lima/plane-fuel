# Projeto B2 - Previsão do Consumo de Combustível de Aeronaves ✈️  

## 📘 Descrição Geral  
Este projeto foi desenvolvido como parte da disciplina **TRA-48 – Inteligência Analítica: Dados, Modelos e Decisões** do **Instituto Tecnológico de Aeronáutica (ITA)**.  
O objetivo é aplicar métodos de **aprendizado de máquina supervisionado** para construir um **modelo preditivo de consumo de combustível (`fuel_burn`)** de aeronaves, com base em dados operacionais de voos sobre o espaço aéreo brasileiro em 2023.  

O desafio consiste em treinar o modelo com o conjunto de dados `data_project_train.Rda` e prever o consumo de combustível para os voos do conjunto `data_project_test.Rda`.  
As previsões são avaliadas pela métrica **RMSE (Root Mean Square Error)** — o grupo com o menor RMSE vence o desafio.

---

## 📂 Estrutura do Projeto  
├── data_project_train.Rda # Base de treinamento (7.279 voos)  
├── data_project_test.Rda # Base de teste (2.427 voos)  
├── data_project_test_groupname.Rda # Arquivo de submissão com previsões do grupo  
├── Projeto_B2_script.R # Script principal em R  
└── README.md # Este arquivo  


---

## ⚙️ Etapas do Desenvolvimento  

### 1. Entendimento do Problema  
O consumo de combustível depende de diversos fatores operacionais e de eficiência da rota. O modelo visa capturar essas relações a partir das variáveis fornecidas.

### 2. Pré-processamento  
- Remoção de registros com `fuel_burn` ausente (apenas na base de treino).  
- Conversão de datas para o formato `POSIXct`.  
- Padronização e verificação de tipos de variáveis.  

### 3. Criação de Novas Features  
Foram criadas variáveis derivadas para melhorar a capacidade preditiva do modelo:
- `avg_speed` – velocidade média (NM/h)  
- `fuel_per_nm` e `fuel_per_min` – consumo relativo  
- `total_ineff` – soma das ineficiências de decolagem e chegada  
- `flight_range` – classificação de voos curtos, médios ou longos  
- `dep_period` – período do dia (manhã, tarde ou noite)  

### 4. Análise Exploratória (EDA)  
Foram realizadas análises gráficas e estatísticas, incluindo:
- Distribuição de `fuel_burn`  
- Relação entre distância voada e consumo  
- Comparação por tipo de aeronave e companhia aérea  
- Correlação entre variáveis numéricas  

### 5. Modelagem  
Foram testados e comparados dois métodos de aprendizado supervisionado:
1. **Regressão Linear Múltipla** – modelo baseline para referência.  
2. **Random Forest** – modelo final selecionado por melhor desempenho preditivo (menor RMSE).  

Modelos adicionais (ex.: XGBoost, Lasso, Elastic Net) podem ser facilmente integrados para comparação.

### 6. Avaliação  
As métricas utilizadas foram:
- **RMSE** – erro quadrático médio da raiz  
- **MAE** – erro absoluto médio  
- **MAPE** – erro percentual absoluto médio  

Também foram analisados:
- Histogramas de resíduos  
- Gráficos de `predito vs observado`  
- Importância das variáveis (feature importance)  

### 7. Previsões e Submissão  
O modelo final foi aplicado à base `data_project_test.Rda` para gerar as previsões de `fuel_burn`.  
O resultado foi salvo como `data_project_test_groupname.Rda` para submissão oficial.

---

## 🧰 Principais Bibliotecas Utilizadas  
- `tidyverse` – manipulação e visualização de dados  
- `lubridate` – tratamento de datas e horários  
- `caret` – particionamento e avaliação de modelos  
- `randomForest` – modelo de árvores de decisão  
- `xgboost` – modelo de boosting (opcional)  
- `GGally` – correlação e EDA gráfica  
- `vip` – importância de variáveis  

---

## 📊 Insights Obtidos  
- A variável **`flown_distance_enr`** (distância voada) é o principal fator explicativo do consumo.  
- Aeronaves **A321** e **B738** têm maior consumo absoluto, mas menor consumo relativo (kg/NM).  
- Voos curtos (< 400 NM) são menos eficientes, devido à maior proporção de tempo em subida/descida.  
- Ineficiências de rota (`kpi_inefficiency_enr`) têm correlação positiva com o consumo.  

---

## 🧩 Próximos Passos  
- Refinar o *feature engineering* com variáveis meteorológicas e de tráfego.  
- Aplicar *tuning* de hiperparâmetros via `caret::train()` ou `tidymodels`.  
- Testar modelos de boosting (LightGBM, CatBoost).  
- Automatizar a geração de relatórios via `RMarkdown`.  

---

## 👥 Autores  
Projeto desenvolvido por **[Nome do Grupo / Integrantes]**,  
para o curso **TRA-48 – Inteligência Analítica: Dados, Modelos e Decisões (ITA, 2025)**.  

---
