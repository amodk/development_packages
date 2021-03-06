## extract data from your Mollie account API
  
**pip install mollie_api_extract** 
  
**Authentication:** You need to pass API key in each function call. No pre-authorization is needed. You may want to store API Key in an environmental variable to avoid displaying it in each function call. In the current version 1.0.1, there are three functions:

#### mollie_payments

*from mollie_api_extract import mollie_payments*  
*payments_data = mollie_payments('access_token','account_name')* 

This function will fetch all data from payments endpoint. access_token is a compulsory field and account_name is optional e.g. **mollie_payments('xxxxyyyyy','My Company GmbH')** or just **mollie_payments('xxxxyyyyy')**. Each API call will fetch 250 rows(max limit) until full extract is complete. As the full extract can run for long duration, after each API call it will print *going to next API requests for 250 rows..* so that the end user can see the progress.  

The output will be a dataframe with following fields:  

['mollie_account', 'profileId', 'resource', 'id', 'mode', 'createdAt',
       'status', 'amount_value', 'amount_currency', 'method', 'locale',
       'sequenceType', 'description', 'details', 'is_cancellable',
       'authorized_at', 'paid_at', 'expires_at', 'expired_at', 'failed_at',
       'amount_refunded', 'amount_refund_currency', 'amount_remaining',
       'amount_remaining_currency', 'amount_captured',
       'amount_captured_currency', 'metadata', 'metadata_order_id',
       'metadata_refund_token', 'metadata_customer_id',
       'restricted_to_country', 'country_code', 'settlement_id', 'customer_id',
       'mandate_id', 'subscription_id', 'order_id',
       'application_fee_amount_value', 'application_fee_amount_currency',
       'application_fee_description', 'settlement_amount',
       'settlement_amount_currency', 'links', 'redirectUrl', 'webhook_url']
       
#### mollie_refunds

*from mollie_api_extract import mollie_refunds*  
*refunds_data = mollie_refunds('access_token','account_name')* 

This function will fetch all data from refunds endpoint. access_token is a compulsory field and account_name is optional e.g. **mollie_refunds('xxxxyyyyy','My Company GmbH')** or just **mollie_refunds('xxxxyyyyy')**. Each API call will fetch 250 rows until full extract is complete.

The output will be a dataframe with following fields:  

['resource', 'id', 'amount', 'status', 'createdAt', 'description',
       'metadata', 'paymentId', 'settlementId', 'settlementAmount', '_links',
       'mollie_account', 'amount_value', 'amount_currency']
       
#### mollie_refund

*from mollie_api_extract import mollie_refund*  
*refunds_data = mollie_refund('payment_id','refund_id','access_token')* 


This function will fetch exactly one refund for which the payment_id and refund_id is given. All three parameters need to be passed. e.g.  **mollie_refund('paymentxxx','refundyyy','tokenzzz')**  

The output will be a dataframe with following fields:

['resource', 'id', 'amount', 'status', 'createdAt', 'description',
       'metadata', 'paymentId', 'settlementId', 'settlementAmount', '_links']


