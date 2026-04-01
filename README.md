## 👤 Autor
**André Garcia** *Analista de Dados em transição do jornalismo cultural para o mercado de tecnologia. Em busca de oportunidade para atuar na transformação de dados brutos em inteligência estratégica e suporte à decisão.*

---

## 📖 Introdução
Este repositório documenta o desenvolvimento de uma solução de Business Intelligence (BI) para uma pizzaria fictícia, focada em transformar dados brutos em inteligência de negócio por meio de modelagem em DAX. Em vez de relatórios apenas visuais, priorizei o cálculo de margens reais e rentabilidade para criar a base estratégica dos futuros dashboards e relatórios de insights.

---

### ⚠️ Nota de Desenvolvimento
Atualmente, o projeto encontra-se na **Fase 1**. 
* **Concluído:** Arquitetura de dados, relacionamentos e dicionário de medidas DAX.
* **Próximas Etapas:** Design do Dashboard Interativo (UX/UI) e Relatório Final de Insights.

2# 🍕 Case Study: Inteligência de Negócio - Pizzaria Plej Granda

Este repositório apresenta o desenvolvimento de uma solução de Business Intelligence focada na análise de performance comercial e rentabilidade para uma operação de pizzas. O projeto visa transformar dados brutos em indicadores estratégicos para suporte à tomada de decisão.

> **Status do Projeto:** 🏗️ Fase 1 (Modelagem e Inteligência DAX) Concluída.

---

## 🚀 Objetivo do Projeto
O objetivo central é responder a perguntas críticas de negócio:
* Quais sabores sustentam o faturamento (Share de Vendas)?
* Qual a lucratividade real por categoria, considerando custos fixos e variáveis?
* Quais produtos são "Estrelas" e quais representam risco ao estoque?
* Como o faturamento se comporta sazonalmente (Visão Trimestral)?

---

## 📂 Estrutura do Repositório
Para garantir uma organização profissional e facilitar a manutenção, o projeto está estruturado da seguinte forma:

* **/data**: Base de dados bruta (arquivos .csv) contendo transações, produtos e categorias.
* **/Case_Study**: O núcleo do desenvolvimento analítico:
    * **01_modelagem_dax**: Contém o dicionário técnico com todas as métricas, variáveis e lógica de negócio implementadas.
    * **02_dashboard**: Local reservado para o arquivo fonte do Power BI (.pbix). *[Em desenvolvimento]*
    * **03_exports**: Relatórios de insights estratégicos e visualizações para consumo da gestão. *[Em desenvolvimento]*

---

## 🧠 Metodologia e Desenvolvimento

Nesta etapa inicial, foquei na construção da **Camada de Inteligência (DAX)**. Diferente de uma análise simples de faturamento, implementei regras de negócio complexas para refletir a realidade operacional:

1.  **Cálculo de Margem Real:** Implementação de custos variáveis distintos por categoria (Veggie, Classic, Chicken, Supreme) somados a custos fixos operacionais por unidade.
2.  **Matriz de Performance:** Cruzamento entre *Share* (Popularidade) e *Margem* (Rentabilidade) para classificar o cardápio.
3.  **Ranking de Estrelas:** Criação de um sistema de rating dinâmico para facilitar a leitura visual do desempenho de cada sabor.

---

## 🛠️ Tecnologias Utilizadas
* **Power BI / DAX:** Modelagem de dados e cálculos estatísticos.
* **Markdown:** Documentação técnica e estruturação do projeto.
* **GitHub:** Versionamento e exposição do portfólio.

---

## 📅 Roadmap de Evolução
O projeto segue um cronograma de entrega em fases:

- [x] **Fase 1:** Modelagem de Dados, Relacionamentos e Dicionário DAX.
- [ ] **Fase 2:** Desenvolvimento do Dashboard Interativo no Power BI (UX/UI Design).
- [ ] **Fase 3:** Publicação do Relatório Final de Insights e Recomendações de Negócio.

---
**Desenvolvido por André Garcia** *Analista de Dados em transição | Especialista em transformar dados em decisões estratégicas.*

