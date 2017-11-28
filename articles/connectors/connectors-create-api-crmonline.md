---
title: "從 Azure 邏輯應用程式的 aaaConnect tooDynamics 365 （線上） |Microsoft 文件"
description: "建立邏輯管理 Dynamics 365 （線上） 的實體，透過 hello hello Dynamics 365 連接器所提供的 API 的應用程式工作流程"
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
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="a85d7-103">邏輯應用程式工作流程從連接 tooDynamics 365</span><span class="sxs-lookup"><span data-stu-id="a85d7-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="a85d7-104">透過邏輯應用程式，您可以連接 tooDynamics 365 （線上），並建立實用的商務流程，建立記錄、 更新項目，或傳回的記錄清單。</span><span class="sxs-lookup"><span data-stu-id="a85d7-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="a85d7-105">與 hello Dynamics 365 連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="a85d7-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="a85d7-106">建置您的商務流程根據 hello 資料取自 Dynamics 365 （線上）。</span><span class="sxs-lookup"><span data-stu-id="a85d7-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="a85d7-107">使用取得回應，然後進行 hello 輸出適用於其他動作的動作。</span><span class="sxs-lookup"><span data-stu-id="a85d7-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="a85d7-108">舉例來說，當 Dynamics 365 (線上) 中有項目更新時，您可以利用 Office 365 來傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a85d7-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="a85d7-109">本主題說明您如何 toocreate 邏輯應用程式的工作中建立 Dynamics 365 Dynamics 365 在每次建立新的負責人時。</span><span class="sxs-lookup"><span data-stu-id="a85d7-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a85d7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a85d7-110">Prerequisites</span></span>
* <span data-ttu-id="a85d7-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a85d7-111">An Azure account.</span></span>
* <span data-ttu-id="a85d7-112">Dynamics 365 (線上) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a85d7-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="a85d7-113">每次在 Dynamics 365 中建立了新的潛在客戶時便建立工作</span><span class="sxs-lookup"><span data-stu-id="a85d7-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="a85d7-114">[登入 tooAzure](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="a85d7-115">在 hello Azure 搜尋方塊中，輸入`Logic apps`，然後按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="a85d7-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![尋找Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="a85d7-117">在 [邏輯應用程式] 下，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp 新增](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="a85d7-119">toocreate hello 邏輯應用程式，完成 hello**名稱**，**訂用帳戶**，**資源群組**，和**位置**欄位，然後再按一下  **建立**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="a85d7-120">選取 hello 新邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a85d7-120">Select hello new logic app.</span></span> <span data-ttu-id="a85d7-121">當您收到 hello**部署成功**通知，請按一下**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="a85d7-122">在 [開發工具] 下，按一下 [邏輯應用程式設計工具]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="a85d7-123">在 hello 範本清單中，按一下 **空白邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="a85d7-124">在 [hello] 搜尋方塊中，輸入`Dynamics 365`。</span><span class="sxs-lookup"><span data-stu-id="a85d7-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a85d7-125">從 hello Dynamics 365 觸發程序清單中，選取**Dynamics 365 – 時建立的記錄**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="a85d7-126">如果您是在 tooDynamics 365 提示的 toosign，請立刻執行。</span><span class="sxs-lookup"><span data-stu-id="a85d7-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="a85d7-127">在 hello 觸發程序的詳細資訊，請輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="a85d7-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="a85d7-128">**組織名稱**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-128">**Organization Name**.</span></span> <span data-ttu-id="a85d7-129">選取您想要 hello 邏輯應用程式 toolisten hello Dynamics 365 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a85d7-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="a85d7-130">**實體名稱**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-130">**Entity Name**.</span></span> <span data-ttu-id="a85d7-131">選取您想要 toolisten hello 實體。</span><span class="sxs-lookup"><span data-stu-id="a85d7-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="a85d7-132">此事件會做為觸發程序 toostart hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a85d7-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="a85d7-133">在本逐步解說中，我們選取 [潛在客戶]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="a85d7-134">**頻率想 toocheck 項目？**</span><span class="sxs-lookup"><span data-stu-id="a85d7-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="a85d7-135">這些值來設定頻率 hello 邏輯應用程式會檢查更新相關的 toohello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a85d7-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="a85d7-136">更新每隔三分鐘 toocheck hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="a85d7-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="a85d7-137">**頻率**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-137">**Frequency**.</span></span> <span data-ttu-id="a85d7-138">選取秒、分鐘、小時或天。</span><span class="sxs-lookup"><span data-stu-id="a85d7-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="a85d7-139">**間隔**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-139">**Interval**.</span></span> <span data-ttu-id="a85d7-140">輸入 hello 數秒、 分鐘、 小時或您想 toopass hello 下次檢查之前的天數。</span><span class="sxs-lookup"><span data-stu-id="a85d7-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![邏輯應用程式觸發程序的詳細資料](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="a85d7-142">按一下 新增步驟，然後按一下新增動作。</span><span class="sxs-lookup"><span data-stu-id="a85d7-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="a85d7-143">在 [hello] 搜尋方塊中，輸入`Dynamics 365`。</span><span class="sxs-lookup"><span data-stu-id="a85d7-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a85d7-144">從 hello 動作清單中，選取**Dynamics 365 – 建立新的記錄**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="a85d7-145">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="a85d7-145">Enter hello following information:</span></span>

    * <span data-ttu-id="a85d7-146">**組織名稱**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-146">**Organization Name**.</span></span> <span data-ttu-id="a85d7-147">選取您想要 hello 流程 toocreate hello 記錄 hello Dynamics 365 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a85d7-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="a85d7-148">請注意，這個執行個體並未 toobe hello 相同執行個體從觸發 hello 事件的位置。</span><span class="sxs-lookup"><span data-stu-id="a85d7-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="a85d7-149">**實體名稱**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-149">**Entity Name**.</span></span> <span data-ttu-id="a85d7-150">選取您想 toocreate 記錄 hello 事件觸發時 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="a85d7-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="a85d7-151">在本逐步解說中，我們選取 [工作]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="a85d7-152">按一下 hello**主旨**出現方塊。</span><span class="sxs-lookup"><span data-stu-id="a85d7-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="a85d7-153">從 hello 動態內容清單隨即出現，您可以選取這些欄位：</span><span class="sxs-lookup"><span data-stu-id="a85d7-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="a85d7-154">**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-154">**Last Name**.</span></span> <span data-ttu-id="a85d7-155">選取此欄位插入 hello 姓氏的 hello hello hello 工作的主旨欄位時，會建立 hello 工作記錄。</span><span class="sxs-lookup"><span data-stu-id="a85d7-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="a85d7-156">**主題**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-156">**Topic**.</span></span> <span data-ttu-id="a85d7-157">選取 hello 負責人 hello hello 工作的主旨欄位至這個欄位插入 hello 主題欄位，當 hello 工作會建立記錄。</span><span class="sxs-lookup"><span data-stu-id="a85d7-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="a85d7-158">按一下**主題**tooadd 該 toohello**主旨**方塊。</span><span class="sxs-lookup"><span data-stu-id="a85d7-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![邏輯應用程式建立新記錄詳細資料](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="a85d7-160">Hello 邏輯應用程式的設計工具工具列上，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="a85d7-162">toostart hello 邏輯應用程式中，按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-162">toostart hello Logic App, click **Run**.</span></span>

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="a85d7-164">現在，在 Dynamics 365 中建立銷售潛在客戶記錄，然後看看流程的運作！</span><span class="sxs-lookup"><span data-stu-id="a85d7-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="a85d7-165">為邏輯應用程式步驟設定進階選項</span><span class="sxs-lookup"><span data-stu-id="a85d7-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="a85d7-166">如何 toofilter 資料在邏輯應用程式步驟中，按一下的 toospecify **Show advanced 選項**在該步驟，然後加入篩選或順序查詢。</span><span class="sxs-lookup"><span data-stu-id="a85d7-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="a85d7-167">例如，您可以使用篩選器查詢 tooget 唯一作用中帳戶，並依 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a85d7-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="a85d7-168">tooperform 這項工作，輸入 hello OData 篩選器查詢`statuscode eq 1`，然後選取**帳戶名稱**從 hello 動態內容的清單。</span><span class="sxs-lookup"><span data-stu-id="a85d7-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="a85d7-169">詳細資訊︰[MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 和 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![邏輯應用程式進階選項](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="a85d7-171">使用進階選項時的最佳作法</span><span class="sxs-lookup"><span data-stu-id="a85d7-171">Best practices when using advanced options</span></span>

<span data-ttu-id="a85d7-172">當您將值 tooa 欄位時，您必須符合 hello 欄位類型，當您輸入的值，或從 hello 動態內容清單中選取值。</span><span class="sxs-lookup"><span data-stu-id="a85d7-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="a85d7-173">欄位類型</span><span class="sxs-lookup"><span data-stu-id="a85d7-173">Field type</span></span>  |<span data-ttu-id="a85d7-174">如何 toouse</span><span class="sxs-lookup"><span data-stu-id="a85d7-174">How toouse</span></span>  |<span data-ttu-id="a85d7-175">其中 toofind</span><span class="sxs-lookup"><span data-stu-id="a85d7-175">Where toofind</span></span>  |<span data-ttu-id="a85d7-176">名稱</span><span class="sxs-lookup"><span data-stu-id="a85d7-176">Name</span></span>  |<span data-ttu-id="a85d7-177">資料類型</span><span class="sxs-lookup"><span data-stu-id="a85d7-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="a85d7-178">文字欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-178">Text fields</span></span>|<span data-ttu-id="a85d7-179">文字欄位需要單行文字或屬於文字類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="a85d7-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="a85d7-180">範例包括 hello 類別和子類別目錄欄位。</span><span class="sxs-lookup"><span data-stu-id="a85d7-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="a85d7-181">設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a85d7-182">category</span><span class="sxs-lookup"><span data-stu-id="a85d7-182">category</span></span> |<span data-ttu-id="a85d7-183">單行文字</span><span class="sxs-lookup"><span data-stu-id="a85d7-183">Single Line of Text</span></span>        
<span data-ttu-id="a85d7-184">整數欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-184">Integer fields</span></span> | <span data-ttu-id="a85d7-185">某些欄位需要整數或屬於整數類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="a85d7-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="a85d7-186">範例包括 [完成百分比] 和 [持續時間]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="a85d7-187">設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a85d7-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="a85d7-188">percentcomplete</span></span> |<span data-ttu-id="a85d7-189">整數</span><span class="sxs-lookup"><span data-stu-id="a85d7-189">Whole Number</span></span>         
<span data-ttu-id="a85d7-190">日期欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-190">Date fields</span></span> | <span data-ttu-id="a85d7-191">某些欄位需要以 mm/dd/yyyy 格式輸入的日期或屬於日期類型欄位的動態內容。</span><span class="sxs-lookup"><span data-stu-id="a85d7-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="a85d7-192">範例包括 [建立日期]、[開始日期]、[實際開始時間]、[上次保留時間]、[實際結束時間] 和 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="a85d7-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="a85d7-193">設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="a85d7-194">createdon</span><span class="sxs-lookup"><span data-stu-id="a85d7-194">createdon</span></span> |<span data-ttu-id="a85d7-195">日期和時間</span><span class="sxs-lookup"><span data-stu-id="a85d7-195">Date and Time</span></span>
<span data-ttu-id="a85d7-196">同時需要記錄識別碼和查閱類型的欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="a85d7-197">參考另一個實體記錄某些欄位需要 hello 記錄識別碼和 hello 查閱類型。</span><span class="sxs-lookup"><span data-stu-id="a85d7-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="a85d7-198">設定 > 自訂 > 自訂 hello 系統 > 實體 > 帳戶 > 欄位</span><span class="sxs-lookup"><span data-stu-id="a85d7-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="a85d7-199">accountid</span><span class="sxs-lookup"><span data-stu-id="a85d7-199">accountid</span></span>  | <span data-ttu-id="a85d7-200">主索引鍵</span><span class="sxs-lookup"><span data-stu-id="a85d7-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="a85d7-201">同時需要記錄識別碼和查閱類型的其他欄位範例</span><span class="sxs-lookup"><span data-stu-id="a85d7-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="a85d7-202">展開 hello 前一個資料表上，以下是不處理 hello 動態內容清單中選取值的欄位的其他範例。</span><span class="sxs-lookup"><span data-stu-id="a85d7-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="a85d7-203">相反地，這些欄位需要這兩個的記錄識別碼和查閱型別中 PowerApps hello 欄位中輸入。</span><span class="sxs-lookup"><span data-stu-id="a85d7-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="a85d7-204">擁有者和擁有者類型。</span><span class="sxs-lookup"><span data-stu-id="a85d7-204">Owner and Owner Type.</span></span> <span data-ttu-id="a85d7-205">hello 擁有者 欄位必須是有效的使用者或小組記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="a85d7-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="a85d7-206">hello 擁有者型別必須是**systemusers**或**小組**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="a85d7-207">客戶和客戶類型。</span><span class="sxs-lookup"><span data-stu-id="a85d7-207">Customer and Customer Type.</span></span> <span data-ttu-id="a85d7-208">hello 客戶欄位必須是有效的帳戶，或連絡記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="a85d7-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="a85d7-209">hello 擁有者型別必須是**帳戶**或**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="a85d7-210">關於和關於類型。</span><span class="sxs-lookup"><span data-stu-id="a85d7-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="a85d7-211">hello 相關欄位必須是有效的記錄識別碼，例如帳戶或連絡記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="a85d7-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="a85d7-212">hello 有關類型必須是 hello 查閱類型 hello 記錄，例如**帳戶**或**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="a85d7-213">hello 下列工作建立動作範例會將對應將它加入有關 hello 工作的欄位 toohello toohello 記錄識別碼的帳戶記錄。</span><span class="sxs-lookup"><span data-stu-id="a85d7-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="a85d7-215">此範例也會將指派的 hello 工作 tooa 特定使用者根據 hello 使用者的記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="a85d7-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="a85d7-217">toofind 一筆記錄的識別碼，請參閱下列章節的 hello:*尋找 hello 記錄識別碼*</span><span class="sxs-lookup"><span data-stu-id="a85d7-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="a85d7-218">尋找 hello 記錄識別碼</span><span class="sxs-lookup"><span data-stu-id="a85d7-218">Find hello record ID</span></span>

1. <span data-ttu-id="a85d7-219">開啟記錄，例如帳戶記錄。</span><span class="sxs-lookup"><span data-stu-id="a85d7-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="a85d7-220">Hello 動作在工具列上，按一下 **快顯**![彈出記錄](./media/connectors-create-api-crmonline/popout-record.png)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="a85d7-221">或者，hello 動作 toocopy hello 完整的 URL 到預設電子郵件程式中，按一下工具列**電子郵件 連結**。</span><span class="sxs-lookup"><span data-stu-id="a85d7-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="a85d7-222">hello %7b 和 %7 d hello URL 的字元編碼之間不會顯示 hello 記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="a85d7-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="a85d7-224">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a85d7-224">Troubleshooting</span></span>
<span data-ttu-id="a85d7-225">tootroubleshoot 失敗的步驟，在邏輯應用程式中檢視的 hello 事件 hello 狀態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a85d7-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="a85d7-226">在 Logic Apps 下，選取您的邏輯應用程式，然後按一下概觀。</span><span class="sxs-lookup"><span data-stu-id="a85d7-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="a85d7-227">hello 摘要區域中顯示，並提供 hello 邏輯應用程式中的 hello 執行狀態。</span><span class="sxs-lookup"><span data-stu-id="a85d7-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![邏輯應用程式執行狀態](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="a85d7-229">tooview 執行任何失敗的詳細資訊按一下 hello 失敗事件。</span><span class="sxs-lookup"><span data-stu-id="a85d7-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="a85d7-230">tooexpand 失敗的步驟中，按一下該步驟。</span><span class="sxs-lookup"><span data-stu-id="a85d7-230">tooexpand a failed step, click that step.</span></span>

   ![展開失敗的步驟](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="a85d7-232">hello 步驟詳細資料會出現，並可協助您疑難排解 hello hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="a85d7-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![失敗步驟的詳細資料](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="a85d7-234">如需針對邏輯應用程式進行疑難排解的詳細資訊，請參閱[診斷邏輯應用程式失敗](../logic-apps/logic-apps-diagnosing-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="a85d7-235">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="a85d7-235">Connector-specific details</span></span>

<span data-ttu-id="a85d7-236">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/crm/)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a85d7-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a85d7-237">Next steps</span></span>
<span data-ttu-id="a85d7-238">瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="a85d7-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
