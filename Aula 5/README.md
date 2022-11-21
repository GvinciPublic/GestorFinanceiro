TB_TRANSFERENCIA ( Transferência )

| Nome da Campo  | Título                 | Tipo      | Máscara             | Tamanho | Permite Nulo |
| -------------- | ---------------------- | --------- | ------------------- | ------- | ------------ |
| TF_ID          | ID da Transferência    | Numérico  |                     | 10      | Não          |
| TF_DESCRICAO   | Descrição da Transf.   | Caracter  |                     | 150     | Não          |
| TF_DATA        | Data                   | Data      | dd/MM/yy            | 8       | Não          |
| TF_CAR_ORIGEM  | Carteira de Origem     | Numérico  |                     | 10      | Não          |
| TF_CAR_DESTINO | Carteira de Destino    | Numérico  |                     | 10      | Não          |
| TF_VALOR       | Valor                  | Numérico  | 99.999.999,99       | 10      | Não          |
| TF_DATA_HORA_INCLUSAO | Data Inclusão   | Data/Hora | dd/MM/yyyy HH:mm:ss | 100     | Sim          |
| CT_ID          | ID da Conta            | Numérico  |                     | 100     | Não          |
| TF_CC_ORIGEM   | Centro de custo de origem  | Numérico  |                     | 100     | Não          |
| TF_CC_DESTINO  | Centro de custo de destino | Numérico  |                     | 100     | Não          |

TB_CONFIGURACOES ( Configurações ) tipo Parâmetros

| Nome da Campo               | Título                           | Tipo      | Tamanho | Permite Nulo |
| --------------              | ----------------------           | --------- | ------- | ------------ |
| CONFIG_ID                   | Id config                        | Numérico  | 10      | Não          |
| CONFIG_CONTA_TRANSF_PADRAO  | Conta padrão para transferências | Numérico  | 10      | Não          |
| CONFIG_CARTEIRA_PADRAO      | Carteira padrão                  | Numérico  | 10      | Sim          |
