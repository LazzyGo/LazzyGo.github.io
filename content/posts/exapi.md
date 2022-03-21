---
title: "交易所api"
date: 2022-03-21T09:13:05Z
tags: ["api"]
---
### bybit
```python
import requests
import json

r=requests.get("https://api-testnet.bybit.com/public/linear/kline?symbol=BTCUSDT&interval=1&limit=2&from=1581231260")
print(json.dumps(json.loads(r.text)['result'],indent=4,sort_keys=True))

kline="https://api-testnet.bybit.com/public/linear/kline"
params={
        'symbol':'BTCUSDT',
        'interval':1,
        'limit':2,
        'from':1581231260
        }
r1=requests.get(kline,params=params)
data=json.loads(r1.text)
data=json.dumps(data['result'],indent=4,sort_keys=True)
print(data)
```

### binance

docs: https://binance-docs.github.io/apidocs/futures/en

```python
import json,requests

def test(url,paramas):
    r=requests.get(url,params=params).text
    data=json.dumps(json.loads(r),indent=4,sort_keys=True)
    print(data)
    return data

url="https://fapi.binance.com/fapi/v1/time"
params={}

r=test(url,params)

#r=requests.get("https://fapi.binance.com/fapi/v1/time")
#print(r.text)
```

### okx

docs: https://www.okex.com/docs/zh

好像不可用
```python
import requests,json

path="/api/swap/v3/instruments/BTC-USD-SWAP/index"
url="https://okx.com"+path
r=requests.get(url).text
data=json.dumps(json.loads(r),indent=4,sort_keys=True)
print(data)
```

### gate

docs: https://www.gate.ac/cn/api2

futures: https://github.com/gateio/gateapi-python

### CoinEx

docs: https://viabtc.github.io/coinex_api_cn_doc/futures/#docsfutures001_http031_market_close

### mexc

docs: https://mxcdevelop.github.io/APIDoc/open.api.v2.cn.html
