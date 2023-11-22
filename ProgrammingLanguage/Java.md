## Java基础

#### 如何编译运行java文件

1. 找到要编译的java文件的路径
2. 编译命令：javac + 文件名.java
3. 编译成功后会生成一个class文件
4. 运行命令：java + 文件名



**Example:**  HelloWorld.java

```java
public class HelloWorld{
  public static void main(String[] args){
        System.out.println("HelloWorld.");
  }
}
```

编译：javac HelloWorld.java

运行：java HelloWorld



#### 注释，关键字和字面量

**注释分类：**

1. 单行注释  格式：//注释信息
2. 多行注释  格式：斜杠+星号 + 注释信息 + 星号+斜杠  例：/*注释信息*/
3. 文档注释  格式：斜杠+星号+星号 + 注释信息 + 星号+斜杠  例：/**注释信息*/

**关键字：**被java赋予了特定含义的英文单词   例：class，class用于（创建/定义）一个类，类是java最基本的组成单元

> 关键字全部==小写==

**字面量：**数据在程序中的书写格式

| 字面量类型 | 说明及举例 |
| :--------- | ---------- |
| 整数类型   | 不带小数点的数字  例：890，-87              |
| 小数类型   | 带小数点的数字  例：1.2                     |
| 字符串类型 | 用双引号括起来的内容  例："HelloWorld"      |
| 字符类型   | 用单引号括起来的，且内容只能有一个  例：'A' |
| 布尔类型   | 布尔值，表示真假（只有两个值：true or false） |
| 空类型     | 一个特殊的值，空值，值为null |
