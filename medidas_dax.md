# Medidas DAX

## Atrasos
% Atrasos = 
AVERAGE(Dim_Pedidos[Atrasado])

## Avaliações 1 Estrela
% Avaliações 1 Estrela = 
DIVIDE(
    CALCULATE(
        COUNTROWS(Dim_Avaliacoes),
        Dim_Avaliacoes[review_score] = 1
    ),
    COUNTROWS(Dim_Avaliacoes)
)

## Avaliações 5 Estrela
% Avaliações 5 Estrelas = 
DIVIDE(
    CALCULATE(
        COUNTROWS(Dim_Avaliacoes),
        Dim_Avaliacoes[review_score] = 5
    ),
    COUNTROWS(Dim_Avaliacoes)
)

## Frete Médio
Frete Médio = 
AVERAGE(
    Fato_Vendas[freight_value]
)

## Frete Total
Frete Total = 
SUM(Fato_Vendas[freight_value])

## Nota Média Categoria
Nota Média Categoria = 
AVERAGE(
Analise_Avaliacoes_Categoria[review_score]
)

## Nota Média Seller
Nota Média Seller = 
CALCULATE(
    AVERAGE(Dim_avaliacoes[review_score]),
    ALLEXCEPT(
        Dim_sellers,
        Dim_sellers[seller_id]
    )
)

## Pedidos
Pedidos = 
DISTINCTCOUNT(Fato_Vendas[order_id])

## Quantidade Seller
Quantidade Sellers = 
DISTINCTCOUNT(
    Dim_sellers[seller_id]
)

## Receita
Receita = 
SUM(Fato_Vendas[price])

## Receita por Seller
Receita por Seller = 
DIVIDE(
    [Receita],
    [Quantidade Sellers]
)

## Tempo Médio Entrega
Tempo Médio Entrega = 
AVERAGEX(
    Dim_Pedidos,
    DATEDIFF(
        Dim_Pedidos[order_purchase_timestamp],
        Dim_Pedidos[order_delivered_customer_date],
        DAY
    )
)

## Ticker Médio
Ticket Médio = 
DIVIDE(
    [Receita],
    [Pedidos]
)
