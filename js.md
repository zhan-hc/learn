- ## 输出['1','5','11'].map(parseInt)结果

  先看看map的语法

  > array.map(function(currentValue,index,arr), thisValue)

  map的第一个参数是个回调函数，三个入参currentValue,index,arr，为了加深理解，我们来看看例子

  ```js
  ['1','5','11'].map(console.log)
  
  // 输出结果
  
  1 0 ['1', '5', '11']
  5 1 ['1', '5', '11']
  11 2 ['1', '5', '11']
  ```

  根据输出结果，可以很好的理解map的三个入参的意义，currentValue,index分别对应当前遍历数组的item值和索引，我们将其解析如下

  ```js
  // ['1','5','11'].map(console.log)等效于
  ['1','5','11'].map((item, index, arr) => {
    return console.log(item, index, arr)
  })
  ```

  这样就很好理解了，再看看题目

  ```js
  // ['1','5','11'].map(parseInt)等同于
  
  ['1','5','11'].map((item, index, arr) => {
    return parseInt(item, index, arr)
  })
  ```

  根据上面的解析我们需要先了解parseInt的语法

  > parseInt(string, radix)

  |  参数  |                         描述                         |
  | :----: | :--------------------------------------------------: |
  | string |               必需。要被解析的字符串。               |
  | radix  | 可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。 |

  当参数 radix 的值为 0，或没有设置该参数时，parseInt() 会根据 string 来判断数字的基数。

  当参数 radix的值小于 2 或者大于 36，则 parseInt() 将返回 NaN

  如果省略参数 radix或其值为 0，则数字将以 10 为基础来解析。

  

  我们来解析一下。整个 `map` 会循环三次：


  第一次：`parseInt('1', 0, ['1', '5', '11'])` 
  >因其 `radix` 的值为 `0`，所以基数为 `10` ，将字符串 `'1'` 转为 `10` 进制的数组就是 `1`

  第二次：`parseInt('5', 1, ['1', '5', '11'])` 
  >因 `radix` 的值为 `1` 不在 `2-36` 范围所以返回 `NAN`

  第三次：`parseInt('11', 2, ['1', '5', '11'])
  > 参数都符合，将 `'11'` 转为二进制数字就是 `3`


  所以最终结果返回 **[1, NAN, 3]**