# hello_word
哈哈绿毛鹦鹉
3.23 
aop 事物管理
1.>
<!-- 事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
<property name="dataSource" ref="dataSource"></property>
</bean>
<!-- 申明建议 -->
<tx:advice id="aopAdvice">
<tx:attributes>
<!--SUPPORTS 表示如果当前上下文环境  中存在事物则用，不存在则不用-->
<tx:method name="list*" propagation="SUPPORTS"/>
<!--REQUIRED 当前操作必须使用事物进行管理  -->
<tx:method name="delete*" propagation="REQUIRED"/>
<tx:method name="save*" propagation="REQUIRED"/>
<tx:method name="update*" propagation="REQUIRED"/>
</tx:attributes>
</tx:advice>
<!-- aop配置 
 proxy-target-class如果为true表示采用jdk动态代理实现
如果为false则表示采用cglib实现
-->
<aop:config proxy-target-class="true">
<!-- 申明切点 -->
<aop:pointcut expression="execution(* com.service..*.(..))" id="pointCut"/>
<!-- 给切点建议 -->
<aop:advisor advice-ref="aopAdvice" pointcut-ref="pointCut"/>
</aop:config>


2、>注解形式

<!-- 事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
<property name="dataSource" ref="dataSource"></property>
</bean>
<!-- 开启spring的注解形式 -->
<tx:annotation-driven  transaction-manager="transactionManager"/>

在service中头   @Transactional

每个方法上 @Transactional(propagation=Propagation.REQUIRED)

查询可以不写 或 @Transactional(propagation=Propagation.NOT_SUPPORTED)
