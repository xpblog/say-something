# [如何使Map不能再新增元素？](https://github.com/xpblog/say-something/issues/17)

[返回目录](https://github.com/xpblog/say-something)

Map不能再新增元素，有人会想到final修饰，但是map是引用对象，所以final只能保证Map map = new HashMap<>()的引用地址不变，并不能保证map里的元素不能新增。

### 利用Collections类提供的方法
`Map map = Collections.unmodifiableMap(map)`，这样如果再往map中添加元素就会报错。

### 自己对map封装
```java
public class MyMap<K,V> {

    private final Map<K,V> map = new ConcurrentHashMap<>();

    public MyMap(Map<K,V> map) {
        map.forEach(this.map::put);
    }

    public V get(K key) {
        return map.get(key);
    }
}
```