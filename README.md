# Gradle in Action

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
