# java中常用的工具类(2) System

System工具类也是java中常用的一个工具类，并且从java 1.0 时代就存在了。它是不能被实例化的。下面是官方介绍
> The System class contains several useful class fields and methods. It cannot be instantiated.
Among the facilities provided by the System class are standard input, standard output, and error output streams; access to externally defined properties and environment variables; a means of loading files and libraries; and a utility method for quickly copying a portion of an array.

以下介绍System的常用方法
### 流相关
```java
// 设置标准输入流
public static void setIn(InputStream in);
// 设置标准输出流
public static void setOut(PrintStream out);
// 设置标准错误输出流
public static void setErr(PrintStream err);
```
以上的流就会在System的标准流中使用
```java
System.in.read();
System.out.println();
System.err.println();
```
获取一个基础虚拟机的流通道
```java
// Returns the channel inherited from the entity that created this Java virtual machine.
// This method returns the channel obtained by invoking the inheritedChannel method of the system-wide default SelectorProvider object.
// In addition to the network-oriented channels described in inheritedChannel, this method may return other kinds of channels in the future.
public static Channel inheritedChannel() throws IOException

System.out.println(System.inheritedChannel());//null
```
### 安全相关
设置或获取 java虚拟机的安全管理器。这个我用的比较少，大家看注释吧。
```java
// Sets the System security.
// If there is a security manager already installed, this method first calls the security manager's checkPermission method with a RuntimePermission("setSecurityManager") permission to ensure it's ok to replace the existing security manager. This may result in throwing a SecurityException.
public static void setSecurityManager(final SecurityManager s);

// if a security manager has already been established for the current application, then that security manager is returned; otherwise, null is returned.
public static SecurityManager getSecurityManager();

// 默认
System.out.println(System.getSecurityManager());// null
```

### 控制台
获取java的控制台对象，关于控制台命令交互可以通过这里获取
```java
// Returns the unique Console object associated with the current Java virtual machine, if any.
// Returns: The system console, if any, otherwise null. 
// Since: 1.6
public static Console console()
```

### 时间相关
这应该是大家使用最频繁的几个接口。
- 毫秒
```java
// 获取当前系统时间戳（公元1970.1.1 凌晨到现在的毫秒数），native虚拟机实现
// the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.
public static native long currentTimeMillis();

```
- 纳秒精度数

获取当前系统的纳秒精度的数（基于当前虚拟机）。这个数是依据当前虚拟机的一个原点计算出来的一个高精度值，与具体的时间无关（比如毫秒方法获取的是1970到今天的时间戳，但纳秒的原点不是具体的某个时间点）   
所以，这个方法的用处也就有了，就是基于同一个虚拟机的纳秒级精度的前后时间比较。  
因为数据比较大，可以会有越界风险
```java
// Returns the current value of the running Java Virtual Machine's high-resolution time source, in nanoseconds.
// This method can only be used to measure elapsed time and is not related to any other notion of system or wall-clock time. The value returned represents nanoseconds since some fixed but arbitrary origin time (perhaps in the future, so values may be negative). The same origin is used by all invocations of this method in an instance of a Java virtual machine; other virtual machine instances are likely to use a different origin.
public static native long nanoTime();
```

### 数据拷贝
说实话，不太理解为什么这个方法会放在这里。可能在虚拟机底层里，数组copy是一个基础功能吧。  
很常用。
```java
// 将src数组srcPos位置开始的length元素复制到dest数组中，从dest数组中的destPos开始。
public static native void arraycopy(Object src,  int  srcPos,Object dest, int destPos, int length);
```

### hash
返回对象的默认hashcode（即时被覆盖也不执行覆盖方法）  
null 返回0
```java
// Returns the same hash code for the given object as would be returned by the default method hashCode(), whether or not the given object's class overrides hashCode(). The hash code for the null reference is zero.
public static native int identityHashCode(Object x);
```

### 系统属性
- 系统属性列表
```java
// Key :  Description of Associated Value
// java.version :  Java Runtime Environment version
// java.vendor : Java Runtime Environment vendor
// java.vendor.url: Java vendor URL
// java.home:  Java installation directory
// java.vm.specification.version : Java Virtual Machine specification version
// java.vm.specification.vendor : Java Virtual Machine specification vendor
// java.vm.specification.name : Java Virtual Machine specification name
// java.vm.version : Java Virtual Machine implementation version
// java.vm.vendor : Java Virtual Machine implementation vendor
// java.vm.name : Java Virtual Machine implementation name
// java.specification.version : Java Runtime Environment specification version
// java.specification.vendor : Java Runtime Environment specification vendor
// java.specification.name : Java Runtime Environment specification name
// java.class.version : Java class format version number
// java.class.path : Java class path
// java.library.path : List of paths to search when loading libraries
// java.io.tmpdir : Default temp file path
// java.compiler : Name of JIT compiler to use
// java.ext.dirs : Path of extension directory or directories Deprecated. This property, and the mechanism which implements it, may be removed in a future release.
// os.name : Operating system name
// os.arch : Operating system architecture
// os.version : Operating system version
// file.separator : File separator ("/" on UNIX)
// path.separator : Path separator (":" on UNIX)
// line.separator : Line separator ("\n" on UNIX)
// user.name : User's account name
// user.home : User's home directory
// user.dir : User's current working directory
public static Properties getProperties()


```
- 设置/替换系统属性

```java
// 设置系统属性：props 换替换原来的系统属性，而非新增
public static void setProperties(Properties props)

```

- 设置key属性

```java
// 设置key的属性，并返回上一个value值
public static String setProperty(String key, String value) 

```

- 删除key属性

```java
// 删除key ，并返回上个value值
public static String clearProperty(String key)

```

- 查询key属性

```java
//根据key 查属性值
public static String getProperty(String key)
// 根据key 查属性值，查不到返回默认值
public static String getProperty(String key, String def)

```

- 系统换行符

linux/unix : \n
windows: \r\n

```java
// On UNIX systems, it returns "\n"; on Microsoft Windows systems it returns "\r\n".
public static String lineSeparator()
```

- 系统环境变量

```java
// 全部环境变量 k：v
public static java.util.Map<String,String> getenv()

// 某个k的环境变量值
public static String getenv(String name)

```

### 系统相关
- 退出

以某个状态终止虚拟机：非0 code 表示非正常结束
```java
// Terminates the currently running Java Virtual Machine. The argument serves as a status code; by convention, a nonzero status code indicates abnormal termination.
// This method calls the exit method in class Runtime. This method never returns normally.
public static void exit(int status) {
    Runtime.getRuntime().exit(status);
}

```

- 垃圾回收

执行垃圾回收
```java
// Runs the garbage collector.
public static void gc() {
    Runtime.getRuntime().gc();
}
```

- 执行Finalization

```java
public static void runFinalization() {
    Runtime.getRuntime().runFinalization();
}
```