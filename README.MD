#LUA

## LUA基本的语法

## Lua+Nginx的使用
如果调用的是lua代码块,就可以在laction模块里面进行操作
示例如下:
```shell script
		location / {
			default_type text/html;
			content_by_lua '
			ngx.say("</html><head>this page drived by lua</head><body>this is body..................</body></html>")
			';
		}	
```
执行的效果如下：
[执行lua代码块](./files/execute-lua-block-1.PNG)

如果调用的lua脚本文件，就可以使用用如下的放在在location模块下操作
示例如下:
```shell script
location / {
	default_type text/html;
	content_by_lua_file /usr/local/openresty/lua_codes/resp-1.lua;
}	
# resp-1.lua脚本如下：
ngx.say("</html><head>this page drived by lua</head><body>this is body..................</body></html>")

```
执行的效果如下：
[执行lua代码块](./files/execute-lua-block-1.PNG)


注意: 默认情况下nginx会开启lua脚本缓存，但是脚本的缓存会导致脚本修改后可能无法及时的看到修改后的样子，因为为了调试可以将nginx的lua脚本缓存关闭
在http模块下添加
lua_code_cache off;
启动会提示损害性能