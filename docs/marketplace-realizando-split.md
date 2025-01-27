# Realizando split de pagamento

Para que o repasse ao revendedor seja automático, utilizamos a API de Transação na integração com Marketplace informando os campos affiliates[], esses campos quando são enviados são identificamos que é referente a transações Marketplace:

> **Observação: a conta do afiliado deve ser criada antes da criação da transação.**


| Dados de Entrada                      |  Obrig.  | Formato / Tam. Max   | Descrição                             |
|---------------------------------------|----------|----------------------|---------------------------------------|
|   affiliates[][email]                 |   Não    | Texto / 100          | Email do afiliado da transação        |
|   affiliates[][percentage]            |   Não    | Número / 3           | Percentual de repasse ao afiliado     |
|   affiliates[][commission_amount]     |   Não    | Decimal / 11         | Valor de repasse ao afiliado          |
|   affiliates[][type_affiliate]        |   Não    | Texto / 100          | Tipo do afiliado                      |
|   affiliates[][url_notification]      |   Não    | Texto / 100          | URL de Notificação do Afiliado        |




> O afiliado precisa ter conta cadastrada na Yapay, senão a transação será **recusada**!



# Código de Exemplo

Abaixo você consegue visualizar um exemplo em JSON da criação passando R$ 22,00 (valor fixo) para o afiliado `emaildoafiliado@afiliado.com`:


> **Exemplo em JSON**

```javascript
    {  
        "token_account":"SEU_TOKEN_AQUI",
        "customer":{  
            "contacts":[  
                {  
                    "type_contact":"H",
                    "number_contact":"1133221122"
                },{  
                    "type_contact":"M",
                    "number_contact":"11999999999"
                }         
            ],
            "addresses":[  
                {  
                    "type_address":"B",
                    "postal_code":"17000-000",
                    "street":"Av Themyscira",
                    "number":"1001",
                    "completion":"A",
                    "neighborhood":"Jd das Rochas",
                    "city":"Themyscira",
                    "state":"SP"
                }
            ],
            "name":"Diana Prince",
            "birth_date": "21/05/1941",
            "cpf":"50235335142",
            "email":"email@cliente.com.br"
        },
        "transaction_product":[  
            {  
                "description":"Camiseta Wonder Woman",
                "quantity":"1",
                "price_unit":"13000.00",
                "code": "1",
                "sku_code": "0001",
                "extra": "Informação Extra"
            }
        ],
        "transaction":{  
            "available_payment_methods": "2,3,4,5,6,7,14,15,16,18,19,21,22,23,27",
            "customer_ip":"127.0.0.1",
            "shipping_type":"Sedex",
            "shipping_price":"0",
            "price_discount": "",
            "url_notification":"http://www.loja.com.br/notificacao",
            "free": "Campo Livre"      
            
        },

        "affiliates":[  
             {  
                 "email":"emaildoafiliado@afiliado.com",
                 "commission_amount":"22",
                 "url_notification": "http://www.lojadoafiliado.com.br/notificacao" 
             }
         ],
         "payment":{  
            "payment_method_id":"3",
            "card_name": "DIANA PRINCE",
            "card_number": "4111111111111111",
            "card_expdate_month": "01",
            "card_expdate_year": "2029",
            "card_cvv": "644",
            "split": "1"
         }
    }

```



# URL de Notificação do Afiliado

Sempre que for adicionado no nó `affiliates` o parâmetro `url_notification` será enviado para a URL do afiliado as alterações dessa transação, junto com os valores de recebimento. **É enviado em parâmetros em form/post**.


Abaixo o exemplo do que é enviado para essa URL de Notificação, e é baseado no exemplo acima, sendo assim o valor da comissão do afiliado é R$ 22,00 (valor fixo):


```html
    transaction_token=68d9aaf5ej7bc02935e51f47f0385416&status_name=Aprovada&payment_method=Boleto%20Bancario&qtd=22.0&price=13000.0
```

Detalhamento de cada campo enviado:

| Campo              |  Descrição                                           |  
|--------------------|------------------------------------------------------|
|  transaction_token | Token da Transação                                   |
|  status_name       | Nome do Status da Transação                          |
|  payment_method    | Forma de Pagamento                                   |
|  qtd               | Valor da comissão que será repassada para o afiliado |
|  price             | Valor total da transação                             |





# Mensagens de Erros

No caso de erro, a API retorna uma mensagem de erro. Assim é possível identificar o erro ocorrido e realizar o tratamento através do código e/ou mensagem retornada.

Abaixo segue os detalhes de cada nó do JSON de resposta:


```javascript
{
    "message_response": {
        "message": "error"
    },
    "error_response": {
        "general_errors": [
            {
                "code": "037022",
                "message": "Afiliado não possui conta. Email: email_informado"
            }
        ]
    }
}
```


As mensagens de erros retornados relacionados a AFILIADOS que são retornados pela API:

| Código    |  Mensagem                                        | Solução                                               |
|-----------|--------------------------------------------------|-------------------------------------------------------|
|  037010   |     E-mail do afiliado informado deve ser diferente do vendedor                         | O email enviado como cliente não pode ser o mesmo que o e-mail do vendedor (token_account) |
|  037021   |     É necessário informar uma comissão ou um percentual para o afiliado.                         | O valor enviado no campo de comissão está vazio |
|  037022   |     Afiliado não possui conta. Email: email_informado                         | O e-mail enviado no parâmetro `affiliates[account_email]` não tem cadastro na Yapay. TODAS as contas de afiliados devem ter conta cadastrada. |
| 22 | Comissão não é um número | O valor enviado no campo de comissão não é um número |

