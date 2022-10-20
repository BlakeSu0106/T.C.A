# Telligent.Consumer.ApiGateway
客戶端的api閘道

# 設定方式
在`ocelot.js`
```js
{
  "Routes": [
    {
      "DownstreamPathTemplate": "/{endpoint}",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "",
          "Port": 80
        }
      ],
      "UpstreamPathTemplate": "/{company}/{service}/{endpoint}",
      "UpstreamHttpMethod": [ "Get", "Post", "Put", "Delete" ],
      "Priority": 0
    }
  ],
  "GlobalConfiguration": {
  }
}
```
1. `DownstreamHostAndPorts.Host` 寫入實際服務的位置
2. `DownstreamHostAndPorts.UpstreamHttpMethod` 寫入所有可能會使用的HttpMethod
3. `Routes` 裡面by到服務