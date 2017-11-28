---
title: "您的第一個函式從 hello Azure 入口網站的 aaaCreate |Microsoft 文件"
description: "深入了解如何使用無伺服器執行的函式的第一個 Azure toocreate hello Azure 入口網站。"
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="3a114-103">在 hello Azure 入口網站中建立您的第一個函式</span><span class="sxs-lookup"><span data-stu-id="3a114-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="3a114-104">Azure 的函式可讓您在無伺服器環境中執行您的程式碼，而不需要 toofirst 建立 VM，或發行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a114-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="3a114-105">本主題中，了解如何 toouse 函式 toocreate hello Azure 入口網站中的"hello world"函式。</span><span class="sxs-lookup"><span data-stu-id="3a114-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![在 hello Azure 入口網站中建立函式應用程式](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="3a114-107">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="3a114-107">Log in tooAzure</span></span>

<span data-ttu-id="3a114-108">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3a114-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="3a114-109">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="3a114-109">Create a function app</span></span>

<span data-ttu-id="3a114-110">您必須擁有您的函式的函式應用程式 toohost hello 執行。</span><span class="sxs-lookup"><span data-stu-id="3a114-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="3a114-111">函式應用程式可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。</span><span class="sxs-lookup"><span data-stu-id="3a114-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="3a114-112">接下來，您會在 hello 新函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="3a114-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="3a114-113"><a name="create-function"></a>建立由 HTTP 觸發的函式</span><span class="sxs-lookup"><span data-stu-id="3a114-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="3a114-114">展開新函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。</span><span class="sxs-lookup"><span data-stu-id="3a114-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="3a114-115">在 hello**快速入門**頁面上，選取**WebHook + API**，**選擇的語言**函式，然後按一下**建立此函數**.</span><span class="sxs-lookup"><span data-stu-id="3a114-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![在 hello Azure 入口網站中的函式快速入門。](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="3a114-117">函式會建立在選擇 HTTP 觸發函式使用 hello 範本的語言。</span><span class="sxs-lookup"><span data-stu-id="3a114-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="3a114-118">您可以藉由傳送 HTTP 要求執行 hello 新函式。</span><span class="sxs-lookup"><span data-stu-id="3a114-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="3a114-119">測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="3a114-119">Test hello function</span></span>

1. <span data-ttu-id="3a114-120">在新的函式中，按一下 </> 取得函式 URL，選取 預設 (函式索引鍵)，然後按一下複製。</span><span class="sxs-lookup"><span data-stu-id="3a114-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![複製 hello Azure 入口網站中的 hello 函式 URL](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="3a114-122">貼入瀏覽器的網址列中的 hello 函式的 URL。</span><span class="sxs-lookup"><span data-stu-id="3a114-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="3a114-123">附加 hello 查詢字串`&name=<yourname>`toothis URL 和按 hello`Enter`您鍵盤 tooexecute hello 要求金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a114-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="3a114-124">hello 以下是 hello 回應 hello Edge 瀏覽器中的 hello 函式所傳回的範例：</span><span class="sxs-lookup"><span data-stu-id="3a114-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![函式回應 hello 瀏覽器中。](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="3a114-126">URL 包含索引鍵所需，根據預設，tooaccess hello 要求您透過 HTTP 的函式。</span><span class="sxs-lookup"><span data-stu-id="3a114-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="3a114-127">當您的函式執行時，追蹤資訊會寫入 toohello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3a114-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="3a114-128">toosee hello 追蹤輸出，從上一個執行 hello，tooyour 函式傳回 hello 入口網站中，按一下向上箭號，在 hello 底部 hello 螢幕 tooexpand hello**記錄**。</span><span class="sxs-lookup"><span data-stu-id="3a114-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![函式會記錄檢視器中 hello Azure 入口網站。](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="3a114-130">清除資源</span><span class="sxs-lookup"><span data-stu-id="3a114-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="3a114-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a114-131">Next steps</span></span>

<span data-ttu-id="3a114-132">您已使用簡單的 HTTP 觸發函式建立了函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a114-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="3a114-133">如需詳細資訊，請參閱 [Azure Functions HTTP 和 webhook 繫結](functions-bindings-http-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="3a114-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



