# 正则编程

<script>
     var menu = {
         "m1_1_1":" //indexof和search的区别是,indexof有两个参数,且不接受正则. 而search只接受正则.<br>//stringObject.indexOf(searchvalue,fromindex) 返回-1 或者idx下标<br>var res = 'asdf123'.indexOf(/\d/);<br>console.log(res);",
         "m1_1_2":"var res = 'asdf'.search(/\d/);//字符串方法<br>console.log(!!~res)//search 返回-1 或者idx下标. 取反运算得到的是-(x+1).",
         "m1_1_3":"var res = /\d/.test('123asdf');//正则方法, 最常用<br>console.log(res); //返回true或者false",
         "m1_1_4":"var res = 'asdf123'.match(/\d/);//字符串方法<br>console.log(res); //返回数组或者null, 带g的时候返回所有匹配数组.",
         "m1_1_5":"var res = /\d/g.exec('asdf123');//正则方法<br>console.log(res); //返回数组或者null, 带g的时候和不带g返回一致.",
         "m1_3_1":'//match 最常用<br>var str = "2017-06-21";<br>var reg = /^(\d{4})-(\d{2})-(\d{2})$/<br>var res = str.match(reg);<br>console.log(res); // 数组 <br>console.log(res[1]) //2017',
         "m1_3_2":'var str = "2017-06-21";<br>var reg = /^(\d{4})-(\d{2})-(\d{2})$/<br>var res = reg.exec(str);<br>console.log(res); // 数组 <br>console.log(res[1]) //2017',
         "m1_3_3":'var reg = /^(\d{4})-(\d{2})-(\d{2})/<br>var str = "2017-06-21";<br>console.log(reg.test(str))  <br>console.log(RegExp.$1)',
         "m1_3_4":"参考test",
         "m1_3_5":'var reg = /^(\d{4})-(\d{2})-(\d{2})/<br>varstr = "2017-06-21";<br>var arr = []<br>str.replace(reg, function(match, year, month, day){<br>\\t arr.push(year, month, day)<br>})<br>console.log(arr);'
     }
</script>

| 方法      | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| `exec`    | 一个在字符串中执行查找匹配的RegExp方法，它返回一个数组（未匹配到则返回null）。 |
| `test`    | 一个在字符串中测试是否匹配的RegExp方法，它返回true或false。  |
| `match`   | 一个在字符串中执行查找匹配的String方法，它返回一个数组或者在未匹配到时返回null。 |
| `search`  | 一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者在失败时返回-1。 |
| `replace` | 一个在字符串中执行查找匹配的String方法，并且使用替换字符串替换掉匹配到的子字符串。 |
| `split`   | 一个使用正则表达式或者一个固定字符串分隔一个字符串，并将分隔后的子字符串存储到数组中的String方法。 |

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

## 1: 正则表达式的四种操作

1. 匹配(查找\验证)

   > - {{"indexof" | exp_pop(0,"menu.m1_1_1",0)}}
   > - {{"search" | exp_pop(0,"menu.m1_1_2",0)}}
   > - {{"test-常用" | exp_pop(0,"menu.m1_1_3",0)}}
   > - {{"match" | exp_pop(0,"menu.m1_1_4",0)}}
   > - {{"exec" | exp_pop(0,"menu.m1_1_5",0)}}

2. 切分

   * split

3. 提取

   * {{"match-常用" | exp_pop(0,"menu.m1_3_1",0)}}
   * {{"exec" | exp_pop(0,"menu.m1_3_2",0)}}
   * {{"test" | exp_pop(0,"menu.m1_3_3",0)}}
   * {{"search" | exp_pop(0,"menu.m1_3_4",0)}}
   * {{"replace" | exp_pop(0,"menu.m1_3_5",0)}}

4. 替换

   * 一般使用replace

## 2: 相关api的注意要点

* search和match的参数问题

  > 我们知道字符串实例的那4个方法参数都支持正则和字符串。
  >
  > 但search和match，会把字符串转换为正则的。
  >
  > 转成以下两种模式
  >
  > string.search(/\./)
  > string.search("\\.")

* match格式(加G和不加G)

  ```js
  var string = "2017.06.27";
  var regex1 = /\b(\d+)\b/;
  var regex2 = /\b(\d+)\b/g;
  console.log( string.match(regex1) );
  console.log( string.match(regex2) );
  // => ["2017", "2017", index: 0, input: "2017.06.27"]
  // => ["2017", "06", "27"]
  ```

* exec和match的比较

  有G的时候, exec能接着上一次匹配后继续匹配, 一般用作while循环

  ```js
  var string = "2017.06.27";
  var reg = /\b\d+\b/g;
  var result 
  while (result = reg.exec(string)) {
    console.log(result, reg.lastIndex);
  }
  ```

* g对exec和test的影响

  **字符串的四个方法,都没问题.  正则的两个方法,都有问题,慎用!!!!**

  **有g的时候, test慎用!!!** 

  **test会记录lastIndex**

  ```javascript
  var regex = /a/g;
  console.log( regex.test("a"), regex.lastIndex );
  console.log( regex.test("aba"), regex.lastIndex );
  console.log( regex.test("ababc"), regex.lastIndex );
  ```

* split相关注意

  ```javascript
  var str = 'html,java,css'
  console.log(str.split(/,/, 2))//可以有长度限制
  
  console.log(str.split(/,/)) 
  console.log(str.split(/(,)/))//有分组的时候,结果数组中是包含分隔符的
  console.log(str.split(/(?:,)/))
  
  //[ 'html', 'java' ]
  //[ 'html', 'java', 'css' ]
  //[ 'html', ',', 'java', ',', 'css' ]
  //[ 'html', 'java', 'css' ]
  ```

* replace的强大

  > $1,$2,...,$99 匹配第1~99个分组里捕获的文本
  > $& 匹配到的子串
  > $` 匹配到的子串的左边文本
  > $' 匹配到的子串的右边文本
  > $$ 美元符号

  把"2,3,5"，变成"5=2+3"

  ```js
  "2,3,5".replace(/(\d+),(\d+),(\d+)/, "$3=$1+$2")
  ```

  把"2,3,5"，变成"222,333,555":

  ```js
  "2,3,5".replace(/(\d+),(\d+),(\d+)/, "$3=$1+$2")
  ```

  把"2+3=5"，变成"2+3=2+3=5=5":

  ```js
  "2+3=5".replace(/=/, "$&$`$&$'$&");
  ```

* 构造函数多用字面量

  ```js
  var string = "2017-06-27 2017.06.27 2017/06/27";
  var reg = new RegExp("\\d{4}(\-|\_|\.)\\d{2}\\1\\d{2}","g");
  console.log(string.match(reg));
  ```

* 私有属性

  > var regex = /\w/img;
  >
  > console.log(regex.global)//true
  >
  > console.log( regex.ignoreCase );//true
  >
  > console.log( regex.multiline );//true
  >
  > console.log(regex.source)//\w





## 3: 真实案例



