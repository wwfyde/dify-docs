# 应用构建

在 MoLook 中，一个“应用”是指基于 GPT 等大型语言模型构建的实际场景应用。通过创建应用，您可以将智能 AI 技术应用于特定的需求。它既包含了开发 AI 应用的工程范式，也包含了具体的交付物。

简而言之，一个应用为开发者交付了：

* 封装友好的 LLM API，可由后端或前端应用直接调用，通过 Token 鉴权
* 开箱即用、美观且托管的 Web App，你可以 WebApp 的模版进行二次开发
* 一套包含 Prompt Engineering、上下文管理、日志分析和标注的易用界面

你可以任选**其中之一**或**全部**，来支撑你的 AI 应用开发。

### 应用类型

MoLook 中提供了两种应用类型：文本生成型与对话型，今后或许会出现更多应用范式（我们应该会及时跟进），MoLook 的最终目标是能覆盖 80% 以上的常规 LLM 应用情景。

文本生成型与对话型应用的区别见下表：

<table><thead><tr><th width="180.33333333333331"></th><th>文本生成型</th><th>对话型</th></tr></thead><tbody><tr><td>WebApp 界面</td><td>表单+结果式</td><td>聊天式</td></tr><tr><td>WebAPI 端点</td><td><code>completion-messages</code></td><td><code>chat-messages</code></td></tr><tr><td>交互方式</td><td>一问一答</td><td>多轮对话</td></tr><tr><td>流式结果返回</td><td>支持</td><td>支持</td></tr><tr><td>上下文保存</td><td>当次</td><td>持续</td></tr><tr><td>用户输入表单</td><td>支持</td><td>支持</td></tr><tr><td>数据集与插件</td><td>支持</td><td>支持</td></tr><tr><td>AI 开场白</td><td>不支持</td><td>支持</td></tr><tr><td>情景举例</td><td>翻译、判断、索引</td><td>聊天或一切</td></tr></tbody></table>

###
