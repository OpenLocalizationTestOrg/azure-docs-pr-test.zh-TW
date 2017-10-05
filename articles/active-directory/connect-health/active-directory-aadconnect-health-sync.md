---
title: "使用 Azure AD Connect Health 進行同步處理 | Microsoft Docs"
description: "這是 Azure AD Connect Health 頁面，其中討論如何監視 Azure AD Connect 同步處理。"
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b06338cb62cc458e7b097db36023f0746d4e969
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="efe9f-103">使用 Azure AD Connect Health 監視 Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="efe9f-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="efe9f-104">下列文件適用於使用 Azure AD Connect Health 來監視 Azure AD Connect (同步處理)。</span><span class="sxs-lookup"><span data-stu-id="efe9f-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="efe9f-105">如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱 [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="efe9f-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="efe9f-106">此外，如需使用 Azure AD Connect Health 來監視 Active Directory 網域服務的詳細資訊，請參閱 [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。</span><span class="sxs-lookup"><span data-stu-id="efe9f-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="efe9f-108">適用於同步處理的 Azure AD Connect Health 警示</span><span class="sxs-lookup"><span data-stu-id="efe9f-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="efe9f-109">＜適用於同步處理的 Azure AD Connect Health 警示＞小節將為您提供作用中警示的清單。</span><span class="sxs-lookup"><span data-stu-id="efe9f-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span></span> <span data-ttu-id="efe9f-110">每個警示都包含相關資訊、解決步驟，以及相關文件的連結。</span><span class="sxs-lookup"><span data-stu-id="efe9f-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span></span> <span data-ttu-id="efe9f-111">選取作用中或已解決的警示，您將會看到一個包含額外資訊的新刀鋒視窗，以及解決警示可以採取的步驟，和其他文件的連結。</span><span class="sxs-lookup"><span data-stu-id="efe9f-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span></span> <span data-ttu-id="efe9f-112">您也可以檢視過去已解決的警示的歷史資料。</span><span class="sxs-lookup"><span data-stu-id="efe9f-112">You can also view historical data on alerts that were resolved in the past.</span></span>

<span data-ttu-id="efe9f-113">選取警示，將會為您提供其他資訊，以及解決警示可以採取的步驟，和其他文件的連結。</span><span class="sxs-lookup"><span data-stu-id="efe9f-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span></span>

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="efe9f-115">有限的警示評估</span><span class="sxs-lookup"><span data-stu-id="efe9f-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="efe9f-116">如果 Azure AD Connect 不使用預設組態 (比方說，如果 [屬性篩選] 從預設組態變更為自訂組態)，則 Azure AD Connect Health 代理程式不會上傳 Azure AD Connect 相關的錯誤事件。</span><span class="sxs-lookup"><span data-stu-id="efe9f-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span></span>

<span data-ttu-id="efe9f-117">這會限制服務的警示評估。</span><span class="sxs-lookup"><span data-stu-id="efe9f-117">This limits the evaluation of alerts by the service.</span></span> <span data-ttu-id="efe9f-118">您應會在 Azure 入口網站中您的服務之下，看到指出這種情況的橫幅。</span><span class="sxs-lookup"><span data-stu-id="efe9f-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="efe9f-120">您可以按一下 [設定] 並允許 Azure AD Connect Health 代理程式上傳所有的錯誤記錄檔，加以變更。</span><span class="sxs-lookup"><span data-stu-id="efe9f-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="efe9f-122">同步處理深入了解</span><span class="sxs-lookup"><span data-stu-id="efe9f-122">Sync Insight</span></span>
<span data-ttu-id="efe9f-123">系統管理員通常想要了解將變更同步至 Azure AD 所花的時間，以及所發生的變更數量。</span><span class="sxs-lookup"><span data-stu-id="efe9f-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span></span> <span data-ttu-id="efe9f-124">此功能使用下列圖形，輕鬆地呈現這項資訊：</span><span class="sxs-lookup"><span data-stu-id="efe9f-124">This feature provides an easy way to visualize this using the below graphs:</span></span>   

* <span data-ttu-id="efe9f-125">同步處理作業的延遲</span><span class="sxs-lookup"><span data-stu-id="efe9f-125">Latency of sync operations</span></span>
* <span data-ttu-id="efe9f-126">物件變更趨勢</span><span class="sxs-lookup"><span data-stu-id="efe9f-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="efe9f-127">同步處理延遲</span><span class="sxs-lookup"><span data-stu-id="efe9f-127">Sync Latency</span></span>
<span data-ttu-id="efe9f-128">這項功能提供連接器同步處理作業 (匯入、匯出等) 延遲的圖形化趨勢。</span><span class="sxs-lookup"><span data-stu-id="efe9f-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="efe9f-129">這提供快速且輕鬆的方式，讓您了解不僅僅作業的延遲 (如果您會發生大量變更也很好)，還提供一個方式來偵測延遲中可能需要進一步調查的異常行為。</span><span class="sxs-lookup"><span data-stu-id="efe9f-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span></span>

![同步處理延遲](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="efe9f-131">根據預設，只會顯示 Azure AD 連接器「匯出」作業的延遲。</span><span class="sxs-lookup"><span data-stu-id="efe9f-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span></span>  <span data-ttu-id="efe9f-132">若要查看連接器上的更多作業，或檢視其他連接器的作業，請以滑鼠右鍵按一下圖表，然後選取 [編輯圖表]，或按一下 [編輯延遲圖表] 按鈕，然後選擇特定作業和連接器。</span><span class="sxs-lookup"><span data-stu-id="efe9f-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="efe9f-133">同步處理物件的變更</span><span class="sxs-lookup"><span data-stu-id="efe9f-133">Sync Object Changes</span></span>
<span data-ttu-id="efe9f-134">這項功能提供正在評估並匯出至 Azure AD 的變更數的圖形化趨勢。</span><span class="sxs-lookup"><span data-stu-id="efe9f-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span></span>  <span data-ttu-id="efe9f-135">現在，嘗試從同步處理記錄檔收集此資訊並不容易。</span><span class="sxs-lookup"><span data-stu-id="efe9f-135">Today, trying to gather this information from the sync logs is difficult.</span></span>  <span data-ttu-id="efe9f-136">圖表不僅可讓您以更簡單的方式監視您的環境中發生的變更數，同時提供正在發生的失敗的視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="efe9f-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span></span>

![同步處理延遲](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="efe9f-138">物件層級同步處理錯誤報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="efe9f-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="efe9f-139">在 Windows Server AD 與 Azure AD 之間使用 Azure AD Connect 同步處理身分識別資料時，針對可能發生的同步處理錯誤，這項功能提供相關的報告。</span><span class="sxs-lookup"><span data-stu-id="efe9f-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="efe9f-140">此報告涵蓋同步處理用戶端所記錄的錯誤 (Azure AD Connect 1.1.281.0 版或更高版本)</span><span class="sxs-lookup"><span data-stu-id="efe9f-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="efe9f-141">它包含同步處理引擎上執行的最後一個同步處理作業所發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="efe9f-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span></span> <span data-ttu-id="efe9f-142">(Azure AD Connector 上的「匯出」)。</span><span class="sxs-lookup"><span data-stu-id="efe9f-142">("Export" on the Azure AD Connector.)</span></span>
* <span data-ttu-id="efe9f-143">用於同步處理的 Azure AD Connect Health 代理程式必須有指向所需端點的輸出連線，此報告才會包含最新的資料。</span><span class="sxs-lookup"><span data-stu-id="efe9f-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span></span>
* <span data-ttu-id="efe9f-144">此報告**每隔 30 分鐘更新一次**，使用的是用於同步處理的 Azure AD Connect Health 代理程式所上傳的資料。</span><span class="sxs-lookup"><span data-stu-id="efe9f-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync.</span></span>
  <span data-ttu-id="efe9f-145">它提供下列重要功能</span><span class="sxs-lookup"><span data-stu-id="efe9f-145">It provides the following key capabilities</span></span>

  * <span data-ttu-id="efe9f-146">錯誤分類</span><span class="sxs-lookup"><span data-stu-id="efe9f-146">Categorization of errors</span></span>
  * <span data-ttu-id="efe9f-147">依各類別之錯誤列出物件</span><span class="sxs-lookup"><span data-stu-id="efe9f-147">List of objects with error per category</span></span>
  * <span data-ttu-id="efe9f-148">集中記錄有關錯誤的所有資料</span><span class="sxs-lookup"><span data-stu-id="efe9f-148">All the data about the errors at one place</span></span>
  * <span data-ttu-id="efe9f-149">並排比較由於衝突而發生錯誤的物件</span><span class="sxs-lookup"><span data-stu-id="efe9f-149">Side by side comparison of Objects with error due to a conflict</span></span>
  * <span data-ttu-id="efe9f-150">將錯誤報告下載為 CVS (即將推出)</span><span class="sxs-lookup"><span data-stu-id="efe9f-150">Download the error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="efe9f-151">錯誤分類</span><span class="sxs-lookup"><span data-stu-id="efe9f-151">Categorization of Errors</span></span>
<span data-ttu-id="efe9f-152">此報告將現有的同步處理錯誤分成下列類別︰</span><span class="sxs-lookup"><span data-stu-id="efe9f-152">The report categorizes the existing synchronization errors in the following categories:</span></span>

| <span data-ttu-id="efe9f-153">類別</span><span class="sxs-lookup"><span data-stu-id="efe9f-153">Category</span></span> | <span data-ttu-id="efe9f-154">說明</span><span class="sxs-lookup"><span data-stu-id="efe9f-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efe9f-155">重複的屬性</span><span class="sxs-lookup"><span data-stu-id="efe9f-155">Duplicate Attribute</span></span> |<span data-ttu-id="efe9f-156">當 Azure AD Connect 嘗試在 Azure AD 中以一或多個重複的屬性值建立或更新物件時發生錯誤，這些屬性在租用戶中必須是唯一的，例如 proxyAddresses、UserPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="efe9f-156">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="efe9f-157">資料不符</span><span class="sxs-lookup"><span data-stu-id="efe9f-157">Data Mismatch</span></span> |<span data-ttu-id="efe9f-158">當大致相符無法比對物件時發生錯誤，導致同步處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="efe9f-158">Errors when the soft-match fails to match objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="efe9f-159">資料驗證失敗</span><span class="sxs-lookup"><span data-stu-id="efe9f-159">Data Validation Failure</span></span> |<span data-ttu-id="efe9f-160">由於無效資料而導致錯誤，例如重要屬性 (例如 UserPrincipalName) 中有不支援的字元；在寫入 Azure AD 之前未能通過驗證的格式錯誤。</span><span class="sxs-lookup"><span data-stu-id="efe9f-160">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="efe9f-161">大型屬性</span><span class="sxs-lookup"><span data-stu-id="efe9f-161">Large Attribute</span></span> |<span data-ttu-id="efe9f-162">當一或多個屬性大於允許的大小、長度或計數時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="efe9f-162">Errors when one or more attributes are larger than the allowed size, length or count.</span></span> |
| <span data-ttu-id="efe9f-163">其他</span><span class="sxs-lookup"><span data-stu-id="efe9f-163">Other</span></span> |<span data-ttu-id="efe9f-164">無法歸入上述類別的其他所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="efe9f-164">All other errors that don't fit in the above categories.</span></span> <span data-ttu-id="efe9f-165">根據意見，此類別將會進一步分成子類別。</span><span class="sxs-lookup"><span data-stu-id="efe9f-165">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="efe9f-166">![同步處理錯誤報告摘要](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![同步處理錯誤報告類別](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="efe9f-166">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="efe9f-167">依各類別之錯誤列出物件</span><span class="sxs-lookup"><span data-stu-id="efe9f-167">List of objects with error per category</span></span>
<span data-ttu-id="efe9f-168">深入每個類別將可找到所發生的錯誤歸入該類別的物件清單。</span><span class="sxs-lookup"><span data-stu-id="efe9f-168">Drilling into each category will provide the list of objects having the error in that category.</span></span>
<span data-ttu-id="efe9f-169">![同步處理錯誤報告清單](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="efe9f-169">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="efe9f-170">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="efe9f-170">Error Details</span></span>
<span data-ttu-id="efe9f-171">每個錯誤的詳細檢視中提供下列資料</span><span class="sxs-lookup"><span data-stu-id="efe9f-171">Following data is available in the detailed view for each error</span></span>

* <span data-ttu-id="efe9f-172">所涉及之「AD 物件」的識別項</span><span class="sxs-lookup"><span data-stu-id="efe9f-172">Identifiers for the *AD Object* involved</span></span>
* <span data-ttu-id="efe9f-173">所涉及之「Azure AD 物件」的識別項 (視情況)</span><span class="sxs-lookup"><span data-stu-id="efe9f-173">Identifiers for the *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="efe9f-174">錯誤描述及如何修正</span><span class="sxs-lookup"><span data-stu-id="efe9f-174">Error description and how to fix</span></span>
* <span data-ttu-id="efe9f-175">相關文章</span><span class="sxs-lookup"><span data-stu-id="efe9f-175">Related articles</span></span>

![同步處理錯誤報告詳細資料](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a><span data-ttu-id="efe9f-177">將錯誤報告下載為 CVS</span><span class="sxs-lookup"><span data-stu-id="efe9f-177">Download the error report as CSV</span></span>
<span data-ttu-id="efe9f-178">選取 [匯出] 按鈕，即可下載包含所有錯誤詳細資料的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="efe9f-178">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="efe9f-179">相關連結</span><span class="sxs-lookup"><span data-stu-id="efe9f-179">Related links</span></span>
* [<span data-ttu-id="efe9f-180">針對同步處理期間的錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="efe9f-180">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="efe9f-181">重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="efe9f-181">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="efe9f-182">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="efe9f-182">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="efe9f-183">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="efe9f-183">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="efe9f-184">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="efe9f-184">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="efe9f-185">使用 Azure AD Connect Health 來搭配 AD FS</span><span class="sxs-lookup"><span data-stu-id="efe9f-185">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="efe9f-186">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="efe9f-186">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="efe9f-187">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="efe9f-187">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="efe9f-188">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="efe9f-188">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)