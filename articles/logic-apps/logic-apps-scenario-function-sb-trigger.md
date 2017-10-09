---
title: "aaaScenario-觸發程序邏輯應用程式與 Azure 函式和 Azure 服務匯流排 |Microsoft 文件"
description: "建立函式 tootrigger 邏輯應用程式使用 Azure 函式和 Azure 服務匯流排"
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
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="312d3-103">案例：使用 Azure Functions 和 Azure 服務匯流排觸發邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="312d3-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="312d3-104">當您需要 toodeploy 長時間執行的接聽程式或工作時，您可以使用 Azure 函式 toocreate 觸發程序邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="312d3-105">例如，您可以建立一個將會在佇列上接聽的函數，接著立即引發邏輯應用程式成為推送觸發程序。</span><span class="sxs-lookup"><span data-stu-id="312d3-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="312d3-106">建置 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="312d3-106">Build hello logic app</span></span>
<span data-ttu-id="312d3-107">在此範例中，您有需要 toobe 觸發每個邏輯應用程式執行的函式。</span><span class="sxs-lookup"><span data-stu-id="312d3-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="312d3-108">首先，建立具有 HTTP 要求觸發程序的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="312d3-109">每當接收佇列訊息時，hello 函式會呼叫該端點。</span><span class="sxs-lookup"><span data-stu-id="312d3-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="312d3-110">建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-110">Create a logic app.</span></span>
2. <span data-ttu-id="312d3-111">選取 hello **Manual-在收到 HTTP 要求時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="312d3-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="312d3-112">（選擇性） 使用這類工具與 hello 佇列訊息指定 JSON 結構描述 toouse [jsonschema.net](http://jsonschema.net)。</span><span class="sxs-lookup"><span data-stu-id="312d3-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="312d3-113">貼上 hello 觸發程序中的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="312d3-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="312d3-114">結構描述可協助了解 hello 圖形的 hello 更輕鬆地透過 hello 流程資料和流程內容的 hello 設計工具。</span><span class="sxs-lookup"><span data-stu-id="312d3-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="312d3-115">新增之後收到佇列訊息時，想要 toooccur 任何其他步驟。</span><span class="sxs-lookup"><span data-stu-id="312d3-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="312d3-116">例如，透過 Office 365 傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="312d3-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="312d3-117">儲存 hello 邏輯應用程式 toogenerate hello 回呼 URL hello 觸發程序 toothis 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="312d3-118">hello URL 會出現在 hello 觸發程序卡上。</span><span class="sxs-lookup"><span data-stu-id="312d3-118">hello URL appears on hello trigger card.</span></span>

![hello 回呼 URL 會出現在 hello 觸發程序卡][1]

## <a name="build-hello-function"></a><span data-ttu-id="312d3-120">建置 hello 函式</span><span class="sxs-lookup"><span data-stu-id="312d3-120">Build hello function</span></span>
<span data-ttu-id="312d3-121">接下來，您必須建立做為 hello 觸發程序，並接聽 toohello 佇列的函式。</span><span class="sxs-lookup"><span data-stu-id="312d3-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="312d3-122">在 hello [Azure 函式的入口網站](https://functions.azure.com/signin)，選取**新函式**，然後選取 hello **ServiceBusQueueTrigger-C#**範本。</span><span class="sxs-lookup"><span data-stu-id="312d3-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions 入口網站][2]
2. <span data-ttu-id="312d3-124">設定 hello 連接 toohello Service Bus 佇列，而 github 會使用 hello Azure 服務匯流排 SDK`OnMessageReceive()`接聽程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="312d3-125">使用 hello 佇列訊息的觸發程序，以撰寫的基本功能 toocall hello 邏輯應用程式端點 （先前建立）。</span><span class="sxs-lookup"><span data-stu-id="312d3-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="312d3-126">以下是函數的完整範例。</span><span class="sxs-lookup"><span data-stu-id="312d3-126">Here's a full example of a function.</span></span> <span data-ttu-id="312d3-127">hello 範例會使用`application/json`訊息內容型別，但是您可以變更此類型為必要。</span><span class="sxs-lookup"><span data-stu-id="312d3-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="312d3-128">tootest，新增佇列訊息透過工具[Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer)。</span><span class="sxs-lookup"><span data-stu-id="312d3-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="312d3-129">請參閱引發 hello 函式會收到 hello 訊息之後，立即 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="312d3-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
