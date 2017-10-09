---
title: "aaaEnabling hello Azure 入口網站中的儲存體度量 |Microsoft 文件"
description: "如何儲存體度量 tooenable hello Blob、 佇列、 表格和檔案服務"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>啟用儲存體度量和檢視度量資料
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>概觀
當您建立新的儲存體帳戶時，預設會啟用「儲存體計量」。 您可以設定監視使用任一 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，Windows PowerShell 或透過儲存體 API 以程式設計的方式。

當您啟用儲存體度量時，您必須選擇 hello 資料的保留期限： 此期間決定多久 hello 儲存體服務可以維持 hello 度量，並且您 hello 空間需要的 toostore 費用它們。 一般而言，您應該於每小時度量的每分鐘度量使用較短的保留期限因為 hello 重大的額外空間所需的每分鐘度量。 您應該選擇的保留期限，您有足夠時間 tooanalyze hello 資料，並下載您想 tookeep 供離線分析或報告之用的任何度量。 請記住，您還是必須支付從儲存體帳戶下載度量資料的費用。

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>如何使用 tooenable 儲存體度量 hello Azure 傳統入口網站
在 [hello [Azure 傳統入口網站](https://manage.windowsazure.com)，您用於儲存體度量的儲存體帳戶 toocontrol hello 設定] 頁面。 如需監視，您可以針對每個 Blob、資料表和佇列設定層級和保留期限 (以天為單位)。 在每個案例中，hello 層級是 hello 下列其中一種：

* 關閉 - 不會收集任何度量。
* 最少 — 儲存體度量 」 會收集一組基本度量，例如輸入/輸出、 可用性、 延遲和成功百分比 hello Blob、 資料表和佇列服務彙總。
* 詳細資訊，完整設定的度量，包括儲存體度量收集 hello 每個儲存體程式開發介面作業的相同度量資訊，除了 toohello 服務等級度量。 詳細資訊度量可供進一步分析在應用程式運作期間發生的問題。

請注意，hello Azure 傳統入口網站目前無法讓您 tooconfigure 分鐘度量，在儲存體帳戶。您必須啟用分鐘度量使用 PowerShell 或以程式設計的方式。

## <a name="how-tooenable-storage-metrics-using-powershell"></a>如何使用 PowerShell tooenable 儲存體度量
您可以使用 hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 目前的設定，儲存體帳戶中使用 PowerShell 在您本機電腦 tooconfigure 儲存體度量和 hello cmdletSet-azurestorageservicemetricsproperty toochange hello 目前設定。

控制儲存體度量的 hello cmdlet 使用下列參數的 hello:

* MetricsType 的可能值為 Hour 和 Minute。
* ServiceType 的可能值為 Blob、Queue 及 Table。
* MetricsLevel 可能的值為 None (hello Azure 傳統入口網站中的對等 tooOff)，服務 (hello Azure 傳統入口網站中的對等 tooMinimal) 和 ServiceAndApi (hello Azure 傳統入口網站中的對等 tooVerbose)。

例如，hello 下列命令會開啟分鐘 hello hello 保留期限預設儲存體帳戶中的 blob 服務的度量設定 toofive 天：

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
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
當您已設定儲存體度量 toomonitor 儲存體帳戶時，它會記錄一組已知資料表中儲存體帳戶中的 hello 度量。 可供在圖表上，您可以使用儲存體帳戶中 hello Azure 傳統入口網站 tooview hello 每小時度量 hello [監視] 頁面。 這個頁面上 hello Azure 傳統入口網站中，您可以：

* 選取 hello 圖表上的度量 tooplot （可用度量的 hello 選擇將取決於您選擇了 hello hello 設定 頁面上的服務的詳細資訊還是最小監控）。
* 選取 hello hello 度量 hello 圖表上顯示的時間範圍。
* 選擇 toouse 絕對或相對比例 tooplot hello 度量資訊。
* 設定電子郵件警示 toonotify 時的特定度量達到特定的值。

如果您想要 toodownload hello 度量長期的儲存體或 tooanalyze 它們在本機，您將需要 toouse 工具或撰寫一些程式碼 tooread hello 資料表。 您必須下載 hello 分鐘度量以供分析。 如果您列出所有 hello 資料表儲存體帳戶中，但您可以直接透過名稱存取這些 hello 資料表不會出現。 許多協力廠商儲存體瀏覽工具會察覺這些資料表，並讓您 tooview 它們直接 (請參閱 hello 部落格文章[Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)取得一份可用的工具)。

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

您應該考慮 hello [監視] 頁面上的 hello Azure 傳統入口網站中的警示設定儲存體度量自動通知您任何的儲存體服務的 hello 行為的重要變更。如果您使用儲存體總管工具 toodownload 此度量資料分隔的格式，您可以使用 Microsoft Excel tooanalyze hello 資料。 請參閱 hello 部落格文章[Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)取得一份可用的儲存體總管工具。

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

## <a name="next-steps"></a>後續步驟：
[啟用儲存體分析記錄和存取記錄檔資料](https://msdn.microsoft.com/library/dn782840.aspx)
