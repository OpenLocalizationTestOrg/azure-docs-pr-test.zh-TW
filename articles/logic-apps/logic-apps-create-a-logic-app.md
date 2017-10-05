---
title: "在雲端應用程式與雲端服務之間建立第一個工作流程 - Azure Logic Apps | Microsoft Docs"
description: "在 Azure Logic Apps 中建立及執行工作流程，以自動執行系統整合和企業應用程式整合 (EAI) 案例的商務程序"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "工作流程, 雲端應用程式, 雲端服務, 商務程序, 系統整合, 企業應用程式整合, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="0c849-104">建立第一個邏輯應用程式工作流程來自動執行雲端應用程式與雲端服務之間的程序</span><span class="sxs-lookup"><span data-stu-id="0c849-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="0c849-105">不需撰寫任何程式碼，您可以在建立並執行工作流程時利用 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)，更輕鬆快速地自動執行商務程序。</span><span class="sxs-lookup"><span data-stu-id="0c849-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="0c849-106">第一個範例示範如何建立基本邏輯應用程式工作流程，以檢查網站上新內容的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="0c849-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="0c849-107">當新項目出現在網站的摘要時，邏輯應用程式會從 Outlook 或 Gmail 帳戶傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0c849-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="0c849-108">若要建立並執行邏輯應用程式，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="0c849-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="0c849-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c849-109">An Azure subscription.</span></span> <span data-ttu-id="0c849-110">如果您沒有訂用帳戶，您可以[開始使用免費 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="0c849-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="0c849-111">否則，您可以[註冊隨用隨付訂用帳戶](https://azure.microsoft.com/pricing/purchase-options/)。</span><span class="sxs-lookup"><span data-stu-id="0c849-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="0c849-112">您的 Azure 訂用帳戶用於邏輯應用程式使用量計費。</span><span class="sxs-lookup"><span data-stu-id="0c849-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="0c849-113">了解 Azure Logic Apps 的[使用量計量](../logic-apps/logic-apps-pricing.md)和[計價](https://azure.microsoft.com/pricing/details/logic-apps)方式。</span><span class="sxs-lookup"><span data-stu-id="0c849-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="0c849-114">此外，這個範例需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="0c849-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="0c849-115">Outlook.com、Office 365 Outlook 或 Gmail 帳戶</span><span class="sxs-lookup"><span data-stu-id="0c849-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="0c849-116">如果您有個人 [Microsoft 帳戶](https://account.microsoft.com/account)，您便有 Outlook.com 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c849-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="0c849-117">否則，如果您有 Azure 工作或學校帳戶，您便有 **Office 365 Outlook** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c849-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="0c849-118">網站的 RSS 摘要連結。</span><span class="sxs-lookup"><span data-stu-id="0c849-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="0c849-119">這個範例會使用 [CNN.com 網站的頭條報導 RSS 摘要](http://rss.cnn.com/rss/cnn_topstories.rss)：`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="0c849-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="0c849-120">新增可啟動工作流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="0c849-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="0c849-121">[*觸發程序*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)是啟動邏輯應用程式工作流程的事件，而且是邏輯應用程式所需的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="0c849-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="0c849-122">登入 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="0c849-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0c849-123">從左側功能表中，選擇 [新增] > [企業整合] > [邏輯應用程式]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c849-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure 入口網站, 新增, 企業整合, 邏輯應用程式](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="0c849-125">您也可以選擇 [新增]，然後在搜尋方塊中輸入 `logic app`，接著按 Enter。</span><span class="sxs-lookup"><span data-stu-id="0c849-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="0c849-126">然後選擇 [邏輯應用程式] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="0c849-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="0c849-127">為您的邏輯應用程式命名並選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c849-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="0c849-128">現在建立或選取 Azure 資源群組，以協助您組織及管理相關的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0c849-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="0c849-129">最後，選取用於裝載您的邏輯應用程式的資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="0c849-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="0c849-130">當您準備就緒，選擇 [釘選到儀表板]，然後選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0c849-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![邏輯應用程式詳細資料](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="0c849-132">當您選取 [釘選到儀表板] 時，邏輯應用程式會在部署後出現於 Azure 儀表板，並自動開啟。</span><span class="sxs-lookup"><span data-stu-id="0c849-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="0c849-133">如果邏輯應用程式未出現在儀表板上，請在 [所有資源] 圖格上選擇 [更多資訊]，然後選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="0c849-134">在左側功能表上，選擇 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="0c849-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="0c849-135">在 [企業整合] 底下，選擇 [Logic Apps]，然後選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="0c849-136">當您第一次開啟邏輯應用程式時，邏輯應用程式設計工具會顯示您可開始使用的範本。</span><span class="sxs-lookup"><span data-stu-id="0c849-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="0c849-137">暫時選擇 [空白邏輯應用程式]，以便從頭建置邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="0c849-138">邏輯應用程式的設計工具隨即開啟並顯示可用的服務和*觸發程序*，您可以使用邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0c849-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="0c849-139">在搜尋方塊中輸入 `RSS`，然後選取此觸發程序︰**RSS - 摘要項目發佈時**</span><span class="sxs-lookup"><span data-stu-id="0c849-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS 觸發程序](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="0c849-141">輸入您想要追蹤之網站的 RSS 摘要連結。</span><span class="sxs-lookup"><span data-stu-id="0c849-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="0c849-142">您也可以變更 [頻率] 和 [間隔]。</span><span class="sxs-lookup"><span data-stu-id="0c849-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="0c849-143">這些設定會決定邏輯應用程式檢查新項目並傳回該時間範圍內找到之所有項目的頻率。</span><span class="sxs-lookup"><span data-stu-id="0c849-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="0c849-144">例如，讓我們每天檢查張貼至 CNN 網站的頭條報導。</span><span class="sxs-lookup"><span data-stu-id="0c849-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![使用 RSS 摘要、頻率和間隔設定觸發程序](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="0c849-146">儲存您目前的工作。</span><span class="sxs-lookup"><span data-stu-id="0c849-146">Save your work for now.</span></span> <span data-ttu-id="0c849-147">(在設計工具命令列上選擇 [儲存]。)</span><span class="sxs-lookup"><span data-stu-id="0c849-147">(On the designer command bar, choose **Save**.)</span></span>

   ![儲存您的邏輯應用程式](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="0c849-149">當您儲存時，邏輯應用程式會上線，但邏輯應用程式目前只會檢查指定之 RSS 摘要中的新項目。</span><span class="sxs-lookup"><span data-stu-id="0c849-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="0c849-150">為了讓此範例更加實用，我們新增了邏輯應用程式在觸發程序引發後執行的動作。</span><span class="sxs-lookup"><span data-stu-id="0c849-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="0c849-151">新增可回應觸發程序的動作</span><span class="sxs-lookup"><span data-stu-id="0c849-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="0c849-152">[動作](./logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0c849-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="0c849-153">將觸發程序新增至邏輯應用程式之後，您可以新增一個動作，以對該觸發程序所產生的資料執行作業。</span><span class="sxs-lookup"><span data-stu-id="0c849-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="0c849-154">在我們的範例中，我們現在新增一個動作，以在新項目出現於網站的 RSS 摘要時傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0c849-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="0c849-155">在設計工具中，於您的觸發程序下選擇 [新增步驟] > **[新增動作]**，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0c849-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![新增動作](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="0c849-157">設計工具會顯示[可用的連接器](../connectors/apis-list.md)，因此您可以選取要在觸發程序引發時執行的動作。</span><span class="sxs-lookup"><span data-stu-id="0c849-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="0c849-158">根據您的電子郵件帳戶，遵循 Outlook 或 Gmail 的步驟。</span><span class="sxs-lookup"><span data-stu-id="0c849-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="0c849-159">若要從 Outlook 帳戶傳送電子郵件，請在搜尋方塊中輸入 `outlook`。</span><span class="sxs-lookup"><span data-stu-id="0c849-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="0c849-160">在 [服務] 之下，針對個人 Microsoft 帳戶選擇 [Outlook.com]，或針對 Azure 工作或學校帳戶選擇 [Office 365 Outlook]。</span><span class="sxs-lookup"><span data-stu-id="0c849-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="0c849-161">在 [動作] 之下，選取 [傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="0c849-161">Under **Actions**, select **Send an email**.</span></span>

       ![選取 Outlook「傳送電子郵件」動作](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="0c849-163">若要從 Gmail 帳戶傳送電子郵件，請在搜尋方塊中輸入 `gmail`。</span><span class="sxs-lookup"><span data-stu-id="0c849-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="0c849-164">在 [動作] 之下，選取 [傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="0c849-164">Under **Actions**, select **Send email**.</span></span>

       ![選擇「Gmail - 傳送電子郵件」](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="0c849-166">當系統提示您輸入認證時，使用您電子郵件帳戶的使用者名稱和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="0c849-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="0c849-167">提供此動作的詳細資料 (如目的地電子郵件地址)，然後選擇要納入電子郵件中資料的參數，例如︰</span><span class="sxs-lookup"><span data-stu-id="0c849-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![選取要納入電子郵件中的資料](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="0c849-169">因此如果您選擇 Outlook，邏輯應用程式可能如此範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0c849-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![已完成的邏輯應用程式](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="0c849-171">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0c849-171">Save your changes.</span></span> <span data-ttu-id="0c849-172">(在設計工具命令列上選擇 [儲存]。)</span><span class="sxs-lookup"><span data-stu-id="0c849-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="0c849-173">您現在可以手動執行邏輯應用程式進行測試。</span><span class="sxs-lookup"><span data-stu-id="0c849-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="0c849-174">在設計工具命令列上選擇 [執行]。</span><span class="sxs-lookup"><span data-stu-id="0c849-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="0c849-175">否則，您可以讓邏輯應用程式根據您設定的排程，檢查指定的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="0c849-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="0c849-176">如果邏輯應用程式找到新的項目，則邏輯應用程式會傳送電子郵件，其中包含您選取的資料。</span><span class="sxs-lookup"><span data-stu-id="0c849-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="0c849-177">如果找不到任何新項目，邏輯應用程式會略過傳送電子郵件的動作。</span><span class="sxs-lookup"><span data-stu-id="0c849-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="0c849-178">若要監視及檢查邏輯應用程式的執行和觸發歷程記錄，請在邏輯應用程式功能表上選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="0c849-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![監視及檢視邏輯應用程式執行和觸發歷程記錄](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="0c849-180">如果找不到您預期的資料，請嘗試在命令列上選擇 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="0c849-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="0c849-181">若要深入了解邏輯應用程式的狀態或執行和觸發歷程記錄，或診斷應用程式邏輯，請參閱[針對邏輯應用程式進行疑難排解](logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="0c849-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="0c849-182">邏輯應用程式會繼續執行，直到您關閉應用程式為止。</span><span class="sxs-lookup"><span data-stu-id="0c849-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="0c849-183">若要暫時關閉應用程式，請在邏輯應用程式功能表上選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="0c849-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="0c849-184">在命令列上選擇 [停用]。</span><span class="sxs-lookup"><span data-stu-id="0c849-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="0c849-185">恭喜，您剛設定並執行第一個基本邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="0c849-186">您也了解如何輕鬆地建立可自動執行程序的工作流程，並整合雲端應用程式和雲端服務 - 全都不需要程式碼。</span><span class="sxs-lookup"><span data-stu-id="0c849-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="0c849-187">管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0c849-187">Manage your logic app</span></span>

<span data-ttu-id="0c849-188">若要管理您的應用程式，您可以執行一些工作，如檢查狀態、編輯、檢視歷程記錄、關閉或刪除邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="0c849-189">登入 [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="0c849-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0c849-190">在左側功能表上，選擇 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="0c849-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="0c849-191">在 [企業整合] 底下選擇 [Logic Apps]。</span><span class="sxs-lookup"><span data-stu-id="0c849-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="0c849-192">選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c849-192">Select your logic app.</span></span> 

   <span data-ttu-id="0c849-193">在邏輯應用程式功能表中，您可以找到下列邏輯應用程式管理工作︰</span><span class="sxs-lookup"><span data-stu-id="0c849-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="0c849-194">Task</span><span class="sxs-lookup"><span data-stu-id="0c849-194">Task</span></span>|<span data-ttu-id="0c849-195">步驟</span><span class="sxs-lookup"><span data-stu-id="0c849-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="0c849-196">檢視應用程式的狀態、執行歷程記錄和一般資訊</span><span class="sxs-lookup"><span data-stu-id="0c849-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="0c849-197">選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="0c849-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="0c849-198">編輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0c849-198">Edit your app</span></span> | <span data-ttu-id="0c849-199">選擇 [邏輯應用程式設計工具]。</span><span class="sxs-lookup"><span data-stu-id="0c849-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="0c849-200">檢視應用程式的工作流程 JSON 定義</span><span class="sxs-lookup"><span data-stu-id="0c849-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="0c849-201">選擇 [邏輯應用程式程式碼檢視]。</span><span class="sxs-lookup"><span data-stu-id="0c849-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="0c849-202">檢視在邏輯應用程式上執行的作業</span><span class="sxs-lookup"><span data-stu-id="0c849-202">View operations performed on your logic app</span></span> | <span data-ttu-id="0c849-203">選擇 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="0c849-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="0c849-204">檢視邏輯應用程式過去的版本</span><span class="sxs-lookup"><span data-stu-id="0c849-204">View past versions for your logic app</span></span> | <span data-ttu-id="0c849-205">選擇 [版本]。</span><span class="sxs-lookup"><span data-stu-id="0c849-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="0c849-206">暫時關閉應用程式</span><span class="sxs-lookup"><span data-stu-id="0c849-206">Turn off your app temporarily</span></span> | <span data-ttu-id="0c849-207">選擇 [概觀]，然後在命令列上選擇 [停用]。</span><span class="sxs-lookup"><span data-stu-id="0c849-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="0c849-208">刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="0c849-208">Delete your app</span></span> | <span data-ttu-id="0c849-209">選擇 [概觀]，然後在命令列上選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0c849-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="0c849-210">輸入邏輯應用程式的名稱，然後選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0c849-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="0c849-211">取得說明</span><span class="sxs-lookup"><span data-stu-id="0c849-211">Get help</span></span>

<span data-ttu-id="0c849-212">若要提出問題、回答問題以及了解其他 Azure Logic Apps 使用者的做法，請造訪 [Azure Logic Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="0c849-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="0c849-213">若要改善 Azure Logic Apps 和連接器，請在 [Azure Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)上票選或提交想法。</span><span class="sxs-lookup"><span data-stu-id="0c849-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c849-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c849-214">Next steps</span></span>

*  [<span data-ttu-id="0c849-215">新增條件並執行工作流程</span><span class="sxs-lookup"><span data-stu-id="0c849-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="0c849-216">邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="0c849-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="0c849-217">從 Azure Resource Manager 範本建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0c849-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
