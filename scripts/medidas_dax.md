# Medidas DAX

## Quantidade de Ações Massivas
```DAX
Qtd Ações = DISTINCTCOUNT(Acionamentos[ID_Acao])
```

## Quantidade de clientes 
```DAX
QTD_CLI = DISTINCTCOUNT(Clientes[ID_Cliente])
```

## Quantidade de contratos 
```DAX
QTD_CONTRATOS = DISTINCTCOUNT(Contratos[ID_Contrato])
```

## Resultado de Pagamento por Status 
```DAX
RESULTADO_PAGAMENTO = 
CALCULATE(
    DISTINCTCOUNT(Acionamentos[ID_Divida]),
    Acionamentos[Resultado] IN {
        "PAGAMENTO PARCIAL",
        "PROMESSA DE PAGAMENTO"
    }
)
```

## Somatoria do saldo da carteira
```DAX
VALOR_CARTEIRA = SUM(Contratos[Valor_Original])
```

## Ticket Médio da carteira 
```DAX
TKM_CARTEIRA = DIVIDE([VALOR_CARTEIRA], [QTD_CLI],0)
```

## Total de Acionamentos
```DAX
% Resultado = 
DIVIDE(
    [Qtd Ações],
    CALCULATE(
        [Qtd Ações],
        ALL(Acionamentos[Resultado])
    )
)
```

## % Representatividade de pagamento
```DAX
%RET_PAGO = 
DIVIDE([RESULTADO_PAGAMENTO],[Qtd Ações],0)
```
