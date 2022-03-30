# API接口文档

可以通过调用API接口，使用可编程的方式生成短链接

### 接口调用地址

自行部署的CloudFlare Worker地址，例如：https://url.dem0.workers.dev 或是自行绑定的域名如 https://yourdomain.com

### 调用方式：HTTP POST 请求格式: JSON
示例：
```
{
	"url": "https://example.com",
    "key": "abcdef",
    "hash" "da8af452167d81d5b1ade222fd0c0510"
}
```


```
#### 指定key/path
curl 'https://yourdomain.com/' -H 'content-type: application/json' -d '{"url":"https://example.com","key":"abcdef", "hash": "da8af452167d81d5b1ade222fd0c0510"}'

#### 非白名单域名
curl 'https://yourdomain.com/' -H 'content-type: application/json' -d '{"url":"https://example.com", "hash": "da8af452167d81d5b1ade222fd0c0510"}'

#### 普通请求 （随机key/path, 白名单域名）
curl 'https://yourdomain.com/' -H 'content-type: application/json' -d '{"url":"https://example.com"}'

```

### 请求参数:

| 参数名 | 类型 | 说明 |是否必须|示例|
| :----:| :----: | :----: | :----: | :----: |
| url | string | 网址（需包括http://或https://) |是|https://example.com|
| key | string | 指定生成的key/path |否|abcdef 成功生成短链接 https://yourdomain.com/abcdef|
| hash | string | md5(url+password) 指定key/path时或者非白名单域名必填|否|da8af452167d81d5b1ade222fd0c0510|

### 响应示例 (JSON)：

```
{
    "status": 200,
    "shortUrl": "https://yourdomain.com/abcdef"
}
```

### 响应参数:
| 参数名 | 类型 | 说明 |示例|
| :----:| :----: | :----: | :----: |
|status|int|	状态码：200为调用成功|200|	
|msg|string|	错误信息描述 |Error: Url illegal.|	
|shortUrl|string| 完整短链接 | https://yourdomain.com/abcdef |

