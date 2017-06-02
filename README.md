
# 悟空数据API文档 

## 一、认证&授权

1. 获取授权码
2. 利用授权码和AppId、AppSecret获取access_token
3. 刷新access_token

### 1.1获取授权码（code）

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/code

请求参数说明

|参数         |说明                           |
|:----        |:----                          |
|app_id       |悟空数据分配给合作伙伴的AppId   |
|redirect_uri |接收Code返回的地址             |

### 1.2利用授权码和AppId、AppSecret获取access_token

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|:----        |:----                         |
|app_id       |悟空数据分配给合作伙伴的AppId   |
|app_secret   |应用的Secret                  |
|grant_type   |值为 authorization_code       |
|code         |在上一步获得的code             |

返回结果示例

``` json
{
    "access_token":"b1d7a9d145c9f251150709d9a879369b82cec96096d4281b7c95cd7e74623496",
    "expires_in":"7200",
    "refresh_token":"f8a0a8b55afe7d85d1c59665330dfb9df0adc8838f4bdedde4ec2cfad0515589",
    "created_at":1490086229
}
```

### 1.3刷新access_token

access_token的有效期为2小时，过去后可用刷新令牌（refresh_token）获得新的access_token.
获取access_token的API受调用次数的限制，调用方需对access_token自行进行缓存。

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|:----        |:----                         |
|app_id       |悟空数据分配给合作伙伴的AppId   |
|grant_type   |值为 refresh_token            |
|app_secret   |应用的Secret                  |
|refresh_token|刷新令牌                      |

返回结果示例

``` json
{
    "access_token":"042a6dc2ecc188ff78a3ab37abe8a67e96b9bff013acedfb1d140579e2fbeb63",
    "expires_in":"7200",
    "refresh_token":"df3501a700c4c93bc2deac76fc396fcc9fd81843ad7f202f26c1a174c7357585",
    "created_at":1490251072
}

```


## 二、数据API

1. 获取潜客列表
2. 获取潜客信息
3. 加入悟空潜客

### 2.1获取潜客列表

获取合作账号下绑定的悟空用户的潜客列表，目前的绑定规则是，在悟空后台手动关联。

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/lists

请求参数说明

|参数             |说明                           |
|:----            |:----                         |
|access_token     |调用接口凭证                   |
|wk_uid           |可选，默认是绑定的全部悟空用户,多个wk_uid用','分割|
|create_at        |可选，按指定日期查询，如2017-1-1 |
|create_at_start  |可选，查询2017-1-1 之后的数据    |
|create_at_end    |可选，查询2017-1-1 之前的数据    |

返回结果示例

``` json
[
    {
        "id":"1",
        "title":"测试列表_A",
        "uid":"1",
        "create_time":"1489725391"
    },
    {
        "id":"88",
        "title":"测试列表_B",
        "uid":"1",
        "create_time":"1489145960"
    }
]

```

### 2.2获取潜客信息

获取合作账号下绑定的悟空用户的潜客信息.

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/potential

请求参数说明

|参数             |说明                           |
|:----            |:----                         |
|access_token     |调用接口凭证                   |
|list_id          |可选，默认是全部列表,多个list_id用','分割|
|create_at        |可选，按指定日期查询，如2017-1-1 |
|create_at_start  |可选，查询2017-1-1 之后的数据    |
|create_at_end    |可选，查询2017-1-1 之前的数据    |

返回结果示例

``` json
[
    {
        "c_id":"100",
        "name":",张三A,张三B,张_三,张三,test,",
        "mobile":"0",
        "email":",123456@qq.com,1234567@QQ.com,"
    },
    {
        "c_id":"101",
        "name":"0",
        "mobile":",13212344321,",
        "email":"0"
    }
]
```

### 2.3加入悟空潜客

提交一条潜客信息到悟空的企业账号对应的用户账户中.
目前支持导入的字段是 姓名、手机号、邮箱、微信、QQ

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/import

请求参数说明

|参数         |说明                           |
|:----        |:----                         |
|access_token |调用接口凭证                   |
|wk_uid       |指定导入目标的一个悟空用户      |
|name         |姓名                          |
|mobile       |手机                          |
|email        |邮箱                          |
|wechat       |微信                          |
|qq           |qq                            |


返回结果示例

``` json

{
    "errcode":"100",
    "errmsg":"success",
}
```


批量导入：

``` json

    {
        "access_token":"access_token",
        "wk_uid":"123",
        "data":[
            {
                "name":"张三",
                "mobile":"13212341234",
                "email":"zhang@163.com",
                "wechat":"wechat_id",
                "qq":"qq123456"
            },
            {
                "name":"李四",
                "mobile":"13212341234",
                "email":"li@163.com",
                "wechat":"wechat_id",
                "qq":"qq123456"
            }
        ]
    }
```































