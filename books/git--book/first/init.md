# init

> 下载 typora
>
> npm install -g gitbook-cli
>
> gitbook init
>
> gitbook build  ./ book     //不要用git build，github page 不识别下滑线。除非把根目录的.nojekyll放入下滑线目录，不过麻烦。 win7创建命令：type nul> .nojekyll
>
> gitbook serve --port 8888

plugins

	> book.json 
	>
	> {
	> 	"plugins":["expand-collapse-popup-window"]
	> }

### asdfadf

<script>
  var my_text="Hello this is an example of customize content.<br>\
if you want to wrap ,you have to type a '<br>',and '\r\n' is no use.<br>\
Like this \r\n see, no use.";
</script>

{{ "Click here" | exp_pop(0,"my_text",0) }}

<script>
  var my_text="Hello this is an example of customize content.<br>\
if you want to wrap ,you have to type a '<br>',and '\r\n' is no use.<br>\
Like this \r\n see, no use.";
</script>

