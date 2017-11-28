---
title: "aaaCreate 您雲端應用程式和雲端服務-Azure 邏輯應用程式之間的第一個工作流程 |Microsoft 文件"
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
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="d03b6-104">建立您的第一個邏輯應用程式的雲端應用程式和雲端服務之間的工作流程 tooautomate 程序</span><span class="sxs-lookup"><span data-stu-id="d03b6-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="d03b6-105">不需撰寫任何程式碼，您可以在建立並執行工作流程時利用 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)，更輕鬆快速地自動執行商務程序。</span><span class="sxs-lookup"><span data-stu-id="d03b6-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="d03b6-106">第一個範例顯示如何 toocreate 基本邏輯應用程式工作流程，以檢查 RSS 摘要，可在網站上的新內容。</span><span class="sxs-lookup"><span data-stu-id="d03b6-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="d03b6-107">當新項目出現在 hello 網站摘要中時，hello 邏輯應用程式會傳送電子郵件從 Outlook 或 Gmail 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="d03b6-108">toocreate，以及執行邏輯應用程式，您會需要這些項目：</span><span class="sxs-lookup"><span data-stu-id="d03b6-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="d03b6-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-109">An Azure subscription.</span></span> <span data-ttu-id="d03b6-110">如果您沒有訂用帳戶，您可以[開始使用免費 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="d03b6-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="d03b6-111">否則，您可以[註冊隨用隨付訂用帳戶](https://azure.microsoft.com/pricing/purchase-options/)。</span><span class="sxs-lookup"><span data-stu-id="d03b6-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="d03b6-112">您的 Azure 訂用帳戶用於邏輯應用程式使用量計費。</span><span class="sxs-lookup"><span data-stu-id="d03b6-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="d03b6-113">了解 Azure Logic Apps 的[使用量計量](../logic-apps/logic-apps-pricing.md)和[計價](https://azure.microsoft.com/pricing/details/logic-apps)方式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="d03b6-114">此外，這個範例需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="d03b6-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="d03b6-115">Outlook.com、Office 365 Outlook 或 Gmail 帳戶</span><span class="sxs-lookup"><span data-stu-id="d03b6-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="d03b6-116">如果您有個人 [Microsoft 帳戶](https://account.microsoft.com/account)，您便有 Outlook.com 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="d03b6-117">否則，如果您有 Azure 工作或學校帳戶，您便有 **Office 365 Outlook** 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="d03b6-118">連結 tooa 網站的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="d03b6-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="d03b6-119">這個範例會使用 hello [RSS 摘要中的最上層的劇本從 hello CNN.com 網站](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="d03b6-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="d03b6-120">新增可啟動工作流程的觸發程序</span><span class="sxs-lookup"><span data-stu-id="d03b6-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="d03b6-121">A [*觸發程序*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)啟動邏輯的應用程式工作流程的事件，而邏輯應用程式所需的 hello 第一個項目。</span><span class="sxs-lookup"><span data-stu-id="d03b6-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="d03b6-122">登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="d03b6-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="d03b6-123">從 hello 左窗格中，選擇 **新增** > **企業整合** > **邏輯應用程式**如下所示：</span><span class="sxs-lookup"><span data-stu-id="d03b6-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure 入口網站, 新增, 企業整合, 邏輯應用程式](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="d03b6-125">您也可以選擇**新增**，然後在 [hello] 搜尋方塊中，輸入`logic app`，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="d03b6-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="d03b6-126">然後選擇 [邏輯應用程式] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="d03b6-127">為您的邏輯應用程式命名並選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="d03b6-128">現在建立或選取 Azure 資源群組，以協助您組織及管理相關的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d03b6-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="d03b6-129">最後，選取裝載應用程式邏輯的 hello 資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="d03b6-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="d03b6-130">當您準備好時，選擇**Pin toodashboard**然後**建立**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![邏輯應用程式詳細資料](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="d03b6-132">當您選取**Pin toodashboard**，邏輯應用程式部署之後，會出現在 hello Azure 儀表板，並會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="d03b6-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="d03b6-133">邏輯應用程式不會出現在 hello 儀表板，在 hello**所有資源**磚中，選擇**更看到**，並選取邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="d03b6-134">或在 hello 左窗格中，選擇 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="d03b6-135">在 [企業整合] 底下，選擇 [Logic Apps]，然後選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="d03b6-136">當您第一次開啟 hello 的應用程式邏輯時，hello 邏輯應用程式的設計工具會顯示您可以使用啟動 tooget 範本。</span><span class="sxs-lookup"><span data-stu-id="d03b6-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="d03b6-137">暫時選擇 [空白邏輯應用程式]，以便從頭建置邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="d03b6-138">hello 邏輯應用程式的設計工具隨即開啟並顯示可用的服務和*觸發程序*，您可以使用邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d03b6-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="d03b6-139">在 hello 搜尋方塊中，輸入`RSS`，然後選取 此觸發程序： **RSS-發行摘要項目時**</span><span class="sxs-lookup"><span data-stu-id="d03b6-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS 觸發程序](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="d03b6-141">輸入您想 tootrack hello 網站的 RSS 摘要 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="d03b6-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="d03b6-142">您也可以變更 [頻率] 和 [間隔]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="d03b6-143">這些設定會決定邏輯應用程式檢查新項目並傳回該時間範圍內找到之所有項目的頻率。</span><span class="sxs-lookup"><span data-stu-id="d03b6-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="d03b6-144">針對此範例中，讓我們來檢查每一天的最上層的劇本張貼 toohello 可以使用網站。</span><span class="sxs-lookup"><span data-stu-id="d03b6-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![使用 RSS 摘要、頻率和間隔設定觸發程序](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="d03b6-146">儲存您目前的工作。</span><span class="sxs-lookup"><span data-stu-id="d03b6-146">Save your work for now.</span></span> <span data-ttu-id="d03b6-147">(在 hello 設計工具命令列上選擇 **儲存**。)</span><span class="sxs-lookup"><span data-stu-id="d03b6-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![儲存您的邏輯應用程式](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="d03b6-149">當您儲存、 邏輯應用程式上線，但目前，邏輯應用程式只會檢查新的項目中的 hello 指定 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="d03b6-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="d03b6-150">此範例中更有用的我們加入觸發程序後，執行邏輯應用程式的動作會引發 toomake。</span><span class="sxs-lookup"><span data-stu-id="d03b6-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="d03b6-151">加入回應 tooyour 觸發程序的動作</span><span class="sxs-lookup"><span data-stu-id="d03b6-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="d03b6-152">[動作](./logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。</span><span class="sxs-lookup"><span data-stu-id="d03b6-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="d03b6-153">新增觸發程序 tooyour 邏輯應用程式之後，您可以加入動作 tooperform 操作該觸發程序所產生的資料。</span><span class="sxs-lookup"><span data-stu-id="d03b6-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="d03b6-154">範例中，我們現在會加入新項目出現時傳送電子郵件中 hello 網站的 RSS 摘要的動作。</span><span class="sxs-lookup"><span data-stu-id="d03b6-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="d03b6-155">在 hello 設計工具，在您的觸發程序中，選擇**新步驟** > **將動作加入**如下所示：</span><span class="sxs-lookup"><span data-stu-id="d03b6-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![新增動作](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="d03b6-157">hello 設計工具會顯示[可用的連接器](../connectors/apis-list.md)，因此觸發程序引發時，您可以選取動作 tooperform。</span><span class="sxs-lookup"><span data-stu-id="d03b6-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="d03b6-158">根據您的電子郵件帳戶，請在 Outlook 或 Gmail 遵循 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d03b6-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="d03b6-159">toosend 電子郵件從 Outlook 帳戶，在 hello 搜尋方塊中輸入`outlook`。</span><span class="sxs-lookup"><span data-stu-id="d03b6-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="d03b6-160">在 [服務] 之下，針對個人 Microsoft 帳戶選擇 [Outlook.com]，或針對 Azure 工作或學校帳戶選擇 [Office 365 Outlook]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="d03b6-161">在 [動作] 之下，選取 [傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-161">Under **Actions**, select **Send an email**.</span></span>

       ![選取 Outlook「傳送電子郵件」動作](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="d03b6-163">toosend 電子郵件是來自您的 Gmail 帳戶，請在 [hello] 搜尋方塊中，輸入`gmail`。</span><span class="sxs-lookup"><span data-stu-id="d03b6-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="d03b6-164">在 [動作] 之下，選取 [傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-164">Under **Actions**, select **Send email**.</span></span>

       ![選擇「Gmail - 傳送電子郵件」](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="d03b6-166">當系統提示您輸入認證時，hello 使用者名稱和密碼登入您的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03b6-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="d03b6-167">提供此動作，像是 hello 目的地電子郵件地址，hello 詳細資料，並選擇 hello 資料 tooinclude hello 參數 hello 電子郵件，例如：</span><span class="sxs-lookup"><span data-stu-id="d03b6-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![電子郵件中的選取資料 tooinclude](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="d03b6-169">因此如果您選擇 Outlook，邏輯應用程式可能如此範例所示︰</span><span class="sxs-lookup"><span data-stu-id="d03b6-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![已完成的邏輯應用程式](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="d03b6-171">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="d03b6-171">Save your changes.</span></span> <span data-ttu-id="d03b6-172">(在 hello 設計工具命令列上選擇 **儲存**。)</span><span class="sxs-lookup"><span data-stu-id="d03b6-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="d03b6-173">您現在可以手動執行邏輯應用程式進行測試。</span><span class="sxs-lookup"><span data-stu-id="d03b6-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="d03b6-174">在 hello 設計工具命令列上選擇 **執行**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="d03b6-175">否則，您可以讓您檢查 hello 指定 RSS 摘要 hello 排程設定為基礎的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="d03b6-176">如果應用程式邏輯尋找新的項目，hello 邏輯應用程式會傳送電子郵件，其中包含您選取的資料。</span><span class="sxs-lookup"><span data-stu-id="d03b6-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="d03b6-177">如果找不到任何新的項目，應用程式邏輯會略過傳送電子郵件的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="d03b6-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="d03b6-178">toomonitor 和核取的執行邏輯應用程式，並觸發歷程記錄，在邏輯應用程式功能表上的選擇 **概觀**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![監視及檢視邏輯應用程式執行和觸發歷程記錄](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="d03b6-180">如果找不到預期在 hello 命令列的 hello 資料再試一次選擇**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="d03b6-181">toolearn 深入了解您的邏輯應用程式狀態或執行，並觸發歷程記錄或 toodiagnose 邏輯應用程式，請參閱[疑難排解應用程式邏輯](logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="d03b6-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="d03b6-182">邏輯應用程式會繼續執行，直到您關閉應用程式為止。</span><span class="sxs-lookup"><span data-stu-id="d03b6-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="d03b6-183">現在，在邏輯應用程式功能表上的應用程式關閉 tooturn 選擇**概觀**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="d03b6-184">在 hello 命令列上選擇 **停用**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="d03b6-185">恭喜，您剛設定並執行第一個基本邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="d03b6-186">您也了解如何輕鬆地建立可自動執行程序的工作流程，並整合雲端應用程式和雲端服務 - 全都不需要程式碼。</span><span class="sxs-lookup"><span data-stu-id="d03b6-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="d03b6-187">管理邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="d03b6-187">Manage your logic app</span></span>

<span data-ttu-id="d03b6-188">toomanage 應用程式，您可以執行工作，例如檢查 hello 狀態、 編輯、 檢視歷程記錄、 關閉或刪除邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="d03b6-189">登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="d03b6-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="d03b6-190">在 hello 左窗格中，選擇 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="d03b6-191">在 [企業整合] 底下選擇 [Logic Apps]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="d03b6-192">選取您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d03b6-192">Select your logic app.</span></span> 

   <span data-ttu-id="d03b6-193">在 hello 邏輯應用程式功能表中，您可以找到這些邏輯應用程式管理工作：</span><span class="sxs-lookup"><span data-stu-id="d03b6-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="d03b6-194">Task</span><span class="sxs-lookup"><span data-stu-id="d03b6-194">Task</span></span>|<span data-ttu-id="d03b6-195">步驟</span><span class="sxs-lookup"><span data-stu-id="d03b6-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="d03b6-196">檢視應用程式的狀態、執行歷程記錄和一般資訊</span><span class="sxs-lookup"><span data-stu-id="d03b6-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="d03b6-197">選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="d03b6-198">編輯應用程式</span><span class="sxs-lookup"><span data-stu-id="d03b6-198">Edit your app</span></span> | <span data-ttu-id="d03b6-199">選擇 [邏輯應用程式設計工具]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="d03b6-200">檢視應用程式的工作流程 JSON 定義</span><span class="sxs-lookup"><span data-stu-id="d03b6-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="d03b6-201">選擇 [邏輯應用程式程式碼檢視]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="d03b6-202">檢視在邏輯應用程式上執行的作業</span><span class="sxs-lookup"><span data-stu-id="d03b6-202">View operations performed on your logic app</span></span> | <span data-ttu-id="d03b6-203">選擇 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="d03b6-204">檢視邏輯應用程式過去的版本</span><span class="sxs-lookup"><span data-stu-id="d03b6-204">View past versions for your logic app</span></span> | <span data-ttu-id="d03b6-205">選擇 [版本]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="d03b6-206">暫時關閉應用程式</span><span class="sxs-lookup"><span data-stu-id="d03b6-206">Turn off your app temporarily</span></span> | <span data-ttu-id="d03b6-207">選擇**概觀**，然後在 hello 命令列上選擇 **停用**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="d03b6-208">刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="d03b6-208">Delete your app</span></span> | <span data-ttu-id="d03b6-209">選擇**概觀**，然後在 hello 命令列上選擇 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="d03b6-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="d03b6-210">輸入邏輯應用程式的名稱，然後選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d03b6-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="d03b6-211">取得說明</span><span class="sxs-lookup"><span data-stu-id="d03b6-211">Get help</span></span>

<span data-ttu-id="d03b6-212">tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="d03b6-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d03b6-213">toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="d03b6-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d03b6-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d03b6-214">Next steps</span></span>

*  [<span data-ttu-id="d03b6-215">新增條件並執行工作流程</span><span class="sxs-lookup"><span data-stu-id="d03b6-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="d03b6-216">邏輯應用程式範本</span><span class="sxs-lookup"><span data-stu-id="d03b6-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="d03b6-217">從 Azure Resource Manager 範本建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="d03b6-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
