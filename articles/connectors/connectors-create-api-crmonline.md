---
title: "從 Azure Logic Apps 連線至 Dynamics 365 (線上) | Microsoft Docs"
description: "建立邏輯應用程式工作流程，以透過 Dynamics 365 連接器提供的 API 管理 Dynamics 365 (線上) 實體"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="3fe68-103">從邏輯應用程式邏輯應用程式連線至 Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="3fe68-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="3fe68-104">使用 Logic Apps，您可以連線至 Dynamics 365 (線上)，並建立實用的商務流程以建立記錄、更新項目或傳回記錄清單。</span><span class="sxs-lookup"><span data-stu-id="3fe68-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="3fe68-105">使用 Dynamics 365 連接器，您可以︰</span><span class="sxs-lookup"><span data-stu-id="3fe68-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="3fe68-106">根據您從 Dynamics 365 (線上) 所取得的資料，來建置您的商務流程。</span><span class="sxs-lookup"><span data-stu-id="3fe68-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="3fe68-107">使用可取得回應的動作，然後提供輸出讓其他動作使用。</span><span class="sxs-lookup"><span data-stu-id="3fe68-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="3fe68-108">舉例來說，當 Dynamics 365 (線上) 中有項目更新時，您可以利用 Office 365 來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="3fe68-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="3fe68-109">本主題說明如何建立邏輯應用程式，以在每次 Dynamics 365 中建立了新的潛在客戶時，便在 Dynamics 365 建立工作。</span><span class="sxs-lookup"><span data-stu-id="3fe68-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fe68-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fe68-110">Prerequisites</span></span>
* <span data-ttu-id="3fe68-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fe68-111">An Azure account.</span></span>
* <span data-ttu-id="3fe68-112">Dynamics 365 (線上) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fe68-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="3fe68-113">每次在 Dynamics 365 中建立了新的潛在客戶時便建立工作</span><span class="sxs-lookup"><span data-stu-id="3fe68-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="3fe68-114">[登入 Azure](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3fe68-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="3fe68-115">在 Azure 搜尋服務方塊中，輸入 `Logic apps` 並按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="3fe68-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![尋找Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="3fe68-117">在 [邏輯應用程式] 下，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp 新增](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="3fe68-119">要建立邏輯應用程式，請完成 [名稱]、[訂用帳戶]、[資源群組] 和 [位置] 欄位，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="3fe68-120">選取新的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fe68-120">Select the new logic app.</span></span> <span data-ttu-id="3fe68-121">當您收到 [部署成功] 通知時，按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="3fe68-122">在 [開發工具] 下，按一下 [邏輯應用程式設計工具]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="3fe68-123">在範本清單中，按一下 [將邏輯應用程式留白]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="3fe68-124">在搜尋方塊中，輸入 `Dynamics 365`。</span><span class="sxs-lookup"><span data-stu-id="3fe68-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="3fe68-125">從 Dynamics 365 觸發程序清單中，選取 [Dynamics 365 – 建立記錄時]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="3fe68-126">如果系統提示您登入 Dynamics 365，請立即登入。</span><span class="sxs-lookup"><span data-stu-id="3fe68-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="3fe68-127">在觸發程序詳細資料中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3fe68-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="3fe68-128">**組織名稱**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-128">**Organization Name**.</span></span> <span data-ttu-id="3fe68-129">選取要讓邏輯應用程式接聽的 Dynamics 365 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fe68-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="3fe68-130">**實體名稱**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-130">**Entity Name**.</span></span> <span data-ttu-id="3fe68-131">選取您希望接聽的實體。</span><span class="sxs-lookup"><span data-stu-id="3fe68-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="3fe68-132">系統會將此事件會當作觸發程序，以啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fe68-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="3fe68-133">在本逐步解說中，我們選取 [潛在客戶]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="3fe68-134">**多久要檢查一次項目？**</span><span class="sxs-lookup"><span data-stu-id="3fe68-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="3fe68-135">這些值會設定邏輯應用程式要多久檢查一次是否有觸發程序的相關更新。</span><span class="sxs-lookup"><span data-stu-id="3fe68-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="3fe68-136">預設設定是每三分鐘檢查是否有更新。</span><span class="sxs-lookup"><span data-stu-id="3fe68-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="3fe68-137">**頻率**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-137">**Frequency**.</span></span> <span data-ttu-id="3fe68-138">選取秒、分鐘、小時或天。</span><span class="sxs-lookup"><span data-stu-id="3fe68-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="3fe68-139">**間隔**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-139">**Interval**.</span></span> <span data-ttu-id="3fe68-140">輸入數字來表示在下一次檢查之前要經過的秒數、分鐘數、小時數、或天數。</span><span class="sxs-lookup"><span data-stu-id="3fe68-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![邏輯應用程式觸發程序的詳細資料](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="3fe68-142">按一下 [新增步驟]，然後按一下 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="3fe68-143">在搜尋方塊中，輸入 `Dynamics 365`。</span><span class="sxs-lookup"><span data-stu-id="3fe68-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="3fe68-144">從動作清單中，選取 [Dynamics 365 – 建立新記錄]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="3fe68-145">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="3fe68-145">Enter the following information:</span></span>

    * <span data-ttu-id="3fe68-146">**組織名稱**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-146">**Organization Name**.</span></span> <span data-ttu-id="3fe68-147">選取要讓流程在其中建立記錄的 Dynamics 365 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fe68-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="3fe68-148">請注意，此執行個體不一定要是與觸發事件相同的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fe68-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="3fe68-149">**實體名稱**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-149">**Entity Name**.</span></span> <span data-ttu-id="3fe68-150">選取要在觸發事件時建立記錄的實體。</span><span class="sxs-lookup"><span data-stu-id="3fe68-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="3fe68-151">在本逐步解說中，我們選取 [工作]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="3fe68-152">按一下出現的 [主旨] 方塊。</span><span class="sxs-lookup"><span data-stu-id="3fe68-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="3fe68-153">您可以從出現的動態內容清單中，選取其中一個欄位：</span><span class="sxs-lookup"><span data-stu-id="3fe68-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="3fe68-154">**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-154">**Last Name**.</span></span> <span data-ttu-id="3fe68-155">選取此欄位，便會在建立工作記錄時於工作的 [主旨] 欄位中插入潛在客戶的姓氏。</span><span class="sxs-lookup"><span data-stu-id="3fe68-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="3fe68-156">**主題**。</span><span class="sxs-lookup"><span data-stu-id="3fe68-156">**Topic**.</span></span> <span data-ttu-id="3fe68-157">選取此欄位，便會在建立工作記錄時於工作的 [主旨] 欄位中插入潛在客戶的 [主題] 欄位。</span><span class="sxs-lookup"><span data-stu-id="3fe68-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="3fe68-158">按一下 [主題]，即可將其新增至 [主旨] 方塊。</span><span class="sxs-lookup"><span data-stu-id="3fe68-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![邏輯應用程式建立新記錄詳細資料](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="3fe68-160">在邏輯應用程式設計工具的工具列上，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="3fe68-162">若要啟動邏輯應用程式，請按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-162">To start the Logic App, click **Run**.</span></span>

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="3fe68-164">現在，在 Dynamics 365 中建立銷售潛在客戶記錄，然後看看流程的運作！</span><span class="sxs-lookup"><span data-stu-id="3fe68-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="3fe68-165">為邏輯應用程式步驟設定進階選項</span><span class="sxs-lookup"><span data-stu-id="3fe68-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="3fe68-166">若要指定如何在邏輯應用程式步驟中篩選資料，請在該步驟中按一下 [顯示進階選項]，接著新增篩選條件或依查詢排序。</span><span class="sxs-lookup"><span data-stu-id="3fe68-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="3fe68-167">例如，您可以使用篩選條件查詢只取得作用中的帳戶，並依帳戶名稱排序。</span><span class="sxs-lookup"><span data-stu-id="3fe68-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="3fe68-168">若要這樣做，請輸入 OData 篩選條件查詢 `statuscode eq 1`，然後從動態內容清單中選取 [帳戶名稱]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="3fe68-169">詳細資訊︰[MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 和 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)。</span><span class="sxs-lookup"><span data-stu-id="3fe68-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![邏輯應用程式進階選項](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="3fe68-171">使用進階選項時的最佳作法</span><span class="sxs-lookup"><span data-stu-id="3fe68-171">Best practices when using advanced options</span></span>

<span data-ttu-id="3fe68-172">當您在欄位中新增值時，無論是輸入值或從動態內容清單中選取值，都必須符合欄位類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="3fe68-173">欄位類型</span><span class="sxs-lookup"><span data-stu-id="3fe68-173">Field type</span></span>  |<span data-ttu-id="3fe68-174">使用方式</span><span class="sxs-lookup"><span data-stu-id="3fe68-174">How to use</span></span>  |<span data-ttu-id="3fe68-175">所在位置</span><span class="sxs-lookup"><span data-stu-id="3fe68-175">Where to find</span></span>  |<span data-ttu-id="3fe68-176">名稱</span><span class="sxs-lookup"><span data-stu-id="3fe68-176">Name</span></span>  |<span data-ttu-id="3fe68-177">資料類型</span><span class="sxs-lookup"><span data-stu-id="3fe68-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="3fe68-178">文字欄位</span><span class="sxs-lookup"><span data-stu-id="3fe68-178">Text fields</span></span>|<span data-ttu-id="3fe68-179">文字欄位需要單行文字或屬於文字類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="3fe68-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="3fe68-180">範例包括 [類別] 和 [子類別] 欄位。</span><span class="sxs-lookup"><span data-stu-id="3fe68-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="3fe68-181">[設定] > [自訂] > [自訂系統] > [實體] > [工作] > [欄位]</span><span class="sxs-lookup"><span data-stu-id="3fe68-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="3fe68-182">category</span><span class="sxs-lookup"><span data-stu-id="3fe68-182">category</span></span> |<span data-ttu-id="3fe68-183">單行文字</span><span class="sxs-lookup"><span data-stu-id="3fe68-183">Single Line of Text</span></span>        
<span data-ttu-id="3fe68-184">整數欄位</span><span class="sxs-lookup"><span data-stu-id="3fe68-184">Integer fields</span></span> | <span data-ttu-id="3fe68-185">某些欄位需要整數或屬於整數類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="3fe68-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="3fe68-186">範例包括 [完成百分比] 和 [持續時間]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="3fe68-187">[設定] > [自訂] > [自訂系統] > [實體] > [工作] > [欄位]</span><span class="sxs-lookup"><span data-stu-id="3fe68-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="3fe68-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="3fe68-188">percentcomplete</span></span> |<span data-ttu-id="3fe68-189">整數</span><span class="sxs-lookup"><span data-stu-id="3fe68-189">Whole Number</span></span>         
<span data-ttu-id="3fe68-190">日期欄位</span><span class="sxs-lookup"><span data-stu-id="3fe68-190">Date fields</span></span> | <span data-ttu-id="3fe68-191">某些欄位需要以 mm/dd/yyyy 格式輸入的日期或屬於日期類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="3fe68-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="3fe68-192">範例包括 [建立日期]、[開始日期]、[實際開始時間]、[上次保留時間]、[實際結束時間] 和 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="3fe68-193">[設定] > [自訂] > [自訂系統] > [實體] > [工作] > [欄位]</span><span class="sxs-lookup"><span data-stu-id="3fe68-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="3fe68-194">createdon</span><span class="sxs-lookup"><span data-stu-id="3fe68-194">createdon</span></span> |<span data-ttu-id="3fe68-195">日期和時間</span><span class="sxs-lookup"><span data-stu-id="3fe68-195">Date and Time</span></span>
<span data-ttu-id="3fe68-196">同時需要記錄識別碼和查閱類型的欄位</span><span class="sxs-lookup"><span data-stu-id="3fe68-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="3fe68-197">某些參考另一個實體記錄的欄位同時需要記錄識別碼和查閱類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="3fe68-198">[設定] > [自訂] > [自訂系統] > [實體] > [帳戶] > [欄位]</span><span class="sxs-lookup"><span data-stu-id="3fe68-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="3fe68-199">accountid</span><span class="sxs-lookup"><span data-stu-id="3fe68-199">accountid</span></span>  | <span data-ttu-id="3fe68-200">主索引鍵</span><span class="sxs-lookup"><span data-stu-id="3fe68-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="3fe68-201">同時需要記錄識別碼和查閱類型的其他欄位範例</span><span class="sxs-lookup"><span data-stu-id="3fe68-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="3fe68-202">延續上表，這邊有更多無法與選自動態內容清單之值搭配運作的欄位範例。</span><span class="sxs-lookup"><span data-stu-id="3fe68-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="3fe68-203">相反地，這些欄位需要同時在 PowerApps 的欄位中輸入記錄識別碼和查閱類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="3fe68-204">擁有者和擁有者類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-204">Owner and Owner Type.</span></span> <span data-ttu-id="3fe68-205">[擁有者] 欄位必須是有效的使用者或小組記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fe68-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="3fe68-206">[擁有者類型] 必須是 [系統使用者] 或 [小組]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="3fe68-207">客戶和客戶類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-207">Customer and Customer Type.</span></span> <span data-ttu-id="3fe68-208">[客戶] 欄位必須是有效的帳戶或連絡人記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fe68-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="3fe68-209">[擁有者類型] 必須是 [帳戶] 或 [連絡人]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="3fe68-210">關於和關於類型。</span><span class="sxs-lookup"><span data-stu-id="3fe68-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="3fe68-211">[關於] 欄位必須是有效的記錄識別碼，例如帳戶或連絡人記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fe68-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="3fe68-212">[關於類型] 必須是記錄的查閱類型，例如 [帳戶] 或 [連絡人]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="3fe68-213">下列工作建立動作範例會新增帳戶記錄，其對應至會將其新增至工作之 [關於] 欄位的記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fe68-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="3fe68-215">此範例也會根據使用者的記錄識別碼，將工作指派給特定使用者。</span><span class="sxs-lookup"><span data-stu-id="3fe68-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="3fe68-217">若要尋找記錄的識別碼，請參閱下一節：＜尋找記錄識別碼＞</span><span class="sxs-lookup"><span data-stu-id="3fe68-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="3fe68-218">尋找記錄識別碼</span><span class="sxs-lookup"><span data-stu-id="3fe68-218">Find the record ID</span></span>

1. <span data-ttu-id="3fe68-219">開啟記錄，例如帳戶記錄。</span><span class="sxs-lookup"><span data-stu-id="3fe68-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="3fe68-220">在 [動作] 工具列上按一下 [彈出] ![彈出記錄](./media/connectors-create-api-crmonline/popout-record.png)。</span><span class="sxs-lookup"><span data-stu-id="3fe68-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="3fe68-221">或者，在 [動作] 工具列上按一下 [以電子郵件傳送連結]，將完整 URL 複製到預設電子郵件程式中。</span><span class="sxs-lookup"><span data-stu-id="3fe68-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="3fe68-222">記錄識別碼會顯示在 URL 的 %7b 和 %7d 編碼字元中間。</span><span class="sxs-lookup"><span data-stu-id="3fe68-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="3fe68-224">疑難排解</span><span class="sxs-lookup"><span data-stu-id="3fe68-224">Troubleshooting</span></span>
<span data-ttu-id="3fe68-225">若要針對邏輯應用程式中的失敗步驟進行疑難排解，請檢視事件的狀態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fe68-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="3fe68-226">在 [Logic Apps] 下，選取您的邏輯應用程式，然後按一下 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="3fe68-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="3fe68-227">隨即會顯示 [摘要] 區域，其中會提供邏輯應用程式的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="3fe68-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![邏輯應用程式執行狀態](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="3fe68-229">若要檢視任何失敗執行的詳細資訊，請按一下失敗的事件。</span><span class="sxs-lookup"><span data-stu-id="3fe68-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="3fe68-230">若要展開失敗的步驟，請按一下該步驟。</span><span class="sxs-lookup"><span data-stu-id="3fe68-230">To expand a failed step, click that step.</span></span>

   ![展開失敗的步驟](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="3fe68-232">隨即會顯示步驟的詳細資料，此資料可協助您針對失敗原因進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3fe68-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![失敗步驟的詳細資料](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="3fe68-234">如需針對邏輯應用程式進行疑難排解的詳細資訊，請參閱[診斷邏輯應用程式失敗](../logic-apps/logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe68-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3fe68-235">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3fe68-235">Connector-specific details</span></span>

<span data-ttu-id="3fe68-236">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/crm/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="3fe68-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3fe68-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fe68-237">Next steps</span></span>
<span data-ttu-id="3fe68-238">請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="3fe68-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
