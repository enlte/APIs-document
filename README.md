# APIs-document
        
# Blockchain Wallet API

The Base URL for all APIs: https://enlte.com/

1.	Creating a new Blockchain Wallet

Endpoint: /transaction_blockchain/createWallet
Query Parameters:

•	password - main wallet password (required). Must be 9 characters in length.

Response: 
```
{
  "guid": "05f290be-dbef-4636-a809-868893c51711",
  "address": "13R9dBgKwBP29JKo11zhfi74YuBsMxJ4qY",
  "status": "true"
}
```

2.	Make Payment

Endpoint: /transaction_blockchain/coinTransfer
Query Parameters:

•	signature- enlte signature to send coin (required). It contains the sender address.
•	raw_data – raw data in base64 format  (required). It contains the receiver address, amount, comment, transaction fee (%).
Response:
```
{
  "to" : "elt9c74owm3ndqyogjknwnhzmq1mju4njqzn7ad7",
  "from": "elt2c08mmmwogrkmmy5oweyotblzjczmjk1y55e2",
  "amount": 2000,
  "tx_fee": 10,
  "tx_hash": "f322d01ad784e5deeb25464a5781c3b20971c1863679ca506e702e3e33c18e9c",
  "status": true
}
```

3.	Get Wallet Balance

Endpoint: /transaction_blockchain/getUserBalance

Query Parameters:

•	address - user wallet address (required)
Response:
```
{"status":"true","Balance":1000.87192847,"other_balance":"100.05305823433"}
```

Here other balance is coin earn from mining.

# Blockchain Data API

1.	Single Block

Endpoint: /transaction_blockchain/single_block

Query Parameters:

•	block_id – block id of process transactions (required)
•	trans_index – transaction index to load next page transactions (optional)
•	loading_type – it is required to load next & previous page. (optional) e.g. next/prev/first/last
Note: To load next page, APIs required the index of last transaction from list. And to load previous page, APIs required the index of first transaction from list.
Response: 

 ```
 {
    "total_tx": "30",
    "curr_hash": "00b341a6d24a02ff85d9910f1f45c48e17668040e042b39e99abbb76c4f1749f",
    "prev_hash": "004e9f8d5217c801c8480fcfb243a01ac825ef06285a8cd13b8c22f3f05462b7",
    "total_amt": "989783.9487004",
    "processed_time": "2018-09-26 10:39:57",
    "txs": [ -- transaction list--]
}
```


2.	Single Transaction


Endpoint: /transaction_blockchain/transaction_detail 

Query Parameters:

•	t_id – transaction id (required)

Response:
```
{
    "data": [
        {
            "id": "68",
            "transaction_id": "3bfd5929c6d5a7562663c7d9ce23525b34707f9d97b77284d74e6a57a5ffb1aa",
            "from_address": "elt01famdfmywuymtixnjgzyzm3ytllowe1o6b23",
            "to_address": "elt9c74owm3ndqyogjknwnhzmq1mju4njqzn7ad7",
            "app_wallet_id": "0",
            "comment": "transfer from old wallet",
            "amount": "9964.89440389",
            "block_id": "3",
            "previous_hash": "66a6f37d17e94db4dd9c65651521b60c1af2dc3c9eab02aad5805f0493f3be97",
            "current_hash": "47bcc6a294f38875bfbbdaf5813dcce7650128d4c24caf73f59bfbb3f4078c1f",
            "utc_date_time": "2018-09-26 10:39:57",
            "tx_fee": "1",
            "status": "1"
        }
    ],
    "status": true
}
```

3.	Transaction list

Endpoint: /transaction_blockchain/transactions_list 

Query Parameters:

•	wallet_id – public address of user (optional)
•	trans_index – transaction index to load next page transactions (optional)
•	loading_type – it is required to load next & previous page. (optional) e.g. next/prev/first/last

Note: 
1.	To load next page, APIs required the index of last transaction from list. And to load previous page, APIs required the index of first transaction from list.
2.	If wallet id is empty, then it will return recently transactions.

Response:
```
{"total_count":"45","txs":[  -- transaction list-- ],"status":"true" }
```


# Mining Data API
1.	Miners

Endpoint: /transaction_blockchain/miners 

Query Parameters: No parameters required

Response:
```
{
    "status_code": 200,
    "status": "true",
    "data": {
        "total_users": 13,
        "active_user": 3,
        "inactive_user": 10
    }
}
```


1.	Pending transactions


Endpoint: /transaction_blockchain/broadcast_unprocessed_hash

Query Parameters: 

•	index – this input is required to load next page transaction (optional) 
Response:
```
{
    "status": "true",
    "data": [ --transaction list-- ]
}
```


2.	Validate transactions


Endpoint: /transaction_blockchain/vote_transactions

Query Parameters: 

•	tx_ids – it is a list of transaction ids for validating (required) 
•	tx_indexes – it is a list of transaction indexes for validating (required) 
•	voter_id – this input is required to load next page transaction (required) 
•	amounts – amount of each transaction (required) 
•	block_hash – It is proof of work created by miner & will consider as block current hash (required) 
•	block_raw – it is raw input of block_hash (required) 

Response:

```
{"status": "true"}
```
