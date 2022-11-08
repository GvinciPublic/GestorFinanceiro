CONS_LANCAMENTOS ( Lançamento )

| Nome da Campo    | Título                  | Tipo      | Máscara             | Tamanho | Permite Nulo |
| --------------   | ----------------------  | --------- | ------------------- | ------- | ------------ |
| LANC_ID          | ID de Lançamento        |
| LANC_DESCRICAO   | Descrição do Lançamento |
| LANC_DATA_VENC   | Data de Vencimento      |
| LANC_DATA_PAG    | Data de Pagamento       |
| LANC_TIPO        | Tipo de Lançamento      |
| LANC_VALOR       | Valor                   |
| LANC_DATA_HORA_INCLUSAO | Data Inclusão    |
| COR_ID           | ID do Correntista       |
| CT_ID            | ID da Conta             |
| CC_ID            | ID do Centro de custo   |
| COR_NOME         | ID da Carteira          |
| CC_NOME          | ID da Carteira          |
| CAR_ID           | ID da Carteira          |
| CAR_NOME         | ID da Carteira          |
| Pago             | Pago?                   | Caracter  |                     | 3       | Não          |


Script da Views

```sql
    Select TB_LANCAMENTO.LANC_ID,
        TB_LANCAMENTO.LANC_DESCRICAO,
        TB_LANCAMENTO.LANC_DATA_VENC,
        TB_LANCAMENTO.LANC_DATA_PAG,
        TB_LANCAMENTO.LANC_TIPO,
        Case When TB_LANCAMENTO.LANC_PAGO = 0 Then 'Não'  Else 'Sim' End As PAGO,
        TB_LANCAMENTO.LANC_DATA_HORA_INCLUSAO,
        TB_CARTEIRA.CAR_ID,
        TB_CARTEIRA.CAR_NOME,
        TB_CORRENTISTA.COR_ID,
        TB_CORRENTISTA.COR_NOME,
        TB_CONTA.CT_ID,
        TB_CONTA.CT_NOME,
        Case When TB_LANCAMENTO.LANC_TIPO = 'Despesa' Then (TB_LANCAMENTO.LANC_VALOR * -1)  Else TB_LANCAMENTO.LANC_VALOR
        End As LANC_VALOR,
        TB_LANCAMENTO.CC_ID,
        TB_CENTRO_DE_CUSTO.CC_NOME
    From TB_LANCAMENTO
    Inner Join TB_CARTEIRA On TB_CARTEIRA.CAR_ID = TB_LANCAMENTO.CAR_ID
    Inner Join TB_CORRENTISTA On TB_CORRENTISTA.COR_ID = TB_LANCAMENTO.COR_ID
    Inner Join TB_CONTA On TB_CONTA.CT_ID = TB_LANCAMENTO.CT_ID
    Inner Join TB_CENTRO_DE_CUSTO On TB_LANCAMENTO.CC_ID = TB_CENTRO_DE_CUSTO.CC_ID

Union All

    Select TB_TRANSFERENCIA.TF_ID,
        TB_TRANSFERENCIA.TF_DESCRICAO,
        TB_TRANSFERENCIA.TF_DATA As LANC_DATA_VENC,
        TB_TRANSFERENCIA.TF_DATA As LANC_DATA_PAG,
        'Transferência' As TIPO,
        'Sim' As PAGO,
        TB_TRANSFERENCIA.TF_DATA_HORA_INCLUSAO,
        TB_TRANSFERENCIA.TF_CAR_DESTINO,
        TB_CARTEIRA.CAR_NOME,
        0 As COR_ID,
        'Transferência' As CORNOME,
        TB_CONTA.CT_ID,
        TB_CONTA.CT_NOME,
        TB_TRANSFERENCIA.TF_VALOR,
        0 As CC_ID,
        '' As CC_NOME
    From TB_TRANSFERENCIA
    Inner Join TB_CONTA On TB_CONTA.CT_ID = TB_TRANSFERENCIA.CT_ID
    Inner Join TB_CARTEIRA On TB_CARTEIRA.CAR_ID = TB_TRANSFERENCIA.TF_CAR_DESTINO

Union All

    Select TB_TRANSFERENCIA.TF_ID,
        TB_TRANSFERENCIA.TF_DESCRICAO,
        TB_TRANSFERENCIA.TF_DATA As LANC_DATA_VENC,
        TB_TRANSFERENCIA.TF_DATA As LANC_DATA_PAG,
        'Transferência' As TIPO,
        'Sim' As PAGO,
        TB_TRANSFERENCIA.TF_DATA_HORA_INCLUSAO,
        TB_TRANSFERENCIA.TF_CAR_ORIGEM,
        TB_CARTEIRA.CAR_NOME,
        0 As COR_ID,
        'Transferência' As CORNOME,
        TB_CONTA.CT_ID,
        TB_CONTA.CT_NOME,
        (TB_TRANSFERENCIA.TF_VALOR * -1),
        0 As CC_ID,
        '' As CC_NOME
    From TB_TRANSFERENCIA
    Left Join TB_CONTA On TB_CONTA.CT_ID = TB_TRANSFERENCIA.CT_ID
    Inner Join TB_CARTEIRA On TB_CARTEIRA.CAR_ID = TB_TRANSFERENCIA.TF_CAR_ORIGEM
```