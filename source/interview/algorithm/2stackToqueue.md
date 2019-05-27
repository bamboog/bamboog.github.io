
#####
```
one_stack,two_stack,queue
```
 - queue.put
   - one_stack.push

 - queue.get
  ```java
  if(two_stack.size>0) {
    two_stack.pop();
  }else{
   while(one_stack.size>0){
     two_stack.push(one_stack.pop());
   }
   if(two_stack.size()>0){
     two_stack.pop();
   }
  }
  ```
