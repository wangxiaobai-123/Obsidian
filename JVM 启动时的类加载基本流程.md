
## 启动步骤

1. **JVM 启动，Bootstrap ClassLoader 加载核心 API**
   - Bootstrap ClassLoader 是启动类加载器，由 C++ 实现，负责加载 Java 核心类库（`rt.jar` 等）。
   - 同时，`ExtClassLoader` 和 `AppClassLoader` 也在此时被 Bootstrap ClassLoader 加载，因为它们本身也属于核心 API 的一部分（`sun.misc.Launcher$ExtClassLoader`、`sun.misc.Launcher$AppClassLoader`）。

2. **ExtClassLoader 加载扩展 API**
   - 扩展类加载器负责加载 `java.ext.dirs` 系统属性所指定的目录下的类库，或者在 Java 9+ 之后变为平台类加载器，负责加载平台模块。

3. **AppClassLoader 加载 CLASSPATH 下的类**
   - 应用程序类加载器负责加载用户类路径（`CLASSPATH`）下定义的类，即你自己的程序代码。

> 这种层层委派的加载逻辑正是 [[双亲委派模型]] 在 JVM 启动时的具体体现。

## 启动流程图示

JVM 启动  
|  
v  
Bootstrap ClassLoader (加载核心 API，同时加载 ExtClassLoader 和 AppClassLoader)  
|  
v  
ExtClassLoader (加载扩展/平台 API)  
|  
v  
AppClassLoader (加载 CLASSPATH 下的程序类)


## 一句话概括
> JVM 启动时，Bootstrap 加载核心并“生下” Ext 和 App，Ext 加载扩展类，App 加载你的程序类，层层递进，本质还是[[双亲委派模型]]的那一套委派机制。
