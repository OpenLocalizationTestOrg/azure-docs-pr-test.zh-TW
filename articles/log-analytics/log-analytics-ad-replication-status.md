---
title: "使用 Azure Log Analytics 監視 Active Directory 複寫狀態 | Microsoft Docs"
description: "Active Directory 複寫狀態解決方案組件會定期監控您的 Active Directory 環境是否有任何複寫失敗，並在 OMS 儀表板上報告結果。"
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
ms.openlocfilehash: bfe52ef5d9d09ffe179faaf6ffbd90ef964fbda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a><span data-ttu-id="569ef-103">使用 Log Analytics 監視 Active Directory 複寫狀態</span><span class="sxs-lookup"><span data-stu-id="569ef-103">Monitor Active Directory replication status with Log Analytics</span></span>

![AD 複寫狀態符號](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

<span data-ttu-id="569ef-105">Active Directory 是企業 IT 環境的重要元件。</span><span class="sxs-lookup"><span data-stu-id="569ef-105">Active Directory is a key component of an enterprise IT environment.</span></span> <span data-ttu-id="569ef-106">為了確保高可用性和高效能，每個網域控制站有它自己的 Active Directory 資料庫複本。</span><span class="sxs-lookup"><span data-stu-id="569ef-106">To ensure high availability and high performance, each domain controller has its own copy of the Active Directory database.</span></span> <span data-ttu-id="569ef-107">網域控制站會彼此複寫，以便將變更傳播到整個企業。</span><span class="sxs-lookup"><span data-stu-id="569ef-107">Domain controllers replicate with each other in order to propagate changes across the enterprise.</span></span> <span data-ttu-id="569ef-108">此複寫處理序中的失敗可導致整個企業發生各種問題。</span><span class="sxs-lookup"><span data-stu-id="569ef-108">Failures in this replication process can cause a variety of problems across the enterprise.</span></span>

<span data-ttu-id="569ef-109">AD 複寫狀態解決方案組件會定期監控您的 Active Directory 環境是否有任何複寫失敗，並在 OMS 儀表板上報告結果。</span><span class="sxs-lookup"><span data-stu-id="569ef-109">The AD Replication Status solution pack regularly monitors your Active Directory environment for any replication failures and reports the results on your OMS dashboard.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="569ef-110">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="569ef-110">Installing and configuring the solution</span></span>
<span data-ttu-id="569ef-111">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="569ef-111">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="569ef-112">您必須將代理程式安裝在隸屬於要評估之網域成員的網域控制站上。</span><span class="sxs-lookup"><span data-stu-id="569ef-112">You must install agents on domain controllers that are members of the domain to be evaluated.</span></span> <span data-ttu-id="569ef-113">或者您必須將代理程式安裝在成員之伺服器上，並設定讓代理程式將 AD 複寫資料傳送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="569ef-113">Or, you must install agents on member servers and configure the agents to send AD replication data to OMS.</span></span> <span data-ttu-id="569ef-114">若要了解如何將 Windows 電腦連接到 OMS，請參閱 [將 Windows 電腦連接到 Log Analytics](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="569ef-114">To understand how to connect Windows computers to OMS, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="569ef-115">如果您的網域控制站已屬於您要連接到 OMS 的現有 System Center Operations Manager 環境，請參閱 [將 Operations Manager 連接到 Log Analytics](log-analytics-om-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="569ef-115">If your domain controller is already part of an existing System Center Operations Manager environment that you want to connect to OMS, see [Connect Operations Manager to Log Analytics](log-analytics-om-agents.md).</span></span>
* <span data-ttu-id="569ef-116">使用 [從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)中所述的處理序，將 Active Directory 複寫狀態方案加入您的 OMS 工作區中。</span><span class="sxs-lookup"><span data-stu-id="569ef-116">Add the Active Directory Replication Status solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="569ef-117">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="569ef-117">There is no further configuration required.</span></span>

## <a name="ad-replication-status-data-collection-details"></a><span data-ttu-id="569ef-118">AD 複寫狀態資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="569ef-118">AD Replication Status data collection details</span></span>
<span data-ttu-id="569ef-119">下表顯示 AD 複寫狀態的資料收集方法和其他資料收集方式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="569ef-119">The following table shows data collection methods and other details about how data is collected for AD Replication Status.</span></span>

| <span data-ttu-id="569ef-120">平台</span><span class="sxs-lookup"><span data-stu-id="569ef-120">platform</span></span> | <span data-ttu-id="569ef-121">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="569ef-121">Direct Agent</span></span> | <span data-ttu-id="569ef-122">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="569ef-122">SCOM agent</span></span> | <span data-ttu-id="569ef-123">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="569ef-123">Azure Storage</span></span> | <span data-ttu-id="569ef-124">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="569ef-124">SCOM required?</span></span> | <span data-ttu-id="569ef-125">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="569ef-125">SCOM agent data sent via management group</span></span> | <span data-ttu-id="569ef-126">收集頻率</span><span class="sxs-lookup"><span data-stu-id="569ef-126">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="569ef-127">Windows</span><span class="sxs-lookup"><span data-stu-id="569ef-127">Windows</span></span> |<span data-ttu-id="569ef-128">&#8226;</span><span class="sxs-lookup"><span data-stu-id="569ef-128">&#8226;</span></span> |<span data-ttu-id="569ef-129">&#8226;</span><span class="sxs-lookup"><span data-stu-id="569ef-129">&#8226;</span></span> |  |  |<span data-ttu-id="569ef-130">&#8226;</span><span class="sxs-lookup"><span data-stu-id="569ef-130">&#8226;</span></span> |<span data-ttu-id="569ef-131">每隔五天</span><span class="sxs-lookup"><span data-stu-id="569ef-131">every five days</span></span> |

## <a name="optionally-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a><span data-ttu-id="569ef-132">(選擇性) 啟用非網域控制站以將 AD 資料傳送至 OMS</span><span class="sxs-lookup"><span data-stu-id="569ef-132">Optionally, enable a non-domain controller to send AD data to OMS</span></span>
<span data-ttu-id="569ef-133">如果您不要將任何網域控制站直接連接到 OMS，您可以使用網域中任何其他 OMS 連線的電腦來收集 AD 複寫狀態解決方案組件的資料並讓它傳送資料。</span><span class="sxs-lookup"><span data-stu-id="569ef-133">If you don't want to connect any of your domain controllers directly to OMS, you can use any other OMS-connected computer in your domain to collect data for the AD Replication Status solution pack and have it send the data.</span></span>

### <a name="to-enable-a-non-domain-controller-to-send-ad-data-to-oms"></a><span data-ttu-id="569ef-134">啟用非網域控制站以將 AD 資料傳送至 OMS</span><span class="sxs-lookup"><span data-stu-id="569ef-134">To enable a non-domain controller to send AD data to OMS</span></span>
1. <span data-ttu-id="569ef-135">確認電腦是您要使用 AD 複寫狀態解決方案監視的網域成員。</span><span class="sxs-lookup"><span data-stu-id="569ef-135">Verify that the computer is a member of the domain that you wish to monitor using the AD Replication Status solution.</span></span>
2. <span data-ttu-id="569ef-136">如果尚未連線，請[將 Windows 電腦連線到 OMS](log-analytics-windows-agents.md)，或[使用現有的 Operations Manager 環境將它連線到 OMS](log-analytics-om-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="569ef-136">[Connect the Windows computer to OMS](log-analytics-windows-agents.md) or [connect it using your existing Operations Manager environment to OMS](log-analytics-om-agents.md), if it is not already connected.</span></span>
3. <span data-ttu-id="569ef-137">該該電腦上，設定下列登錄機碼︰</span><span class="sxs-lookup"><span data-stu-id="569ef-137">On that computer, set the following registry key:</span></span>

   * <span data-ttu-id="569ef-138">機碼：**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span><span class="sxs-lookup"><span data-stu-id="569ef-138">Key: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span></span>
   * <span data-ttu-id="569ef-139">值：**IsTarget**</span><span class="sxs-lookup"><span data-stu-id="569ef-139">Value: **IsTarget**</span></span>
   * <span data-ttu-id="569ef-140">數值資料︰**true**</span><span class="sxs-lookup"><span data-stu-id="569ef-140">Value Data: **true**</span></span>

   > [!NOTE]
   > <span data-ttu-id="569ef-141">在您重新啟動 Microsoft Monitoring Agent service (HealthService.exe) 後，這些變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="569ef-141">These changes do not take effect until your restart the Microsoft Monitoring Agent service (HealthService.exe).</span></span>
   >
   >

## <a name="understanding-replication-errors"></a><span data-ttu-id="569ef-142">了解複寫錯誤</span><span class="sxs-lookup"><span data-stu-id="569ef-142">Understanding replication errors</span></span>
<span data-ttu-id="569ef-143">將 AD 複寫狀態資料傳送至 OMS 後，您會在 OMS 儀表板上看到如下圖所示的圖格，指出目前有多少複寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-143">Once you have AD replication status data sent to OMS, you see a tile similar to the following image on the OMS dashboard indicating how many replication errors you currently have.</span></span>  
![AD 複寫狀態圖格](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

<span data-ttu-id="569ef-145">**重大複寫錯誤** 就是達到或超過 Active Directory 樹系 75% [標記存留期](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-145">**Critical Replication Errors** are errors that are at or above 75% of the [tombstone lifetime](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) for your Active Directory forest.</span></span>

<span data-ttu-id="569ef-146">當您按一下圖格時，您可以檢視有關錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="569ef-146">When you click the tile, you can view more information about the errors.</span></span>
<span data-ttu-id="569ef-147">![AD 複寫狀態儀表板](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span><span class="sxs-lookup"><span data-stu-id="569ef-147">![AD Replication Status dashboard](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span></span>

### <a name="destination-server-status-and-source-server-status"></a><span data-ttu-id="569ef-148">目的地伺服器狀態和來源伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="569ef-148">Destination Server Status and Source Server Status</span></span>
<span data-ttu-id="569ef-149">這些欄位會顯示發生複寫錯誤的目的地伺服器和來源伺服器的狀態。</span><span class="sxs-lookup"><span data-stu-id="569ef-149">These columns show the status of destination servers and source servers that are experiencing replication errors.</span></span> <span data-ttu-id="569ef-150">每個網域控制站名稱後面的數字表示該網域控制站上的複寫錯誤數目。</span><span class="sxs-lookup"><span data-stu-id="569ef-150">The number after each domain controller name indicates the number of replication errors on that domain controller.</span></span>

<span data-ttu-id="569ef-151">目的地伺服器和來源伺服器的錯誤都會顯示，因為從來源伺服器的觀點來看，有些問題比較容易排解，而從目的地伺服器的觀點來看，另一些問題則比較容易排解。</span><span class="sxs-lookup"><span data-stu-id="569ef-151">The errors for both destination servers and source servers are shown because some problems are easier to troubleshoot from the source server perspective and others from the destination server perspective.</span></span>

<span data-ttu-id="569ef-152">在此範例中，您可以看到許多目的地伺服器的錯誤數目大致相同，但有一部來源伺服器 (ADDC35) 具有比其他伺服器更多的錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-152">In this example, you can see that many destination servers have roughly the same number of errors, but there's one source server (ADDC35) that has many more errors than all the others.</span></span> <span data-ttu-id="569ef-153">ADDC35 上可能有些問題導致它無法將資料傳送至其複寫夥伴。</span><span class="sxs-lookup"><span data-stu-id="569ef-153">It's likely that there is some problem on ADDC35 that is causing it to fail to send data to its replication partners.</span></span> <span data-ttu-id="569ef-154">修正 ADDC35 上的問題可能會解決目的地伺服器區域中出現的許多錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-154">Fixing the problems on ADDC35 might resolve many of the errors that appear in the destination server area.</span></span>

### <a name="replication-error-types"></a><span data-ttu-id="569ef-155">複寫錯誤類型</span><span class="sxs-lookup"><span data-stu-id="569ef-155">Replication Error Types</span></span>
<span data-ttu-id="569ef-156">此區域可提供在您的企業中偵測到的錯誤類型相關資訊。</span><span class="sxs-lookup"><span data-stu-id="569ef-156">This area gives you information about the types of errors detected throughout your enterprise.</span></span> <span data-ttu-id="569ef-157">每個錯誤都有唯一的數字代碼和訊息，可協助您判斷錯誤的根本原因。</span><span class="sxs-lookup"><span data-stu-id="569ef-157">Each error has a unique numerical code and a message that can help you determine the root cause of the error.</span></span>

<span data-ttu-id="569ef-158">頂端的圓圈可讓您了解在您的環境中哪些錯誤較常和較不常出現。</span><span class="sxs-lookup"><span data-stu-id="569ef-158">The donut at the top gives you an idea of which errors appear more and less frequently in your environment.</span></span>

<span data-ttu-id="569ef-159">會顯示多個網域控制站在何時遇到相同的複寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-159">It shows you when multiple domain controllers experience the same replication error.</span></span> <span data-ttu-id="569ef-160">在此情況下，您可以在一個網域控制站上探索或識別解決方案，然後在受到相同錯誤影響的其他網域控制站上重複執行。</span><span class="sxs-lookup"><span data-stu-id="569ef-160">In this case, you may be able to discover or identify a solution on one domain controller, then repeat it on other domain controllers affected by the same error.</span></span>

### <a name="tombstone-lifetime"></a><span data-ttu-id="569ef-161">標記存留期</span><span class="sxs-lookup"><span data-stu-id="569ef-161">Tombstone Lifetime</span></span>
<span data-ttu-id="569ef-162">標記存留期決定已刪除的物件 (稱為標記) 會保留在 Active Directory 資料庫中多久。</span><span class="sxs-lookup"><span data-stu-id="569ef-162">The tombstone lifetime determines how long a deleted object, referred to as a tombstone, is retained in the Active Directory database.</span></span> <span data-ttu-id="569ef-163">當已刪除的物件超過標記存留期時，記憶體回收程序會從 Active Directory 資料庫中自動將它移除。</span><span class="sxs-lookup"><span data-stu-id="569ef-163">When a deleted object passes the tombstone lifetime, a garbage collection process automatically removes it from the Active Directory database.</span></span>

<span data-ttu-id="569ef-164">對大多數最新版的 Windows 而言，預設標記存留期為 180 天，但是在較舊的版本上為 60 天，而 Active Directory 系統管理員可予以明確變更。</span><span class="sxs-lookup"><span data-stu-id="569ef-164">The default tombstone lifetime is 180 days for most recent versions of Windows, but it was 60 days on older versions, and it can be changed explicitly by an Active Directory administrator.</span></span>

<span data-ttu-id="569ef-165">請務必知道您是否有很接近或超過標記存留期的複寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-165">It's important to know if you're having replication errors that are approaching or are past the tombstone lifetime.</span></span> <span data-ttu-id="569ef-166">如果有兩個網域控制站遭遇存留超過標記存留期的複寫錯誤，即使此複寫錯誤已經修正，這兩個網域控制站之間的複寫還是會停用。</span><span class="sxs-lookup"><span data-stu-id="569ef-166">If two domain controllers experience a replication error that persists past the tombstone lifetime, replication is disabled between those two domain controllers, even if the underlying replication error is fixed.</span></span>

<span data-ttu-id="569ef-167">標記留存期區域可協助您找出可能停用的位置。</span><span class="sxs-lookup"><span data-stu-id="569ef-167">The Tombstone Lifetime area helps you identify places where disabled replication is in danger of happening.</span></span> <span data-ttu-id="569ef-168">[超過 100% TSL]  類別中的每個錯誤代表至少在樹系的標記存留期內，尚未在其來源與目的地伺服器之間複寫的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="569ef-168">Each error in the **Over 100% TSL** category represents a partition that has not replicated between its source and destination server for at least the tombstone lifetime for the forest.</span></span>

<span data-ttu-id="569ef-169">在此情況下，只修正複寫錯誤還不夠。</span><span class="sxs-lookup"><span data-stu-id="569ef-169">In this situation, simply fixing the replication error will not be enough.</span></span> <span data-ttu-id="569ef-170">您最少必須手動調查，先找出並清除停留物件，才可以重新開始複寫。</span><span class="sxs-lookup"><span data-stu-id="569ef-170">At a minimum, you need to manually investigate to identify and clean up lingering objects before you can restart replication.</span></span> <span data-ttu-id="569ef-171">您甚至可能需要解除委任網域控制站。</span><span class="sxs-lookup"><span data-stu-id="569ef-171">You may even need to decommission a domain controller.</span></span>

<span data-ttu-id="569ef-172">除了找出已存留超過標記存留期的複寫錯誤，您也要注意任何落入 **50-75% TSL** 或 **75-100% TSL** 類別的錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-172">In addition to identifying any replication errors that have persisted past the tombstone lifetime, you also want to pay attention to any errors falling into the **50-75% TSL** or **75-100% TSL** categories.</span></span>

<span data-ttu-id="569ef-173">這些是明顯滯留 (非暫時性) 的錯誤，因此可能需要您的介入才能解決。</span><span class="sxs-lookup"><span data-stu-id="569ef-173">These are errors that are clearly lingering, not transient, so they likely need your intervention to resolve.</span></span> <span data-ttu-id="569ef-174">好消息是它們尚未到達標記存留期。</span><span class="sxs-lookup"><span data-stu-id="569ef-174">The good news is that they have not yet reached the tombstone lifetime.</span></span> <span data-ttu-id="569ef-175">如果您立即修正這些問題，而在到達標記存留期之前  ，可以最少的手動介入來重新開始複寫。</span><span class="sxs-lookup"><span data-stu-id="569ef-175">If you fix these problems promptly and *before* they reach the tombstone lifetime, replication can restart with minimal manual intervention.</span></span>

<span data-ttu-id="569ef-176">如先前所述，AD 複寫狀態解決方案的儀表板圖格會顯示您環境中的「重大」  複寫錯誤數目，其定義為超過 75% 標記存留期的錯誤 (包括超過 100% TSL 的錯誤)。</span><span class="sxs-lookup"><span data-stu-id="569ef-176">As noted earlier, the dashboard tile for the AD Replication Status solution shows the number of *critical* replication errors in your environment, which is defined as errors that are over 75% of tombstone lifetime (including errors that are over 100% of TSL).</span></span> <span data-ttu-id="569ef-177">請努力讓此數字保持在 0。</span><span class="sxs-lookup"><span data-stu-id="569ef-177">Strive to keep this number at 0.</span></span>

> [!NOTE]
> <span data-ttu-id="569ef-178">所有標記存留期百分比計算都是以 Active Directory 樹系的實際標記存留期為基礎，所以即使您已設定自訂標記存留期值，仍可確信這些百分比是精確的。</span><span class="sxs-lookup"><span data-stu-id="569ef-178">All the tombstone lifetime percentage calculations are based on the actual tombstone lifetime for your Active Directory forest, so you can trust that those percentages are accurate, even if you have a custom tombstone lifetime value set.</span></span>
>
>

### <a name="ad-replication-status-details"></a><span data-ttu-id="569ef-179">AD 複寫狀態詳細資料</span><span class="sxs-lookup"><span data-stu-id="569ef-179">AD Replication status details</span></span>
<span data-ttu-id="569ef-180">當您按一下其中一份清單中的任何項目時，您會看到有關使用「記錄檔搜尋」的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="569ef-180">When you click any item in one of the lists, you see additional details about it using Log Search.</span></span> <span data-ttu-id="569ef-181">結果會經過篩選，僅顯示該項目的相關錯誤。</span><span class="sxs-lookup"><span data-stu-id="569ef-181">The results are filtered to show only the errors related to that item.</span></span> <span data-ttu-id="569ef-182">例如，如果您按一下列在 [目的地伺服器狀態 (ADDC02)] 之下的第一個網域控制站，您會看到搜尋結果已篩選成顯示將該網域控制站列為目的地伺服器的錯誤︰</span><span class="sxs-lookup"><span data-stu-id="569ef-182">For example, if you click on the first domain controller listed under **Destination Server Status (ADDC02)**, you see search results filtered to show errors with that domain controller listed as the destination server:</span></span>

![搜尋結果中的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

<span data-ttu-id="569ef-184">從這裡，您可以進一步篩選、修改搜尋查詢等。</span><span class="sxs-lookup"><span data-stu-id="569ef-184">From here, you can filter further, modify the search query, and so on.</span></span> <span data-ttu-id="569ef-185">如需使用記錄檔搜尋的詳細資訊，請參閱 [記錄檔搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="569ef-185">For more information about using the Log Search, see [Log searches](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="569ef-186">**HelpLink** 欄位會顯示 TechNet 頁面的 URL，其中包含該特定錯誤的其他詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="569ef-186">The **HelpLink** field shows the URL of a TechNet page with additional details about that specific error.</span></span> <span data-ttu-id="569ef-187">您可以將此連結複製並貼入瀏覽器視窗，以查看疑難排解和修正此錯誤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="569ef-187">You can copy and paste this link into your browser window to see information about troubleshooting and fixing the error.</span></span>

<span data-ttu-id="569ef-188">您也可以按一下 [匯出]  將結果匯出至 Excel。</span><span class="sxs-lookup"><span data-stu-id="569ef-188">You can also click **Export** to export the results to Excel.</span></span> <span data-ttu-id="569ef-189">匯出資料可以幫助您以任何想要的方式來視覺化複寫錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="569ef-189">Exporting the data can help you visualize replication error data in any way you'd like.</span></span>

![Excel 中匯出的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a><span data-ttu-id="569ef-191">AD 複寫狀態常見問題集</span><span class="sxs-lookup"><span data-stu-id="569ef-191">AD Replication Status FAQ</span></span>
<span data-ttu-id="569ef-192">**問︰多久更新一次 AD 複寫狀態資料？**</span><span class="sxs-lookup"><span data-stu-id="569ef-192">**Q: How often is AD replication status data updated?**</span></span>
<span data-ttu-id="569ef-193">答︰此資訊會每隔五天更新一次。</span><span class="sxs-lookup"><span data-stu-id="569ef-193">A: The information is updated every five days.</span></span>

<span data-ttu-id="569ef-194">**問：是否有設定此資料更新頻率的方法？**</span><span class="sxs-lookup"><span data-stu-id="569ef-194">**Q: Is there a way to configure how often this data is updated?**</span></span>
<span data-ttu-id="569ef-195">答：目前沒有。</span><span class="sxs-lookup"><span data-stu-id="569ef-195">A: Not at this time.</span></span>

<span data-ttu-id="569ef-196">**問︰我需要將所有的網域控制站加入至我的 OMS 工作區，才能查看複寫狀態嗎？**</span><span class="sxs-lookup"><span data-stu-id="569ef-196">**Q: Do I need to add all of my domain controllers to my OMS workspace in order to see replication status?**</span></span>
<span data-ttu-id="569ef-197">答︰否，只需加入單一網域控制站。</span><span class="sxs-lookup"><span data-stu-id="569ef-197">A: No, only a single domain controller must be added.</span></span> <span data-ttu-id="569ef-198">如果您的 OMS 工作區中有多個網域控制站，這些網域控制站的資料都會傳送至 OMS。</span><span class="sxs-lookup"><span data-stu-id="569ef-198">If you have multiple domain controllers in your OMS workspace, data from all of them is sent to OMS.</span></span>

<span data-ttu-id="569ef-199">**問︰我不想要將任何網域控制站新增至我的 OMS 工作區。仍可使用 AD 複寫狀態解決方案嗎？**</span><span class="sxs-lookup"><span data-stu-id="569ef-199">**Q: I don't want to add any domain controllers to my OMS workspace. Can I still use the AD Replication Status solution?**</span></span>
<span data-ttu-id="569ef-200">答： 會。</span><span class="sxs-lookup"><span data-stu-id="569ef-200">A: Yes.</span></span> <span data-ttu-id="569ef-201">您可以設定要啟用此解決方案的登錄機碼值。</span><span class="sxs-lookup"><span data-stu-id="569ef-201">You can set the value of a registry key to enable it.</span></span> <span data-ttu-id="569ef-202">請參閱[啟用非網域控制站以將 AD 資料傳送至 OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="569ef-202">See [To enable a non-domain controller to send AD data to OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

<span data-ttu-id="569ef-203">**問：負責收集資料之處理序的名稱為何？**</span><span class="sxs-lookup"><span data-stu-id="569ef-203">**Q: What is the name of the process that does the data collection?**</span></span>
<span data-ttu-id="569ef-204">答︰AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="569ef-204">A: AdvisorAssessment.exe</span></span>

<span data-ttu-id="569ef-205">**問：收集資料需要花費多少時間？**</span><span class="sxs-lookup"><span data-stu-id="569ef-205">**Q: How long does it take for data to be collected?**</span></span>
<span data-ttu-id="569ef-206">答︰資料收集時間取決於 Active Directory 環境的大小，但所需時間通常少於 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="569ef-206">A: Data collection time depends on the size of the Active Directory environment, but usually takes less than 15 minutes.</span></span>

<span data-ttu-id="569ef-207">**問：收集的資料類型為何？**</span><span class="sxs-lookup"><span data-stu-id="569ef-207">**Q: What type of data is collected?**</span></span>
<span data-ttu-id="569ef-208">答：複寫資訊是透過 LDAP 收集。</span><span class="sxs-lookup"><span data-stu-id="569ef-208">A: Replication information is collected via LDAP.</span></span>

<span data-ttu-id="569ef-209">**問：是否有設定資料收集時間的方法？**</span><span class="sxs-lookup"><span data-stu-id="569ef-209">**Q: Is there a way to configure when data is collected?**</span></span>
<span data-ttu-id="569ef-210">答：目前沒有。</span><span class="sxs-lookup"><span data-stu-id="569ef-210">A: Not at this time.</span></span>

<span data-ttu-id="569ef-211">**問︰我需要哪些權限才能收集資料？**</span><span class="sxs-lookup"><span data-stu-id="569ef-211">**Q: What permissions do I need to collect data?**</span></span>
<span data-ttu-id="569ef-212">答︰Active Directory 的一般使用者權限就足夠了。</span><span class="sxs-lookup"><span data-stu-id="569ef-212">A: Normal user permissions to Active Directory are sufficient.</span></span>

## <a name="troubleshoot-data-collection-problems"></a><span data-ttu-id="569ef-213">疑難排解資料收集問題</span><span class="sxs-lookup"><span data-stu-id="569ef-213">Troubleshoot data collection problems</span></span>
<span data-ttu-id="569ef-214">為了收集資料，AD 複寫狀態解決方案組件需要至少有一個網域控制站連接至您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="569ef-214">In order to collect data, the AD Replication Status solution pack requires at least one domain controller to be connected to your OMS workspace.</span></span> <span data-ttu-id="569ef-215">連接網域控制站後，會彈出訊息顯示**資料仍在收集中**。</span><span class="sxs-lookup"><span data-stu-id="569ef-215">Until you connect a domain controller, a message appears indicating that **data is still being collected**.</span></span>

<span data-ttu-id="569ef-216">如果您需要連接其中一個網域控制站的協助，您可以檢視 [將 Windows 電腦連接到 Log Analytics](log-analytics-windows-agents.md)文件。</span><span class="sxs-lookup"><span data-stu-id="569ef-216">If you need assistance connecting one of your domain controllers, you can view documentation at [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="569ef-217">或者，如果您的網域控制站已連接到現有的 System Center Operations Manager 環境，您可以檢視 [將 System Center Operations Manage 連接到 Log Analytics](log-analytics-om-agents.md)文件。</span><span class="sxs-lookup"><span data-stu-id="569ef-217">Alternatively, if your domain controller is already connected to an existing System Center Operations Manager environment, you can view documentation at [Connect System Center Operations Manager to Log Analytics](log-analytics-om-agents.md).</span></span>

<span data-ttu-id="569ef-218">如果您不想將任何網域控制站直接連接到 OMS 或 SCOM，請參閱 [啟用非網域控制站以將 AD 資料傳送至 OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。</span><span class="sxs-lookup"><span data-stu-id="569ef-218">If you don't want to connect any of your domain controllers directly to OMS or to SCOM, see [To enable a non-domain controller to send AD data to OMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="569ef-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="569ef-219">Next steps</span></span>
* <span data-ttu-id="569ef-220">使用 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md) 可檢視詳細的 Active Directory 複寫狀態資料。</span><span class="sxs-lookup"><span data-stu-id="569ef-220">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Active Directory Replication status data.</span></span>
