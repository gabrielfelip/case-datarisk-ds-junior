# Case Técnico – Modelo de Previsão de Inadimplência | DataRisk

## Sobre o projeto

Este projeto foi desenvolvido como parte de um desafio técnico de Ciência de Dados para construção de um modelo preditivo de risco de crédito.

O objetivo foi desenvolver um modelo de Machine Learning capaz de identificar clientes com maior probabilidade de inadimplência, utilizando dados históricos de pagamentos, informações cadastrais e dados financeiros.

O problema foi tratado como uma classificação binária:

- 0: pagamento realizado sem atraso
- 1: pagamento realizado com atraso

A solução foi desenvolvida utilizando Python, técnicas de análise de dados, engenharia de atributos e modelos de classificação.

---

## Objetivo do projeto

Construir um modelo capaz de auxiliar na identificação antecipada de clientes com maior risco de atraso em pagamentos, contribuindo para uma tomada de decisão mais eficiente em cenários de análise de crédito.

---

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Scikit-learn
- Jupyter Notebook
- Git/GitHub

Principais técnicas utilizadas:

- Análise exploratória de dados (EDA)
- Tratamento de dados ausentes
- Engenharia de atributos
- Codificação de variáveis categóricas
- Modelagem de classificação
- Avaliação de métricas

---

## Dados utilizados

Foram utilizadas três principais fontes de dados:

### Base cadastral

Contém informações relacionadas ao perfil dos clientes:

- Segmento industrial
- Porte da empresa
- CEP
- Domínio de e-mail
- Data de cadastro
- Informações cadastrais gerais

### Base de informações mensais

Contém informações atualizadas dos clientes:

- Renda do mês anterior
- Número de funcionários

### Base de pagamentos

Contém o histórico financeiro utilizado para treinamento do modelo:

- Data de emissão do documento
- Data de vencimento
- Data de pagamento
- Valor a pagar
- Taxa
- Dias de atraso

---

# Desenvolvimento da solução

## 1. Análise exploratória dos dados

Foram realizadas análises iniciais para compreender o comportamento dos dados, incluindo:

- Distribuição da variável alvo
- Quantidade de clientes inadimplentes
- Distribuição dos atrasos
- Valores ausentes
- Características dos clientes

A variável alvo apresentou desbalanceamento entre as classes:

- Classe 0 (sem atraso): 92,98%
- Classe 1 (com atraso): 7,02%

Por esse motivo, além da acurácia, foram analisadas métricas como Precision, Recall e F1-score, dando maior atenção à identificação correta da classe inadimplente.

---

## 2. Tratamento dos dados

Foram realizadas etapas de preparação dos dados:

- Conversão e padronização de datas
- Tratamento de valores ausentes
- Ajuste dos tipos de dados
- Criação de novas variáveis
- Codificação de variáveis categóricas
- Remoção de informações inconsistentes

---

## 3. Engenharia de atributos

Foram criadas novas variáveis buscando melhorar a capacidade preditiva do modelo.

### Tempo de relacionamento do cliente

Foi calculado o tempo entre a data de cadastro do cliente e a data do pagamento, buscando representar o histórico de relacionamento.

### Informações temporais

Foram extraídas informações como:

- Ano de emissão
- Mês de emissão
- Ano de cadastro
- Mês de cadastro

### Transformação financeira

Foi aplicada transformação logarítmica no valor a pagar para reduzir o impacto de valores extremos e melhorar o comportamento da variável durante o treinamento.

---

## 4. Análise de Data Leakage

Durante o desenvolvimento foi identificado que algumas variáveis relacionadas diretamente ao atraso poderiam gerar uma previsão irreal, pois continham informações posteriores ao evento que deveria ser previsto.

Para avaliar esse impacto, foram desenvolvidos dois cenários:

- Modelo utilizando informações comportamentais de atraso
- Modelo sem informações relacionadas ao atraso

O segundo cenário representa melhor uma aplicação real, utilizando apenas informações disponíveis antes da ocorrência da inadimplência.

---

# Modelagem

O algoritmo utilizado foi:

## Random Forest Classifier

O modelo foi escolhido por apresentar boa capacidade de lidar com:

- Relações não lineares entre variáveis
- Diferentes padrões de comportamento dos clientes
- Grande quantidade de atributos após o tratamento dos dados

Foram treinados dois modelos para comparação.

---

# Modelo 1 - Com informações de atraso

Este modelo utilizou variáveis relacionadas ao comportamento de atraso dos clientes.

Resultados:

```
Accuracy: 99%

Classe inadimplente:

Precision: 88%
Recall: 94%
F1-score: 91%
```

O modelo apresentou excelente desempenho, porém utiliza informações que podem representar vazamento de dados, pois estão diretamente relacionadas ao evento previsto.

---

# Modelo 2 - Sem informações de atraso

Neste cenário foram removidas variáveis relacionadas ao atraso, utilizando apenas informações disponíveis previamente.

Resultados:

```
Accuracy: 96%

Classe inadimplente:

Precision: 66%
Recall: 77%
F1-score: 71%
```

Este modelo apresenta uma avaliação mais realista para um ambiente produtivo de análise de crédito, pois busca prever o risco antes que o atraso aconteça.

---

# Conclusões

O desenvolvimento demonstrou a importância de avaliar não apenas o desempenho do modelo, mas também a qualidade das informações utilizadas durante o treinamento.

O primeiro modelo apresentou métricas superiores devido à utilização de informações relacionadas ao atraso, porém o segundo modelo representa melhor um cenário real de previsão antecipada de risco.

Como próximos passos, poderiam ser exploradas melhorias como:

- Ajuste de hiperparâmetros
- Testes com outros algoritmos de classificação
- Avaliação utilizando ROC-AUC
- Ajuste do threshold de classificação
- Técnicas para lidar com desbalanceamento de classes
- Análise da importância das variáveis

---

# Estrutura do projeto

```
case-datarisk-ds-junior/

├── data/
│
├── modelo_inadimplencia.ipynb
│
├── requirements.txt
│
├── README.md
│
└── Case DS Júnior 2025.pdf
```

---

# Como executar o projeto

Clone o repositório:

```bash
git clone https://github.com/gabrielfelip/case-datarisk-ds-junior.git
```

Crie um ambiente virtual:

```bash
python -m venv .venv
```

Ative o ambiente virtual:

Windows:

```bash
.venv\Scripts\activate
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

Execute o notebook:

```bash
jupyter notebook modelo_inadimplencia.ipynb
```

---

# Autor

Gabriel Felipe

Projeto desenvolvido para fins de estudo e portfólio em Ciência de Dados.