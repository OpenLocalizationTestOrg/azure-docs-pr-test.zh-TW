---
title: "aaaEnabling hello Azure 入口網站中的儲存體度量 |Microsoft 文件"
description: "如何儲存體度量 tooenable hello Blob、 佇列、 表格和檔案服務"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>啟用 Azure 儲存體計量和檢視計量資料
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>概觀
當您建立新的儲存體帳戶時，預設會啟用「儲存體計量」。 您可以設定監視透過 hello [Azure 入口網站](https://portal.azure.com)或 Windows PowerShell 或以程式設計方式透過其中一個 hello 儲存體用戶端程式庫。

您可以設定 hello 度量資料的保留期限： 此期間決定多久 hello 儲存體服務可以維持 hello 度量，並且您 hello 空間需要的 toostore 費用它們。 一般而言，您應該於每小時度量的每分鐘度量使用較短的保留期限因為 hello 重大的額外空間所需的每分鐘度量。 您應該選擇的保留期限，您有足夠時間 tooanalyze hello 資料，並下載您想 tookeep 供離線分析或報告之用的任何度量。 請記住，您還是必須支付從儲存體帳戶下載度量資料的費用。

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>如何使用 tooenable 度量 hello Azure 入口網站
請遵循這些步驟 tooenable 中的計量 hello [Azure 入口網站](https://portal.azure.com):

1. 瀏覽 tooyour 儲存體帳戶。
1. 選取**診斷**上 hello**功能表**刀鋒視窗
1. 請確認**狀態**設定得**上**。
1. 選取 hello hello 服務的度量，您需要 toomonitor。
1. 指定保留原則 tooindicate 多久 tooretain 度量和記錄資料。
1. 選取 [ **儲存**]。

請注意該 hello [Azure 入口網站](https://portal.azure.com)目前無法讓您 tooconfigure 分鐘度量，在儲存體帳戶; 您必須啟用分鐘度量使用 PowerShell 或以程式設計的方式。

## <a name="how-tooenable-metrics-using-powershell"></a>如何使用 PowerShell tooenable 度量
您可以使用 hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 目前的設定，儲存體帳戶中使用 PowerShell 在您本機電腦 tooconfigure 儲存體度量和 hello cmdletSet-azurestorageservicemetricsproperty toochange hello 目前設定。

控制儲存體度量的 hello cmdlet 使用下列參數的 hello:

* MetricsType：可能值為 Hour 和 Minute。
* ServiceType：可能值為 Blob、Queue 及 Table。
* MetricsLevel：可能值為 None、服務，以及 ServiceAndApi。

例如，hello 下列命令會開啟分鐘 hello hello 保留期限預設儲存體帳戶中的 Blob 服務的度量設定 toofive 天：

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

hello comando siguiente recupera hello 目前每小時度量層級和保留天數的預設儲存體帳戶中的 hello blob 服務：

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

如需如何 tooconfigure hello Azure PowerShell cmdlet toowork 您 Azure 訂用帳戶及如何 tooselect hello 預設儲存體帳戶 toouse 資訊，請參閱：[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="how-tooenable-storage-metrics-programmatically"></a>如何 tooenable 儲存體度量以程式設計的方式
hello 下列 C# 程式碼片段顯示如何 tooenable 度量和記錄 hello Blob 服務使用 hello 儲存體用戶端程式庫適用於.NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>檢視儲存體度量
設定儲存體分析度量 toomonitor 儲存體帳戶之後，儲存體分析會記錄在一組已知資料表儲存體帳戶中的 hello 度量。 您可以在 hello 設定圖表 tooview 每小時度量[Azure 入口網站](https://portal.azure.com):

1. 瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。
1. 選取**度量**在 hello**功能表**刀鋒視窗中的 hello 服務其計量想 tooview。
1. 選取**編輯**想 tooconfigure hello 圖表上。
1. 在 hello**編輯圖表**刀鋒視窗中，選取 hello**時間範圍**，**圖表類型**，和您想要顯示 hello 圖表中的 hello 度量。
1. 選取 [確定]

如果您想 toodownload hello 度量的長期存放裝置或 tooanalyze 它們在本機，您必須：

* 使用會察覺這些資料表，並將 tooview 可讓您和下載這些工具。
* 撰寫自訂的應用程式或指令碼 tooread 和 hello 資料表儲存。

許多協力廠商儲存體瀏覽工具會察覺這些資料表，並讓您 tooview 它們直接。
如需可用工具的清單，請參閱 [Azure 儲存體用戶端工具](storage-explorers.md)。

> [!NOTE]
> 從 0.8.0 版的 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)，您可以檢視和下載 hello 分析度量資料表。
> 
> 

順序 tooaccess hello 分析中的資料表以程式設計的方式，請注意是否您列出儲存體帳戶中的所有 hello 資料表 hello 分析資料表不會出現。 您可以直接透過名稱，存取它們，或使用 hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello.NET 用戶端程式庫 tooquery hello 資料表名稱中。

### <a name="hourly-metrics"></a>每小時度量
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>每分鐘度量
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>容量
* $MetricsCapacityBlob

您可以找到 hello 結構描述的完整詳細資料，在這些資料表[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)。 以下的 hello 範例資料列僅顯示部分 hello 可用的資料行，但說明 hello 方式儲存體度量會儲存這些度量的一些重要功能：

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Availability | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

此範例中的每分鐘度量資料，hello 資料分割索引鍵會使用分鐘解析 hello 時間。 hello 資料列索引鍵識別 hello hello 資料列中儲存的資訊類型，這資訊、 hello 存取類型和 hello 要求類型之兩個部分所組成：

* 使用者或系統，其中使用者是指 tooall 使用者要求 toohello 儲存體服務，而系統會參考儲存體分析所做的 toorequests hello 存取類型。
* hello 要求類型是所有在此情況下它可能摘要行，或者它會識別例如 QueryEntity 或 UpdateEntity hello 特定 API。

所有 hello 如上 hello 範例資料記錄 （從上午 11:00 開始） 的一分鐘，QueryEntities 要求因此 hello 數目加上 hello QueryEntity 要求數目加上 hello UpdateEntity 要求數目加總 tooseven，是 hello 總上所顯示hello user: All 資料列。 同樣地，您可以藉由計算衍生 hello 平均端對端延遲 104.4286 hello user: All 資料列上的 ((143.8 * 5) + 3 + 9) / 7。

## <a name="metrics-alerts"></a>計量警示
您應該考慮設定警示 hello [Azure 入口網站](https://portal.azure.com)讓儲存體度量自動通知您重要的儲存體服務的 hello 行為的變更。 如果您使用儲存體總管工具 toodownload 此度量資料分隔的格式，您可以使用 Microsoft Excel tooanalyze hello 資料。 如需可用的儲存體總管工具清單，請參閱 [Azure 儲存體用戶端工具](storage-explorers.md)。 您可以設定警示 hello**警示規則**刀鋒視窗中，存取**監視**hello 儲存體帳戶功能表刀鋒視窗中。

> [!IMPORTANT]
> 可能的儲存體事件與 hello 對應每小時或分鐘度量資料時就會記錄之間的延遲。 中的每分鐘度量 hello 案例中，可能會一次寫入幾分鐘的資料。 這會導致 tootransactions 進行彙總 hello 交易 hello 目前的分鐘到幾分鐘。 當發生這種情況時，服務可能沒有 hello 的所有可用的度量資料的 hello 警示設定警示的間隔，可能會導致非預期地引發 tooalerts。
>

## <a name="accessing-metrics-data-programmatically"></a>以程式設計方式存取度量資料
hello 下列清單顯示範例 C# 程式碼可存取某幾分鐘的 hello 分鐘度量，並且會顯示在主控台視窗中的 hello 結果。 它會使用 hello Azure 儲存體程式庫第 4 版包含 hello CloudAnalyticsClient 類別，可簡化存取儲存體中的 hello 度量資料表。

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>當您啟用儲存體度量時，會產生哪些費用？
寫入要求 toocreate 資料表實體的度量資訊會收費 hello 標準費率適用 tooall Azure 儲存體作業。

由用戶端 toometrics 資料的讀取與刪除要求也是標準費率計費。 如果您已設定資料保留原則，就不需要在 Azure 儲存體刪除舊的度量資料時付費。 不過，如果您刪除分析資料，您的帳戶則需支付 hello 刪除作業。

hello 度量資料表所使用的 hello 容量也會列入計費： 您可以使用下列用來儲存度量資料的容量 tooestimate hello 數量的 hello:

* 如果每小時的服務會利用每項服務中的每個 API，大約 148KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用服務和應用程式開發介面層級摘要。
* 如果每小時的服務會利用每項服務中的每個 API，大約 12KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用只服務層級摘要。
* hello blob 的容量資料表有兩個資料列加入每一天 （提供的記錄檔的使用者已選擇加入）： 這表示，此資料表的每日 hello 大小增加總 tooapproximately 300 個位元組。

## <a name="next-steps"></a>後續步驟
[啟用儲存體記錄和存取記錄檔資料](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
