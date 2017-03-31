####Validation校验

* 控制层controller：校验页面请求的参数的合法性

* 业务层service(使用较多)：主要校验关键业务参数，仅限于service接口中使用的参数

* 持久层dao：一般是不校验的


####开发过程

* 配置校验器
* 校验器注入到处理器适配器中
* 在POJO中添加校验规则

在需要校验的POJO前面添加`@Validated`，在需要校验的POJO后边添加`BindingResult`接收校验出错信息。

注意：`@Validated`和`BindingResult`是配对出现

####分组校验


####数据回显

定义：表单提交后，如果出现错误，将刚才提交的数据回显到刚才的提交页面。springmvc默认对POJO数据进行回显：POJO数据传入controller方法后，springmvc自动将POJO数据放到request域，key等于pojo类型(首字母小写)，使用@ModelAttribute("items")显式指定key。


@ModelAttribute还可以将方法的返回值传到页面



