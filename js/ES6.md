1.简介
    ecmascript5.1版本之后的版本统称为es6，es6于2015年发布。
    es2015指2015年发布的ecmascript标准，每年发布完一版之后，会继续讨论下一版的内容，在明年同一时候发布，称为es2016...es2017...等，这些版本统称为es6，其实更像6.1，6.2...
2.let和const
    let 
        声明的变量只有在let当前行所在的代码块内有效，即新增块级作用域：以花括号包裹，for/if使用花括号的情况都是块级作用域

        不存在变量提升的情况，变量提升指的是在声明之前就可以调用，只是值为undefined，这是var定义变量的情况。let使用必须在声明之后，否则报错。

        块级作用域+无变量提升=>暂时性死区：如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错，即不可用。

        不允许重复声明
    块级作用域
        出现理由；
            1.内层变量上升覆盖外层变量
            2.for循环中循环数泄露为全局变量
        ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域
    const
        声明常量，一旦声明，该常量值则不能改变。
            常量 普通类型 不允许改变值
                引用类型 不允许改变地址，可以改变值
    六种变量声明方法；
        ES5 只有两种声明变量的方法：var命令和function命令。ES6 除了添加let和const命令，后面章节还会提到，另外两种声明变量的方法：import命令和class命令。所以，ES6 一共有 6 种声明变量的方法。
3.变量的解构赋值
    数组解构赋值
        变量以数组的形式放在等式左边，右边是要给左边变量赋值的数组，下标对应的变量和值即可赋值成功，格式如下：
        let [a, b, c] = [1, 2, 3];
        本质是“模式匹配”，只要等式两边模式相同，即可对应匹配

        解构失败，变量的值为undefined
            如果等式右边不是数组（或对象，是不可遍历的结构，或者本身就不具备Iterator接口），则解构失败
        解构不完全 即等号左边的模式，只匹配一部分的等号右边的数组

        解构赋值允许指定默认值。
            ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined（右边数组对应位置没有值或者值为undefined），默认值才会生效。
    对象解构赋值
        变量以对象的形式放在等式左边，右边是要给左边变量赋值的对象，变量名与对象key对应即可赋值成功
        格式：let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
        实质格式：let { foo:foo1, bar:bar1 } = { foo: 'aaa', bar: 'bbb' },foo1、bar1被赋值成功，而非foo和bar
        经典：let { log, sin, cos } = Math;
    字符串解构赋值
        先转化为对象，然后属性进行解构（length也是一个属性）
    数字和布尔
        先转化为对象
    函数参数

    尽量不要使用圆括号

    用途：
        1.交换变量的值
            let x = 1
            let y = 2
            [x,y] = [y,x]
        2.从对象和数组中提取值
            函数多个返回值
            json
            函数参数

4.字符串扩展
    字符的表示方法：字符串形式引号内直接表示  转义表示

    转义表示一个字符的六种方法如下：
        '\z' === 'z'  // true
        '\172' === 'z' // true
        '\x7A' === 'z' // true
        '\u007A' === 'z' // true
        '\u{7A}' === 'z' // true es6新增，可以将超过4位的码点（大于0xFFFF的码点）放入大括号进行解析

    字符串新增遍历器接口，可以使用for...of遍历字符串（可以很好识别大于0xFFFF的码点）

    模版字符串 放在反引号内（`）
        可以当作单行字符串/多行字符串使用
        可以中间放入变量/表达式 ${} 

    标签模版 标签指函数 模版指模版，作参数
        let a = 5;
        let b = 10;

        tag`Hello ${ a + b } world ${ a * b }`;
        // 等同于
        tag(['Hello ', ' world ', ''], 15, 50);
    （细节暂且不纠）
5.字符串新增方法
    string.fromCodePoint() 将unicode码点转化为字符串
        fromCharCode() 无法识别unicode码点大于0xFFFF，string.fromCodePoint()可以
        string.fromCodePoint()传入多个参数，会被合并返回一个字符串

    String.raw() 该方法返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，往往用于模板字符串的处理方法

    str.codePointAt() 实例方法，不是String对象方法
        charAt() 返回字符串中指定位置的字符串（指定位置的字符）
        charCodeAt() 返回指定位置的字符的unicode编码（不能很好处理四个字节的字符，即大于0xFFFF的码点，只能分别返回前两个字节和后两个字节的值）
        codePointAt() codePointAt(0)可以很好的返回四个字节的字符unicode编码十进制码点，通过toString()可以转为16进制

        字符是2字节还是4字节判断：
            根据一个字符unicode编码不同，会有需要2个或者4个字节进行存储，码点大于0xFFFF，则需要32位存储，即四个字节。可以通过codePointAt()方法进行判断：
                function is32Bit(c) {
                    return c.codePointAt(0) > 0xFFFF;
                }
        
        codePointAt(0)拿到十进制，codePointAt(1)拿到四字节的第二个两字节，会有一定的错误，for...of.../...运算符可以很好的拿到

    normalize()

    includes(), startsWith(), endsWith() 实例方法，判断字符串中是否含有一个字串
        includes()：返回布尔值，表示是否找到了参数字符串
        startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部
        endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部

    repeat(num) 实例方法，表示将字符串复制几次，返回复制拼接后的字符串
        num若为小数，则向下取整
           若为负数或者Infinity，会报错
           若为NaN等同于 0
           若为字符串，先转化为数字

    padStart(max,str)，padEnd() 实例方法 字符串补全长度，果某个字符串不够指定长度，会在头部或尾部补全
        一共接受两个参数，第一个参数是字符串补全生效的最大长度，第二个参数是用来补全的字符串。

        padStart()的常见用途:
            为数值补全指定位数
                '1'.padStart(10, '0') // "0000000001"
            另一个用途是提示字符串格式。
                '09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"

    trimStart()，trimEnd() 实例方法 消除字符串头部/尾部的空格

    matchAll() 实例方法，返回一个符合指定正则表达式的字符串
6.数字新增方法
    二进制和八进制新增表示法
        分别用前缀0b（或0B）和0o（或0O）表示
    Number.isFinite(), Number.isNaN() 
        用来检查一个数值是否为有限的（finite），即不是Infinity
            如果参数类型不是数值，Number.isFinite一律返回false
        用来检查一个值是否为NaN
            如果参数类型不是NaN，Number.isNaN一律返回false
    Number.parseInt(), Number.parseFloat() 全局方法移到Number对象上，减少全局函数，作用相同
    Number.isInteger() 判断一个数值是否为整数
        js数值存储采用64位双精度格式（整数也是，所以1和1.0相等），数值精度最多可以达到 53 个二进制位（1 个隐藏位与 52 个有效位），如果数值的精度超过这个限度，第54位及后面的位就会被丢弃，此时isInteger()可能误判（超过则舍弃）
    Number.EPSILON 极小常量 1.00..001 误差如果小于这个值，就可以认为已经没有意义了，即不存在误差了。可以用于误差判断。
        function withinErrorMargin (left, right) {
            return Math.abs(left - right) < Number.EPSILON * Math.pow(2, 2);
        }
    安全整数和 Number.isSafeInteger()

    Math 对象的扩展
        Math.trunc() 去掉浮点数的小数部分
        Math.sign() 判断一个数是正数、负数或者0
        其他略
    
    指数运算符 （**）右结合，从右往左算
        2 ** 2 // 4
        2 ** 3 // 8

        赋值运算符（**=）
        let b = 4;
        b **= 3;
        // 等同于 b = b * b * b;
    Math.pow(x,y)
        返回 x 的 y 次幂的值（v8引擎在数大时会两者值会有差别）



