 ### 1. 2会执行，因为每一个script是独立的块，是独立编译执行的
 ```
    <script>
        error;
        console.log(1)
    </script>

    <script>
        console.log(2)
    </script>

 ```
### 2. 语法错误try catch是无法捕获的
#### 加hint在编译阶段发现
```
try{
    var error = "error"：

}catch(e){
    console.log(e)
}


```
### 3.try可以捕获的正常的错误
```
try{
    console.log(error)

}catch(e){
    console.log(e)
}
```
### 4.try catch 无法捕获异步的错误
#### window.onerror可以解决

```
try{
    setTimeout(function(){
        console.log(error)
    },10)

}catch(e){
    console.log(e)
}
window.onerror = function(msg,url,row,col,error){
    console.log("error",msg);
    return true
}
```
### 5 捕获http协议的状态码错误

```
<body>
    <img src="./xx.png" />
</body>

<script>
    window.addEventListener("error",(msg,url,row,col,error)=>{
        console.log("error",msg);
        return true
    },true)//false 无法捕获

</script>

```

### 6.捕获promise的错误

```
    new Promise((resolve,reject)=>{
        reject('错误')
    })
    new Promise((resolve,reject)=>{
        throw 'error'
    })
<script>
    window.addEventListener("unhandledrejection",(e)=>{
        e.preventDefault();
        console.log(e.reason);
        return true
    })//false 无法捕获

</script>

```

### 6.uncatchException
#### 若添加了 uncatchException 处理器，当函数抛出错误时，进程也不会退出
```
process.on("uncatchException", function(e) {
console.log(e);
process.exit(1);
});

```

### 7.代理ajax 的报错
```


```


### 8.向服务端发送错误 *不能用ajax会占用并发
```
navigator.sendBeacon("xx.php");
https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon;
这个方法主要用于满足统计和诊断代码的需要，这些代码通常尝试在卸载（unload）文档之前向web服务器发送数据

```
### 8.开源项目
```
https;//github.com/lgwebdream/zanePerfor

```

