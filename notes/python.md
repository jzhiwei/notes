# PYTHON

解释型语言，运行速度慢，开发速度快

## 基本数据类型

### Number

#### int

- 使用int类型做除法运算(/)时会得到float类型，使用//会得到int类型的结果。

- bin() | 0b: 以二进制格式输出

- oct() | 0o: 以八进制格式输出

- hex() | 0x: 以十六进制格式输出

#### float
#### bool

- True: 也可以使用非0数字、非空字符串、非空数组表示

- Flase: 0、空字符串、空数组、None

#### complex（复数）

- - -
### 序列

    可以通过下标访问元素、切片操作、使用+、*操作符

#### str

- 可以使用单引号('')或者双引号("")表示字符串；使用三引号('''或""")或者\可以定义多行字符串

- 在字符串前面使用r或R表示字符串原样输出，不会进行转义

    ```
    print '\"To be, or not to be\": that is the question.\nWhether it\'s nobler in the mind to suffer.'

    print r'''"To be, or not to be": that is the question.
    Whether it's nobler in the mind to suffer.'''

    输出: 
    "To be, or not to be": that is the question. 
    Whether it's nobler in the mind to suffer.
    ```

- str * n: 输出n次字符串

    ` >>> 'hello'*2  -> 'hellohello'`

- str[n]: 获取指定下标的字符

- str[-n]: 从后往前数第n个字符
    
- str[start:end]: 截取字符串。start表示开始位置，end表示结束位置（包头不包尾）。如果end为负数表示从后往前的第n个字符为结束位置（也不包括第n个字符）。如果end为空，表示直到字符串末尾。

- 显示中文使用字母u

    ` >>> print u'中文 日文 韩文' -> 中文 日文 韩文 `

- 如果中文字符报错，需要在py文件第一行添加注释

    ` # -*- coding:utf-8 -*- ` 
- - -

#### 列表（list）

- 使用[]定义，通过索引获取元素。如果使用开始位置和结束位置获取元素，返回的类型还是列表。

- 正序访问下标从0开始。倒序访问从-1开始，表示倒数第一。

- append(): 追加新元素到列表的末尾

    ```
    L = ['Adam','Lisa','Bart']
    L.append('Paul')
    print L -> ['Adam','Lisa','Bart','Paul']
    ```
- - -
#### 元组（tuple）

- - -

### 无序
