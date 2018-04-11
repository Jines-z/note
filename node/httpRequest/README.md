## HTTP请求
使用request模块
~~~
var request = require('request')
function params (options) {
    var paramString = ''
    for (var i in options) {
        paramString += i + '=' + options[i] + '&'
    }
    return paramString.slice(0, -1)
}
var data = {
    name: 'xxx',
    age: 'xxx',
    accountType: 'xxx',
    openId: 'xxxxxxxxx'
}
var urlData = params(data)
var cookie_val = 'session_id=openId;session_type=accessToken;'
var option = {
    url: 'http://xxx.xxx.com/xx/xx?' + urlData,
    headers: {
        'Cookie': cookie_val
    }
}
request(option, function(error, response, body) {
    console.log(body)
})
~~~
[目录](https://github.com/beverle-y/note)