# 从 Notion 导入数据

MoLook 数据集支持从 Notion 导入，并设置 **同步** 使得数据在 Notion 更新后便自动同步到 MoLook。

### 授权验证

1. 在创建数据集，选择数据源时，点击 **同步自 Notion 内容-- 去绑定，根据提示完成授权验证。**
2. 你也可以：进入 **设置 -- 数据来源 -- 添加数据源** 中点击 Notion 来源 **绑定** ，完成授权验证。

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption><p>绑定 Notion</p></figcaption></figure>

### 导入 Notion 数据

完成验证授权后，进入创建数据集页面，点击 \*\*同步自 Notion 内容 ，\*\*选择需要的授权页面进行导入。

### 进行分段和清洗

接下来，选择你的**分段设置**和**索引方式**，**保存并处理**。等待 MoLook 为你处理这些数据，通常该步骤在 LLM 供应商中需要消耗 Token。MoLook 不仅支持普通类型页面导入，并且会将 database 类型下的页面属性进行汇总保存。

_**请注意：图片和文件暂不支持导入，表格类数据会被转换为文本展示。**_

### 同步 Notion 数据

如果您的 Notion 内容有修改，您可以直接在 MoLook 数据集 **文档列表页**中点击 **同步** 即可进行数据一键同步，该步骤是需要消耗 Token。

<figure><img src="../../.gitbook/assets/sync-notion.png" alt=""><figcaption><p>同步 Notion 内容</p></figcaption></figure>

### 社区版 Notion 的集成配置方法

Notion集成分为**内部集成**（internal integration）和**外部集成**（public integration）两种方式。可按需在 MoLook 里配置。两种集成方式的具体区别请参阅 [Notion 官方文档](https://developers.notion.com/docs/authorization)。

### 1、**使用 internal 集成方式**

首先，在集成的设置页面中[创建集成](https://www.notion.so/my-integrations)。默认情况下，所有集成都以内部集成开始；内部集成将与您选择的工作区相关联，因此您需要是工作区所有者才能创建集成。

具体操作步骤：

点击“**New integration**”按钮，类型默认是 **Internal**（不可修改），选择关联的空间，输入集成名称并上传 logo 后，点击“Submit”，集成创建成功。

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

创建集成后，您可以根据需要在 Capabilities 选项卡下更新其设置，并在 Secrets 下点击 “Show” 按钮然后复制 Secrets。

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

复制后回到 MoLook 源代码下，在 **.env** 文件里配置相关环境变量，环境变量如下：

**NOTION\_INTEGRATION\_TYPE** = internal or **NOTION\_INTEGRATION\_TYPE** = public

**NOTION\_INTERNAL\_SECRET**=you-internal-secret

### 2、**使用 Public 集成方式**

**需要将 internal 集成升级为 public 集成**，导航到集成的 Distribution 页面，然后切换开关以公开集成。将开关切换到公共设置，您需要在下面的 Organization Information 表单中填写其他信息，包括您的公司名称、网站和重定向 URL 等信息，然后点击“Submit”按钮。

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

在集成的设置页面中成功公开集成后，您将能够在密钥选项卡中访问集成的密钥：

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

回到 MoLook 源代码下，在 **.env** 文件里配置相关环境变量，环境变量如下：

**NOTION\_INTEGRATION\_TYPE**=public

**NOTION\_CLIENT\_SECRET**=you-client-secret

**NOTION\_CLIENT\_ID**=you-client-id

配置完成后，即可在数据集中操作 Notion 的数据导入及同步功能。
