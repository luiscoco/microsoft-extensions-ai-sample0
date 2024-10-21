# Microsoft.Extensions.AI

https://www.nuget.org/packages/Microsoft.Extensions.AI.AzureAIInference/

https://learn.microsoft.com/en-us/collections/d2z1bmomeo55kr?source=learn

https://github.com/dotnet/ai-samples

## 1. How to create GitHub Token (GH_TOKEN)

Navigate to the **GitHub AI Models** web page: https://github.com/marketplace/models

![image](https://github.com/user-attachments/assets/25a4fc82-3485-4964-b64e-e73af09b68e9)

Select the **AI Model**: gpt-4o-mini (https://github.com/marketplace/models/azure-openai/gpt-4o-mini)

![image](https://github.com/user-attachments/assets/c43ae989-5456-4090-bff0-f88e83d25fb5)

![image](https://github.com/user-attachments/assets/2af69732-d116-4985-8fee-0a1f19bdac9e)

We press in the **Get API key** button

![image](https://github.com/user-attachments/assets/64b9272b-7602-472f-81c8-a4b88ef5cfda)

We can also navigate to this web page to generate the GitHub Token: https://github.com/settings/tokens?type=beta

![image](https://github.com/user-attachments/assets/948ffb84-ee5e-4c90-b2aa-9c1230cc0261)

Now we have to create an **Environmental Variable** called GH_TOKEN to store the Gihtub Token value

![image](https://github.com/user-attachments/assets/d0d4d86d-da90-4239-a754-20aacf21be27)

We input the Github Key input data

![image](https://github.com/user-attachments/assets/bb850318-502c-4566-a8af-a8bea4d244f7)




## 2. Sample 1: Chat

```csharp
using Azure;
using Microsoft.Extensions.AI;

IChatClient client =
    new Azure.AI.Inference.ChatCompletionsClient(
        new("https://models.inference.ai.azure.com"),
        new AzureKeyCredential(Environment.GetEnvironmentVariable("GH_TOKEN")!))
    .AsChatClient("gpt-4o-mini");

Console.WriteLine(await client.CompleteAsync("What is AI?"));
```

## 3. Sample 2: Chat + Conversation History

## 4. Sample 3: Chat streaming

## 5. Sample 4: Tool calling

## 6. Sample 5: Caching

## 7. Sample 6: Telemetry

## 8. Sample 7: Telemetry, Caching, and Tool Calling

## 9. Sample 8: Dependency Injection

## 10. Sample 9: Minimal Web API

