# Service Keys
Service keys被用来接口调用。Service keys有全部的权限来操作Shipyard接口。

#例子
## 创建Service key
```
shipyard cli> shipyard add-service-key -d "test key"
created key: Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry
```
## 查看Service key列表
```
shipyard cli> shipyard service-keys
Key                                     Description
Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry    test key
```
## 使用Service key
```
curl -s -H 'X-Service-Key: Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry' http://localhost:8080/api/engines
[
    {
        "engine": {
            "labels": [
                "local",
                "dev"
            ],
            "memory": 2048,
            "cpus": 4,
            "addr": "http://10.1.2.3:2375",
            "id": "local"
        },
        "id": "a08b8518-e963-4eb5-959a-566bd270cd28"
    }
]
```
## 删除Service key
```
shipyard cli> shipyard remove-service-key Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry
removed Z2uwezQGoaIcfiRSQBRbktrzdbFRWKlVTEry
```
