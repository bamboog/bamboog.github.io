#### 一致性hash
- 做一个hash环
- 资源hash  到环上
- input hash 到环
- 寻找顺时针最近的资源节点

```java
// put
treeMap.put(ip.hashCode());  //

//get
tail = treeMap.tailMap(key);
if(tail == null){
  treeMap.get(treeMap.getFirstKey());
}else {
  treeMap.get(tail.getFirstKey());
}

```
