# ajax

------

## XMLHttpRequest的基本使用

XML的get请求发送

```js
var xhr = new XMLHttpRequest()
xhr.open('GET','url')
xhr.send()
xhr.onreadystatechange = function(){
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

## 数据交换格式

### XML

传输数据用 体积大效率低 解析困难

### JSON

用字符串来表示js的对象和数组

两种结构

对象结构 {key:value,key:value} key必须是使用英文的双引号包裹的字符串, value则可以是基本的数据结构类型

反序列化 JSON->JS  JSON.prase()

序列化 JS -> JSON  JSON.stringify()

## axios

## 使用axios发起GET请求

```js
axios.get('url',{params:{/*参数*/}}).then(callback)


var url = "xxxxxxxxx"
var obj = {
    name : xxx,
    age : xx
}
axios.get(url,{params:obj}).then(function(res){
    console.log(res.data);
})
```

POST同理

```js
// 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/post'
 // 要提交到服务器的数据
 var dataObj = { location: '北京', address: '顺义' }
 // 调用 axios.post() 发起 POST 请求
 axios.post(url, dataObj).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(result)
 })
```



直接使用axios发起GET()和POST()请求

```js
axios({
    method:'GET'/'POST',
    url:  'url',
    params/data:{ name : xx,age:xx}}).then(function(res){
    console.log(res.data);
})



```