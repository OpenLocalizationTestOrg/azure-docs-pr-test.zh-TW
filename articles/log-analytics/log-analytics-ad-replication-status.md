---
title: "Active Directory 複寫狀態，以及 Azure Log Analytics aaaMonitor |Microsoft 文件"
description: "定期 hello Active Directory 複寫狀態解決方案組件監視 Active Directory 環境的任何複寫失敗，並報告 hello 結果 OMS 儀表板上。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a><span data-ttu-id="aa9fa-103">使用 Log Analytics 監視 Active Directory 複寫狀態</span><span class="sxs-lookup"><span data-stu-id="aa9fa-103">Monitor Active Directory replication status with Log Analytics</span></span>

![AD 複寫狀態符號](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

<span data-ttu-id="aa9fa-105">Active Directory 是企業 IT 環境的重要元件。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-105">Active Directory is a key component of an enterprise IT environment.</span></span> <span data-ttu-id="aa9fa-106">tooensure 高可用性和高效能，每個網域控制站有它自己的 hello Active Directory 資料庫複本。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-106">tooensure high availability and high performance, each domain controller has its own copy of hello Active Directory database.</span></span> <span data-ttu-id="aa9fa-107">網域控制站複寫彼此順序 toopropagate 變更 hello 企業。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-107">Domain controllers replicate with each other in order toopropagate changes across hello enterprise.</span></span> <span data-ttu-id="aa9fa-108">在此複寫程序中的失敗可導致各種問題 hello 企業。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-108">Failures in this replication process can cause a variety of problems across hello enterprise.</span></span>

<span data-ttu-id="aa9fa-109">定期 hello AD 複寫狀態解決方案組件監視 Active Directory 環境的任何複寫失敗，並報告 hello 結果 OMS 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-109">hello AD Replication Status solution pack regularly monitors your Active Directory environment for any replication failures and reports hello results on your OMS dashboard.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="aa9fa-110">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="aa9fa-110">Installing and configuring hello solution</span></span>
<span data-ttu-id="aa9fa-111">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-111">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="aa9fa-112">您必須是評估 hello 網域 toobe 的成員的網域控制站上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-112">You must install agents on domain controllers that are members of hello domain toobe evaluated.</span></span> <span data-ttu-id="aa9fa-113">或者，您必須在成員伺服器上安裝代理程式和設定 hello 代理程式 toosend AD 複寫資料 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-113">Or, you must install agents on member servers and configure hello agents toosend AD replication data tooOMS.</span></span> <span data-ttu-id="aa9fa-114">如何 tooconnect Windows 電腦 tooOMS，請參閱的 toounderstand[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-114">toounderstand how tooconnect Windows computers tooOMS, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="aa9fa-115">如果您的網域控制站已經是您想 tooconnect tooOMS 現有 System Center Operations Manager 環境的一部分，請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-115">If your domain controller is already part of an existing System Center Operations Manager environment that you want tooconnect tooOMS, see [Connect Operations Manager tooLog Analytics](log-analytics-om-agents.md).</span></span>
* <span data-ttu-id="aa9fa-116">新增 hello OMS 工作區中使用 hello 程序中所述的 Active Directory 複寫狀態方案 tooyour [hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-116">Add hello Active Directory Replication Status solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="aa9fa-117">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-117">There is no further configuration required.</span></span>

## <a name="ad-replication-status-data-collection-details"></a><span data-ttu-id="aa9fa-118">AD 複寫狀態資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="aa9fa-118">AD Replication Status data collection details</span></span>
<span data-ttu-id="aa9fa-119">hello 下表顯示資料收集方法，以及如何針對 AD 複寫狀態收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-119">hello following table shows data collection methods and other details about how data is collected for AD Replication Status.</span></span>

| <span data-ttu-id="aa9fa-120">平台</span><span class="sxs-lookup"><span data-stu-id="aa9fa-120">platform</span></span> | <span data-ttu-id="aa9fa-121">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="aa9fa-121">Direct Agent</span></span> | <span data-ttu-id="aa9fa-122">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="aa9fa-122">SCOM agent</span></span> | <span data-ttu-id="aa9fa-123">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="aa9fa-123">Azure Storage</span></span> | <span data-ttu-id="aa9fa-124">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="aa9fa-124">SCOM required?</span></span> | <span data-ttu-id="aa9fa-125">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="aa9fa-125">SCOM agent data sent via management group</span></span> | <span data-ttu-id="aa9fa-126">收集頻率</span><span class="sxs-lookup"><span data-stu-id="aa9fa-126">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="aa9fa-127">Windows</span><span class="sxs-lookup"><span data-stu-id="aa9fa-127">Windows</span></span> |<span data-ttu-id="aa9fa-128">&#8226;</span><span class="sxs-lookup"><span data-stu-id="aa9fa-128">&#8226;</span></span> |<span data-ttu-id="aa9fa-129">&#8226;</span><span class="sxs-lookup"><span data-stu-id="aa9fa-129">&#8226;</span></span> |  |  |<span data-ttu-id="aa9fa-130">&#8226;</span><span class="sxs-lookup"><span data-stu-id="aa9fa-130">&#8226;</span></span> |<span data-ttu-id="aa9fa-131">每隔五天</span><span class="sxs-lookup"><span data-stu-id="aa9fa-131">every five days</span></span> |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a><span data-ttu-id="aa9fa-132">（選擇性） 啟用非網域控制站 toosend AD 資料 tooOMS</span><span class="sxs-lookup"><span data-stu-id="aa9fa-132">Optionally, enable a non-domain controller toosend AD data tooOMS</span></span>
<span data-ttu-id="aa9fa-133">如果您不想 tooconnect 任何網域控制站直接 tooOMS，您可以使用其他 OMS 連線的電腦在您的網域 toocollect 資料 hello AD 複寫狀態方案組件，並讓它傳送嗨資料。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-133">If you don't want tooconnect any of your domain controllers directly tooOMS, you can use any other OMS-connected computer in your domain toocollect data for hello AD Replication Status solution pack and have it send hello data.</span></span>

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a><span data-ttu-id="aa9fa-134">非網域控制站 toosend AD 資料 tooOMS tooenable</span><span class="sxs-lookup"><span data-stu-id="aa9fa-134">tooenable a non-domain controller toosend AD data tooOMS</span></span>
1. <span data-ttu-id="aa9fa-135">請確認該 hello 電腦是您想使用 hello AD 複寫狀態解決方案 toomonitor hello 網域的成員。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-135">Verify that hello computer is a member of hello domain that you wish toomonitor using hello AD Replication Status solution.</span></span>
2. <span data-ttu-id="aa9fa-136">[連接 hello Windows 電腦 tooOMS](log-analytics-windows-agents.md)或[連接使用您現有的 Operations Manager 環境 tooOMS](log-analytics-om-agents.md)，如果您尚未連接。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-136">[Connect hello Windows computer tooOMS](log-analytics-windows-agents.md) or [connect it using your existing Operations Manager environment tooOMS](log-analytics-om-agents.md), if it is not already connected.</span></span>
3. <span data-ttu-id="aa9fa-137">該電腦上，設定下列登錄機碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="aa9fa-137">On that computer, set hello following registry key:</span></span>

   * <span data-ttu-id="aa9fa-138">機碼：**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-138">Key: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span></span>
   * <span data-ttu-id="aa9fa-139">值：**IsTarget**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-139">Value: **IsTarget**</span></span>
   * <span data-ttu-id="aa9fa-140">數值資料︰**true**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-140">Value Data: **true**</span></span>

   > [!NOTE]
   > <span data-ttu-id="aa9fa-141">這些變更不會影響直到您重新啟動 hello Microsoft Monitoring Agent 服務 (HealthService.exe)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-141">These changes do not take effect until your restart hello Microsoft Monitoring Agent service (HealthService.exe).</span></span>
   >
   >

## <a name="understanding-replication-errors"></a><span data-ttu-id="aa9fa-142">了解複寫錯誤</span><span class="sxs-lookup"><span data-stu-id="aa9fa-142">Understanding replication errors</span></span>
<span data-ttu-id="aa9fa-143">一旦傳送 tooOMS AD 複寫狀態資料，您會看到下列影像指出您目前有多少複寫錯誤 hello OMS 儀表板上並排顯示類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-143">Once you have AD replication status data sent tooOMS, you see a tile similar toohello following image on hello OMS dashboard indicating how many replication errors you currently have.</span></span>  
![AD 複寫狀態圖格](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

<span data-ttu-id="aa9fa-145">**重要的複寫錯誤**錯誤會等於或高於 75%的 hello[標記存留時間](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx)為 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-145">**Critical Replication Errors** are errors that are at or above 75% of hello [tombstone lifetime](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) for your Active Directory forest.</span></span>

<span data-ttu-id="aa9fa-146">當您按一下 hello 磚時，您可以檢視 hello 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-146">When you click hello tile, you can view more information about hello errors.</span></span>
<span data-ttu-id="aa9fa-147">![AD 複寫狀態儀表板](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span><span class="sxs-lookup"><span data-stu-id="aa9fa-147">![AD Replication Status dashboard](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span></span>

### <a name="destination-server-status-and-source-server-status"></a><span data-ttu-id="aa9fa-148">目的地伺服器狀態和來源伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="aa9fa-148">Destination Server Status and Source Server Status</span></span>
<span data-ttu-id="aa9fa-149">這些資料行會顯示 hello 狀態，目的地伺服器以及發生複寫錯誤的來源伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-149">These columns show hello status of destination servers and source servers that are experiencing replication errors.</span></span> <span data-ttu-id="aa9fa-150">每個網域控制站名稱之後的 hello 數字表示該網域控制站上的複寫錯誤的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-150">hello number after each domain controller name indicates hello number of replication errors on that domain controller.</span></span>

<span data-ttu-id="aa9fa-151">目的地伺服器和來源伺服器 hello 錯誤會顯示，因為某些問題會更容易 tootroubleshoot 觀點 hello 來源伺服器和其他人 hello 目的地伺服器檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-151">hello errors for both destination servers and source servers are shown because some problems are easier tootroubleshoot from hello source server perspective and others from hello destination server perspective.</span></span>

<span data-ttu-id="aa9fa-152">在此範例中，您可以看到多個目的地伺服器都面臨 hello 相同數目的錯誤，但有一部來源伺服器 (ADDC35) 多詳細的錯誤，所有 hello 比其他項目。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-152">In this example, you can see that many destination servers have roughly hello same number of errors, but there's one source server (ADDC35) that has many more errors than all hello others.</span></span> <span data-ttu-id="aa9fa-153">很可能導致 toofail toosend 資料 tooits 複寫協力電腦的 ADDC35 上沒有發生問題。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-153">It's likely that there is some problem on ADDC35 that is causing it toofail toosend data tooits replication partners.</span></span> <span data-ttu-id="aa9fa-154">修正 hello 問題 ADDC35 上可能會解決許多 hello 目的地伺服器 區域中出現的 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-154">Fixing hello problems on ADDC35 might resolve many of hello errors that appear in hello destination server area.</span></span>

### <a name="replication-error-types"></a><span data-ttu-id="aa9fa-155">複寫錯誤類型</span><span class="sxs-lookup"><span data-stu-id="aa9fa-155">Replication Error Types</span></span>
<span data-ttu-id="aa9fa-156">這個區域可讓您的整個企業內偵測到錯誤的 hello 類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-156">This area gives you information about hello types of errors detected throughout your enterprise.</span></span> <span data-ttu-id="aa9fa-157">每個錯誤有唯一的數字代碼和訊息，可協助您判斷 hello hello 錯誤根本原因。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-157">Each error has a unique numerical code and a message that can help you determine hello root cause of hello error.</span></span>

<span data-ttu-id="aa9fa-158">hello 甜甜圈 hello 頂端讓您的瞭解其中錯誤會出現多個且較不常在您的環境。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-158">hello donut at hello top gives you an idea of which errors appear more and less frequently in your environment.</span></span>

<span data-ttu-id="aa9fa-159">它會示範多個網域控制站發生 hello 時相同的複寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-159">It shows you when multiple domain controllers experience hello same replication error.</span></span> <span data-ttu-id="aa9fa-160">在此情況下，您可能會無法 toodiscover 或識別一個網域控制站，方案然後重複它在其他網域控制站上受到 hello 相同錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-160">In this case, you may be able toodiscover or identify a solution on one domain controller, then repeat it on other domain controllers affected by hello same error.</span></span>

### <a name="tombstone-lifetime"></a><span data-ttu-id="aa9fa-161">標記存留期</span><span class="sxs-lookup"><span data-stu-id="aa9fa-161">Tombstone Lifetime</span></span>
<span data-ttu-id="aa9fa-162">hello 標記存留時間決定多久已刪除的物件，參考 tooas 標記，會保留在 hello Active Directory 資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-162">hello tombstone lifetime determines how long a deleted object, referred tooas a tombstone, is retained in hello Active Directory database.</span></span> <span data-ttu-id="aa9fa-163">已刪除的物件會傳遞 hello 標記存留時間，記憶體回收處理會自動移除它從 hello Active Directory 資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-163">When a deleted object passes hello tombstone lifetime, a garbage collection process automatically removes it from hello Active Directory database.</span></span>

<span data-ttu-id="aa9fa-164">hello 預設標記存留期為 180 天的最新的 Windows 版本，但它是較舊的版本 60 天和它的 Active Directory 系統管理員可以明確地變更。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-164">hello default tombstone lifetime is 180 days for most recent versions of Windows, but it was 60 days on older versions, and it can be changed explicitly by an Active Directory administrator.</span></span>

<span data-ttu-id="aa9fa-165">如果您有已接近或超過 hello 標記存留時間的複寫錯誤，很重要的 tooknow。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-165">It's important tooknow if you're having replication errors that are approaching or are past hello tombstone lifetime.</span></span> <span data-ttu-id="aa9fa-166">如果兩個網域控制站發生複寫錯誤的 hello 標記存留時間超過持續發生，是停用複寫之間的兩個網域控制站，即使固定的 hello 基礎複寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-166">If two domain controllers experience a replication error that persists past hello tombstone lifetime, replication is disabled between those two domain controllers, even if hello underlying replication error is fixed.</span></span>

<span data-ttu-id="aa9fa-167">hello 標記存留時間區域，可協助您識別可能發生已停用的複寫的所在的位置。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-167">hello Tombstone Lifetime area helps you identify places where disabled replication is in danger of happening.</span></span> <span data-ttu-id="aa9fa-168">每個錯誤中 hello**超過 100 %tsl**類別代表尚未複寫其來源和目的地伺服器之間的在最少 hello 樹系的 hello 標記存留時間的資料分割。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-168">Each error in hello **Over 100% TSL** category represents a partition that has not replicated between its source and destination server for at least hello tombstone lifetime for hello forest.</span></span>

<span data-ttu-id="aa9fa-169">在此情況下，只需修正 hello 複寫錯誤將不太夠。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-169">In this situation, simply fixing hello replication error will not be enough.</span></span> <span data-ttu-id="aa9fa-170">至少，您需要 toomanually 調查 tooidentify 並清除延遲物件，然後才能重新啟動複寫。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-170">At a minimum, you need toomanually investigate tooidentify and clean up lingering objects before you can restart replication.</span></span> <span data-ttu-id="aa9fa-171">您甚至可能需要 toodecommission 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-171">You may even need toodecommission a domain controller.</span></span>

<span data-ttu-id="aa9fa-172">在加法 tooidentifying hello 標記存留時間，超過的保存任何複寫錯誤您也想 toopay 注意 tooany 錯誤落入 hello **50-75 %tsl**或**75 100 %tsl**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-172">In addition tooidentifying any replication errors that have persisted past hello tombstone lifetime, you also want toopay attention tooany errors falling into hello **50-75% TSL** or **75-100% TSL** categories.</span></span>

<span data-ttu-id="aa9fa-173">這些是會清楚地延遲、 不暫時性的因此它們可能需要您介入 tooresolve 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-173">These are errors that are clearly lingering, not transient, so they likely need your intervention tooresolve.</span></span> <span data-ttu-id="aa9fa-174">hello 好消息是，它們尚未到達 hello 標記存留時間。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-174">hello good news is that they have not yet reached hello tombstone lifetime.</span></span> <span data-ttu-id="aa9fa-175">如果您立即修正這些問題和*之前*到達 hello 標記存留時間，複寫可以重新啟動具有最少手動介入。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-175">If you fix these problems promptly and *before* they reach hello tombstone lifetime, replication can restart with minimal manual intervention.</span></span>

<span data-ttu-id="aa9fa-176">如前文所述，hello AD 複寫狀態解決方案的 hello 儀表板磚會顯示 hello 數目*重大*複寫錯誤，在您環境中，定義為超過 75%的標記存留時間 （包括錯誤錯誤會超過 100%的 TSL）。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-176">As noted earlier, hello dashboard tile for hello AD Replication Status solution shows hello number of *critical* replication errors in your environment, which is defined as errors that are over 75% of tombstone lifetime (including errors that are over 100% of TSL).</span></span> <span data-ttu-id="aa9fa-177">盡可能 tookeep 0 這個數字。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-177">Strive tookeep this number at 0.</span></span>

> [!NOTE]
> <span data-ttu-id="aa9fa-178">所有的 hello 標記存留期百分比計算根據您的 Active Directory 樹系的 hello 實際的標記存留時間，讓您可以信任這些百分比是正確的即使您擁有設定自訂的標記存留時間值。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-178">All hello tombstone lifetime percentage calculations are based on hello actual tombstone lifetime for your Active Directory forest, so you can trust that those percentages are accurate, even if you have a custom tombstone lifetime value set.</span></span>
>
>

### <a name="ad-replication-status-details"></a><span data-ttu-id="aa9fa-179">AD 複寫狀態詳細資料</span><span class="sxs-lookup"><span data-stu-id="aa9fa-179">AD Replication status details</span></span>
<span data-ttu-id="aa9fa-180">當您按一下其中一個 hello 清單中的任何項目時，您會看到資訊，請使用 記錄搜尋的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-180">When you click any item in one of hello lists, you see additional details about it using Log Search.</span></span> <span data-ttu-id="aa9fa-181">hello 結果是已篩選的 tooshow 只有 hello 錯誤 toothat 相關項目。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-181">hello results are filtered tooshow only hello errors related toothat item.</span></span> <span data-ttu-id="aa9fa-182">例如，如果您按一下第一個網域控制站 hello 底下所列**目的地伺服器狀態 (ADDC02)**，您會看到篩選 tooshow 錯誤與該列為 hello 目的地伺服器的網域控制站的搜尋結果：</span><span class="sxs-lookup"><span data-stu-id="aa9fa-182">For example, if you click on hello first domain controller listed under **Destination Server Status (ADDC02)**, you see search results filtered tooshow errors with that domain controller listed as hello destination server:</span></span>

![搜尋結果中的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

<span data-ttu-id="aa9fa-184">從這裡，您可以進一步篩選，修改 hello 的搜尋查詢，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-184">From here, you can filter further, modify hello search query, and so on.</span></span> <span data-ttu-id="aa9fa-185">如需使用記錄搜尋 hello 的詳細資訊，請參閱[記錄搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-185">For more information about using hello Log Search, see [Log searches](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="aa9fa-186">hello **HelpLink**欄位會顯示有關該特定錯誤的其他詳細資料與 TechNet 頁面 hello URL。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-186">hello **HelpLink** field shows hello URL of a TechNet page with additional details about that specific error.</span></span> <span data-ttu-id="aa9fa-187">您可以複製並貼入您的瀏覽器視窗 toosee 資訊，疑難排解和修正 hello 錯誤相關的此連結。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-187">You can copy and paste this link into your browser window toosee information about troubleshooting and fixing hello error.</span></span>

<span data-ttu-id="aa9fa-188">您也可以按一下**匯出**tooexport hello 結果 tooExcel。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-188">You can also click **Export** tooexport hello results tooExcel.</span></span> <span data-ttu-id="aa9fa-189">匯出 hello 資料可協助您以任何您想要的方式複寫錯誤資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-189">Exporting hello data can help you visualize replication error data in any way you'd like.</span></span>

![Excel 中匯出的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a><span data-ttu-id="aa9fa-191">AD 複寫狀態常見問題集</span><span class="sxs-lookup"><span data-stu-id="aa9fa-191">AD Replication Status FAQ</span></span>
<span data-ttu-id="aa9fa-192">**問︰多久更新一次 AD 複寫狀態資料？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-192">**Q: How often is AD replication status data updated?**</span></span>
<span data-ttu-id="aa9fa-193">答： hello 資訊會更新每隔五天。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-193">A: hello information is updated every five days.</span></span>

<span data-ttu-id="aa9fa-194">**問： 是否有這項資料更新頻率的方式 tooconfigure？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-194">**Q: Is there a way tooconfigure how often this data is updated?**</span></span>
<span data-ttu-id="aa9fa-195">答：目前沒有。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-195">A: Not at this time.</span></span>

<span data-ttu-id="aa9fa-196">**問： 我需要 tooadd 所有我的網域控制站 toomy OMS 工作區中訂單 toosee 複寫狀態？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-196">**Q: Do I need tooadd all of my domain controllers toomy OMS workspace in order toosee replication status?**</span></span>
<span data-ttu-id="aa9fa-197">答︰否，只需加入單一網域控制站。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-197">A: No, only a single domain controller must be added.</span></span> <span data-ttu-id="aa9fa-198">如果您有多個網域控制站，您的 OMS 工作區中，所有這些資料會傳送 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-198">If you have multiple domain controllers in your OMS workspace, data from all of them is sent tooOMS.</span></span>

<span data-ttu-id="aa9fa-199">**問： 我不想 tooadd 任何網域控制站 toomy OMS 工作區。仍然可以使用 hello AD 複寫狀態方案嗎？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-199">**Q: I don't want tooadd any domain controllers toomy OMS workspace. Can I still use hello AD Replication Status solution?**</span></span>
<span data-ttu-id="aa9fa-200">答： 會。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-200">A: Yes.</span></span> <span data-ttu-id="aa9fa-201">您可以設定的登錄金鑰 tooenable hello 值它。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-201">You can set hello value of a registry key tooenable it.</span></span> <span data-ttu-id="aa9fa-202">請參閱[tooenable 非網域控制站 toosend AD 資料 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-202">See [tooenable a non-domain controller toosend AD data tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

<span data-ttu-id="aa9fa-203">**問： hello 沒有 hello 資料收集的 hello 程序名稱為何？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-203">**Q: What is hello name of hello process that does hello data collection?**</span></span>
<span data-ttu-id="aa9fa-204">答︰AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="aa9fa-204">A: AdvisorAssessment.exe</span></span>

<span data-ttu-id="aa9fa-205">**問： 如何花費時間的資料收集的 toobe？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-205">**Q: How long does it take for data toobe collected?**</span></span>
<span data-ttu-id="aa9fa-206">答： 資料收集時間的 hello 的 Active Directory 環境的 hello 大小而定，但程序通常需要 15 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-206">A: Data collection time depends on hello size of hello Active Directory environment, but usually takes less than 15 minutes.</span></span>

<span data-ttu-id="aa9fa-207">**問：收集的資料類型為何？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-207">**Q: What type of data is collected?**</span></span>
<span data-ttu-id="aa9fa-208">答：複寫資訊是透過 LDAP 收集。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-208">A: Replication information is collected via LDAP.</span></span>

<span data-ttu-id="aa9fa-209">**問： 是否有方法 tooconfigure，資料收集時間？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-209">**Q: Is there a way tooconfigure when data is collected?**</span></span>
<span data-ttu-id="aa9fa-210">答：目前沒有。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-210">A: Not at this time.</span></span>

<span data-ttu-id="aa9fa-211">**問： 哪些權限執行我需要 toocollect 資料嗎？**</span><span class="sxs-lookup"><span data-stu-id="aa9fa-211">**Q: What permissions do I need toocollect data?**</span></span>
<span data-ttu-id="aa9fa-212">答： 一般使用者權限 tooActive 目錄，已足夠。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-212">A: Normal user permissions tooActive Directory are sufficient.</span></span>

## <a name="troubleshoot-data-collection-problems"></a><span data-ttu-id="aa9fa-213">疑難排解資料收集問題</span><span class="sxs-lookup"><span data-stu-id="aa9fa-213">Troubleshoot data collection problems</span></span>
<span data-ttu-id="aa9fa-214">在訂單 toocollect 資料，hello AD 複寫狀態解決方案組件都需要至少一個網域控制站連線的 toobe tooyour OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-214">In order toocollect data, hello AD Replication Status solution pack requires at least one domain controller toobe connected tooyour OMS workspace.</span></span> <span data-ttu-id="aa9fa-215">連接網域控制站後，會彈出訊息顯示**資料仍在收集中**。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-215">Until you connect a domain controller, a message appears indicating that **data is still being collected**.</span></span>

<span data-ttu-id="aa9fa-216">如果您需要協助連接其中一個網域控制站，您可以檢視文件，網址[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-216">If you need assistance connecting one of your domain controllers, you can view documentation at [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="aa9fa-217">或者，如果您的網域控制站已經連線的 tooan 現有 System Center Operations Manager 環境，您可以檢視文件，網址[連接 System Center Operations Manager tooLog 分析](log-analytics-om-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-217">Alternatively, if your domain controller is already connected tooan existing System Center Operations Manager environment, you can view documentation at [Connect System Center Operations Manager tooLog Analytics](log-analytics-om-agents.md).</span></span>

<span data-ttu-id="aa9fa-218">如果您不想 tooconnect 任何網域控制站直接 tooOMS 或 tooSCOM，請參閱[tooenable 非網域控制站 toosend AD 資料 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-218">If you don't want tooconnect any of your domain controllers directly tooOMS or tooSCOM, see [tooenable a non-domain controller toosend AD data tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa9fa-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa9fa-219">Next steps</span></span>
* <span data-ttu-id="aa9fa-220">使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Active Directory 複寫狀態資料。</span><span class="sxs-lookup"><span data-stu-id="aa9fa-220">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Active Directory Replication status data.</span></span>
