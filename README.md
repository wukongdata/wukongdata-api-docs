
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
|----         |:----:                        |
|appid        | 悟空数据分配给合作伙伴的AppId  |
|redirect_uri | 接收Code返回的地址            |

### 1.2利用授权码和AppId、AppSecrect获取access_token

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|----         |:----:                        |
|appid        | 悟空数据分配给合作伙伴的AppId  |
|appsecret    | 应用的Secret                 |
|code         | 在上一步获得的code            |

~~返回结果示例~~

### 1.3刷新access_token

access_token的有效期为2小时，过去后可用刷新令牌（refresh_token）获得新的access_token.
获取access_token的API受调用次数的限制，调用方需对access_token自行进行缓存。

**接口调用请求说明**

> POST http://open.wukongdata.com/oauth/token

请求参数说明

|参数         |说明                           |
|----         |:----:                        |
|appid        | 悟空数据分配给合作伙伴的AppId  |
|appsecret    | 应用的Secret                 |
|refresh_token| 刷新令牌                     |

~~返回结果示例~~



## 二、数据API

1. 获取潜客列表
2. 获取悟空潜客
3. 加入悟空潜客

### 2.1获取潜客列表

获取合作账号绑定悟空的企业账号下的全部潜客列表，悟空的企业账号是指在悟空平台注册的公司账号。
目前的绑定规则是，在悟空后台手动关联。

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/list

请求参数说明

|参数         |说明                           |
|----         |:----:                        |
|access_token | 调用接口凭证                  |
|company_id   | 可选，默认是全部              |

~~返回结果示例~~

### 2.2获取潜客列表

获取合作账号绑定悟空的企业账号下的全部潜客.

**接口调用请求说明**

> POST http://open.wukongdata.com/openv1/potential

请求参数说明

|参数         |说明                           |
|----         |:----:                        |
|access_token | 调用接口凭证                  |
|company_id   | 可选，默认是全部              |

~~返回结果示例~~


### 2.3加入悟空潜客

获取合作账号绑定悟空的企业账号下的全部潜客.

**接口调用请求说明**

> POST http://open.wukongdata.com/importv1/potential

请求参数说明

|参数         |说明                           |
|----         |:----:                        |
|access_token | 调用接口凭证                  |
|company_id   | 可选，默认是不向任何绑定公司导入                |

~~返回结果示例~~































