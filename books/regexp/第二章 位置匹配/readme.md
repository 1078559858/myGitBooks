# 位置匹配

<script>
    var menu = {
        "m2_a_1":'#hello#',
        "m2_a_2":'#I# <br>' + '#love#<br>' + '#javascript#<br>',
        "m2_b_1":'\\b是单词边界，具体就是\\w和\\W之间的位置，也包括\\w和^之间的位置，也包括\\w和$之间的位置。',
        "m2_b_2":'[#JS#] #Lesson_01#.#mp4#',
        "m2_b_3":'#[J#S]# L#e#s#s#o#n#_#0#1.m#p#4',
        "m2_c_1":'he#l#lo',
        "m2_c_2":'#h#ell#o#',
        "m4_a_1":'/.^/',
        "m4_b_1":'/(?=\d{3}$)/g',
        "m4_b_2":'/(?=(\d{3})+$)/g',
        "m4_b_3":'/(?!^)(?=(\d{3})+$)/g',
        "m4_b_4":'/(?!\\b)(?=(\\d{3})+\\b)/g <br> /\\B(?=(\\d{3})+\\b)/g',
        "m4_c_1":'/^[0-9A-Za-z]{6,12}$/',
        "m4_c_2":'/(?=.*[0-9])^[0-9A-Za-z]{6,12}$/',
        "m4_c_3":'/(?=.*[0-9])(?=.*[a-z])^[0-9A-Za-z]{6,12}$/',
        "m4_c_4":'/(?!^[0-9]{6,12}$)(?!^[a-z]{6,12}$)(?!^[A-Z]{6,12}$)^[0-9A-Za-z]{6,12}$/;'
    }
</script>



1. 什么是位置？

   > 相邻字符之间的位置

2. 如何匹配位置

   > 在ES5中，共有6个**锚字符**：
   >
   > ^ $ \b \B (?=p) (?!p)

   1. 脱字符和美元符号

      > ^（脱字符）匹配开头，在多行匹配中匹配行开头。
      >
      > $（美元符号）匹配结尾，在多行匹配中匹配行结尾。

      > 练习1: "hello".replace(/^|$/g, '#')
      >
      > {{"answer" | exp_pop(0,"menu.m2_a_1",0)}}
      >
      > 
      >
      > 练习2: "I\nlove\njavascript".replace(/^|$/gm, '#')
      >
      > {{"answer" | exp_pop(0,"menu.m2_a_2",0)}}

   2.  **\b和\B**

      > \b 代表什么?
      >
      > {{"answer" | exp_pop(0,"menu.m2_b_1",0)}}
      >
      > 
      >
      > ```js
      > var result = "[JS] Lesson_01.mp4".replace(/\b/g, '#');
      > 
      > console.log(result);
      > ```
      >
      > {{"answer" | exp_pop(0,"menu.m2_b_2",0)}}
      >
      > 
      >
      > ```js
      > var result = "[JS] Lesson_01.mp4".replace(/\B/g, '#');
      > 
      > console.log(result); 
      > ```
      >
      > {{"answer" | exp_pop(0,"menu.m2_b_3",0)}}

   3. **(?=p)和(?!p)**

      > 匹配 : p前面的那个位置
      >
      > ```js
      > var result = "hello".replace(/(?=l)/g, '#');
      > 
      > console.log(result);
      > ```
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_1",0)}}
      >
      > ```js
      > var result = "hello".replace(/(?!l)/g, '#');
      > 
      > console.log(result);
      > ```
      >
      > {{"answer" | exp_pop(0,"menu.m2_c_2",0)}}

3. 位置的特性

   > 位置理解空字符

4. 案例

   1. 不匹配任何

      {{"answer" | exp_pop(0,"menu.m4_a_1",0)}}

   2. 数字的千位分隔符表示

      > * 弄出最后一个逗号
      >
      >   {{"answer" | exp_pop(0,"menu.m4_b_1",0)}}
      >
      > * 弄出所有逗号
      >
      >   {{"answer" | exp_pop(0,"menu.m4_b_2",0)}}
      >
      > * 不匹配开头
      >
      >   {{"answer" | exp_pop(0,"menu.m4_b_3",0)}}
      >
      > * 支持其他形式: "12345678 123456789"
      >
      >   {{"answer" | exp_pop(0,"menu.m4_b_4",0)}}

   3. 验证密码问题

      密码长度6-12位，由数字、小写字符和大写字母组成，但必须至少包括2种字符。

      > 1. 不考虑2种字符
      >
      >    {{"answer" | exp_pop(0,"menu.m4_c_1",0)}}
      >
      > 2. 判断是否包含有某一种字符
      >
      >    {{"answer" | exp_pop(0,"menu.m4_c_2",0)}}
      >
      > 3. 同时包含具体两种字符
      >
      >    {{"answer" | exp_pop(0,"menu.m4_c_3",0)}}
      >
      > 4. 用另一种方法解答: (?!p)
      >
      >    {{"answer" | exp_pop(0,"menu.m4_c_4",0)}}

# 疑问

1. > var obj = "12345567";
   >
   > console.log(obj.replace(/(?=(\d{3})+$)/g, ',')) 
   >
   > console.log(obj.replace(/(?=(\d{3})+)/g, ',')) 
   >
   > console.log(obj.replace(/(?=(\d{3})$)/g, ',')) 
   >
   > console.log(obj.replace(/(?=(\d{3}))/g, ',')) 
   >
   > //后面三个都能理解,就是第一个理解不了. 为什么$不像第三个一样代表当前行的最末尾?

2. > \/.^\/ 这个正则有什么意义?

3. > /(?=.*[0-9])^[0-9A-Za-z]{6,12}$/;
   > 这里面的脱字节有什么含义?

4. > (?=.*[0-9])^  为什么不代表第一个开头?  为什么/^a/就代表第一个开头而不是中间的开始? 

   ps: 已在知乎请教作者,等待回复中.