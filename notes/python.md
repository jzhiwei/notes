# PYTHON

解释型语言，运行速度慢，开发速度快

- [基本数据类型](#基本数据类型)
    - [Number](#Number)
        - [int](#int)
        - [float](#float)
        - [bool](#bool)
        - [complex](#complex)
    - [序列](#序列)
        - [str](#str)
        - [list](#列表list)
        - [tuple](#元组tuple)
        - [切片操作](#切片)
        - [zip](#zip)
        - [enumerate](#enumerate)
    - [无序](#无序)
        - [set](#集合set)
        - [dict](#字典dict)

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

    ` >>> 'hello'*2  => 'hellohello'`

- str[n]: 获取指定下标的字符

- str[-n]: 从后往前数第n个字符
    
- str[start:end]: 截取字符串。start表示开始位置，end表示结束位置（包头不包尾）。如果end为负数表示从后往前的第n个字符为结束位置（也不包括第n个字符）。如果end为空，表示直到字符串末尾。

- 显示中文使用字母u

    ` >>> print u'中文 日文 韩文' => 中文 日文 韩文 `

- 如果中文字符报错，需要在py文件第一行添加注释

    ` # -*- coding:utf-8 -*- ` 
- - -

#### 列表（list）

    使用[]定义，通过索引获取元素。如果使用开始位置和结束位置获取元素，返回的类型还是列表。

    正序访问下标从0开始。倒序访问从-1开始，表示倒数第一。

- append()
    
    追加新元素到列表的末尾

    ```
    L = ['Adam','Lisa','Bart']
    L.append('Paul')
    print L => ['Adam','Lisa','Bart','Paul']
    ```

- insert()

    插入新元素。参数1表示插入的位置；参数2表示插入的元素。

    - 如果在前面的位置插入，原来的元素会依次向后移动；
    - 如果指定的位置查过数组范围，则在数组末尾添加；
    - 如果指定的位置是负数，表示从后向前的第几位中插入，如果负数超过了数组的范围，则会在第一个位置插入。

    ``` 
    L = ['Adam','Lisa','Bart']
    L.insert(0,'Paul')
    print L => ['Paul','Adam','Lisa','Bart']
    ```
    ```
    L = [1,2,3]
    L.insert(-1,4)
    print L => [1,2,4,3]
    ```

- pop()

    删除数组中最后一个元素，并返回该元素。

    - 如果指定参数，表示删除该索引位置的元素；
    - 如果参数为负数，表示从后往前数删除第几个元素
        
        pop()不同于insert()，pop()指定的位置参数不能越界

    ```
    L = [1,2,3]
    del_ele = L.pop()
    print del_ele => 3
    print L => [1,2]
    ```
    ```
    L = [1,2,3]
    del_ele = L.pop(1)
    print del_ele => 2
    print L => [1,3]
    ```

- range()

    生成列表

    ```
    L = range(1,6)
    print L => [1,2,3,4,5]

    L = range(6)
    print L => [0,1,2,3,4,5]
    ```
    ```
    L = [x * x for x in range(1,6)]
    print L => [1,4,9,16,25] = [1*1,2*2,3*3,4*4,5*5]
    ```
    ```
    L = [x * (x+1) for x in range(1,100,2)]
    [1*2,3*4,5*6,...,99*100]

    L = [x * (x+1) for x in range(1,100,3)]
    [1*2,4*5,7*8,...]
    ```
    条件判断
    ```
    L = [x * x for x in range(1,11) if x % 2 == 0]
    print L => [4,16,36,64,100] = [2*2,4*4,6*6,8*8,10*10]
    ```
    多层循环
    ```
    L = [m + n for m in 'ABC' for n in '123']
    print L => ['A1','A2','A3','B1','B2','B3','C1','C2','C3']
    
    L = []
    for m in 'ABC':
        for n in '123':
            L.append(m + n)
    ```
    利用 3 层for循环的列表生成式，找出对称的 3 位数。例如，121 就是对称数，因为从右到左倒过来还是 121。
    ```
    L = [100 * i + 10 * j + k for i in range(1,10) for j in range(10) for k in range(10) if i == k]
    print L => [101,111,121,131,...,989,999]
    ```

- - -
#### 元组（tuple）

    使用()定义
- 如果元组中只有一个元素，返回该元素本身的类型；如果表示只有一个元素的元组，使用(e,)

    ``` 
    t = ()    
    print t => () 
    ```
    ``` 
    t = (1)    
    print t => 1 
    ```
    ``` 
    t = (1,)    
    print t => (1,) 
    ```

- 元组是不可变的，指的是本身的指向不能变。如果元组中的元素包含list，那么list中的元素是可以修改的
    ``` 
    t = (1,2,['x','y'])   
    L = t[2]
    L[0] = 'a'
    L[1] = 'b' 
    print t => (1,2,['a','b']) 
    ```
- - -
#### 切片

    L = [start_index : end_index : step]

    ```
    L = ['Adam','Lisa','Bart','Paul'] 
    
    L[0:3] = L[:3] => ['Adam','Lisa','Bart']

    L[1:3] => ['Adam','Lisa','Bart']

    L[:] => ['Adam','Lisa','Bart','Paul']

    L[::2] => ['Adam','Bart']

    L[-2:] => ['Bart','Paul']

    L[:-2] => ['Adam','Lisa']

    L[-3:-1] => ['Lisa','Bart']

    L[-4,-1,2] => ['Adam','Bart']
    ```
#### zip()

    把两个序列合并成一个由元组组成的list
    ```
    L = zip([10,20,30],['A','B','C'])
    print L => [(10,'A'),(20,'B'),(30,'C')]
    ```
#### enumerate()

    取索引函数，可以使用zip() + range()实现类似效果
    ```
    L = ['Adam','Lisa','Bart'] 
    for index,name in enumerate(L):
        print index, '-', name
    0 - Adam
    1 - Lisa
    2 - Bart
    ```
- - -

### 无序

#### 集合（set）

    无序不可重复，使用set()表示空集

- 创建集合

    ```
    s = set(['a','b','c'])
    print s => set(['a','b','c'])
    ```
    如果list包含重复元素，set会自动去掉重复元素
    ```
    s = set(['a','b','c','c'])
    print s => set['a','b','c']
    print len(s) => 3
    ```

- 集合运算

    -: 差集（保留运算符左边集合中不同与右边集合的元素）

    ```
    s1 = set([1,2,3])
    s2 = set([3,4,5])
    s1 - s2 = set([1,2])
    ```

    &: 交集（两个集合中相同的元素）

    ```
    s1 = set([1,2,3])
    s2 = set([3,4,5])
    s1 & s2 = set([3])
    ```
    |: 并集（把集合中不重复的元素组成一个集合）
    ```
    s1 = set([1,2,3])
    s2 = set([3,4,5])
    s1 | s2 = set([1,2,3,4,5])
    ```
- add()

    添加元素。如果添加的元素已经存在，不会报错

- remove()

    删除元素。如果删除的元素不存在，会报错。

- - -

#### 字典（dict）

    {}表示空字典。key值必须是不可变类型。

- len()

    计算集合的大小

- get(key)

    判断key对应的value，如果key不存在返回None。

- values()

    把一个dict转换成由其中的value组成的list

- itervalues()

    在迭代过程中依次从dict中取出value

- items()

    把dict转成包含tuple的list

    ```
    d = {'Adam':95,'Lisa':85,'Bart':59}
    print d.items() => [('Lisa',85),('Adam',95),('Bart',59)]
    ```

- iteritems()

    在迭代过程中不断给出tuple，不占用额外内存