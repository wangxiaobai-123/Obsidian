# Maven 默认约定与规则

## 1. 标准项目目录结构
- 项目主代码：`src/main/java/`
- 项目资源文件：`src/main/resources/`
- 测试代码：`src/test/java/`
- 测试资源：`src/test/resources/`
- 所有构建输出：`target/`

Maven 自动识别这些目录，无需额外配置。

## 2. 包命名约定
Java 类的包名应与 POM 中的 `groupId` 和 `artifactId` 保持一致。
**示例**：
若 `groupId` = `com.juvenxu.mvnbook`，`artifactId` = `helloworld`，则包名应为 `com.juvenxu.mvnbook.helloworld`。
这样命名清晰、逻辑统一，且便于在仓库中搜索构件。

## 3. 构建命令与默认行为

### clean
- 执行 `clean:clean` 生命周期
- 删除整个 `target/` 目录，清理所有编译产物

### compile
- 执行 `compiler:compile` 任务前，会先自动执行 `resources:resources` 处理资源文件
- 将 `src/main/java/` 下的主代码编译到 `target/classes/`
- 编译后的 `.class` 文件保持原包结构，例如：
  `target/classes/com/juvenxu/mvnbook/helloworld/HelloWorld.class`

### 其他常用命令（补充）
- `test`：编译并运行测试
- `package`：编译、测试并打包（jar/war 等），输出到 `target/`
- `install`：将包安装到本地仓库

## 4. 总结
- **物理结构**由 Maven 默认目录约定决定（`src/main/java` → `target/classes`）
- **逻辑结构**（包名）由 POM 的 `groupId` 和 `artifactId` 共同决定
- **构建过程**依赖标准生命周期，所有产物都在 `target/` 下，并自动映射包路径
