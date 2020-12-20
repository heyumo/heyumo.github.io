---
title: MybatisPlus
categories:
	
date: 2019-12-10 22:32:32
notshow: true
---

MybatisPlus 知识总览

#### 一、简介与集成 MybatisPlus

	MyBatis-Plus(简称 MP),是一个 MyBatis 的增强工具包，只做增强不做改变. 为简化开 发工作、提高生产率而生   
我们的愿景是成为 Mybatis 最好的搭档，就像 魂斗罗 中的 1P、2P，基友搭配，效率 翻倍。 

文档发布地址: https://mp.baomidou.com/

 pom.xml  依赖配置 
 
 ``` java
     <!-- mp 依赖 --> 
	 <dependency> 
		<groupId>com.baomidou</groupId> 
		<artifactId>mybatis-plus</artifactId>  
		<version>2.3</version> 
	  </dependency>   
 ```
	  特别说明: Mybatis 及 Mybatis-Spring 依赖请勿加入项目配置，以免引起版本冲突！！！ Mybatis-Plus 会自动帮你维护！ 
 

#### 二、MP的CRUD

1) 提出问题:  假设我们已存在一张 tbl_employee 表，且已有对应的实体类 Employee，实现 tbl_employee 表的 CRUD 操作我们需要做什么呢？ 
2) 实现方式: 基于 Mybatis    需要编写 EmployeeMapper 接口，并手动编写 CRUD 方法  提供 EmployeeMapper.xml 映射文件，并手动编写每个方法对应的 SQL 语句. 
	基于 MP  只需要创建 EmployeeMapper 接口, 并继承 BaseMapper 接口.这就是使用 MP 
    需要完成的所有操作，甚至不需要创建 SQL 映射文件。 
	
	插入操作 :
	1) Integer insert(T entity); 
	2) @TableName
	3) 	全局的 MP 配置: <property name="tablePrefix" value="tbl_"></property> 
	4) @TableField 
	5) 全局的 MP 配置: <property name="dbColumnUnderline" value="true"></property>
	6) @TableId 
	7) 全局的 MP 配置: <property name="idType" value="0"></property>
	8) 支持主键自增的数据库插入数据获取主键值 Mybatis: 需要通过 useGeneratedKeys  以及  keyProperty 来设置 MP: 自动将主键值回写到实体类中 
	9) Integer  insertAllColumn(T entity) 
	
#### 三、条件构造器 EntityWrapper 

1) Mybatis-Plus 通过 EntityWrapper（简称 EW，MP 封装的一个查询条件构造器）或者 Condition（与 EW 类似） 来让用户自由的构建查询条件，简单便捷，没有额外的负担， 能够有效提高开发效率 
2) 实体包装器，主要用于处理 sql 拼接，排序，实体参数查询等 
3) 注意: 使用的是数据库字段，不是 Java 属性! 

``` java
	List<Employee> userList = employeeMapper.selectPage( 
	new Page<Employee>(2, 3),         
	new EntityWrapper<Employee>().eq("last_name", "MybatisPlus")     
	.eq("gender", 1)    
	.between("age", 18, 50)   ); 
	
```
#### 四、ActiveRecord(活动记录)  

Active Record(活动记录)，是一种领域模型模式，特点是一个模型类对应关系型数据库中的 一个表，而模型类的一个实例对应表中的一行记录。 
 
ActiveRecord 一直广受动态语言（ PHP 、 Ruby 等）的喜爱，而 Java 作为准静态语言， 对于 ActiveRecord 往往只能感叹其优雅，所以 MP 也在 AR 道路上进行了一定的探索 

#### 五、代码生成器 
1) MP 提供了大量的自定义设置，生成的代码完全能够满足各类型的需求 
2) MP 的代码生成器  和 Mybatis MBG 代码生成器: MP 的代码生成器都是基于 java 代码来生成。
	MBG 基于 xml 文件进行代码生成 MyBatis 的代码生成器可生成: 实体类、Mapper 接口、Mapper 映射文件 
	MP 的代码生成器可生成: 实体类(可以选择是否支持 AR)、Mapper 接口、Mapper 映射文件、 Service 层、Controller 层.   
			

#### 六、MP插件
分页插件 ：
	com.baomidou.mybatisplus.plugins.PaginationInterceptor 
执行分析插件 ：1) com.baomidou.mybatisplus.plugins.SqlExplainInterceptor

性能分析插件 ：1) com.baomidou.mybatisplus.plugins.PerformanceInterceptor 
				2) 性能分析拦截器，用于输出每条 SQL 语句及其执行时间 
				3) SQL 性能执行分析,开发环境使用 ， 超过指定时间，停止运行。有助于发现问题 
				
乐观锁插件 ：com.baomidou.mybatisplus.plugins.OptimisticLockerInterceptor
			2)如果想实现如下需求: 当要更新一条记录的时候，希望这条记录没有被别人更新 
			
#### 七、自定义全局操作 
		
		根据 MybatisPlus 的 AutoSqlInjector 可以自定义各种你想要的 sql ,注入到全局中，相当于自 定义 Mybatisplus 自动注入的方法。 
		之前需要在 xml 中进行配置的 SQL 语句，现在通过扩展 AutoSqlInjector 在加载 mybatis 环境 时就注入。 

#### 八、公共字段自动填充 

```java
	com.baomidou.mybatisplus.mapper.MetaObjectHandler 
	insertFill(MetaObject metaObject) 
	updateFill(MetaObject metaObject) 
```
#### 九、Oracle 主键 Sequence 

MySQL:   支持主键自增。 IdType.Auto 
Oracle:   序列(Sequence) 
 1) 实体类配置主键 Sequence  @KeySequence(value=”序列名”，clazz=xxx.class 主键属性类 型) 
 2) 全局 MP 主键生成策略为 IdType.INPUT  
 3) 全局 MP 中配置 Oracle 主键 Sequence 
	com.baomidou.mybatisplus.incrementer.OracleKeyGenerator 
4) 可以将@keySequence 定义在父类中，可实现多个子类对应的多个表公用一个 Sequence 
#### 十、Idea 快速开发
	快速开发插件，为效率而生. 
	MybatisX:File -> Settings -> Plugins -> Browse Repositories.. 输入 mybatisx 安装下载 