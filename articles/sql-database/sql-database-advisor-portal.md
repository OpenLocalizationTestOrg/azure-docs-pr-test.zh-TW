---
title: "aaaApply 效能建議 Azure SQL Database |Microsoft 文件"
description: "您可以使用 hello Azure 入口網站 toofind 效能建議可以將您的 Azure SQL Database 或 toocorrect 的效能最佳化，您的工作負載中所識別的一些問題。"
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
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="0f144-103">尋找和套用效能建議</span><span class="sxs-lookup"><span data-stu-id="0f144-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="0f144-104">您可以使用 hello Azure 入口網站 toofind 效能建議可以將您的 Azure SQL Database 或 toocorrect 的效能最佳化，您的工作負載中所識別的一些問題。</span><span class="sxs-lookup"><span data-stu-id="0f144-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="0f144-105">**效能建議**Azure 入口網站中的頁面可讓您根據其潛在影響 toofind hello 熱門建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="0f144-106">檢視建議</span><span class="sxs-lookup"><span data-stu-id="0f144-106">Viewing recommendations</span></span>

<span data-ttu-id="0f144-107">tooview 並套用效能的建議，您需要 hello 正確[角色型存取控制](../active-directory/role-based-access-control-what-is.md)在 Azure 中的權限。</span><span class="sxs-lookup"><span data-stu-id="0f144-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="0f144-108">**讀取器**， **SQL DB 參與者**權限是必要的 tooview 建議，和**擁有者**， **SQL DB 參與者**不需要權限tooexecute 任何動作;建立或卸除索引並取消索引建立。</span><span class="sxs-lookup"><span data-stu-id="0f144-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="0f144-109">使用 Azure 入口網站上遵循步驟 toofind 效能建議事項的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f144-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="0f144-110">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0f144-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0f144-111">跳過**更多服務** > **SQL 資料庫**，然後選取您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f144-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="0f144-112">瀏覽過**效能建議**tooview hello 選取的資料庫可用的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="0f144-113">效能建議為 shonw hello 資料表類似 toohello hello 遵循圖上顯示的其中一個：</span><span class="sxs-lookup"><span data-stu-id="0f144-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![建議](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="0f144-115">建議會依照其對成下列類別目錄的 hello 效能的潛在影響：</span><span class="sxs-lookup"><span data-stu-id="0f144-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="0f144-116">影響</span><span class="sxs-lookup"><span data-stu-id="0f144-116">Impact</span></span> | <span data-ttu-id="0f144-117">說明</span><span class="sxs-lookup"><span data-stu-id="0f144-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f144-118">高</span><span class="sxs-lookup"><span data-stu-id="0f144-118">High</span></span> |<span data-ttu-id="0f144-119">具有強烈影響的建議應該提供 hello 最重要的效能影響。</span><span class="sxs-lookup"><span data-stu-id="0f144-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="0f144-120">中型</span><span class="sxs-lookup"><span data-stu-id="0f144-120">Medium</span></span> |<span data-ttu-id="0f144-121">中度影響建議會改善效能，但不顯著。</span><span class="sxs-lookup"><span data-stu-id="0f144-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="0f144-122">低</span><span class="sxs-lookup"><span data-stu-id="0f144-122">Low</span></span> |<span data-ttu-id="0f144-123">低影響建議比沒有建議時提供更好的效能，但改善可能不顯著。</span><span class="sxs-lookup"><span data-stu-id="0f144-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="0f144-124">Azure SQL Database 需要 toomonitor 活動至少一天中順序 tooidentify 一些建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="0f144-125">比隨機收訊活動暴增的 hello Azure SQL Database 可以更輕鬆地將最佳化的一致的查詢模式。</span><span class="sxs-lookup"><span data-stu-id="0f144-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="0f144-126">如果建議不使用 corrently，hello**效能建議**頁面會提供訊息說明原因。</span><span class="sxs-lookup"><span data-stu-id="0f144-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="0f144-127">您也可以檢視 hello hello 歷史操作狀態。</span><span class="sxs-lookup"><span data-stu-id="0f144-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="0f144-128">選取建議或狀態 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f144-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="0f144-129">以下是範例的 < Create index"hello Azure 入口網站中的建議動作。</span><span class="sxs-lookup"><span data-stu-id="0f144-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![建立索引](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="0f144-131">套用建議</span><span class="sxs-lookup"><span data-stu-id="0f144-131">Applying recommendations</span></span>
<span data-ttu-id="0f144-132">Azure SQL Database 可讓您完整控制建議的方式啟用使用任何下列三個選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f144-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="0f144-133">一次套用一個個別的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="0f144-134">啟用 hello 自動微調 tooautomatically 套用建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="0f144-135">tooimplement 建議手動執行 hello 建議針對您的資料庫 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0f144-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="0f144-136">選取任何建議 tooview 其詳細資料，然後按一下**檢視指令碼**tooreview hello 確切的 hello 建議的建立方式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f144-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="0f144-137">hello 資料庫仍在線上時套用 hello 建議-使用效能建議或自動調整永遠不會讓資料庫離線。</span><span class="sxs-lookup"><span data-stu-id="0f144-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="0f144-138">套用個別的建議</span><span class="sxs-lookup"><span data-stu-id="0f144-138">Apply an individual recommendation</span></span>
<span data-ttu-id="0f144-139">您可以一次檢閱並接受一個建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="0f144-140">在 hello**建議**刀鋒視窗中，選取的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="0f144-141">在 [hello**詳細資料**刀鋒視窗中按一下**套用**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f144-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![套用建議](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="0f144-143">Hello 資料庫上，將會套用選取的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="0f144-144">移除 hello 清單中的建議</span><span class="sxs-lookup"><span data-stu-id="0f144-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="0f144-145">如果您的建議清單包含您想從 hello 清單 tooremove 項目，您可以捨棄 hello 建議：</span><span class="sxs-lookup"><span data-stu-id="0f144-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="0f144-146">Hello 清單中選取建議**建議**tooopen hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f144-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="0f144-147">按一下**捨棄**上 hello**詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0f144-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="0f144-148">如有需要，您可以將丟棄的項目加回 toohello**建議**清單：</span><span class="sxs-lookup"><span data-stu-id="0f144-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="0f144-149">在 hello**建議**刀鋒視窗中按一下**捨棄檢視**。</span><span class="sxs-lookup"><span data-stu-id="0f144-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="0f144-150">選取已捨棄的項目從 hello 清單 tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f144-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="0f144-151">（選擇性） 按一下**復原捨棄**tooadd hello 索引上一頁 toohello 主要清單**建議**。</span><span class="sxs-lookup"><span data-stu-id="0f144-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="0f144-152">啟用自動微調</span><span class="sxs-lookup"><span data-stu-id="0f144-152">Enable automatic tuning</span></span>
<span data-ttu-id="0f144-153">您可以自動設定 hello Azure SQL Database tooimplement 建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="0f144-154">當建議可供使用時將會自動套用。</span><span class="sxs-lookup"><span data-stu-id="0f144-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="0f144-155">為所有建議受 hello 與服務如果 hello 效能影響為負值 hello 建議將還原。</span><span class="sxs-lookup"><span data-stu-id="0f144-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="0f144-156">在 hello**建議**刀鋒視窗中，按一下 **自動化**:</span><span class="sxs-lookup"><span data-stu-id="0f144-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![建議程式設定](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="0f144-158">選取動作 tooautomate:</span><span class="sxs-lookup"><span data-stu-id="0f144-158">Select actions tooautomate:</span></span>
   
    ![建議的索引](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="0f144-160">手動執行 hello 建議 T-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="0f144-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="0f144-161">選取任何建議，然後按一下檢視指令碼 。</span><span class="sxs-lookup"><span data-stu-id="0f144-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="0f144-162">針對資料庫執行這個指令碼 toomanually 套用 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="0f144-163">*以手動方式執行的索引不受監視且 hello 服務的效能影響驗證*因此建議您在建立 tooverify 之後監視這些索引它們提供效能提升和調整或刪除它們，如果必要的。</span><span class="sxs-lookup"><span data-stu-id="0f144-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="0f144-164">如需有關建立索引的詳細資訊，請參閱 [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0f144-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="0f144-165">取消建議</span><span class="sxs-lookup"><span data-stu-id="0f144-165">Canceling recommendations</span></span>
<span data-ttu-id="0f144-166">可以取消處於**擱置中**、**確認中**或**成功**狀態的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="0f144-167">狀態為 **執行中** 的建議無法取消。</span><span class="sxs-lookup"><span data-stu-id="0f144-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="0f144-168">在 hello 中選取建議**微調記錄**區域 tooopen hello**建議詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0f144-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="0f144-169">按一下**取消**tooabort hello 套用 hello 建議的處理程序。</span><span class="sxs-lookup"><span data-stu-id="0f144-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="0f144-170">監視作業</span><span class="sxs-lookup"><span data-stu-id="0f144-170">Monitoring operations</span></span>
<span data-ttu-id="0f144-171">套用建議時可能不會立即執行。</span><span class="sxs-lookup"><span data-stu-id="0f144-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="0f144-172">hello 入口網站提供建議的 hello 狀態相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f144-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="0f144-173">hello 下面是可以是索引的可能狀態：</span><span class="sxs-lookup"><span data-stu-id="0f144-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="0f144-174">狀態</span><span class="sxs-lookup"><span data-stu-id="0f144-174">Status</span></span> | <span data-ttu-id="0f144-175">說明</span><span class="sxs-lookup"><span data-stu-id="0f144-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f144-176">Pending</span><span class="sxs-lookup"><span data-stu-id="0f144-176">Pending</span></span> |<span data-ttu-id="0f144-177">已收到套用建議命令，且已排程執行。</span><span class="sxs-lookup"><span data-stu-id="0f144-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="0f144-178">執行中</span><span class="sxs-lookup"><span data-stu-id="0f144-178">Executing</span></span> |<span data-ttu-id="0f144-179">正在套用 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="0f144-180">驗證中</span><span class="sxs-lookup"><span data-stu-id="0f144-180">Verifying</span></span> |<span data-ttu-id="0f144-181">已成功套用建議事項和 hello 服務要衡量 hello 優點。</span><span class="sxs-lookup"><span data-stu-id="0f144-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="0f144-182">成功</span><span class="sxs-lookup"><span data-stu-id="0f144-182">Success</span></span> |<span data-ttu-id="0f144-183">已成功套用建議，並證實有益處。</span><span class="sxs-lookup"><span data-stu-id="0f144-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="0f144-184">錯誤</span><span class="sxs-lookup"><span data-stu-id="0f144-184">Error</span></span> |<span data-ttu-id="0f144-185">將套用 hello 建議 hello 程序期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0f144-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="0f144-186">這可以是暫時性的問題，或可能是結構描述變更 toohello 資料表和 hello 指令碼已不再有效。</span><span class="sxs-lookup"><span data-stu-id="0f144-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="0f144-187">還原</span><span class="sxs-lookup"><span data-stu-id="0f144-187">Reverting</span></span> |<span data-ttu-id="0f144-188">hello 建議已套用，但已視為非效能，並自動還原。</span><span class="sxs-lookup"><span data-stu-id="0f144-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="0f144-189">已還原</span><span class="sxs-lookup"><span data-stu-id="0f144-189">Reverted</span></span> |<span data-ttu-id="0f144-190">hello 建議已還原。</span><span class="sxs-lookup"><span data-stu-id="0f144-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="0f144-191">按一下從 hello 清單 toosee 同處理序建議更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="0f144-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![建議的索引](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="0f144-193">還原建議</span><span class="sxs-lookup"><span data-stu-id="0f144-193">Reverting a recommendation</span></span>
<span data-ttu-id="0f144-194">如果您使用 hello 效能建議 tooapply hello 建議 （表示您沒有手動執行 hello T-SQL 指令碼） 它將會自動將它還原如果找到 hello 效能影響 toobe 負數。</span><span class="sxs-lookup"><span data-stu-id="0f144-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="0f144-195">如果您只想 toorevert 因故建議您可以 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0f144-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="0f144-196">選取已成功套用建議事項中 hello**微調記錄**區域。</span><span class="sxs-lookup"><span data-stu-id="0f144-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="0f144-197">按一下**Revert**上 hello**建議詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0f144-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![建議的索引](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="0f144-199">監視索引建議的效能影響</span><span class="sxs-lookup"><span data-stu-id="0f144-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="0f144-200">已成功實作建議之後 （目前，索引作業和參數化查詢建議只） 您可以按一下**查詢 Insights** hello 建議詳細資料 刀鋒視窗 tooopen 上[查詢效能深入資訊](sql-database-query-performance.md)並查看您排名最前面查詢 hello 效能影響。</span><span class="sxs-lookup"><span data-stu-id="0f144-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![監視效能影響](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="0f144-202">摘要</span><span class="sxs-lookup"><span data-stu-id="0f144-202">Summary</span></span>
<span data-ttu-id="0f144-203">Azure SQL Database 會提供可改善 SQL Database 效能的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="0f144-204">藉由提供 T-SQL 指令碼，以及獨立且全自動的，您會獲得最佳化資料庫的實用協助，並最終改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="0f144-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f144-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f144-205">Next steps</span></span>
<span data-ttu-id="0f144-206">監視您的建議，並繼續 tooapply 它們 toorefine 效能。</span><span class="sxs-lookup"><span data-stu-id="0f144-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="0f144-207">資料庫工作負載會動態地持續變更。</span><span class="sxs-lookup"><span data-stu-id="0f144-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="0f144-208">Azure SQL Database 會繼續 toomonitor，並提供可以改善您的資料庫效能的建議。</span><span class="sxs-lookup"><span data-stu-id="0f144-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="0f144-209">請參閱[自動微調](sql-database-automatic-tuning.md)toolearn 深入了解 hello Azure SQL Database 中的自動調整。</span><span class="sxs-lookup"><span data-stu-id="0f144-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="0f144-210">如需 Azure SQL Database 效能建議的概觀，請參閱[效能建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="0f144-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="0f144-211">請參閱[查詢效能深入資訊](sql-database-query-performance.md)toolearn 有關檢視 hello 您排名最前面的查詢效能影響。</span><span class="sxs-lookup"><span data-stu-id="0f144-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f144-212">其他資源</span><span class="sxs-lookup"><span data-stu-id="0f144-212">Additional resources</span></span>
* [<span data-ttu-id="0f144-213">查詢存放區</span><span class="sxs-lookup"><span data-stu-id="0f144-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="0f144-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="0f144-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="0f144-215">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="0f144-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

