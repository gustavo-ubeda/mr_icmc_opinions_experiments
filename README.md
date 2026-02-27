# Análise de Reclamações

Este projeto utiliza técnicas de processamento de linguagem natural e aprendizado de máquina para analisar reclamações de clientes, extrair informações e treinar modelos para prever a qualidade do atendimento.

## Etapas do Processo

O fluxo de trabalho é dividido em várias etapas, cada uma implementada em um notebook Jupyter.

### 1. Criação da Base de Dados (`1_database_create.ipynb`)

Nesta etapa, os dados brutos são coletados de duas fontes distintas:

- **Reclame Aqui:** Dados de reclamações extraídos através de um scraper.
- **Consumidor.gov:** Arquivos CSV contendo reclamações.

Os dados são unificados em um único DataFrame e salvos no formato Parquet (`db_reclamacoes.parquet`) para as próximas fases. Acesse https://drive.google.com/file/d/1V6tA_fRnLrZJXZv8zDxVXCmW494XNhcu/view?usp=sharing para ter acesso direto aos dados adquiridos para a pesquisa.

### 2. Pré-processamento e Limpeza (`2_database_preprocess.ipynb`)

O notebook realiza a limpeza e a preparação dos dados brutos. As principais atividades incluem:

- Análise exploratória para entender a distribuição dos dados.
- Conversão da nota de atendimento em uma classificação binária (Bom/Ruim).
- Remoção de dados duplicados, nulos e colunas irrelevantes.
- Filtragem de empresas com baixo volume de dados ou classes muito desbalanceadas.
- O resultado é salvo em `db_reclamacoes_clean.parquet`.

### 3. Extração de Features com LLM (`3_feature_extractions.ipynb`)

Utilizando um modelo de linguagem avançado (GPT), esta etapa enriquece os dados com informações estruturadas. Para cada par de reclamação e resposta, o modelo é instruído a:

- Gerar resumos anonimizados da reclamação e da resposta.
- Extrair o tipo de reclamação, o produto/serviço envolvido e palavras-chave.
- Analisar a qualidade da resposta da empresa (genérica, parcial ou específica).
- Os dados enriquecidos são salvos em um arquivo CSV.

### 4. Vetorização de Texto (`4_vectorizing.ipynb`)

Aqui, os dados textuais gerados na etapa anterior são transformados em vetores numéricos (embeddings) para que possam ser utilizados pelos modelos de machine learning. Diferentes técnicas são aplicadas:

- **Clássicas:** Bag-of-Words (BoW) e TF-IDF.
- **Transformers:** BERT, DistilBERT, RoBERTa, e outros modelos de embeddings.
- **OpenAI:** Embeddings da OpenAI.

Os vetores resultantes são adicionados ao conjunto de dados e salvos em um novo arquivo CSV.

### 5. Modelagem e Treinamento (`5_modeling_basic.ipynb` e `5_modeling_advanced.ipynb`)

Nesta fase final, diferentes modelos de aprendizado de máquina são treinados e avaliados para prever a qualidade do atendimento com base nos vetores gerados.

- **Modelos Tradicionais:** São utilizados classificadores como `Random Forest`, `SVM` e `MLP (Multi-layer Perceptron)`.
- **Redes Neurais (CNN):** Um modelo de rede neural convolucional também é treinado e avaliado.

Os resultados, incluindo métricas de performance como F1-score, precisão e recall, são salvos em uma planilha (`reclamacoes_results.xlsx`) e visualizados em gráficos para comparação entre os diferentes modelos e técnicas de vetorização.

## Como executar

Para instalar as dependências do projeto, execute o seguinte comando:

```bash
pip install -r requirements.txt
```

Depois, execute os notebooks na ordem numérica para reproduzir todo o processo.