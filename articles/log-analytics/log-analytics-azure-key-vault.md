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
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Log Analytics 中的 Azure Key Vault 分析解決方案

![Key Vault 符號](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

您可以在 Azure 金鑰保存庫 AuditEvent 記錄的記錄分析 tooreview 使用 hello Azure 金鑰保存庫的方案。

toouse hello 方案，您需要 tooenable 記錄 Azure 金鑰保存庫診斷和直接 hello 診斷 tooa 記錄分析工作區。 不需要 toowrite hello 記錄 tooAzure Blob 儲存體。

> [!NOTE]
> 在年 1 月 2017 hello 會支援從金鑰保存庫 tooLog 分析變更傳送記錄檔的方式。 如果您使用 hello 金鑰保存庫方案顯示*（已過時）* hello 標題中，請參閱太[從 hello 舊的金鑰保存庫方案移轉](#migrating-from-the-old-key-vault-solution)步驟中，您需要 toofollow。
>
>

## <a name="install-and-configure-hello-solution"></a>安裝和設定 hello 方案
使用下列指示 tooinstall hello，並設定 hello Azure 金鑰保存庫方案：

1. 啟用從 hello Azure 金鑰保存庫解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 啟用診斷記錄的 hello 金鑰保存庫資源 toomonitor、 使用任一 hello[入口網站](#enable-key-vault-diagnostics-in-the-portal)或[PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>金鑰保存庫中啟用診斷 hello 入口網站

1. 在 hello Azure 入口網站，瀏覽 toohello 金鑰保存庫資源 toomonitor
2. 選取*診斷記錄檔*tooopen hello 遵循頁面

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. 按一下*開啟診斷*tooopen hello 遵循頁面

   ![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. 診斷，tooturn 按一下*上*下*狀態*
5. 按一下 [hello] 核取方塊*傳送 tooLog 分析*
6. 選取現有的 Log Analytics 工作區，或建立工作區
7. tooenable *AuditEvent*記錄檔，在記錄檔下按一下 hello 核取方塊
8. 按一下*儲存*tooenable hello 記錄診斷 tooLog 分析

### <a name="enable-key-vault-diagnostics-using-powershell"></a>使用 PowerShell 啟用 Key Vault 診斷
下列 PowerShell 指令碼的 hello 提供的範例 toouse `Set-AzureRmDiagnosticSetting` tooenable 金鑰保存庫的診斷記錄：
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>檢閱 Azure 金鑰保存庫資料收集的詳細資料
Azure 金鑰保存庫方案會直接從 hello 金鑰保存庫中收集診斷記錄檔。
不必要的 toowrite hello 記錄 tooAzure Blob 儲存體，而且沒有代理程式需要的資料收集。

hello 下表顯示資料收集方法，以及如何針對 Azure 金鑰保存庫收集資料的其他詳細資料。

| 平台 | 直接代理程式 | Systems Center Operations Manager 代理程式 | Azure | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | 與抵達同時 |

## <a name="use-azure-key-vault"></a>使用 Azure 金鑰保存庫
之後您[hello 方案安裝](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)，hello，即可檢視 hello 金鑰保存庫資料**Azure 金鑰保存庫**磚從 hello**概觀**記錄分析的頁面。

![Azure 金鑰保存庫圖格的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

按一下 hello 之後**概觀**磚中，您可以檢視您的記錄檔，接著再深入的摘要中 toodetails hello 下列類別：

* 經過一段時間的所有金鑰保存庫作業的數量
* 經過一段時間的失敗作業數量
* 依作業的平均作業延遲
* Hello 1000 毫秒以上之作業數目與 1000 毫秒以上之作業的清單作業的服務品質

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure 金鑰保存庫儀表板的影像](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>tooview 的任何作業的詳細資料
1. 在 hello**概觀**頁面上，按一下 hello **Azure 金鑰保存庫**磚。
2. 在 [hello **Azure 金鑰保存庫**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 的詳細資訊，請參閱 hello 記錄搜尋] 頁面中的資訊。

    在任何 hello 記錄搜尋 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。 您也可以篩選由 facet toonarrow hello 結果。

## <a name="log-analytics-records"></a>Log Analytics 記錄
hello Azure 金鑰保存庫方案會分析具有一種記錄**KeyVaults**從收集[AuditEvent 記錄](../key-vault/key-vault-logging.md)Azure 診斷內。  這些記錄屬性會在下表中的 hello:  

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*AzureDiagnostics* |
| SourceSystem |*Azure* |
| CallerIpAddress |Hello 用戶端 hello 要求者 IP 位址 |
| 類別 | *AuditEvent* |
| CorrelationId |選擇性的 GUID，hello 用戶端可以傳遞 toocorrelate 用戶端與服務端 （金鑰保存庫） 記錄檔的記錄檔。 |
| DurationMs |以毫秒為單位 tooservice hello REST API 要求所花費的時間。 這次不包括網路延遲，讓您測量 hello 用戶端的 hello 時間可能不符合此時間。 |
| httpStatusCode_d |Hello 要求所傳回的 HTTP 狀態碼 (例如， *200*) |
| id_s |Hello 要求的唯一識別碼 |
| identity_claim_appid_g | Hello 應用程式識別碼的 GUID |
| OperationName |Hello 作業，如中所述的名稱[Azure 金鑰保存庫記錄](../key-vault/key-vault-logging.md) |
| OperationVersion |Hello 用戶端所要求的 REST API 版本 (例如*2015年-06-01*) |
| requestUri_s |Hello 要求 Uri |
| 資源 |Hello 金鑰保存庫的名稱 |
| ResourceGroup |Hello 金鑰保存庫的資源群組 |
| ResourceId |Azure 資源管理員資源識別碼。 為金鑰保存庫的記錄檔，這是 hello 金鑰保存庫的資源 id。 |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |HTTP 狀態 (例如 *OK*) |
| ResultType |REST API 要求的結果 (例如 *Success*) |
| SubscriptionId |Hello 包含 hello 金鑰保存庫的訂用帳戶的 azure 訂用帳戶 ID |

## <a name="migrating-from-hello-old-key-vault-solution"></a>從舊金鑰保存庫方案 hello 移轉
在年 1 月 2017 hello 會支援從金鑰保存庫 tooLog 分析變更傳送記錄檔的方式。 這些變更會提供下列優點 hello:
+ 記錄檔寫入直接 tooLog 分析 hello 不需要 toouse 儲存體帳戶
+ 從記錄檔時的 hello 時間延遲越少產生 toothem 可以使用這個記錄分析
+ 較少的組態步驟
+ 所有 Azure 診斷類型的通用格式

toouse hello 更新方案：

1. [設定診斷 toobe 從金鑰保存庫直接傳送 tooLog 分析](#enable-key-vault-diagnostics-in-the-portal)  
2. 啟用使用 hello 程序中所述的 hello Azure 金鑰保存庫解決方案[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)
3. 更新任何已儲存的查詢、 儀表板或警示 toouse hello 新的資料類型
  + 型別是來自變更： KeyVaults tooAzureDiagnostics。 您可以使用 hello ResourceType toofilter tooKey 保存庫的記錄檔。
  - 與其使用 `Type=KeyVaults`，請改用 `Type=AzureDiagnostics ResourceType=VAULTS`
  + 欄位：(欄位名稱區分大小寫)
  - 如有後置字元的任何欄位\_s， \_d 或\_g hello 名稱，變更 hello 第一個字元 toolower 案例中
  - 如有後的置字元的任何欄位\_o 在 [名稱] hello 資料會分成根據 hello 巢狀欄位名稱的個別欄位。 例如，hello hello 呼叫端的 UPN 會儲存在欄位`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - 變更欄位 CallerIpAddress tooCallerIPAddress
   - 欄位 RemoteIPCountry 已不存在
4. 移除 hello*金鑰保存庫分析 （已過時）*方案。 如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Hello 新方案中看不到 hello 變更之前，收集資料。 您可以繼續 tooquery，針對使用此資料 hello 舊的類型和欄位名稱。

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Azure 金鑰保存庫的資料。
