#### jar管理

- 底层管理逻辑
```
WatchService  监控文件夹变化

ModuleXmlApplicationContext  
setclassloader
refresh
setConfigLocations

抽象一个Module
{
  ModuleXmlApplicationContext context;
  String name;
  String desc;
  Date create;
}

抽象一个ModuleManager
{
  get
  rigester  add-map
  remove
}

实现里面放个 map
```
