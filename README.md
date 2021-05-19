# mybatisplus-maven-plugin

### 一、简介

  * mybatis-plus 代码生成工具的 maven 插件版本

### 二、使用方法

  * 在项目的pom文件中配置以下内容

```xml
<plugin>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatisplus-maven-plugin</artifactId>
    <version>1.0</version>
    <configuration>
        <!-- 输出目录(默认java.io.tmpdir) -->
        <outputDir>${project.basedir}/src/main/java</outputDir>
        <!-- 是否覆盖同名文件(默认false) -->
        <fileOverride>true</fileOverride>
        <!-- mapper.xml 中添加二级缓存配置(默认true) -->
        <enableCache>false</enableCache>
        <!-- 开发者名称 -->
        <author>chenmin</author>
        <!-- 是否开启 ActiveRecord 模式(默认true) -->
        <activeRecord>false</activeRecord>
        <!-- 数据源配置，( **必配** ) -->
        <dataSource>
            <driverName>com.mysql.cj.jdbc.Driver</driverName>
            <url>jdbc:mysql://127.0.0.1:3306/test</url>
            <username>root</username>
            <password>root</password>
        </dataSource>
        <strategy>
            <!-- 字段生成策略，四种类型，从名称就能看出来含义：
                            nochange(不做任何改变，原样输出),
                            underline_to_camel,(下划线转驼峰命名)
                            remove_prefix,(仅去掉前缀)
                            remove_prefix_and_camel(去掉前缀并且转驼峰)
                            remove_underline(去掉第一个下划线之前内容，后面原样输出)
                            remove_underline_and_camel(去掉第一个下划线之前内容，后面转驼峰) -->
            <naming>remove_underline_and_camel</naming>
            <fieldNaming>underline_to_camel</fieldNaming>
            <!-- 表前缀 -->
            <tablePrefix>tb_</tablePrefix>
            <!--Entity中的ID生成策略（默认 id_worker）-->
            <idGenType>assign_id</idGenType>
            <!--自定义超类-->
            <superMapperClass>com.baomidou.mybatisplus.core.mapper.BaseMapper</superMapperClass>
            <superServiceClass>com.baomidou.mybatisplus.extension.service.IService</superServiceClass>
            <superServiceImplClass>com.baomidou.mybatisplus.extension.service.impl.ServiceImpl</superServiceImplClass>
        </strategy>
        <packageInfo>
            <!-- 父级包名称，如果不写，下面的service等就需要写全包名(默认com.baomidou) -->
            <parent>com.test</parent>
            <!--service包名(默认service)-->
            <service>service.interfaces</service>
            <!--serviceImpl包名(默认service.impl)-->
            <serviceImpl>service.impl</serviceImpl>
            <!--entity包名(默认entity)-->
            <entity>bean</entity>
            <!--mapper包名(默认mapper)-->
            <mapper>mapper</mapper>
            <!--xml包名(默认mapper.xml)-->
            <xml>${project.basedir}/src/main/resources/mapper</xml>
            <controller>controller</controller>
        </packageInfo>
        <template>
            <!-- 定义controller模板的路径 -->
            <!--<controller>/template/controller1.java.vm</controller>-->
        </template>
    </configuration>
    <dependencies>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.19</version>
        </dependency>
    </dependencies>
</plugin>
```

- 执行

下载源码的同学！可使用mvn clean install将自定义的这个插件安装到本地仓库。
执行：`mvn clean install`

命令：`mvn com.baomidou:mybatisplus-maven-plugin:1.0:code`

显然这个命令太长了，使用很不方便，可在settings.xml中配置如下：

```xml
<pluginGroups>
	<pluginGroup>com.baomidou</pluginGroup>
</pluginGroups>
```
然后使用简单命令：`mvn mp:code`

