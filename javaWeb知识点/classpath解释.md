####classpath:和classpath*:的区别

一般的工程结构src/main/java和src/main/resources都属于classpath，前者存放java源代码，后者存放资源文件，比如配置文件，默认情况下，src/main/java目录只打包源代码，而不会打包其它文件。

`classpath`本质是jvm的根路径，jvm获取资源都是从该根路径下找的，注意这个根路径是个逻辑路径，并不是磁盘路径。

一般classpath指向的是classes，也就是编译路径的根路径，而一般classes中放着这些文件:

* java文件编译好的class文件
* properties配置文件
* xml配置文件


`classpath:`只会到你的classes路径中查找找文件。`classpath*:`不仅会到classes路径，还包括jar文件中(classes路径)进行查找