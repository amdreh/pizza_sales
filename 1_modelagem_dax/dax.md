# 🍕 Análise de Vendas de Pizzaria

## 1- Venda de pizza por sabor

Para responder quais são as cinco pizzas mais vendidas e as cinco menos vendidas, foi criada a medida `[faturamento_relativo]`.

```DAX
faturamento_relativo = 
SUMX( // SUMX é um somatório que percorre toda a tabela order_details linha a linha.
    order_details,
    order_details[quantity] * RELATED(pizzas[price]) // faturamento_relativo recebe somatório do produto da quantidade de pedidos com o preço das pizzas de dada linha.
)
```

### 1.1- Mais vendidas

#### Por faturamento

Para mostrar porcentagens absolutas no gráfico de barras com filtro n superior criei esta medida abaixo, que calcula a participação percentual de cada pizza no faturamento.

```DAX
faturamento_%_share = 
DIVIDE(
    [faturamento_relativo], 
    [faturamento_absoluto]
)
```

**Qual é a diferença entre faturamento e quantidade?**

- A quantidade mostra apenas o volume de produção (quais mais saíram do forno).
- O faturamento mostra quais pizzas geram mais dinheiro, considerando preço e margem.

#### Por quantidade

```DAX
qtd_vendida = SUM(order_details[quantity]) // [qtd_vendida] recebe o somatório da coluna quantidade da tabela order_details.
```

### 1.2. Menos vendidas

Utiliza as mesmas medidas já criadas.

---

## 2- Venda de pizza por tamanho

Utiliza as mesmas medidas já criadas anteriormente.

---

## 3- Desempenho das vendas mês a mês e trimestrais

- Uso de hierarquia na coluna `date` da tabela `orders`
- Medida utilizada: `[faturamento_relativo]`

### Perguntas respondidas:
- Qual trimestre tem as melhores vendas? Redobrar atenção a contratação de funcionários temporários e de estoque para dar conta da demanda. 
- Qual trimestre tem as piores vendas? Reduzir custos fixos renegociando contratos, cortando insumos e reduzindo o cardário, deixando de oferecer os sabores de pior faturamento.

---

## 4- Faturamento médio de cada dia da semana

### Perguntas respondidas:
- Qual dia tem as melhores médias de faturamento? Como a casa fica cheia, é sugerido ao marketing buscar aumentar o ticket médio. 
- Qual dia tem as piores médias de faturamento? É sugerido à equipe de marketing atrair o público com promoções ou um programa de compra coletiva. 

---

## 5- Margem de lucro x Share de vendas

### 5.1- Margem de lucro

**Observação:**
- Veggie = 25%
- Classic = 30%
- Chicken/Supreme = 40%
- Custo fixo adicional = $2

#### Custo total

```DAX
custo_total =

SUMX(
    order_details, // A função SUMX vai percorrer a tabela order_details linha a linha, fazer um somatório e retornar o resultado na medida custo_total.

    VAR Percentual =
        SWITCH(
            RELATED(pizza_types[category]),
            "Veggie", 0.25,
            "Classic", 0.3,
            "Chicken", 0.4,
            "Supreme", 0.4,
            0.3
        )

    VAR PrecoUnitario = RELATED(pizzas[price]) // A variável PrecoUnitario recebe o valor da coluna preço da tabela pizzas
    VAR Custo = 2 // A variável Custo recebe 2.

    RETURN

    ((PrecoUnitario * Percentual) + Custo) * order_details[quantity] 
)
```

#### Margem de lucro

```DAX
margem_lucro_perc = DIVIDE([lucro_liquido], [faturamento_relativo]) // margem_lucro_perc recebe a divisão do [lucro_liquido] pelo [faturamento_relativo].
```

---

### 5.2- Share de vendas por categoria

```DAX
share_vendas_por_cat =

VAR VendasCategoria = [faturamento_relativo]

VAR VendasDaLoja = CALCULATE([faturamento_relativo], ALL(pizza_types))

RETURN

DIVIDE (VendasCategoria, VendasDaLoja, 0)
```

**Por que usar margem + share?**

- Margem → mostra rentabilidade  
- Share → mostra popularidade  

---

### Share por pizza

```DAX
share_vendas_por_pizza =

VAR VendaSabor = [faturamento_relativo]
VAR VendaTotal = CALCULATE([faturamento_relativo], ALL(pizzas))

RETURN

DIVIDE(VendaSabor, VendaTotal, 0)
```

---

## Estratégia baseada em dados

| Share | Margem | Ação |
|------|--------|------|
| Alto | Alta | Focar no marketing |
| Alto | Baixa | Reduzir custos |
| Baixo | Alta | Fazer promoção |
| Baixo | Baixa | Retirar do cardápio |

---

## Sistema de estrelas (popularidade)

```DAX
estrelas_share = 
VAR Valor = [share_vendas_por_pizza]

VAR Ranking =
    IF(Valor >= 0.05, "★★★★★",
    IF(Valor >= 0.04, "★★★★",
    IF(Valor >= 0.03, "★★★",
    IF(Valor >= 0.02, "★★", 
    "★"))))

RETURN Ranking
```

---

## Margem de lucro percentual

O processo é o mesmo do cálculo de share, substituindo `[share_vendas_por_pizza]` por `[margem_lucro_perc]`.
