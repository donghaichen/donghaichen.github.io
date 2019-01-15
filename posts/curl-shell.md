### 简介

参数	| 用途
---|---|
-X | 请求方式(注意必须为大写POST)
-v | 请求信息
-H | 请求header
-d | 请求参数

### 示例

```bash
curl -v -X PUT -H 'Authorization:Bearer eyJ0eXAiOiJKV1QiLCJhbGciO' -d 'age=18&cupSize=A' http://127.0.0.1/api/v1/userInfo
```