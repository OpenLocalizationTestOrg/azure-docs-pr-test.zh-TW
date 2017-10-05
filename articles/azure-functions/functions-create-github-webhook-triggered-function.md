---
title: "在 GitHub Webhook 所觸發的 Azure 中建立函式 | Microsoft Docs"
description: "使用 Azure Functions 建立 GitHub Webhook 所叫用的無伺服器函式。"
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
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="af100-103">建立由 GitHub Webhook 所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="af100-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="af100-104">了解如何使用 GitHub 專屬的承載來建立由 HTTP Webhook 要求所觸發的函式。</span><span class="sxs-lookup"><span data-stu-id="af100-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Azure 入口網站中由 GitHub Webhook 所觸發的函式](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="af100-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="af100-106">Prerequisites</span></span>

+ <span data-ttu-id="af100-107">一個 GitHub 帳戶至少要有一個專案。</span><span class="sxs-lookup"><span data-stu-id="af100-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="af100-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="af100-108">An Azure subscription.</span></span> <span data-ttu-id="af100-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="af100-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="af100-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="af100-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="af100-112">接下來，您要在新的函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="af100-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="af100-113">建立 GitHub webhook 觸發函式</span><span class="sxs-lookup"><span data-stu-id="af100-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="af100-114">展開函式應用程式，然後按一下 [Functions] 旁的 [+] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="af100-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="af100-115">如果這是您函式應用程式中的第一個函式，請選取 [自訂函式]。</span><span class="sxs-lookup"><span data-stu-id="af100-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="af100-116">這會顯示一組完整的函式範本。</span><span class="sxs-lookup"><span data-stu-id="af100-116">This displays the complete set of function templates.</span></span>

    ![Azure 入口網站中的 Functions 快速入門](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="af100-118">針對所需語言選取 **GitHub WebHook** 範本。</span><span class="sxs-lookup"><span data-stu-id="af100-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="af100-119">**為您的函式命名**，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="af100-119">**Name your function**, then select **Create**.</span></span>

     ![在 Azure 入口網站中建立 GitHub Webhook 觸發的函式](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="af100-121">在您的新函式中，按一下 [</> 取得函式 URL]，然後複製並儲存值。</span><span class="sxs-lookup"><span data-stu-id="af100-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="af100-122">對 [</> 取得 GitHub 祕密] 執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="af100-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="af100-123">您可使用這些值在 GitHub 中設定 Webhook。</span><span class="sxs-lookup"><span data-stu-id="af100-123">You use these values to configure the webhook in GitHub.</span></span>

    ![檢閱函式程式碼](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="af100-125">接下來，您會在 GitHub 存放庫中建立 Webhook。</span><span class="sxs-lookup"><span data-stu-id="af100-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="af100-126">設定 Webhook</span><span class="sxs-lookup"><span data-stu-id="af100-126">Configure the webhook</span></span>

1. <span data-ttu-id="af100-127">在 GitHub 中，瀏覽至您自己的存放庫。</span><span class="sxs-lookup"><span data-stu-id="af100-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="af100-128">您也可以使用已分歧的任何存放庫。</span><span class="sxs-lookup"><span data-stu-id="af100-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="af100-129">如果您需要將存放庫分岔，請使用 <https://github.com/Azure-Samples/functions-quickstart>。</span><span class="sxs-lookup"><span data-stu-id="af100-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="af100-130">按一下 [設定]，然後按一下 [Webhook] 和 [新增 Webhook]。</span><span class="sxs-lookup"><span data-stu-id="af100-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![新增 GitHub webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="af100-132">使用資料表中指定的設定，然後按一下 [新增 Webhook]。</span><span class="sxs-lookup"><span data-stu-id="af100-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![設定 webhook URL 和密碼](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="af100-134">設定</span><span class="sxs-lookup"><span data-stu-id="af100-134">Setting</span></span> | <span data-ttu-id="af100-135">建議的值</span><span class="sxs-lookup"><span data-stu-id="af100-135">Suggested value</span></span> | <span data-ttu-id="af100-136">說明</span><span class="sxs-lookup"><span data-stu-id="af100-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="af100-137">**承載 URL**</span><span class="sxs-lookup"><span data-stu-id="af100-137">**Payload URL**</span></span> | <span data-ttu-id="af100-138">複製的值</span><span class="sxs-lookup"><span data-stu-id="af100-138">Copied value</span></span> | <span data-ttu-id="af100-139">使用 **</> 取得函式 URL** 所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="af100-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="af100-140">**祕密**</span><span class="sxs-lookup"><span data-stu-id="af100-140">**Secret**</span></span>   | <span data-ttu-id="af100-141">複製的值</span><span class="sxs-lookup"><span data-stu-id="af100-141">Copied value</span></span> | <span data-ttu-id="af100-142">使用 **</> 取得 GitHub 祕密**所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="af100-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="af100-143">**內容類型**</span><span class="sxs-lookup"><span data-stu-id="af100-143">**Content type**</span></span> | <span data-ttu-id="af100-144">application/json</span><span class="sxs-lookup"><span data-stu-id="af100-144">application/json</span></span> | <span data-ttu-id="af100-145">函式預期使用 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="af100-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="af100-146">事件觸發程序</span><span class="sxs-lookup"><span data-stu-id="af100-146">Event triggers</span></span> | <span data-ttu-id="af100-147">讓我選取個別事件</span><span class="sxs-lookup"><span data-stu-id="af100-147">Let me select individual events</span></span> | <span data-ttu-id="af100-148">我們只想對問題註解事件來觸發。</span><span class="sxs-lookup"><span data-stu-id="af100-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="af100-149">問題註解</span><span class="sxs-lookup"><span data-stu-id="af100-149">Issue comment</span></span> |  |

<span data-ttu-id="af100-150">現在，GitHub Webhook 已設定成在新增問題註解時觸發您的函式。</span><span class="sxs-lookup"><span data-stu-id="af100-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="af100-151">測試函式</span><span class="sxs-lookup"><span data-stu-id="af100-151">Test the function</span></span>

1. <span data-ttu-id="af100-152">在 GitHub 存放庫的新瀏覽器視窗中開啟 [問題] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="af100-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="af100-153">在新視窗中，按一下 [新增問題]，輸入標題，然後按一下 [提交新問題]。</span><span class="sxs-lookup"><span data-stu-id="af100-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="af100-154">在問題中輸入註解，然後按一下 [註解] 。</span><span class="sxs-lookup"><span data-stu-id="af100-154">In the issue, type a comment and click **Comment**.</span></span>

    ![新增 GitHub 問題註解。](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="af100-156">返回入口網站，並檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="af100-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="af100-157">您應該會看到具有新註解文字的追蹤項目。</span><span class="sxs-lookup"><span data-stu-id="af100-157">You should see a trace entry with the new comment text.</span></span>

     ![檢視記錄中的註解文字。](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="af100-159">清除資源</span><span class="sxs-lookup"><span data-stu-id="af100-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="af100-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af100-160">Next steps</span></span>

<span data-ttu-id="af100-161">您已建立函式，此函式會在收到 GitHub Webhook 所提出的要求時開始執行。</span><span class="sxs-lookup"><span data-stu-id="af100-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="af100-162">如需 Webhook 觸發程序的詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](functions-bindings-http-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="af100-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
