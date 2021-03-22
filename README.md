# Atlassian Confluence in Docker

## 使用

### 快速开始

```
docker run -d -p 8090:8090 wwtg99/atlassian-confluence:latest
```

### 数据持久化

```
docker run -d -p 8080:8080 -v <path1>:/var/atlassian/confluence -v <path2>:/opt/atlassian/confluence/logs wwtg99/atlassian-confluence:latest
```

## 配置

### 环境变量

Environment Variable | Description
--- | ---
X_PROXY_NAME | Sets the Tomcat Connectors ProxyName attribute
X_PROXY_PORT | Sets the Tomcat Connectors ProxyPort attribute
X_PROXY_SCHEME | If set to https the Tomcat Connectors secure=true and redirectPort equal to X_PROXY_PORT
X_PATH | Sets the Tomcat connectors path attribute

详细配置可参考 <https://github.com/cptactionhank/docker-atlassian-confluence#configuration>

## 破解本体

本容器已内置破解工具。

1. 容器启动后打开 http://localhost:8090 Confluence 配置页面，选择产品配置，下一步，下一步到授权码页面，当看到服务器 ID 后，记录下服务器 ID。
2. 用 `docker exec` 进入容器，执行如下命令

```
java -jar /atlassian-agent.jar -m <your email> -n <your name> -o <your organization> -p conf -s <服务器ID>
```

会输出许可证，复制到页面中激活即可。

## 破解插件

1. 在应用市场安装应用。
2. 安装完成后，在管理应用页面，查看应用密钥，例如 `eu.softwareplant.bigpicture`
3. 用 `docker exec` 进入容器，执行如下命令

```
java -jar /atlassian-agent.jar -m <your email> -n <your name> -o <your organization> -p '<应用密钥>' -s <服务器ID>
```

会输出许可证，复制到页面中激活即可。

详细破解流程可参考 <https://gitee.com/pengzhile/atlassian-agent>

## 感谢

Docker 镜像制作参考 [cptactionhank/docker-atlassian-confluence](https://github.com/cptactionhank/docker-atlassian-confluence)

感谢 [pengzhile/atlassian-agent](https://gitee.com/pengzhile/atlassian-agent) 提供破解工具。
