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
