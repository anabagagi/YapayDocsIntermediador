# Tabela de Campos

Para a integração via <span class="post">POST</span>, segue abaixo os dados necessários para envio:

| Dados de Entrada                         |  Obrig.  | Formato / Tam. Max   | Descrição                                                  |
|------------------------------------------|----------|----------------------|------------------------------------------------------------|
| token_account                            |   Sim    |  Texto /20           |  Token de identificação do vendedor                      |
| customer[name]                           |   Sim    |  Texto /100          |  Nome do Comprador                                       |
| customer[cpf]                            |   Sim    |  Texto /14           |  CPF do Comprador                                        |
| customer[email]                          |   Sim    |  Texto /100          |  E-mail do Comprador                                     |
| customer[trade_name]                     |   Não    |  Texto /100          |  Nome Fantasia do Comprador                              |
| customer[company_name]                   |   Não    |  Texto /100          |  Razão Social do Comprador                               |
| customer[cnpj]                           |   Não    |  Texto /18           |  CNPJ do Comprador                                       |
| customer[inscricao_municipal]            |   Não    |  Texto /20           |  Inscrição Municipal do Comprador                        |
| customer[contacts][][type_contact]       |   Sim    |  Texto /1            |  Tipo do Contato <sup>1</sup> (Tabela 1)                 |
| customer[contacts][][number_contact]     |   Sim    |  Texto /11           |  Número do telefone do Comprador                         |
| customer[addresses][][type_address]      |   Sim    |  Texto /1            |  Tipo do Endereço <sup>1</sup> (Tabela 2)                |
| customer[addresses][][postal_code]       |   Sim    |  Texto /8            |  CEP do endereço do Comprador                            |
| customer[addresses][][street]            |   Sim    |  Texto /120          |  Nome da rua do Comprador                                |
| customer[addresses][][number]            |   Sim    |  Texto /10           |  Número do endereço do Comprador                         |
| customer[addresses][][neighborhood]      |   Sim    |  Texto /100          |  Bairro do endereço do Comprador                         |
| customer[addresses][][completion]        |   Não    |  Texto /100          |  Complemento do endereço do Comprador                    |
| customer[addresses][][city]              |   Sim    |  Texto /120          |  Cidade do endereço do Comprador                         |
| customer[addresses][][state]             |   Sim    |  Texto /2            |  Estado do endereço do Comprador                         |
| customer[birth_date]                     |   Não    |  Data / 10           |  Data de aniversário do Comprador                        |
| transaction[available_payment_methods]   |   Não    |  Texto /20           |  Meios de Pagamento disponíveis <sup>2</sup> (Tabela 3)  |
| transaction[order_number]                |   Não    |  Texto /2            |  Número do pedido                                        |
| transaction[customer_ip]                 |   Sim    |  Texto /15           |  IP do Comprador                                         |
| transaction[shipping_type]               |   Não    |  Texto /100          |  Tipo do envio                                           |
| transaction[shipping_price]              |   Não    |  Decimal / 11        |  Preço de Envio. Formato: 0.00                           |
| transaction[price_discount]              |   Não    |  Decimal / 11        |  Valor do desconto. Formato: 0.00                        |
| transaction[price_additional]            |   Não    |  Decimal / 11        |  Valor adicional. Formato: 0.00                          | 
| transaction[url_notification]            |   Não    |  Texto /255          |  URL de Notificação Automática de Status<sup>5</sup>     |
| transaction[free]                        |   Não    |  Texto /200          |  Campo Livre                                             |
| transaction[sub_store]                   |   Não    |  Texto /20           |  Sub-Loja                                                |
| transaction_product[][description]       |   Sim    |  Texto /100          |  Nome do produto <sup>1</sup>                            |
| transaction_product[][quantity]          |   Sim    |  Número / 3          |  Quantidade do item do produto                           |
| transaction_product[][price_unit]        |   Sim    |  Decimal / 11        |  Valor unitário. Formato: 0.00                           |
| transaction_product[][code]              |   Não    |  Texto /10           |  Código do produto                                       |
| transaction_product[][sku_code]          |   Não    |  Texto /50           |  Código SKU do produto                                   |
| transaction_product[][extra]             |   Não    |  Texto /100          |  Campo Livre do produto                                  |
| transaction[max_split_transaction]       |   Não    |  Número /10          |  Número máximo de parcelas                                  |
| payment[payment_method_id]               |   Sim    |  Texto /2            |  Forma de Pagamento                                      |
| payment[split]                           |   Sim    |  Texto /2            |  Número de parcelas (01 a 12)                            |
| payment[person_card_id]                  |   Não    |  Texto /100          |  Código do cartão cadastrado em nosso cofre <sup>3</sup> |
| payment[card_name]                       |   Não    |  Texto /100          |  Nome impresso no cartão                                 |
| payment[card_number]                     |   Não    |  Número /20          |  Número do cartão                                        |
| payment[card_expdate_month]              |   Não    |  Número /2           |  Mês de vencimento do cartão                             |
| payment[card_expdate_year]               |   Não    |  Número / 4          |  Ano de vencimento do cartão                             |
| payment[card_cvv]                        |   Não    |  Número /3           |  Código de segurança do cartão                           |
| payment[billet_date_expiration]          |   Não    |  Data / 10           |  Data de Vendimento do Boleto                            |
| affiliates[][account_email]              |   Não    |  Texto / 100         |  Email do afiliado da transação                          |
| affiliates[][percentage]                 |   Não    |  Número / 3          |  Percentual de repasse ao afiliado <sup>4</sup>          |
| affiliates[][commission_amount]          |   Não    |  Decimal / 11        |  Valor de repasse ao afiliado <sup>5</sup>               |
| reseller_token                           |   Não    |  Texto               |  Valor de repasse ao afiliado <sup>6</sup>               |
| finger_print                             |   Não    |  Texto /100          |  Token gerado pelo FingerPrint <sup>7</sup>              |


> <sup>1</sup> Note que nas informações acima que alguns dados possuem uma característica diferente, tendo um elemento [] dentro de sua formatação. Isso ocorre justamente para permitir que sejam enviados diversos itens na mesma requisição. 


> <sup>2</sup> O parâmetro `transaction[available_payment_methods]` permite que sejam enviados os códigos de meios de pagamento que poderão ser disponibilizados no processo de recobrança de transações. Os códigos deverão ser enviados separados por vírgula (,). Esse campo é útil quando a loja oferece uma condição especial de pagamento, por exemplo Desconto de 10% no Boleto Bancário. Assim deve-se enviar apenas o código do boleto bancário para que seja disponibilizada somente esta forma de pagamento no processo de recobrança.


> <sup>3</sup> O parâmetro `payment[person_card_id]` é informado com o código do cartão de crédito cadastrado em nossos cofres. Esse código é vinculado ao Vendedor e ao Cliente do Cartão de Crétido.


> <sup>4</sup> O parâmetro `affiliates[][]` é informado quando é necessário que seja feito Repasse Automático ao Revendedor. Essa opção é utilizada na Integração com Marketplace.


> <sup>5</sup> O parâmetro `transaction[url_notification]` é informado para comunicar a sua aplicação a cada alteração de status de uma transação. Saiba mais em Notificação Automática de Status.


> <sup>6</sup> O parâmetro `reseller_token` é informado para comunicar que a transação é vinculada a um revendedor. Dessa forma todas as transações que são enviadas com esse parâmetro ficam vinculadas ao revendedor.


> <sup>7</sup> O parâmetro `finger_print` é informado por um script Javascript que faz uma coleta de dados e realiza a analise das informações disponíveis publicamente na máquina. Dessa forma é realizada a Análise de Risco.