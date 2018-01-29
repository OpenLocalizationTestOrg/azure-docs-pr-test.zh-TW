---
title: "Azure Cosmos DB 診斷記錄 | Microsoft Docs"
description: "使用本教學課程來協助您開始使用 Azure Cosmos DB 記錄。"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2017
ms.author: mimig
ms.openlocfilehash: 835f6ffce9b2e1bb4b6cfd7476bb3fdb24a4f092
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="azure-cosmos-db-diagnostic-logging"></a>Azure Cosmos DB 診斷記錄

一旦您開始使用一或多個 Azure Cosmos DB 資料庫，您可能想要監視資料庫的存取方式和時間。 Azure Cosmos DB 中的診斷記錄，可讓您執行這項監視。 藉由啟用診斷記錄，您可以將記錄傳送至 [Azure 儲存體](https://azure.microsoft.com/services/storage/)、將它們串流處理至 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)，及/或將它們匯出到 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) (這是 [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) 的一部份)。

![透過 Log Analytics 將診斷記錄送至儲存體、事件中樞或 Operations Management Suite](./media/logging/azure-cosmos-db-logging-overview.png)

使用本教學課程，透過 Azure 入口網站、CLI 或 PowerShell 開始使用 Azure Cosmos DB 記錄。

## <a name="what-is-logged"></a>會記錄什麼內容？

* 系統會記錄所有已驗證的 REST SQL API 要求，包括因為存取權限、系統錯誤或要求錯誤而發生的失敗要求。 目前未提供對 MongoDB、圖表和資料表 API 的支援。
* 對資料庫本身的作業，包括對所有文件、容器和資料庫的 CRUD 作業。
* 對帳戶金鑰的作業，包括建立、修改或刪除這些金鑰。
* 產生 401 回應的未經驗證要求。 例如，沒有持有人權杖的要求，或格式不正確或已過期的要求，或具有無效權杖的要求。

## <a name="prerequisites"></a>先決條件
若要完成本教學課程，您必須具備下列資源：

* 現有的 Azure Cosmos DB 帳戶、資料庫和容器。 如需建立這些資源的指示，請參閱[使用 Azure 入口網站建立資料庫帳戶](create-sql-api-dotnet.md#create-a-database-account)、[CLI 範例](cli-samples.md)或 [PowerShell 範例](powershell-samples.md)。

<a id="#turn-on"></a>
## <a name="turn-on-logging-in-the-azure-portal"></a>在 Azure 入口網站中開啟記錄

1. 在 [Azure 入口網站](https://portal.azure.com)中，於您的 Azure Cosmos DB 帳戶左側瀏覽區中按一下 [診斷記錄]，然後按一下 [開啟診斷]。

    ![在 Azure 入口網站中開啟 Azure Cosmos DB 的診斷記錄](./media/logging/turn-on-portal-logging.png)

2. 在 [診斷設定] 頁面中，執行下列動作： 

    * **名稱**。 輸入要建立之記錄的名稱。

    * **封存至儲存體帳戶**。 若要使用此選項，您需要可以連接的現有儲存體帳戶。 若要在入口網站中建立新的儲存體帳戶，請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)，依指示建立一個 Resource Manager (一般用途帳戶)。 然後返回入口網站的此頁面選取您的儲存體帳戶。 新建立的儲存體帳戶可能在數分鐘後才會出現在下拉式功能表中。
    * **串流處理至事件中樞**。 若要使用此選項，您需要可以連接的現有事件中樞命名空間和事件中樞。 若要建立事件中樞命名空間，請參閱[使用 Azure 入口網站建立事件中樞命名空間和事件中樞](../event-hubs/event-hubs-create.md)。 然後返回入口網站的此頁面選取事件中樞命名空間和原則名稱。
    * **傳送至 Log Analytics**。     若要使用此選項，請使用現有的工作區，或是在入口網站中依照[建立新的工作區](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace)的步驟建立新的 Log Analytics 工作區。 如需有關如何檢視 Log Analytics 記錄的詳細資訊，請參閱[檢視 Log Analytics 中的記錄](#view-in-loganalytics)。
    * **記錄 DataPlaneRequests**。 選取此選項可記錄 SQL、圖形、資料表 API 帳戶的診斷。 如果您要封存至儲存體帳戶，可以為診斷記錄選取保留期限。 保留期限過後，就會自動刪除記錄。
    * **記錄 MongoRequests**。 選取此選項可記錄 MongoDB API 帳戶的診斷。 如果您要封存至儲存體帳戶，可以為診斷記錄選取保留期限。 保留期限過後，就會自動刪除記錄。
    * **計量要求**。 選取此選項可儲存 [Azure 計量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)中的詳細資料。 如果您要封存至儲存體帳戶，可以為診斷記錄選取保留期限。 保留期限過後，就會自動刪除記錄。

3. 按一下 [檔案] 。

    如果您收到錯誤，指出「無法更新 \<工作區名稱> 的診斷。 訂用帳戶 \<訂用帳戶識別碼> 未註冊為使用 microsoft.insights」， 請遵循[針對 Azure 診斷進行疑難排解](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)的指示註冊帳戶，然後重試此程序。

    未來如果您想變更診斷記錄的儲存方式，隨時可以返回此頁面修改帳戶的診斷記錄設定。

## <a name="turn-on-logging-using-cli"></a>使用 CLI 開啟記錄

若要使用 Azure CLI 啟用計量和診斷記錄功能，請使用下列 Cmdlet：

- 若要啟用儲存體帳戶中的診斷記錄檔的儲存體，使用下列命令︰

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   `resourceId` 是 Azure Cosmos DB 帳戶的名稱。 `storageId` 是您要傳送記錄的目的地儲存體帳戶名稱。

- 若要啟用將診斷記錄檔串流至事件中樞，使用下列命令︰

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   `resourceId` 是 Azure Cosmos DB 帳戶的名稱。 `serviceBusRuleId` 將會是此格式的字串︰

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- 若要啟用將診斷記錄檔傳送到 Log Analytics 工作區，請使用此命令︰

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

您可以結合這些參數讓多個輸出選項。

## <a name="turn-on-logging-using-powershell"></a>使用 PowerShell 開啟記錄

若要使用 PowerShell 開啟記錄，您需要最低版本為 1.0.1 的 Azure Powershell。

若要安裝 Azure PowerShell，並將它與 Azure 訂用帳戶建立關聯，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。

如果您已安裝 Azure PowerShell 但不知道版本，請從 PowerShell 主控台輸入 `(Get-Module azure -ListAvailable).Version`。  

### <a id="connect"></a>連線到您的訂用帳戶
開始 Azure PowerShell 工作階段，並使用下列命令登入您的 Azure 帳戶：  

```powershell
Login-AzureRmAccount
```

在快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱與密碼。 Azure PowerShell 會取得與此帳戶相關聯的所有訂用帳戶，並依預設使用第一個訂用帳戶。

如果您有多個訂用帳戶，您可能必須指定用來建立 Azure 金鑰保存庫的那一個特定訂用帳戶。 輸入下列命令以查看您帳戶的訂用帳戶：

```powershell
Get-AzureRmSubscription
```

然後，輸入下列命令，以指定與所要記錄之 Azure Cosmos DB 帳戶相關聯的訂用帳戶：

```powershell
Set-AzureRmContext -SubscriptionId <subscription ID>
```

> [!NOTE]
> 如果您有多個與帳戶相關聯的訂用帳戶，指定訂用帳戶非常重要。
>
>

如需設定 Azure PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。

### <a id="storage"></a>建立新的儲存體帳戶來儲存記錄
雖然您可以使用現有的儲存體帳戶來儲存記錄，在本教學課程中，我們將建立 Azure Cosmos DB 記錄專用的新儲存體帳戶。 為了方便起見，我們將儲存體帳戶詳細資料儲存到名為 **sa** 的變數。

為了進一步簡化管理，在本教學課程中，我們會使用包含 Azure Cosmos DB 資料庫的同一個資源群組。 視情況將 ContosoResourceGroup、contosocosmosdblogs 和 'North Central US' 的值替換成您自己的值：

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup `
-Name contosocosmosdblogs -Type Standard_LRS -Location 'North Central US'
```

> [!NOTE]
> 如果您決定使用現有儲存體帳戶，則必須使用和 Azure Cosmos DB 訂用帳戶相同的訂用帳戶，此外也必須使用 Resource Manager 部署模型，而非傳統部署模型。
>
>

### <a id="identify"></a>識別記錄的 Azure Cosmos DB 帳戶
將 Azure Cosmos DB 帳戶名稱設為名為 **account** 的變數，其中的 ResourceName 是 Azure Cosmos DB 帳戶的名稱。

```powershell
$account = Get-AzureRmResource -ResourceGroupName ContosoResourceGroup `
-ResourceName contosocosmosdb -ResourceType "Microsoft.DocumentDb/databaseAccounts"
```

### <a id="enable"></a>啟用記錄
若要啟用 Azure Cosmos DB 的記錄，請使用 Set-AzureRmDiagnosticSetting Cmdlet 搭配分別代表下列項目的變數：新儲存體帳戶、Azure Cosmos DB 帳戶及要啟用記錄的類別目錄。 執行下列命令，將 **-Enabled** 旗標設為 **$true**：

```powershell
Set-AzureRmDiagnosticSetting  -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests
```

命令的輸出應該如以下所示：

```powershell
    StorageAccountId            : /subscriptions/<subscription-ID>/resourceGroups/ContosoResourceGroup/providers`
    /Microsoft.Storage/storageAccounts/contosocosmosdblogs
    ServiceBusRuleId            :
    EventHubAuthorizationRuleId :
    Metrics
        TimeGrain       : PT1M
        Enabled         : False
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    Logs
        Category        : DataPlaneRequests
        Enabled         : True
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    WorkspaceId                 :
    Id                          : /subscriptions/<subscription-ID>/resourcegroups/ContosoResourceGroup/providers`
    /microsoft.documentdb/databaseaccounts/contosocosmosdb/providers/microsoft.insights/diagnosticSettings/service
    Name                        : service
    Type                        :
    Location                    :
    Tags                        :
```

這個結果可確認資料庫記錄現已啟用，系統會將資訊儲存到儲存體帳戶中。

您也可以選擇性地設定記錄檔的保留原則，以便自動刪除較舊的記錄檔。 例如，使用 **-RetentionEnabled** 旗標將保留原則設為 **$true** 並將 **-RetentionInDays** 參數設為 **90**，以便自動刪除超過 90 天的舊記錄檔。

```powershell
Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
 -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests`
  -RetentionEnabled $true -RetentionInDays 90
```

### <a id="access"></a>存取記錄
**DataPlaneRequests** 類別目錄的 Azure Cosmos DB 記錄會儲存在您提供之儲存體帳戶的 **insights-logs-data-plane-requests** 容器中。 

首先，建立容器名稱的變數。 此變數會用於逐步解說剩餘的各個部分。

```powershell
    $container = 'insights-logs-dataplanerequests'
```

若要列出此容器中的所有 blob，請輸入：

```powershell
Get-AzureStorageBlob -Container $container -Context $sa.Context
```

其輸出類似如下範例：

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 10510193
ContentType       : application/octet-stream
LastModified      : 9/28/2017 7:49:04 PM +00:00
SnapshotTime      :
ContinuationToken:
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.`
                    LazyAzureStorageContext
Name              : resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS`
/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/CONTOSOCOSMOSDB/y=2017/m=09/d=28/h=19/m=00/PT1H.json
```

在此輸出中我們可以看到，blob 遵循以下命名慣例：`resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/<Database Account Name>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json`

日期和時間值使用 UTC。

因為可以使用相同的儲存體帳戶來收集多個資源的記錄，blob 名稱中的完整資源識別碼很適合用來只存取或下載所需 blob。 但在這麼做之前，我們要先討論如何下載所有 blob。

首先，建立資料夾來下載 blob。 例如︰

```powershell
New-Item -Path 'C:\Users\username\ContosoCosmosDBLogs'`
 -ItemType Directory -Force
```

然後取得所有 blob 的清單：  

```powershell
$blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context
```

透過 'Get-AzureStorageBlobContent' 以管道傳送這份清單，將 blob 下載到目的地資料夾：

```powershell
$blobs | Get-AzureStorageBlobContent `
 -Destination 'C:\Users\username\ContosoCosmosDBLogs'
```

在執行第二個命令時，blob 名稱中的 **/** 分隔符號會在目的地資料夾下建立完整資料夾結構。 此資料夾結構將會用來下載 blob 並儲存為檔案。

若要有所選擇地下載 blob，請使用萬用字元。 例如︰

* 如果您有多個資料庫，並且只想下載其中的 CONTOSOCOSMOSDB3 資料庫的記錄：

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/DATABASEACCOUNTS/CONTOSOCOSMOSDB3
    ```

* 如果您有多個資源群組，並且只想下載其中某個資源群組的記錄，請使用 `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`：

    ```powershell
    Get-AzureStorageBlob -Container $container `
    -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
    ```
* 如果您想下載 2017 年 7 月份當月的所有記錄，請使用 `-Blob '*/year=2017/m=07/*'`：

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/year=2017/m=07/*'
    ```

此外：

* 查詢資料庫資源的診斷設定狀態：`Get-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
* 停用您資料庫帳戶資源的 **DataPlaneRequests** 類別目錄記錄：`Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories DataPlaneRequests`


在這些查詢中傳回的 blob 會儲存為文字，格式化為 JSON blob，如下列程式碼所示。 

```json
{
    "records":
    [
        {
           "time": "Fri, 23 Jun 2017 19:29:50.266 GMT",
           "resourceId": "contosocosmosdb",
           "category": "DataPlaneRequests",
           "operationName": "Query",
           "resourceType": "Database",
           "properties": {"activityId": "05fcf607-6f64-48fe-81a5-f13ac13dd1eb",`
           "userAgent": "documentdb-dotnet-sdk/1.12.0 Host/64-bit MicrosoftWindowsNT/6.2.9200.0 AzureSearchIndexer/1.0.0",`
           "resourceType": "Database","statusCode": "200","documentResourceId": "",`
           "clientIpAddress": "13.92.241.0","requestCharge": "2.260","collectionRid": "",`
           "duration": "9250","requestLength": "72","responseLength": "209", "resourceTokenUserRid": ""}
        }
    ]
}
```

若要深入了解每個 JSON blob 中的資料，請參閱[解讀 Azure Cosmos DB 記錄](#interpret)。

## <a name="managing-your-logs"></a>管理記錄

Azure Cosmos DB 作業執行後兩個小時，就可以在您的帳戶中使用記錄。 儲存體帳戶中的記錄由您全權管理：

* 請使用標準的 Azure 存取控制方法限制可存取記錄的人員，藉此來保護記錄。
* 刪除不想繼續保留在儲存體帳戶中的記錄。
* 封存到儲存體帳戶的資料層要求保留週期，是選取 [記錄 DataPlaneRequests] 時在入口網站中設定的。 若要變更該設定，請參閱[在 Azure 入口網站中開啟記錄](#turn-on-logging-in-the-azure-portal)。


<a id="#view-in-loganalytics"></a>
## <a name="view-logs-in-log-analytics"></a>檢視 Log Analytics 中的記錄

如果您開啟記錄時選取 [傳送至 Log Analytics] 選項，集合中的診斷資料會在兩個小時內轉送到 Log Analytics。 這表示如果您開啟記錄功能後立即查看 Log Analytics，將不會看到任何資料。 只需等待兩個小時，然後再試一次。 

檢視記錄前，您應檢查確認您的 Log Analytics 工作區是否已升級為使用新的 Log Analytics 查詢語言。 若要檢查此升級，開啟 [Azure 入口網站](https://portal.azure.com)，按一下最左邊的 [Log Analytics]，然後選取工作區名稱，如下圖所示。 即會顯示如下圖中的 [OMS 工作區] 頁面。

![Azure 入口網站中的 Log Analytics](./media/logging/azure-portal.png)

如果您在 [OMS 工作區] 頁面上看到下列訊息，則您的工作區尚未升級為使用新語言。 如需升級至新查詢語言的詳細資訊，請參閱[將 Azure Log Analytics 工作區升級至新的記錄搜尋](../log-analytics/log-analytics-log-search-upgrade.md)。 

![Log Analytics 升級注意事項](./media/logging/upgrade-notification.png)

若要檢視 Log Analytics 中的診斷資料，從左側功能表或此頁面的 [管理] 區域開啟 [記錄搜尋] 頁面，如下圖所示。

![Azure 入口網站中的記錄搜尋選項](./media/logging/log-analytics-open-log-search.png)

現在您已經啟用資料收集，請使用新的查詢語言執行下列記錄搜尋範例，查看最新的十個記錄 `AzureDiagnostics | take 10`。

![take 10 記錄搜尋範例](./media/logging/log-analytics-query.png)

<a id="#queries"></a>
### <a name="queries"></a>查詢

以下是一些您可以輸入 [記錄搜尋] 方塊中的額外查詢，可協助您監視 Azure Cosmos DB 容器。 這些查詢使用[新語言](../log-analytics/log-analytics-log-search-upgrade.md)。 

若要深入了解每個記錄搜尋傳回資料的意義，請參閱[解讀 Azure Cosmos DB 記錄](#interpret)。

* 所有 Azure Cosmos DB 的診斷記錄皆在指定的時段內。

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests"
    ```

* 十個最新記錄的事件。

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | take 10
    ```

* 所有作業，依作業類型群組。

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName
    ```

* 所有作業，依資源群組。

    ```
    AzureActivity | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```

* 所有使用者活動，依資源群組。 請注意，這是活動記錄，不診斷記錄。

    ```
    AzureActivity | where Caller == "test@company.com" and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```

* 哪些作業費時超過 3 毫秒。

    ```
    AzureDiagnostics | where toint(duration_s) > 30000 and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by clientIpAddress_s, TimeGenerated
    ```

* 哪些代理程式正在執行此作業。

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName, userAgent_s
    ```

* 長時間執行的作業何時執行。

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | project TimeGenerated , toint(duration_s)/1000 | render timechart
    ```

如需有關使用新的記錄搜尋語言的詳細資訊，請參閱[了解 Log Analytics 中的記錄搜尋](../log-analytics/log-analytics-log-search-new.md)。 

## <a id="interpret"></a>解讀記錄

診斷資料儲存在 Azure 儲存體中，Log Analytics 使用非常類似的結構描述。 

下表說明每個記錄項目的內容。

| Azure 儲存體欄位或屬性 | Log Analytics 屬性 | 說明 |
| --- | --- | --- |
| 分析 | TimeGenerated | 作業發生的日期和時間 (UTC)。 |
| ResourceId | 資源 | 啟用記錄的 Azure Cosmos DB 帳戶。|
| category | 類別 | 針對 Azure Cosmos DB 記錄，DataPlaneRequests 是唯一可用的值。 |
| operationName | OperationName | 作業名稱。 這個值可以是下列任一作業：Create、Update、Read、ReadFeed、Delete、Replace、Execute、SqlQuery、Query、JSQuery、Head、HeadFeed 或 Upsert。   |
| properties | n/a | 此欄位的內容描述於下列資料列中。 |
| activityId | activityId_g | 所記錄作業的唯一 GUID。 |
| userAgent | userAgent_s | 此字串指定執行要求的用戶端使用者代理程式。 格式為 {使用者代理程式名稱}/{版本}。|
| resourceType | ResourceType | 存取的資源類型。 這個值可以是下列任一資源類型：Database、Collection、Document、Attachment、User、Permission、StoredProcedure、Trigger、UserDefinedFunction 或 Offer。 |
| StatusCode |statusCode_s | 作業的回應狀態。 |
| requestResourceId | ResourceId | 關於要求的 resourceId，根據執行的要求，可能表示 databaseRid、collectionRid 或 documentRid。|
| clientIpAddress | clientIpAddress_s | 用戶端的 IP 位址。 |
| requestCharge | requestCharge_s | 作業使用的 RU 數 |
| collectionRid | collectionId_s | 集合的唯一識別碼。|
| duration | duration_s | 以刻度為單位的作業持續時間。 |
| requestLength | requestLength_s | 以位元組為單位的要求長度。 |
| responseLength | requestLength_s | 以位元組為單位的回應長度。|
| resourceTokenUserRid | resourceTokenUserRid_s | 使用[資源權杖](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#resource-tokens)進行驗證時，此欄位是非空白值，表示使用者的資源識別碼。 |

## <a name="next-steps"></a>後續步驟

- 若要了解如何啟用記錄和各種 Azure 服務支援的計量和記錄類別目錄，請閱讀 [Microsoft Azure 中的計量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)和 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章。
- 閱讀下列文章來了解事件中樞：
   - [Azure 事件中樞是什麼？](../event-hubs/event-hubs-what-is-event-hubs.md)
   - [開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- 閱讀[從 Azure 儲存體下載計量和診斷記錄](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
- 閱讀[了解 Log Analytics 中的記錄搜尋](../log-analytics/log-analytics-log-search-new.md)
