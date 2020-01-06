# Nova API Document

## WatcherToken

Watchertoken can be obtained from the observer link generation.(`ACCOUNT SETTINGS`-`MINING GROUP`-`SETTING`-`SET OBSERVER LINK`)
Starting with the 'wow' character

## API

Note: Authentication requires passing the accessToken in the request header. 
The parameter name is: authorization, the value is Bearer TOKEN, and TOKEN is replaced with the token value to be transmitted.

### 1. Get workers stats info

**URL**

`GET https://novablock.com/api/v1/worker/stats`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|

**Results**

```json
{
    "err_no":0,
    "data":{
        "workers_active":143,
        "workers_inactive":0,
        "workers_dead":0,
        "shares_15m":36.623,
        "shares_1h":36.105,
        "workers_total":143,
        "shares_24h":36.143,
        "shares_unit":"P"
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|workers_active|number of active workers|
|workers_inactive|number of inactive workers|
|workers_dead|number of dead workers|
|workers_total|number of workers|
|shares_15m|15min hashrate|
|shares_1h|1h hashrate|
|shares_24h|24h hashrate|
|shares_unit|hashrate unit|

---

### 2. Get workers lists

**URL**

`GET https://novablock.com/api/v1/workers`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|
|pagesize|int|true|per page size|
|page|int|true|current page|
|status|string|true|Optional value:ALL,ACTIVE,INACTIVE,DEAD|


**Results**

```json
{
    "err_no":0,
    "data":{
        "page":1,
        "page_size":10,
        "page_count":15,
        "total_count":143,
        "data":[
            {
                "region_id":"sv",
                "worker_id":"6617213270852685986",
                "worker_name":"1-1",
                "shares_15m":295.236,
                "shares_24h":299.823,
                "reject_rate":0,
                "accept_count":356558,
                "active_duration_sec":5219373,
                "session_first_share_time":1573076516,
                "last_share_time":1578295889,
                "status":"ACTIVE",
                "shares_unit":"T"
            },
            ...
        ],
        "workers_active":143,
        "workers_inactive":0,
        "workers_dead":0
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|region_id|Region|
|worker_id|Mining machine id|
|worker_name|Mineral machine name|
|shares_15m|Real-time Hashrate|
|shares_24h|24h Hashrate|
|shares_unit|Hashrate unit|
|reject_rate|Reject rate|
|accept_count|Number of accept|
|last_share_time|Recent submission time|
|status|Status|

---

### 3. Get worker detail info

**URL**

`GET https://novablock.com/api/v1/worker/{worker_id}`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|

**Results**

```json
{
    "err_no":0,
    "data":{
        "worker_id":"8380394089686781802",
        "worker_name":"1-2",
        "shares_15m":325.26,
        "shares_24h":305.713,
        "shares_unit":"T",
        "miner_agent":"cgminer/4.10.0a9",
        "accept_count":355826,
        "reject_rate":0,
        "last_share_ip":"173.209.162.144",
        "last_share_lan_ip":0,
        "last_share_time":1578296763,
        "active_duration_sec":5317191,
        "session_first_share_time":1572979572,
        "worker_status":"ACTIVE"
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|worker_id|Mining machine id|
|worker_name|Mineral machine name|
|shares_15m|Real-time Hashrate|
|shares_24h|24h Hashrate|
|shares_unit|Hashrate unit|
|miner_agent|miner agent|
|accept_count|Number of accept|
|reject_rate|Reject Hashrate|
|last_share_ip|Last submitted ip|
|last_share_lan_ip|Last submitted to the internal network ip|
|last_share_time|Last submitted time|
|worker_status|status|

---

### 4. Get cloud hashrate machines

**URL**

`GET https://novablock.com/api/v1/worker/cloud`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|

**Results**

```json
{
    "err_no":0,
    "data":{
        "unit":"T",
        "data":[
            {
                "from_puid":351,
                "to_puid":354,
                "worker_name":"jmehr88",
                "worker_id":"1450213277007954",
                "reject_rate":0,
                "shares_unit":"T",
                "last_share_ip":0,
                "miner_agent":"fake_cgminer/4.10.0",
                "shares_15m":191.028,
                "last_share_time":1578297492,
                "shares_24h":188.576,
                "status":"ACTIVE"
            }
        ],
        "total_hashrate":191.028
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|from_puid|source of hashrate puid|
|to_puid|receiver of hashrate puid|
|worker_id|Mining machine id|
|worker_name|Mineral machine name|
|shares_15m|Real-time Hashrate|
|shares_24h|24h Hashrate|
|shares_unit|Hashrate unit|
|miner_agent|miner agent|
|reject_rate|Reject Hashrate|
|last_share_ip|Last submitted ip|
|last_share_time|Last submitted time|
|worker_status|status|

---

### 5. Get rewards stats

**URL**

`GET https://novablock.com/api/v1/payout/stats`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|

**Results**

```json
{
    "err_no":0,
    "data":{
        "total_paid_amount":"4349272893",
        "yesterday_amount":"65706492",
        "balance":0,
        "today_estimate":20420207,
        "last_payment_time":1578271450
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|total_paid_amount|Cumulative paid|
|yesterday_amount|Yesterday earnings|
|balance|Balance|
|today_estimate	|Today earnings(estimated)|
|last_payment_time|last payment time|

---

### 6. Get reward history

**URL**

`GET https://novablock.com/api/v1/payout/history`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin|
|pagesize|int|true|per page size|
|page|int|true|current page|

**Results**

```json
{
    "err_no":0,
    "data":{
        "current_page":1,
        "data":[
            {
                "date":20200105,
                "coin_type":"btc",
                "amount":65706492,
                "change":-0.0095,
                "share_accept":36.412,
                "share_unit":"P",
                "reject_rate":0.0009,
                "address":"1pm2S9aKV6ugD5mTLiJRHH1QYXKLMgZj3",
                "address_created_at":1573057700,
                "txhash":"a76d83edc2ce9a9bd644e195b2f3fb803c27517b383602d5f66b3d7fdc2ba48e",
                "unpaid_reason":null,
                "payment_status":"PAID",
                "paid_at":1578271450,
                "created_at":1578270605,
                "rate":null,
                "coinexchange":null,
                "bill_type":0
            },
            ...
        ],
        "first_page_url":"https://novablock.com/api/v1/payout/history?page=1",
        "from":1,
        "last_page":7,
        "last_page_url":"https://novablock.com/api/v1/payout/history?page=7",
        "next_page_url":"https://novablock.com/api/v1/payout/history?page=2",
        "path":"https://novablock.com/api/v1/payout/history",
        "per_page":10,
        "prev_page_url":null,
        "to":10,
        "total":62
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|date|-|
|coin_type|-|
|amount|Amount of income|
|change|Daily change|
|share_accept|Daily hashrate|
|share_unit|hashrate unit|
|reject_rate|Reject Rate|
|address|Payment address|
|txhash|Trading hash|
|unpaid_reason|Reasons for non-payment|
|payment_status|Payment status: ```PAID``` paid,```PENDING``` Paying,```DELAYED``` delay payment|
|paid_at|Payment time|

---

### 7. Get payout history

**URL**

`GET https://novablock.com/api/v1/payout/pay-records`

**Request parameter**

|Field|Type|Require|Remark|
|:---:|:---:|:---:|:---:|
|puid|int|true|mining group id|
|coin_type|string|true|coin,can be `all`|
|start_time|int|true|start date time|
|end_time|int|true|end date time|
|page_size|int|true|per page size|
|page|int|true|current page|

**Results**

```json
{
    "err_no":0,
    "data":{
        "current_page":1,
        "data":[
            {
                "coin_type":"btc",
                "txhash":"a76d83edc2ce9a9bd644e195b2f3fb803c27517b383602d5f66b3d7fdc2ba48e",
                "amount":"0.65706492",
                "address":"1pm2S9aKV6ugD5mTLiJRHH1QYXKLMgZj3",
                "pay_date":"20200106",
                "name":"horizon1"
            },
            ...
        ],
        "first_page_url":"/?page=1",
        "from":1,
        "last_page":1,
        "last_page_url":"/?page=1",
        "next_page_url":null,
        "path":"/",
        "per_page":10,
        "prev_page_url":null,
        "to":8,
        "total":8
    }
}
```

**Return field description**

|Return field|Description|
|:---:|:---:|
|coin_type|-|
|txhash|Trading hash|
|amount|Amount of income|
|address|Payment address|
|pay_date|pay date|
|name|mining group name|

---
