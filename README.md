 <br/>
<p align="center">
  <img src="https://i.imgur.com/SuoAxtp.png" width="60%">
</p>


# Diagon Alley: Decentralised Market-Stall Protocol
Diagon Alley is a decentralised market-stall protocol, that shifts emphasis from the frontend market to the merchants stall. If a frontend market (indexer) gets taken down, merchants just point their stalls elsewhere. Game-theoretically the winner of Diagon Alley is the most forthright, although suggestions on limiting bad behaviour are very welcome.

## Indexers
An indexer is a simple frontend server and GUI that routes product, payment and shipping information between merchant and buyer. Each merchant has products in a *stall*. The stall chooses what products to list with the indexer. An indexer has one endpoint.  

* `/register/<indexer_ID>` **POST** The `<indexer_ID>` is generated by the stall. the endpoint is for stalls to fetch rating data (0-100%), register products and check the indexer is online. 

  Body (application/json)<br/>
  ```{"stall_url": <string>}```
  
  Returns 200 OK (application/json)<br/>
  ```{"shopstatus": <boolean>, "rating": <int>}```
  
The indexer uses the `<stall_url>` and `<indexer_ID>` for the stall endpoints.

## Stalls
A stall can choose to list some/all products with an *indexer*. A stall is a small server that has three endpoints.

* `/products/<indexer_ID>` **GET** for fetching all products associated with an indexer ID
  
  Returns 200 OK (application/json)<br/>
  ```[{"product_id":<string>, "product_name":<string>, "categories":<list>, "description":<string>,  "image":<string>, "price":<int>, "quantity":<int>}, {"product_id":<string>, "product_name":<string>, "categories":<list>, "description":<string>,  "image":<string>, "price":<int>, "quantity":<int>}]```


* `/order/<indexer_ID>` **POST** for placing an order and sending shipping data. Returns a lightning-network invoice and checking/order ID

  Body (application/json)<br/>
  ```{"product_id": <string>, "address": <string>, "shippingzone": <integer>, "email": <string>, "quantity": <integer>}```
  
  Returns 201 CREATED (application/json)<br/>
  ```{"payment_request": <string>, "checking_id": <string>}```
  
* `/checkshipped/<checking_id>` **GET** for checking if an order has been shipped

  Returns 200 OK (application/json)<br/>
  ```{"shipped": <boolean>}```





