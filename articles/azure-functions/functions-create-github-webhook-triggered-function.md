---
title: "aaaCreate GitHub webhook 所觸發的 Azure 中的函式 |Microsoft 文件"
description: "使用 Azure 函式 toocreate GitHub webhook 所叫用的無伺服器函式。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="3f9ff-103">建立由 GitHub Webhook 所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="3f9ff-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="3f9ff-104">深入了解如何 toocreate webhook GitHub 特定裝載與 HTTP 要求所觸發的函式。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook 觸發 hello Azure 入口網站中的函式](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="3f9ff-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="3f9ff-106">Prerequisites</span></span>

+ <span data-ttu-id="3f9ff-107">一個 GitHub 帳戶至少要有一個專案。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="3f9ff-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-108">An Azure subscription.</span></span> <span data-ttu-id="3f9ff-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="3f9ff-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="3f9ff-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="3f9ff-112">接下來，您會在 hello 新函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="3f9ff-113">建立 GitHub webhook 觸發函式</span><span class="sxs-lookup"><span data-stu-id="3f9ff-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="3f9ff-114">展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="3f9ff-115">如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="3f9ff-116">這會顯示 hello 組完整的函式樣板。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-116">This displays hello complete set of function templates.</span></span>

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="3f9ff-118">選取 hello **GitHub WebHook**所需語言的範本。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="3f9ff-119">**為您的函式命名**，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-119">**Name your function**, then select **Create**.</span></span>

     ![在 hello Azure 入口網站中建立 GitHub webhook 觸發函式](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="3f9ff-121">在新的函數中，按一下  **<> / Get 函式 URL**，然後複製並儲存 hello 值。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="3f9ff-122">請勿 hello 相同的動作，如**<> / 取得 GitHub 密碼**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="3f9ff-123">您可以使用這些值 tooconfigure hello webhook GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![檢閱 hello 函式程式碼](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="3f9ff-125">接下來，您會在 GitHub 存放庫中建立 Webhook。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="3f9ff-126">設定 hello webhook</span><span class="sxs-lookup"><span data-stu-id="3f9ff-126">Configure hello webhook</span></span>

1. <span data-ttu-id="3f9ff-127">在 GitHub 中瀏覽您所擁有的 tooa 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="3f9ff-128">您也可以使用已分歧的任何存放庫。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="3f9ff-129">如果您需要 toofork 儲存機制，使用<https://github.com/Azure-Samples/functions-quickstart>。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="3f9ff-130">按一下 [設定]，然後按一下 [Webhook] 和 [新增 Webhook]。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![新增 GitHub webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="3f9ff-132">使用 hello 資料表中所指定的設定，然後按一下 **新增 webhook**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![設定 hello webhook URL 和密碼](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="3f9ff-134">設定</span><span class="sxs-lookup"><span data-stu-id="3f9ff-134">Setting</span></span> | <span data-ttu-id="3f9ff-135">建議的值</span><span class="sxs-lookup"><span data-stu-id="3f9ff-135">Suggested value</span></span> | <span data-ttu-id="3f9ff-136">說明</span><span class="sxs-lookup"><span data-stu-id="3f9ff-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="3f9ff-137">**承載 URL**</span><span class="sxs-lookup"><span data-stu-id="3f9ff-137">**Payload URL**</span></span> | <span data-ttu-id="3f9ff-138">複製的值</span><span class="sxs-lookup"><span data-stu-id="3f9ff-138">Copied value</span></span> | <span data-ttu-id="3f9ff-139">使用所傳回的 hello 值**<> / Get 函式 URL**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="3f9ff-140">**祕密**</span><span class="sxs-lookup"><span data-stu-id="3f9ff-140">**Secret**</span></span>   | <span data-ttu-id="3f9ff-141">複製的值</span><span class="sxs-lookup"><span data-stu-id="3f9ff-141">Copied value</span></span> | <span data-ttu-id="3f9ff-142">使用所傳回的 hello 值**<> / 取得 GitHub 密碼**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="3f9ff-143">**內容類型**</span><span class="sxs-lookup"><span data-stu-id="3f9ff-143">**Content type**</span></span> | <span data-ttu-id="3f9ff-144">application/json</span><span class="sxs-lookup"><span data-stu-id="3f9ff-144">application/json</span></span> | <span data-ttu-id="3f9ff-145">hello 函式必須要有 JSON 裝載。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="3f9ff-146">事件觸發程序</span><span class="sxs-lookup"><span data-stu-id="3f9ff-146">Event triggers</span></span> | <span data-ttu-id="3f9ff-147">讓我選取個別事件</span><span class="sxs-lookup"><span data-stu-id="3f9ff-147">Let me select individual events</span></span> | <span data-ttu-id="3f9ff-148">我們只想 tootrigger 問題註解的事件。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="3f9ff-149">問題註解</span><span class="sxs-lookup"><span data-stu-id="3f9ff-149">Issue comment</span></span> |  |

<span data-ttu-id="3f9ff-150">現在，hello webhook 加入新的問題註解的使用者設定的 tootrigger 是您的函式。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="3f9ff-151">測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="3f9ff-151">Test hello function</span></span>

1. <span data-ttu-id="3f9ff-152">在您的 GitHub 儲存機制，開啟 hello**問題**新的瀏覽器視窗中索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="3f9ff-153">在 hello 新視窗中，按一下 **新議題**，請輸入標題，然後按一下**提交新議題**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="3f9ff-154">Hello 問題輸入註解，然後按一下**註解**。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![新增 GitHub 問題註解。](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="3f9ff-156">返回 toohello 入口網站，並檢視 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="3f9ff-157">您應該會看到 hello 新註解文字的追蹤項目。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-157">You should see a trace entry with hello new comment text.</span></span>

     ![檢視 hello hello 記錄檔中的註解文字。](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="3f9ff-159">清除資源</span><span class="sxs-lookup"><span data-stu-id="3f9ff-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="3f9ff-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f9ff-160">Next steps</span></span>

<span data-ttu-id="3f9ff-161">您已建立函式，此函式會在收到 GitHub Webhook 所提出的要求時開始執行。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="3f9ff-162">如需 Webhook 觸發程序的詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](functions-bindings-http-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="3f9ff-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
