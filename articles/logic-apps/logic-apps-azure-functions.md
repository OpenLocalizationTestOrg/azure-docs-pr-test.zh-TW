---
title: "透過 Azure Functions 的適用於 Azure Logic Apps 的自訂程式碼 | Microsoft Docs"
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
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="9b878-103">透過 Azure Functions 新增並執行適用於 Logic Apps 的自訂程式碼</span><span class="sxs-lookup"><span data-stu-id="9b878-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="9b878-104">若要在邏輯應用程式中執行 C# 或 node.js 的自訂程式碼片段，您可以透過 Azure Functions 建立自訂函式。</span><span class="sxs-lookup"><span data-stu-id="9b878-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="9b878-105">[Azure Functions](../azure-functions/functions-overview.md) 提供 Microsoft Azure 中無伺服器運算的功能，並有助於執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="9b878-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="9b878-106">邏輯應用程式中欄位的進階格式設定或計算</span><span class="sxs-lookup"><span data-stu-id="9b878-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="9b878-107">在工作流程中執行計算。</span><span class="sxs-lookup"><span data-stu-id="9b878-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="9b878-108">利用 C# 或 node.js 中支援的函式來擴充邏輯應用程式功能</span><span class="sxs-lookup"><span data-stu-id="9b878-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="9b878-109">建立邏輯應用程式的自訂函式</span><span class="sxs-lookup"><span data-stu-id="9b878-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="9b878-110">建議您在 Azure Functions 入口網站中，從**一般 Webhook - 節點**或**一般 Webhook - C#** 範本建立新的函式。</span><span class="sxs-lookup"><span data-stu-id="9b878-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="9b878-111">結果會建立自動填入以接受來自邏輯應用程式之 `application/json` 的範本。</span><span class="sxs-lookup"><span data-stu-id="9b878-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="9b878-112">系統即會自動偵測您從這些範本建立的函式，並顯示於邏輯應用程式設計工具的 [我的區域中的 Azure Functions] 下方。</span><span class="sxs-lookup"><span data-stu-id="9b878-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="9b878-113">在 Azure 入口網站中函式的 [整合] 窗格上，您的範本應該會顯示將 [模式] 設為 [Webhook]，以及將 [Webhook 類型] 設為 [一般 JSON]。</span><span class="sxs-lookup"><span data-stu-id="9b878-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="9b878-114">Webhook 函數會接受要求，並透過 `data` 變數將它傳入方法。</span><span class="sxs-lookup"><span data-stu-id="9b878-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="9b878-115">您可以使用點標記法 (例如 `data.function-name`) 來存取承載的屬性。</span><span class="sxs-lookup"><span data-stu-id="9b878-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="9b878-116">例如，將日期時間值轉換為日期字串的簡單 JavaScript 函數看起來如以下範例︰</span><span class="sxs-lookup"><span data-stu-id="9b878-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="9b878-117">從 Logic Apps 呼叫 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9b878-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="9b878-118">若要列出您訂用帳戶中的容器，並選取您想要呼叫的函式，可在邏輯應用程式設計工具中，按一下 [動作] 功能表，然後從 [我的區域中的 Azure Functions] 中選取。</span><span class="sxs-lookup"><span data-stu-id="9b878-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="9b878-119">選取函式之後，系統會要求您指定輸入承載物件。</span><span class="sxs-lookup"><span data-stu-id="9b878-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="9b878-120">這個物件是邏輯應用程式要傳送到函式的訊息，且必須是 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9b878-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="9b878-121">例如，如果我想要傳入 Salesforce 觸發程序的**上次修改**日期，函式承載可能看起來如下範例：</span><span class="sxs-lookup"><span data-stu-id="9b878-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![上次修改日期][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="9b878-123">從函數觸發 Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9b878-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="9b878-124">您可以從函式內部觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b878-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="9b878-125">請參閱[做為可呼叫端點的邏輯應用程式](logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="9b878-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="9b878-126">建立含有手動觸發程序的邏輯應用程式，然後從您的函式內，產生 HTTP POST 到手動觸發程序 URL，其中包含您想要傳送到邏輯應用程式的承載。</span><span class="sxs-lookup"><span data-stu-id="9b878-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="9b878-127">從邏輯應用程式設計工具建立函式</span><span class="sxs-lookup"><span data-stu-id="9b878-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="9b878-128">您也可以從設計工具中建立 node.js webhook 函式。</span><span class="sxs-lookup"><span data-stu-id="9b878-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="9b878-129">首先，選取 [我的區域中的 Azure Functions]  ，然後選擇適用於您的函數的容器。</span><span class="sxs-lookup"><span data-stu-id="9b878-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="9b878-130">如果您還沒有容器，就必須從 [Azure Functions 入口網站](https://functions.azure.com/signin)建立一個。</span><span class="sxs-lookup"><span data-stu-id="9b878-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="9b878-131">然後選取 建立新的) 。</span><span class="sxs-lookup"><span data-stu-id="9b878-131">Then select **Create New**.</span></span>  

<span data-ttu-id="9b878-132">若要根據您想要計算的資料來產生範本，請指定您打算傳入函數的內容物件。</span><span class="sxs-lookup"><span data-stu-id="9b878-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="9b878-133">這個物件必須是 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9b878-133">This object must be a JSON object.</span></span> <span data-ttu-id="9b878-134">例如，如果您從 FTP 動作傳入檔案內容，內容承載可能看起來如下範例：</span><span class="sxs-lookup"><span data-stu-id="9b878-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![內容承載][2]

> [!NOTE]
> <span data-ttu-id="9b878-136">因為此物件無法轉換為字串，所以會直接將內容新增至 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="9b878-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="9b878-137">不過，如果物件不是 JSON 權杖 (也就是字串或 JSON 物件/陣列)，即會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9b878-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="9b878-138">若要將物件轉換為字串，請加上引號，如本文的第一個圖例所示。</span><span class="sxs-lookup"><span data-stu-id="9b878-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="9b878-139">設計工具接著會產生您可以內嵌建立的函數範本。</span><span class="sxs-lookup"><span data-stu-id="9b878-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="9b878-140">變數會根據您想要傳入函數的內容預先建立。</span><span class="sxs-lookup"><span data-stu-id="9b878-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
