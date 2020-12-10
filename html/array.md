# [JavaScript Array 对象](https://www.runoob.com/jsref/jsref-obj-array.html)

---


---

# Array 对象
```Array``` 对象用于在变量中存储多个值:
```js
var cars = ["Saab", "Volvo", "BMW"];
```
第一个数组元素的索引值为 0，第二个索引值为 1，以此类推。

# 数组属性
| 属性 | 描述 |
|-|-|
| constructor | 返回创建数组对象的原型函数。 |
| length | 设置或返回数组元素的个数。 |
| prototype | 允许你向数组对象添加属性或方法。 |
# ```Array``` 对象方法
| 方法 | 描述 |
|-|-|
| concat() | 连接两个或更多的数组，并返回结果。 |
| copyWithin() | 从数组的指定位置拷贝元素到数组的另一个指定位置中。 |
| entries() | 返回数组的可迭代对象。 |
| every() | 检测数值元素的每个元素是否都符合条件。 |
| fill() | 使用一个固定值来填充数组。 |
| filter() | 检测数值元素，并返回符合条件所有元素的数组。 |
| find() | 返回符合传入测试（函数）条件的数组元素。 |
| findIndex() | 返回符合传入测试（函数）条件的数组元素索引。 |
| forEach() | 数组每个元素都执行一次回调函数。 |
| from() | 通过给定的对象中创建一个数组。 |
| includes() | 判断一个数组是否包含一个指定的值。 |
| indexOf() | 搜索数组中的元素，并返回它所在的位置。 |
| isArray() | 判断对象是否为数组。 |
| join() | 把数组的所有元素放入一个字符串。 |
| keys() | 返回数组的可迭代对象，包含原始数组的键(key)。 |
| lastIndexOf() | 搜索数组中的元素，并返回它最后出现的位置。 |
| map() | 通过指定函数处理数组的每个元素，并返回处理后的数组。 |
| pop() | 删除数组的最后一个元素并返回删除的元素。 |
| push() | 向数组的末尾添加一个或更多元素，并返回新的长度。 |
| [```reduce()```](#JavaScript:reduce()方法) | 将数组元素计算为一个值（从左到右）。 |
| reduceRight() | 将数组元素计算为一个值（从右到左）。 |
| reverse() | 反转数组的元素顺序。 |
| shift() | 删除并返回数组的第一个元素。 |
| slice() | 选取数组的一部分，并返回一个新数组。 |
| some() | 检测数组元素中是否有元素符合指定条件。 |
| sort() | 对数组的元素进行排序。 |
| splice() | 从数组中添加或删除元素。 |
| toString() | 把数组转换为字符串，并返回结果。 |
| unshift() | 向数组的开头添加一个或更多元素，并返回新的长度。 |
| valueOf() | 返回数组对象的原始值。 |

---------------

# JavaScript:reduce()方法
> https://www.runoob.com/jsref/jsref-reduce.html

# 语法
```array.reduce(function(total, currentValue, currentIndex, arr), initialValue)```

# 参数
<table class="tecspec"> 
  <tbody>
    <tr>
      <th style="width:25%">参数</th>
      <th>描述</th>
    </tr>  
    <tr>
      <td><em>function(total,currentValue, index,arr)</em></td>
      <td>必需。用于执行每个数组元素的函数。<br>函数参数:
        <table class="tecspec"> 
          <tbody>
            <tr>
              <th style="width:25%">参数</th>
              <th>描述</th>
            </tr>  
              <tr>
              <td><em>total</em></td>
              <td>必需。<em>初始值</em>, 或者计算结束后的返回值。</td>
              </tr>
            <tr>
              <td><em>currentValue</em></td>
              <td>必需。当前元素</td>
            </tr>
            <tr>
              <td><em>currentIndex</em></td>
              <td>可选。当前元素的索引</td>
            </tr>
              <tr>
              <td><em>arr</em></td>
              <td>可选。当前元素所属的数组对象。</td>
            </tr>
          </tbody>
        </table>
      </td>
    </tr>
    <tr>
      <td><em>initialValue</em></td>
      <td>可选。传递给函数的初始值</td>
    </tr>
  </tbody>
</table>


# 定义和用法
```reduce()``` 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

```reduce()``` 可以作为一个高阶函数，用于函数的 ```compose```。

注意: ```reduce()``` 对于空数组是不会执行回调函数的。

**实例**
计算数组元素相加后的总和：
```js
var numbers = [65, 44, 12, 4];
 
function getSum(total, num) {
    return total + num;
}
function myFunction(item) {
    document.getElementById("demo").innerHTML = numbers.reduce(getSum);
}
```
输出结果：
```js
125
```