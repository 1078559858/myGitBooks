# gitbook简介

gitbook 是本书的编辑工具，简单易用。



# 下载和安装

* 下载 typora   (一款编辑工具)
* npm install -g gitbook-cli
* gitbook init
* gitbook build   ./    book  
* gitbook serve --port 8888

> 不要只用git build，github.io page 不识别下滑线。除非把根目录的.nojekyll放入下滑线目录，不过太麻烦。 win7创建命令：type nul> .nojekyll

# 插件使用

* 折叠框

  + 效果:   

    <script>
    	var my_text="Hello this is an example of customize content.<br>\
    if you want to wrap ,you have to type a '<br>',and '\r\n' is no use.<br>\
    Like this \r\n see, no use.";
    </script>

    {{ "Click here" | exp_pop(0,"my_text",0) }}

  * 代码

    ```html
    <scritp>
        var my_text = `hello world<br>` + 
            `hello world 2 <br>` + 
            `hello world 3`;
    </scritp>
    ```

    > \{\{Click here" | exp_pop(0, "my_text", 0)\}\}

    

  * 引入

    > //book.json 引入 
    >
    > {
    > 	"plugins":["expand-collapse-popup-window"]
    > }