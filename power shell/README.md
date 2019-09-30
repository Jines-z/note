## PowerShell 给命令设置 alias

#### 1、验证是否存在 $Profile
```shell script
test-path $Profile
```
false: 配置文件不存在（继续步骤2）。

true : 不多说了，直接跳过步骤2和3吧。除非你想创建一个新的配置文件，不过这将删除当前的配置文件。

#### 2、创建一个新的配置文件
```shell script
New-Item -Path $Profile -ItemType file -Force
```

#### 3、再次验证是否成功创建新的配置文件
重复步骤1吧，结果应该为 `true`。

#### 4、在记事本中打开配置文件
```shell script
notepad $Profile
```

#### 5、开始键入你需要的配置
```shell script
function Start-npmWithTaobao {
    $argList = $args -Join ' '
    Start-Process -FilePath 'npm' -ArgumentList "--registry=https://registry.npm.taobao.org $argList"  -NoNewWindow -Wait
}
Set-Alias tnpm Start-npmWithTaobao
```

注意事项：
*   Set-Alias 这个方法不支持语句/命令，只能给 function 或者 program 设置 alias。
*   Start-Process 的参数可参考 [这个链接](https://docs.microsoft.com/zh-cn/powershell/module/Microsoft.PowerShell.Management/Start-Process?view=powershell-7)
*   PowerShell 的 verb（也就是 function 的第一个单词，就是上面那个 Start）是有限制的，所有可用的 verb 可以通过 Get-Verb 这个方法得到。

[目录](https://github.com/jines-z/note)
