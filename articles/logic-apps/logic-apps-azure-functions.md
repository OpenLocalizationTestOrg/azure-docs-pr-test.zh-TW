---
title: "aaaCustom Azure 邏輯應用程式與 Azure 函式的程式碼 |Microsoft 文件"
description: "使用 Azure Functions 建立並執行適用於 Azure Logic Apps 的自訂程式碼"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="9604b-103">透過 Azure Functions 新增並執行適用於 Logic Apps 的自訂程式碼</span><span class="sxs-lookup"><span data-stu-id="9604b-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="9604b-104">toorun 自訂程式碼片段的 C# 或 node.js 邏輯應用程式中的，您可以建立自訂函式，透過 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="9604b-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="9604b-105">[Azure Functions](../azure-functions/functions-overview.md) 提供 Microsoft Azure 中無伺服器運算的功能，並有助於執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="9604b-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="9604b-106">邏輯應用程式中欄位的進階格式設定或計算</span><span class="sxs-lookup"><span data-stu-id="9604b-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="9604b-107">在工作流程中執行計算。</span><span class="sxs-lookup"><span data-stu-id="9604b-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="9604b-108">擴充功能，支援以 C# 或 node.js 的 hello 邏輯應用程式的功能</span><span class="sxs-lookup"><span data-stu-id="9604b-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="9604b-109">建立邏輯應用程式的自訂函式</span><span class="sxs-lookup"><span data-stu-id="9604b-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="9604b-110">我們建議您建立函式可在 hello Azure 函式的入口網站，從 hello**泛型 Webhook-節點**或**泛型 Webhook-C#**範本。</span><span class="sxs-lookup"><span data-stu-id="9604b-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="9604b-111">hello 結果建立自動填入內容的範本接受`application/json`從邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9604b-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="9604b-112">您從這些範本建立的函式會自動偵測，而且會在邏輯應用程式的設計工具出現在 hello **Azure 函式在我的區域。**</span><span class="sxs-lookup"><span data-stu-id="9604b-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="9604b-113">Hello hello 上的 Azure 入口網站中**整合**窗格為您的函式中，您的範本應該會顯示**模式**設定得**Webhook**和**Webhook 類型**設定得**泛型 JSON**。</span><span class="sxs-lookup"><span data-stu-id="9604b-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="9604b-114">Webhook 函式接受要求，並將它傳遞到 hello 方法，透過`data`變數。</span><span class="sxs-lookup"><span data-stu-id="9604b-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="9604b-115">您可以使用點標記法，例如存取承載 hello 屬性`data.function-name`。</span><span class="sxs-lookup"><span data-stu-id="9604b-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="9604b-116">例如，簡單的 JavaScript 函式，將日期時間值轉換成日期字串看起來像下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="9604b-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="9604b-117">從 Logic Apps 呼叫 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9604b-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="9604b-118">在您的訂用帳戶和您想 toocall，在邏輯應用程式設計師中，選取的 hello 函式的 toolist hello 容器按一下 hello**動作**功能表，然後選取從**Azure 函式在我的區域**。</span><span class="sxs-lookup"><span data-stu-id="9604b-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="9604b-119">您選取 hello 函式之後，您就詢問 toospecify 輸入的裝載物件。</span><span class="sxs-lookup"><span data-stu-id="9604b-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="9604b-120">此物件是 hello 邏輯應用程式傳送 toohello 函式，而且必須是 JSON 物件的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="9604b-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="9604b-121">例如，如果您想要在 hello toopass**上次修改**日期 Salesforce 觸發程序，從 hello 函式的內容可能類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="9604b-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![上次修改日期][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="9604b-123">從函數觸發 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9604b-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="9604b-124">您可以從函式內部觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9604b-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="9604b-125">請參閱[做為可呼叫端點的邏輯應用程式](logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="9604b-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="9604b-126">建立了手動觸發程序邏輯應用程式，然後從您的函式內產生且您想要傳送 toohello 邏輯應用程式的 hello 承載 HTTP POST toohello 手動觸發程序 URL。</span><span class="sxs-lookup"><span data-stu-id="9604b-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="9604b-127">從邏輯應用程式設計工具建立函式</span><span class="sxs-lookup"><span data-stu-id="9604b-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="9604b-128">您也可以從 hello 設計工具建立 node.js webhook 函式。</span><span class="sxs-lookup"><span data-stu-id="9604b-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="9604b-129">首先，選取 [我的區域中的 Azure Functions]  ，然後選擇適用於您的函數的容器。</span><span class="sxs-lookup"><span data-stu-id="9604b-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="9604b-130">如果您還沒有容器，您需要從 hello 一個 toocreate [Azure 函式的入口網站](https://functions.azure.com/signin)。</span><span class="sxs-lookup"><span data-stu-id="9604b-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="9604b-131">然後選取 建立新的) 。</span><span class="sxs-lookup"><span data-stu-id="9604b-131">Then select **Create New**.</span></span>  

<span data-ttu-id="9604b-132">toogenerate 想 toocompute，hello 資料為基礎的範本會指定您計劃 toopass 到函式的 hello 內容物件。</span><span class="sxs-lookup"><span data-stu-id="9604b-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="9604b-133">這個物件必須是 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9604b-133">This object must be a JSON object.</span></span> <span data-ttu-id="9604b-134">比方說，如果您從 FTP 動作傳入 hello 檔案內容，hello 內容承載看起來像本範例中：</span><span class="sxs-lookup"><span data-stu-id="9604b-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![內容承載][2]

> [!NOTE]
> <span data-ttu-id="9604b-136">因為此物件未轉換為字串，hello 的內容新增直接 toohello JSON 裝載。</span><span class="sxs-lookup"><span data-stu-id="9604b-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="9604b-137">不過，如果 hello 物件不是 JSON 權杖 （也就是字串或 JSON 物件/陣列），就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9604b-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="9604b-138">本文章中的 hello 第一個圖例中所示，toocast hello 物件做為字串，加上引號。</span><span class="sxs-lookup"><span data-stu-id="9604b-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="9604b-139">hello 設計工具會產生您可以建立內嵌函式樣板。</span><span class="sxs-lookup"><span data-stu-id="9604b-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="9604b-140">變數會預先建立根據您計劃 toopass hello 函式的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="9604b-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
