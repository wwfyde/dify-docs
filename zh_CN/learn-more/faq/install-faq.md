# 本地部署相关

### 1. 本地部署初始化后，密码错误如何重置？

若使用 docker compose 方式部署，可执行以下命令进行重置

```
docker exec -it docker-api-1 flask reset-password
```

输入账户 email 以及两次新密码即可。

### 2. 本地部署日志中报 File not found 错误，如何解决？

```
ERROR:root:Unknown Error in completion
Traceback (most recent call last):
  File "/www/wwwroot/dify/dify/api/libs/rsa.py", line 45, in decrypt
    private_key = storage.load(filepath)
  File "/www/wwwroot/dify/dify/api/extensions/ext_storage.py", line 65, in load
    raise FileNotFoundError("File not found")
FileNotFoundError: File not found
```

该错误可能是由于更换了部署方式，或者 `api/storage/privkeys` 删除导致，这个文件是用来加密大模型密钥的，因此丢失后不可逆。可以使用如下命令进行重置加密公私钥：

*   Docker compose 部署

    ```
    docker exec -it docker-api-1 flask reset-encrypt-key-pair
    ```
*   源代码启动

    进入 api 目录

    ```
    flask reset-encrypt-key-pair
    ```

    按照提示进行重置。

### **3. 安装时后无法登录，登录成功，但后续接口均提示 401？**

这可能是由于切换了域名/网址，导致前端和服务端跨域。跨域和身份会涉及到下方的配置：

1. CORS 跨域配置
   1.  `CONSOLE_CORS_ALLOW_ORIGINS`

       控制台 CORS 跨域策略，默认为 `*`，即所有域名均可访问。
   2.  `WEB_API_CORS_ALLOW_ORIGINS`

       WebAPP CORS 跨域策略，默认为 `*`，即所有域名均可访问。

### **4. 启动后页面一直在 loading，查看请求提示 CORS 错误？**

这可能是由于切换了域名/网址，导致前端和服务端跨域，请将 `docker-compose.yml` 中所有的以下配置项改为新的域名：

`CONSOLE_API_URL:` 控制台 API 的后端 URL。 `CONSOLE_WEB_URL:` 控制台网页的前端 URL。 `SERVICE_API_URL:` 服务 API 的 URL。 `APP_API_URL:` WebApp API 的后端 URL。 `APP_WEB_URL:` WebApp 的 URL。

更多信息，请查看：[环境变量](../../getting-started/install-self-hosted/environments.md)

### 5. 部署后如何升级版本？

如果你是通过镜像启动，请重新拉取最新镜像完成升级。 如果你是通过源码启动，请拉取最新代码，然后启动，完成升级。

源码部署更新时，需要进入 api 目录下，执行以下命令将数据库结构迁移至最新版本：

`flask db upgrade`

### 6. 使用 Notion 导入时如何配置环境变量？

[**Notion 的集成配置地址**](https://www.notion.so/my-integrations)\*\*。\*\*进行私有化部署时，请设置以下配置：

1. **`NOTION_INTEGRATION_TYPE`** ：该值应配置为（**public/internal**）。由于 Notion 的 Oauth 重定向地址仅支持 https，如果在本地部署，请使用 Notion 的内部集成。
2. **`NOTION_CLIENT_SECRET`** ： Notion OAuth 客户端密钥（用于公共集成类型）。
3. **`NOTION_CLIENT_ID`** ： OAuth 客户端ID（用于公共集成类型）。
4. **`NOTION_INTERNAL_SECRET`** ： Notion 内部集成密钥，如果 `NOTION_INTEGRATION_TYPE` 的值为 **internal**，则需要配置此变量。

### 7. 本地部署版，如何更改空间的名称？

在数据库 `tenants` 表里修改。

### 8. 想修改访问应用的域名，在哪里修改？

在 `docker_compose.yaml` 里面找到 APP\_WEB\_URL 配置域名。

### 9. 如果发生数据库迁移，需要备份哪些东西？

需要备份数据库、配置的存储以及向量数据库数据，若为 docker compose 方式部署，可直接备份 `dify/docker/volumes` 目录下所有数据内容。

### 10. 为什么 Docker 部署 MoLook，本地启动 OpenLLM 用 127.0.0.1 却无法访问本地的端口？

127.0.0.1 是容器内部地址， MoLook 配置的服务器地址需要宿主机局域网 IP 地址。

### 11. 本地部署版如何解决数据集文档上传的大小限制和数量限制。

可参考官网[环境变量说明文档](https://docs.dify.ai/v/zh-hans/getting-started/install-self-hosted/environments)去配置。

### 12. 本地部署版如何通过邮箱邀请成员？

本地部署版，邀请成员可通过邮箱邀请，输入邮箱邀请后，页面显示邀请链接，复制邀请链接转发给用户，用户打开链接通过邮箱登录设置密码即可登录到你的空间内。

### 13. 本地部署版本遇到这个错误需要怎么办 Can't load tokenizer for 'gpt2'

```
Can't load tokenizer for 'gpt2'. If you were trying to load it from 'https://huggingface.co/models', make sure you don't have a local directory with the same name. Otherwise, make sure 'gpt2' is the correct path to a directory containing all relevant files for a GPT2TokenizerFast tokenizer.
```

可参考官网[环境变量说明文档](https://docs.dify.ai/v/zh-hans/getting-started/install-self-hosted/environments)去配置。以及相关 [Issue](https://github.com/langgenius/dify/issues/1261)。

### 14. 本地部署 80 端口被占用应该如何解决？

本地部署 80 端口被占用，可通过停止占用 80 端口的服务，或者修改 docker-compose.yaml 里面的端口映射，将 80 端口映射到其他端口。通常 Apache 和 Nginx 会占用这个端口，可通过停止这两个服务来解决。

### 15. 文本转语音遇到这个错误怎么办？

```
[openai] Error: ffmpeg is not installed
```

由于 OpenAI TTS 实现了音频流分段，源码部署时需要安装 ffmpeg 才可正常使用，详细步骤：

**Windows:**

1. 访问 [FFmpeg 官方网站](https://ffmpeg.org/download.html)，下载已经编译好的 Windows shared 库。
2. 下载并解压 FFmpeg 文件夹，它会生成一个类似于 "ffmpeg-20200715-51db0a4-win64-static" 的文件夹。
3. 将解压后的文件夹移动到你想要的位置，例如 C:\Program Files\。
4. 将 FFmpeg 的 bin 目录所在的绝对路径添加到系统环境变量中。
5. 打开命令提示符，输入"ffmpeg -version"，如果能看到 FFmpeg 的版本信息，那么说明安装成功。

**Ubuntu:**

1. 打开终端。
2. 输入以下命令来安装 FFmpeg：`sudo apt-get update`，然后输入`sudo apt-get install ffmpeg`。
3. 输入"ffmpeg -version" 来检查是否安装成功。

**CentOS:**

1. 首先，你需要启用EPEL存储库。在终端中输入：`sudo yum install epel-release`
2. 然后，输入：`sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm`
3. 更新 yum 包，输入：`sudo yum update`
4. 最后，安装 FFmpeg，输入：`sudo yum install ffmpeg ffmpeg-devel`
5. 输入"ffmpeg -version" 来检查是否安装成功。

**Mac OS X:**

1. 打开终端。
2. 如果你还没有安装 Homebrew，你可以通过在终端中输入以下命令来安装：`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
3. 使用 Homebrew 安装 FFmpeg，输入：`brew install ffmpeg`
4. 输入 "ffmpeg -version" 来检查是否安装成功。

### 16. 本地部署时，如果遇到 Nginx 配置文件挂载失败，如何解决？

```
Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: error mounting "/run/desktop/mnt/host/d/Documents/docker/nginx/nginx.conf" to rootfs at "/etc/nginx/nginx.conf": mount /run/desktop/mnt/host/d/Documents/docker/nginx/nginx.conf:/etc/nginx/nginx.conf (via /proc/self/fd/9), flags: 0x5000: not a directory: unknown: Are you trying to mount a directory onto a file (or vice-versa)? Check if the specified host path exists and is the expected type
```

请下载完整的项目，进入 docker 执行 `docker-compose up -d` 即可。

```
git clone https://github.com/langgenius/dify.git
cd dify/docker
docker compose up -d
```

### 17. Migrate Vector Database to Qdrant or Milvus

如果您想将向量数据库从 Weaviate 迁移到 Qdrant 或 Milvus，您需要迁移向量数据库中的数据。以下是迁移方法：

步骤：

1. 如果您从本地源代码开始，请将 `.env` 文件中的环境变量修改为您要迁移到的向量数据库。 例如：`VECTOR_STORE=qdrant`
2. 如果您从 docker-compose 开始，请将 `docker-compose.yaml` 文件中的环境变量修改为您要迁移到的向量数据库，api 和 worker 都需要修改。 例如：

```
# The type of vector store to use. Supported values are `weaviate`, `qdrant`, `milvus`.
VECTOR_STORE: weaviate
```

3. 执行以下命令

```
flask vdb-migrarte # or docker exec -it docker-api-1 flask vdb-migrarte
```

### 18. 为什么Sandbox需要SYS\_ADMIN权限？

#### 为什么需要 SYS\_ADMIN 权限？

Sandbox 基于`Seccomp`进行沙箱隔离，而Docker也是基于`Seccomp`进行资源隔离，并且，在Docker中，Linux Seccomp BPF是被默认禁用的，导致无法在容器中使用`Seccomp`，因此，需要SYS\_ADMIN权限来启用`Seccomp`。

### 19. 我如何将我自己创建的应用设置为应用模板？

目前还不支持将你自己创建的应用设置为模板。现有的模板是由MoLook官方为云版本用户参考提供的。如果你正在使用云版本，你可以将应用添加到你的工作空间或者在修改后定制它们以创建你自己的应用。如果你正在使用社区版本并且需要为你的团队创建更多的应用模板，你可以咨询我们的商务团队以获得付费技术支持：[business@dify.ai](mailto:business@dify.ai)

### 20.502 Bad Gateway

这是因为Nginx将服务转发到了错误的位置导致的，首先确保容器正在运行，然后以Root权限运行以下命令：
```
docker ps -q | xargs -n 1 docker inspect --format '{{ .Name }}: {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```
在输出内容中找到这两行：
```
/docker-web-1: 172.19.0.5
/docker-api-1: 172.19.0.7
```
记住后面的IP地址。然后打开你存放dify源代码的地方，打开`dify/docker/nginx/conf.d`,将`http://api:5001`替换为`http://172.19.0.7:5001`,将`http://web:3000`替换为`http://172.19.0.5:3000`，随后重启Nginx容器或者重载配置。
你可能在重新启动相关容器时需要再次根据IP进行配置。

#### 安全性问题

至于安全性问题，我们禁用了Sandbox中所有进程的文件、网络、IPC、PID、用户、mount、UTS、系统访问等能力，以确保恶意代码不会被执行，同时，我们还额外隔离了容器中的文件和网络，以确保在即使代码被执行，也无法对系统造成危害。
