# sockethttp-ext-demo
[sockethttp](https://github.com/fred913/sockethttp/)的一个简单的扩展程序示例


### Contributor
 - Sheng Fan [Github](https://github.com/fred913)

### Plugin development documentation
#### create extension info file:
 - create a json file like `ext_demo/ext.json` as follows:
 ```json
 {
    "extname": "HTTP method support: Options",
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
 - Line 4 ~ 12 is for `open(...)` function in python. As follows: 
```
[
    args (array), 
    kwargs (key-value pair)
]
```
 - so this json code is same as `a = open("./a.json", "r", encoding="utf-8")` in python.
```json
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
 - __Why not use `open("./a.json", "r", encoding="utf-8")` directly in ext.py?__
   
   First, `extension.py` is using `exec` and reading file content to execute the extension script, not using `importlib.import_module` or `__import__`. This way will protect the code in the `extension.py`. And the environment is defined in a variable (using `exec` method).
 ----
 #### In case of the following situations, submit a pull request or issue:
 - Bugs that can cause fatal errors
 - Introduce some new features
