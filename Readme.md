Token Contract
-----------------

#### Prerequisites


* Endpoint network:

https://api-kylin.eoslaomao.com:443

* Contract name:newtoken1234

{"active_key": {"public": "EOS8LZvcBaHRr2BkTuHF7VLu6RSYDiLXTdgC8Hfq2gy8NyvG21kif", "private": "5HsYvS2up39AEghpYWY86nMkZu6sCMjHi4xgRbRFo7dB6QadRdz"}, "owner_key": {"public": "EOS7f4gSRwwQdvnrJeQccmfe7S4YKaWrhTfpUEEnv5jwaGQ2sxggw", "private": "5Jkg1tQytHYyDiYTncT5yL7bjQs9LQnmtMACgGnkoZJDeSkH5Wk"}}, "account": "newtoken1234"}

{"msg": "succeeded", "keys": {"active_key": {"public": "EOS6SFr926qCPu2AAykpDs3XtbjaK8qTAGLYi5NCWcrXjnXEXRawg", "private": "5KNKCiY2VjM4pfLPpcrWD2tTHT75VsSeUZzhSAjyc1zBhMYJtnw"}, "owner_key": {"public": "EOS719Grp36iRKDm2A7s3cuAZvTdmtSUVwHpVVzknL5MQYjjgcQsn", "private": "5JyGegPVKpsjQiRRJJa8EDV6VRxwWdKJrVLav866qyrzuzktei6"}}, "account": "levietquoc12"}

{"msg": "succeeded", "keys": {"active_key": {"public": "EOS832jSQ8DvwY7Yz7m16UtrrKBTxoWE8y3ri2pzR7ams7wB7VQ8j", "private": "5JCKatfbwtfgwcRqSQDXA2o9s3P4KkVY1motXgwWUVFZ3cwz85t"}, "owner_key": {"public": "EOS7NZJKEiA76CpiLxqV3tfAx7n4jmc7z9TxL6uXy6QxpwMxDoruw", "private": "5KLzAJ97EvtuJ4tPnP5hnvddyMcEYPbd84uYUVFAvJeekL8BGd9"}}, "account": "tester123444"}

##### Set contract to newtoken1234 account
````bash
eosio-cpp -I include -o eosio.token.wasm eosio.token.cpp --abigen
$ cleos -u https://api-kylin.eoslaomao.com:443 set contract newtoken1234 ./eosio.token/ -p newtoken1234
````

##### create tokens

````bash
$ cleos -u https://api-kylin.eoslaomao.com:443 push action newtoken1234 create '[newtoken1234, "100000000.0000 TOKEN"]' -p newtoken1234

$ cleos -u https://api-kylin.eoslaomao.com:443 get table newtoken1234 TOKEN stat
{
  "rows": [{
      "supply": "0.0000 TOKEN",
      "max_supply": "100000000.0000 TOKEN",
      "issuer": "newtoken1234"
    }
  ],
  "more": false
}
````


##### issue token 
````bash


$ cleos -u https://api-kylin.eoslaomao.com:443 push action newtoken1234 issue '[tester123444, "12345.0000 TOKEN", "first transfer"]' -p newtoken1234

cleos -u https://api-kylin.eoslaomao.com:443 get table newtoken1234 tester123444 accounts
{
  "rows": [{
      "balance": "12345.0000 TOKEN",
      "staking": "0.0000 TOKEN",
      "frozen": "0.0000 TOKEN"
    }
  ],
  "more": false
}
$ cleos -u https://api-kylin.eoslaomao.com:443 push action newtoken1234 transfer '[tester123444, levietquoc12, "100.0000 TOKEN", "first transfer"]' -p tester123444

$ cleos -u https://api-kylin.eoslaomao.com:443 get table newtoken1234 levietquoc12 accounts
{
  "rows": [{
      "balance": "100.0000 TOKEN",
      "staking": "0.0000 TOKEN",
      "frozen": "100.0000 TOKEN"
    }
  ],
  "more": false
}

$ cleos -u https://api-kylin.eoslaomao.com:443 push action newtoken1234 stake '[tester123444, "15.0000 TOKEN"]' -p tester123444

$ cleos -u https://api-kylin.eoslaomao.com:443 get table newtoken1234 tester123444 accounts
{
  "rows": [{
      "balance": "12245.0000 TOKEN",
      "staking": "15.0000 TOKEN",
      "frozen": "0.0000 TOKEN"
    }
  ],
  "more": false
}

$ cleos -u https://api-kylin.eoslaomao.com:443 push action newtoken1234 unstake '[tester123444, "5.0000 TOKEN"]' -p tester123444

$ cleos -u https://api-kylin.eoslaomao.com:443 get table newtoken1234 tester123444 accounts
{
  "rows": [{
      "balance": "12245.0000 TOKEN",
      "staking": "10.0000 TOKEN",
      "frozen": "0.0000 TOKEN"
    }
  ],
  "more": false
}

````