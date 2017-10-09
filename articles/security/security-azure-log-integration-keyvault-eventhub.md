---
title: "從 Azure 金鑰保存庫的 aaaIntegrate 記錄使用事件中心 |Microsoft 文件"
description: "提供 hello 必要步驟 toomake 金鑰保存庫的教學課程使用 Azure 記錄檔整合記錄可用 tooa SIEM"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Azure 記錄整合教學課程：使用事件中樞處理Azure Key Vault 事件

您可以使用 Azure 記錄檔整合 tooretrieve 記錄事件，並讓它們使用 tooyour 安全性資訊和事件管理 (SIEM) 系統。 本教學課程示範如何 Azure 記錄檔整合可以透過 Azure 事件中心取得的使用的 tooprocess 記錄檔。
 
使用此教學課程 tooget 熟悉 Azure 記錄檔整合和事件中心的工作，同時透過下列方式 hello 範例步驟，並了解每個步驟如何支援 hello 方案。 然後您可以採取什麼您已學習到以下 toocreate 自己步驟 toosupport 貴公司的獨特需求。

>[!WARNING]
hello 步驟與本教學課程中的命令不是預期的 toobe 複製和貼上。 這些步驟和命令僅供範例之用。 請勿使用即時環境中的 「 現狀 」 hello PowerShell 命令。 您必須根據自己專屬的環境自訂這些命令。


本教學課程會引導您進行 Azure 金鑰保存庫活動記錄的 tooan 事件中心，並且讓它成為可從 JSON 檔案 tooyour SIEM 系統的 hello 程序。 接著，您可以設定您的 SIEM 系統 tooprocess hello 的 JSON 檔案。

>[!NOTE]
>大部分的 hello 本教學課程步驟包括設定金鑰保存庫、 儲存體帳戶和事件中心。 hello 特定 Azure 記錄檔整合步驟會在本教學課程中的 hello 結尾處。 請勿在生產環境中執行這些步驟。 這些步驟僅供實驗室環境之用。 您必須自訂 hello 步驟，然後才在生產環境中使用。

提供資訊沿著 hello 方式可協助您了解每個步驟的 hello 動機。 連結 tooother 文件可讓您更多詳細資料的特定主題。

如需本教學課程提到的 hello 服務的詳細資訊，請參閱： 

- [Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)
- [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Azure 記錄整合](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>初始設定

您可以完成這篇文章中的 hello 步驟之前，您需要下列 hello:

1. Azure 訂用帳戶和該訂用帳戶上具有系統管理員權限的帳戶。 如果您沒有訂用帳戶，則可以建立[免費帳戶](https://azure.microsoft.com/free/)。
 
2. 存取 toohello 的系統符合 hello 安裝 Azure 記錄檔整合需求的網際網路。 hello 系統可在雲端服務，或裝載於內部。

3. 已安裝 [Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324)。 tooinstall 它：

   a. 使用上述步驟 2 中的遠端桌面 tooconnect toohello 系統。   
   b. 將複製 hello Azure 記錄檔整合安裝程式 toohello 系統。 您可以[下載 hello 安裝檔案](https://www.microsoft.com/download/details.aspx?id=53324)。   
   c. 啟動 hello 安裝程式，並接受 hello Microsoft 軟體授權條款。   
   d. 如果您將提供的遙測資訊，請保留 hello 選取核取方塊。 如果不而是傳送使用方式資訊 tooMicrosoft，清除 [hello] 核取方塊。
   
   如需有關 Azure 記錄檔整合以及 tooinstall，請參閱[Azure 記錄與整合 Azure 診斷記錄 Windows 事件轉送](security-azure-log-integration-get-started.md)。

4. hello 最新的 PowerShell 版本。
 
   如果您已安裝 Windows Server 2016，便至少擁有 PowerShell 5.0。 如果您正在使用任何其他版本的 Windows Server，則可能已安裝舊版 PowerShell。 您可以檢查 hello 版本輸入```get-host```PowerShell 視窗中。 如果您尚未安裝 PowerShell 5.0，則可以[進行下載](https://www.microsoft.com/download/details.aspx?id=50395)。

   您至少有之後 PowerShell 5.0 中，您可以繼續 tooinstall hello 最新版本：
   
   a. 在 PowerShell 視窗中，輸入 hello```Install-Module Azure```命令。 完成 hello 安裝步驟。    
   b. 輸入 hello```Install-Module AzureRM```命令。 完成 hello 安裝步驟。

   如需詳細資訊，請參閱[安裝 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0) (英文)。


## <a name="create-supporting-infrastructure-elements"></a>建立支援基礎結構元素

1. 開啟提升權限的 PowerShell 視窗，並移過**C:\Program Files\Microsoft Azure 記錄檔整合**。
2. 執行 hello 指令碼 LoadAzLogModule.ps1 匯入 hello AzLog cmdlet。 輸入 hello`.\LoadAzLogModule.ps1`命令。 (請注意 hello"。 \"命令中。)您應該會看到如下的結果：</br>

   ![載入的模組清單](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. 輸入 hello`Login-AzureRmAccount`命令。 在 hello 登入視窗中，輸入 hello 訂用帳戶將用於此教學課程中的 hello 認證資訊。

   >[!NOTE]
   >如果這是 hello tooAzure 下從這部電腦中登入您的第一次，您會看到訊息，以允許 Microsoft toocollect PowerShell 使用狀況資料。 我們建議您啟用此資料集合，因為它會在使用的 tooimprove Azure PowerShell。

4. 成功驗證之後，您登入，您會看到 hello hello 下列螢幕擷取畫面中的資訊。 記下 hello 訂用帳戶 ID 與訂用帳戶名稱，因為您需要它們 toocomplete 稍後步驟。

   ![PowerShell 視窗](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. 建立變數，稍後將會用 toostore 值。 輸入每個 hello 下列 PowerShell 程式行。 您可能需要 tooadjust hello 值 toomatch 您的環境。
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (您的訂用帳戶名稱可能會不同。 您可以看到它作為 hello 輸出的 hello 前一個命令的一部分。）
    - ```$location = 'West US'```（這個變數會使用的 toopass hello 位置建立資源的位置。 您可以變更這個變數 toobe 您所選擇任何的位置。）
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```（hello 名稱可以是任何項目，但它應該包含小寫字母和數字）。
    - ``` $storageName = $name```（hello 儲存體帳戶名稱將會使用此變數）。
    - ```$rgname = $name ```（這個變數會使用 hello 資源群組名稱）。
    - ``` $eventHubNameSpaceName = $name```（這是 hello hello 事件中樞命名空間名稱）。
6. 指定您將使用的 hello 訂用帳戶：
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. 建立資源群組：
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   如果您輸入`$rg`此時，您應該會看到輸出類似 toothis 螢幕擷取畫面：

   ![建立資源群組之後的輸出](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. 建立儲存體帳戶將會使用的 tookeep 追蹤的狀態資訊：
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. 建立 hello 事件中樞命名空間。 這是必要的 toocreate 事件中心。
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. 取得將用於與 hello insights 提供者的 hello 規則識別碼：
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. 取得所有可能的 Azure 位置，並在稍後步驟中加入可用的 hello 名稱 tooa 變數：
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    如果您輸入`$locations`此時，您看到 hello 位置名稱不含 hello Get AzureRmLocation 所傳回的額外資訊。
12. 建立 Azure Resource Manager 記錄設定檔： 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    如需 hello Azure 記錄檔的設定檔的詳細資訊，請參閱[hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)。

> [!NOTE]
> 當您嘗試 toocreate 記錄檔的設定檔，您可能會收到錯誤訊息。 然後，您可以檢閱 Get AzureRmLogProfile 和移除 AzureRmLogProfile hello 文件。 如果您執行 Get AzureRmLogProfile，您會看到 hello 記錄檔的設定檔的資訊。 您可以刪除現有記錄檔 hello 設定檔輸入 hello```Remove-AzureRmLogProfile -name 'Log Profile Name' ```命令。
>
>![資源管理員設定檔錯誤](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>建立金鑰保存庫

1. 建立 hello 金鑰保存庫：

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. 設定金鑰保存庫 hello 的記錄：

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>產生記錄活動

要求需要 toobe 傳送 tooKey 保存庫 toogenerate 記錄檔 」 活動。 產生金鑰、儲存密碼或從金鑰保存庫讀取密碼等動作都會建立記錄項目。

1. 顯示目前儲存體金鑰 hello:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. 產生新的 **key2**：
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. 再次顯示 hello 索引鍵，並看到**key2**會保存不同的值：
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. 設定和讀取密碼 toogenerate 額外的記錄項目：
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![傳回的密碼](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>設定 Azure 記錄整合

既然您已經設定所有 hello 必要的項目 toohave 金鑰保存庫記錄 tooan 事件中樞，您會需要 tooconfigure Azure 記錄檔整合：

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

執行每個事件中樞的 hello AzLog 命令：

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

之後約一分鐘執行 hello 最後兩個命令，您應該會看到所產生的 JSON 檔案。 您可以藉由監視 hello 目錄，確認**C:\users\AzLog\EventHubJson**。

## <a name="next-steps"></a>後續步驟

- [Azure 記錄整合常見問題集](security-azure-log-integration-faq.md)
- [開始使用 Azure 記錄整合](security-azure-log-integration-get-started.md)
- [將記錄從 Azure 資源整合到 SIEM 系統](security-azure-log-integration-overview.md)
