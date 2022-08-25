---
title: Kotlin Base

date: 2022-08-25 11:47:53

description: Kotlin 基础教程

keywords: Kotlin

tags: 
  - Kotlin
  - Android
  - 
categories: Kotlin

---

## HelloWorld

```kotlin
package hello                      //  可选的包头
 
fun main(args: Array<String>) {    // 包级可见的函数，接受一个字符串数组作为参数
   println("Hello World!")         // 分号可以省略
}
```
### 面向对象
```kotlin
class Greeter(val name: String) {
   fun greet() { 
      println("Hello, $name")
   }
}
 
fun main(args: Array<String>) {
   Greeter("World!").greet()          // 创建一个对象不用 new 关键字
}
```
### 为什么选择 Kotlin？
简洁: 大大减少样板代码的数量。
安全: 避免空指针异常等整个类的错误。
互操作性: 充分利用 JVM、Android 和浏览器的现有库。
工具友好: 可用任何 Java IDE 或者使用命令行构建。

### Kotlin 使用命令行编译
Kotlin 命令行编译工具下载地址：https://github.com/JetBrains/kotlin/releases/tag/v1.1.2-2，目前最新为 1.1.2-2。

你可以选择一个最新的稳定版下载。

下载完成后，解压到指定目录，然后将 bin 目录添加到系统环境变量。bin 目录包含编译和运行 Kotlin 所需的脚本。

### SDKMAN!
在 OS X、Linux、Cygwin、FreeBSD 和 Solaris 系统上也可以使用更简单的安装方法，命令如下：
``` kotlin
$ curl -s https://get.sdkman.io | bash
$ sdk install kotlin
```
### Homebrew
在 OS X 下，你可以使用 Homebrew 安装：
``` kotlin
$ brew update
$ brew install kotlin
```
### MacPorts
如果你是 MacPorts 用户，可以使用以下命令安装：
``` kotlin
$ sudo port install kotlin
```

## 创建和运行第一个程序
创建一个名为 hello.kt 文件，代码如下：
``` kotlin
hello.kt
fun main(args: Array<String>) {
    println("Hello, World!")
}
```
使用 Kotlin 编译器编译应用:
``` kotlion
$ kotlinc hello.kt -include-runtime -d hello.jar
```
-d: 用来设置编译输出的名称，可以是 class 或 .jar 文件，也可以是目录。
-include-runtime : 让 .jar 文件包含 Kotlin 运行库，从而可以直接运行。
如果你想看所有的可用选项，运行:
``` kotlin
$ kotlinc -help
```
运行应用
``` kotlin
$ java -jar hello.jar
Hello, World!
```
### 编译成库
若需要将生成的 jar 包供其他 Kotlin 程序使用，可无需包含 Kotlin 的运行库：
``` kotlin
$ kotlinc hello.kt -d hello.jar
```
由于这样生成的 .jar 文件不包含 Kotlin 运行库，所以你应该确保当它被使用时，运行时在你的 classpath 上。

你也可以使用 kotlin 命令来运行 Kotlin 编译器生成的 .jar 文件
``` kotlin
$ kotlin -classpath hello.jar HelloKt
```
HelloKt 为编译器为 hello.kt 文件生成的默认类名。

运行 REPL（交互式解释器）
我们可以运行如下命令得到一个可交互的 shell，然后输入任何有效的 Kotlin 代码，并立即看到结果

![image-20220825114103310](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220825114103310.png)

使用命令行执行脚本
Kotlin 也可以作为一个脚本语言使用，文件后缀名为 .kts 。

例如我们创建一个名为 list_folders.kts，代码如下：
``` kotlin
import java.io.File
val folders = File(args[0]).listFiles { file -> file.isDirectory() }
folders?.forEach { folder -> println(folder) }
```
执行时通过 -script 选项设置相应的脚本文件。
``` kotlin
$ kotlinc -script list_folders.kts <path_to_folder>$ kotlinc -script list_folders.kts
```

## Kotlin Android 环境搭建

### 安装 Kotlin 插件

Android Studio 从 3.0（preview）版本开始将内置安装 Kotlin 插件。

打开 Settings ( Mac 为 Preferences) 面板，在右侧找到 Plugins 选项 (快捷键 Ctrl+, Mac 下为 command+)，搜索框输入 "Kotlin" 查找，点击 Search in repositories(仓库中搜索)，然后安装即可，安装完成之后需要重启 Android Studio。

![image-20220825114206140](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220825114206140.png)

![image-20220825114218887](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220825114218887.png)

### 创建新工程

选择 Start a new Android Studio project 或者 File | New project，大多数选项均有默认值 ，只需要按几次"回车"键即可。

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495853720-4994-0-create-new-project.png)

Android Studio 3.0 在当前对话框中提供启用 Kotlin 支持的选项，勾选后可以跳过 "配置 Kotlin 工程（Configuring Kotlin in the project）"的步骤。

选择 Android 版本:

![image-20220825114303851](https://cdn.zenless.top/gh/zhonghanlu/PicGo/img/image-20220825114303851.png)

选择需要创建的 Activity 样式:

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495853838-1520-0-create-new-project.png)

命名该 Activity:

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495853838-8955-1-create-new-project.png)

在 Android Studio 3.0 中，可以选择使用 Kotlin 创建 activity，因此也不需要"将Java 代码转换为 Kotlin（Converting Java code to Kotlin）"这一步骤。

早期版本中则会先使用 Java 创建 activity，然后再使用自动转换工具 进行转换。

### 将 Java 代码转换为 Kotlin

重新打开Android Studio，新建一个Android项目吧，添加一个默认的MainActivity

打开 MainActivity.java 文件，通过菜单栏依次调出 Code | Convert Java File to Kotlin File：

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854751-7389-convert-java-to-kotlin.png)

转换完成后即可看到使用 Kotlin 编写的 activity。

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854753-3864-converted-code.png)

### 工程中配置 Kotlin

在开始编辑此文件时，Android Studio 会提示当前工程还未配置 Kotlin，根据提示完成操作即可，或者可以在菜单栏中选择 Tools

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854757-6620-kotlin-not-configured.png)

选择配置时有如下对话框，选择已安装的最新版本即可。

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854752-7001-re-kotlin-in-project-details.png)

Kotlin 配置完成后，应用程序的 build.gradle 文件会更新。 你能看到新增了 apply plugin: 'kotlin-android' 及其依赖。

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854750-1825-sync-project-with-gradle.png)

同步工程，在提示框中点击"立即同步（Sync Now）"或者使用 Sync Project with Gradle Files命令。

![img](https://www.runoob.com/wp-content/uploads/2017/05/1495854764-6190-sync-project-with-gradle-2.png)

## Kotlin 基础语法

 

## 结束

暂且结束   转载菜鸟教程+自我理解
