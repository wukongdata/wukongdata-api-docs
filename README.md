
# 悟空数据API文档 

## 一、认证&授权

1. 获取授权码
2. 利用授权码和AppId、AppSecrect获取access_token
3. 刷新access_token

### 1.1获取授权码（code）

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/code

请求参数说明

|参数         |说明                           |
|----         |----                          |
|appid        |悟空数据分配给合作伙伴的AppId   |
|redirect_uri |接收Code返回的地址             |

### 1.2利用授权码和AppId、AppSecrect获取access_token

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|----         |----                          |
|appid        |悟空数据分配给合作伙伴的AppId   |
|appsecret    |应用的Secret                  |
|code         |在上一步获得的code             |

~~返回结果示例~~

### 1.3刷新access_token

access_token的有效期为2小时，过去后可用刷新令牌（refresh_token）获得新的access_token.
获取access_token的API受调用次数的限制，调用方需对access_token自行进行缓存。

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|----         |----                          |
|appid        |悟空数据分配给合作伙伴的AppId   |
|appsecret    |应用的Secret                  |
|refresh_token|刷新令牌                      |

~~返回结果示例~~



## 二、数据API

1. 获取潜客列表
2. 获取潜客信息
3. 加入悟空潜客

### 2.1获取潜客列表

获取合作账号下绑定的悟空用户的潜客列表，目前的绑定规则是，在悟空后台手动关联。

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/list

请求参数说明

|参数             |说明                           |
|----             |----                          |
|access_token     |调用接口凭证                   |
|wk_uid           |可选，默认是绑定的全部悟空用户   |
|create_at        |可选，按指定日期查询，如2017-1-1 |
|create_at_start  |可选，查询2017-1-1 之后的数据    |
|create_at_end    |可选，查询2017-1-1 之前的数据    |

~~返回结果示例~~

### 2.2获取潜客信息

获取合作账号下绑定的悟空用户的潜客信息.

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/potential

请求参数说明

|参数             |说明                           |
|----             |----                          |
|access_token     |调用接口凭证                   |
|wk_uid           |可选，默认是绑定的全部悟空用户   |
|create_at        |可选，按指定日期查询，如2017-1-1 |
|create_at_start  |可选，查询2017-1-1 之后的数据    |
|create_at_end    |可选，查询2017-1-1 之前的数据    |

~~返回结果示例~~


### 2.3加入悟空潜客

提交一条潜客信息到悟空的企业账号对应的用户账户中.
目前支持导入的字段是 姓名、手机号、邮箱、微信、QQ

**接口调用请求说明**

> POST http://open.wukongdata.com/importv1/potential

请求参数说明

|参数         |说明                           |
|----         |----                          |
|access_token | 调用接口凭证                  |
|wk_uid       | 指定导入目标的悟空用户         |
|name         |姓名                          |
|mobile       |手机                          |
|email        |邮箱                          |
|wechat       |微信                          |
|qq           |qq                            |




~~返回结果示例~~


批量导入：

``` json

    {
        "access_token":"access_token",
        "wk_uid":"123",
        "data":[
            {
                "name":"\u674ebuli",
                "mobile":"13212341234",
                "email":"li@163.com",
                "wechat":"wechat_id",
                "qq":"qq123456"
            },
            {
                "name":"\u674ebuli",
                "mobile":"13212341234",
                "email":"li@163.com",
                "wechat":"wechat_id",
                "qq":"qq123456"
            }
        ]
    }
```































