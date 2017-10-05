---
title: "從 Azure 入口網站建立您的第一個函式 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站來建立您的第一個 Azure 函式以進行無伺服器執行。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="ece6a-103">在 Azure 入口網站中建立您的第一個函式</span><span class="sxs-lookup"><span data-stu-id="ece6a-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="ece6a-104">Azure Functions 可讓您在無伺服器環境中執行程式碼，而不需要先建立 VM 或發佈 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="ece6a-105">在本主題中，請學習如何使用 Functions 在 Azure 入口網站中建立「hello world」函式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![在 Azure 入口網站中建立函式應用程式](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="ece6a-107">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="ece6a-107">Log in to Azure</span></span>

<span data-ttu-id="ece6a-108">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ece6a-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="ece6a-109">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="ece6a-109">Create a function app</span></span>

<span data-ttu-id="ece6a-110">您必須擁有函式應用程式以便主控函式的執行。</span><span class="sxs-lookup"><span data-stu-id="ece6a-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="ece6a-111">函式應用程式可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。</span><span class="sxs-lookup"><span data-stu-id="ece6a-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="ece6a-112">接下來，您要在新的函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="ece6a-113"><a name="create-function"></a>建立由 HTTP 觸發的函式</span><span class="sxs-lookup"><span data-stu-id="ece6a-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="ece6a-114">展開新的函式應用程式，然後按一下 [Functions] 旁的 **+** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ece6a-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="ece6a-115">在 [即刻開始使用] 頁面上，選取 [WebHook + API]，並**選擇您的函式語言**，然後按一下 [建立此函式]。</span><span class="sxs-lookup"><span data-stu-id="ece6a-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Azure 入口網站中的 Functions 快速入門。](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="ece6a-117">系統隨即會使用由 HTTP 觸發之函式的範本，以您所選的語言來建立函式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="ece6a-118">您可以藉由傳送 HTTP 要求來執行新的函式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="ece6a-119">測試函式</span><span class="sxs-lookup"><span data-stu-id="ece6a-119">Test the function</span></span>

1. <span data-ttu-id="ece6a-120">在新的函式中，按一下 [</> 取得函式 URL]，選取 [預設 (函式索引鍵)]，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="ece6a-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![從 Azure 入口網站複製函式 URL](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="ece6a-122">將函式 URL 貼入瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="ece6a-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="ece6a-123">將查詢字串 `&name=<yourname>` 附加至此 URL，並按鍵盤上的 `Enter` 鍵執行要求。</span><span class="sxs-lookup"><span data-stu-id="ece6a-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="ece6a-124">下列是 Edge 瀏覽器中函式所傳回的範例回應：</span><span class="sxs-lookup"><span data-stu-id="ece6a-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![瀏覽器中的函式回應。](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="ece6a-126">要求 URL 預設會包含所需金鑰，以便透過 HTTP 存取您的函式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="ece6a-127">當函式執行時，系統會將追蹤資訊寫入到記錄中。</span><span class="sxs-lookup"><span data-stu-id="ece6a-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="ece6a-128">若要查看上次執行的追蹤輸出，請在入口網站中返回您的函式，然後按一下畫面底部的向上箭號來展開**記錄**。</span><span class="sxs-lookup"><span data-stu-id="ece6a-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Azure 入口網站中的函式記錄檢視器。](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ece6a-130">清除資源</span><span class="sxs-lookup"><span data-stu-id="ece6a-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="ece6a-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ece6a-131">Next steps</span></span>

<span data-ttu-id="ece6a-132">您已使用簡單的 HTTP 觸發函式建立了函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ece6a-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="ece6a-133">如需詳細資訊，請參閱 [Azure Functions HTTP 和 webhook 繫結](functions-bindings-http-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="ece6a-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



