---
description: Learn about the Different Models Supported by MoLook.
---

# Model Configuration

MoLook supports major model providers like OpenAI's GPT series and Anthropic's Claude series. Each model's capabilities and parameters differ, so select a model provider that suits your application's needs. **Obtain the API key from the model provider's official website before using it in MoLook.**

## Model Types in MoLook

MoLook classifies models into 4 types, each for different uses:

1.  **System Inference Models:** Used in applications for tasks like chat, name generation, and suggesting follow-up questions.

    > Providers include [OpenAI](https://platform.openai.com/account/api-keys)、[Azure OpenAI Service](https://azure.microsoft.com/en-us/products/ai-services/openai-service/)、[Anthropic](https://console.anthropic.com/account/keys)、Hugging Face Hub、Replicate、Xinference、OpenLLM、[iFLYTEK SPARK](https://www.xfyun.cn/solutions/xinghuoAPI)、[WENXINYIYAN](https://console.bce.baidu.com/qianfan/ais/console/applicationConsole/application)、[TONGYI](https://dashscope.console.aliyun.com/api-key\_management?spm=a2c4g.11186623.0.0.3bbc424dxZms9k)、[Minimax](https://api.minimax.chat/user-center/basic-information/interface-key)、ZHIPU(ChatGLM) [Ollama](https://docs.dify.ai/tutorials/model-configuration/ollama)、[LocalAI](https://github.com/mudler/LocalAI)、.
2.  **Embedding Models:** Employed for embedding segmented documents in knowledge and processing user queries in applications.

    > Providers include OpenAI, ZHIPU (ChatGLM), Jina AI([Jina Embeddings 2](https://jina.ai/embeddings/)).
3.  [**Rerank Models**](https://docs.dify.ai/advanced/retrieval-augment/rerank)**:** Enhance search capabilities in LLMs.

    > Provider: Cohere.
4.  **Speech-to-Text Models:** Convert spoken words to text in conversational applications.

    > Provider: OpenAI.

MoLook plans to add more LLM providers as technology and user needs evolve.

## Hosted Model Trial Service

MoLook offers trial quotas for cloud service users to experiment with different models. Set up your model provider before the trial ends to ensure uninterrupted application use.

* OpenAI Hosted Model Trial: Includes 200 invocations for models like GPT3.5-turbo, GPT3.5-turbo-16k, text-davinci-003 models.

## Setting the Default Model

MoLook automatically selects the default model based on usage. Configure this in `Settings > Model Provider`.

<figure><img src="../../.gitbook/assets/image-default-models.png" alt=""><figcaption></figcaption></figure>

## Model Integration Settings

Choose your model in MoLook's `Settings > Model Provider`.

<figure><img src="../../.gitbook/assets/image-20231210143654461.png" alt=""><figcaption></figcaption></figure>

Model providers fall into two categories:

1. Proprietary Models: Developed by providers such as OpenAI and Anthropic.
2. Hosted Models: Offer third-party models, like Hugging Face and Replicate.

Integration methods differ between these categories.

**Proprietary Model Providers:** MoLook connects to all models from an integrated provider. Set the provider's API key in MoLook to integrate.

{% hint style="info" %}
MoLook uses [PKCS1\_OAEP](https://pycryptodome.readthedocs.io/en/latest/src/cipher/oaep.html) encryption to protect your API keys. Each user (tenant) has a unique key pair for encryption, ensuring your API keys remain confidential.
{% endhint %}

**Hosted Model Providers:** Integrate third-party models individually.

Specific integration methods are not detailed here.

* [Hugging Face](https://docs.dify.ai/advanced/model-configuration/hugging-face)
* [Replicate](https://docs.dify.ai/advanced/model-configuration/replicate)
* [Xinference](https://docs.dify.ai/advanced/model-configuration/xinference)
* [OpenLLM](https://docs.dify.ai/advanced/model-configuration/openllm)

## Using Models

Once configured, these models are ready for application use.

<figure><img src="../../.gitbook/assets/choice-model-in-app.png" alt=""><figcaption></figcaption></figure>
