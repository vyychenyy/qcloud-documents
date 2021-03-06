## 1. 接口描述

本接口（GetCertificates）用于查询用户的HTTPS证书信息，支持分页查询。

接口请求域名：<font style="color:red">cdn.api.qcloud.com</font>

1）接入的域名为海外CDN加速域名；

2) 单次最多查询100个证书信息。

[调用Demo](https://cloud.tencent.com/document/product/228/1734)

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://cloud.tencent.com/doc/api/231/4473)页面。其中，此接口的Action字段为GetCertificates。

| 参数名称      | 是否必选 | 类型     | 描述                                       |
| --------- | ---- | ------ | ---------------------------------------- |
| offset    | 是   | Int    | 分页查询偏移量地址                             |
| limit     | 是   | Int    | 指定查询的最大返回数量                   |

## 3. 输出参数

| 参数名称     | 类型     | 描述                                       |
| -------- | ------ | ---------------------------------------- |
| code     | Int    | 公共错误码，0表示成功，其他值表示失败。详见错误码页面的[公共错误码](https://cloud.tencent.com/doc/api/231/5078#1.-.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。 |
| message  | String | 模块错误信息描述，与接口相关                           |
| codeDesc | String | 英文错误信息，或业务侧错误码。                          |
| data     | Array  | 结果数据，详细说明见下文                             |

#### data字段说明
| 参数名称  | 类型   | 描述                                 |
| -------- | ------ | ----------------------------------- |
| total    | Int    | 返回的HTTPS证书总数|
| hosts    | Array  | HTTPS证书数组，详细说明见下面          |

#### hosts字段说明
| 参数名称     | 类型   | 描述                                 |
| ----------- | ------ | ----------------------------------- |
| host_id     | Int    | 域名ID|
| host        | String | 域名          |
| status      | String | 证书状态，包括：success, progress, fail, delete |
| message     | String | 备注信息 |
| cert_id     | String | 证书ID |
| common_name | String | 证书名称 |
| source      | Int    | 证书来源，0表示自有证书，1表示托管证书|
| hy          | String | 回源方式，http或是https|
| expire_time | String | 证书过期时间 |
| update_time | String | 证书更新时间 |

## 4. 示例

### 4.1 输入示例

> offset:0
> limit:10


### 4.2 GET 请求


GET 请求需要将所有参数都加在 URL 后：

```
https://cdn.api.qcloud.com/v2/index.php?
Action=GetCertificates
&SecretId=XXXXXXXXXXXXXXXXXXXXXXXXX
&Timestamp=1462440051
&Nonce=123456789
&Signature=XXXXXXXXXXXXXXXXXXXXXXXXXX
&offset=0
&limit=10
```

### 4.3 POST 请求
POST请求时，参数填充在HTTP Request-body 中，请求地址：

```
https://cdn.api.qcloud.com/v2/index.php
```

参数支持 form-data、x-www-form-urlencoded 等格式，参数数组如下：

```
array (
  'Action' => 'GetCertificates',
  'SecretId' => 'XXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  'Timestamp' => 1462868615,
  'Nonce' => 520585444,
  'Signature' => 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  'offset' => 0,
  "limit' => 10,
)
```

### 4.4 返回结果示例

```json
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "hosts": [
            {
                "host_id": 11111111,
                "host": "www.test.com",
                "status": "success",
                "message": "test",
                "cert_id": "abcdefg",
                "common_name": "www.test.com",
                "source": 1,
                "hy": "https",
                "expire_time": "2018-07-27 07:59:59",
                "update_time": "2017-07-26 17:44:57"
            }
        ],
        "total": 0
    }
}
```







