# Hands-on Engenharia de Dados Mackenzie

### Integrantes

|Nome                              |                          
|---------------------------       |
|Henrique Guilherme - RA: 10444658 |
|Mônica Dyna - RA: 10444608        |
|Renato Mori - RA: 10444622        |
|Vinícius Soares - RA: 10444899    |

# Visão Geral

### Show Data Project
A violência contra a mulher é um problema grave que afeta diretamente a saúde, segurança e direitos das mulheres. Analisando os dados de violência ao longo dos anos, podemos identificar tendências, padrões e áreas de maior risco, o que é fundamental para desenvolver políticas públicas eficazes e campanhas de conscientização.

### Objetivo 
Criar um MVP que possa ingerir dados públicos de violência contra a mulher no Estado de Minas Gerais, processá-los através das camadas de dados Bronze, Silver e Gold usando o Azure Data Factory para transformar esses dados e gerar insights valiosos para a formulação de políticas públicas e dar visibilidade à violência contra a mulher mudou ao longo dos anos. 

## Atividades técnicas para o MVP

1. Verificação dos arquivos brutos;
2. Levantamento de requisitos;
3. Definição e desenho da arquitetura;
4. Preparação do ambiente;
5. Desenvolvimento;
6. Teste e validação.

## [Checklist](https://github.com/orgs/Show-Instituto-de-Pesquisa/projects/1/views/1) 

![conceptual architecture](./images/checklist_sample.png)

## Requisitos
- Sistema resiliente;
- Deve suportar ingestão de dados em batch e em streaming;
- As camadas de dados devem manter rastreabilidade e serem isoladas umas das outras;
- O projeto não deve ultrapassar X reais de custo com ferramentas;
- Deve-se ter uma camada de governança de custos, dados sensíveis e linhagem de dados;
- O projeto deve suportar o consumo de dados para Analytics.

# Arquitetura

### Conceito Lambda
![conceptual architecture](./images/conceptual_architecture.png)

### O que é a arquitetura Lambda?
É um estilo de design de sistemas de processamento de dados que visa proporcionar uma solução robusta e eficiente para processar grandes volumes de dados em tempo real e em lote.

Ela foi criada para lidar com os desafios de Big Data e combina duas camadas principais de processamento: a `batch layer` e a `speed layer`. Além disso, há a serving layer que une os resultados dessas duas camadas para fornecer respostas rápidas às consultas.

---

### `Batch layer`
A batch layer é um dos componentes de uma arquitetura lambda, usada para processar grandes volumes de dados em intervalos regulares, realizando processamento em lote para gerar visões completas e precisas dos dados ao longo do tempo.

- Vantagens

    - Precisão dos Dados: O processamento em lote garante que todas as entradas de dados sejam consideradas, resultando em agregações e análises precisas.

    - Histórico Completo: Mantém um registro completo e imutável dos dados, permitindo reprocessamento e análises históricas.

 - Desvantagens

    - Latência: Não é adequada para necessidades de processamento em tempo real, pois há um atraso inerente ao processamento em lote.

    - Recursos Computacionais: Pode exigir uma grande quantidade de recursos computacionais, especialmente para grandes volumes de dados.

---

### `Speed layer`

A speed layer é uma parte crucial da arquitetura Lambda, projetada para processar dados em tempo real. Enquanto a batch layer lida com grandes volumes de dados de forma não urgente, a speed layer garante que os dados recentes sejam processados e disponibilizados quase instantaneamente. Isso permite que o sistema responda rapidamente a eventos e consultas.

- Vantagens
    - Processamento de Dados em Tempo Real: A função principal da speed layer é processar os dados em tempo real, ou seja, assim que os dados chegam, eles são imediatamente analisados e transformados. Isso permite que as informações mais recentes sejam rapidamente integradas ao sistema.

    - Atualizações Incrementais: Enquanto a batch layer processa grandes volumes de dados em lote, a speed layer faz atualizações incrementais, processando apenas os dados novos ou modificados desde a última execução. Isso reduz a quantidade de dados a ser processada e melhora a eficiência.

- Desvantagens
    - Complexidade de Implementação: Requer configuração e gerenciamento cuidadosos para garantir desempenho e confiabilidade.

    - Escalabilidade: Pode enfrentar desafios de escalabilidade dependendo do volume de dados e da carga de trabalho.

    - Custo: Se não for bem implementada, a arquitetura Lambda pode introduzir latências indesejadas em alguns casos de uso, o que pode não ser aceitável para certos negócios e pode requerer investimentos adicionais para otimização.

---


### Plataformas e soluções (Azure)
![architecture stack](./images/stack_architecture.png)

---

### Pipeline e tratamento de dados

![Azure Data Factory Pipeline](./images/adf_pipeline.png)

![Dataflow bronze para silver](./images/data_flow_bronze_to_silver.png)

![Dataflow silver para gold](./images/data_flow_silver_to_gold.png)

![Dados agregados por cidade](./images/aggregate_data.png)

---

<img src="./images/event-hubs.png" alt="drawing" width="40"/>

**Azure Event Hubs**: Plataforma de streaming de dados em tempo real que pode transmitir milhões de eventos por segundo com baixa latência. Compatível com Apache Kafka.

---
<img src="./images/data-lake.png" alt="drawing" width="40"/>

**Azure Data Lake Storage**: Solução de armazenamento de dados em nuvem projetada para grandes quantidades de dados estruturados e não estruturados, facilitando análises de Big Data.

---

<img src="./images/azure-synapse.jpg" alt="drawing" width="40"/>

**Azure Synapse Analytics**: Plataforma de análise integrada que combina data warehousing e análise de Big Data, permitindo análises avançadas e insights em tempo real.

---
<img src="./images/data-factory.png" alt="drawing" width="40"/>

**Azure Data Factory**: Serviço de integração de dados que automatiza e orquestra processos de ETL (Extração, Transformação, Carregamento) e integração de dados entre diferentes fontes.

---
<img src="./images/power-bi.png" alt="drawing" width="50"/>

**Microsoft Power BI**: Ferramenta de visualização de dados que permite criar dashboards interativos e relatórios para ajudar na tomada de decisões com base em dados.

---
<img src="./images/azure-ml.png" alt="drawing" width="40"/>

**Azure ML**: Plataforma de machine learning que facilita a criação, treinamento e implantação de modelos de machine learning.

---
<img src="./images/azure-kv.png" alt="drawing" width="40"/>

**Azure Key Vault**: Serviço de gerenciamento de segredos que armazena e controla o acesso a senhas, certificados, chaves de criptografia e outros segredos.

---
<img src="./images/azure-purview.png" alt="drawing" width="40"/>

**Azure Purview**: Serviço de governança de dados que ajuda a descobrir, entender e gerenciar dados em toda a organização, garantindo conformidade e segurança.

---
<img src="./images/azure-cost.png" alt="drawing" width="40"/>

**Azure Cost Management**: Conjunto de ferramentas que ajudam as organizações a analisar, monitorar e otimizar os custos com o Microsoft Cloud. Oferece relatórios detalhados e alertas para ajudar a controlar os gastos.

---

<img src="./images/azure-monitor.jpg" alt="drawing" width="40"/>

**Azure Monitor** : Solução de monitoramento que coleta, analisa e responde a dados de monitoramento de ambientes de nuvem e locais. Ajuda a maximizar a disponibilidade e o desempenho dos aplicativos e serviços.

## Calculadora de custos

## Insights e conclusão
<!-- 
    Insights de dados

    Conclusão sobre o projeto visão técnica e de negócios
    Mencionar  Machine Learning e PowerBI
    Falar sobre arquitetura e custos
    Dificuldades e lessons learned
    Possibilidades de melhoria pro futuro
 -->