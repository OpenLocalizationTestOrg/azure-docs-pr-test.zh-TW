---
title: "Log Analytics 中的 Azure 金鑰保存庫解決方案 | Microsoft Docs"
description: "您可以使用 Log Analytics 中的 Azure 金鑰保存庫解決方案來檢閱 Azure 金鑰保存庫記錄檔。"
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
ms.openlocfilehash: 651586e0846ffb22a23e64b73c2cc614980d9b92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="12f1a-103">Log Analytics 中的 Azure Key Vault 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="12f1a-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Key Vault 符號](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="12f1a-105">您可以使用 Log Analytics 中的 Azure 金鑰保存庫解決方案來檢閱 Azure 金鑰保存庫 AuditEvent 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="12f1a-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="12f1a-106">若要使用此解決方案，您需要啟用 Azure Key Vault 診斷的記錄，並將診斷導向至 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="12f1a-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="12f1a-107">不需要將記錄寫入 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="12f1a-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="12f1a-108">從 2017 年 1 月開始，從 Key Vault 傳送記錄到 Log Analytics 的支援方式已變更。</span><span class="sxs-lookup"><span data-stu-id="12f1a-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="12f1a-109">如果您使用的 Key Vault 解決方案標題中顯示 *(已過時)*，請參閱[從舊的 Key Vault 解決方案進行移轉](#migrating-from-the-old-key-vault-solution)，以取得您必須遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="12f1a-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="12f1a-110">安裝和設定解決方案</span><span class="sxs-lookup"><span data-stu-id="12f1a-110">Install and configure the solution</span></span>
<span data-ttu-id="12f1a-111">使用下列指示來安裝和設定 Azure 金鑰保存庫解決方案︰</span><span class="sxs-lookup"><span data-stu-id="12f1a-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="12f1a-112">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Azure Key Vault 解決方案。</span><span class="sxs-lookup"><span data-stu-id="12f1a-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="12f1a-113">使用[入口網站](#enable-key-vault-diagnostics-in-the-portal)或 [PowerShell](#enable-key-vault-diagnostics-using-powershell)，針對要監視的 Key Vault 資源啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="12f1a-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="12f1a-114">在入口網站中啟用 Key Vault 診斷</span><span class="sxs-lookup"><span data-stu-id="12f1a-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="12f1a-115">在 Azure 入口網站中，瀏覽至要監視的 Key Vault 資源</span><span class="sxs-lookup"><span data-stu-id="12f1a-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="12f1a-116">選取 [診斷記錄] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="12f1a-116">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="12f1a-118">按一下 [開啟診斷] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="12f1a-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="12f1a-120">若要開啟診斷，請按一下 [狀態] 下的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="12f1a-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="12f1a-121">按一下 [傳送到 Log Analytics] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="12f1a-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="12f1a-122">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="12f1a-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="12f1a-123">若要啟用 *AuditEvent* 記錄，請按一下 [記錄] 下的核取方塊</span><span class="sxs-lookup"><span data-stu-id="12f1a-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="12f1a-124">按一下 [儲存] 以啟用 Log Analytics 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="12f1a-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="12f1a-125">使用 PowerShell 啟用 Key Vault 診斷</span><span class="sxs-lookup"><span data-stu-id="12f1a-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="12f1a-126">下列 PowerShell 指令碼示範如何使用 `Set-AzureRmDiagnosticSetting` 啟用 Key Vault 的診斷記錄︰</span><span class="sxs-lookup"><span data-stu-id="12f1a-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="12f1a-127">檢閱 Azure 金鑰保存庫資料收集的詳細資料</span><span class="sxs-lookup"><span data-stu-id="12f1a-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="12f1a-128">Azure Key Vault 解決方案會直接從 Key Vault 收集診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="12f1a-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="12f1a-129">不需要將記錄寫入 Azure Blob 儲存體，也不需要代理程式來收集資料。</span><span class="sxs-lookup"><span data-stu-id="12f1a-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="12f1a-130">下表顯示 Azure 金鑰保存庫的資料收集方法及如何收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12f1a-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="12f1a-131">平台</span><span class="sxs-lookup"><span data-stu-id="12f1a-131">Platform</span></span> | <span data-ttu-id="12f1a-132">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="12f1a-132">Direct agent</span></span> | <span data-ttu-id="12f1a-133">Systems Center Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="12f1a-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="12f1a-134">Azure</span><span class="sxs-lookup"><span data-stu-id="12f1a-134">Azure</span></span> | <span data-ttu-id="12f1a-135">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="12f1a-135">Operations Manager required?</span></span> | <span data-ttu-id="12f1a-136">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="12f1a-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="12f1a-137">收集頻率</span><span class="sxs-lookup"><span data-stu-id="12f1a-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="12f1a-138">Azure</span><span class="sxs-lookup"><span data-stu-id="12f1a-138">Azure</span></span> |  |  |<span data-ttu-id="12f1a-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="12f1a-139">&#8226;</span></span> |  |  | <span data-ttu-id="12f1a-140">與抵達同時</span><span class="sxs-lookup"><span data-stu-id="12f1a-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="12f1a-141">使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="12f1a-141">Use Azure Key Vault</span></span>
<span data-ttu-id="12f1a-142">在您[安裝解決方案](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)之後，按一下 Log Analytics [概觀] 頁面的 [Azure Key Vault] 圖格來檢視金鑰保存庫資料。</span><span class="sxs-lookup"><span data-stu-id="12f1a-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="12f1a-144">按一下 [概觀] 圖格之後，您可以檢視記錄檔的摘要，然後深入下列類別的詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="12f1a-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="12f1a-145">經過一段時間的所有金鑰保存庫作業的數量</span><span class="sxs-lookup"><span data-stu-id="12f1a-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="12f1a-146">經過一段時間的失敗作業數量</span><span class="sxs-lookup"><span data-stu-id="12f1a-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="12f1a-147">依作業的平均作業延遲</span><span class="sxs-lookup"><span data-stu-id="12f1a-147">Average operational latency by operation</span></span>
* <span data-ttu-id="12f1a-148">作業的服務品質，顯示花費超過 1000 毫秒的作業數目及花費超過 1000 毫秒的作業清單</span><span class="sxs-lookup"><span data-stu-id="12f1a-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="12f1a-151">檢視任何作業的詳細資料</span><span class="sxs-lookup"><span data-stu-id="12f1a-151">To view details for any operation</span></span>
1. <span data-ttu-id="12f1a-152">在 [概觀] 頁面上，按一下 [Azure 金鑰保存庫] 圖格。</span><span class="sxs-lookup"><span data-stu-id="12f1a-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="12f1a-153">在 [Azure 金鑰保存庫] 儀表板上，檢閱其中一個刀鋒視窗中的摘要資訊，然後按一下其中一個，在記錄搜尋頁面中檢視詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="12f1a-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="12f1a-154">您可以在任何 [記錄搜尋] 頁面上，按時間、詳細結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="12f1a-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="12f1a-155">您也可以按 Facet 篩選以縮減結果。</span><span class="sxs-lookup"><span data-stu-id="12f1a-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="12f1a-156">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="12f1a-156">Log Analytics records</span></span>
<span data-ttu-id="12f1a-157">Azure 金鑰保存庫解決方案會分析從 Azure 診斷的 [AuditEvent 記錄檔](../key-vault/key-vault-logging.md)收集的 **KeyVaults** 類型記錄。</span><span class="sxs-lookup"><span data-stu-id="12f1a-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="12f1a-158">下表是這些記錄的屬性：</span><span class="sxs-lookup"><span data-stu-id="12f1a-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="12f1a-159">屬性</span><span class="sxs-lookup"><span data-stu-id="12f1a-159">Property</span></span> | <span data-ttu-id="12f1a-160">說明</span><span class="sxs-lookup"><span data-stu-id="12f1a-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="12f1a-161">類型</span><span class="sxs-lookup"><span data-stu-id="12f1a-161">Type</span></span> |<span data-ttu-id="12f1a-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="12f1a-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="12f1a-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="12f1a-163">SourceSystem</span></span> |<span data-ttu-id="12f1a-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="12f1a-164">*Azure*</span></span> |
| <span data-ttu-id="12f1a-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="12f1a-165">CallerIpAddress</span></span> |<span data-ttu-id="12f1a-166">提出要求之用戶端的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="12f1a-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="12f1a-167">類別</span><span class="sxs-lookup"><span data-stu-id="12f1a-167">Category</span></span> | <span data-ttu-id="12f1a-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="12f1a-168">*AuditEvent*</span></span> |
| <span data-ttu-id="12f1a-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="12f1a-169">CorrelationId</span></span> |<span data-ttu-id="12f1a-170">選擇性的 GUID，用戶端可傳遞此 GUID 來讓用戶端記錄與服務端 (金鑰保存庫) 記錄相互關聯。</span><span class="sxs-lookup"><span data-stu-id="12f1a-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="12f1a-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="12f1a-171">DurationMs</span></span> |<span data-ttu-id="12f1a-172">服務 REST API 要求時所花費的時間，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="12f1a-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="12f1a-173">這個時間不包括網路延遲，因此在用戶端所測量到的時間可能不符合此時間。</span><span class="sxs-lookup"><span data-stu-id="12f1a-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="12f1a-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="12f1a-174">httpStatusCode_d</span></span> |<span data-ttu-id="12f1a-175">由要求傳回的 HTTP 狀態碼 (例如 *200*)</span><span class="sxs-lookup"><span data-stu-id="12f1a-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="12f1a-176">id_s</span><span class="sxs-lookup"><span data-stu-id="12f1a-176">id_s</span></span> |<span data-ttu-id="12f1a-177">要求的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="12f1a-177">Unique ID of the request</span></span> |
| <span data-ttu-id="12f1a-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="12f1a-178">identity_claim_appid_g</span></span> | <span data-ttu-id="12f1a-179">應用程式識別碼的 GUID</span><span class="sxs-lookup"><span data-stu-id="12f1a-179">GUID for the application id</span></span> |
| <span data-ttu-id="12f1a-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="12f1a-180">OperationName</span></span> |<span data-ttu-id="12f1a-181">[Azure 金鑰保存庫記錄](../key-vault/key-vault-logging.md)中所記載的作業名稱</span><span class="sxs-lookup"><span data-stu-id="12f1a-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="12f1a-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="12f1a-182">OperationVersion</span></span> |<span data-ttu-id="12f1a-183">用戶端所要求的 REST API 版本 (例如 *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="12f1a-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="12f1a-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="12f1a-184">requestUri_s</span></span> |<span data-ttu-id="12f1a-185">要求的 Uri</span><span class="sxs-lookup"><span data-stu-id="12f1a-185">Uri of the request</span></span> |
| <span data-ttu-id="12f1a-186">資源</span><span class="sxs-lookup"><span data-stu-id="12f1a-186">Resource</span></span> |<span data-ttu-id="12f1a-187">金鑰保存庫的名稱</span><span class="sxs-lookup"><span data-stu-id="12f1a-187">Name of the key vault</span></span> |
| <span data-ttu-id="12f1a-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="12f1a-188">ResourceGroup</span></span> |<span data-ttu-id="12f1a-189">金鑰保存庫的資源群組</span><span class="sxs-lookup"><span data-stu-id="12f1a-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="12f1a-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="12f1a-190">ResourceId</span></span> |<span data-ttu-id="12f1a-191">Azure 資源管理員資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="12f1a-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="12f1a-192">對於 Key Vault 記錄來說，這是 Key Vault 的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="12f1a-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="12f1a-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="12f1a-193">ResourceProvider</span></span> |<span data-ttu-id="12f1a-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="12f1a-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="12f1a-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="12f1a-195">ResourceType</span></span> | <span data-ttu-id="12f1a-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="12f1a-196">*VAULTS*</span></span> |
| <span data-ttu-id="12f1a-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="12f1a-197">ResultSignature</span></span> |<span data-ttu-id="12f1a-198">HTTP 狀態 (例如 *OK*)</span><span class="sxs-lookup"><span data-stu-id="12f1a-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="12f1a-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="12f1a-199">ResultType</span></span> |<span data-ttu-id="12f1a-200">REST API 要求的結果 (例如 *Success*)</span><span class="sxs-lookup"><span data-stu-id="12f1a-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="12f1a-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="12f1a-201">SubscriptionId</span></span> |<span data-ttu-id="12f1a-202">包含金鑰保存庫的訂用帳戶的 Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="12f1a-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="12f1a-203">從舊的 Key Vault 解決方案進行移轉</span><span class="sxs-lookup"><span data-stu-id="12f1a-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="12f1a-204">從 2017 年 1 月開始，從 Key Vault 傳送記錄到 Log Analytics 的支援方式已變更。</span><span class="sxs-lookup"><span data-stu-id="12f1a-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="12f1a-205">這些變更可提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="12f1a-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="12f1a-206">記錄會直接寫入 Log Analytics，而不需要使用儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="12f1a-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="12f1a-207">當 Log Analytics 中具有產生的記錄時，延遲會變得較低</span><span class="sxs-lookup"><span data-stu-id="12f1a-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="12f1a-208">較少的組態步驟</span><span class="sxs-lookup"><span data-stu-id="12f1a-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="12f1a-209">所有 Azure 診斷類型的通用格式</span><span class="sxs-lookup"><span data-stu-id="12f1a-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="12f1a-210">若要使用更新的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="12f1a-210">To use the updated solution:</span></span>

1. [<span data-ttu-id="12f1a-211">將診斷設定為直接從 Key Vault 傳送到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="12f1a-211">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="12f1a-212">使用[從方案庫新增 Log Analytics 解決方案](log-analytics-add-solutions.md)中所述的程序，啟用 Azure Key Vault 解決方案</span><span class="sxs-lookup"><span data-stu-id="12f1a-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="12f1a-213">更新任何已儲存的查詢、儀表板或警示，以使用新的資料類型</span><span class="sxs-lookup"><span data-stu-id="12f1a-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="12f1a-214">類型從 KeyVaults 變更為 AzureDiagnostics。</span><span class="sxs-lookup"><span data-stu-id="12f1a-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="12f1a-215">您可以使用 ResourceType 篩選 Key Vault 記錄。</span><span class="sxs-lookup"><span data-stu-id="12f1a-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="12f1a-216">與其使用 `Type=KeyVaults`，請改用 `Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="12f1a-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="12f1a-217">欄位：(欄位名稱區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="12f1a-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="12f1a-218">針對任何名稱尾碼有 \_s、\_d 或 \_g 的欄位，請將第一個字元變更為小寫</span><span class="sxs-lookup"><span data-stu-id="12f1a-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="12f1a-219">針對任何名稱尾碼有 \_o 的欄位，資料會根據巢狀欄位名稱分割為個別欄位。</span><span class="sxs-lookup"><span data-stu-id="12f1a-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="12f1a-220">例如，呼叫端的 UPN 會儲存在欄位 `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="12f1a-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="12f1a-221">欄位 CallerIpAddress 變更為 CallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="12f1a-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="12f1a-222">欄位 RemoteIPCountry 已不存在</span><span class="sxs-lookup"><span data-stu-id="12f1a-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="12f1a-223">移除 *Key Vault 分析 (已過時)* 解決方案。</span><span class="sxs-lookup"><span data-stu-id="12f1a-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="12f1a-224">如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="12f1a-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="12f1a-225">在變更之前所收集的資料不會顯示在新的解決方案中。</span><span class="sxs-lookup"><span data-stu-id="12f1a-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="12f1a-226">您可以繼續使用舊的類型和欄位名稱查詢此資料。</span><span class="sxs-lookup"><span data-stu-id="12f1a-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="12f1a-227">疑難排解</span><span class="sxs-lookup"><span data-stu-id="12f1a-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="12f1a-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12f1a-228">Next steps</span></span>
* <span data-ttu-id="12f1a-229">使用 [Log Analytics 中的記錄搜尋](log-analytics-log-searches.md)來檢視詳細的 Azure 金鑰保存庫資料。</span><span class="sxs-lookup"><span data-stu-id="12f1a-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
