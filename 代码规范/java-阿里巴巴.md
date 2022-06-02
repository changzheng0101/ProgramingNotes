IDE中的换行必须使用UNIX格式，不能用Windows格式





equals容易空指针异常，尽量不要让里面的值为object

```java
"test".equals(object) //不推荐
object.equals("test") //推荐
```



包装类对象都用equals来判断是否相等



构造函数中不允许插入逻辑，如果有逻辑，放到init方法中



方法顺序 公有保护>私有>getter&setter



get和set中不要增加业务逻辑



重写equals，必须也实现hashcode



```
List<String> a = new ArrayList<String>(); 
list.add("1"); 
list.add("2"); 
for (String item : list) { 
if ("1".equals(item)) { 
list.remove(item); 
} 
} 
//可能出错代码

```





线程资源必须通过线程池提供，不能自行显式创建线程



