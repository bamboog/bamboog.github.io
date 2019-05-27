####  LRU
```
Least recently used
- put的时候，如果满了，应该谁被踢出

那么，
get的时候，记录get的次数 。。。 lru_k
等等，是否可以直接移动到头部，put的时候放到头，删除尾部就行  --  lru
```

- 实现
```java
    map = new LinkedHashMap<Integer, Integer>(capacity, 0.75f, true){
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > CAPACITY;
            }
        };
```
