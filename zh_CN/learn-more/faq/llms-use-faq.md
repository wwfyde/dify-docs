# LLM 配置与使用

### 1. 如何在国内环境中使用 OpenAI 代理服务器进行访问？

MoLook 支持 OpenAI 的自定义 API 域名能力，支持任何兼容 OpenAI 的大模型 API 服务器。社区版中，通过 **设置 --> 模型供应商 --> OpenAI --> 编辑 API** 入口处填写目标服务器地址即可。

### **2. 如何选择基础模型？**

* gpt-3.5-turbo gpt-3.5-turbo 是 gpt-3 模型系列的升级版，它比 gpt-3 更强大，可以处理更复杂的任务。 它在理解长文本和跨文档推理方面有重大提高。 gpt-3.5 turbo 可以产生更连贯和更具说服力的文本。它在摘要、翻译和创意写作方面也有很大提高。 擅长：**长文本理解、跨文档推理、摘要、翻译、创意写作。**
* gpt-4 gpt-4 是最新最强大的 Transformer 语言模型。它拥有预训练的参数量增至约 200 亿，这使其在所有语言任务上都达到了最高水平，特别是在需要深入理解和生成长、复杂响应的任务上。gpt-4 可以处理人类语言的所有方面，包括理解抽象概念和跨页面的推理。gpt-4 是第一个真正的通用语言理解系统，它可以胜任人工智能领域内的任何自然语言处理任务。擅长： **所有 NLP 任务，语言理解，长文本生成，跨文档推理，抽象概念理解**具体可参考[文档](https://platform.openai.com/docs/models/overview)。

### **3. 为什么建议 max\_tokens 设置小一点？**

因为在自然语言处理中，较长的文本输出通常需要更长的计算时间和更多的计算资源。因此，限制输出文本的长度可以在一定程度上降低计算成本和计算时间。例如设置：max\_tokens=500 ，表示最多只考虑输出文本的前 500 个 token，而超过这个长度的部分将会被丢弃。这样做的目的是保证输出文本的长度不会超过 LLM 的接受范围，同时还可以充分利用计算资源，提高模型的运行效率。另一方面，更多的情况是，限制 max\_tokens 能够增加 prompt 的长度，如 gpt-3.5-turbo 的限制为 4097 tokens，如果设置 max\_tokens=4000，那么 prompt 就只剩下 97 tokens 可用，如果超过就会报错。

### **4. 数据集长文本如何切分比较合理？**

在一些自然语言处理应用中，通常会将文本按照段落或者句子进行切分，以便更好地处理和理解文本中的语义和结构信息。最小切分单位取决于具体的任务和技术实现。例如：

* 对于文本分类任务，通常将文本按照句子或者段落进行切分
* 对于机器翻译任务，则需要将整个句子或者段落作为切分单位。

最后，还需要进行实验和评估来确定最合适的 embedding 技术和切分单位。可以在测试集上 / 命中测试比较不同技术和切分单位的性能表现，并选择最优的方案。

### 5. 我们在获取数据集分段时用的什么距离函数？

我们使用[余弦相似度](https://en.wikipedia.org/wiki/Cosine\_similarity)。距离函数的选择通常无关紧要。OpenAI 嵌入被归一化为长度 1，这意味着：

仅使用点积可以稍微更快地计算余弦相似度

余弦相似度和欧几里德距离将导致相同的排名

* > 如果将归一化后的嵌入向量用于计算余弦相似度或欧几里德距离，并基于这些相似性度量对向量进行排序，得到的排序结果将是相同的。也就是说，无论是使用余弦相似度还是欧几里德距离来衡量向量之间的相似性，排序后的结果将是一致的。这是因为在归一化后，向量的长度不再影响它们之间的相对关系，只有方向信息被保留下来。因此，使用归一化的向量进行相似性度量时，不同的度量方法将得到相同的排序结果。在向量归一化后，将所有向量的长度缩放到 1，这意味着它们都处于单位长度上。单位向量只描述了方向而没有大小，因为它们的长度恒为 1。_具体原理可问 ChatGPT._

当嵌入向量被归一化为长度 1 后，计算两个向量之间的余弦相似度可以简化为它们的点积。因为归一化后的向量长度都为 1，点积的结果就等同于余弦相似度的结果。由于点积运算相对于其他相似度度量（如欧几里德距离）的计算速度更快，因此使用归一化的向量进行点积计算可以稍微提高计算效率。

### 6. 如何免费申领智谱·AI、讯飞星火、MiniMax 模型的体验额度？

我们联合大模型厂商向中国用户提供一定的 token 体验额度。通过 MoLook \*\*设置 --> 模型供应商 --> 显示更多模型供应商。\*\*在智谱·AI、讯飞星火或 MiniMax 图标处点击【免费获取】，如果你在英文界面看不到领取入口，请将产品语言切换成为中文：

* \*\*智谱·AI： 免费领取 1000 万 token，\*\*点击【免费领取】，只需输入手机号及验证码，即可到账额度，不限制是否注册过智谱·AI。
* **讯飞星火 （V1.5 模型、V2.0 模型）：免费领取 600 万token，V1.5 模型、V2.0 模型各 300 万 token，额度不互通**，需要从 MoLook 的入口进入，完成讯飞星火开放平台的注册（仅限未注册过讯飞星火的手机号），返回 MoLook 静候 5 分钟，刷新页面即可在 MoLook 页面体现可用额度。
* **MiniMax：免费领取 100 万 token**，只需点击【免费领取】即可到账额度，无需手动注册流程，不限制是否注册过 MiniMax 账号。

体验额度到账后，在应用内 **提示词编排 --> 模型及参数 --> 语言模型** 处选择需使用的模型即可。

### 7. 填写 OpenAI key，校验失败报错提示：“**校验失败： You exceeded your current quota， please check your plan and billing details。**”是什么原因？

说明你的 OpenAI key 的账号没费用了，请前往 OpenAI 充值。

### 8. 使用 OpenAI 的 key 在应用里对话，有如下报错提示，是什么原因？

报错一：

```JSON
The server encountered an internal error and was unable to complete your request。Either the server is overloaded or there is an error in the application
```

报错二：

```JSON
Rate limit reached for default-gpt-3.5-turboin organization org-wDrZCxxxxxxxxxissoZb on requestsper min。 Limit: 3 / min. Please try again in 20s. Contact us through our help center   at help.openai.com   if you continue to haveissues. Please add a payment method toyour account to increase your rate limit.Visit https://platform.openai.com/account/billingto add a payment method.
```

请检查是否达到了官方接口调用速率限制。具体请参考 [OpenAI 官方文档说明](https://platform.openai.com/docs/guides/rate-limits)。

### 9. 用户自部署后，智聊不可使用，报错如下：**Unrecognized request argument supplied:functions**，该怎么解决？

首先请检查前后端版本是否是最新版且前后端版本保持一致；其次，该错误有可能是因为您使用了 Azure OpenAI 的 key，但没有成功部署模型，请检查您使用的 Azure OpenAI 里是否部署了模型；其中 gpt-3.5-turbo 模型版本必须是 0613 以上版本。（因为 0613 之前的版本不支持 智聊 所使用的 function call 能力，所以无法使用）

### 10. 设置 OpenAI Key 时，报错如下，是什么原因？

```JSON
Error communicating with OpenAl: HTTPSConnectionPool(host='api.openai.com', port=443): Max retriesexceeded with url: /v1/chat/completions (Caused byNewConnectionError( <urllib3.connection.HTTPSConnection object at 0x7f0462ed7af0>; Failed toestablish a new connection: [Errno -3] Temporary failure in name resolution'))
```

通常情况下是由于您的环境设置了代理，请检查是否设置代理。

### 11. 应用里切换模型使用时遇到如下报错，该怎么解决？

```JSON
Anthropic: Error code: 400 - f'error': f'type': "invalid request error, 'message': 'temperature: range: -1 or 0..1)
```

由于每个模型的参数取值不同，需要按照当前模型的该参数值范围设置。

### 12. 遇到如下报错提示，该如何解决？

```JSON
Query or prefix prompt is too long, you can reduce the preix prompt, or shrink the max token, or switch to a llm with a larger token limit size
```

在编排页参数设置里，调小“最大 token”的值即可。

### 13. MoLook 里面默认的模型是什么，可否使用开源的模型？

默认的模型可以在 **设置 - 模型供应商** 处配置，目前支持 OpenAI / Azure OpenAl / Anthropic 等模型厂商的文本生成型模型，同时支持 Hugging Face/ Replicate / xinference 上托管的开源模型的接入。

### 14. 在社区版中，数据集开启 **Q\&A 分段模式**一直显示排队中，是什么原因？

请检查您所使用的 Embedding 模型 api-key 是否达到了速率限制。

### 15. 用户在使用应用时遇到报错“Invalid token”，该怎么解决？

如果遇到报错为 “Invalid token”，你可尝试如下两种解决办法：

* 浏览器清除缓存（Cookies、Session Storage 和 Local Storage），如果是手机里使用则清除对应 APP 的缓存，重新访问；
* 二是重新生成一个 App 网址，重新网址进入即可。

### 16. 数据集文档上传的大小限制有哪些？

目前数据集文档上传单个文档最大是 15MB，总文档数量限制 100 个。如您本地部署版本需要调整修改该限制，请参考[文档](https://docs.dify.ai/v/zh-hans/getting-started/faq/install-faq#11.-ben-di-bu-shu-ban-ru-he-jie-jue-shu-ju-ji-wen-dang-shang-chuan-de-da-xiao-xian-zhi-he-shu-liang)。

### 17. 为什么选择了 Claude 模型，还是会消耗 OpenAI 的费用？

因为 Claude 不支持 Embedding 模型，因此 Embedding 过程以及其他对话生成，下一个问题建议等默认都是用的 OpenAI 的 key，因此还是会消耗 OpenAI 的额度。也可以在**设置-模型供应商**里设置其他默认推理模型和 Embedding 模型。

### 18. 有什么方式能控制更多地使用上下文数据而不是模型自身生成能力吗？

是否使用数据集，会和数据集的描述有关系，尽可能把数据集描述写清楚，具体可参考[此文档编写技巧](https://docs.dify.ai/v/zh-hans/advanced/datasets)。

### 19. 上传数据集文档是 Excel，该如何更好地分段？

首行设置表头，后面每行显示内容，不要有其他多余的表头设置，不要设置复杂格式的表格内容。

如下方表格示例，仅需保留第二行的表头，首行（表格1）为多余表头，需删掉。

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 20 买了 ChatGPT plus，为什么在 dify 里还不能使用 GPT4？

OpenAI 的 GPT4 模型 API 和 ChatGPT Plus 是两个产品，分开收费的，模型的 API 有自己的定价，具体参考 [OpenAI 定价文档](https://openai.com/pricing) 。付费申请要先绑卡，绑了卡会有 GPT3.5 的权限，但没有 GPT4 的权限，GPT4 的权限得有一次支付的账单，具体参考 [OpenAI 官方文档](https://platform.openai.com/account/billing/overview)。

### 21. 如何增加其他的 Embedding Model？

MoLook 支持以下作为 Embedding 模型使用，只需在配置框中选择 `Embeddings` 类型即可。

* Azure
* LocalAI
* MiniMax
* OpenAI
* Replicate
* XInference

### 22. 如何把自己创建的应用设置成应用模板？

该功能为 MoLook 官方提供的应用模板供云端版用户参考使用，暂未支持将自己创建的应用设置成应用模板。如您使用云端版，可 **添加到工作区** 或 **自定义** 修改后成为你自己的应用。如您使用社区版，需要为团队内创建更多的应用模板，您可咨询我们商业化团队获得付费的技术支持：`business@dify.ai`

###

###
