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
Sendo [faturamento_absoluto]:

```DAX
faturamento_absoluto = 
CALCULATE(
    [faturamento_relativo], 
    ALL(pizza_types)
)
```

>**Qual é a diferença entre faturamento e quantidade?**
>
>- A quantidade mostra apenas o volume de produção (quais mais saíram do forno).
>- O faturamento mostra quais pizzas geram mais dinheiro, considerando preço e margem.

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
custo_estimado =

SUMX(
    order_details, // A função SUMX vai percorrer a tabela order_details linha a linha, fazer um somatório e retornar o resultado na medida custo_estimado.

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
margem_lucro_perc = DIVIDE([lucro_liquido], [faturamento_relativo],0)  // margem_lucro_perc recebe a divisão do [lucro_liquido] pelo [faturamento_relativo].
```

---

### 5.2- Share de vendas por categoria

```DAX
share_vendas_por_cat = 
//Criei a variável VendasCategoria recebendo o conteúdo de total vendas
VAR VendasCategoria = [faturamento_relativo]

//Criei a variável VendaDaLoja recebendo o somatório dos valores de vendas_total em sua integralidade, ignorando qualquer restrição de filtros que atuem sobre a tabela pizza_types 
VAR VendasDaLoja = CALCULATE([faturamento_relativo], ALL(pizza_types))

RETURN
//Após o return é feita a operação propriamente dita, dividindo as variáveis acima criadas uma pela outra. O zero é o valor alternativo a ser utilizado caso a divisão tenha um resultado inválido
DIVIDE (vendasCategoria, VendasDaLoja, 0)
```

**Por que usar margem + share?**

- Margem → mostra rentabilidade  
- Share → mostra popularidade  

---

### Share por pizza

```DAX
share_vendas_por_pizza = 
VAR VendaSabor = [faturamento_relativo]
VAR VendaTotal = CALCULATE([faturamento_relativo], ALL(pizzas)) // Ignora os filtros da pizza e pega o total geral

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

```DAX
estrelas_margem = 
VAR Valor = [margem_lucro_perc]
RETURN
    IF(Valor >= 0.60, "★★★★★",
    IF(Valor >= 0.56, "★★★★",
    IF(Valor >= 0.52, "★★★",
    IF(Valor >= 0.49, "★★", 
    "★"))))
```
## 6- Outras medidas

```DAX
faturamento_medio_por_dia = 
AVERAGEX( // Calcula a média linha por linha
    VALUES(orders[date]), // Pega as datas da coluna date sem repetições.
    [faturamento_relativo]
)

// Se fosse pegar datas repetidas, o cálculo consideraria cada pedido do dia. 
```

```DAX

lucro_liquido = [faturamento_relativo]-[custo_estimado]
```

```DAX
maiores_piores_faturamentos = 
VAR _rank_top = RANKX(ALL(pizza_types[name]), [faturamento_relativo], , DESC, DENSE) // Cria uma variável que classifica todas as pizzas por faturamento, em ordem decrescente e mantendo valores empatados

VAR _rank_bottom = RANKX(ALL(pizza_types[name]), [faturamento_relativo], , ASC, DENSE) // A única diferença para o bloco de cima é a ordem crescente

VAR _resultado = IF(_rank_top <= 5, [faturamento_relativo], IF(_rank_bottom <= 5, [faturamento_relativo], BLANK())) // Se a pizza estiver entre as cinco primeiras ou as cinco últimas em faturamento, mostra seu faturamento. 

RETURN _resultado
```

```DAX
maiores_piores_qtd_vendida = // Segue o mesmo princípio do anterior, mas trocando o faturamento pela quantidade de pizzas vendidas

VAR _rank_top = RANKX(ALL(pizza_types[name]), [qtd_vendida], , DESC, DENSE)

VAR _rank_bottom = RANKX(ALL(pizza_types[name]), [qtd_vendida], , ASC, DENSE)

VAR _resultado = IF(_rank_top <= 5, [qtd_vendida], IF(_rank_bottom <= 5, [qtd_vendida], BLANK()))

RETURN _resultado
```

```DAX
rank_cor_qtd_vendida = RANKX(ALL(pizza_types[name]), [qtd_vendida], , DESC, DENSE) // Classifica as pizzas por quantidade vendida em ordem decrescente. É usado na formatação condicional que muda a cor no gráfico Ranking: maiores e menores vendas
```

```DAX
rank_cor_faturamento = 
RANKX(ALL(pizza_types[name]), [faturamento_relativo], , DESC, DENSE) // Similar ao código acima, só que pegando o faturamento em vez da quantidade
```
