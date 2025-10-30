# Lab 5: Getting Started with Your Own Copilot

### Estimated Duration: 30 minutes

Semantic Kernel is an SDK that integrates Large Language Models (LLMs) like OpenAI, Azure OpenAI, and Hugging Face with conventional programming languages like C#, Python, and Java. Semantic Kernel achieves this by allowing you to define plugins that can be chained together in just a few lines of code.

What makes Semantic Kernel _special_, however, is its ability to _automatically_ orchestrate plugins with AI. With Semantic Kernel
[planners](https://learn.microsoft.com/en-us/semantic-kernel/ai-orchestration/planner), you can ask an LLM to generate a plan that achieves a user's unique goal. Afterward, Semantic Kernel will execute the plan for the user.

## Lab objectives

You will be able to complete the following tasks:

- Task 1: Configure and Run the Semantic Kernel Sample
- Task 2: Configure Azure AI Search

### Task 1: Configure and Run the Semantic Kernel Sample

In this task, you will configure the Semantic Kernel plugin in Visual Studio Code, create a C# Home Automation app using Azure OpenAI, and build and run the application to interact with it.

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/vs-01.png)

1. In the **Visual Studio Code** from the left panel, select **Semantic Kernel** **(1)** plugin, expand  by click on **AI ENDPOINTS (OPENAI)** **(2)**, click on **Switch EndPoint Provider** **(3)**, and select **AzureOpenAI** **(4)**.

    ![](./Media/miyagi-image92.png)

1. Under **AI ENDPOINTS (Azure OPENAI)**, click on **Sign in to Azure** **(1)**, in the pop-up  **The extension 'Semantic Kernel Tools' wants to sign in using Microsoft** click on **Allow** **(2)**.

   ![](./Media/miyagi-image93.png)

1. This will redirect to **Microsoft login page**, select your Azure account **<inject key="AzureAdUserEmail"></inject>**, and navigate back to the **Visual studio code**.

   ![](./Media/azurelogin.png)

1. Navigate back to the **Visual Studio Code** From the **Functions panel**, click on the **Get started icon** **(1)** and follow the wizard to **Create a new app** **(2)** with the semantic function.

   ![](./Media/miyagi-image95.png)

1. Choose **Semantic Kernel: C# Home Automation**.

    ![](./Media/kkernal1.png)

1. Browse the location `C:\LabFiles` **(1)** and **Select location for new app** **(2)**.

   ![](./Media/miyagi-image97.png)

1. Click on **Yes, I trust authors**.

   ![](./Media/miyagi-image98.png)

1. Navigate to the **appsettings.json** **(1)** file and replace the existing **script** **(2)** with the following. The `AzureOpenAIOptions` section in appsettings.json stores configuration settings for Azure OpenAI services, such as API key, endpoint URL, and model name, used for authentication and service access.

   ```
   {
   "AzureOpenAIOptions": {
     "ChatDeploymentName": "",
     "Endpoint": "",
     "ApiKey": ""
      }
   }
   ```

   ![](./Media/replaceappsetting.png)

1. In ASP.NET Core, `appsettings.json` is a configuration file that stores various application settings, such as service endpoints, and other application-specific settings and saves the file **Ctrl + S**. 

    | **Variables**       | **Values**                                             |
    | --------------------|--------------------------------------------------------|
    | ChatDeploymentName  | **<inject key="CompletionModel" enableCopy="true"/>**  |
    | Endpoint            | **<inject key="OpenAIEndpoint" enableCopy="true"/>**   |
    | ApiKey              | **<inject key="OpenAIKey" enableCopy="true"/>**        |

1. Make sure your `appsettings.json` file looks as shown in the screenshot below.

    ![](./Media/miyagi-image(99).png)

1. Navigate to the **Program.cs** **(1)** file and replace existing code with the following. The  `Program.cs` file sets up a .NET application using dependency injection and Semantic Kernel. It configures services, including Azure OpenAI for chat completion, and adds various plugins `(MyTimePlugin, MyAlarmPlugin, MyLightPlugin)`. The `AzureOpenAIOptions` are loaded from configuration files and environment variables. A hosted service `(Worker)` handles the main execution logic. A home automation kernel is created with a collection of these plugins and added to the dependency injection container. 

      ```
      using HomeAutomation.Options;
      using HomeAutomation.Plugins;
      using Microsoft.Extensions.DependencyInjection;
      using Microsoft.Extensions.Hosting;
      using Microsoft.Extensions.Options;
      using Microsoft.SemanticKernel;
      using Microsoft.SemanticKernel.ChatCompletion;
      using Microsoft.SemanticKernel.Connectors.OpenAI;
      
      namespace HomeAutomation;
      
      internal static class Program
      {
          internal static async Task Main(string[] args)
          {
              HostApplicationBuilder builder = Host.CreateApplicationBuilder(args);
      
              // Actual code to execute is found in Worker class
              builder.Services.AddHostedService<Worker>();
      
              // Get configuration
              builder.Services.AddOptions<AzureOpenAIOptions>()
                              .Bind(builder.Configuration.GetSection(nameof(AzureOpenAIOptions)))
                              .ValidateDataAnnotations()
                              .ValidateOnStart();
      
              // Chat completion service that kernels will use
              builder.Services.AddSingleton<IChatCompletionService>(sp =>
              {
                  /*OpenAIOptions options = sp.GetRequiredService<IOptions<OpenAIOptions>>().Value;
      
                  // A custom HttpClient can be provided to this constructor
                  return new OpenAIChatCompletionService(options.ChatModelId, options.ApiKey);
      
                   Alternatively, you can use plain, Azure OpenAI after loading AzureOpenAIOptions instead
                     of OpenAI options with builder.Services.AddOptions:*/
      
                  AzureOpenAIOptions options = sp.GetRequiredService<IOptions<AzureOpenAIOptions>>().Value;
      
                  return new AzureOpenAIChatCompletionService(options.ChatDeploymentName, options.Endpoint, options.ApiKey); 
              });
      
              // Add plugins that can be used by kernels
              // The plugins are added as singletons so that they can be used by multiple kernels
              builder.Services.AddSingleton<MyTimePlugin>();
              builder.Services.AddSingleton<MyAlarmPlugin>();
              builder.Services.AddKeyedSingleton<MyLightPlugin>("OfficeLight");
              builder.Services.AddKeyedSingleton<MyLightPlugin>("PorchLight", (sp, key) =>
              {
                  return new MyLightPlugin(turnedOn: true);
              });
      
              /* To add an OpenAI or OpenAPI plugin, you need to be using Microsoft.SemanticKernel.Plugins.OpenApi.
                 Then create a temporary kernel, use it to load the plugin and add it as keyed singleton.
              Kernel kernel = new();
              KernelPlugin openAIPlugin = await kernel.ImportPluginFromOpenAIAsync("<plugin name>", new Uri("<OpenAI-plugin>"));
              builder.Services.AddKeyedSingleton<KernelPlugin>("MyImportedOpenAIPlugin", openAIPlugin);
      
              KernelPlugin openApiPlugin = await kernel.ImportPluginFromOpenApiAsync("<plugin name>", new Uri("<OpenAPI-plugin>"));
              builder.Services.AddKeyedSingleton<KernelPlugin>("MyImportedOpenApiPlugin", openApiPlugin);*/
      
              // Add a home automation kernel to the dependency injection container
              builder.Services.AddKeyedTransient<Kernel>("HomeAutomationKernel", (sp, key) =>
              {
                  // Create a collection of plugins that the kernel will use
                  KernelPluginCollection pluginCollection = [];
                  pluginCollection.AddFromObject(sp.GetRequiredService<MyTimePlugin>());
                  pluginCollection.AddFromObject(sp.GetRequiredService<MyAlarmPlugin>());
                  pluginCollection.AddFromObject(sp.GetRequiredKeyedService<MyLightPlugin>("OfficeLight"), "OfficeLight");
                  pluginCollection.AddFromObject(sp.GetRequiredKeyedService<MyLightPlugin>("PorchLight"), "PorchLight");
      
                  // When created by the dependency injection container, Semantic Kernel logging is included by default
                  return new Kernel(sp, pluginCollection);
              });
      
              using IHost host = builder.Build();
      
              await host.RunAsync();
          }
      }
      ```

1. Navigate to **Worker.cs** file, and update the line number 29, and **CTRL+S**.

    ```
    ToolCallBehavior = ToolCallBehavior.AutoInvokeKernelFunctions
    ```
    
1. Configure an Azure OpenAI endpoint by Opening a New **Terminal** click on **(...) (1)** next to **View** menu and select **Terminal (2)** > **New Terminal (3)**.

    ![](./Media/semtic-newterminal.png)

1. Execute the following commands to install the necessary packages.
    
    ```
    dotnet add package Microsoft.Extensions.Hosting --version 9.0.0-preview.3.24172.9
    dotnet add package Microsoft.Extensions.Options.DataAnnotations --version 9.0.0-preview.3.24172.9
    dotnet add package Microsoft.SemanticKernel --version 1.11.0
    ```

    >**Note**: These commands are used in a .NET Core or .NET 5+ project to add NuGet packages to the project. Here's what each command does:

    > **dotnet add package Microsoft.Extensions.Hosting --version 9.0.0-preview.3.24172.9**: Adds the Microsoft.Extensions.Hosting package to the project with a specific version (9.0.0-preview.3.24172.9). This package provides hosting and startup abstractions for .NET applications.

    > **dotnet add package Microsoft.Extensions.Options.DataAnnotations --version 9.0.0-preview.3.24172.9**: Adds the Microsoft.Extensions.Options.DataAnnotations package to the project with a specific version (9.0.0-preview.3.24172.9). This package extends the options framework in .NET to support data annotations for configuration objects.

    > **dotnet add package Microsoft.SemanticKernel --version 1.11.0**: Adds the Microsoft.SemanticKernel package to the project with a specific version (1.11.0). This package likely provides functionality related to semantic analysis and processing within the application.

1. To build and run the Home Automation application from the terminal use the following commands:

    ```PowerShell
    dotnet build
    dotnet run
    ```
    
    ![](./Media/dotnetbuild.png)

    > **Note**: Please disregard the warning.
    
    > **Note** The commands dotnet build and dotnet run are fundamental in .NET Core and .NET 5+ environments for building and running .NET applications locally on your machine.

1. After running `dotnet run`, you can ask a few questions and review the response. For example: `What time is it?` **(1)** and get the **Result (2)**.

    ![](./Media/miyagi-image100.png)

1. **Example 2:** `Set an alarm for 6:00 am.`

    ![](./Media/miyagi-image101.png)

1. To include additional questions, navigate to the **worker.cs** file and insert your new questions at **line number 32**.

    ![](./Media/miyagi-image102.png)

1. Alternatively, you can pose any question to in the terminal.

### Task 2: Configure Azure AI Search

In this task, you'll configure Azure AI Search by importing data from CosmosDB into a search index named "realestate-us-sample-index". You customize the index and create an indexer named "realestate-us-sample-indexer" to synchronize data. Finally, you verify the search functionality by querying data for "Seattle".

1. Navigate back to the **Azure portal** tab, in Search resources, services and docs (G+/) box at the top of the portal, enter **AI Search (1)**, and then select **AI Search (2)** under services.

    ![](./Media/miyagi-image25.png)

1. In **AI Foundry | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](./Media/L5T2S2.png)

1. In the overview tab of the search service, click on the **Import data**.

    ![](./Media/miyagi-image103.png)
   
1. From the drop-down select **Data Source** as **Samples (1)**, select the **CosmosDB hotels-sample (2)**, and click on **Next : Add cognitive skills (Optional) (3)**.

   ![](./Media/miyagi-image104.png)
   
1. In **Cognitive skills** leave as default and click on **Skip to: Customize target index**.

    ![](./Media/miyagi-image105.png)
   
1. In the **Customize target index**, Enter the index name as **realestate-us-sample-index** **(1)** and click on **Next: Create an indexer** **(2)**.

   ![](./Media/miyagi-image106.png)
   
1. In the **Create an indexer**, change the indexer name as **realestate-us-sample-indexer (1)** and click on **Submit (2)**.

   ![](./Media/miyagi-image107.png)
   
1. From the left navigation pane under navigate back to **Search management**, and select **Indexes (1)** then click on **realestate-us-sample-index (2)**.

    ![](./Media/L5T2S9.png)

    > **Note**: Please click on **Refresh** if the index is not yet visible.

1. Click on **realestate-us-sample-index** in the search bar enter **Seattle (1)** and click on **Search (2)** then view thw **Result (3)**.

   ![](./Media/miyagi-image(109).png)

### Summary

In this lab, you learned how to configure and run the Semantic Kernel sample by integrating the SDK into your project, setting up LLM providers, defining plugins, and executing the code. Additionally, you gained knowledge on configuring Azure AI Search, including creating or selecting an index, setting up fields, configuring Semantic Kernel to interact with Azure, defining plugins, and testing the integration for enhanced search capabilities.

### You have successfully completed this lab.

### Conclusion

By completing **Build Intelligent Apps with Microsoft's Copilot stack & Azure OpenAI**, you will gain the knowledge and hands-on experience needed to design and implement AI-powered solutions using Microsoft’s Copilot stack. You will understand how to effectively apply Generative AI, RAG patterns, and Semantic Kernel to real-world business scenarios, enabling you to build intelligent, context-aware Copilots that enhance productivity, streamline workflows, and deliver personalized user experiences. 
