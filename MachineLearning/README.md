# Documentação: Machine Learning

## 1. Informações Gerais do Dataset

### Estrutura do Dataset

- **Tamanho**: Aproximadamente 100.000 registros  
- **Variáveis**: 27 colunas, incluindo identificadores, dados demográficos, informações financeiras e comportamentais  
- **Variável Alvo**: `Credit_Mix`, categorizada em:
  - `Poor` (Ruim)
  - `Standard` (Padrão)
  - `Good` (Bom)

### Descrição das Variáveis

| Variável                     | Descrição (Português)                                     |
|-----------------------------|------------------------------------------------------------|
| `ID`                        | Identificação da linha                                     |
| `Customer_ID`               | Identificador do cliente                                   |
| `Month`                     | Mês da transação/dado                                     |
| `Name`                      | Nome do cliente                                           |
| `Age`                       | Idade do cliente                                          |
| `SSN`                       | Número de Seguridade Social (ou CPF)                      |
| `Occupation`                | Ocupação profissional                                     |
| `Annual_Income`             | Renda anual                                               |
| `Monthly_Inhand_Salary`     | Salário mensal líquido                                    |
| `Num_Bank_Accounts`         | Número de contas bancárias                                |
| `Num_Credit_Card`           | Número de cartões de crédito                              |
| `Interest_Rate`             | Taxa de juros                                             |
| `Num_of_Loan`               | Quantidade de empréstimos ativos                          |
| `Type_of_Loan`              | Tipos de empréstimos existentes                           |
| `Delay_from_due_date`       | Dias de atraso em relação à data de vencimento            |
| `Num_of_Delayed_Payment`    | Número de pagamentos atrasados                            |
| `Changed_Credit_Limit`      | Alteração no limite de crédito                            |
| `Num_Credit_Inquiries`      | Número de consultas de crédito                            |
| `Credit_Mix`                | Tipo de crédito utilizado                                 |
| `Outstanding_Debt`          | Dívida pendente                                           |
| `Credit_Utilization_Ratio`  | Índice de utilização do crédito                           |
| `Credit_History_Age`        | Tempo de histórico de crédito                             |
| `Payment_of_Min_Amount`     | Indica se o pagamento mínimo foi realizado                |
| `Total_EMI_per_month`       | Total de parcelas mensais (EMI)                           |
| `Amount_invested_monthly`   | Valor investido mensalmente                               |
| `Payment_Behaviour`         | Comportamento de pagamento                                |
| `Monthly_Balance`           | Saldo mensal                                              |

🔗 **Link para download do dataset**: [Kaggle - Credit Score Classification](https://www.kaggle.com/datasets/parisrohan/credit-score-classification/data)

---

## 2. Pré-processamento

### Importação de Dados e Bibliotecas

- **Bibliotecas utilizadas**: `pandas`, `numpy`, `matplotlib`, `seaborn`
- **Leitura do dataset**: `pd.read_csv()`

---

### Remoção de Colunas Irrelevantes ou Sensíveis

**Colunas removidas**:

- `ID`, `Customer_ID`, `Name`, `SSN`  
  *Justificativa*: Dados identificadores ou pessoais

- `Month`  
  *Justificativa*: Sem valor temporal útil no modelo

- `Occupation`  
  *Justificativa*: Alta cardinalidade e baixa padronização

- `Type_of_Loan`  
  *Justificativa*: Múltiplos valores concatenados, difícil de codificar

- `Changed_Credit_Limit`  
  *Justificativa*: Redundante com outras variáveis

- `Payment_Behaviour`  
  *Justificativa*: Difícil de transformar e potencialmente redundante

- `Annual_Income`  
  *Justificativa*: Redundante com `Monthly_Inhand_Salary`

- `Credit_Utilization_Ratio`, `Credit_History_Age`, `Monthly_Balance`, `Interest_Rate`, `Num_Credit_Inquiries`  
  *Justificativa*: Dados técnicos não acessíveis diretamente por usuários comuns

---

### Colunas Mantidas

- `Age`
- `Monthly_Inhand_Salary`
- `Num_Bank_Accounts`
- `Num_Credit_Card`
- `Num_of_Loan`
- `Delay_from_due_date`
- `Num_of_Delayed_Payment`
- `Outstanding_Debt`
- `Payment_of_Min_Amount`
- `Total_EMI_per_month`
- `Amount_invested_monthly`

---

### Tratamento de Valores Inválidos

- Substituição de valores como `'_'`, `'__10000__'`, `'_____'` por `NaN`

---

### Conversão de Dados para Tipos Numéricos

- Remoção de caracteres não numéricos em colunas como:
  - `Age`
  - `Annual_Income`
  - `Num_of_Loan`
  - `Outstanding_Debt`

- Conversão para `float` usando `pd.to_numeric()`

---

### Tratamento de Valores Ausentes

- Identificação e tratamento de valores `NaN` nas colunas numéricas

---

### Remoção de Outliers

- Aplicação do método **IQR (Intervalo Interquartil)** para detectar e remover valores extremos

---

### Visualizações Utilizadas

- **Boxplot**
- **Pairplot**
- **Countplot** (para a variável alvo `Credit_Mix`)
- **Matriz de Correlação** e **Heatmap** para análise de relações entre variáveis numéricas



### Questionário de Informações Financeiras (Relacionadas ao Dataset)

- **Idade**  
  *(coluna: `Age`)*

- **Informe a sua renda líquida mensal**  
  *(coluna: `Monthly_Inhand_Salary` - salário líquido mensal)*

- **Informe o número de contas bancárias em que você é o titular**  
  *(coluna: `Num_Bank_Accounts` - número de contas bancárias)*

- **Informe o número de cartões de crédito que você possui**  
  *(coluna: `Num_Credit_Card` - número de cartões de crédito)*

- **Informe quantos empréstimos ativos você possui atualmente**  
  *(coluna: `Num_of_Loan` - número de empréstimos)*

- **Quantos dias, em média, você costuma atrasar o pagamento de dívidas?**  
  *(coluna: `Delay_from_due_date` - dias de atraso em relação à data de vencimento)*

- **Quantas vezes você se atrasou para fazer o pagamento de uma dívida?**  
  *(coluna: `Num_of_Delayed_Payment` - número de dívidas em atraso)*

- **Qual o valor total de dívidas não pagas (pendentes) que você tem no momento?**  
  *(coluna: `Outstanding_Debt` - dívida pendente)*

- **Qual o total de parcelas mensais (EMIs) que você possui?**  
  *(coluna: `Total_EMI_per_month` - total de parcelas mensais)*

- **Informe o valor total investido mensalmente**  
  *(coluna: `Amount_invested_monthly` - valor investido mensalmente)*


## 3. Treinamento do Modelo

### Algoritmo Escolhido
- **Random Forest Classifier**

### Justificativa
- Escolhido por sua robustez, capacidade de lidar com dados numéricos e categóricos, boa performance em classificações multiclasse e interpretabilidade por meio de importâncias de atributos.
- 
- ### Resultados do Modelo Random Forest

Após o treinamento com otimização via validação cruzada (GridSearchCV), o modelo Random Forest obteve os seguintes resultados no conjunto de validação:

- **Melhores hiperparâmetros encontrados**:
  - `max_depth`: None  
  - `min_samples_leaf`: 1  
  - `n_estimators`: 200  

- **Tempo de treinamento**: 328.86 segundos

- **Desempenho no conjunto de validação**:
  - **Acurácia**: `96,86%`
  - **F1-Score Ponderado**: `96,86%`

- **Relatório de Classificação**:

| Classe    | Precisão | Revocação | F1-Score | Suporte |
|-----------|----------|-----------|----------|---------|
| Bad       | 0.98     | 0.99      | 0.98     | 1765    |
| Good      | 0.98     | 0.94      | 0.96     | 2995    |
| Standard  | 0.96     | 0.98      | 0.97     | 4709    |
| **Média Macro** | **0.97** | **0.97** | **0.97** | **9469** |
| **Média Ponderada** | **0.97** | **0.97** | **0.97** | **9469** |

> 🟢 O modelo apresentou excelente desempenho em todas as classes, com acurácia geral de aproximadamente **97%**.


### Seleção de Atributos (Features Utilizadas no Treinamento)
As seguintes variáveis foram mantidas após o pré-processamento para treinamento:

- `Age` (Idade)  
- `Monthly_Inhand_Salary` (Salário mensal líquido)  
- `Num_Bank_Accounts` (Número de contas bancárias)  
- `Num_Credit_Card` (Número de cartões de crédito)  
- `Num_of_Loan` (Número de empréstimos ativos)  
- `Delay_from_due_date` (Dias de atraso em relação à data de vencimento)  
- `Num_of_Delayed_Payment` (Número de pagamentos atrasados)  
- `Outstanding_Debt` (Dívida pendente)  
- `Payment_of_Min_Amount` (Indicador se o pagamento mínimo foi realizado)  
- `Total_EMI_per_month` (Total de parcelas mensais - EMI)  
- `Amount_invested_monthly` (Valor investido mensalmente)

> **Nota:** Algumas colunas com dados técnicos ou sensíveis foram removidas para aproximar o modelo de um cenário realista de uso com dados informados por usuários.

### Divisão dos Dados
- Conjunto de treino (`train.csv`) e teste (`test.csv`) foram carregados separadamente.
- Os dados foram balanceados e padronizados onde necessário.

### Treinamento e Avaliação
- O modelo **RandomForestClassifier** foi treinado utilizando as 11 variáveis mantidas.
- Avaliação com métricas como **acurácia**, **matriz de confusão**, **classification report** e **importância das variáveis**.
- A análise da **feature importance** indicou quais variáveis mais impactam a predição do `Credit_Mix`.

### Armazenamento
- O modelo final foi salvo como: `random_forest_creditmix_model.pkl` (no Colab/Drive).
