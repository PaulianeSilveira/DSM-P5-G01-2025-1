# Projeto Integrador: Classificação do Mix de Crédito

## 🌟 Visão Geral do Projeto

Este projeto visa desenvolver um modelo de Machine Learning capaz de classificar a **qualidade do Mix de Crédito** de um cliente. Utilizando dados financeiros e comportamentais, o modelo categoriza o perfil de crédito em 'Bom', 'Padrão' ou 'Ruim', oferecendo um sistema robusto para otimizar a avaliação de crédito e a tomada de decisões estratégicas em instituições financeiras.

## 🎯 Objetivos

* **Principal:** Criar um modelo de classificação que preveja a qualidade do `Credit_Mix` de um indivíduo.
* **Secundários:**
    * Analisar e compreender os fatores que mais influenciam a qualidade do Mix de Crédito.
    * Apoiar a gestão de risco e a personalização de ofertas de produtos financeiros.

## 📊 Módulo de Machine Learning

### 1. Informações Gerais do Dataset

**Nome do Dataset:** Credit Score Classification
**Origem:** Kaggle
🔗 **Link para download do dataset:** [https://www.kaggle.com/datasets/parisrohan/credit-score-classification](https://www.kaggle.com/datasets/parisrohan/credit-score-classification)

**Estrutura do Dataset**

* **Tamanho:** Aproximadamente 100.000 registros
* **Variáveis:** 27 colunas, incluindo identificadores, dados demográficos, informações financeiras e comportamentais.
* **Variável Alvo:** `Credit_Mix`, categorizada em:
    * `Poor` (Ruim)
    * `Standard` (Padrão)
    * `Good` (Bom)
* **Contexto do Projeto:** No escopo deste trabalho, a coluna `Credit_Mix` foi explicitamente selecionada como a variável alvo para classificação e representa uma **avaliação da QUALIDADE GERAL do portfólio de crédito do cliente**, e não apenas os tipos específicos de crédito que ele possui.

**Descrição Detalhada das Variáveis**

A tabela a seguir lista todas as variáveis do dataset, sua descrição em português e uma observação concisa sobre sua utilização no projeto. As justificativas completas para a remoção ou manutenção de cada coluna podem ser encontradas na seção **"Justificativas Detalhadas de Seleção de Variáveis"** abaixo.

| Variável                   | Descrição (Português)                              | Status no Projeto |
| :------------------------- | :------------------------------------------------- | :---------------- |
| `ID`                       | Identificação da linha                             | Removida          |
| `Customer_ID`              | Identificador do cliente                           | Removida          |
| `Month`                    | Mês da transação/dado                              | Removida          |
| `Name`                     | Nome do cliente                                    | Removida          |
| `Age`                      | Idade do cliente                                   | Mantida           |
| `SSN`                      | Número de Seguridade Social (ou CPF)               | Removida          |
| `Occupation`               | Ocupação profissional                              | Removida          |
| `Annual_Income`            | Renda anual                                        | Removida          |
| `Monthly_Inhand_Salary`    | Salário mensal líquido                             | Mantida           |
| `Num_Bank_Accounts`        | Número de contas bancárias                         | Mantida           |
| `Num_Credit_Card`          | Número de cartões de crédito                       | Mantida           |
| `Interest_Rate`            | Taxa de juros                                      | Removida          |
| `Num_of_Loan`              | Quantidade de empréstimos ativos                   | Mantida           |
| `Type_of_Loan`             | Tipos de empréstimos existentes                    | Removida          |
| `Delay_from_due_date`      | Dias de atraso em relação à data de vencimento     | Mantida           |
| `Num_of_Delayed_Payment`   | Número de pagamentos atrasados                     | Mantida           |
| `Changed_Credit_Limit`     | Alteração no limite de crédito                     | Removida          |
| `Num_Credit_Inquiries`     | Número de consultas de crédito                     | Removida          |
| `Credit_Mix`               | Tipo de crédito utilizado                          | ALVO              |
| `Outstanding_Debt`         | Dívida pendente                                    | Mantida           |
| `Credit_Utilization_Ratio` | Índice de utilização do crédito                    | Removida          |
| `Credit_History_Age`       | Tempo de histórico de crédito                      | Removida          |
| `Payment_of_Min_Amount`    | Indica se o pagamento mínimo foi realizado         | Removida          |
| `Total_EMI_per_month`      | Total de parcelas mensais (EMI)                    | Mantida           |
| `Amount_invested_monthly`  | Valor investido mensalmente                        | Mantida           |
| `Payment_Behaviour`        | Comportamento de pagamento                         | Removida          |
| `Monthly_Balance`          | Saldo mensal                                       | Removida          |

**Justificativas Detalhadas de Seleção de Variáveis**

Esta seção detalha as razões para a inclusão ou exclusão de cada variável no modelo, complementando a tabela de "Descrição Detalhada das Variáveis".

* **`ID`, `Customer_ID`, `Name`, `SSN`:** Removidas por serem identificadores únicos ou dados pessoais sensíveis (como SSN), sem valor preditivo direto para a classificação do Mix de Crédito e que poderiam levantar questões de privacidade.
* **`Month`:** Removida por não adicionar valor temporal útil ao modelo de classificação estática de `Credit_Mix`.
* **`Occupation`, `Type_of_Loan`, `Payment_Behaviour`:** Removidas devido à alta cardinalidade e/ou complexidade na padronização e transformação em features úteis. Embora pudessem ser candidatas à codificação, foram consideradas inviáveis para uso direto ou descartadas na seleção final de features após tentativas de pré-processamento.
* **`Annual_Income`:** Removida por ser considerada redundante com `Monthly_Inhand_Salary` após a fase de pré-processamento, onde uma dessas métricas de renda foi priorizada.
* **`Interest_Rate`, `Num_Credit_Inquiries`, `Credit_Utilization_Ratio`, `Credit_History_Age`, `Monthly_Balance`:** Removidas por serem consideradas dados técnicos ou internos, cujo impacto na qualidade do crédito já pode estar refletido em outras variáveis mantidas. Além disso, não seriam informações facilmente acessíveis ou fornecidas por um usuário final em um questionário para predição.
* **`Changed_Credit_Limit`:** Removida por ser potencialmente redundante com outras variáveis relacionadas ao endividamento e uso do crédito.
* **`Payment_of_Min_Amount` (e sua versão codificada `Payment_of_Min_Amount_encoded`):** Removida. Apesar de inicialmente considerada como uma variável comportamental importante, foi descartada na etapa final de seleção de features para o modelo, após a sua codificação.
* **Variáveis Mantidas (`Age`, `Monthly_Inhand_Salary`, `Num_Bank_Accounts`, `Num_Credit_Card`, `Num_of_Loan`, `Delay_from_due_date`, `Num_of_Delayed_Payment`, `Outstanding_Debt`, `Total_EMI_per_month`, `Amount_invested_monthly`):** Estas colunas foram consideradas essenciais para o modelo, abrangendo aspectos demográficos, financeiros e comportamentais de pagamento que são cruciais para a avaliação da qualidade do Mix de Crédito.

### 2. Pré-processamento e Análise Exploratória de Dados (EDA)

Esta etapa foi fundamental para preparar os dados brutos, garantindo a qualidade e o formato adequado para o treinamento do modelo de Machine Learning.

* **Importação de Dados e Bibliotecas:** Utilização de bibliotecas como `pandas` para manipulação de dados, `numpy` para operações numéricas e `matplotlib`/`seaborn` para visualização. Os datasets de treino (`train.csv`) e teste (`test.csv`) foram carregados via `pd.read_csv()`.

* **Seleção de Features:**
    Uma curadoria rigorosa de features foi aplicada para garantir a relevância, acessibilidade e qualidade dos dados para o modelo. As colunas foram selecionadas com base em sua utilidade preditiva e na necessidade de remover informações irrelevantes, redundantes ou sensíveis, conforme detalhado na seção **"Justificativas Detalhadas de Seleção de Variáveis"** acima.

* **Tratamento de Valores Inválidos:** Identificação e substituição de valores inconsistentes ou representações de nulo (como `_`, `__10000__`, `_____`) por `NaN` para padronização.

* **Conversão de Tipos de Dados:** Colunas que deveriam ser numéricas, mas que foram importadas como objetos devido a caracteres não numéricos, foram limpas e convertidas para o tipo `float` usando `pd.to_numeric()`. Isso incluiu `Age`, `Num_of_Loan`, `Outstanding_Debt`, `Amount_invested_monthly`.

* **Tratamento de Valores Ausentes (NaN):** Estratégias foram aplicadas para lidar com os valores `NaN` remanescentes nas colunas numéricas (e.g., imputação por média/mediana, ou remoção, dependendo da coluna e volume de ausência).

* **Remoção de Outliers:** O método do **Intervalo Interquartil (IQR)** foi aplicado para detectar e mitigar o impacto de valores extremos que poderiam distorcer o treinamento do modelo.

* **Codificação de Variáveis Categóricas:** Variáveis categóricas foram transformadas em formato numérico. A variável alvo `Credit_Mix` foi codificada usando `LabelEncoder`. Outras colunas categóricas (`Credit_Score`, `Occupation`, `Type_of_Loan`, `Payment_Behaviour`, `Payment_of_Min_Amount`) foram consideradas para `OneHotEncoder` ou `LabelEncoder` (e suas versões codificadas foram posteriormente avaliadas para inclusão final no modelo).

* **Escalamento de Features Numéricas:** As features numéricas que seriam utilizadas pelos modelos foram padronizadas usando `StandardScaler` (média 0 e desvio padrão 1). Isso é crucial para algoritmos sensíveis à escala, como KNN, SVM e Regressão Logística.

* **Alinhamento de Colunas:** As colunas dos conjuntos de treino e teste foram alinhadas para garantir consistência após o pré-processamento.

* **Análise Exploratória (EDA):** Visualizações foram cruciais para entender os dados:
    * **Visualização de Distribuições:** Boxplots e histogramas foram utilizados para entender a distribuição das variáveis numéricas e identificar potenciais desvios ou problemas.
    * **Análise da Variável Alvo:** Um `countplot` foi gerado para visualizar a distribuição das classes 'Good', 'Standard' e 'Poor' em `Credit_Mix`, revelando um **desbalanceamento** que foi um ponto chave considerado na escolha das métricas de avaliação e estratégias de modelagem.
    * **Relações entre Variáveis:** `Pairplots` foram usados para identificar relações visuais entre pares de variáveis, e uma `Matriz de Correlação` (com `Heatmap`) foi criada para quantificar a relação linear entre as features numéricas, auxiliando na compreensão das dependências.

### 3. Modelagem e Treinamento

Nesta fase, diversos algoritmos de Machine Learning foram implementados e avaliados para identificar o modelo mais eficaz na classificação da qualidade do `Credit_Mix` dos clientes.

* **Modelos Avaliados:**
    * K-Nearest Neighbors (KNN)
    * Random Forest (Floresta Aleatória)
    * Decision Tree (Árvore de Decisão)
    * Support Vector Machine (SVM)
    * Gaussian Naive Bayes (Gaussian NB)
    * Logistic Regression (Regressão Logística)
    * Linear Discriminant Analysis (LDA)

* **Estratégias de Tratamento de Desbalanceamento:**
    Dada a identificação de desbalanceamento nas classes da variável alvo (`Credit_Mix`), a estratégia adotada focou em garantir uma avaliação justa e a otimização dos modelos para um bom desempenho em todas as classes, sem a aplicação direta de técnicas de reamostragem nos dados. As principais ações foram:
    * **Divisão Estratificada:** Durante a divisão dos dados para treino e validação (`train_test_split`), o parâmetro `stratify=y_train` foi utilizado para assegurar que as proporções das classes da variável alvo fossem mantidas nos subconjuntos, preservando a distribuição original do desbalanceamento.
    * **Métrica de Otimização Ponderada:** Na otimização de hiperparâmetros via `GridSearchCV`, a métrica de pontuação principal utilizada foi o **F1-Score ponderado (`scoring='f1_weighted'`)**. Esta métrica é crucial para datasets desbalanceados, pois calcula uma média do F1-Score para cada classe, ponderando pelo número de instâncias em cada classe, garantindo que o modelo seja otimizado para um bom equilíbrio entre precisão e recall em todas as classes, e não apenas na majoritária.
    * **Avaliação Detalhada:** A performance dos modelos foi analisada com base em métricas ponderadas (como a Acurácia Ponderada, Precision, Recall e F1-Score ponderados) e relatórios de classificação detalhados por classe, fornecendo uma visão completa do desempenho em cada categoria do `Credit_Mix`.

* **Métricas de Avaliação:** Para uma avaliação robusta e considerando o desbalanceamento das classes, foram utilizadas métricas como:
    * **Acurácia Ponderada (Weighted Average Accuracy):** Métrica principal para o modelo final.
    * Precision, Recall e F1-Score (calculados por classe e em médias ponderadas/macro para uma visão completa do desempenho).
    * Matriz de Confusão para análise detalhada dos erros e acertos em cada classe.
* **Otimização de Hiperparâmetros:** A otimização dos hiperparâmetros para cada modelo foi realizada utilizando o método **GridSearchCV**. Este método explora sistematicamente combinações de parâmetros pré-definidas para encontrar a que oferece o melhor desempenho de acordo com a métrica de avaliação escolhida (`f1_weighted`).

### 4. Resultados e Insights

A fase de avaliação consolidou o desempenho do modelo escolhido e revelou importantes insights sobre os dados.

* **Melhor Modelo:** O algoritmo **RandomForestClassifier** demonstrou o melhor desempenho geral e robustez para o problema de classificação.
* **Métricas de Desempenho do Modelo Final:**
    * **Acurácia Ponderada:** 96.86% (Indicando uma alta capacidade preditiva geral do modelo).
    * **Matriz de Confusão Detalhada:** A análise da matriz de confusão revelou um ponto crítico de sucesso para a aplicação de negócios: o modelo obteve **zero classificações errôneas de clientes com `Credit_Mix` 'Ruim' como 'Bom'**. Este resultado é fundamental para a gestão de risco, minimizando a chance de aprovar crédito para perfis de alto risco.
* **Importância das Features:** Através da análise do modelo Random Forest, a feature `Número de Pagamentos Atrasados` (`Num_of_Delayed_Payment`) foi consistentemente identificada como a **variável mais importante** para prever a qualidade do `Credit_Mix` dos clientes, seguida por `Número de Contas Bancárias` e `Dívida Pendente`.

### 5. Implantação e Valor Estratégico

Este modelo de Machine Learning de alta performance representa um **valor fundamental para o Projeto Integrador**, oferecendo um sistema robusto para otimizar a avaliação de crédito e a tomada de decisões estratégicas em contextos financeiros. Sua aplicação potencial inclui:

* **Melhorar a Precisão na Avaliação de Risco:** Permite uma classificação mais assertiva do perfil de crédito de novos e atuais clientes.
* **Auxiliar na Segmentação de Clientes:** Facilita a identificação de segmentos de clientes com base na qualidade de seu perfil de crédito para estratégias direcionadas.
* **Informar Estratégias de Negócio:** Pode guiar a personalização de produtos e serviços financeiros, bem como decisões sobre concessão ou ajuste de crédito.

### 6. Como Utilizar o Modelo (Exemplo de Entradas para Predição)

Para prever o `Credit_Mix` de um novo cliente utilizando este modelo, as seguintes informações seriam necessárias. Este questionário representa um exemplo de como os dados de entrada seriam coletados:

* **Idade** (coluna: `Age`)
* **Informe a sua renda líquida mensal** (coluna: `Monthly_Inhand_Salary`)
* **Informe o número de contas bancárias em que você é o titular** (coluna: `Num_Bank_Accounts`)
* **Informe o número de cartões de crédito que você possui** (coluna: `Num_Credit_Card`)
* **Informe quantos empréstimos ativos você possui atualmente** (coluna: `Num_of_Loan`)
* **Quantos dias, em média, você costuma atrasar o pagamento de dívidas?** (coluna: `Delay_from_due_date`)
* **Quantas vezes você se atrasou para fazer o pagamento de uma dívida?** (coluna: `Num_of_Delayed_Payment`)
* **Qual o valor total de dívidas não pagas (pendentes) que você tem no momento?** (coluna: `Outstanding_Debt`)
* **Qual o total de parcelas mensais (EMIs) que você possui?** (coluna: `Total_EMI_per_month`)
* **Informe o valor total investido mensalmente** (coluna: `Amount_invested_monthly`)

---

