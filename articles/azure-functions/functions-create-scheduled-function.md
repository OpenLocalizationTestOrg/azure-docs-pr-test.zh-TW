---
title: "在 Azure 中建立會按照排程來執行的函式 | Microsoft Docs"
description: "了解如何在 Azure 中建立函式，並使其按照您定義的排程來執行。"
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
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="af8ca-103">在 Azure 中建立由計時器觸發的函式</span><span class="sxs-lookup"><span data-stu-id="af8ca-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="af8ca-104">了解如何使用 Azure Functions 來建立函式，並使其按照您定義的排程來執行。</span><span class="sxs-lookup"><span data-stu-id="af8ca-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![在 Azure 入口網站中建立函式應用程式](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="af8ca-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="af8ca-106">Prerequisites</span></span>

<span data-ttu-id="af8ca-107">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="af8ca-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="af8ca-108">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="af8ca-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="af8ca-109">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="af8ca-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="af8ca-111">接下來，您要在新的函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="af8ca-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="af8ca-112">建立由計時器觸發的函式</span><span class="sxs-lookup"><span data-stu-id="af8ca-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="af8ca-113">展開函式應用程式，然後按一下 [Functions] 旁的 [+] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="af8ca-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="af8ca-114">如果這是您函式應用程式中的第一個函式，請選取 [自訂函式]。</span><span class="sxs-lookup"><span data-stu-id="af8ca-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="af8ca-115">這會顯示一組完整的函式範本。</span><span class="sxs-lookup"><span data-stu-id="af8ca-115">This displays the complete set of function templates.</span></span>

    ![Azure 入口網站中的 Functions 快速入門](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="af8ca-117">針對所需語言選取 **TimerTrigger** 的範本。</span><span class="sxs-lookup"><span data-stu-id="af8ca-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="af8ca-118">然後使用表格中所指定的設定︰</span><span class="sxs-lookup"><span data-stu-id="af8ca-118">Then use the settings as specified in the table:</span></span>

    ![在 Azure 入口網站中建立計時器觸發函式。](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="af8ca-120">設定</span><span class="sxs-lookup"><span data-stu-id="af8ca-120">Setting</span></span> | <span data-ttu-id="af8ca-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="af8ca-121">Suggested value</span></span> | <span data-ttu-id="af8ca-122">說明</span><span class="sxs-lookup"><span data-stu-id="af8ca-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="af8ca-123">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="af8ca-123">**Name your function**</span></span> | <span data-ttu-id="af8ca-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="af8ca-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="af8ca-125">定義計時器觸發函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="af8ca-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="af8ca-126">**[排程](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="af8ca-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="af8ca-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="af8ca-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="af8ca-128">含有六個欄位的 [CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)，它會將函式排程為每分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="af8ca-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="af8ca-129">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="af8ca-129">Click **Create**.</span></span> <span data-ttu-id="af8ca-130">系統隨即會以您所選的語言建立函式，並讓它每分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="af8ca-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="af8ca-131">檢視寫入到記錄的追蹤資訊以確認執行情形。</span><span class="sxs-lookup"><span data-stu-id="af8ca-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Azure 入口網站中的函式記錄檢視器。](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="af8ca-133">現在，您可以變更函式的排程，使其降低執行頻率，例如降低為每小時一次。</span><span class="sxs-lookup"><span data-stu-id="af8ca-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="af8ca-134">更新計時器排程</span><span class="sxs-lookup"><span data-stu-id="af8ca-134">Update the timer schedule</span></span>

1. <span data-ttu-id="af8ca-135">展開您的函式，然後按一下 [整合]。</span><span class="sxs-lookup"><span data-stu-id="af8ca-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="af8ca-136">您可以在這裡定義函式的輸入和輸出繫結，以及設定排程。</span><span class="sxs-lookup"><span data-stu-id="af8ca-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="af8ca-137">輸入 `0 0 */1 * * *` 作為新的 [排程] 值，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="af8ca-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![函式便會在 Azure 入口網站中更新計時器排程。](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="af8ca-139">您現在已擁有每小時執行一次的函式。</span><span class="sxs-lookup"><span data-stu-id="af8ca-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="af8ca-140">清除資源</span><span class="sxs-lookup"><span data-stu-id="af8ca-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="af8ca-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af8ca-141">Next steps</span></span>

<span data-ttu-id="af8ca-142">您已建立會根據排程來執行的函式。</span><span class="sxs-lookup"><span data-stu-id="af8ca-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="af8ca-143">如需計時器觸發程序的詳細資訊，請參閱[使用 Azure Functions 排程程式碼執行](functions-bindings-timer.md)。</span><span class="sxs-lookup"><span data-stu-id="af8ca-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>