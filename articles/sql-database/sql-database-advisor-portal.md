---
title: "套用效能建議 - Azure SQL Database |Microsoft Docs"
description: "您可以使用 Azure 入口網站，找出可最佳化 Azure SQL Database 的效能建議，或修正在工作負載中找到的一些問題。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 018afaa8b08bd001e55693390e80c8e2c4f33a30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="2afb1-103">尋找和套用效能建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="2afb1-104">您可以使用 Azure 入口網站，找出可最佳化 Azure SQL Database 的效能建議，或修正在工作負載中找到的一些問題。</span><span class="sxs-lookup"><span data-stu-id="2afb1-104">You can use the Azure portal to find performance recommendations that can optimize performance of your Azure SQL Database or to correct some issue identified in your workload.</span></span> <span data-ttu-id="2afb1-105">您可以在 Azure 入口網站中的 [效能建議] 頁面找到根據潛在影響所提出排名最前面的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-105">**Performance recommendation** page in Azure portal enables you to find the top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="2afb1-106">檢視建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-106">Viewing recommendations</span></span>

<span data-ttu-id="2afb1-107">若要檢視和套用效能建議，您在 Azure 中必須有正確的[角色型存取控制](../active-directory/role-based-access-control-what-is.md)權限。</span><span class="sxs-lookup"><span data-stu-id="2afb1-107">To view and apply performance recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="2afb1-108">需要**讀取者**、**SQL DB 參與者**權限，才能檢視建議，以及需要**擁有者**、**SQL DB 參與者**權限，才能執行任何動作；建立或卸除索引並取消建立索引。</span><span class="sxs-lookup"><span data-stu-id="2afb1-108">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="2afb1-109">使用下列步驟在 Azure 入口網站上尋找效能建議：</span><span class="sxs-lookup"><span data-stu-id="2afb1-109">Use the following steps to find performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="2afb1-110">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2afb1-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2afb1-111">移至 [更多服務] > [SQL Database]，然後選取您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2afb1-111">Go to **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="2afb1-112">瀏覽至 [效能建議] 來檢視適用於所選資料庫的可用建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-112">Navigate to **Performance recommendation** to view available recommendations for the selected database.</span></span>

<span data-ttu-id="2afb1-113">資料表中顯示的效能建議類似於下圖：</span><span class="sxs-lookup"><span data-stu-id="2afb1-113">Performance recommendations are shonw in the table similar to the one shown on the following figure:</span></span>

![建議](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="2afb1-115">依照可能帶來的效能影響排序，建議分成下列類別：</span><span class="sxs-lookup"><span data-stu-id="2afb1-115">Recommendations are sorted by their potential impact on performance into the following categories:</span></span>

| <span data-ttu-id="2afb1-116">影響</span><span class="sxs-lookup"><span data-stu-id="2afb1-116">Impact</span></span> | <span data-ttu-id="2afb1-117">說明</span><span class="sxs-lookup"><span data-stu-id="2afb1-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2afb1-118">高</span><span class="sxs-lookup"><span data-stu-id="2afb1-118">High</span></span> |<span data-ttu-id="2afb1-119">高影響建議提供最明顯的效能影響。</span><span class="sxs-lookup"><span data-stu-id="2afb1-119">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="2afb1-120">中型</span><span class="sxs-lookup"><span data-stu-id="2afb1-120">Medium</span></span> |<span data-ttu-id="2afb1-121">中度影響建議會改善效能，但不顯著。</span><span class="sxs-lookup"><span data-stu-id="2afb1-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="2afb1-122">低</span><span class="sxs-lookup"><span data-stu-id="2afb1-122">Low</span></span> |<span data-ttu-id="2afb1-123">低影響建議比沒有建議時提供更好的效能，但改善可能不顯著。</span><span class="sxs-lookup"><span data-stu-id="2afb1-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="2afb1-124">Azure SQL Database 必須至少監視活動一整天，才能找出一些建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-124">Azure SQL Database needs to monitor activities at least for a day in order to identify some recommendations.</span></span> <span data-ttu-id="2afb1-125">相較於隨機蹦出的零星活動，一致的查詢模式更有利於 Azure SQL Database 最佳化。</span><span class="sxs-lookup"><span data-stu-id="2afb1-125">The Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="2afb1-126">如果 [效能建議]  頁面中目前沒有可用的建議，該頁面會提供訊息說明原因。</span><span class="sxs-lookup"><span data-stu-id="2afb1-126">If recommendations are not corrently available, the **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="2afb1-127">您也可以檢視歷程記錄作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="2afb1-127">You can also view the status of the historical operations.</span></span> <span data-ttu-id="2afb1-128">選取建議或狀態來查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2afb1-128">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="2afb1-129">以下是 Azure 入口網站中「建立索引」建議的範例。</span><span class="sxs-lookup"><span data-stu-id="2afb1-129">Here is an example of "Create index" recommendation in the Azure portal.</span></span>

![建立索引](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="2afb1-131">套用建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-131">Applying recommendations</span></span>
<span data-ttu-id="2afb1-132">Azure SQL Database 可讓您使用下列 3 個選項的其中任一選項來控制建議的啟用方式：</span><span class="sxs-lookup"><span data-stu-id="2afb1-132">Azure SQL Database gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="2afb1-133">一次套用一個個別的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="2afb1-134">啟用自動調整功能，以自動套用建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-134">Enable the Automatic tuning to automatically apply recommendations.</span></span>
* <span data-ttu-id="2afb1-135">若要手動實作建議，請針對您的資料庫執行建議的 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2afb1-135">To implement a recommendation manually, run the recommended T-SQL script against your database.</span></span>

<span data-ttu-id="2afb1-136">選取任何建議來檢視其詳細資料，然後按一下 [檢視指令碼]  來檢閱將如何建立建議的確切詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2afb1-136">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="2afb1-137">套用建議時，資料庫仍保持連線 -- 使用效能建議或自動調整功能不會使資料庫離線。</span><span class="sxs-lookup"><span data-stu-id="2afb1-137">The database remains online while the recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="2afb1-138">套用個別的建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-138">Apply an individual recommendation</span></span>
<span data-ttu-id="2afb1-139">您可以一次檢閱並接受一個建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="2afb1-140">選取 [建議] 刀鋒視窗上的某個建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-140">On the **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="2afb1-141">在 [詳細資料] 刀鋒視窗上按一下 [套用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2afb1-141">On the **Details** blade click **Apply** button.</span></span>
   
    ![套用建議](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="2afb1-143">針對資料庫套用選取的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-143">Selected recommendation will be applied on the database.</span></span>

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="2afb1-144">從清單中移除建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-144">Removing recommendations from the list</span></span>
<span data-ttu-id="2afb1-145">如果建議的清單中包含您想從清單中移除的項目，您可以捨棄該建議：</span><span class="sxs-lookup"><span data-stu-id="2afb1-145">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="2afb1-146">在 [建議] 清單中選取建議，以開啟詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2afb1-146">Select a recommendation in the list of **Recommendations** to open the details.</span></span>
2. <span data-ttu-id="2afb1-147">在 [詳細資料] 刀鋒視窗上按一下 [捨棄]。</span><span class="sxs-lookup"><span data-stu-id="2afb1-147">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="2afb1-148">如有需要，您可以將捨棄的項目加回到 **建議** 清單：</span><span class="sxs-lookup"><span data-stu-id="2afb1-148">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="2afb1-149">在 [建議] 刀鋒視窗上按一下 [檢視已捨棄]。</span><span class="sxs-lookup"><span data-stu-id="2afb1-149">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="2afb1-150">從清單中選取捨棄的項目以檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2afb1-150">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="2afb1-151">(選擇性) 按一下 [復原捨棄]，將索引加回到**建議**的主要清單。</span><span class="sxs-lookup"><span data-stu-id="2afb1-151">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="2afb1-152">啟用自動微調</span><span class="sxs-lookup"><span data-stu-id="2afb1-152">Enable automatic tuning</span></span>
<span data-ttu-id="2afb1-153">您可以將 Azure SQL Database 設為自動實作建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-153">You can set the Azure SQL Database to implement recommendations automatically.</span></span> <span data-ttu-id="2afb1-154">當建議可供使用時將會自動套用。</span><span class="sxs-lookup"><span data-stu-id="2afb1-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="2afb1-155">因為所有建議都由服務管理，所以若對效能產生負面影響，就會還原該建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-155">As with all recommendations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="2afb1-156">在 [建議] 刀鋒視窗上按一下 [自動化]：</span><span class="sxs-lookup"><span data-stu-id="2afb1-156">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![建議程式設定](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="2afb1-158">選取要自動執行的動作：</span><span class="sxs-lookup"><span data-stu-id="2afb1-158">Select actions to automate:</span></span>
   
    ![建議的索引](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="2afb1-160">手動執行建議的 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="2afb1-160">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="2afb1-161">選取任何建議，然後按一下 [檢視指令碼] 。</span><span class="sxs-lookup"><span data-stu-id="2afb1-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="2afb1-162">對資料庫執行這個指令碼，以手動套用建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-162">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="2afb1-163"> ，因此建議您在建立這些索引之後監視索引，以確認它們能夠提高效能，且於必要時調整或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="2afb1-163">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="2afb1-164">如需有關建立索引的詳細資訊，請參閱 [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2afb1-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="2afb1-165">取消建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-165">Canceling recommendations</span></span>
<span data-ttu-id="2afb1-166">可以取消處於**擱置中**、**確認中**或**成功**狀態的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="2afb1-167">狀態為 **執行中** 的建議無法取消。</span><span class="sxs-lookup"><span data-stu-id="2afb1-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="2afb1-168">在 [調整歷程記錄] 區域中選取建議，以開啟 [建議詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2afb1-168">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="2afb1-169">按一下 [取消]  以中止套用建議的程序。</span><span class="sxs-lookup"><span data-stu-id="2afb1-169">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="2afb1-170">監視作業</span><span class="sxs-lookup"><span data-stu-id="2afb1-170">Monitoring operations</span></span>
<span data-ttu-id="2afb1-171">套用建議時可能不會立即執行。</span><span class="sxs-lookup"><span data-stu-id="2afb1-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="2afb1-172">入口網站會提供有關建議狀態的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2afb1-172">The portal provides details regarding the status of recommendation.</span></span> <span data-ttu-id="2afb1-173">索引有下列可能的狀態：</span><span class="sxs-lookup"><span data-stu-id="2afb1-173">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="2afb1-174">狀態</span><span class="sxs-lookup"><span data-stu-id="2afb1-174">Status</span></span> | <span data-ttu-id="2afb1-175">說明</span><span class="sxs-lookup"><span data-stu-id="2afb1-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2afb1-176">Pending</span><span class="sxs-lookup"><span data-stu-id="2afb1-176">Pending</span></span> |<span data-ttu-id="2afb1-177">已收到套用建議命令，且已排程執行。</span><span class="sxs-lookup"><span data-stu-id="2afb1-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="2afb1-178">執行中</span><span class="sxs-lookup"><span data-stu-id="2afb1-178">Executing</span></span> |<span data-ttu-id="2afb1-179">正在套用建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-179">The recommendation is being applied.</span></span> |
| <span data-ttu-id="2afb1-180">驗證中</span><span class="sxs-lookup"><span data-stu-id="2afb1-180">Verifying</span></span> |<span data-ttu-id="2afb1-181">成功套用建議，而服務正在衡量益處。</span><span class="sxs-lookup"><span data-stu-id="2afb1-181">Recommendation was successfully applied and the service is measuring the benefits.</span></span> |
| <span data-ttu-id="2afb1-182">成功</span><span class="sxs-lookup"><span data-stu-id="2afb1-182">Success</span></span> |<span data-ttu-id="2afb1-183">已成功套用建議，並證實有益處。</span><span class="sxs-lookup"><span data-stu-id="2afb1-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="2afb1-184">錯誤</span><span class="sxs-lookup"><span data-stu-id="2afb1-184">Error</span></span> |<span data-ttu-id="2afb1-185">套用建議程序期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2afb1-185">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="2afb1-186">這可能是暫時性問題，也可能是資料表的結構描述變更，造成指令碼不再有效。</span><span class="sxs-lookup"><span data-stu-id="2afb1-186">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="2afb1-187">還原</span><span class="sxs-lookup"><span data-stu-id="2afb1-187">Reverting</span></span> |<span data-ttu-id="2afb1-188">已套用建立但被認為無助於效能，正在自動還原。</span><span class="sxs-lookup"><span data-stu-id="2afb1-188">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="2afb1-189">已還原</span><span class="sxs-lookup"><span data-stu-id="2afb1-189">Reverted</span></span> |<span data-ttu-id="2afb1-190">已還原建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-190">The recommendation was reverted.</span></span> |

<span data-ttu-id="2afb1-191">按一下清單中正在處理的建議以查看其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="2afb1-191">Click an in-process recommendation from the list to see more details:</span></span>

![建議的索引](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="2afb1-193">還原建議</span><span class="sxs-lookup"><span data-stu-id="2afb1-193">Reverting a recommendation</span></span>
<span data-ttu-id="2afb1-194">如果您使用效能建議來套用建議 (表示您未手動執行 T-SQL 指令碼)，如果建議程式發現會對效能造成負面影響，它將會自動還原建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-194">If you used the performance recommendations to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="2afb1-195">如果您因為任何原因想要還原建議，您可以執行以下步驟：</span><span class="sxs-lookup"><span data-stu-id="2afb1-195">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="2afb1-196">在 [調整歷程記錄]  區域中選取已成功套用的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-196">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="2afb1-197">在 [建議詳細資料] 刀鋒視窗上按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="2afb1-197">Click **Revert** on the **recommendation details** blade.</span></span>

![建議的索引](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="2afb1-199">監視索引建議的效能影響</span><span class="sxs-lookup"><span data-stu-id="2afb1-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="2afb1-200">成功實作建議之後 (目前僅提供索引作業和參數化查詢建議)，您可以按一下 [建議詳細資料] 刀鋒視窗上的 [Query Insights]  來開啟 [ [查詢效能深入解析](sql-database-query-performance.md) ]，並查看排名最前面查詢對效能的影響。</span><span class="sxs-lookup"><span data-stu-id="2afb1-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![監視效能影響](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="2afb1-202">摘要</span><span class="sxs-lookup"><span data-stu-id="2afb1-202">Summary</span></span>
<span data-ttu-id="2afb1-203">Azure SQL Database 會提供可改善 SQL Database 效能的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="2afb1-204">藉由提供 T-SQL 指令碼，以及獨立且全自動的，您會獲得最佳化資料庫的實用協助，並最終改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="2afb1-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2afb1-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2afb1-205">Next steps</span></span>
<span data-ttu-id="2afb1-206">監視建議，並繼續套用建議以改善效能。</span><span class="sxs-lookup"><span data-stu-id="2afb1-206">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="2afb1-207">資料庫工作負載會動態地持續變更。</span><span class="sxs-lookup"><span data-stu-id="2afb1-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="2afb1-208">Azure SQL Database 會繼續監視並提供可能改善資料庫效能的建議。</span><span class="sxs-lookup"><span data-stu-id="2afb1-208">Azure SQL Database will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="2afb1-209">若要深入了解 Azure SQL Database 中的自動調整功能，請參閱[自動調整](sql-database-automatic-tuning.md)。</span><span class="sxs-lookup"><span data-stu-id="2afb1-209">See [Automatic tuning](sql-database-automatic-tuning.md) to learn more about the automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="2afb1-210">如需 Azure SQL Database 效能建議的概觀，請參閱[效能建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="2afb1-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="2afb1-211">請參閱[查詢效能深入解析](sql-database-query-performance.md)，以了解如何檢視排名最前面查詢的效能影響。</span><span class="sxs-lookup"><span data-stu-id="2afb1-211">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2afb1-212">其他資源</span><span class="sxs-lookup"><span data-stu-id="2afb1-212">Additional resources</span></span>
* [<span data-ttu-id="2afb1-213">查詢存放區</span><span class="sxs-lookup"><span data-stu-id="2afb1-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="2afb1-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="2afb1-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="2afb1-215">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="2afb1-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

