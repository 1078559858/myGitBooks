# 字符匹配

<script>
    var menu = {
        "m1_a_1":"//g是全局搜索 global <br> /ab{2,5}c/g",
        "m1_b_1":"/a[123]b/",
        "m2_a_1":'[1-6a-fG-M]',
        "m2_a_2":'[-az]或[az-]或[a\\-z]即要么放在开头，要么放在结尾，要么转义',
        "m2_b_1":'[^abc]',
        "m2_c_1":"\\d \\D [0-9]",
        "m2_c_2":"[0-9a-zA-Z_] 数字、大小写字母和下划线",
        "m2_c_3":"[\\t\\v\\n\\r\\f] 表示空白符 <br>包括空格、水平制表符、垂直制表符、换行符、回车符、换页符. <br> 记忆方式：s是space character的首字母",
        "m2_c_4":"\\b \\B 一般用来获取，不用来匹配。",
        "m2_c_5":"[^\\n\\r\\u2028\\u2029] 换行符、回车符、行分隔符和段分隔符除外",
        "m2_c_6":"[\\d\\D]、[\\w\\W]、[\\s\\S]、[^]",
        "m3_a_1":"{m,}",
        "m3_a_2":"{m,m}",
        "m3_a_3":"{0,1} ？",
        "m3_a_4":"{1,} +",
        "m3_a_5":"*",
        "m3_b_1":"/\d{2,5}?/",
        "m3_b_2":"{m,n}? <br> {m,}? <br> ?? <br> +? <br> *?",
        "m4_a_1":"/good|bye/",
        "m4_a_2":"/^a|b$/ 和 /^((a)|(b))$/是有区别的",
        "m5_a_1":"/#([0-9a-fA-F]{6}|[0-9a-fA-F]{3})/g",
        "m5_b_1":"/^([01][0-9]|[2][0-3]):[0-5][0-9]$/",
        "m5_c_1":"/^[0-9]{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$/",
        "m5_d_1":'/^[a-zA-Z]:\\\\([^\\\\:*<>|"?\\r\\n/]+\\\\)*([^\\\\:*<>|"?\\r\\n/]+)?$/',
        "m5_e_1":'/id=".*?"/   <br>优化：/id="[^"]*"/'
    }
</script>

1. 两种匹配模式

   1. 横向模糊：正则可匹配的字符串的长度不是固定的，可以是多种情况的

      > 练习： 匹配一个a，2到5个b，一个c
      >
      > {{"answer" | exp_pop(0,"menu.m1_a_1",0)}}

   2. 纵向模糊：具体到某一位字符时，有多种可能。

      > 练习：匹配  "a1b"、"a2b"、"a3b"
      >
      > {{"answer" | exp_pop(0,"menu.m1_b_1",0)}}

2. 字符组：（虽然叫组，但是只匹配一个字符）

   1. 范围表示法

      > 表示：[123456abcdefGHIJKLM]
      >
      > {{"answer" | exp_pop(0,"menu.m2_a_1",0)}}
      >
      > 
      >
      > 匹配“a”、“-”、“z”这三者中任意一个字符(三种表示方法)
      >
      > {{"answer" | exp_pop(0,"menu.m2_a_2",0)}}

   2. 排除：**字符组**第一位放**脱字符**表示求反：

      > 练习：不能是"a"、"b"、"c"
      >
      > {{"answer" | exp_pop(0,"menu.m2_b_1",0)}}

   3. 简写：

      > 数字和非数字？
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_1",0)}}
      >
      > \w 和  \W的含义？
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_2",0)}}
      >
      > \s 和 \S 的含义？
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_3",0)}}
      >
      > 匹配字的边界?   [\b的作用是什么？](https://blog.csdn.net/nicajonh/article/details/78815869)
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_4",0)}}
      >
      > 通配符代表什么？ ./.* 代表什么意义？
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_5",0)}}
      >
      > 匹配任意字符的四种方式？
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_6",0)}}

3. 量词： 重复 

   1. 简写

      > 至少出现m次。
      >
      > {{"answer" | exp_pop(0,"menu.m3_a_1",0)}}
      >
      > 出现m次
      >
      > {{"answer" | exp_pop(0,"menu.m3_a_2",0)}}
      >
      > 出现0次或者一次
      >
      > {{"answer" | exp_pop(0,"menu.m3_a_3",0)}}
      >
      > 至少出现一次
      >
      > {{"answer" | exp_pop(0,"menu.m3_a_4",0)}}
      >
      > 任意次
      >
      > {{"answer" | exp_pop(0,"menu.m3_a_5",0)}}

   2. 惰性匹配： 量词后面加个问号就能实现惰性匹配.   

      > 表示： 匹配2到5次都行，当2个就够的时候，就不在往下尝试了。
      >
      > {{"answer" | exp_pop(0,"menu.m3_b_1",0)}}
      >
      > 一共五种简写，五种惰性匹配方法：
      >
      > {{"answer" | exp_pop(0,"menu.m3_b_2",0)}}

4. 分支结构： 管道符， 惰性匹配。

   > 匹配： good 或者 bye 
   >
   > {{"answer" | exp_pop(0,"menu.m4_a_1",0)}}
   >
   > 注意：如果有脱字符在最前面，有什么要注意的？
   >
   > {{"answer" | exp_pop(0,"menu.m4_a_2",0)}}

5. 案例分析

   1. 匹配16进制颜色

      > \#ffbbad
      >
      > \#Fc01DF
      >
      > \#FFF
      >
      > \#ffE
      >
      > {{"answer" | exp_pop(0,"menu.m5_a_1",0)}}

   2. 匹配时间

      > 23:59
      >
      > 02:07
      >
      > {{"answer" | exp_pop(0,"menu.m5_b_1",0)}}

   3. 匹配日期

      > 2017-06-10
      >
      > {{"answer" | exp_pop(0,"menu.m5_c_1",0)}}

   4. 匹配路径

      > F:\study\javascript\regex\regular expression.pdf
      >
      > F:\study\javascript\regex\
      >
      > F:\study\javascript
      >
      > F:\
      >
      > ps:[ ^\\:*<>|"?\r\n/ ]来表示合法字符
      >
      > ps: 盘符 [ a-zA-Z ]:\\\\
      >
      > {{"answer" | exp_pop(0,"menu.m5_d_1",0)}}

   5. 匹配ID

      > ```html
      > <div id="container" class="main"></div>
      > ```
      >
      > {{"answer" | exp_pop(0,"menu.m5_e_1",0)}}
