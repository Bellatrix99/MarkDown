apply示例:

**[javascript]**[
](http://blog.csdn.net/myhahaxiao/article/details/6952321#)

 <script type="text/javascript"> 

 

```javascript
/*定义一个人类*/ 

 **function Person(name,age)** 

 { 

    **this.name=name;** 

    **this.age=age;** 

  } 

  /*定义一个学生类*/ 

  function Student(name,age,grade) 

  { 

    Person.apply(**this,arguments);** 

    **this.grade=grade;** 

  } 

  //创建一个学生类 

  **var student=\**new Student("zhangsan",21,"一年级");\**** 

  //测试 

  alert("name:"+student.name+"\n"+"age:"+student.age+"\n"+"grade:"+student.grade); 

  //大家可以看到测试结果name:zhangsan age:21 grade:一年级 

  //学生类里面我没有给name和age属性赋值啊,为什么又存在这两个属性的值呢,这个就是apply的神奇之处. 
```

</script> 



分析: Person.apply(this,arguments);

this:在创建对象在这个时候代表的是student

arguments:是一个数组,也就是[“zhangsan”,”21”,”一年级”];

​          也就是通俗一点讲就是:用student去执行Person这个类里面的内容,在Person这个类里面存在this.name等之类的语句,这样就将属性创建到了student对象里面

