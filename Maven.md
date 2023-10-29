# Maven

到官网下载Maven包

解压后配置环境变量

配置bin目录下的setting.xml文件，修改本地文件存放位置+配置阿里云私服



### 配置idea

setting——maven

修改Maven home path & User setting file & User repo



### Maven常用命令

1. 编译：mvn compile
2. 清理：mvn clean
3. 测试：mvn test
4. 打包：mvn package
5. 安装：mvn install

### Maven生命周期

clean——default——site

maven在同一生命周期内，执行后面的命令会自动执行前面的



### maven坐标

1. groupld:定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima)
2. artifactld:定义当前Maven项目名称（通常是模块名称，例如order-service、goods-service)
3. version:定义当前项目版本号

例如：

``````
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>5.1.46</version>
</dependency>
``````

### idea导入maven文件

右侧maven添加，选中项目的pol.xml文件，导入即可

### maven插件

maven Helper

可以右键文件夹run或debug maven

### Maven依赖管理

使用坐标导入jar包

Web:https://mvnrepository.com/

1. 在pom.xml文件中编写<dependencies>标签
2. 使用<dependencies>标签中使用<dependency>引入坐标
3. 定义坐标的groupId, artifactld, version
4. 点击**刷新**按钮，使坐标生效

#### 依赖范围

通过设置坐标的依赖范围（scope），可以设置对应的jar包作用范围，默认值为compile

![1698498735006](/Users/fog/Documents/笔记/1698498735006.png)

| 依赖范围 | 编译classpath | 测试classpath | 运行classpath |       例子        |
| :------: | :-----------: | :-----------: | :-----------: | :---------------: |
| compile  |       Y       |       Y       |       Y       |      logback      |
|   test   |       -       |       Y       |       -       |       Junit       |
| provided |       Y       |       Y       |       -       |    Servlet-api    |
| runtime  |       -       |       Y       |       Y       |       jdbc        |
|  system  |       Y       |       Y       |       -       | 存储在本地的jar包 |
|  improt  |               |               |               |                   |

