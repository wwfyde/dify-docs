# 创建应用

### 创建应用的步骤

<figure><img src="../../.gitbook/assets/create-app.png" alt=""><figcaption><p>创建应用</p></figcaption></figure>

<details>

<summary>第 1 步，以管理员登录 MoLook 后，前往主导航应用页</summary>



</details>

<details>

<summary>第 2 步，点击“创建新应用”</summary>

此外，我们在创建应用界面中提供了一些模版，你可以在创建应用的弹窗中点击**从模版创建**，这些模版将为你要开发的应用提供启发和参考。

</details>

<details>

<summary>第 3 步，选择对话型或文本生成型应用，并为它起个名字</summary>

应用名称今后可以随时修改。

</details>

### 从配置文件创建

如果你从社区或其它人那里获得了一个模版，你可以点击**从应用配置文件创建**，上传后可加载对方应用中的大部分设置项（但目前不包括数据集）。

### 你的应用

{% hint style="info" %}
如果你是第一次使用，这里会提示你输入 OpenAI 的 API 密钥。一个可正常使用的 LLM 密钥是使用 MoLook 的前提，如果你还没有请前往[申请](https://platform.openai.com/account/api-keys)一个。
{% endhint %}

<figure><img src="../../.gitbook/assets/openaiKey.png" alt=""><figcaption><p>输入 OpenAI Key</p></figcaption></figure>

**创建应用**或**选择一个已有应用**后，会来到一个显示应用概况的**应用概览页**。你可以在这里直接访问你的 WebApp 或查看 API 状态，也可以开启或关闭它们。

**统计**显示了该应用一段时间内的用量、活跃用户数和 LLM 调用消耗—这使你可以持续改进应用运营的经济性，我们将逐步提供更多有用的可视化能力，请**告诉我们**你想要的。

1. 全部消息数（Total Messages），反映 AI 每天的互动总次数，每回答用户一个问题算一条 Message。提示词编排和调试的会话不计入。
2. 活跃用户数（Active Users），与 AI 有效互动，即有一问一答以上的唯一用户数。提示词编排和调试的会话不计入。
3. 平均会话互动数（Average Session Interactions），反映每个会话用户的持续沟通次数，如果用户与 AI 问答了 10 轮，即为 10。该指标反映了用户粘性。仅在对话型应用提供。
4. 用户满意度（User Satisfaction Rate），每 1000 条消息的点赞数。反应了用户对回答十分满意的比例。
5. 平均响应时间（Average Response Time），衡量 AI 应用处理和回复用户请求所花费的平均时间，单位为毫秒，反映性能和用户体验。仅在文本型应用提供。
6. 费用消耗（Token Usage），反映每日该应用请求语言模型的 Tokens 花费，用于成本控制。

### 接下来

* 试试你的 **WebApp**
* 逛一逛左侧的配置、开发和 Logs 页
* 试着参考**案例**配置一个应用
* 如果你具备开发前端应用的能力，请查阅 **API 文档**
