# 0x00 前言
Burp自带的SQLi扫描，发送的burp感觉有点多，在有waf的情况下，收到极大的限制。所以写一款适合自己的SQLi扫描插件（只发送一次数据包）。

# 0x01 检测原理
检测时间注入(减少发包量)，报错型注入(检测页面是否有sql错误提示，不需要发包)。
采用的payload是`11^%0axor(sleep(5))#'xor(sleep(5))#"^xor(sleep(5))#'`，浏览器中``11%0axor(sleep(5))%23'xor(sleep(5))%23"xor(sleep(5))%23'``,这样可以一次性检测数字型、字符型使用`'`或`"`作为分隔符的字符型)注入。不过`Insert`、`Limit`、`()`等一些注入，还没有找到好的办法进行检测。

payload
`11%0axor(sleep(5))%23'xor(sleep(5))%23"xor(sleep(5))%23'`
`1||sleep(5)/*'||sleep(5)||'"||sleep(5)||"*/`
