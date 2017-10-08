---
title: "在 Azure 中的排程執行的函式 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate azure 中執行的函式根據您定義的排程。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="cf0da-103">在 Azure 中建立由計時器觸發的函式</span><span class="sxs-lookup"><span data-stu-id="cf0da-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="cf0da-104">了解如何 toouse Azure 函式 toocreate 執行的函式以您定義的排程。</span><span class="sxs-lookup"><span data-stu-id="cf0da-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![在 hello Azure 入口網站中建立函式應用程式](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="cf0da-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="cf0da-106">Prerequisites</span></span>

<span data-ttu-id="cf0da-107">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="cf0da-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="cf0da-108">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="cf0da-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="cf0da-109">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="cf0da-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="cf0da-111">接下來，您會在 hello 新函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="cf0da-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="cf0da-112">建立由計時器觸發的函式</span><span class="sxs-lookup"><span data-stu-id="cf0da-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="cf0da-113">展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。</span><span class="sxs-lookup"><span data-stu-id="cf0da-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="cf0da-114">如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。</span><span class="sxs-lookup"><span data-stu-id="cf0da-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="cf0da-115">這會顯示 hello 組完整的函式樣板。</span><span class="sxs-lookup"><span data-stu-id="cf0da-115">This displays hello complete set of function templates.</span></span>

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="cf0da-117">選取 hello **TimerTrigger**所需語言的範本。</span><span class="sxs-lookup"><span data-stu-id="cf0da-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="cf0da-118">然後使用 hello 資料表中所指定的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="cf0da-118">Then use hello settings as specified in hello table:</span></span>

    ![Hello Azure 入口網站中建立計時器觸發函式。](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="cf0da-120">設定</span><span class="sxs-lookup"><span data-stu-id="cf0da-120">Setting</span></span> | <span data-ttu-id="cf0da-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="cf0da-121">Suggested value</span></span> | <span data-ttu-id="cf0da-122">說明</span><span class="sxs-lookup"><span data-stu-id="cf0da-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="cf0da-123">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="cf0da-123">**Name your function**</span></span> | <span data-ttu-id="cf0da-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="cf0da-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="cf0da-125">定義 hello 計時器觸發函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="cf0da-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="cf0da-126">**[排程](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="cf0da-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="cf0da-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="cf0da-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="cf0da-128">六個欄位[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)，它會排程函式 toorun 每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="cf0da-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="cf0da-129">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cf0da-129">Click **Create**.</span></span> <span data-ttu-id="cf0da-130">系統隨即會以您所選的語言建立函式，並讓它每分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="cf0da-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="cf0da-131">藉由檢視追蹤資訊寫入 toohello 記錄檔，請確認執行。</span><span class="sxs-lookup"><span data-stu-id="cf0da-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![函式會記錄檢視器中 hello Azure 入口網站。](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="cf0da-133">現在，您可以變更 hello 函式的排程，使其執行較少，例如每個小時一次。</span><span class="sxs-lookup"><span data-stu-id="cf0da-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="cf0da-134">更新 hello 計時器排程</span><span class="sxs-lookup"><span data-stu-id="cf0da-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="cf0da-135">展開您的函式，然後按一下 [整合]。</span><span class="sxs-lookup"><span data-stu-id="cf0da-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="cf0da-136">這是定義輸入和輸出繫結您的函式和也設定 hello 排程位置。</span><span class="sxs-lookup"><span data-stu-id="cf0da-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="cf0da-137">輸入 `0 0 */1 * * *` 作為新的 排程 值，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="cf0da-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![函式會更新計時器 hello Azure 入口網站中的排程。](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="cf0da-139">您現在已擁有每小時執行一次的函式。</span><span class="sxs-lookup"><span data-stu-id="cf0da-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="cf0da-140">清除資源</span><span class="sxs-lookup"><span data-stu-id="cf0da-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="cf0da-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf0da-141">Next steps</span></span>

<span data-ttu-id="cf0da-142">您已建立會根據排程來執行的函式。</span><span class="sxs-lookup"><span data-stu-id="cf0da-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="cf0da-143">如需計時器觸發程序的詳細資訊，請參閱[使用 Azure Functions 排程程式碼執行](functions-bindings-timer.md)。</span><span class="sxs-lookup"><span data-stu-id="cf0da-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>