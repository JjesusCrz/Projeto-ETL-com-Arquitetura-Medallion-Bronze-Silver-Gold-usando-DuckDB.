🏗 Projeto ETL com Arquitetura Medallion (Bronze, Silver, Gold) usando DuckDB
📌 Sobre o Projeto

Este projeto foi desenvolvido como parte de uma pós-graduação em Engenharia de Dados com o objetivo de construir um pipeline ETL completo utilizando dados extraídos de um arquivo CSV oriundo do SAP.

A solução foi construída seguindo o padrão Medallion Architecture (Bronze → Silver → Gold), aplicando boas práticas de ingestão, tratamento, refinamento e modelagem de dados para consumo analítico.

🎯 Objetivos

Realizar ingestão de dados brutos (raw) em camada Bronze

Aplicar limpeza, tipagem e deduplicação na camada Silver

Construir camada Gold orientada ao consumo analítico

Persistir todas as camadas em banco DuckDB

Aplicar versionamento com Git

Desenvolver o pipeline utilizando Jupyter Notebook no VS Code

🛠 Tecnologias Utilizadas

Python

Pandas

DuckDB

SQL

Datetime

OS

Jupyter Notebook (VS Code)

Git (versionamento)

🧱 Arquitetura do Projeto
CSV (origem SAP)
        ↓
🥉 Bronze - Dados brutos + histórico
        ↓
🥈 Silver - Dados tratados + última versão por produto
        ↓
🥇 Gold - Dimensão pronta para consumo analítico

🥉 Camada Bronze — Raw Data
Objetivo

Armazenar os dados exatamente como recebidos do SAP, mantendo histórico e rastreabilidade.

Principais ações realizadas:

Leitura do CSV com Pandas

Inclusão das colunas:

data_ingestao

nome_arquivo

Criação da tabela bronze_z0019

Persistência no banco dados_duckdb.db

Características:

Dados sem transformação estrutural

Preservação do formato original

Permite auditoria e reprocessamento

🥈 Camada Silver — Dados Tratados
Objetivo

Limpar, padronizar e consolidar os dados.

Transformações realizadas:

Remoção de colunas técnicas (data_ingestao, nome_arquivo)

Deduplicação utilizando:

ROW_NUMBER() OVER (PARTITION BY NATBR ORDER BY data_ingestao DESC)


Seleção da versão mais recente por produto

Renomeação de colunas técnicas do SAP para nomes semânticos

Conversão de tipos (int32, float32)

Resultado:

Tabela produtos contendo dados limpos e consolidados.

🥇 Camada Gold — Modelagem Analítica
Objetivo

Preparar os dados para consumo por ferramentas de BI ou análises estratégicas.

Implementação:

Criação da dimensão dim_produtos

Seleção apenas das colunas relevantes para consumo:

id

nm_produto

vl_preco

Resultado:

Estrutura simplificada, orientada ao negócio.

🗄 Estrutura do Banco de Dados

Banco criado:

dados_duckdb.db


Tabelas criadas:

bronze_z0019

produtos

dim_produtos

📂 Estrutura do Repositório
├── notebooks/
│   ├── bronze.ipynb
│   ├── silver.ipynb
│   └── gold.ipynb
│
├── dados_duckdb.db
├── README.md
└── .gitignore

🔄 Versionamento

O projeto foi versionado utilizando Git, permitindo:

Controle de versões

Histórico de alterações

Evolução incremental do pipeline

🧠 Conceitos Aplicados

Arquitetura Medallion

ETL / ELT

Deduplicação com Window Functions

Tipagem de dados

Persistência em banco analítico

Separação de responsabilidades por camada

Modelagem dimensional (dimensão)

🚀 Possíveis Evoluções

Implementar tabela fato

Construir modelo estrela

Automatizar execução do pipeline

Adicionar validações de qualidade de dados

Implementar testes

Containerizar com Docker

Orquestrar com Airflow

📊 Resultado Final

O projeto demonstra a construção de um pipeline estruturado e organizado, simulando um ambiente real de Engenharia de Dados, desde a ingestão até a modelagem analítica.

👨‍💻 Autor

Joel
Projeto desenvolvido como parte de especialização em Engenharia de Dados.
