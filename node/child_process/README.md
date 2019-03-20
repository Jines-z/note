## Child_Process 子进程

基石： `child_process.spawn()`、 `child_process.spawnSync()`

* `spawn()`：使用指定的命令行参数创建新进程，可捕获 stdout、stderr。

* `spawnSync()`：`spawn()` 的同步函数，会阻塞 Node.js 事件循环。

* `exec()`：衍生一个 shell 并在 shell 上运行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式一次性返回.

* `execSync()`：`exec()` 的同步函数，会阻塞 Node.js 事件循环。

* `execFile()`：类似 `exec()`，但直接衍生命令，且无需先衍生 shell。

* `execFileSync()`：`execFile()` 的同步函数，会阻塞 Node.js 事件循环。

* `fork()`：衍生一个新的 Node.js 进程，并通过建立 IPC 通讯通道来调用指定的模块，该通道允许父进程与子进程之间相互发送信息。

**坑点：**
* 无法用子进程来读取，用子进程设置的 node 环境变量，需套一层 npm。

* Windows 上无法脱离 `cmd.exe` 直接执行 `.cmd` 批处理，可以设置 `shell` 为 `true` 以隐式调用 cmd。

Windows 和 Mac 下的不同：
```Javascript
Windows

spawn('npm run build', {
    stdio: [0, 1, 2],
    shell: process.platform === 'win32',
    detached: false
})
```

```Javascript
Mac

spawn('npm', ['run', 'build'], {
    stdio: [0, 1, 2],
    shell: process.platform === 'win32',
    detached: false
})
```


[目录](https://github.com/jines-z/note)
