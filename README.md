# Projeto ETL Comercial – Departamento de Vendas

## 📌 Visão Geral
Este projeto implementa um fluxo **ETL** (Extração, Transformação e Carga) para o **departamento comercial**, extraindo dados do banco transacional `PlantAndHealth` e preparando-os para **análises estratégicas** no **Excel** e **Power BI**.

O objetivo principal é **integrar e otimizar o acesso aos dados de vendas**, permitindo que a equipe comercial tome decisões mais rápidas e precisas, sem sobrecarregar o banco transacional.

---

## 🎯 Objetivos do Projeto
- Extrair informações comerciais dos últimos **3 anos** do banco de dados transacional.
- Organizar os dados históricos e recentes em **arquivos Parquet** para consultas otimizadas.
- Processar e preparar os dados para consumo direto no Excel e Power BI.
- Reduzir a carga no banco transacional com **cargas incrementais** e armazenamento em formato colunar.

---

## ⚙️ Tecnologias Utilizadas
- **Python** – Automação e manipulação de dados
- **SQLAlchemy** – Conexão e consultas SQL no banco transacional
- **Pandas** – Processamento e manipulação de dados
- **DuckDB** – Integração, junção e processamento de dados
- **Parquet** – Armazenamento otimizado para análise
- **Power BI / Excel** – Consumo final dos dados

---

## 📂 Estrutura do Projeto

etl_comercial/
│
├── dags/ # Scripts e fluxos de execução
├── data/ # Arquivos Parquet gerados
├── notebooks/ # Testes e prototipagem
├── requirements.txt # Dependências do projeto
└── README.md # Documentação do projeto


---

## 🛠️ Etapas do Processo ETL

1. **Extração**
   - Conexão ao banco `PlantAndHealth` via SQLAlchemy.
   - Extração de:
     - **Histórico de 3 anos** → `vendas_passados.parquet`
     - **Dados recentes (último ano/mês)** → `vendas_recentes.parquet`
   - Objetivo: preservar históricos completos e permitir cargas rápidas com dados mais recentes.

2. **Transformação**
   - Leitura dos arquivos Parquet com **DuckDB**.
   - União das bases históricas e recentes.
   - Processamento adicional para padronização e enriquecimento dos dados.

3. **Carga**
   - Exportação para arquivos Parquet otimizados para consulta.
   - Disponibilização para consumo direto em **Excel** e **Power BI**.

---

## 📊 Benefícios do Projeto
- **Performance**: consultas mais rápidas graças ao uso de arquivos Parquet.
- **Eficiência operacional**: redução do tempo de carregamento no Power BI e Excel.
- **Baixa carga no banco de produção**: evita consultas pesadas no banco transacional.
- **Organização**: dados históricos e atuais organizados em um pipeline claro.

---

## 🔎 Diagrama do Fluxo de Dados
```mermaid
flowchart LR
    A[Banco Transacional PlantAndHealth] -->|SQLAlchemy + Pandas| B[Parquet - Vendas Passados]
    A -->|SQLAlchemy + Pandas| C[Parquet - Vendas Recentes]
    B -->|DuckDB| D[Dados Integrados e Processados]
    C -->|DuckDB| D
    D -->|Parquet Final| E[Excel / Power BI]

