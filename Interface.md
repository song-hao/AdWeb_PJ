# 前后端接口

## 用户登录

> url: user.do?action=login

### 请求参数

|key|description|type|
|---|---|---|
|account|账号|string|
|password|密码|string|

### 请求示例

> user.do?action=login?account=aaa&password=bbb

### 返回参数

|key|description|
|---|---|
|status|状态码, 0为正常, 其它值为发生错误|
|user|用户信息, 若发生错误则不存在该标签|

### 返回示例

	{
		"status": "0", //状态码, 0为正常
		"user": {
			"id": "3",
			"head": "img/a.jpg", // 头像图片url
			"name": "测试用户",
			"account": "test"
		}
	}

## 用户注册

> url: user.do?action=register

### 请求参数

|key|description|type|
|---|---|---|
|account|账号|string|
|password|密码|string|
|name|昵称|string|

### 请求示例

> user.do?action=register?account=aaa&password=bbb&name=啦啦啦

### 返回参数

|key|description|
|---|---|
|status|状态码, 0为正常, 其它值为发生错误(比如账号重复)|
|user|用户信息, 若发生错误则不存在该标签|

### 返回示例

	{
		"status": "0", //状态码, 0为正常
		"user": {
			"id": "4",
			"head": "img/a.jpg", // 头像图片url
			"name": "啦啦啦",
			"account": "aaa"
		}
	}

## 景观信息获取

> url: attraction.do?action=get

### 请求参数

|key|description|type|
|---|---|---|
|x1|地图可视范围左上角的经度lng|double|
|y1|地图可视范围左上角的维度lat|double|
|x2|地图可视范围右下角的经度lng|double|
|y2|地图可视范围右下角的维度lat|double|
|sort|按照什么属性排序|none(无), rating(评分), favor(收藏数), footprint(足迹), wish(心愿)|
|type|选取什么类型景观|all(所有), 或上海近代公园、上海工业遗址等|

### 请求示例

> attraction.do?action=get&x1=116.01&y1=36.1&x2=116.26&y2=36.4&sort=none&type=all

### 返回参数

|key|description|
|---|---|
|attractionList|景观信息列表, 详见示例|

### 返回示例

	[
		{
			"type": "上海工业遗址",
			"attractions": [
				{
					"id": "2",
					"lng": "116.133",
					"lat": "36.384",
					"bounds": [
						{
								"lng": xx.xx,
								"lat": xx.xx
						},
						{
								"lng": xx.xx,
								"lat": xx.xx
						},
						...
					]
					"name": "1933老场坊",
					"information": "这是景观的基本信息",
					"introduction": "这是关于景观的详细介绍",
					"rating": "4.2",
					"footprint": "20",
					"favor": "10",
					"wish": "15",
					"rating5": "100",
					"rating4": "80",
					"rating3": "60",
					"rating2": "20",
					"rating1": "10",
					"type": "上海工业遗址"
				},
				...
			]
		},
		...
	]

## 评价景观

> url: attraction.do?action=rate

### 请求参数

|key|description|type|
|---|---|---|
|userId|用户的id|integer|
|attractionId|景观的id|integer|
|rating|评分|integer|
|content|评价的内容|string|
|image|图片(形式待定)|file|

### 请求示例

> attraction.do?action=rate&userId=1&attractionId=17&rating=4&content=这个地方真不错

## 收藏景观

> url: attraction.do?action=favor

### 请求参数

|key|description|type|
|---|---|---|
|userId|用户的id|integer|
|attractionId|景观的id|integer|

### 请求示例

> attraction.do?action=favor&userId=1&attractionId=17

### 返回参数

|key|description|
|---|---|
|status|状态码, 0为正常, 其它值为发生错误(比如已评价)|

### 返回示例

	{
		"status": "0" or "1" or "-1"...
	}


## 加入足迹

> url: attraction.do?action=footprint

### 请求参数

|key|description|type|
|---|---|---|
|userId|用户的id|integer|
|attractionId|景观的id|integer|

### 请求示例

> attraction.do?action=footprint&userId=1&attractionId=17

### 返回参数

|key|description|
|---|---|
|status|状态码, 0为正常, 其它值为发生错误(比如已评价)|

### 返回示例

	{
		"status": "0" or "1" or "-1"...
	}


## 加入心愿单

> url: attraction.do?action=wish

### 请求参数

|key|description|type|
|---|---|---|
|userId|用户的id|integer|
|attractionId|景观的id|integer|

### 请求示例

> attraction.do?action=wish&userId=1&attractionId=17

### 返回参数

|key|description|
|---|---|
|status|状态码, 0为正常, 其它值为发生错误(比如已评价)|

### 返回示例

	{
		"status": "0" or "1" or "-1"...
	}
