# [ESTUDO DE CASO] Aquele da Pizzaria🍕 

![Status](https://img.shields.io/badge/Status-Fase%201%20Conclu%C3%ADda-green)
![Tecnologia](https://img.shields.io/badge/Tecnologia-Power%20BI%20%2F%20DAX-yellow)

## 👤 Autor
**André Garcia** *Analista de Dados em transição do jornalismo cultural para o mercado de tecnologia. Em busca de oportunidade para atuar na transformação de dados brutos em inteligência estratégica e suporte à decisão.*

---

## 📖 Sobre o Projeto

### Introdução
Este repositório documenta o desenvolvimento de uma solução de Business Intelligence (BI) para uma pizzaria fictícia, focada em transformar dados brutos em inteligência de negócio por meio de modelagem em DAX. Em vez de relatórios apenas visuais, priorizei o cálculo de margens reais e rentabilidade para criar a base estratégica dos futuros dashboards e relatórios de insights.

Este projeto visa transformar dados transacionais em indicadores estratégicos para suporte à tomada de decisão, analisando a performance comercial e a saúde financeira da operação.

---

### 🚀 Objetivo do Projeto
O objetivo central é responder a perguntas críticas de negócio:
* Quais são as 5 melhores e as 5 piores pizzas por faturamento e por quantidade vendida?
* Qual é o tamanho de pizza mais vendido?
* Qual foi o faturamento mês a mês do ano? E trimestre a trimestre?
* Qual foi o faturamento médio de cada dia da semama?

Além disso, o projeto realiza um **comparativo entre o Share de Vendas e a Margem de Lucro** para orientar decisões estratégicas, como:
* Identificar em quais sabores focar as ações de marketing.
* Analisar onde é necessário reduzir custos operacionais.
* Definir quais produtos devem receber promoções ou serem retirados do cardápio.

---

### 🧠 Metodologia e Desenvolvimento
Na primeira fase, utilizei código DAX para implementar regras de negócio robustas em uma análise de faturamento:

1. **Cálculo de Margem Real:** Implementação de lógica para estimativa de custo de pizza por categoria (Veggie, Classic, Chicken, Supreme) considerando custos operacionais variáveis.
2. **Matriz de Performance:** Cruzamento entre *Share* (Popularidade) e *Margem* (Rentabilidade) para classificação estratégica do mix de produtos.
3. **Ranking de Estrelas:** Criação de um sistema de rating dinâmico para facilitar a leitura visual do desempenho de cada sabor no modelo.

---

### 📂 Estrutura do Repositório
Os arquivos do projeto estão organizados da seguinte forma:

* **1_modelagem_dax**: Contém o arquivo `dax.md`, com a documentação e explicação de cada medida criada.
* **2_dashboard**: Local reservado para os dashboards que responderão às questões propostas. *(Em desenvolvimento)*
* **3_relatorio**: Espaço para o relatório analítico comparativo entre share e margem. *(Em desenvolvimento)*
* **data**: Base de dados original (arquivos .csv) disponibilizada via Kaggle.
* **README.md**: Documentação principal e apresentação do projeto.

---

### 🛠️ Tecnologias Utilizadas
* **Power BI / DAX:** Modelagem de dados e inteligência de negócio.
* **Markdown:** Documentação técnica e estruturação do projeto.
* **GitHub:** Versionamento e exposição do portfólio.

---

### 📅 Roadmap de Evolução
- [x] **Fase 1:** Modelagem de Dados, Relacionamentos e Dicionário DAX.
- [ ] **Fase 2:** Desenvolvimento do Dashboard Interativo no Power BI (UX/UI Design).
- [ ] **Fase 3:** Publicação do Relatório Final de Insights e Recomendações.

---
**Desenvolvido por André Garcia** *Analista de Dados em transição*
