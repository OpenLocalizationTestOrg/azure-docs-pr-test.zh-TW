---
title: "記錄分析中的金鑰保存庫方案 aaaAzure |Microsoft 文件"
description: "您可以在 Azure 金鑰保存庫所記錄的記錄分析 tooreview 使用 hello Azure 金鑰保存庫的方案。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="7bd84-103">Log Analytics 中的 Azure Key Vault 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="7bd84-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Key Vault 符號](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="7bd84-105">您可以在 Azure 金鑰保存庫 AuditEvent 記錄的記錄分析 tooreview 使用 hello Azure 金鑰保存庫的方案。</span><span class="sxs-lookup"><span data-stu-id="7bd84-105">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="7bd84-106">toouse hello 方案，您需要 tooenable 記錄 Azure 金鑰保存庫診斷和直接 hello 診斷 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="7bd84-106">toouse hello solution, you need tooenable logging of Azure Key Vault diagnostics and direct hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="7bd84-107">不需要 toowrite hello 記錄 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7bd84-107">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd84-108">在年 1 月 2017 hello 會支援從金鑰保存庫 tooLog 分析變更傳送記錄檔的方式。</span><span class="sxs-lookup"><span data-stu-id="7bd84-108">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="7bd84-109">如果您使用 hello 金鑰保存庫方案顯示*（已過時）* hello 標題中，請參閱太[從 hello 舊的金鑰保存庫方案移轉](#migrating-from-the-old-key-vault-solution)步驟中，您需要 toofollow。</span><span class="sxs-lookup"><span data-stu-id="7bd84-109">If hello Key Vault solution you are using shows *(deprecated)* in hello title, refer too[migrating from hello old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need toofollow.</span></span>
>
>

## <a name="install-and-configure-hello-solution"></a><span data-ttu-id="7bd84-110">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="7bd84-110">Install and configure hello solution</span></span>
<span data-ttu-id="7bd84-111">使用下列指示 tooinstall hello，並設定 hello Azure 金鑰保存庫方案：</span><span class="sxs-lookup"><span data-stu-id="7bd84-111">Use hello following instructions tooinstall and configure hello Azure Key Vault solution:</span></span>

1. <span data-ttu-id="7bd84-112">啟用從 hello Azure 金鑰保存庫解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="7bd84-112">Enable hello Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="7bd84-113">啟用診斷記錄的 hello 金鑰保存庫資源 toomonitor、 使用任一 hello[入口網站](#enable-key-vault-diagnostics-in-the-portal)或[PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="7bd84-113">Enable diagnostics logging for hello Key Vault resources toomonitor, using either hello [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a><span data-ttu-id="7bd84-114">金鑰保存庫中啟用診斷 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="7bd84-114">Enable Key Vault diagnostics in hello portal</span></span>

1. <span data-ttu-id="7bd84-115">在 hello Azure 入口網站，瀏覽 toohello 金鑰保存庫資源 toomonitor</span><span class="sxs-lookup"><span data-stu-id="7bd84-115">In hello Azure portal, navigate toohello Key Vault resource toomonitor</span></span>
2. <span data-ttu-id="7bd84-116">選取*診斷記錄檔*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="7bd84-116">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="7bd84-118">按一下*開啟診斷*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="7bd84-118">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="7bd84-120">診斷，tooturn 按一下*上*下*狀態*</span><span class="sxs-lookup"><span data-stu-id="7bd84-120">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="7bd84-121">按一下 [hello] 核取方塊*傳送 tooLog 分析*</span><span class="sxs-lookup"><span data-stu-id="7bd84-121">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="7bd84-122">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="7bd84-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="7bd84-123">tooenable *AuditEvent*記錄檔，在記錄檔下按一下 hello 核取方塊</span><span class="sxs-lookup"><span data-stu-id="7bd84-123">tooenable *AuditEvent* logs, click hello checkbox under Log</span></span>
8. <span data-ttu-id="7bd84-124">按一下*儲存*tooenable hello 記錄診斷 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="7bd84-124">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="7bd84-125">使用 PowerShell 啟用 Key Vault 診斷</span><span class="sxs-lookup"><span data-stu-id="7bd84-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="7bd84-126">下列 PowerShell 指令碼的 hello 提供的範例 toouse `Set-AzureRmDiagnosticSetting` tooenable 金鑰保存庫的診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="7bd84-126">hello following PowerShell script provides an example of how toouse `Set-AzureRmDiagnosticSetting` tooenable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="7bd84-127">檢閱 Azure 金鑰保存庫資料收集的詳細資料</span><span class="sxs-lookup"><span data-stu-id="7bd84-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="7bd84-128">Azure 金鑰保存庫方案會直接從 hello 金鑰保存庫中收集診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7bd84-128">Azure Key Vault solution collects diagnostics logs directly from hello Key Vault.</span></span>
<span data-ttu-id="7bd84-129">不必要的 toowrite hello 記錄 tooAzure Blob 儲存體，而且沒有代理程式需要的資料收集。</span><span class="sxs-lookup"><span data-stu-id="7bd84-129">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="7bd84-130">hello 下表顯示資料收集方法，以及如何針對 Azure 金鑰保存庫收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7bd84-130">hello following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="7bd84-131">平台</span><span class="sxs-lookup"><span data-stu-id="7bd84-131">Platform</span></span> | <span data-ttu-id="7bd84-132">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="7bd84-132">Direct agent</span></span> | <span data-ttu-id="7bd84-133">Systems Center Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="7bd84-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="7bd84-134">Azure</span><span class="sxs-lookup"><span data-stu-id="7bd84-134">Azure</span></span> | <span data-ttu-id="7bd84-135">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="7bd84-135">Operations Manager required?</span></span> | <span data-ttu-id="7bd84-136">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="7bd84-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="7bd84-137">收集頻率</span><span class="sxs-lookup"><span data-stu-id="7bd84-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="7bd84-138">Azure</span><span class="sxs-lookup"><span data-stu-id="7bd84-138">Azure</span></span> |  |  |<span data-ttu-id="7bd84-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="7bd84-139">&#8226;</span></span> |  |  | <span data-ttu-id="7bd84-140">與抵達同時</span><span class="sxs-lookup"><span data-stu-id="7bd84-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="7bd84-141">使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="7bd84-141">Use Azure Key Vault</span></span>
<span data-ttu-id="7bd84-142">之後您[hello 方案安裝](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)，hello，即可檢視 hello 金鑰保存庫資料**Azure 金鑰保存庫**磚從 hello**概觀**記錄分析的頁面。</span><span class="sxs-lookup"><span data-stu-id="7bd84-142">After you [install hello solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view hello Key Vault data by clicking hello **Azure Key Vault** tile from hello **Overview** page of Log Analytics.</span></span>

![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="7bd84-144">按一下 hello 之後**概觀**磚中，您可以檢視您的記錄檔，接著再深入的摘要中 toodetails hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="7bd84-144">After you click hello **Overview** tile, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="7bd84-145">經過一段時間的所有金鑰保存庫作業的數量</span><span class="sxs-lookup"><span data-stu-id="7bd84-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="7bd84-146">經過一段時間的失敗作業數量</span><span class="sxs-lookup"><span data-stu-id="7bd84-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="7bd84-147">依作業的平均作業延遲</span><span class="sxs-lookup"><span data-stu-id="7bd84-147">Average operational latency by operation</span></span>
* <span data-ttu-id="7bd84-148">Hello 1000 毫秒以上之作業數目與 1000 毫秒以上之作業的清單作業的服務品質</span><span class="sxs-lookup"><span data-stu-id="7bd84-148">Quality of service for operations with hello number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a><span data-ttu-id="7bd84-151">tooview 的任何作業的詳細資料</span><span class="sxs-lookup"><span data-stu-id="7bd84-151">tooview details for any operation</span></span>
1. <span data-ttu-id="7bd84-152">在 hello**概觀**頁面上，按一下 hello **Azure 金鑰保存庫**磚。</span><span class="sxs-lookup"><span data-stu-id="7bd84-152">On hello **Overview** page, click hello **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="7bd84-153">在 [hello **Azure 金鑰保存庫**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 的詳細資訊，請參閱 hello 記錄搜尋] 頁面中的資訊。</span><span class="sxs-lookup"><span data-stu-id="7bd84-153">On hello **Azure Key Vault** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information about it in hello log search page.</span></span>

    <span data-ttu-id="7bd84-154">在任何 hello 記錄搜尋 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="7bd84-154">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="7bd84-155">您也可以篩選由 facet toonarrow hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7bd84-155">You can also filter by facets toonarrow hello results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="7bd84-156">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="7bd84-156">Log Analytics records</span></span>
<span data-ttu-id="7bd84-157">hello Azure 金鑰保存庫方案會分析具有一種記錄**KeyVaults**從收集[AuditEvent 記錄](../key-vault/key-vault-logging.md)Azure 診斷內。</span><span class="sxs-lookup"><span data-stu-id="7bd84-157">hello Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="7bd84-158">這些記錄屬性會在下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7bd84-158">Properties for these records are in hello following table:</span></span>  

| <span data-ttu-id="7bd84-159">屬性</span><span class="sxs-lookup"><span data-stu-id="7bd84-159">Property</span></span> | <span data-ttu-id="7bd84-160">說明</span><span class="sxs-lookup"><span data-stu-id="7bd84-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7bd84-161">類型</span><span class="sxs-lookup"><span data-stu-id="7bd84-161">Type</span></span> |<span data-ttu-id="7bd84-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="7bd84-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="7bd84-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="7bd84-163">SourceSystem</span></span> |<span data-ttu-id="7bd84-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="7bd84-164">*Azure*</span></span> |
| <span data-ttu-id="7bd84-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="7bd84-165">CallerIpAddress</span></span> |<span data-ttu-id="7bd84-166">Hello 用戶端 hello 要求者 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7bd84-166">IP address of hello client who made hello request</span></span> |
| <span data-ttu-id="7bd84-167">類別</span><span class="sxs-lookup"><span data-stu-id="7bd84-167">Category</span></span> | <span data-ttu-id="7bd84-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="7bd84-168">*AuditEvent*</span></span> |
| <span data-ttu-id="7bd84-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7bd84-169">CorrelationId</span></span> |<span data-ttu-id="7bd84-170">選擇性的 GUID，hello 用戶端可以傳遞 toocorrelate 用戶端與服務端 （金鑰保存庫） 記錄檔的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7bd84-170">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="7bd84-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="7bd84-171">DurationMs</span></span> |<span data-ttu-id="7bd84-172">以毫秒為單位 tooservice hello REST API 要求所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="7bd84-172">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="7bd84-173">這次不包括網路延遲，讓您測量 hello 用戶端的 hello 時間可能不符合此時間。</span><span class="sxs-lookup"><span data-stu-id="7bd84-173">This time does not include network latency, so hello time that you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="7bd84-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="7bd84-174">httpStatusCode_d</span></span> |<span data-ttu-id="7bd84-175">Hello 要求所傳回的 HTTP 狀態碼 (例如， *200*)</span><span class="sxs-lookup"><span data-stu-id="7bd84-175">HTTP status code returned by hello request (for example, *200*)</span></span> |
| <span data-ttu-id="7bd84-176">id_s</span><span class="sxs-lookup"><span data-stu-id="7bd84-176">id_s</span></span> |<span data-ttu-id="7bd84-177">Hello 要求的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="7bd84-177">Unique ID of hello request</span></span> |
| <span data-ttu-id="7bd84-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="7bd84-178">identity_claim_appid_g</span></span> | <span data-ttu-id="7bd84-179">Hello 應用程式識別碼的 GUID</span><span class="sxs-lookup"><span data-stu-id="7bd84-179">GUID for hello application id</span></span> |
| <span data-ttu-id="7bd84-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="7bd84-180">OperationName</span></span> |<span data-ttu-id="7bd84-181">Hello 作業，如中所述的名稱[Azure 金鑰保存庫記錄](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="7bd84-181">Name of hello operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="7bd84-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="7bd84-182">OperationVersion</span></span> |<span data-ttu-id="7bd84-183">Hello 用戶端所要求的 REST API 版本 (例如*2015年-06-01*)</span><span class="sxs-lookup"><span data-stu-id="7bd84-183">REST API version requested by hello client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="7bd84-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="7bd84-184">requestUri_s</span></span> |<span data-ttu-id="7bd84-185">Hello 要求 Uri</span><span class="sxs-lookup"><span data-stu-id="7bd84-185">Uri of hello request</span></span> |
| <span data-ttu-id="7bd84-186">資源</span><span class="sxs-lookup"><span data-stu-id="7bd84-186">Resource</span></span> |<span data-ttu-id="7bd84-187">Hello 金鑰保存庫的名稱</span><span class="sxs-lookup"><span data-stu-id="7bd84-187">Name of hello key vault</span></span> |
| <span data-ttu-id="7bd84-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7bd84-188">ResourceGroup</span></span> |<span data-ttu-id="7bd84-189">Hello 金鑰保存庫的資源群組</span><span class="sxs-lookup"><span data-stu-id="7bd84-189">Resource group of hello key vault</span></span> |
| <span data-ttu-id="7bd84-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="7bd84-190">ResourceId</span></span> |<span data-ttu-id="7bd84-191">Azure 資源管理員資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="7bd84-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="7bd84-192">為金鑰保存庫的記錄檔，這是 hello 金鑰保存庫的資源 id。</span><span class="sxs-lookup"><span data-stu-id="7bd84-192">For Key Vault logs, this is hello Key Vault resource ID.</span></span> |
| <span data-ttu-id="7bd84-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="7bd84-193">ResourceProvider</span></span> |<span data-ttu-id="7bd84-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="7bd84-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="7bd84-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="7bd84-195">ResourceType</span></span> | <span data-ttu-id="7bd84-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="7bd84-196">*VAULTS*</span></span> |
| <span data-ttu-id="7bd84-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="7bd84-197">ResultSignature</span></span> |<span data-ttu-id="7bd84-198">HTTP 狀態 (例如 *OK*)</span><span class="sxs-lookup"><span data-stu-id="7bd84-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="7bd84-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="7bd84-199">ResultType</span></span> |<span data-ttu-id="7bd84-200">REST API 要求的結果 (例如 *Success*)</span><span class="sxs-lookup"><span data-stu-id="7bd84-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="7bd84-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="7bd84-201">SubscriptionId</span></span> |<span data-ttu-id="7bd84-202">Hello 包含 hello 金鑰保存庫的訂用帳戶的 azure 訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="7bd84-202">Azure subscription ID of hello subscription containing hello Key Vault</span></span> |

## <a name="migrating-from-hello-old-key-vault-solution"></a><span data-ttu-id="7bd84-203">從舊金鑰保存庫方案 hello 移轉</span><span class="sxs-lookup"><span data-stu-id="7bd84-203">Migrating from hello old Key Vault solution</span></span>
<span data-ttu-id="7bd84-204">在年 1 月 2017 hello 會支援從金鑰保存庫 tooLog 分析變更傳送記錄檔的方式。</span><span class="sxs-lookup"><span data-stu-id="7bd84-204">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="7bd84-205">這些變更會提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7bd84-205">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="7bd84-206">記錄檔寫入直接 tooLog 分析 hello 不需要 toouse 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7bd84-206">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="7bd84-207">從記錄檔時的 hello 時間延遲越少產生 toothem 可以使用這個記錄分析</span><span class="sxs-lookup"><span data-stu-id="7bd84-207">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="7bd84-208">較少的組態步驟</span><span class="sxs-lookup"><span data-stu-id="7bd84-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="7bd84-209">所有 Azure 診斷類型的通用格式</span><span class="sxs-lookup"><span data-stu-id="7bd84-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="7bd84-210">toouse hello 更新方案：</span><span class="sxs-lookup"><span data-stu-id="7bd84-210">toouse hello updated solution:</span></span>

1. [<span data-ttu-id="7bd84-211">設定診斷 toobe 從金鑰保存庫直接傳送 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="7bd84-211">Configure diagnostics toobe sent directly tooLog Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="7bd84-212">啟用使用 hello 程序中所述的 hello Azure 金鑰保存庫解決方案[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="7bd84-212">Enable hello Azure Key Vault solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="7bd84-213">更新任何已儲存的查詢、 儀表板或警示 toouse hello 新的資料類型</span><span class="sxs-lookup"><span data-stu-id="7bd84-213">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="7bd84-214">型別是來自變更： KeyVaults tooAzureDiagnostics。</span><span class="sxs-lookup"><span data-stu-id="7bd84-214">Type is change from: KeyVaults tooAzureDiagnostics.</span></span> <span data-ttu-id="7bd84-215">您可以使用 hello ResourceType toofilter tooKey 保存庫的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7bd84-215">You can use hello ResourceType toofilter tooKey Vault Logs.</span></span>
  - <span data-ttu-id="7bd84-216">與其使用 `Type=KeyVaults`，請改用 `Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="7bd84-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="7bd84-217">欄位：(欄位名稱區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="7bd84-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="7bd84-218">如有後置字元的任何欄位\_s， \_d 或\_g hello 名稱，變更 hello 第一個字元 toolower 案例中</span><span class="sxs-lookup"><span data-stu-id="7bd84-218">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
  - <span data-ttu-id="7bd84-219">如有後的置字元的任何欄位\_o 在 [名稱] hello 資料會分成根據 hello 巢狀欄位名稱的個別欄位。</span><span class="sxs-lookup"><span data-stu-id="7bd84-219">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span> <span data-ttu-id="7bd84-220">例如，hello hello 呼叫端的 UPN 會儲存在欄位`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="7bd84-220">For example, hello UPN of hello caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="7bd84-221">變更欄位 CallerIpAddress tooCallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="7bd84-221">Field CallerIpAddress changed tooCallerIPAddress</span></span>
   - <span data-ttu-id="7bd84-222">欄位 RemoteIPCountry 已不存在</span><span class="sxs-lookup"><span data-stu-id="7bd84-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="7bd84-223">移除 hello*金鑰保存庫分析 （已過時）*方案。</span><span class="sxs-lookup"><span data-stu-id="7bd84-223">Remove hello *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="7bd84-224">如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="7bd84-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="7bd84-225">Hello 新方案中看不到 hello 變更之前，收集資料。</span><span class="sxs-lookup"><span data-stu-id="7bd84-225">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="7bd84-226">您可以繼續 tooquery，針對使用此資料 hello 舊的類型和欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="7bd84-226">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7bd84-227">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7bd84-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="7bd84-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7bd84-228">Next steps</span></span>
* <span data-ttu-id="7bd84-229">使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Azure 金鑰保存庫的資料。</span><span class="sxs-lookup"><span data-stu-id="7bd84-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure Key Vault data.</span></span>
