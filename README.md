# Diagon Alley: Decentralised Market-Stall Protocol
Diagon Alley is a decentralised market-stall protocol, that shifts emphasis on the frontend market to the merchants backend.

## Indexers
An indexer is a simple frontend middle-man that routes product, payment and shipping information between merchant and seller. Each merchant has products in a "stall" they allow an indexer to list.

## Stalls
A stall can choose to list some/all products with an "indexer". A stall is a small server that has three endpoints.

* /products/<indexer-ID> GET for fetching all products associated with an indexer ID
  
  ```Returns 201 CREATED (application/json)<br/>
  [{"categories":"cakes","description":"yummy cakes","id":"MF79QWYNGUO8XTwNXqBPmw==","image":"https://sddfvafbsd","price":20000,"product":"Welsh Cakes","quantity":20,"wallet":"93465fc1fd8f4c2c9f4bf32a3717d2fd"}]```


* /order/<indexer-ID> POST for placing an order and sending shipping data, returns a lightning-network invoice and checking(order) ID)

  Body (application/json)<br/>
  {"id": <string>, "address": <string>, "shippingzone": <integer>, "email": <string>, "quantity": <integer>}<br/>
  Returns 201 CREATED (application/json)<br/>
  {"checking_id": <string>,"payment_request": <string>}



