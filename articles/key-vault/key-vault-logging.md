---
title: "金鑰保存庫記錄 aaaAzure |Microsoft 文件"
description: "使用開始使用 Azure 金鑰保存庫本教學課程 toohelp 記錄。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Azure 金鑰保存庫記錄
大部分地區均提供 Azure 金鑰保存庫。 如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。

## <a name="introduction"></a>簡介
建立一或多個金鑰保存庫之後，您可能會想 toomonitor 如何及何時您金鑰保存庫會存取，以及由誰。 想要做到這點，您可以啟用金鑰保存庫記錄，以在您提供的 Azure 儲存體帳戶中儲存這方面的資訊。 系統會自動為您指定的儲存體帳戶建立新的容器，其名稱為 **insights-logs-auditevent** ，而您也可以使用同一個儲存體帳戶來收集多個金鑰保存庫的記錄。

您可以存取您的記錄資訊最多，10 分鐘後 hello 金鑰保存庫作業。 但大多不用這麼久。  是由 tooyou toomanage 您儲存體帳戶中的記錄檔：

* 使用標準的 Azure 存取控制方法 toosecure 記錄藉由限制誰可以存取它們。
* 刪除您不再想 tookeep 儲存體帳戶中的記錄檔。

使用開始使用 Azure 金鑰保存庫記錄、 toocreate 此教學課程 toohelp 儲存體帳戶啟用記錄，並解譯 hello 記錄收集的資訊。  

> [!NOTE]
> 本教學課程不包括如何 toocreate 金鑰保存庫、 金鑰或密碼的指示。 如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。 或者，如需跨平台命令列介面的指示，請參閱 [這個對等的教學課程](key-vault-manage-with-cli2.md)。
>
> 目前，您無法在 hello Azure 入口網站中設定 Azure 金鑰保存庫。 請改用這些 Azure PowerShell 指示。
>
>

如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您必須擁有下列 hello:

* 所使用的現有金鑰保存庫。  
* Azure PowerShell ( **至少必須是 1.0.1 版**)。 tooinstall Azure PowerShell，將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 如果您已安裝 Azure PowerShell，並不知道 hello 版本 hello Azure PowerShell 主控台中，輸入`(Get-Module azure -ListAvailable).Version`。  
* 足夠的 Azure 儲存體以儲存金鑰保存庫記錄。

## <a id="connect"></a>連接 tooyour 訂用帳戶
啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：  

    Login-AzureRmAccount

在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。 Azure PowerShell 會取得所有 hello 訂用帳戶相關聯，與此帳戶，而且依預設，會使用 hello 第一個。

如果您有多個訂閱，您可能必須 toospecify 已使用的 toocreate 特定的 Azure 金鑰保存庫。 輸入下列帳戶 toosee hello 訂閱 hello:

    Get-AzureRmSubscription

然後，toospecify hello 訂用帳戶與金鑰保存庫會記錄您、 型別相關聯：

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> 這個步驟很重要，如果您有多個與帳戶相關聯的訂用帳戶會特別實用。 如果略過這個步驟，可能會收到錯誤 tooregister Microsoft.Insights。
>   
>

如需有關如何設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a id="storage"></a>建立新的儲存體帳戶來儲存記錄
雖然您可以使用現有的儲存體帳戶記錄，我們將建立新的儲存體帳戶將專用的 tooKey 保存庫的記錄檔。 為了方便起見，當我們的 toospecify 這的更新版本中，我們將會儲存 hello 詳細資料放入變數，名為**sa**。

其他易於管理，我們將也使用 hello 相同的資源群組，因為其中包含我們金鑰保存庫 hello。 從 hello[快速入門教學課程](key-vault-get-started.md)，名為此資源群組**ContosoResourceGroup** ，我們將持續 toouse hello 東亞 」 位置。 請視情況將這些值替換成您自己的值：

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> 如果您決定 toouse 現有的儲存體帳戶，則必須使用為金鑰保存庫，它必須使用 hello Resource Manager 部署模型，而非 hello 傳統部署模型 hello 相同訂用帳戶。
>
>

## <a id="identify"></a>識別 hello 記錄金鑰保存庫
取得開始教學課程中，在我們的金鑰保存庫名稱是**ContosoKeyVault**，因此我們將持續的名稱，並將 hello 詳細資料儲存到變數，名為 toouse **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>啟用記錄
tooenable 記錄金鑰保存庫，我們將使用 hello 組 AzureRmDiagnosticSetting cmdlet 時，我們建立我們新的儲存體帳戶和我們的金鑰保存庫以及 hello 變數。 我們也會隨即制定 hello **-啟用**旗標太**$true**並設定 hello 類別 tooAuditEvent （hello 唯一類別進行金鑰保存庫記錄）：

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

這個 hello 輸出包含：

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


這可確認現在您金鑰保存庫，儲存資訊 tooyour 儲存體帳戶啟用記錄。

您也可以選擇性地設定記錄檔的保留原則，以便自動刪除較舊的記錄檔。 例如，將設定保留原則使用**-RetentionEnabled**旗標太**$true**並設定**-RetentionInDays**參數太**90**讓會自動刪除超過 90 天的記錄檔。

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

所記錄的內容：

* 會記錄所有已驗證的 REST API 要求，包括因為存取權限、系統錯誤或要求錯誤而發生的失敗要求。
* 作業 hello 金鑰保存庫本身，其中包括建立、 刪除、 設定金鑰保存庫的存取原則，並更新金鑰保存庫屬性，例如標記。
* 金鑰和秘密 hello 金鑰保存庫中，包括建立、 修改或刪除這些機碼或密碼; 上的作業作業，例如登入驗證、 加密、 解密、 包裝並解除包裝金鑰、 取得密碼、 列出金鑰和密碼，以及其版本。
* 產生 401 回應的未經驗證要求。 例如，沒有持有人權杖的要求，或格式不正確或已過期的要求，或具有無效權杖的要求。  

## <a id="access"></a>存取記錄
金鑰保存庫的記錄檔會儲存在 hello **insights-記錄檔-auditevent** hello 您提供的儲存體帳戶中的容器。 toolist 所有 hello blob，在此容器中，都輸入：

首先，建立 hello 容器名稱的變數。 這將會使用其餘的 hello 逐步 hello。

    $container = 'insights-logs-auditevent'

toolist 所有 hello blob，在此容器中，都輸入：

    Get-AzureStorageBlob -Container $container -Context $sa.Context
hello 輸出看起來類似 toothis:

**容器 Uri：https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**名稱**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

您可以從這個輸出中看到，hello blob 遵循命名慣例： **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h i n =<hour>/m =<minute>/filename.json**

hello 日期和時間值會使用 UTC。

由於 hello 相同儲存體帳戶可以是使用的 toocollect 記錄檔中的多個資源，hello 完整資源識別碼 hello blob 名稱中是很有幫助 tooaccess 或下載僅 hello blob，您需要。 這樣做之前，將會先涵蓋如何 toodownload 所有 hello blob。

首先，建立資料夾 toodownload hello blob。 例如：

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

然後取得所有 blob 的清單：  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

您可以將這份清單透過 ' Get AzureStorageBlobContent' toodownload hello blob 管道傳送至我們的目的資料夾：

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

當您執行這個第二個命令時，hello  **/**  hello blob 名稱中的分隔符號建立完整資料夾結構 hello 目的地資料夾下的，此結構會使用 toodownload 和存放區 hello blob 檔案。

tooselectively 下載 blob 時，使用萬用字元。 例如：

* 如果您有多個金鑰保存庫，並想要只在一個金鑰保存庫，名為 CONTOSOKEYVAULT3 toodownload 記錄檔：

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* 如果您有多個資源群組，並想 toodownload 記錄檔只在一個資源群組，使用`-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* 如果您想 toodownload hello 的所有記錄的 2016 年 1 月 hello 月，使用`-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

您現在準備好 toostart 查看功能的 hello 記錄。 但才會繼續，您可能需要 tooknow Get AzureRmDiagnosticSetting 的兩個多個參數：

* tooquery hello 狀態的診斷設定金鑰保存庫資源：`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* toodisable 記錄金鑰保存庫資源：`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>解譯金鑰保存庫記錄
各個 blob 皆會儲存為文字，並格式化為 JSON blob。 以下是執行 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`後所得到的範例記錄項目：

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


hello 下表列出 hello 欄位名稱和描述。

| 欄位名稱 | 說明 |
| --- | --- |
| 分析 |日期和時間 (UTC)。 |
| resourceId |Azure 資源管理員資源識別碼。 為金鑰保存庫的記錄檔，這一定是 hello 金鑰保存庫的資源 id。 |
| operationName |Hello 作業，如 hello 下一個表格中所述的名稱。 |
| operationVersion |這是 hello hello 用戶端要求的 REST API 版本。 |
| category |適用於金鑰保存庫記錄 AuditEvent hello 單一、 可用值。 |
| resultType |REST API 要求的結果。 |
| resultSignature |HTTP 狀態。 |
| resultDescription |其他 hello 結果可用時的詳細描述。 |
| durationMs |以毫秒為單位 tooservice hello REST API 要求所花費的時間。 這不包括 hello 網路延遲，讓您測量 hello 用戶端 hello 時間可能不符合此時間。 |
| callerIpAddress |Hello 用戶端 hello 要求者 IP 位址。 |
| correlationId |選擇性的 GUID，hello 用戶端可以傳遞 toocorrelate 用戶端與服務端 （金鑰保存庫） 記錄檔的記錄檔。 |
| 身分識別 |從 hello 權杖提出 hello REST API 要求時提供的身分識別。 和 Azure PowerShell Cmdlet 所產生之要求的案例一樣，這通常是「使用者」、「服務主體」或「使用者+appId」的組合。 |
| 屬性 |此欄位會包含不同 hello 作業 (operationName) 為基礎的資訊。 在大部分情況下，包含用戶端資訊 （hello 使用者代理字串 hello 用戶端所傳遞），hello 確切的 REST API 要求 URI、 與 HTTP 狀態碼。 此外，要求 （例如，KeyCreate 或 VaultGet） 的結果傳回的物件時它也會包含 hello （為"id") 的金鑰 URI、 保存庫 URI 或 URI 密碼。 |

hello **operationName**欄位值的 ObjectVerb 格式。 例如：

* 金鑰保存庫的所有作業都有 hello '保存庫`<action>`' 格式，例如`VaultGet`和`VaultCreate`。
* 索引鍵的所有作業都有 hello '索引鍵`<action>`' 格式，例如`KeySign`和`KeyList`。
* 密碼的所有作業都有 hello '密碼`<action>`' 格式，例如`SecretGet`和`SecretListVersions`。

hello 下表列出 hello operationName 和對應的 REST API 命令。

| operationName | REST API 命令 |
| --- | --- |
| 驗證 |透過 Azure Active Directory 端點 |
| VaultGet |[取得金鑰保存庫的相關資訊](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[建立或更新金鑰保存庫](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[刪除金鑰保存庫](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[更新金鑰保存庫](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[列出資源群組中的所有金鑰保存庫](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[建立金鑰](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[取得金鑰的相關資訊](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[將金鑰匯入保存庫](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[備份金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx)。 |
| KeyDelete |[刪除金鑰](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[還原金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[使用金鑰簽署](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[使用金鑰驗證](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[包裝金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[解除包裝金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[使用金鑰加密](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[使用金鑰解密](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[更新金鑰](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[列出保存庫中的 hello 索引鍵](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[金鑰的清單 hello 版本](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[建立密碼](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[取得密碼](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[更新密碼](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[刪除秘密](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[列出保存庫中的密碼](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[列出密碼的版本](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>使用 Log Analytics

您可以在 Azure 金鑰保存庫 AuditEvent 記錄的記錄分析 tooreview 使用 hello Azure 金鑰保存庫的方案。 如需詳細資訊，包括如何 tooset 其設定，請參閱[記錄分析中的 Azure 金鑰保存庫方案](../log-analytics/log-analytics-azure-key-vault.md)。 如果您需要從 hello 舊金鑰保存庫已提供解決方案 hello 記錄分析在預覽期間，您先路由傳送您的記錄檔 tooan Azure 儲存體帳戶並設定從該處的記錄分析 tooread toomigrate 本文也會包含指示。

## <a id="next"></a>接續步驟
如需在 Web 應用程式中使用 Azure 金鑰保存庫的教學課程，請參閱 [從 Web 應用程式使用 Azure 金鑰保存庫](key-vault-use-from-web-application.md)。

程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。

如需 Azure 金鑰保存庫的 Azure PowerShell 1.0 Cmdlet 清單，請參閱 [Azure 金鑰保存庫 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。

如需金鑰輪替和使用 Azure 金鑰保存庫稽核記錄檔的教學課程，請參閱[如何與結束 tooend toosetup 金鑰保存庫金鑰旋轉和稽核](key-vault-key-rotation-log-monitoring.md)。
