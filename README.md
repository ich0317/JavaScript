# <center>**JavaScript 笔记**</center>
本文收集了前端工作中可能会用到的一些JS方法属性。

## 目录  
- [位运算](#operators)
- [字符串](#string)
- [数字](#array)
- [函数](#fn)
- [数字](#number)
- [对象](#obj)
- [其他](#other)  
  
## <a id="operators">位运算</a> 
[具体用法详解 >>](http://c.biancheng.net/view/5469.html) 

1. 使用左移运算符 << 迅速得出2的次方  
```
  1 << 2      // 4  2的2次方
  1 << 0       // 1024  2的10次方
```
2. 使用 ^ 切换变量 0 或 1  
```
  togle = toggle ? 1 : 0;     // before  
  toggle ^= 0;                // after
```
3. 使用 & 判断奇偶性  
```
  7 & 1   // 基数 & 1 等于 1
  8 & 1   // 偶数 & 1 等于 0
```  
4. 使用 !! 将数字转为布尔值  
```
  !!1     // true
  !!0     // false
  !!5.6   // true
```
5. 使用~、>>、<<、>>>、|来取整
```
  ~~5.6       // 5  
  5.6 >> 0    // 5  
  5.6 << 0    // 5  
  5.6 | 0     // 5  
  5.6 >>> 0   // 5  

  ！注意：不能用于负数
```
6. 使用^来完成值交换
```
  // before
  var a = 1, b = 2, temp;
  temp = a;
  a = b;
  b = temp;

  // after
  var a = 1, b = 2;
  a ^= b;
  b ^= a;
  a ^= b;
  console.log(a)
  console.log(b)  

  // ES6
  [b, a] = [a = 1, b = 2]
```
7. 使用 n + 0.5 | 0 来替代 Math.round()
```
  var a = 5.6;
  console.log( a + 0.5 | 0 )    // 6

  var a = -5.6;
  cosnole.log( a - 0.5 | 0 )    // -6
```
## <a id="string">字符串</a>
1. 使用toString(16)取随机数字符串
```
  Math.random().toString(16).substring(2, 15);    // 最多取13位
```
2. 使用.link() 创建链接
```
  'baidu'.link( 'http://www.baidu.com' )
```
3. 使用 Array 来重复字符
```
  // before
  for (var a = "", i = 7; i--;) a+= 0;  

  // after  
  Array(7).join(0)  

  // ES6
  "0".repeat(6)                          

```
4. 返回字符串的字节长度
```
  const byteSize = str => new Blob([str]).size;
  byteSize('Hello World');
```

## <a id="array">数组</a>
1. 创建过去七天的数组，如果将代码中的减号换成加号，你将得到未来7天的数组集合
```
  [...Array(7).keys()].map(days=>new Date(Date.now()-86400000*days));
```
2. 取数组最大值
```
  Math.max(...[2, 1, 6, 4])
```
3. 扁平化n维数组
```
  [1,2,['a',['3','4']]].flat(n) //n表示维度, n=Infinity时为无限大
```
4. 类数组转数组
```
  // ES5  
  Array.prototype.slice.call(arrlike)

  // ES6
  [...arrlike]
  -
  Array.from(arguments)
```

## <a id="fn">函数</a>
1.两元素是否包含关系，适用于点击非弹窗区域关闭弹窗 compareDocumentPosition/contains
```
var p1=document.getElementById("p1");
var p2=document.getElementById("p2");
p1.compareDocumentPosition(p2);
//返回结果 ie8+
//   0              元素一致 
//   1              节点在不同的文档（或者一个在文档之外） 
//   2              节点 p2 在节点 p1 之前 
//   4              节点 p1 在节点 p2 之前 
//   8              节点 p2 包含节点 p1 
//   16             节点 p1 包含节点 p2 
//   32             浏览器的私有使用
//   20             一旦一个节点 p1 包含另一个节点 p2，包含 p2（+16） 且在 p1 之前（+4），则最后的结果是数字 20  

p1.contains(p2)   // 如果p1包含p2 返回true 否则返回false
```

## <a id="number">数字</a>
1. 生成指定范围的随机整数
```
  const randomIntegerInRange = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;

  randomIntegerInRange(0, 5); // 0 - 5之间随机数（包含0和5）
```

## <a id="obj">对象</a>

## <a id="other">其他</a>
1. 获取URL后面参数 如 localhost/index.html?a=1&b=2;
```
  let oQuery={};
  location.search.replace(/([^?&]+)=([^?&]+)/g,(s,k,v)=>oQuery[k]=v);
  console.log(oQuery)
```
2. 判断数据类型（比较全面）
```
  Object.prototype.toString.call()

```
3. 转义`HTML`，防止XSS
```
  const escapeHTML = str =>
  str.replace(
    /[&<>'"]/g,
    tag =>
      ({
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        "'": '&#39;',
        '"': '&quot;'
      }[tag] || tag)
  );
  escapeHTML('<a href="#">Im a XSS</a>');
```# JavaScript
