# Demo


## 一、标题
# 标题1
## 标题2
### 标题3
#### 标题4

标题1（下加三个等号）
===

标题2（下加三个横线）
---

## 二、段落

我是zither，什么都不加这一段就是段落（段落结束加两个空格） 
段落和段落之间要空行  
  我

## 三、强调

**我是粗体**  
*我是斜体*  _我也是斜体_  
***我是加粗和倾斜的***  
~~我是删除线~~

## 四、列表

### 无序列表
- Name:zither  
  - Name：zither  
- qq:325831871   
### 有序列表
1. Name:zither  
  1. Name:zither  
2. QQ:325831871  
3. 插入4
4. 三个列表之后

## 五、链接
### 内嵌式链接  
- 外部链接  
  [百度][baidu]
- 内部链接1：链接仓库的其他文件  
  [ListPractice][ListPractice]
- 内部链接2：链接本文档的其他部分  
  [本文档--列表](MarkDown笔记.md#无序列表) 

### 引用式链接
见下面。  

[百度]:http://www.baidu.com
[baidu]:http://www.baidu.com
[ListPractice]:ListPractice.md
[liu]:https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1476903450,289056256&amp;fm=26&amp;gp=0.jpg

## 六、 图片
- 语法格式  
    ! [alt] (url text)  
- 外部图片  
  ![刘德华](https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1476903450,289056256&fm=26&gp=0.jpg "刘德华")
- 仓库内部图片  
  ![仓库内的刘德华](images/timg.jpg "刘德华")

- 图片的引用式链接  
  ![刘德华][liu]

## 七、引用
> 这是一个引文。 
> >这是多重引文
> >>三重引文

--《出处》

## 八、代码块
- 行内代码  
  这个代码中用来声明变量的是`var a = 10`,打印变量内容是`console.log(a)`
- 块式代码  
```javascript
var str = "hello world"
```

## 九、水平分割线
- 三个横线（前面不能写东西，否则变成了标题）、三个*、三个下划线

---
***
___

## 十、HTML代码
<p align = 'center'>Hello World</p>

## 十一、表格

|这|是|表头|
|---|:----:|---:|
|cewerwwrerll1|   ceqweqweqwll2    |     cellsfdd3      |
|**row2**|row3|row4|
|img|demo|![][liu]|

- 精简表格  
这|是|表头
---|:----:|---:
cewerwwrerll1|   ceqweqweqwll2    |     cellsfdd3      
row2|row3|row4

## 十二、GFM
Github Flvored Markdown -- GFM

- task list  任务列表  
  - [x] task1  
  - [ ] task2 
  - [x] task3 
- emoji 表情符号
  - 阳光  
    :partly_sunny:

## 十三、总结
