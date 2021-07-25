# Gradle in Action

### 使用 Gradle 7.1

```text
------------------------------------------------------------
Gradle 7.1.1
------------------------------------------------------------

Build time:   2021-07-02 12:16:43 UTC
Revision:     774525a055494e0ece39f522ac7ad17498ce032c

Kotlin:       1.4.31
Groovy:       3.0.7
Ant:          Apache Ant(TM) version 1.10.9 compiled on September 27 2020
JVM:          16.0.1 (Homebrew 16.0.1+0)
OS:           Mac OS X 11.5 x86_64
```

### [左移符号失效](https://stackoverflow.com/a/55793096)

> Could not find method leftShift() for arguments...
> 
> << has deprecated in 4.x and removed in 5.0 version

### 命令修正

```shell
# Chapter03 3.2.1
# java -cp build/classes/main com.manning.gia.todo.ToDoApp
# 最好保证 java 的 jvm 和 gradle -v 中显示的 jvm 一致
java -cp build/libs/todo-app.jar com.manning.gia.todo.ToDoApp
```

### 不兼容修正

```shell
# error: Source option 6 is no longer supported. Use 7 or later.
# error: Target option 6 is no longer supported. Use 7 or later.
# sourceCompatibility = 1.7

# warning: [options] source value 7 is obsolete and will be removed in a future release
# warning: [options] target value 7 is obsolete and will be removed in a future release
# warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
sourceCompatibility = 1.8
```

### 命令升级

#### compile -> implementation

* [What's the difference between implementation, api and compile in Gradle?](https://stackoverflow.com/a/44493379)
* [API and implementation separation](https://docs.gradle.org/current/userguide/java_library_plugin.html#sec:java_library_separation)
* [Gradle 依赖配置 api VS implementation](https://www.jianshu.com/p/dd932f951137)

#### runtime -> runtimeOnly

* [runtime finally removed in Gradle 7](https://stackoverflow.com/a/66910991)

#### classesDir -> classesDirs

* [Gradle: Could not get unknown property 'classesDir' for main classes](https://stackoverflow.com/a/57957298)

#### main -> mainClass

> The JavaExec.main property has been deprecated. This is scheduled to be removed in Gradle 8.0. Please use the mainClass property instead. See [JavaExec:main](https://docs.gradle.org/7.1.1/dsl/org.gradle.api.tasks.JavaExec.html#org.gradle.api.tasks.JavaExec:main) for more details.

#### jetty -> gretty-gradle-plugin/gretty

* [Gretty gradle plugin: Getting started](https://gretty-gradle-plugin.github.io/gretty-doc/Getting-started.html)
* [Error while replacing jetty plugin to gretty plugin gradle](https://stackoverflow.com/a/50122733)
* [Error:(2, 0) Plugin with id 'jetty' not found](https://stackoverflow.com/a/53650574)

**启动命令变更**

```shell
# gradle jettyRun
gradle appRun
```

由于 Groovy 2.5 不支持 JDK 16，报错如下:

```text
Exception in thread "main" org.codehaus.groovy.control.MultipleCompilationErrorsException: startup failed:
General error during semantic analysis: Unsupported class file major version 60

java.lang.IllegalArgumentException: Unsupported class file major version 60
```

需要以 JDK 8 版本编译，先设定 gradle jdk 属性:

```shell
~ cat .gradle/gradle.properties
org.gradle.java.home=/Library/Java/JavaVirtualMachines/jdk1.8.0_271.jdk/Contents/Home
```

再将兼容性设定为 1.8:

```shell
# 在项目 build.gradle 加入
sourceCompatibility = 1.8
targetCompatibility = 1.8
```

最终 jetty 成功运行：

```text
gradle appRun
19:53:55 INFO  Jetty 9.4.24.v20191120 started and listening on port 8080
19:53:55 INFO  ToDo Application runs at:
19:53:55 INFO    http://localhost:8080/todo-webapp-customized
```

**DSL: jettyRun -> gretty**, 参考 [Gretty configuration](https://gretty-gradle-plugin.github.io/gretty-doc/Gretty-configuration.html).
