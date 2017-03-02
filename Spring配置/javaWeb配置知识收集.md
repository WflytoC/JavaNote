SpringMVC的配置文件本质上是配置Bean(java类)的

####spring.profiles.active 针对多种启动环境的spring配置

工程一般在会跑在正式环境、测试环境上，当打包或者运行的时候，切换数据库信息可能会是很麻烦的问题。

在spring配置文件中配置两种环境信息：

	<beans profile="dev">  
        <context:property-placeholder location="classpath:jdbc-dev.properties"/>  
    </beans>  

    <beans profile="prd">  
        <context:property-placeholder location="classpath:jdbc-prd.properties"/>  
    </beans> 

在web.xml中配置使用哪种环境信息，tomcat启动的时候自动去加载对应的环境信息：

	<context-param>  
        <param-name>spring.profiles.active</param-name>  
        <param-value>dev</param-value>  
    </context-param>