TB_LANCAMENTO ( Lançamento )

| Nome da Campo    | Título                  | Tipo      | Máscara             | Tamanho | Permite Nulo |
| --------------   | ----------------------  | --------- | ------------------- | ------- | ------------ |
| LANC_ID          | ID de Lançamento        | Numérico  |                     | 10      | Não          |
| LANC_DESCRICAO   | Descrição do Lançamento | Caracter  |                     | 150     | Não          |
| LANC_DATA_VENC   | Data de Vencimento      | Data      | dd/MM/yy            | 8       | Não          |
| LANC_TIPO        | Tipo de Lançamento      | Caracter  |                     | 50      | Não          |
| LANC_VALOR       | Valor                   | Numérico  | 99.999.999,99       | 10      | Não          |
| LANC_VALOR_EFETIVO | Valor efetivo         | Numérico  | 99.999.999,99       | 10      | Não          |
| LANC_PAGO        | Pago?                   | Lógico    |                     | 10      | Não          |
| LANC_DATA_HORA_INCLUSAO | Data Inclusão    | Data/Hora | dd/MM/yyyy HH:mm:ss | 19      | Sim          |
| COR_ID           | ID do Correntista       | Numérico  |                     | 10      | Sim          |
| CT_ID            | ID da Conta             | Numérico  |                     | 10      | Não          |
| CAR_ID           | ID da Carteira          | Numérico  |                     | 10      | Não          |
| CC_ID            | ID do Centro de custo   | Numérico  |                     | 10      | Não          |
| LANC_DATA_PAG    | Data de Pagamento       | Data      | dd/MM/yy            | 8       | Sim          |
| LANC_CONTROLE    | Controle de lançamentos | Caracter  |                     | 40      | Sim          |
