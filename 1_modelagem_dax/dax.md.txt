# 🍕 Análise de Vendas de Pizzaria

## Venda de pizza por sabor

Para responder quais são as cinco pizzas mais vendidas e as cinco menos vendidas, foi criada a medida `[total_vendas]`.

### 1.1. Mais vendidas

#### Por faturamento

```DAX
total_vendas = 
SUMX( // SUMX é um somatório que percorre toda a tabela order_details linha a linha.
    order_details,
    order_details[quantity] * RELATED(pizzas[price]) // total_vendas recebe somatório do produto da quantidade de pedidos com o preço das pizzas de dada linha.
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

## Venda de pizza por tamanho

Utiliza as mesmas medidas já criadas anteriormente.

---

## Desempenho das vendas trimestrais

- Uso de hierarquia na coluna `date` da tabela `orders`
- Medida utilizada: `[total_vendas]`

### Perguntas respondidas:
- Qual trimestre tem as melhores vendas?
- Qual trimestre tem as piores vendas?

---

## Margem de lucro x Share de vendas

### 4.1. Margem de lucro

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
margem_lucro_perc = DIVIDE([lucro_liquido], [total_vendas]) // margem_lucro_perc recebe a divisão do [lucro_liquido] pelo [total_vendas].
```

---

### 4.2. Share de vendas por categoria

```DAX
share_vendas_por_cat =

VAR VendasCategoria = [total_vendas]

VAR VendasDaLoja = CALCULATE([total_vendas], ALL(pizza_types))

RETURN

DIVIDE (VendasCategoria, VendasDaLoja, 0)
```

**Por que usar margem + share?**

- Margem → mostra rentabilidade  
- Share → mostra popularidade  

---

### 4.3. Share por pizza

```DAX
share_vendas_por_pizza =

VAR VendaSabor = [total_vendas]
VAR VendaTotal = CALCULATE([total_vendas], ALL(pizzas))

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
