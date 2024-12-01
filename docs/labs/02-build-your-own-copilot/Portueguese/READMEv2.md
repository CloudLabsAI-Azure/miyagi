# Desenvolva Aplicativos com Inteligência Artificial utilizando a Suite de Ferramentas Copilot da Microsoft e o Serviço Azure OpenAI

## Visão geral do workshop

Neste workshop, você adquirirá uma forte compreensão dos conceitos básicos de IA generativa, Azure Open AI, padrões de Geração Aumentada de Recuperação (RAG), Kernel Semântico e como utilizar estes conceitos para criar o seu próprio copiloto para atender às suas necessidades de negócio. Você também explorará casos de uso que revelam a gama de possibilidades oferecidas pelos produtos Copilot. Utilizando a pilha Copilot da Microsoft e casos de uso práticos, este workshop irá guiá-lo na concepção e criação de sistemas inteligentes que integram modelos básicos, resultando em maior produtividade e experiências de produto altamente personalizadas.

### O que esperar?

Aprenda os Conceitos:

O primeiro segmento do workshop consiste em uma apresentação que fornecerá uma base sólida nos conceitos de IA generativa e o guiará no processo de criação do seu próprio copiloto utilizando a pilha Copilot da Microsoft.

## Laboratório prático:

No segmento prático (que será a maior parte deste workshop), os participantes terão uma exposição profunda às características da Pilha Copilot, especialmente com Kernel Semântico, Engenharia de Prompts e Azure Cognitive Search. Durante esta parte prática do laboratório, você irá clonar um exemplo de aplicação de Consultor de Investimentos e o implantará no Azure. Esta aplicação aproveita o poder do Azure OpenAI, RAG, Semantic Kernel e outros serviços Azure. Ao explorar os recursos-chave deste aplicativo, você obterá um entendimento profundo dos mecanismos que impulsionam essas funcionalidades:

Copiloto de Consultor de Investimentos: Este Copiloto, desenvolvido com IA Generativa, fornece recomendações de investimento com base nas preferências do usuário. Ele utiliza Azure OpenAI, Semantic Kernel, Azure Cognitive Search (com indexação vetorial para incorporações), Azure Cosmos DB, Container Apps e Azure API Management.

Copiloto de chat: Obtenha assistência em tempo real com investimentos utilizando esta funcionalidade. Ele utiliza Azure OpenAI, Semantic Kernel, Azure Cognitive Search (com indexação vetorial para incorporações), Azure Cosmos DB, Container Apps e Azure API Management.

### Projecto Miyagi – Exemplo de previsão para [copilot stack](https://learn.microsoft.com/en-us/semantic-kernel/overview/#semantic-kernel-is-at-the-center-of- o -copiloto-stack)

O Projecto Miyagi apresenta a pilha Copilot da Microsoft num [workshop de visão](https://github.com/Azure-Samples/intelligent-app-workshop) destinado a projetar, desenvolver e implementar aplicações inteligentes de nível empresarial. Ao explorar [casos de uso] de ML generativo e tradicional (https://iappwksp.com/wksp/05-use-cases/), a Miyagi oferece uma abordagem experiencial para o desenvolvimento de experiências de produtos com IA que melhoram a produtividade e permitem a hiperpersonalização. Além disso, o workshop apresenta a engenheiros de software tradicionais padrões emergentes de engenharia de prompts, como cadeia de pensamento e augmentação com recuperação de informação, bem como técnicas como vetorização para memória de longo prazo, ajuste fino de modelos OSS e plug-ins ou ferramentas para ampliar e fundamentar LLMs.

O projeto inclui exemplos de utilização do [Kernel Semântico](https://learn.microsoft.com/en-us/semantic-kernel/overview/#semantic-kernel-is-at-the-center-of-the-copilot -stack), [Promptflow](https://promptflow.azurewebsites.net/overview-what-is-prompt-flow.html), [LlamaIndex](https://github.com/jerryjliu/llama_index), [LangChain ](https://github.com/hwchase17/langchain#readme), armazenamentos vetoriais ([Azure Cognitive Search](https://github.com/Azure/cognitive-search-vector-pr), [CosmosDB Postgres pgvector ] (https://learn.microsoft.com/en-us/azure/cosmos-db/postgresql/howto-use-pgvector) e ferramentas para geração de imagens, como o [DreamFusion](https://huggingface.co/thegovind / reddogpillmodel512) e [ControlNet](https://github.com/lllyasviel/ControlNet). Além disso, ele apresenta modelos de base pré-treinados e ajustados no AzureML, como o Llama2. Aproveite este projeto para adquirir conhecimento enquanto moderniza e transforma seus aplicativos com IA e ajusta finamente seus dados privados para criar seus próprios Copilots.

Esta base de código poliglota utiliza uma multiplicidade de microsserviços para implementar diversos [casos de uso](https://iappwksp.com/wksp/05-use-cases/) utilizando a nossa pilha Copilot. Inclui recursos de geração de texto e imagens personalizados para coaching financeiro, resumo e orquestração semelhante a agentes. Construída sobre uma arquitetura orientada a eventos nativa da nuvem (EDA), a solução apresenta atributos de qualidade de nível empresarial, como disponibilidade, escalabilidade e manutenibilidade."

Embarque em uma jornada para transformar suas aplicações em sistemas inteligentes de ponta com este workshop autoguiado e descubra o que é possível.

### Front-end
A interação com modelos de linguagem de grande escala é mais do que apenas conversar. Este exemplo mostra alguns casos de uso.

![frontend](../Media/wip-ui.png)

### Arquitetura

#### Arquitetura lógica de alto nível

![azure](../Media/wip-azure.png)

#### Orquestração do Kernel Semântico para a aplicação Miyagi

![sk-orchestration](../Media/sk-memory-orchestration.png)

#### Panorama geral

![pilha copiloto](../Media/basic-arch.png)

### Pilha do copilot

![pilha copiloto](../Media/copilot-stack.png)

### Serviços e capacidades

- [Azure OpenAI](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/models)
  - gpt-4
  - gpt-35-turbo
  - text-embedding-ada-002
- [Semantic Kernel](https://github.com/microsoft/semantic-kernel)
- [Use your own data with Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/use-your-data-quickstart?tabs=command-line&pivots=rest-api#example-curl-commands)
- [AzureML PromptFlow](https://learn.microsoft.com/en-us/azure/machine-learning/prompt-flow/overview-what-is-prompt-flow?view=azureml-api-2)
- [TypeChat](https://microsoft.github.io/TypeChat)
- [Azure Functions](https://azure.microsoft.com/en-ca/products/functions/)
- [APIM](https://learn.microsoft.com/en-us/azure/api-management/)
- [Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)
- [Event Grid](https://learn.microsoft.com/en-us/azure/event-grid/overview)
- [Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-overview)
- [Cosmos DB](https://azure.microsoft.com/en-us/products/cosmos-db/)
- [Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-introduction)
- [LangChain](https://github.com/hwchase17/langchain#readme)
- [Foundation Models from CogServices](https://azure.microsoft.com/en-us/blog/announcing-a-renaissance-in-computer-vision-ai-with-microsofts-florence-foundation-model/)
- [Qdrant](https://qdrant.tech/solutions/)
- [Microsoft DeepSpeed Chat](https://github.com/microsoft/DeepSpeedExamples/tree/master/applications/DeepSpeed-Chat)
- [Azure Web PubSub](https://azure.microsoft.com/en-us/products/web-pubsub)
- [Azure Communication Services (ACS)](https://learn.microsoft.com/en-us/azure/communication-services/overview#common-scenarios)

## Resumo

### Introdução à criação de aplicações inteligentes com a pilha Copilot da Microsoft e o Azure OpenAI

### Introdução ao ambiente CloudLabs

### Laboratório 1 - Execute localmente a aplicação Miyagi

Neste laboratório, o foco está na configuração da aplicação Miyagi para prontidão operacional. Posteriormente, a atenção passa para a compreensão da implementação detalhada do serviço de recomendação. A fase prática envolve a execução do serviço de recomendação e a implementação local do frontend Miyagi para testes e desenvolvimento.

### Laboratório 2.1: Conteinerizando a UI Miyagi e do serviço de recomendação para o Azure Kubernetes Service (AKS)

Neste laboratório, irá criar as imagens Docker e publicá-las no Azure Kubernetes Service (AKS).

### Laboratório 3 – Expor a API OpenAI por meio de um Serviço de Gerenciamento de APIs

Neste laboratório, você verificará e criará APIs no serviço de gerenciamento de APIs implementado para atualizar a imagem Docker do serviço de recomendação. A revisão do serviço de recomendação a partir do Container App encapsula a abordagem meticulosa para manutenção e otimização de aplicações conteinerizadas dentro do escopo do projeto.

### Primeiros passos para seu próprio copiloto

Neste laboratório, você criará a sua própria aplicação Copilot utilizando as ferramentas Semantic Kernal. Além disso, irá configurar o Azure AI Search.
