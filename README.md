# Microsoft.Extensions.AI

https://www.nuget.org/packages/Microsoft.Extensions.AI.AzureAIInference/

https://learn.microsoft.com/en-us/collections/d2z1bmomeo55kr?source=learn

https://github.com/dotnet/ai-samples

![image](https://github.com/user-attachments/assets/2160239e-7816-47a5-8174-f8cf0f6490d9)

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

We input the **Github Key** input data

![image](https://github.com/user-attachments/assets/bb850318-502c-4566-a8af-a8bea4d244f7)

![image](https://github.com/user-attachments/assets/92bb5c5f-1078-4ecd-bca2-14ad8dae6cbf)

See the result

![image](https://github.com/user-attachments/assets/add56971-83b1-4d0c-9332-2600e0f3a18a)

Now we have to create an **Environmental Variable** called GH_TOKEN to store the Gihtub Token value

![image](https://github.com/user-attachments/assets/d0d4d86d-da90-4239-a754-20aacf21be27)

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

We are going to integrate the above sample in a Blazor Web App and deploy it to Azure

We first run **Visual Studio 2022** and create a new project

![image](https://github.com/user-attachments/assets/5abdd1f6-338d-4fa5-abdf-b4efce1aff59)

We select the **Blazor Web App** project template in Visual Studio 2022

![image](https://github.com/user-attachments/assets/0224afc3-d7e9-438e-b06c-8574d9e95256)

We input the project name and location and press the Next button

![image](https://github.com/user-attachments/assets/b560ed48-fc2b-498b-815e-dbcc9a9c7804)

We select the **.NET9** framework and press the Create button

![image](https://github.com/user-attachments/assets/9c287c36-e8f7-4074-b3c7-1081c9c39375)

We review the project folders and files structure

![image](https://github.com/user-attachments/assets/96da0d32-fa8c-4ad7-9e80-307b2d8785f1)

We add the **Microsoft.Extension.AI** Nuget package

```
NuGet\Install-Package Microsoft.Extensions.AI -Version 9.0.0-preview.9.24507.7
```

![image](https://github.com/user-attachments/assets/77f29fe7-ba4c-4caa-84af-ae7ce36bb3d4)

We create a new razor component

![image](https://github.com/user-attachments/assets/c5ccb215-bb0b-46c4-851b-4d2f36eb061f)

We input the razor component name

![image](https://github.com/user-attachments/assets/889c415b-3879-4592-8964-bae0becb0bfd)

We verify the new component was created

![image](https://github.com/user-attachments/assets/27c06302-5866-41b4-b977-e368295360cd)

We define the component UI, including **bootstrap5** styles

```razor
@page "/chat"
@using Azure.AI.Inference
@using Microsoft.Extensions.AI
@inject IJSRuntime JSRuntime

<h3>Chat with AI</h3>

<div class="mb-3">
    <label for="userInput" class="form-label">Your Question:</label>
    <input type="text" id="userInput" @bind="userInput" class="form-control" />
</div>

<button class="btn btn-primary" @onclick="SendMessage">Send</button>

<div class="mt-4">
    <h5>Response:</h5>
    <div class="border p-3 rounded" style="min-height: 100px;">
        @if (!string.IsNullOrEmpty(aiResponse))
        {
            @aiResponse
        }
        else
        {
            <span class="text-muted">No response yet.</span>
        }
    </div>
</div>

@code {
    private string userInput = string.Empty;
    private string aiResponse = string.Empty;

    private async Task SendMessage()
    {
        try
        {
            IChatClient client = new ChatCompletionsClient(
                new Uri("https://models.inference.ai.azure.com"),
                new AzureKeyCredential(Environment.GetEnvironmentVariable("GH_TOKEN")!))
                .AsChatClient("gpt-4o-mini");

            aiResponse = await client.CompleteAsync(userInput);
        }
        catch (Exception ex)
        {
            aiResponse = $"Error: {ex.Message}";
        }
    }
}
```





## 3. Sample 2: Chat + Conversation History

## 4. Sample 3: Chat streaming

## 5. Sample 4: Tool calling

## 6. Sample 5: Caching

## 7. Sample 6: Telemetry

## 8. Sample 7: Telemetry, Caching, and Tool Calling

## 9. Sample 8: Dependency Injection

## 10. Sample 9: Minimal Web API

