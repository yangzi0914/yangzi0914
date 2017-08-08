---
title: 正则表达式
---
### 1、简介
>   正则表达式：要检索某个文本的时候，可以使用一种模式对这个文本的内容进行解析，这个模式可以是一个单独的字符，也可以是一系列复杂的字符，可以实现对文本内容的解析、校验、替换等功能。RegExp是正则表达式的缩写。

### 2、创建正则表达式对象
1.构造函数法  
````javascript
var parrent = new RegExp("box", "gi");
````
2.字面量法  
````javascript
var parrent = /box/gi;  //该变量下文将继续使用
````

### 3、正则表达式的方法
###### 1、test()
````javascript
var str = "this is a Box box box";  //该变量下文将继续使用
parrent.test(str);
````
**功能**：查找参数字符串中是否存在正则表达式所写的模式规则  
**参数**：要检索的字符串。  
**返回值**：布尔值，true表示找到符合该模式的字符串，false表示未找到。  
**注意**：*这个方法只要找到匹配模式中的规则，就立即返回true，就不会再往下找了，所以这个方法 全局模式匹配'g' 无效*
###### 2、exec()
````javascript
parrent.exec(str);
````
**功能**：查找参数字符串中是否存在正则表达式所描述的模式规则。  
**参数**：要检索的字符串。  
**返回值**：数组或者null，不存在则返回null；存在的话返回的是数组，该数组的第0个元素存放的是匹配文本，除了常规的数组元素之外，返回的数组还含有两个对象属性。index 属性声明的是匹配文本的起始字符在str中的位置，input属性声明的是对str的引用。

**注意**：  
*如果正则表达式的模式修饰符写成"g"，exec()的工作原理：找到第一个匹配的字符串，并存储它所在的位置（下标），如果再次运行exec()检索同一个字符串的话，则从刚才存储的位置开始检索，并找到下一个匹配到的字符串，然后把该字符串的位置存储起来，以此类推。当检索到结果为null的时候，下一次在调用exec()方法时，会从头开始。*  
*使用test()方法检索同一个字符串的话，也会对位置进行存储，所以当test()和exec()方法混合使用的时候，要注意。*  
*如果正则表达式的模式修饰符没有用"g"，则每次都是从头开始查找，返回的是第一次查找到的位置。*
````javascript
//指定一个模式，给一个字符串，打印出符合这个模式的字符串的每一个位置
var myStr = "Ligth of my life of Fire fire fire fire fire";
var myParrent = new RegExp("fire", "gi");

while (true) {
	var ret = myParrent.exec(myStr);
	if (ret == null) {
		break;
	}
	console.log(ret);
	console.log(ret.index);
}
````
###### 3、compile()
````javascript
parrent.compile("bob");
````
**功能**：用于修改正则表达式模式，也可以修改模式修饰符(可选)。  
**参数**：要替换的模式

### 4.与正则相关的字符串方法
正则表达式也可以作为字符串的部分方法的参数
###### 1.match()
````javascript
str.match(/box/gi);
````
**功能**：在字符串内检索指定的子字符串，或找到一个或多个正则表达式的匹配。该方法类似 indexOf()，但是它返回指定的子串，而不是子串开始的位置。  
**参数**：指定的子串或者正则表达式  
**返回值**：数组或者null，找到匹配的字符串则返回数组，数组的内容依赖于参数regexp是否具有全局标志g。如果有g，数组内容为所有匹配的子串，如果没有g，则返回的数组与前面exec()方法返回的数组一样，第0个元素存放的是匹配文本，并包含index属性和input属性。  

###### 2.search()
````javascript
str.search(/B0x/gi);
````
**功能**：用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。  
**参数**：指定的子串或者正则表达式  
**返回值**：找到返回子串开始位置的下标，没有找到返回-1  
**注意**：*"g"修饰符无用，和前面test()方法原理一样*

###### 3.repalce()
````javascript
str.replace(/box/g, "tom");
````
**功能**：用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。 
**参数**：参数1：被替换的子串或者正则表达式；参数2：新子串  
**返回值**：替换后新生成的字符串（源字符串不变）

###### 4.split()
````javascript
str.split(/box/g);
````
**功能**：用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。  
**参数**：参数1：切割点字符串或正则表达式；参数2：(可选)返回的数组的最大长度，不指定则整个字符串都会被切割  
**返回值**：数组，数组元素为切割好的子串

### 4、正则表达式元字符
###### 1.转义字符
\ 将下一个字符转换成为一个特殊字符或一个原义字符。例如'n'匹配原义字符"n"。'\n'匹配特殊字符换行符; "[]"匹配特殊字符[],而"\[\]"则匹配原义字符"[]"。  
'\\' 这个字符很特殊，在字符串也需要转义。用 '\\\\'表示。
````javascript
var str = "[ this is \\ a chr";
console.log(str);
````

###### 2.单个字符
元字符 | 匹配内容
---|---
. | 匹配除换行符外的任意字符
[a-z0-9] | []是字符集合，表示匹配方括号中所包含的任意一个字符, -表示字符范围。匹配指定范围内的任意一个字符. 这里表示匹配a到z或0到9(即所有的小写字母或数字)中的任意一个字符
[^a-z0-9] | []中的^(脱字符)表示非,这里表示匹配除了a-z和0-9(即除了所有的小写字母或数字)以外的任意一个字符
[\u4e00-\u9fa5] | 匹配汉字
\d | 匹配数字,效果同[0-9]
\D | 匹配非数字,效果同[^0-9]
\w | 匹配数字,字母,下划线,效果同[0-9a-zA-Z_]
\W | 匹配非数字,字母,下划线,效果同[^0-9a-zA-Z_]
\s | 匹配任何空白字符，包括空格、换页符、换行符、回车符、制表符等等。等价于[ \f\n\r\t]。
\S | 匹配非空字符,等价于[^ \f\n\r\t]

###### 3.锚字符
元字符 | 匹配内容
---|---
^ | 行首匹配,和在[]字符集和中的 ^ 不是一个意思。
$ | 行尾匹配

###### 4.多个字符
元字符 | 匹配内容
---|---
(xyz) | 整组匹配，这里代表匹配xyz这组符串。
x? | 匹配0个或1个x
x* | 匹配0个或任意多个x
x+ | 匹配至少一个x
x{n} | 匹配确定的n个x(n是一个非负整数)
x{n,} | 匹配至少n个x(n是一个非负整数)
x{n,m} | 匹配至少n个,最多m个x(n是一个非负整数)
x\|y | \| 表示或,这里代表匹配x或y
**贪婪模式下尽可能多的匹配，元字符后面跟?表示非贪婪模式，非贪婪模式下尽可能少的重复**  
* x*? 匹配x任意次，但尽可能少匹配---例如/x.*i/.exec('xiaoyangzi123'),匹配'xi',而/x.*i/.exec('xiaoyangzi123'),匹配'xiaoyangzi' 
* x+? 匹配1次或更多次，但尽可能少匹配---例如/x.+?a/.exec('xiaoyangzi123')匹配'xia',而/x.+a/.exec('xiaoyangzi123')匹配'xiaoya'，但/x.+?i/.exec('xiaoyangzi123')依然匹配'xiaoyangzi'，因为至少需要匹配1次

* x?? 匹配x0次或1次，但尽可能少匹配(以下不再举例)
* x{n,m}? 匹配x n到m次，但尽可能少匹配
* x{n,}? 匹配x n次以上，但尽可能少匹配

###### 5.整组匹配进阶
元字符 | 匹配内容
---|---
(xyz) | 匹配xyz,并捕获文本到自动命名($1,$2...)的组里
(?:xyz) | 匹配xyz,不捕获匹配的文本，也不给此分组分配组号(即$1,$2..取不到该组)
a(?=xyz) | 匹配xyz前面的位置的a---例如/(\S(?=\d{3}))/.exec('xiaoyangzi123')，匹配到'i'，RegExp.$1为'i'
a(?!xyz) | 匹配后面跟的不是xyz的a---例如/\d+(?!\.)/.exec('3.141')匹配"141"而不是"3.141"

### 5、正则表达式应用demo
注册页面信息验证
: * 账号长度在6-16之间，只能由数字、字母、下划线组成；首字母不能是数字
: * 密码长度必须在6-12之间；不允许出现空白字符
: * 邮箱首字符不能是数字, 用户名由字母数字下划线组成的163或qq或126邮箱  
: * 邮编必须是6位数字  
: * 电话必须是1开头的11位数字
````html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8"/>
        <title>注册页面验证</title>
        <script type="text/javascript">
            window.onload = function(){
                $("user").onfocus = function(){
                    $("u").innerHTML = "长度在6-16之间,只能由数字/字母/下划线组成;首字母不能是数字";
    			}
                $("user").onblur = function(){
                    var parrent1 = /^[a-z_]\w{5,15}$/i;
                    if( parrent1.test($("user").value) ){
                        $("u").innerHTML = "输入正确!"
                    }else{
                        $("u").innerHTML = "输入错误!"
                    }
                }
                $("pwd").onfocus = function(){
                    $("p").innerHTML = "长度必须在6-12之间,不允许出现空白字符";
                }
                $("pwd").onblur = function(){
                    var parrent2 = /^\S{6,12}$/;
                    if( parrent2.test($("pwd").value) ){
                        $("p").innerHTML = "输入正确！"
                    }else{
                        $("p").innerHTML = "输入错误！"
                    }
                }
                $("email").onfocus = function(){
                    $("e").innerHTML = "首字符不能是数字, 用户名由字母数字下划线组成的163或qq或126邮箱";
                }
                $("email").onblur = function(){
                    var parrent3 = /^[a-z_]\w*(@163\.com|@qq\.com|@126\.com)$/i;
                    if( parrent3.test($("email").value) ){
                        $("e").innerHTML = "输入正确！";
                    }else{
                        $("e").innerHTML = "输入错误！";
                    }
                }
                $("you").onfocus = function(){
                    $("y").innerHTML = "必须是6位数字";
                }
                $("you").onblur = function(){
                    var parrent4 = /^\d{6}$/;
                    if( parrent4.test($("you").value) ){
                        $("y").innerHTML = "输入正确！"
                    }else{
                        $("y").innerHTML = "输入错误！"
                    }
                }
                $("tel").onfocus = function(){
                    $("t").innerHTML = "必须是11位数字，开头必须是1";
                }
                $("tel").onblur = function(){
                    var parrent5 = /^1\d{10}$/;
                    if( parrent5.test($("tel").value) ){
                        $("t").innerHTML = "输入正确！";
                    }else{
                        $("t").innerHTML = "输入错误！";
                    }
                }
            }
            
            function $ (idName) {
                return document.getElementById(idName);
            }
        </script>
    </head>
    <body>
    	账号<input type="text" id="user" placeholder="请输入用户名"/><span id="u"></span><br/>
    	密码<input type="password" id="pwd" placeholder="请输入密码"/><span id="p"></span><br/>
    	邮箱<input type="text" id="email" placeholder="请输入邮箱"/><span id="e"></span><br/>
    	邮编<input type="text" id="you" placeholder="请输邮编"/><span id="y"></span><br/>
    	电话<input type="text" id="tel" placeholder="请输入电话号码"/><span id="t"></span><br/>
    </body>
</html>
````
