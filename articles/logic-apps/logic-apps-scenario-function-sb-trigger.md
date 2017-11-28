---
title: "案例 - 使用 Azure Functions 與 Azure 服務匯流排觸發邏輯應用程式 | Microsoft Docs"
description: "使用 Azure Functions 和 Azure 服務匯流排建立觸發邏輯應用程式的函式"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="14533-103">案例：使用 Azure Functions 和 Azure 服務匯流排觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="14533-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="14533-104">當您需要部署長時間執行的接聽程式或工作時，可以使用 Azure Functions 來建立邏輯應用程式的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="14533-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="14533-105">例如，您可以建立一個將會在佇列上接聽的函數，接著立即引發邏輯應用程式成為推送觸發程序。</span><span class="sxs-lookup"><span data-stu-id="14533-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="14533-106">建置邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="14533-106">Build the logic app</span></span>
<span data-ttu-id="14533-107">在此範例中，您會有針對需要觸發的每個邏輯應用程式執行的函數。</span><span class="sxs-lookup"><span data-stu-id="14533-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="14533-108">首先，建立具有 HTTP 要求觸發程序的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="14533-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="14533-109">每當收到佇列訊息時，函數即會呼叫該端點。</span><span class="sxs-lookup"><span data-stu-id="14533-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="14533-110">建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="14533-110">Create a logic app.</span></span>
2. <span data-ttu-id="14533-111">選取 [手動 - 收到 HTTP 要求時] 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="14533-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="14533-112">您可以選擇性地利用 [jsonschema.net](http://jsonschema.net)之類的工具，來指定要與佇列訊息搭配使用的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="14533-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="14533-113">在觸發程序中貼上結構描述。</span><span class="sxs-lookup"><span data-stu-id="14533-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="14533-114">結構描述有助於讓設計工具了解資料的形式，而且可以更輕鬆地透過工作流程傳送屬性。</span><span class="sxs-lookup"><span data-stu-id="14533-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="14533-115">新增您想要在收到佇列訊息之後發生的任何其他步驟。</span><span class="sxs-lookup"><span data-stu-id="14533-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="14533-116">例如，透過 Office 365 傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="14533-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="14533-117">儲存邏輯應用程式，以產生此邏輯應用程式的觸發程序的回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="14533-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="14533-118">URL 會出現在觸發程序卡上。</span><span class="sxs-lookup"><span data-stu-id="14533-118">The URL appears on the trigger card.</span></span>

![回呼 URL 會出現在觸發程序卡上][1]

## <a name="build-the-function"></a><span data-ttu-id="14533-120">建置函數</span><span class="sxs-lookup"><span data-stu-id="14533-120">Build the function</span></span>
<span data-ttu-id="14533-121">接著，您必須建立一個函數，以做為觸發程序並接聽佇列。</span><span class="sxs-lookup"><span data-stu-id="14533-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="14533-122">在 [Azure Functions 入口網站](https://functions.azure.com/signin)中，依序選取 [新增函數] 與 [ServiceBusQueueTrigger - C#] 範本。</span><span class="sxs-lookup"><span data-stu-id="14533-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions 入口網站][2]
2. <span data-ttu-id="14533-124">設定服務匯流排佇列的連接，其可使用服務匯流排 SDK `OnMessageReceive()` 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="14533-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="14533-125">撰寫基本的函數，使用佇列訊息做為觸發程序來呼叫邏輯應用程式端點 (稍早建立的)。</span><span class="sxs-lookup"><span data-stu-id="14533-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="14533-126">以下是函數的完整範例。</span><span class="sxs-lookup"><span data-stu-id="14533-126">Here's a full example of a function.</span></span> <span data-ttu-id="14533-127">此範例會使用 `application/json` 訊息內容類型，但是您可以視需要變更此類型。</span><span class="sxs-lookup"><span data-stu-id="14533-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="14533-128">若要進行測試，請透過 [服務匯流排總管](https://github.com/paolosalvatori/ServiceBusExplorer)之類的工具來新增佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="14533-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="14533-129">請查看在函數收到訊息之後立即引發的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="14533-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
