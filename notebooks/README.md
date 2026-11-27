# Notebooks

Rodar na ordem. Cada um abre no Google Colab e clona o repositório na primeira célula (exceto o 01, que lê os dados brutos no Google Drive).

| Notebook | Fase CRISP-DM | O que faz |
|---|---|---|
| 01_preparacao | 3. Preparação | Lê Censo, Indicadores e INSE, cria as variáveis e gera `dados/tabela_analitica.csv` |
| 02_eda | 2. Entendimento dos dados | Distribuições, associações, controle por INSE, quintis de INSE, VIF, correlações, histogramas, ausência |
| 03_modelagem | 4. Modelagem | Dummy, Regressão Logística, Random Forest e Hist Gradient Boosting × 3 cenários × 3 etapas, validação agrupada por município |
| 04_avaliacao_implantacao | 5. Avaliação e 6. Implantação | Recall@k, calibração, SHAP, sensibilidade do limiar, perfis, geografia, overfitting, erros, lista priorizada e relatório PDF |
