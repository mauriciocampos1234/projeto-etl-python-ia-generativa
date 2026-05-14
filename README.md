# Projeto: ETL com Python e IA Generativa

Este projeto implementa um pipeline **ETL (Extract, Transform, Load)** para um cenário bancário, onde dados de clientes são enriquecidos com mensagens personalizadas geradas por IA (Gemini) e enviados de volta para uma API.

## Do que se trata

- Lê IDs de clientes em um arquivo CSV.
- Busca os dados de cada cliente em uma API bancária (`GET /users/{id}`).
- Gera mensagens de marketing personalizadas sobre investimentos usando IA generativa.
- Atualiza os clientes na API com essas mensagens (`PUT /users/{id}`), preenchendo o campo `news`.

## Objetos do projeto (principais artefatos e entidades)

### Artefatos
- `notebooks/desafio-etl-jupyter-notebook.ipynb`  
  Notebook principal com todo o fluxo ETL.
- `dados/ids-clientes.csv`  
  Lista de IDs dos clientes usados na extração.
- `dados/dados-a-serem-populados.md`  
  Guia auxiliar para popular e testar dados na API.
- `.devcontainer/`  
  Configuração de ambiente para execução em container.

### Entidades de dados
- **Cliente (`user`)**: registro principal retornado pela API.
- **Account**: dados de conta bancária (número, agência, saldo, limite).
- **Card**: dados de cartão (número mascarado, limite).
- **News**: lista de mensagens/novidades adicionadas ao cliente (ícone + descrição).

### Componentes lógicos no notebook
- **Extract**: leitura do CSV + requisições `GET`.
- **Transform**: geração de mensagens com Gemini e controle de cota (classe `AdvancedQuotaManager`).
- **Load**: envio dos dados enriquecidos via `PUT`.
