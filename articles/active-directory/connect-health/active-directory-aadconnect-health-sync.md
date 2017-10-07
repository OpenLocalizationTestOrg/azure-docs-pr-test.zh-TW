---
title: "與同步處理的 Azure AD Connect Health aaaUsing |Microsoft 文件"
description: "這是將討論如何 toomonitor Azure AD Connect 同步處理的 hello Azure AD Connect Health 頁面。"
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
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="a34b5-103">使用 Azure AD Connect Health 監視 Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="a34b5-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="a34b5-104">下列文件的 hello 是特定 toomonitoring Azure AD Connect （同步） 與 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="a34b5-104">hello following documentation is specific toomonitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="a34b5-105">如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱 [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="a34b5-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="a34b5-106">此外，如需使用 Azure AD Connect Health 來監視 Active Directory 網域服務的詳細資訊，請參閱 [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。</span><span class="sxs-lookup"><span data-stu-id="a34b5-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="a34b5-108">適用於同步處理的 Azure AD Connect Health 警示</span><span class="sxs-lookup"><span data-stu-id="a34b5-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="a34b5-109">同步處理區段 hello Azure AD Connect Health 警示會提供 hello 的作用中警示清單。</span><span class="sxs-lookup"><span data-stu-id="a34b5-109">hello Azure AD Connect Health Alerts for sync section provides you hello list of active alerts.</span></span> <span data-ttu-id="a34b5-110">每個警示都包含相關資訊、 解決步驟和連結 toorelated 文件。</span><span class="sxs-lookup"><span data-stu-id="a34b5-110">Each alert includes relevant information, resolution steps, and links toorelated documentation.</span></span> <span data-ttu-id="a34b5-111">藉由選取作用中或已解決的警示，您會看到新的刀鋒視窗的詳細資訊，請為 tooresolve hello 警示及連結 tooadditional 文件，您可以採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="a34b5-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take tooresolve hello alert, and links tooadditional documentation.</span></span> <span data-ttu-id="a34b5-112">您也可以在 hello 過去已解決的警示檢視歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a34b5-112">You can also view historical data on alerts that were resolved in hello past.</span></span>

<span data-ttu-id="a34b5-113">只要選取的警示的其他資訊以及步驟會提供您可以採取 tooresolve hello 警示和連結 tooadditional 文件。</span><span class="sxs-lookup"><span data-stu-id="a34b5-113">By selecting an alert you will be provided with additional information as well as steps you can take tooresolve hello alert and links tooadditional documentation.</span></span>

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="a34b5-115">有限的警示評估</span><span class="sxs-lookup"><span data-stu-id="a34b5-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="a34b5-116">如果 Azure AD Connect 不使用 hello 預設組態 （例如，如果屬性篩選從 hello 預設組態 tooa 自訂組態變更），然後 hello Azure AD Connect Health 代理程式將不會上傳 hello 錯誤事件相關的 tooAzureAD Connect。</span><span class="sxs-lookup"><span data-stu-id="a34b5-116">If Azure AD Connect is NOT using hello default configuration (for example, if Attribute Filtering is changed from hello default configuration tooa custom configuration), then hello Azure AD Connect Health agent will not upload hello error events related tooAzure AD Connect.</span></span>

<span data-ttu-id="a34b5-117">這會由 hello 服務限制 hello 評估的警示。</span><span class="sxs-lookup"><span data-stu-id="a34b5-117">This limits hello evaluation of alerts by hello service.</span></span> <span data-ttu-id="a34b5-118">您會看到將橫幅指出此情況下您的服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a34b5-118">You'd will see a banner that indicates this condition in hello Azure Portal under your service.</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="a34b5-120">您可以透過按一下 [設定]，並允許 Azure AD Connect Health 代理程式 tooupload 所有的錯誤記錄檔來變更這個設定。</span><span class="sxs-lookup"><span data-stu-id="a34b5-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent tooupload all error logs.</span></span>

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="a34b5-122">同步處理深入了解</span><span class="sxs-lookup"><span data-stu-id="a34b5-122">Sync Insight</span></span>
<span data-ttu-id="a34b5-123">需要系統管理員頻繁地 tooknow hello toosync 變更 tooAzure AD 和變更正在進行中的 hello 數量所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="a34b5-123">Admins Frequently want tooknow about hello time it takes toosync changes tooAzure AD and hello amount of changes taking place.</span></span> <span data-ttu-id="a34b5-124">這項功能提供簡單的方式 toovisualize 此使用圖形下方的 hello:</span><span class="sxs-lookup"><span data-stu-id="a34b5-124">This feature provides an easy way toovisualize this using hello below graphs:</span></span>   

* <span data-ttu-id="a34b5-125">同步處理作業的延遲</span><span class="sxs-lookup"><span data-stu-id="a34b5-125">Latency of sync operations</span></span>
* <span data-ttu-id="a34b5-126">物件變更趨勢</span><span class="sxs-lookup"><span data-stu-id="a34b5-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="a34b5-127">同步處理延遲</span><span class="sxs-lookup"><span data-stu-id="a34b5-127">Sync Latency</span></span>
<span data-ttu-id="a34b5-128">這項功能提供的圖形化趨勢 hello 同步處理作業 （匯入、 匯出、 等等） 的連接器的延遲。</span><span class="sxs-lookup"><span data-stu-id="a34b5-128">This feature provides a graphical trend of latency of hello sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="a34b5-129">這可提供快速並輕鬆 toounderstand 不僅 hello 可能需要進一步調查的 hello 延遲，您的作業 （如果有發生變更的大型集合，此項會較大），但方式 toodetect 異常的延遲。</span><span class="sxs-lookup"><span data-stu-id="a34b5-129">This provides a quick and easy way toounderstand not only hello latency of your operations (larger if you have a large set of changes occurring) but also a way toodetect anomalies in hello latency that may require further investigation.</span></span>

![同步處理延遲](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="a34b5-131">根據預設，會顯示只有 hello 的 hello Azure AD 連接器 hello 'Export' 作業的延遲。</span><span class="sxs-lookup"><span data-stu-id="a34b5-131">By default, only hello latency of hello 'Export' operation for hello Azure AD connector is shown.</span></span>  <span data-ttu-id="a34b5-132">toosee hello 連接器上的多個作業或 tooview 作業，從其他連接器，以滑鼠右鍵按一下在 hello 圖上，選取 編輯圖表或 hello 」 編輯延遲圖表 」 按鈕上按一下，然後選擇 hello 特定作業和連接器。</span><span class="sxs-lookup"><span data-stu-id="a34b5-132">toosee more operations on hello connector or tooview operations from other connectors, right-click on hello chart,  select Edit Chart or click on hello "Edit Latency Chart" button and choose hello specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="a34b5-133">同步處理物件的變更</span><span class="sxs-lookup"><span data-stu-id="a34b5-133">Sync Object Changes</span></span>
<span data-ttu-id="a34b5-134">這項功能提供的圖形化 hello 數的變更，會在評估並匯出 tooAzure AD 趨勢。</span><span class="sxs-lookup"><span data-stu-id="a34b5-134">This feature provides a graphical trend of hello number of changes that are being evaluated and exported tooAzure AD.</span></span>  <span data-ttu-id="a34b5-135">今天，嘗試 toogather hello 同步處理記錄檔的這項資訊是很困難。</span><span class="sxs-lookup"><span data-stu-id="a34b5-135">Today, trying toogather this information from hello sync logs is difficult.</span></span>  <span data-ttu-id="a34b5-136">hello 圖表可讓您，不但更簡單的方式監視 hello 數目會在您的環境中進行的變更，但 hello 失敗所發生的視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="a34b5-136">hello chart gives you, not only a simpler way of monitoring hello number of changes that are occurring in your environment, but also a visual view of hello failures that are occurring.</span></span>

![同步處理延遲](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="a34b5-138">物件層級同步處理錯誤報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a34b5-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="a34b5-139">在 Windows Server AD 與 Azure AD 之間使用 Azure AD Connect 同步處理身分識別資料時，針對可能發生的同步處理錯誤，這項功能提供相關的報告。</span><span class="sxs-lookup"><span data-stu-id="a34b5-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="a34b5-140">hello 報表涵蓋 hello 同步用戶端所記錄的錯誤 (Azure AD Connect 1.1.281.0 版或更高版本)</span><span class="sxs-lookup"><span data-stu-id="a34b5-140">hello report covers errors recorded by hello sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="a34b5-141">Hello 上次同步處理作業 hello 同步處理引擎中包含 hello 發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a34b5-141">It includes hello errors that occurred in hello last synchronization operation on hello sync engine.</span></span> <span data-ttu-id="a34b5-142">（「 匯出 」 上 hello Azure AD 連接器。）</span><span class="sxs-lookup"><span data-stu-id="a34b5-142">("Export" on hello Azure AD Connector.)</span></span>
* <span data-ttu-id="a34b5-143">Azure AD Connect Health 代理程式進行同步必須 hello 報表 tooinclude hello 最新資料的傳出連線所需的 toohello 結束點。</span><span class="sxs-lookup"><span data-stu-id="a34b5-143">Azure AD Connect Health agent for sync must have outbound connectivity toohello required end points for hello report tooinclude hello latest data.</span></span>
* <span data-ttu-id="a34b5-144">hello 報表是**更新之後每隔 30 分鐘**使用 hello 資料上傳由 Azure AD Connect Health 代理程式進行同步。它提供下列重要功能的 hello</span><span class="sxs-lookup"><span data-stu-id="a34b5-144">hello report is **updated after every 30 minutes** using hello data uploaded by Azure AD Connect Health agent for sync. It provides hello following key capabilities</span></span>

  * <span data-ttu-id="a34b5-145">錯誤分類</span><span class="sxs-lookup"><span data-stu-id="a34b5-145">Categorization of errors</span></span>
  * <span data-ttu-id="a34b5-146">依各類別之錯誤列出物件</span><span class="sxs-lookup"><span data-stu-id="a34b5-146">List of objects with error per category</span></span>
  * <span data-ttu-id="a34b5-147">所有 hello hello 錯誤，在某個位置的相關資料</span><span class="sxs-lookup"><span data-stu-id="a34b5-147">All hello data about hello errors at one place</span></span>
  * <span data-ttu-id="a34b5-148">並排比較的物件，因為 tooa 衝突錯誤</span><span class="sxs-lookup"><span data-stu-id="a34b5-148">Side by side comparison of Objects with error due tooa conflict</span></span>
  * <span data-ttu-id="a34b5-149">Hello 錯誤報表下載為 CSV，（即將推出）</span><span class="sxs-lookup"><span data-stu-id="a34b5-149">Download hello error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="a34b5-150">錯誤分類</span><span class="sxs-lookup"><span data-stu-id="a34b5-150">Categorization of Errors</span></span>
<span data-ttu-id="a34b5-151">hello 報表來分類 hello 現有同步處理中的錯誤 hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="a34b5-151">hello report categorizes hello existing synchronization errors in hello following categories:</span></span>

| <span data-ttu-id="a34b5-152">類別</span><span class="sxs-lookup"><span data-stu-id="a34b5-152">Category</span></span> | <span data-ttu-id="a34b5-153">說明</span><span class="sxs-lookup"><span data-stu-id="a34b5-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a34b5-154">重複的屬性</span><span class="sxs-lookup"><span data-stu-id="a34b5-154">Duplicate Attribute</span></span> |<span data-ttu-id="a34b5-155">當 Azure AD Connect 嘗試在 Azure AD 中以一或多個重複的屬性值建立或更新物件時發生錯誤，這些屬性在租用戶中必須是唯一的，例如 proxyAddresses、UserPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="a34b5-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="a34b5-156">資料不符</span><span class="sxs-lookup"><span data-stu-id="a34b5-156">Data Mismatch</span></span> |<span data-ttu-id="a34b5-157">Hello 軟比對失敗會導致同步處理錯誤的 toomatch 物件時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a34b5-157">Errors when hello soft-match fails toomatch objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="a34b5-158">資料驗證失敗</span><span class="sxs-lookup"><span data-stu-id="a34b5-158">Data Validation Failure</span></span> |<span data-ttu-id="a34b5-159">錯誤，因為 tooinvalid 資料，例如在重要的屬性，例如 UserPrincipalName，不支援的字元格式化之前寫入在 Azure AD 中驗證失敗的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a34b5-159">Errors due tooinvalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="a34b5-160">大型屬性</span><span class="sxs-lookup"><span data-stu-id="a34b5-160">Large Attribute</span></span> |<span data-ttu-id="a34b5-161">當一或多個屬性都是大於 hello 錯誤允許大小、 長度或計數。</span><span class="sxs-lookup"><span data-stu-id="a34b5-161">Errors when one or more attributes are larger than hello allowed size, length or count.</span></span> |
| <span data-ttu-id="a34b5-162">其他</span><span class="sxs-lookup"><span data-stu-id="a34b5-162">Other</span></span> |<span data-ttu-id="a34b5-163">所有其他錯誤無法容納的 hello 上方類別目錄。</span><span class="sxs-lookup"><span data-stu-id="a34b5-163">All other errors that don't fit in hello above categories.</span></span> <span data-ttu-id="a34b5-164">根據意見，此類別將會進一步分成子類別。</span><span class="sxs-lookup"><span data-stu-id="a34b5-164">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="a34b5-165">![同步處理錯誤報告摘要](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![同步處理錯誤報告類別](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="a34b5-165">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="a34b5-166">依各類別之錯誤列出物件</span><span class="sxs-lookup"><span data-stu-id="a34b5-166">List of objects with error per category</span></span>
<span data-ttu-id="a34b5-167">鑽研至每個類別會提供物件都有 hello 錯誤類別目錄中的 hello 的清單。</span><span class="sxs-lookup"><span data-stu-id="a34b5-167">Drilling into each category will provide hello list of objects having hello error in that category.</span></span>
<span data-ttu-id="a34b5-168">![同步處理錯誤報告清單](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="a34b5-168">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="a34b5-169">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="a34b5-169">Error Details</span></span>
<span data-ttu-id="a34b5-170">下列資料位於 hello 詳細檢視每個錯誤</span><span class="sxs-lookup"><span data-stu-id="a34b5-170">Following data is available in hello detailed view for each error</span></span>

* <span data-ttu-id="a34b5-171">識別項的 hello *AD 物件*涉及</span><span class="sxs-lookup"><span data-stu-id="a34b5-171">Identifiers for hello *AD Object* involved</span></span>
* <span data-ttu-id="a34b5-172">識別項的 hello *Azure AD 物件*涉及 （視情況）</span><span class="sxs-lookup"><span data-stu-id="a34b5-172">Identifiers for hello *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="a34b5-173">錯誤描述以及 toofix</span><span class="sxs-lookup"><span data-stu-id="a34b5-173">Error description and how toofix</span></span>
* <span data-ttu-id="a34b5-174">相關文章</span><span class="sxs-lookup"><span data-stu-id="a34b5-174">Related articles</span></span>

![同步處理錯誤報告詳細資料](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a><span data-ttu-id="a34b5-176">Hello 錯誤報表下載為 CSV</span><span class="sxs-lookup"><span data-stu-id="a34b5-176">Download hello error report as CSV</span></span>
<span data-ttu-id="a34b5-177">藉由選取 hello 「 匯出 」 按鈕，您可以下載所有 hello 錯誤相關的所有 hello 詳細資料的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="a34b5-177">By selecting hello "Export" button you can download a CSV file with all hello details about all hello errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="a34b5-178">相關連結</span><span class="sxs-lookup"><span data-stu-id="a34b5-178">Related links</span></span>
* [<span data-ttu-id="a34b5-179">針對同步處理期間的錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a34b5-179">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="a34b5-180">重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="a34b5-180">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="a34b5-181">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="a34b5-181">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="a34b5-182">Azure AD Connect Health 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="a34b5-182">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="a34b5-183">Azure AD Connect Health 操作</span><span class="sxs-lookup"><span data-stu-id="a34b5-183">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="a34b5-184">使用 Azure AD Connect Health 來搭配 AD FS</span><span class="sxs-lookup"><span data-stu-id="a34b5-184">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="a34b5-185">在 AD DS 使用 Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="a34b5-185">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="a34b5-186">Azure AD Connect Health 常見問題集</span><span class="sxs-lookup"><span data-stu-id="a34b5-186">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="a34b5-187">Azure AD Connect Health 版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="a34b5-187">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)