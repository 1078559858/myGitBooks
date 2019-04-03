# 表达式括号的作用

<script>
    var menu = {
        "m3_a_1":'\/\\d{4}(-|\\\/|\\\.)\\d{2}\\1\\d{2}\/',
        "m3_a_2":'123 <br> 1<br>23<br>3',
        "m4_a_1":'(?:p)',
        "m5_a_1":"str.replace(/^\s+|\s+$/g, '')",
        "m5_a_2":'str.replace(/^\s*(.*?)\s*$/g, "$1")',
        "m5_b_1":'function titleize(str) {<br>\\t return str.toLowerCase().replace(/(?:^|\s)\w/g, function(c) {<br>\\t \\t return c.toUpperCase();<br>\\t });<br>}',
        "m5_b_2":'待定。。。。',
        "m5_c_1":"function camelize(str) {<br>\\t return str.replace(/[-_\s]+(.)?/g, function(match, c) { <br>\\t \\t return c ? c.toUpperCase() : ''; <br>\\t }); <br>}",
        "m5_c_2":"待定。。。。",
        "m5_d_1":"function dasherize(str) {<br>\\t return str.replace(/([A-Z])/g, '-$1').replace(/[-_\s]+/g, '-').toLowerCase();<br>}",
        "m5_d_2":'待定...',
        "m5_f_1":'\/\<\(\[\^\>\]\+\)\>\[\\\d\\\D\]\*\<\\\/\\1\>\/',
        "m5_f_2":"待定。。。"
    }
</script>

提供了分组，分组可以在javascript中、正则中引用。

1. 分组和分支结构

   ```js
   //分组结构
   /(ab)+/g
   
   //多选分支结构
   (p1|p2)
   ```

2. 捕获分组

   > 练习： 提取年月日
   >
   > ```js
   > var regex = /(\d{4})-(\d{2})-(\d{2})/;
   > var string = "2017-06-12";
   > 
   > regex.test(string); // 正则操作即可，例如
   > //regex.exec(string);
   > //string.match(regex);
   > 
   > console.log(RegExp.$1); // "2017"
   > console.log(RegExp.$2); // "06"
   > console.log(RegExp.$3); // "12"
   > ```
   >
   > 练习： 替换
   >
   > ```js
   > var regex = /(\d{4})-(\d{2})-(\d{2})/;
   > var string = "2017-06-12";
   > var result = string.replace(regex, "$2/$3/$1");
   > console.log(result); // "06/12/2017"
   > 
   > 或者：
   > var result = string.replace(regex, function() {
   > 	return RegExp.$2 + "/" + RegExp.$3 + "/" + RegExp.$1;
   > });
   > console.log(result); // "06/12/2017"
   > 
   > 或者：
   > var result = string.replace(regex, function(match, year, month, day) {
   > 	return month + "/" + day + "/" + year;
   > });
   > console.log(result); // "06/12/2017"
   > ```

3. 反向引用

   > 匹配如下三种格式，且分隔符一致
   >
   > 2016-06-12
   >
   > 2016/06/12
   >
   > 2016.06.12
   >
   > {{"answer" | exp_pop(0,"menu.m3_a_1",0)}}

   > 括号嵌套：
   >
   > var regex = /^()\1\2\3\4$/;
   >
   > var string = "1231231233";
   >
   > console.log( regex.test(string) ); // true
   >
   > console.log( RegExp.$1 ); // ?
   >
   > console.log( RegExp.$2 ); // ?
   >
   > console.log( RegExp.$3 ); // ?
   >
   > console.log( RegExp.$4 ); // ?
   >
   > {{"answer" | exp_pop(0,"menu.m3_a_2",0)}}

4. 非捕获分组

   > 捕获分组 伪代码是什么？
   >
   > {{"answer" | exp_pop(0,"menu.m4_a_1",0)}}

5. 相关案例

   1. trim实现

      > 替换开头和结尾空白字符
      >
      > {{"answer" | exp_pop(0,"menu.m5_a_1",0)}}
      >
      > 
      >
      > 匹配字符串，提取数据（捕获分组）
      >
      > {{"answer" | exp_pop(0,"menu.m5_a_2",0)}}

   2. 转换首字母大小写

      > 捕获分组法
      >
      > {{"answer" | exp_pop(0,"menu.m5_b_1",0)}}
      >
      > 
      >
      > 非捕获分组法
      >
      > {{"answer" | exp_pop(0,"menu.m5_b_2",0)}}

   3. 驼峰化

      > 捕获分组法(作者的代码首字母大写了，怎么消除？)
      >
      > {{"answer" | exp_pop(0,"menu.m5_c_1",0)}}
      >
      > 
      >
      > 非捕获分组法
      >
      > {{"answer" | exp_pop(0,"menu.m5_c_2",0)}}

   4. 中划线化(驼峰逆过程)

      > 捕获分组法
      >
      > {{"answer" | exp_pop(0,"menu.m5_d_1",0)}}
      >
      > 
      >
      > 非捕获分组法
      >
      > {{"answer" | exp_pop(0,"menu.m5_d_2",0)}}

   5. html转义和反转义

      ```js
      // 将HTML特殊字符转换成等值的实体
      function escapeHTML(str) {
      	var escapeChars = {
      	  '¢' : 'cent',
      	  '£' : 'pound',
      	  '¥' : 'yen',
      	  '€': 'euro',
      	  '©' :'copy',
      	  '®' : 'reg',
      	  '<' : 'lt',
      	  '>' : 'gt',
      	  '"' : 'quot',
      	  '&' : 'amp',
      	  '\'' : '#39'
      	};
      	return str.replace(new RegExp('[' + Object.keys(escapeChars).join('') +']', 'g'), function(match) {
      		return '&' + escapeChars[match] + ';';
      	});
      }
      console.log( escapeHTML('<div>Blah blah blah</div>') );
      // => &lt;div&gt;Blah blah blah&lt;/div&gt;
      ```

      ```js
      // 实体字符转换为等值的HTML。
      function unescapeHTML(str) {
      	var htmlEntities = {
      	  nbsp: ' ',
      	  cent: '¢',
      	  pound: '£',
      	  yen: '¥',
      	  euro: '€',
      	  copy: '©',
      	  reg: '®',
      	  lt: '<',
      	  gt: '>',
      	  quot: '"',
      	  amp: '&',
      	  apos: '\''
      	};
      	return str.replace(/\&([^;]+);/g, function(match, key) {
      		if (key in htmlEntities) {
      			return htmlEntities[key];
      		}
      		return match;
      	});
      }
      console.log( unescapeHTML('&lt;div&gt;Blah blah blah&lt;/div&gt;') );
      // => <div>Blah blah blah</div>
      ```

   6. 匹配成对标签

      > 反引用法
      >
      > {{"answer" | exp_pop(0,"menu.m5_f_1",0)}}
      >
      > 
      >
      > 作者提供的不支持嵌套匹配，怎么办？
      >
      > {{"answer" | exp_pop(0,"menu.m5_f_2",0)}}

# 疑问

1. > console.log( "\7\8\9".split("") ); //[ '\u0007', '8', '9' ] 为什么是这个结果？ 8和9不转义了？

2. 实例中的待定选项还未完成。。。。