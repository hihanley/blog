# 使用 `VS Code` 开发 Java 项目

## maven 阿里云镜像配置
使用 `VS Code` 打开 Java 项目前, 修改 `pom.xml` 文件:
```xml
<project>
    <!-- ... -->
    <repositories>
        <repository>
            <id>aliyunmaven</id>
            <name>阿里云公共仓库</name>
            <url>https://maven.aliyun.com/repository/public</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>aliyunmaven</id>
            <name>阿里云公共仓库</name>
            <url>https://maven.aliyun.com/repository/public</url>
        </pluginRepository>
    </pluginRepositories>
</project>
```

## 自定义 `VS Code` 的 Java Runtime
修改 `VS Code` 配置文件:
```jsonc
{
    // ...
    "java.configuration.runtimes": [
        {
            "name": "JavaSE-17",
            "path": "/absolute/path" // path to jdk install path, not java bin path.
        }
    ]
}
```