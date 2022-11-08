CONS_CARTEIRA_SALDO ( Saldo de Carteiras ) View

| Nome da Campo    | Título                  | Tipo      | Máscara        | Tamanho |
| --------------   | ----------------------  | --------- | -------------- | ------- |
| CAR_ID           | ID da Carteira          |           |                |         |
| CAR_NOME         | Nome da Carteira        |           |                |         |
| Saldo            | Saldo                   | Numérico  | 99.999.999,99  | 10      |
| Pendente         | Pendente                | Numérico  | 99.999.999,99  | 10      |


Script da Views

```sql
    Select Cons_lancamentos.CAR_ID, 
        Cons_lancamentos.CAR_NOME, 
        Sum(Case When Cons_lancamentos.PAGO = 'Não' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Pendente, 
        Sum(Case When Cons_lancamentos.PAGO = 'Sim' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Saldo 
    From Cons_lancamentos 
    Group By Cons_lancamentos.CAR_ID, Cons_lancamentos.CAR_NOME
```

| Nome da Campo    | Título                  | Tipo      | Máscara        | Tamanho |
| --------------   | ----------------------  | --------- | -------------- | ------- |
| Mes              | Mês                     | Caracter  |                | 10      |
| Tipo             | Tipo                    | Caracter  |                | 10      |
| Valor            | Saldo                   | Numérico  | 99.999.999,99  | 10      |

Script da Views

```sql
    Select Top 24 tb.Mes, tb.Tipo, tb.Valor, tb.A, tb.M 
    From (
            Select Top 1000 
                Format(Cons_lancamentos.LANC_DATA_VENC, 'MM/yyyy') As Mes, 
                'Receitas' As Tipo, 
                Sum(Cons_lancamentos.LANC_VALOR) As Valor, 
                Year(Cons_lancamentos.LANC_DATA_VENC) As A, 
                Month(Cons_lancamentos.LANC_DATA_VENC) As M 
            From Cons_lancamentos 
            Where Cons_lancamentos.LANC_DATA_VENC Between DateAdd(M, -5, GetDate()) And DateAdd(M, +6, GetDate()) And Cons_lancamentos.LANC_TIPO = 'Receita' 
            Group By Format(Cons_lancamentos.LANC_DATA_VENC, 'MM/yyyy'), Year(Cons_lancamentos.LANC_DATA_VENC), Month(Cons_lancamentos.LANC_DATA_VENC) 
        
        Union All 
        
            Select Top 1000 
                Format(Cons_lancamentos.LANC_DATA_VENC, 'MM/yyyy') As Mes, 
                'Despesas' As Tipo, 
                Sum(Cons_lancamentos.LANC_VALOR * -1) As Valor, 
                Year(Cons_lancamentos.LANC_DATA_VENC) As A, 
                Month(Cons_lancamentos.LANC_DATA_VENC) As M 
            From Cons_lancamentos 
            Where Cons_lancamentos.LANC_DATA_VENC Between DateAdd(M, -5, GetDate()) And DateAdd(M, +6, GetDate()) And Cons_lancamentos.LANC_TIPO = 'Despesa' 
            Group By Format(Cons_lancamentos.LANC_DATA_VENC, 'MM/yyyy'), Year(Cons_lancamentos.LANC_DATA_VENC), Month(Cons_lancamentos.LANC_DATA_VENC)
        ) As tb 
    Order By tb.A, tb.M
```