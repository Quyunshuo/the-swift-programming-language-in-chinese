# 语法总结
完整语法一览。

## 词法结构

> 空白符语法：
>
> *空白符* → *空白符项* *空白符*可选 \
> *空白符项* → *换行符* \
> *空白符项* → *行内空格* \
> *空白符项* → *注释* \
> *空白符项* → *多行注释* \
> *空白符项* → U+0000, U+000B, 或 U+000C
>
> *换行符* → U+000A \
> *换行符* → U+000D \
> *换行符* → U+000D 后接 U+000A
>
> *行内空格* → *行内空格符* *行内空格*可选 \
> *行内空格符* → U+0009 或 U+0020
>
> *注释* → **`//`** *注释文本* *换行符* \
> *多行注释* → **`/*`** *多行注释文本* **`*/`**
>
> *注释文本* → *注释文本项* *注释文本*可选 \
> *注释文本项* → 除 U+000A 或 U+000D 外的任意 Unicode 标量值
>
> *多行注释文本* → *多行注释文本项* *多行注释文本*可选 \
> *多行注释文本项* → *多行注释* \
> *多行注释文本项* → *注释文本项* \
> *多行注释文本项* → 除 **`/*`** 或 **`*/`** 外的任意 Unicode 标量值

> 标识符语法：
>
> *标识符* → *标识符头（Head）* *标识符字符集*可选 \
> *标识符* → **`` ` ``** *标识符头（Head）* *标识符字符集*可选 **`` ` ``** \
> *标识符* → *隐式参数名* \
> *标识符* → *属性包装器呈现值* \
> *标识符集* → *标识符* | *标识符* **`,`** *标识符集*
>
> *标识符头（Head）* → A 到 Z 的大写或小写字母 \
> *标识符头（Head）* → **`_`** \
> *标识符头（Head）* → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, 或 U+00B7–U+00BA \
> *标识符头（Head）* → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, 或 U+00F8–U+00FF \
> *标识符头（Head）* → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, 或 U+180F–U+1DBF \
> *标识符头（Head）* → U+1E00–U+1FFF \
> *标识符头（Head）* → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, 或 U+2060–U+206F \
> *标识符头（Head）* → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, 或 U+2776–U+2793 \
> *标识符头（Head）* → U+2C00–U+2DFF 或 U+2E80–U+2FFF \
> *标识符头（Head）* → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, 或 U+3040–U+D7FF \
> *标识符头（Head）* → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, 或 U+FE30–U+FE44 \
> *标识符头（Head）* → U+FE47–U+FFFD \
> *标识符头（Head）* → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, 或 U+40000–U+4FFFD \
> *标识符头（Head）* → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, 或 U+80000–U+8FFFD \
> *标识符头（Head）* → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, 或 U+C0000–U+CFFFD \
> *标识符头（Head）* → U+D0000–U+DFFFD 或 U+E0000–U+EFFFD
>
> *标识符字符* → 数字 0 到 9 \
> *标识符字符* → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, 或 U+FE20–U+FE2F \
> *标识符字符* → *标识符头（Head）* \
> *标识符字符集* → *标识符字符项* *标识符字符集*可选
>
> *隐式参数名* → **`$`** *十进制数字* \
> *属性包装器呈现值* → **`$`** *标识符字符集*

> 字面量语法：
>
> *字面量* → *数字字面量* | *字符串字面量* | *正则表达式字面量* | *布尔字面量* | *空字面量*
>
> *数字字面量* → **`-`** 可选 *整型字面量* | **`-`** 可选 *浮点型字面量* \
> *布尔字面量* → **`true`** | **`false`** \
> *空字面量* → **`nil`**

> 整型字面量语法：
>
> *整型字面量* → *二进制字面量* \
> *整型字面量* → *八进制字面量* \
> *整型字面量* → *十进制字面量* \
> *整型字面量* → *十六进制字面量*
>
> *二进制字面量* → **`0b`** *二进制数字* *二进制字面量字符* 可选 \
> *二进制数字* → 数字 0 或 1 \
> *二进制字面量字符* → *二进制数字* | **`_`** \
> *二进制字面量字符* → *二进制字面量字符* *二进制字面量字符* 可选
>
> *八进制字面量* → **`0o`** *八进制数字* *八进制字面量字符* 可选 \
> *八进制数字* → 数字 0 到 7 \
> *八进制字面量字符* → *八进制数字* | **`_`** \
> *八进制字面量字符* → *八进制字面量字符* *八进制字面量字符* 可选
>
> *十进制字面量* → *十进制数字* *十进制字面量字符* 可选 \
> *十进制数字* → 数字 0 到 9 \
> *十进制数字* → *十进制数字* *十进制数字* 可选 \
> *十进制字面量字符* → *十进制数字* | **`_`** \
> *十进制字面量字符* → *十进制字面量字符* *十进制字面量字符* 可选
>
> *十六进制字面量* → **`0x`** *十六进制数字* *十六进制字面量字符* 可选 \
> *十六进制数字* → 数字 0 到 9，a 到 f，或 A 到 F \
> *十六进制字面量字符* → *十六进制数字* | **`_`** \
> *十六进制字面量字符* → *十六进制字面量字符* *十六进制字面量字符* 可选

> 浮点型字面量语法：
>
> *浮点型字面量* → *十进制字面量* *十进制分数* 可选 *十进制指数* 可选 \
> *浮点型字面量* → *十六进制字面量* *十六进制分数* 可选 *十六进制指数*
>
> *十进制分数* → **`.`** *十进制字面量* \
> *十进制指数* → *浮点数 e* *正负号* 可选 *十进制字面量*
>
> *十六进制分数* → **`.`** *十六进制数字* *十六进制字面量字符* 可选 \
> *十六进制指数* → *浮点数 p* *正负号* 可选 *十进制字面量*
>
> *浮点数 e* → **`e`** | **`E`** \
> *浮点数 p* → **`p`** | **`P`** \
> *正负号* → **`+`** | **`-`**

> 字符串字面量语法：
>
> *字符串字面量* → *静态字符串字面量* | *插值字符串字面量*
>
> *字符串开分隔定界符* → *字符串扩展分隔符* 可选 **`"`** \
> *字符串闭分隔定界符* → **`"`** *字符串扩展分隔符* 可选
>
> *静态字符串字面量* → *字符串开分隔定界符* *引用文本* 可选 *字符串闭分隔定界符* \
> *静态字符串字面量* → *多行字符串开分隔定界符* *多行引用文本* 可选 *多行字符串闭分隔定界符*
>
> *多行字符串开分隔定界符* → *字符串扩展分隔符* 可选 **`"""`** \
> *多行字符串闭分隔定界符* → **`"""`** *字符串扩展分隔符* 可选 \
> *字符串扩展分隔符* → **`#`** *字符串扩展分隔符* 可选
>
> *引用文本* → *引用文本项* *引用文本* 可选 \
> *引用文本项* → *转义字符* \
> *引用文本项* → 任何 Unicode 标量值，除了 **`"`**、**`\`**、U+000A 或 U+000D
>
> *多行引用文本* → *多行引用文本项* *多行引用文本* 可选 \
> *多行引用文本项* → *转义字符* \
> *多行引用文本项* → 任何 Unicode 标量值，除了 **`\`** \
> *多行引用文本项* → *转义换行符*
>
> *插值字符串字面量* → *字符串开分隔定界符* *插值文本* 可选 *字符串闭分隔定界符* \
> *插值字符串字面量* → *多行字符串开分隔定界符* *多行插值文本* 可选 *多行字符串闭分隔定界符*
>
> *插值文本* → *插值文本项* *插值文本* 可选 \
> *插值文本项* → **`\(`** *表达式* **`)`** | *引用文本项*
>
> *多行插值文本* → *多行插值文本项* *多行插值文本* 可选 \
> *多行插值文本项* → **`\(`** *表达式* **`)`** | *多行引用文本项*
>
> *转义序列* → **`\`** *字符串扩展分隔符* \
> *转义字符* → *转义序列* **`0`** | *转义序列* **`\`** | *转义序列* **`t`** | *转义序列* **`n`** | *转义序列* **`r`** | *转义序列* **`"`** | *转义序列* **`'`** \
> *转义字符* → *转义序列* **`u`** **`{`** *unicode-标量-数字* **`}`** \
> *unicode-标量-数字* → 一到八位十六进制数字
>
> *转义换行符* → *转义序列* *内联空格* 可选 *换行符*

> 正则表达式字面量语法：
>
> *正则表达式字面量* → *正则表达式字面量开分隔定界符* *正则表达式* *正则表达式字面量闭分隔定界符* \
> *正则表达式* → 任何正则表达式
>
> *正则表达式字面量开分隔定界符* → *正则表达式扩展分隔符* 可选 **`/`** \
> *正则表达式字面量闭分隔定界符* → **`/`** *正则表达式扩展分隔符* 可选
>
> *正则表达式扩展分隔符* → **`#`** *正则表达式扩展分隔符* 可选

> 运算符语法：
>
> *运算符* → *运算符头* *运算符字符集* 可选 \
> *运算符* → *点运算符头* *点运算符字符集*
>
> *运算符头* → **`/`** | **`=`** | **`-`** | **`+`** | **`!`** | **`*`** | **`%`** | **`<`** | **`>`** | **`&`** | **`|`** | **`^`** | **`~`** | **`?`** \
> *运算符头* → U+00A1–U+00A7 \
> *运算符头* → U+00A9 或 U+00AB \
> *运算符头* → U+00AC 或 U+00AE \
> *运算符头* → U+00B0–U+00B1 \
> *运算符头* → U+00B6、U+00BB、U+00BF、U+00D7 或 U+00F7 \
> *运算符头* → U+2016–U+2017 \
> *运算符头* → U+2020–U+2027 \
> *运算符头* → U+2030–U+203E \
> *运算符头* → U+2041–U+2053 \
> *运算符头* → U+2055–U+205E \
> *运算符头* → U+2190–U+23FF \
> *运算符头* → U+2500–U+2775 \
> *运算符头* → U+2794–U+2BFF \
> *运算符头* → U+2E00–U+2E7F \
> *运算符头* → U+3001–U+3003 \
> *运算符头* → U+3008–U+3020 \
> *运算符头* → U+3030
>
> *运算符字符* → *运算符头* \
> *运算符字符* → U+0300–U+036F \
> *运算符字符* → U+1DC0–U+1DFF \
> *运算符字符* → U+20D0–U+20FF \
> *运算符字符* → U+FE00–U+FE0F \
> *运算符字符* → U+FE20–U+FE2F \
> *运算符字符* → U+E0100–U+E01EF \
> *运算符字符集* → *运算符字符* *运算符字符集* 可选
>
> *点运算符头* → **`.`** \
> *点运算符字符* → **`.`** | *运算符字符* \
> *点运算符字符集* → *点运算符字符* *点运算符字符集* 可选
>
> *中缀运算符* → *运算符* \
> *前缀运算符* → *运算符* \
> *后缀运算符* → *运算符*

## 类型

> 类型语法：
>
> *类型* → *函数类型* \
> *类型* → *数组类型* \
> *类型* → *字典类型* \
> *类型* → *类型标识符* \
> *类型* → *元组类型* \
> *类型* → *可选类型* \
> *类型* → *隐式解析可选类型* \
> *类型* → *协议合成类型* \
> *类型* → *不透明类型* \
> *类型* → *元类型* \
> *类型* → *任意类型* \
> *类型* → *自身类型* \
> *类型* → **`(`** *type* **`)`**

> 类型注释语法：
>
> *类型注释* → **`:`** *属性（Attributes）* 可选 **`inout`** 可选 *类型*

> 类型标识符语法：
>
> *类型标识符* → *类型名* *泛型实参子句* 可选 | *类型名* *泛型实参子句* 可选 **`.`** *类型标识符* \
> *类型名* → *标识符*

> 元组类型语法：
>
> *元组类型* → **`(`** **`)`** | **`(`** *元组类型元素* **`,`** *元组类型元素集* **`)`** \
> *元组类型元素集* → *元组类型元素* | *元组类型元素* **`,`** *元组类型元素集* \
> *元组类型元素* → *元素名* *类型注释* | *类型* \
> *元素名* → *标识符*

> 函数类型语法：
>
> *函数类型* → *属性* 可选 *函数类型子句* **`async`** 可选 *throws* 可选 **`->`** *类型*
>
> *函数类型子句* → **`(`** **`)`** \
> *函数类型子句* → **`(`** *函数类型参数集* **`...`** 可选 **`)`**
>
> *函数类型参数集* → *函数类型参数* | *函数类型参数* **`,`** *函数类型参数集* \
> *函数类型参数* → *属性* 可选 **`inout`** 可选 *类型* | *参数标签* *类型注释* \
> *参数标签* → *标识符*
>
> *throws 子句* → **`throws`** | **`throws`** **`(`** *类型* **`)`**

> 数组类型语法：
>
> *数组类型* → **`[`** *类型* **`]`**

> 字典类型语法：
>
> *字典类型* → **`[`** *类型* **`:`** *类型* **`]`**

> 可选类型语法：
>
> *可选类型* → *类型* **`?`**

> 隐式解析可选类型语法：
>
> *隐式解析可选类型* → *类型* **`!`**

> 协议合成类型语法：
>
> *协议合成类型* → *类型标识符* **`&`** *协议合成延续* \
> *协议合成延续* → *类型标识符* | *协议合成类型*

> 不透明类型语法：
>
> *不透明类型* → **`some`** *类型*

> 被包装的协议类型语法：
>
> *被包装的协议类型* → **`any`** *类型*

> 元类型语法：
>
> *元类型* → *类型* **`.`** **`Type`** | *类型* **`.`** **`Protocol`**

> 任意类型语法：
>
> *任意类型* → **`Any`**

> 自身类型语法：
>
> *自身类型* → **`Self`**

> 类型继承子句语法：
>
> *类型继承子句* → **`:`** *类型继承集* \
> *类型继承集* → *属性* 可选 *类型标识符* | *属性* 可选 *类型标识符* **`,`** *类型继承集*

## 表达式

> 表达式语法：
>
> *表达式* → *try 运算符* 可选 *await 运算符* 可选 *前缀表达式* *中缀表达式* 可选

> 前缀表达式语法：
>
> *前缀表达式* → *前缀运算符* 可选 *后缀表达式* \
> *前缀表达式* → *输入输出表达式*

> 输入输出表达式语法：
>
> *输入输出表达式* → **`&`** *基础表达式*

> try 表达式语法：
>
> *try 运算符* → **`try`** | **`try`** **`?`** | **`try`** **`!`**

> await 表达式语法：
>
> *await 运算符* → **`await`**

> 中缀表达式语法：
>
> *中缀表达式* → *中缀运算符* *前缀表达式* \
> *中缀表达式* → *赋值运算符* *try 运算符* 可选 *await 运算符* 可选 *前缀表达式* \
> *中缀表达式* → *条件运算符* *try 运算符* 可选 *await 运算符* 可选 *前缀表达式* \
> *中缀表达式* → *类型转换运算符* \
> *中缀表达式* → *中缀表达式* *中缀表达式* 可选

> 赋值运算符语法：
>
> *赋值运算符* → **`=`**

> 条件运算符语法：
>
> *条件运算符* → **`?`** *表达式* **`:`**

> 类型转换运算符语法：
>
> *类型转换运算符* → **`is`** *类型* \
> *类型转换运算符* → **`as`** *类型* \
> *类型转换运算符* → **`as`** **`?`** *类型* \
> *类型转换运算符* → **`as`** **`!`** *类型*

> 基础表达式语法：
>
> *基础表达式* → *标识符* *泛型实参子句* 可选 \
> *基础表达式* → *字面量表达式* \
> *基础表达式* → *self 表达式* \
> *基础表达式* → *父类表达式* \
> *基础表达式* → *条件表达式* \
> *基础表达式* → *闭包表达式* \
> *基础表达式* → *圆括号表达式* \
> *基础表达式* → *元组表达式* \
> *基础表达式* → *隐式成员表达式* \
> *基础表达式* → *通配符表达式* \
> *基础表达式* → *宏展开表达式* \
> *基础表达式* → *key-path 表达式* \
> *基础表达式* → *选择器表达式* \
> *基础表达式* → *key-path 字符串表达式*

> 字面量表达式语法：
>
> *字面量表达式* → *字面量* \
> *字面量表达式* → *数组字面量* | *字典字面量* | *playground 字面量*
>
> *数组字面量* → **`[`** *数组字面量项* 可选 **`]`** \
> *数组字面量项* → *数组字面量项* **`,`** 可选 | *数组字面量项* **`,`** *数组字面量项* \
> *数组字面量项* → *表达式*
>
> *字典字面量* → **`[`** *字典字面量项* **`]`** | **`[`** **`:`** **`]`** \
> *字典字面量项* → *字典字面量项* **`,`** 可选 | *字典字面量项* **`,`** *字典字面量项* \
> *字典字面量项* → *表达式* **`:`** *表达式*
>
> *playground 字面量* → **`#colorLiteral`** **`(`** **`red`** **`:`** *表达式* **`,`** **`green`** **`:`** *表达式* **`,`** **`blue`** **`:`** *表达式* **`,`** **`alpha`** **`:`** *表达式* **`)`** \
> *playground 字面量* → **`#fileLiteral`** **`(`** **`resourceName`** **`:`** *表达式* **`)`** \
> *playground 字面量* → **`#imageLiteral`** **`(`** **`resourceName`** **`:`** *表达式* **`)`**

> self 表达式语法：
>
> *self 表达式* → **`self`** | *self 方法表达式* | *self 下标表达式* | *self 构造器表达式*
>
> *self 方法表达式* → **`self`** **`.`** *标识符* \
> *self 下标表达式* → **`self`** **`[`** *函数调用参数表* **`]`** \
> *self 构造器表达式* → **`self`** **`.`** **`init`**

> 父类表达式语法：
>
> *父类表达式* → *父类方法表达式* | *父类下标表达式* | *父类构造器表达式*
>
> *父类方法表达式* → **`super`** **`.`** *标识符* \
> *父类下标表达式* → **`super`** **`[`** *函数调用参数表* **`]`** \
> *父类构造器表达式* → **`super`** **`.`** **`init`**

> 条件表达式语法：
>
> *条件表达式* → *if 表达式* | *switch 表达式*
>
> *if 表达式* → **`if`** *条件集* **`{`** *语句* **`}`** *if 表达式后续* \
> *if 表达式后续* → **`else`** *if 表达式* \
> *if 表达式后续* → **`else`** **`{`** *语句* **`}`**
>
> *switch 表达式* → **`switch`** *表达式* **`{`** *switch表 达式 case* **`}`** \
> *switch 表达式 case* → *switch 表达式 case* *switch 表达式 case* 可选 \
> *switch case 表达式* → *case 标签* *语句* \
> *switch case 表达式* → *default 标签* *语句*

> 闭包表达式语法：
>
> *闭包表达式* → **`{`** *属性* 可选 *闭包签名* 可选 *语句* 可选 **`}`**
>
> *闭包签名* → *捕获列表* 可选 *闭包参数子句* **`async`** 可选 *throws* 可选 *函数结果* 可选 **`in`** \
> *闭包签名* → *捕获列表* **`in`**
>
> *闭包参数子句* → **`(`** **`)`** | **`(`** *闭包参数集* **`)`** | *标识符集* \
> *闭包参数集* → *闭包参数* | *闭包参数* **`,`** *闭包参数集* \
> *闭包参数* → *闭包参数名* *类型注释* 可选 \
> *闭包参数* → *闭包参数名* *类型注释* **`...`** \
> *闭包参数名* → *标识符*
>
> *捕获列表* → **`[`** *捕获列表项* **`]`** \
> *捕获列表项* → *捕获列表项* | *捕获列表项* **`,`** *捕获列表项* \
> *捕获列表项* → *捕获说明符* 可选 *标识符* \
> *捕获列表项* → *捕获说明符* 可选 *标识符* **`=`** *表达式* \
> *捕获列表项* → *捕获说明符* 可选 *self 表达式* \
> *捕获说明符* → **`weak`** | **`unowned`** | **`unowned(safe)`** | **`unowned(unsafe)`**

> 隐式成员表达式语法：
>
> *隐式成员表达式* → **`.`** *标识符* \
> *隐式成员表达式* → **`.`** *标识符* **`.`** *后缀表达式*

> 圆括号表达式语法：
>
> *圆括号表达式* → **`(`** *表达式* **`)`**

> 元组表达式语法：
>
> *元组表达式* → **`(`** **`)`** | **`(`** *元组元素* **`,`** *元组元素集* **`)`** \
> *元组元素集* → *元组元素* | *元组元素* **`,`** *元组元素集* \
> *元组元素* → *表达式* | *标识符* **`:`** *表达式*

> 通配符表达式语法：
>
> *通配符表达式* → **`_`**

> 宏展开表达式语法：
>
> *宏展开表达式* → **`#`** *标识符* *泛型参数子句* 可选 *函数调用参数子句* 可选 *尾随闭包* 可选

> key-path 表达式语法：
>
> *key-path 表达式* → **`\`** *类型* 可选 **`.`** *key-path 组件* \
> *key-path 组件* → *key-path 组件* | *key-path 组件* **`.`** *key-path 组件* \
> *key-path 组件* → *标识符* *key-path 后缀* 可选 | *key-path 后缀*
>
> *key-path 后缀* → *key-path 后缀* *key-path 后缀* 可选 \
> *key-path 后缀* → **`?`** | **`!`** | **`self`** | **`[`** *函数调用参数集* **`]`**

> 选择器表达式语法：
>
> *选择器表达式* → **`#selector`** **`(`** *表达式* **`)`** \
> *选择器表达式* → **`#selector`** **`(`** **`getter:`** *表达式* **`)`** \
> *选择器表达式* → **`#selector`** **`(`** **`setter:`** *表达式* **`)`**

> key-path 字符串表达式语法：
>
> *key-path 字符串表达式* → **`#keyPath`** **`(`** *表达式* **`)`**

> 后缀表达式语法：
>
> *后缀表达式* → *基本表达式* \
> *后缀表达式* → *后缀表达式* *后缀运算符* \
> *后缀表达式* → *函数调用表达式* \
> *后缀表达式* → *构造器表达式* \
> *后缀表达式* → *显式成员表达式* \
> *后缀表达式* → *后缀 self 表达式* \
> *后缀表达式* → *下标表达式* \
> *后缀表达式* → *强制取值表达式* \
> *后缀表达式* → *可选链式表达式*

> 函数调用表达式语法：
>
> *函数调用表达式* → *后缀表达式* *函数调用参数子句* \
> *函数调用表达式* → *后缀表达式* *函数调用参数子句* 可选 *尾随闭包*
>
> *函数调用参数子句* → **`(`** **`)`** | **`(`** *函数调用参数集* **`)`** \
> *函数调用参数集* → *函数调用参数* | *函数调用参数* **`,`** *函数调用参数集* \
> *函数调用参数* → *表达式* | *标识符* **`:`** *表达式* \
> *函数调用参数* → *运算符* | *标识符* **`:`** *运算符*
>
> *尾随闭包* → *闭包表达式* *带标签的尾随闭包* 可选 \
> *带标签的尾随闭包* → *带标签的尾随闭包* *带标签的尾随闭包* 可选 \
> *带标签的尾随闭包* → *标识符* **`:`** *闭包表达式*

> 构造器表达式语法：
>
> *构造器表达式* → *后缀表达式* **`.`** **`init`** \
> *构造器表达式* → *后缀表达式* **`.`** **`init`** **`(`** *参数名* **`)`**

> 显式成员表达式语法：
>
> *显式成员表达式* → *后缀表达式* **`.`** *十进制数字* \
> *显式成员表达式* → *后缀表达式* **`.`** *标识符* *泛型参数子句* 可选 \
> *显式成员表达式* → *后缀表达式* **`.`** *标识符* **`(`** *参数名* **`)`** \
> *显式成员表达式* → *后缀表达式* *条件编译块*
>
> *参数名* → *参数名* *参数名* 可选 \
> *参数名* → *标识符* **`:`**

> 后缀 self表达式语法：
>
> *后缀 self 表达式* → *后缀表达式* **`.`** **`self`**

> 下标表达式语法：
>
> *下标表达式* → *后缀表达式* **`[`** *函数调用参数集* **`]`**

> 强制取值表达式语法：
>
> *强制取值表达式* → *后缀表达式* **`!`**

> 可选链式表达式语法：
>
> *可选链式表达式* → *后缀表达式* **`?`**

## 语句

> 语句语法：
>
> *语句* → *表达式* **`;`** 可选 \
> *语句* → *声明* **`;`** 可选 \
> *语句* → *循环语句* **`;`** 可选 \
> *语句* → *分支语句* **`;`** 可选 \
> *语句* → *标签语句* **`;`** 可选 \
> *语句* → *控制转移语句* **`;`** 可选 \
> *语句* → *延迟语句* **`;`** 可选 \
> *语句* → *执行语句* **`;`** 可选 \
> *语句* → *编译控制语句* \
> *语句集* → *语句* *语句集* 可选

> 循环语句语法：
>
> *循环语句* → *for-in 语句* \
> *循环语句* → *while 语句* \
> *循环语句* → *repeat-while 语句*

> for-in 语句语法：
>
> *for-in 语句* → **`for`** **`case`** 可选 *模式* **`in`** *表达式* *where 子句* 可选 *代码块*

> while 语句语法：
>
> *while 语句* → **`while`** *条件集* *代码块*
>
> *条件集* → *条件* | *条件* **`,`** *条件集* \
> *条件* → *表达式* | *可用性条件* | *case 条件* | *可选绑定条件*
>
> *case 条件* → **`case`** *模式* *构造器* \
> *可选绑定条件* → **`let`** *模式* *构造器* 可选 | **`var`** *模式* *构造器* 可选

> repeat-while 语句语法：
>
> *repeat-while 语句* → **`repeat`** *代码块* **`while`** *表达式*

> 分支语句语法：
>
> *分支语句* → *if 语句* \
> *分支语句* → *guard 语句* \
> *分支语句* → *switch 语句*

> if 语句语法：
>
> *if 语句* → **`if`** *条件集* *代码块* *else 子句* 可选 \
> *else 子句* → **`else`** *代码块* | **`else`** *if 语句*

> guard 语句语法：
>
> *guard 语句* → **`guard`** *条件集* **`else`** *代码块*

> switch 语句语法：
>
> *switch 语句* → **`switch`** *表达式* **`{`** *switch 语句* 可选 **`}`** \
> *switch 语句* → *switch 语句* *switch 语句* 可选 \
> *switch 语句* → *case 标签* *语句集* \
> *switch 语句* → *default 标签* *语句集* \
> *switch 语句* → *条件 switch 语句*
>
> *case 标签* → *属性* 可选 **`case`** *case 项集* **`:`** \
> *case 项集* → *模式* *where 子句* 可选 | *模式* *where 子句* 可选 **`,`** *case 项集* \
> *default 标签* → *属性* 可选 **`default`** **`:`**
>
> *where 子句* → **`where`** *where 表达式* \
> *where 表达式* → *表达式*
>
> *条件 switch 语句* → *switch-if 指令子句* *switch-elseif 指令子句集* 可选 *switch-else 指令子句* 可选 *endif 指令* \
> *switch-if 指令子句* → *if 指令* *编译条件* *switch-case 集* 可选 \
> *switch-elseif 指令子句* → *elseif 指令子句* *switch-elseif 指令子句集* 可选 \
> *switch-elseif 指令子句* → *elseif 指令* *编译条件* *switch-case 集* 可选 \
> *switch-else 指令子句* → *else 指令* *switch-case 集* 可选

> 标签语句语法：
>
> *标签语句* → *语句标签* *循环语句* \
> *标签语句* → *语句标签* *if 语句* \
> *标签语句* → *语句标签* *switch 语句* \
> *标签语句* → *语句标签* *do 语句*
>
> *语句标签* → *标签名* **`:`** \
> *标签名* → *标识符*

> 控制转移语句语法：
>
> *控制转移语句* → *break 语句* \
> *控制转移语句* → *continue 语句* \
> *控制转移语句* → *fallthrough 语句* \
> *控制转移语句* → *return 语句* \
> *控制转移语句* → *throw 语句*

> break 语句语法：
>
> *break 语句* → **`break`** *标签名* 可选

> continue 语句语法：
>
> *continue 语句* → **`continue`** *标签名* 可选

> fallthrough 语句语法：
>
> *fallthrough 语句* → **`fallthrough`**

> return 语句语法：
>
> *return 语句* → **`return`** *表达式* 可选

> throw 语句语法：
>
> *throw 语句* → **`throw`** *表达式*

> defer 语句语法：
>
> *defer 语句* → **`defer`** *代码块*

> do 语句语法：
>
> *do 语句* → **`do`** *throws 子句* 可选 *代码块* *catch 子句* 可选 \
> *catch 子句集* → *catch 子句* *catch 子句* 可选 \
> *catch 子句* → **`catch`** *catch 模式集* 可选 *代码块* \
> *catch 模式集* → *catch 模式* | *catch 模式* **`,`** *catch 模式集* \
> *catch 模式* → *模式* *where 子句* 可选

> 编译控制语句语法：
>
> *编译控制语句* → *条件编译块* \
> *编译控制语句* → *行控制语句* \
> *编译控制语句* → *诊断语句*

> 条件编译块语法：
>
> *条件编译块* → *if 指令子句* *elseif 指令子句集* 可选 *else 指令子句* 可选 *endif 指令*
>
> *if 指令子句* → *if 指令* *编译条件* *语句集* 可选 \
> *elseif 指令子句* → *elseif 指令子句* *elseif 指令子句集* 可选 \
> *elseif 指令子句* → *elseif 指令* *编译条件* *语句集* 可选 \
> *else 指令子句* → *else 指令* *语句集* 可选 \
> *if 指令* → **`#if`** \
> *elseif 指令* → **`#elseif`** \
> *else 指令* → **`#else`** \
> *endif 指令* → **`#endif`**
>
> *编译条件* → *平台条件* \
> *编译条件* → *标识符* \
> *编译条件* → *布尔字面量* \
> *编译条件* → **`(`** *编译条件* **`)`** \
> *编译条件* → **`!`** *编译条件* \
> *编译条件* → *编译条件* **`&&`** *编译条件* \
> *编译条件* → *编译条件* **`||`** *编译条件*
>
> *平台条件* → **`os`** **`(`** *操作系统* **`)`** \
> *平台条件* → **`arch`** **`(`** *体系结构* **`)`** \
> *平台条件* → **`swift`** **`(`** **`>=`** *swift 版本* **`)`** | **`swift`** **`(`** **`<`** *swift 版本* **`)`** \
> *平台条件* → **`compiler`** **`(`** **`>=`** *swift 版本* **`)`** | **`compiler`** **`(`** **`<`** *swift 版本* **`)`** \
> *平台条件* → **`canImport`** **`(`** *导入路径* **`)`** \
> *平台条件* → **`targetEnvironment`** **`(`** *环境* **`)`**
>
> *操作系统* → **`macOS`** | **`iOS`** | **`watchOS`** | **`tvOS`** | **`visionOS`** | **`Linux`** | **`Windows`** \
> *体系结构* → **`i386`** | **`x86_64`** | **`arm`** | **`arm64`** \
> *swift 版本* → *十进制数字* *swift 版本后缀* 可选 \
> *swift 版本后缀* → **`.`** *十进制数字* *swift 版本后缀* 可选 \
> *环境* → **`simulator`** | **`macCatalyst`**

> 行控制语句语法：
>
> *行控制语句* → **`#sourceLocation`** **`(`** **`file:`** *文件路径* **`,`** **`line:`** *行号* **`)`** \
> *行控制语句* → **`#sourceLocation`** **`(`** **`)`** \
> *行号* → 大于零的十进制整数 \
> *文件路径* → *静态字符串字面量*

> 可用性条件语法：
>
> *可用性条件* → **`#available`** **`(`** *可用性参数* **`)`** \
> *可用性条件* → **`#unavailable`** **`(`** *可用性参数* **`)`** \
> *可用性参数* → *可用性参数* | *可用性参数* **`,`** *可用性参数* \
> *可用性参数* → *平台名* *平台版本* \
> *可用性参数* → **`*`**
>
> *平台名* → **`iOS`** | **`iOSApplicationExtension`** \
> *平台名* → **`macOS`** | **`macOSApplicationExtension`** \
> *平台名* → **`macCatalyst`** | **`macCatalystApplicationExtension`** \
> *平台名* → **`watchOS`** | **`watchOSApplicationExtension`** \
> *平台名* → **`tvOS`** | **`tvOSApplicationExtension`** \
> *平台名* → **`visionOS`** | **`visionOSApplicationExtension`** \
> *平台版本* → *十进制数字* \
> *平台版本* → *十进制数字* **`.`** *十进制数字* \
> *平台版本* → *十进制数字* **`.`** *十进制数字* **`.`** *十进制数字*

## 声明

> 声明语法：
>
> *声明* → *导入声明* \
> *声明* → *常量声明* \
> *声明* → *变量声明* \
> *声明* → *类型别名声明* \
> *声明* → *函数声明* \
> *声明* → *枚举声明* \
> *声明* → *结构体声明* \
> *声明* → *类声明* \
> *声明* → *actor 声明* \
> *声明* → *协议声明* \
> *声明* → *构造器声明* \
> *声明* → *析构器声明* \
> *声明* → *扩展声明* \
> *声明* → *下标声明* \
> *声明* → *运算符声明* \
> *声明* → *优先级组声明*

> 顶级声明语法：
>
> *顶级声明* → *语句集* 可选

> 代码块语法：
>
> *代码块* → **`{`** *语句集* 可选 **`}`**

> 导入声明语法：
>
> *导入声明* → *属性* 可选 **`import`** *导入类型* 可选 *导入路径*
>
> *导入类型* → **`typealias`** | **`struct`** | **`class`** | **`enum`** | **`protocol`** | **`let`** | **`var`** | **`func`** \
> *导入路径* → *标识符* | *标识符* **`.`** *导入路径*

> 常量声明语法：
>
> *常量声明* → *属性* 可选 *声明修饰符* 可选 **`let`** *模式构造器集*
>
> *模式构造器集* → *模式构造器* | *模式构造器* **`,`** *模式构造器集* \
> *模式构造器* → *模式* *构造器* 可选 \
> *构造器* → **`=`** *表达式*

> 变量声明语法：
>
> *变量声明* → *变量声明头* *模式构造器集* \
> *变量声明* → *变量声明头* *变量名* *类型注解* *代码块* \
> *变量声明* → *变量声明头* *变量名* *类型注解* *getter-setter* \
> *变量声明* → *变量声明头* *变量名* *类型注解* *getter-setter 关键字（Keyword）块* \
> *变量声明* → *变量声明头* *变量名* *构造器* *willSet-didSet 块* \
> *变量声明* → *变量声明头* *变量名* *类型注解* *构造器* 可选 *willSet-didSet 块*
>
> *变量声明头* → *属性* 可选 *声明修饰符* 可选 **`var`** \
> *变量名* → *标识符*
>
> *getter-setter* → *代码块* \
> *getter-setter* → **`{`** *getter 子句* *setter 子句* 可选 **`}`** \
> *getter-setter* → **`{`** *setter 子句* *getter 子句* **`}`** \
> *getter 子句* → *属性* 可选 *可变性修饰符* 可选 **`get`** *代码块* \
> *setter 子句* → *属性* 可选 *可变性修饰符* 可选 **`set`** *setter 名* 可选 *代码块* \
> *setter 名* → **`(`** *标识符* **`)`**
>
> *getter-setter 关键字（Keyword）块* → **`{`** *getter 关键字子句* *setter 关键字子句* 可选 **`}`** \
> *getter-setter 关键字（Keyword）块* → **`{`** *setter关键字子句* *getter 关键字子句* **`}`** \
> *getter 关键字子句* → *属性* 可选 *可变性修饰符* 可选 **`get`** \
> *setter 关键字子句* → *属性* 可选 *可变性修饰符* 可选 **`set`**
>
> *willSet-didSet 块* → **`{`** *willSet 子句* *didSet 子句* 可选 **`}`** \
> *willSet-didSet 块* → **`{`** *didSet 子句* *willSet 子句* 可选 **`}`** \
> *willSet 子句* → *属性* 可选 **`willSet`** *setter 名* 可选 *代码块* \
> *didSet 子句* → *属性* 可选 **`didSet`** *setter 名* 可选 *代码块*

> 类型别名声明语法：
>
> *类型别名声明* → *属性* 可选 *访问级别修饰符* 可选 **`typealias`** *类型别名名* *泛型参数子句* 可选 *类型别名赋值* \
> *类型别名名* → *标识符* \
> *类型别名赋值* → **`=`** *类型*

> 函数声明语法：
>
> *函数声明* → *函数头* *函数名* *泛型参数子句* 可选 *函数签名* *泛型 where 子句* 可选 *函数体* 可选
>
> *函数头* → *属性* 可选 *声明修饰符* 可选 **`func`** \
> *函数名* → *标识符* | *运算符*
>
> *函数签名* → *参数子句* **`async`** 可选 *throws 子句* 可选 *函数结果* 可选 \
> *函数签名* → *参数子句* **`async`** 可选 **`rethrows`** *函数结果* 可选 \
> *函数结果* → **`->`** *属性* 可选 *类型* \
> *函数体* → *代码块*
>
> *参数子句* → **`(`** **`)`** | **`(`** *参数集* **`)`** \
> *参数集* → *参数* | *参数* **`,`** *参数集* \
> *参数* → *外部参数名* 可选 *本地参数名* *参数类型注解* *默认参数子句* 可选 \
> *参数* → *外部参数名* 可选 *本地参数名* *参数类型注解* \
> *参数* → *外部参数名* 可选 *本地参数名* *参数类型注解* **`...`**
>
> *外部参数名* → *标识符* \
> *本地参数名* → *标识符* \
> *参数类型注解* → **`:`** *属性* 可选 *参数修饰符* 可选 *类型* \
> *参数修饰符* → **`inout`** | **`borrowing`** | **`consuming`** \
> *默认参数子句* → **`=`** *表达式*

> 枚举声明语法：
>
> *枚举声明* → *属性* 可选 *访问级别修饰符* 可选 *联合式枚举* \
> *枚举声明* → *属性* 可选 *访问级别修饰符* 可选 *原始值式枚举*
>
> *联合式枚举* → **`indirect`** 可选 **`enum`** *枚举名* *泛型参数子句* 可选 *类型继承子句* 可选 *泛型 where 子句* 可选 **`{`** *联合式枚举成员* 可选 **`}`** \
> *联合式枚举成员* → *联合式枚举成员* *联合式枚举成员* 可选 \
> *联合式枚举成员* → *声明* | *联合式枚举 case 子句* | *编译控制语句* \
> *联合式枚举 case 子句* → *属性* 可选 **`indirect`** 可选 **`case`** *联合式枚举 case 集* \
> *联合式枚举 case 集* → *联合式枚举 case* | *联合式枚举 case* **`,`** *联合式枚举 case 集* \
> *联合式枚举 case* → *枚举case名* *元组类型* 可选 \
> *枚举名* → *标识符* \
> *枚举 case 名* → *标识符*
>
> *原始值式枚举* → **`enum`** *枚举名* *泛型参数子句* 可选 *类型继承子句* *泛型 where 子句* 可选 **`{`** *原始值式枚举成员*
> *原始值式枚举成员集* → *原始值式枚举成员* *原始值式枚举成员集*可选 \
> *原始值式枚举成员集* → *声明* | *原始值式枚举 case 子句* | *编译控制语句* \
> *原始值式枚举 case 子句* → *属性*可选 **`case`** *原始值式枚举 case 集* \
> *原始值式枚举 case 集* → *原始值式枚举 case* | *原始值式枚举 case* **`,`** *原始值式枚举 case 集* \
> *原始值式枚举 case* → *枚举 case 名* *原始值赋值*可选 \
> *原始值赋值* → **`=`** *原始值字面量* \
> *原始值字面量* → *数值字面量* | *静态字符串字面量* | *布尔字面量*

> 结构声明语法：
>
> *结构声明* → *属性*可选 *访问级别修饰符*可选 **`struct`** *结构名* *泛型参数子句*可选 *类型继承子句*可选 *泛型 where 子句*可选 *结构主体* \
> *结构名* → *标识符* \
> *结构主体* → **`{`** *结构成员集*可选 **`}`**
>
> *结构成员集* → *结构成员* *结构成员集*可选 \
> *结构成员* → *声明* | *编译控制语句*

> 类声明语法：
>
> *类声明* → *属性*可选 *访问级别修饰符*可选 **`final`** 可选 **`class`** *类名* *泛型参数子句*可选 *类型继承子句*可选 *泛型 where 子句*可选 *类主体* \
> *类声明* → *属性*可选 **`final`** *访问级别修饰符*可选 **`class`** *类名* *泛型参数子句*可选 *类型继承子句*可选 *泛型 where子句*可选 *类主体* \
> *类名* → *标识符* \
> *类主体* → **`{`** *类成员*可选 **`}`**
>
> *类成员* → *类成员* *类成员*可选 \
> *类成员* → *声明* | *编译控制语句*

> actor 声明语法：
>
> *actor 声明* → *属性*可选 *访问级别修饰符*可选 **`actor`** *actor 名* *泛型参数子句*可选 *类型继承子句*可选 *泛型 where 子句*可选 *actor 主体* \
> *actor 名* → *标识符* \
> *actor 主体* → **`{`** *actor 成员*可选 **`}`**
>
> *actor 成员* → *actor 成员* *actor 成员*可选 \
> *actor 成员* → *声明* | *编译控制语句*

> 协议声明语法：
>
> *协议声明* → *属性*可选 *访问级别修饰符*可选 **`protocol`** *协议名* *类型继承子句*可选 *泛型 where 子句*可选 *协议主体* \
> *协议名* → *标识符* \
> *协议主体* → **`{`** *协议成员*可选 **`}`**
>
> *协议成员* → *协议成员* *协议成员*可选 \
> *协议成员* → *协议成员声明* | *编译控制语句*
>
> *协议成员声明* → *协议属性声明* \
> *协议成员声明* → *协议方法声明* \
> *协议成员声明* → *协议构造器声明* \
> *协议成员声明* → *协议下标声明* \
> *协议成员声明* → *协议关联类型声明* \
> *协议成员声明* → *类型别名声明*

> 协议属性声明语法：
>
> *协议属性声明* → *变量声明头* *变量名* *类型注解* *getter-setter 关键字块*

> 协议方法声明语法：
>
> *协议方法声明* → *函数头* *函数名* *泛型参数子句*可选 *函数签名* *泛型 where 子句*可选

> 协议构造器声明语法：
>
> *协议构造器声明* → *构造器头* *泛型参数子句*可选 *参数子句* *抛出子句*可选 *泛型 where 子句*可选 \
> *协议构造器声明* → *构造器头* *泛型参数子句*可选 *参数子句* **`rethrows`** *泛型 where 子句*可选

> 协议下标声明语法：
>
> *协议下标声明* → *下标头* *下标结果* *泛型 where 子句*可选 *getter-setter 关键字块*

> 协议关联类型声明语法：
>
> *协议关联类型声明* → *属性*可选 *访问级别修饰符*可选 **`associatedtype`** *类型别名名* *类型继承子句*可选 *类型别名赋值*可选 *泛型 where 子句*可选

> 构造器声明语法：
>
> *构造器声明* → *构造器头* *泛型参数子句*可选 *参数子句* **`async`** 可选 *抛出子句*可选 *泛型 where 子句*可选 *构造器主体* \
> *构造器声明* → *构造器头* *泛型参数子句*可选 *参数子句* **`async`** 可选 **`rethrows`** *泛型 where 子句*可选 *构造器主体* \
> *构造器头* → *属性*可选 *声明修饰符*可选 **`init`** \
> *构造器头* → *属性*可选 *声明修饰符*可选 **`init`** **`?`** \
> *构造器头* → *属性*可选 *声明修饰符*可选 **`init`** **`!`** \
> *构造器主体* → *代码块*

> 析构器声明语法：
>
> *析构器声明* → *属性*可选 **`deinit`** *代码块*

> 扩展声明语法：
>
> *扩展声明* → *属性*可选 *访问级别修饰符*可选 **`extension`** *类型标识符* *类型继承子句*可选 *泛型 where 子句*可选 *扩展主体* \
> *扩展主体* → **`{`** *扩展成员*可选 **`}`**
>
> *扩展成员* → *扩展成员* *扩展成员*可选 \
> *扩展成员* → *声明集* | *编译控制语句*

> 下标声明语法：
>
> *下标声明* → *下标头* *下标结果* *泛型 where 子句*可选 *代码块* \
> *下标声明* → *下标头* *下标结果* *泛型 where 子句*可选 *getter-setter 块* \
> *下标声明* → *下标头* *下标结果* *泛型 where 子句*可选 *getter-setter 关键字块* \
> *下标头* → *属性*可选 *声明修饰符*可选 **`subscript`** *泛型参数子句*可选 *参数子句* \
> *下标结果* → **`->`** *特性*可选 *类型*

> 宏声明语法：
>
> *宏声明* → *宏头* *标识符* *泛型参数子句*可选 *宏签名* *宏定义*可选 *泛型 where子句* \
> *宏头* → *属性*可选 *声明修饰符*可选 **`macro`**  \
> *宏签名* → *参数子句* *宏函数签名结果*可选 \
> *宏函数签名结果* → **`->`** *类型* \
> *宏定义* → **`=`** *表达式*

> 运算符声明语法：
>
> *运算符声明* → *前缀运算符声明* | *后缀运算符声明* | *中缀运算符声明*
>
> *前缀运算符声明* → **`prefix`** **`operator`** *运算符* \
> *后缀运算符声明* → **`postfix`** **`operator`** *运算符* \
> *中缀运算符声明* → **`infix`** **`operator`** *运算符* *中缀运算符组*可选
>
> *中缀运算符组* → **`:`** *优先级组名*

> 优先级组声明语法：
>
> *优先级组声明* → **`precedencegroup`** *优先级组名* **`{`** *优先级组属性*可选 **`}`**
>
> *优先级组属性* → *优先级组属性* *优先级组属性*可选 \
> *优先级组属性* → *优先级组关系* \
> *优先级组属性* → *优先级组赋值* \
> *优先级组属性* → *优先级组结合*
>
> *优先级组关系* → **`higherThan`** **`:`** *优先级组名集* \
> *优先级组关系* → **`lowerThan`** **`:`** *优先级组名集*
>
> *优先级组赋值* → **`assignment`** **`:`** *布尔字面量*
>
> *优先级组结合* → **`associativity`** **`:`** **`left`** \
> *优先级组结合* → **`associativity`** **`:`** **`right`** \
> *优先级组结合* → **`associativity`** **`:`** **`none`**
>
> *优先级组名集* → *优先级组名* | *优先级组名* **`,`** *优先级组名* \
> *优先级组名* → *标识符*

> 声明修饰符语法：
>
> *声明修饰符* → **`class`** | **`convenience`** | **`dynamic`** | **`final`** | **`infix`** | **`lazy`** | **`optional`** | **`override`** | **`postfix`** | **`prefix`** | **`required`** | **`static`** | **`unowned`** | **`unowned`** **`(`** **`safe`** **`)`** | **`unowned`** **`(`** **`unsafe`** **`)`** | **`weak`** \
> *声明修饰符* → *访问级别修饰符* \
> *声明修饰符* → *可变性修饰符* \
> *声明修饰符* → *actor 隔离修饰符* \
> *声明修饰符* → *声明修饰符* *声明修饰符*可选
>
> *访问级别修饰符* → **`private`** | **`private`** **`(`** **`set`** **`)`** \
> *访问级别修饰符* → **`fileprivate`** | **`fileprivate`** **`(`** **`set`** **`)`** \
> *访问级别修饰符* → **`internal`** | **`internal`** **`(`** **`set`** **`)`** \
> *访问级别修饰符* → **`package`** | **`package`** **`(`** **`set`** **`)`** \
> *访问级别修饰符* → **`public`** | **`public`** **`(`** **`set`** **`)`** \
> *访问级别修饰符* → **`open`** | **`open`** **`(`** **`set`** **`)`**
>
> *可变性修饰符* → **`mutating`** | **`nonmutating`**
>
> *actor 隔离修饰符* → **`nonisolated`**

## 属性

> 属性语法：
>
> *属性* → **`@`** *属性名* *属性参数子句*可选 \
> *属性名* → *标识符* \
> *属性参数子句* → **`(`** *平衡令牌*可选 **`)`** \
> *属性* → *属性* *属性*可选
>
> *平衡令牌集* → *平衡令牌* *平衡令牌集*可选 \
> *平衡令牌* → **`(`** *平衡令牌集*可选 **`)`** \
> *平衡令牌* → **`[`** *平衡令牌集*可选 **`]`** \
> *平衡令牌* → **`{`** *平衡令牌集*可选 **`}`** \
> *平衡令牌* → 任何标识符、关键字、字面量或运算符 \
> *平衡令牌* → 任何标点符号，除了 **`(`**,  **`)`**,  **`[`**,  **`]`**,  **`{`**, 或  **`}`**

## 模式

> 模式语法：
>
> *模式* → *通配符模式* *类型注解*可选 \
> *模式* → *标识符模式* *类型注解*可选 \
> *模式* → *值绑定模式* \
> *模式* → *元组模式* *类型注解*可选 \
> *模式* → *枚举 case 模式* \
> *模式* → *可选模式* \
> *模式* → *类型转换模式* \
> *模式* → *表达式模式*

> 通配符模式语法：
>
> *通配符模式* → **`_`**

> 标识符模式语法：
>
> *标识符模式* → *标识符*

> 值绑定模式语法：
>
> *值绑定模式* → **`var`** *模式* | **`let`** *模式*

> 元组模式语法：
>
> *元组模式* → **`(`** *元组模式元素集*可选 **`)`** \
> *元组模式元素集* → *元组模式元素* | *元组模式元素* **`,`** *元组模式元素集* \
> *元组模式元素* → *模式* | *标识符* **`:`** *模式*

> 枚举 case 模式语法：
>
> *枚举 case 模式* → *类型标识符*可选 **`.`** *枚举 case 名* *元组模式*可选

> 可选模式语法：
>
> *可选模式* → *标识符模式* **`?`**

> 类型转换模式语法：
>
> *类型转换模式* → *is 模式* | *as 模式* \
> *is 模式* → **`is`** *类型* \
> *as 模式* → *模式* **`as`** *类型*

> 表达式模式语法：
>
> *表达式模式* → *表达式*

## 泛型参数和参数

> 泛型参数子句语法：
>
> *泛型参数子句* → **`<`** *泛型参数集* **`>`** \
> *泛型参数集* → *泛型参数* | *泛型参数* **`,`** *泛型参数集* \
> *泛型参数* → *类型名* \
> *泛型参数* → *类型名* **`:`** *类型标识符* \
> *泛型参数* → *类型名* **`:`** *协议组合类型*
>
> *泛型 where子句* → **`where`** *需求集* \
> *需求集* → *需求* | *需求* **`,`** *需求集* \
> *需求* → *符合要求* | *同类型要求*
>
> *符合要求* → *类型标识符* **`:`** *类型标识符* \
> *符合要求* → *类型标识符* **`:`** *协议组合类型* \
> *同类型要求* → *类型标识符* **`==`** *类型*

> 泛型参数子句语法：
>
> *泛型参数子句* → **`<`** *泛型参数集* **`>`** \
> *泛型参数集* → *泛型参数* | *泛型参数* **`,`** *泛型参数集* \
> *泛型参数* → *类型*