## HTTPS服务器
#### 1、创建自己的CA机构
为CA生成私钥
* openssl genrsa -out ca-key.pem -des 1024

通过CA私钥生成CSR
* openssl req -new -key ca-key.pem -out ca-csr.pem

通过CSR文件和私钥生成CA证书
* openssl x509 -req -in ca-csr.pem -signkey ca-key.pem -out ca-cert.pem

#### 2、创建服务器端证书
为服务器生成私钥
* openssl genrsa -out server-key.pem 1024

指定一份openssl.cnf文件
~~~
[req]
    distinguished_name = req_distinguished_name
    req_extensions = v3_req

    [req_distinguished_name]
    countryName = Country Name (2 letter code)
    countryName_default = CN
    stateOrProvinceName = State or Province Name (full name)
    stateOrProvinceName_default = BeiJing
    localityName = Locality Name (eg, city)
    localityName_default = YaYunCun
    organizationalUnitName  = Organizational Unit Name (eg, section)
    organizationalUnitName_default  = Domain Control Validated
    commonName = Internet Widgits Ltd
    commonName_max  = 64

    [ v3_req ]
    # Extensions to add to a certificate request
    basicConstraints = CA:FALSE
    keyUsage = nonRepudiation, digitalSignature, keyEncipherment
    subjectAltName = @alt_names

    [alt_names]
	#注意这个IP.1的设置，IP地址需要和你的服务器的监听地址一样
    IP.1 = 127.0.0.1
~~~
利用服务器私钥文件服务器生成CSR
* openssl req -new -key server-key.pem -config openssl.cnf -out server-csr.pem

#### 3、创建客户端证书
生成客户端私钥
* openssl genrsa -out client-key.pem

利用私钥生成CSR
* openssl req -new -key client-key.pem -out client-csr.pem

生成客户端证书
* openssl x509 -req -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -in client-csr.pem -out client-cert.pem

#### Node
~~~Javascript
var https = require('https');
var express = require('express');
var app = express();
var fs = require("fs");
var options = {
    key: fs.readFileSync('./keys/server-key.pem'),
    ca: [fs.readFileSync('./keys/ca-cert.pem')],
    cert: fs.readFileSync('./keys/server-cert.pem')
};
var httpsServer = https.createServer(options,app);
httpsServer.listen(3000,'192.168.20.131');
app.get('/', function(req, res) {
    res.sendfile(__dirname + '/index.html');
});
~~~



[目录](https://github.com/jines-z/note)
