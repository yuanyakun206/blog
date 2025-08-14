---
title: axios常用方法
date: 2025-08-13 15:55:47
tags: axios
categories:
- [前端基础知识,网络]
---
在 Axios 中，get 和 post 方法的参数略有不同 。以下是它们的详细参数说明：

### 1. axios.get(url, config)

- url: 请求的 URL 地址。

- config: 可选的配置对象，包含以下属性：

- params: URL 查询参数，类型为对象。例如：{ id: 123 } 会被转换为 ?id=123。

- headers: 自定义请求头，类型为对象。例如：{ 'Authorization': 'Bearer token' }。

- timeout: 请求超时时间，单位为毫秒。

- responseType: 响应类型，可以是 arraybuffer, blob, document, json, text, stream。

- withCredentials: 表示跨域请求时是否需要使用凭证（cookies）。

- validateStatus: 自定义状态码的有效性，默认是 status >= 200 && status < 300。

#### 示例

```javascript
axios.get('https://api.example.com/data', {
  params: {
    id: 123,
  },
  headers: {
    'Authorization': 'Bearer token',  
  },  timeout: 1000,
});
```



### 2. axios.post(url, data, config)

- url: 请求的 URL 地址。

- data: 要发送的数据，通常是对象或字符串。

- config: 可选的配置对象，包含以下属性（与 get 方法相同）：

- headers: 自定义请求头。

- timeout: 请求超时时间。

- responseType: 响应类型。

- withCredentials: 是否使用凭证。

- validateStatus: 自定义状态码的有效性。

#### 示例

```javascript
axios.post('https://api.example.com/data', {
  name: 'John Doe',  age: 30, 
}, {
  headers: {
    'Content-Type': 'application/json',  
  },
  timeout: 1000,
}); 

//post 传 param （?）写法 
export const readNotification = (notificationId) => {
  return axios
    .post(`${baseUrl}/read`, {}, { params: { notificationId } })
    .then((res) => res.data); };
```