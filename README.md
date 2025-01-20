# Previsão de Aluguéis de Bicicletas com Machine Learning Automatizado

Este repositório fornece um guia passo a passo para treinar e implantar um modelo de machine learning automatizado no Azure Machine Learning, com o objetivo de prever o número de aluguéis de bicicletas com base em dados históricos.

## Visão Geral

Utilizaremos o Azure Machine Learning para:

1. **Criar um workspace**: Configurar o ambiente de trabalho no Azure.
2. **Carregar e preparar os dados**: Importar o conjunto de dados histórico de aluguéis de bicicletas.
3. **Configurar e executar o AutoML**: Definir as configurações para o treinamento automatizado do modelo.
4. **Implantar o modelo**: Disponibilizar o modelo treinado para uso em previsões.

## Passo a Passo

### 1. Criar um Workspace do Azure Machine Learning

1. Acesse o [Portal do Azure](https://portal.azure.com/) e faça login com suas credenciais.
2. Selecione **+ Criar um recurso** e procure por **Machine Learning**.
3. Crie um novo recurso com as seguintes configurações:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie ou selecione um existente.
   - **Nome**: Nome único para o workspace.
   - **Região**: Selecione a região geográfica mais próxima.
4. Após a criação, acesse o recurso e selecione **Iniciar o estúdio** para abrir o Azure Machine Learning Studio.

### 2. Carregar e Preparar os Dados

1. No Azure Machine Learning Studio, navegue até a seção **Conjuntos de dados**.
2. Selecione **+ Criar conjunto de dados** e escolha **A partir de arquivos locais**.
3. Configure o conjunto de dados:
   - **Nome**: `bike-rentals`
   - **Descrição**: `Dados históricos de aluguéis de bicicletas`
   - **Tipo de dados**: Tabela (mltable)
4. Faça o upload dos arquivos de dados disponíveis em [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals).

### 3. Configurar e Executar o AutoML

1. No Azure Machine Learning Studio, acesse a seção **ML Automatizado**.
2. Crie um novo experimento com as seguintes configurações:
   - **Nome do experimento**: `mslearn-bike-rental`
   - **Tipo de tarefa**: Regressão
   - **Conjunto de dados**: Selecione `bike-rentals`
   - **Coluna de destino**: `rentals`
3. Nas configurações adicionais:
   - **Métrica primária**: `NormalizedRootMeanSquaredError`
   - **Modelos permitidos**: Selecione apenas `RandomForest` e `LightGBM`
   - **Limites**:
     - **Avaliações máximas**: `3`
     - **Máximo de avaliações simultâneas**: `3`
     - **Tempo limite de experimento (minutos)**: `15`
     - **Tempo limite de iteração (minutos)**: `15`
4. Inicie o experimento e aguarde a conclusão do treinamento.

### 4. Implantar o Modelo

1. Após a conclusão do experimento, selecione o melhor modelo identificado.
2. Clique em **Implantar** e configure o endpoint de serviço:
   - **Nome do serviço**: `bike-rental-predictor`
   - **Tipo de computação**: ACI (Azure Container Instance)
3. Após a implantação, teste o endpoint fornecendo novos dados para prever o número de aluguéis de bicicletas.

## Referências

- [Documentação Oficial do Exercício](https://microsoftlearning.github.io/mslearn-ai-fundamentals.pt-br/Instructions/Labs/01-machine-learning.html)
- [Princípios Básicos do Aprendizado de Máquina](https://learn.microsoft.com/pt-br/training/modules/fundamentals-machine-learning/)

---

Este guia foi elaborado com base na documentação oficial da Microsoft para auxiliar no treinamento e implantação de modelos de machine learning automatizados no Azure.
