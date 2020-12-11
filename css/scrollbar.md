# [滚动条样式](https://www.cnblogs.com/ranyonsue/p/9487599.html)

![滚动条组成](https://images2018.cnblogs.com/blog/940884/201808/940884-20180816152620621-1300097326.png)

## 自定义滚动条实现

此部分针对```webkit```内核的浏览器，使用伪类来改变滚动条的默认样式，详情如下：


## 滚动条组成部分

1. **```::-webkit-scrollbar```** 滚动条整体部分

2. **```::-webkit-scrollbar-thumb```** 滚动条里面的小方块，能向上向下移动（或向左向右移动）

3. **```::-webkit-scrollbar-track```** 滚动条的轨道（里面装有```Thumb```）

4. **```::-webkit-scrollbar-button```** 滚动条的轨道的两端按钮，由于通过点击微调小方块的位置。

5. **```::-webkit-scrollbar-track-piece```** 内层轨道，滚动条中间部分

6. **```::-webkit-scrollbar-corner```** 边角，即垂直滚动条和水平滚动条相交的地方

7. **```::-webkit-resizer```** 两个滚动条的交汇处上用于拖动调整元素大小的小控件

## 其他设置项：

**```:horizontal```**  
//horizontal伪类适用于任何水平方向上的滚动条  
  
**```:vertical```**  
//vertical伪类适用于任何垂直方向的滚动条  
  
**```:decrement```**  
//decrement伪类适用于按钮和轨道碎片。表示递减的按钮或轨道碎片，例如可以使区域向上或者向右移动的区域和按钮  
  
**```:increment```**  
//increment伪类适用于按钮和轨道碎片。表示递增的按钮或轨道碎片，例如可以使区域向下或者向左移动的区域和按钮  
  
**```:start```**  
//start伪类适用于按钮和轨道碎片。表示对象（按钮 轨道碎片）是否放在滑块的前面  
  
**```:end```**  
//end伪类适用于按钮和轨道碎片。表示对象（按钮 轨道碎片）是否放在滑块的后面  
  
**```:double-button```**  
//double-button伪类适用于按钮和轨道碎片。判断轨道结束的位置是否是一对按钮。也就是轨道碎片紧挨着一对在一起的按钮。  
  
**```:single-button```**  
//single-button伪类适用于按钮和轨道碎片。判断轨道结束的位置是否是一个按钮。也就是轨道碎片紧挨着一个单独的按钮。  
  
**```:no-button```**  
no-button伪类表示轨道结束的位置没有按钮。  
  
**```:corner-present```**  
//corner-present伪类表示滚动条的角落是否存在。  
  
**```:window-inactive```**  
//适用于所有滚动条，表示包含滚动条的区域，焦点不在该窗口的时候。  
```css  
::-webkit-scrollbar-track-piece:start {  
/*滚动条上半边或左半边*/  
}  
  
::-webkit-scrollbar-thumb:window-inactive {  
/*当焦点不在当前区域滑块的状态*/  
}  
  
::-webkit-scrollbar-button:horizontal:decrement:hover {  
/*当鼠标在水平滚动条下面的按钮上的状态*/  
} 
```