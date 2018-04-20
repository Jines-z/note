## 定位和天气

#### 1、获取经纬度

```Javascript
getLocation = () =>{
    return new Promise ((resolve, reject)=>{
        navigator.geolocation.getCurrentPosition((position)=>{
            resolve(position.coords)
        },(error)=>{
            let errorMessage = '失败：' + JSON.stringify(error.message)
            reject(errorMessage)
        },{
            enableHighAccuracy: true,
            timeout: 20000,
            maximumAge: 1000
        })
    })
}
// navigator.geolocation是一个整体内置对象，非路由navigator
```

#### 2、封装一个Get -fetch

```Javascript
const params = (options) =>{
    let paramString = ''
    for (let i in options) {
        paramString += i + '=' + options[i] + '&'
    }
    return paramString.slice(0,-1)
}
const Get = (url,options,cb) =>{
    fetch(url+params(options))
        .then((response)=>response.json())
        .then((responseBody)=>{
            cb(responseBody)
        })
        .catch((error)=>{
            cb(error)
        })
}
export default Get
```

#### 3、高德api逆地理编码

```Javascript
this.getLocation().then((coords)=>{
    const {longitude,latitude} = coords
    let url = 'http://restapi.amap.com/v3/geocode/regeo?'
    let options = {
        key:'注册成为开发者，创建一个key',
        location:longitude+','+latitude
    }
    Get(url,options,(responseBody)=>{
        if(responseBody.status ==1){
            const {adcode,city,district} = responseBody.regeocode.addressComponent
            // adcode获取天气用
            // city城市   district区域   .....
        }
    })
}).catch((errorMessage)=>{
    console.log(errorMessage)
})
```

#### 4、高德api天气

```Javascript
let url = 'http://restapi.amap.com/v3/weather/weatherInfo?'
let options = {
    key:'注册成为开发者，创建一个key',
    city:adcode,
    extensions:'base',
    output:'JSON'
}
Get(url,options,(res)=>{
    if (res.status == 1) {
        const {weather,temperature} = res.lives[0]
        // weather多云啥的    temperature气温  ......
    }
})
```

[高德API](http://lbs.amap.com/)

登录-> 控制台-> 应用管理 ->创建新应用 ->生成key

[目录](https://github.com/beverle-y/note)