# 设计模式

### Builder Pattern

### Singleton Pattern

```
# 第一种方式，直接创建实例对象

public class Singleton {

    private Singleton() {}

    private static Singleton uniqueInstance = new Singleton();

    public static Singleton getInstance() {
        return uniqueInstance;
    }
}
```
```
# 第二种方式，延迟创建实例对象。此方法在多线程环境下会出现创建多个实例对象的问题。

public class Singleton {

    private Singleton() {}

    private static Singleton uniqueInstance;

    public static Singleton getInstance() {
        if(uniqueInstance == null)
            uniqueInstance = new Singleton();
        return uniqueInstance;
    }
}
```
```
# 第三种方式，使用锁机制来保证在多线程环境下只创建一个实例。使用synchronized会降低程序性能

public class Singleton {

    private Singleton() {}

    private static Singleton uniqueInstance;

    public synchronized static Singleton getInstance() {
        if(uniqueInstance == null)
            uniqueInstance = new Singleton();
        return uniqueInstance;
    }
}
```
```
# 第四种方式，使用双重检查加锁，只在第一次创建时进行同步以提高程序性能

public class Singleton {

    private Singleton() {}

    private volatile static Singleton uniqueInstance;

    public static Singleton getInstance() {
        if(uniqueInstance == null) {
            synchronized(Singleton.class) {
                if(uniqueInstance == null)
                    uniqueInstance = new Singleton();
            }
        }
        return uniqueInstance;
            
    }
}
```