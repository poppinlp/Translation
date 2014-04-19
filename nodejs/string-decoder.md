> 贡献者：梁鹏  
> 翻译时间：2014年4月19日  
> 原文来源：http://www.nodejs.org/api/string_decoder.html  
> 原文作者：NodeJS  
> 原文标题：String Decoder  

#StringDecoder
> Stability: 3 - Stable

通过`require('string_decoder')`来使用这个模块。该模块用来把缓冲内容解码为字符串。该模块是`buffer.toString()`的一个简单接口，但提供了额外的对于utf8的支持。

```
var StringDecoder = require('string_decoder').StringDecoder;
var decoder = new StringDecoder('utf8');

var cent = new Buffer([0xC2, 0xA2]);
console.log(decoder.write(cent));

var euro = new Buffer([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro));
```

##Class: StringDecoder
接受一个`encoding`参数，参数默认为`utf8`。

##decoder.write(buffer)
返回一个解码后的字符串。

##decoder.end()
返回缓冲中留下的任何字节。
