#### 快排

 - 分而治之  
  - 34561298
  - 分开  left= 345  ; right = 1298,分隔元素是 middle = 6;(奇偶取那个)
  - 使得 left中的每一个元素小于等于middle,right中的每一个元素都大于等于middle
 -


 ```java
   quickSort(array,from,to){
     if(from<to){
       middle = patition(array,from,to);
       quickSort(array,from,middle-1);
       quickSort(array,middle+1,to);
     }
   }

   patition(array,from,to){
     int last = array[to];
     int middle = from-1;
     for (int j=form;j<to ; j++) {
       if(array[j]<=last){
         middle += 1;
         exchange(array[middle],array[j]);
       }
     }

     exchange(array[middle+1],array[to]);
     return middle+1;
   }

   exchange(){

   }

 ```
