# sockethttp-ext-demo
[sockethttp](https://github.com/fred913/sockethttp/)的一个简单的扩展程序示例

### 贡献者

 - Sheng Fan [Github](https://github.com/fred913)

### 插件开发文档

#### 创建一个插件信息文件：
 - 创建一个类似于下方代码的JSON文件（要求命名为 `ext.json` ）:
 

``` json
 {
    "extname": "HTTP OPTIONS请求支持（示例）",
    "extfiles": {
        "a": [
            [
                "./a.json",
                "r"
            ],
            {
                "encoding": "utf-8"
            }
        ]
    }
}
 ```

 - 第4~12行为 `open(...)` 函数的参数，如下所示

``` 
[
    [
        open函数的匿名参数
    ], 
    {
        open函数的命名参数
    }
]
```

 - 所以以下代码放在extfiles中等同于在代码开头放置 `a = open("./a.json", "r", encoding="utf-8")`。

``` json
"extfiles": {
    "a": [
        [
            "./a.json",
            "r"
        ],
        {
            "encoding": "utf-8"
        }
    ]
}
```

#### __为什么不直接在ext.py使用 `open("./a.json", "r", encoding="utf-8")` ?__

 - 首先，我觉得需要说明一下 `extension.py` 的实现原理。 `load_extension` 其实是读取代码目录下extension目录中指定文件夹中的 `ext.json` 和 `ext.py` 的。
 - 在获得文件内容之后，extension.py会直接使用compile函数和exec函数运行这段代码，然后通过修改和读取`locals`和`globals`环境实现获取`ext`函数，然后返回供用户调用。这些代码实现在exec中实现非常简单，这就是为什么不使用`importlib.import_module`和`__import__`的原因了。
 - 但是，这段代码也带来了一个困扰，也就是读取文件的相对目录并不是`extensions/xxx`，而是`extensions`所在的目录。所以在`ext.json`中提供了一个获取扩展所在目录下文件的方法。所有可传入`open`函数的参数都可以在`ext.json`文件中定义。
 ----

