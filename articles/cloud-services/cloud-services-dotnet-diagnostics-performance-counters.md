---
title: "在 Azure 診斷的效能計數器 aaaUse |Microsoft 文件"
description: "使用在 Azure 雲端服務或虛擬機器 toofind 瓶頸的效能計數器和調整效能。"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>在 Azure 應用程式中建立及使用效能計數器
本文說明 hello 好處，以及如何 tooput 效能計數器到 Azure 應用程式。 您可以使用它們 toocollect 資料、 找出瓶頸，並微調系統和應用程式效能。

適用於 Windows Server、 IIS 和 ASP.NET 的效能計數器也會收集與使用 Azure web 角色、 背景工作角色和虛擬機器 toodetermine hello 健全狀況。 您也可以建立和使用自訂效能計數器。  

您可以採取下列方法來檢查效能計數器資料：

1. 直接在 hello 與 hello 效能監視器 工具存取的應用程式主機上使用遠端桌面
2. 使用 System Center Operations Manager hello Azure 管理組件
3. 在含有其他監視工具存取 hello tooAzure 儲存體傳輸診斷資料。 如需詳細資訊，請參閱 [在 Azure 儲存體中儲存和檢視診斷資料](https://msdn.microsoft.com/library/azure/hh411534.aspx) 。  

如需有關監視的應用程式中 hello hello 效能[Azure 入口網站](http://portal.azure.com/)，請參閱[tooMonitor 雲端服務如何](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)。

如上建立記錄和追蹤策略，以及使用診斷和其他技術 tootroubleshoot 問題的其他詳細指引和最佳化 Azure 應用程式，請參閱[開發 azure 的疑難排解最佳作法應用程式](https://msdn.microsoft.com/library/azure/hh771389.aspx)。

## <a name="enable-performance-counter-monitoring"></a>啟用效能計數器監視
預設不會啟用效能計數器。 您的應用程式或啟動工作必須修改 hello 預設診斷代理程式設定 tooinclude hello 特定效能計數器，您希望 toomonitor 每個角色執行個體。

### <a name="performance-counters-available-for-microsoft-azure"></a>Microsoft Azure 可用的效能計數器
Azure 提供 Windows Server、 IIS 和 ASP.NET 堆疊 hello hello 可用的效能計數器的子集。 hello 下表列出一些 Azure 應用程式特別感興趣的 hello 效能計數器。

| 計數器類別：物件 (執行個體) | 計數器名稱 | 參考 |
| --- | --- | --- |
| .NET CLR 例外狀況 (全域) |# Exceps Thrown / sec |例外狀況效能計數器 |
| .NET CLR 記憶體 (全域) |記憶體回收中的時間 % |記憶體效能計數器 |
| ASP.NET |應用程式重新啟動 |ASP.NET 的效能計數器 |
| ASP.NET |要求執行時間 |ASP.NET 的效能計數器 |
| ASP.NET |中斷連接的要求 |ASP.NET 的效能計數器 |
| ASP.NET |背景工作角色處理序重新啟動 |ASP.NET 的效能計數器 |
| ASP.NET 應用程式 (**總計**) |要求總數 |ASP.NET 的效能計數器 |
| ASP.NET 應用程式 (**總計**) |要求/秒 |ASP.NET 的效能計數器 |
| ASP.NET v4.0.30319 |要求執行時間 |ASP.NET 的效能計數器 |
| ASP.NET v4.0.30319 |要求等候時間 |ASP.NET 的效能計數器 |
| ASP.NET v4.0.30319 |目前的要求 |ASP.NET 的效能計數器 |
| ASP.NET v4.0.30319 |已排入佇列的要求 |ASP.NET 的效能計數器 |
| ASP.NET v4.0.30319 |遭拒絕的要求 |ASP.NET 的效能計數器 |
| 記憶體 |可用的 MB |記憶體效能計數器 |
| 記憶體 |認可的位元組 |記憶體效能計數器 |
| 處理器(總計) |% Processor Time |ASP.NET 的效能計數器 |
| TCPv4 |連接失敗 |TCP 物件 |
| TCPv4 |Connections Established |TCP 物件 |
| TCPv4 |Connections Reset |TCP 物件 |
| TCPv4 |Segments Sent/sec |TCP 物件 |
| 網路介面(*) |Bytes Received/sec |網路介面物件 |
| 網路介面(*) |Bytes Sent/sec |網路介面物件 |
| 網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2) |Bytes Received/sec |網路介面物件 |
| 網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2) |Bytes Sent/sec |網路介面物件 |
| 網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2) |Bytes Total/sec |網路介面物件 |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>建立並新增自訂效能計數器 tooyour 應用程式
Azure 有支援 toocreate 和修改自訂效能計數器針對 web 角色和背景工作角色。 hello 計數器可能會使用的 tootrack 並監視特定應用程式的行為。 您可以用更高權限，建立和刪除啟動工作、Web 角色或背景工作角色的自訂效能計數器類別和規範。

> [!NOTE]
> 變更 toocustom 效能計數器的程式碼必須有更高的權限 toorun。 如果 hello 程式碼中的 web 角色或背景工作角色，hello 角色必須包含 hello 標記<Runtime executionContext="elevated" />hello ServiceDefinition.csdef 檔案中的 hello 角色 tooinitialize 正確。
>
>

您可以傳送自訂效能計數器資料 tooAzure 儲存體使用 hello 診斷代理程式。

hello Azure 程序會產生 hello 標準效能計數器資料。 自訂效能計數器資料必須由 Web 角色或背景工作角色應用程式建立。 請參閱[效能計數器型別](https://msdn.microsoft.com/library/z573042h.aspx)hello 資料類型的自訂效能計數器中可儲存的資訊。 如需在 Web 角色中建立及設定自訂效能計數器資料的範例，請參閱 [PerformanceCounters 範例](http://code.msdn.microsoft.com/azure/) 。

## <a name="store-and-view-performance-counter-data"></a>儲存和檢視效能計數器資料
Azure 會快取效能計數器資料與其他診斷資訊。 此資料是用於遠端監視執行 hello 角色執行個體時使用遠端桌面存取 tooview 工具，例如效能監視器。 toopersist hello hello 角色執行個體外部的資料，hello 診斷代理程式必須傳送 hello tooAzure 儲存資料。 hello hello 快取效能計數器資料的大小上限可以設定在 hello 診斷代理程式，或者可能是針對所有 hello 診斷資料，設定 toobe 共用限制的一部分。 如需設定 hello 緩衝區大小的詳細資訊，請參閱[OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx)和[DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)。 請參閱[Azure 儲存體中檢視診斷資料及進行](https://msdn.microsoft.com/library/azure/hh411534.aspx)hello 診斷代理程式 tootransfer 資料 tooa 儲存體帳戶所設定的概觀。

記錄每個設定的效能計數器執行個體的指定的取樣率，並傳送 hello 取樣資料依排程的傳輸要求或隨選傳輸要求 toohello 儲存體帳戶。 可將自動傳輸的頻率排程為每分鐘一次。 傳送 hello 診斷代理程式的效能計數器資料會儲存在資料表中，WADPerformanceCountersTable，hello 儲存體帳戶中。 使用標準 Azure 儲存體 API 方法即可存取和查詢此資料表。 請參閱[Microsoft Azure PerformanceCounters 範例](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9)查詢及顯示 hello WADPerformanceCountersTable 資料表中的效能計數器資料的範例。

> [!NOTE]
> 依據 hello 診斷代理程式的傳輸頻率和佇列延遲，hello hello 儲存體帳戶中的最新效能計數器資料可能過期幾分鐘時間。
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>使用診斷組態檔來啟用效能計數器
使用下列程序 tooenable 效能計數器，Azure 應用程式中的 hello。

## <a name="prerequisites"></a>必要條件
本節假設您擁有 hello 診斷監視器匯入您的應用程式，並加入 hello 診斷組態檔案 tooyour Visual Studio 方案 （在 SDK 2.4 和以下的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本）。 如需詳細資訊，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services-dotnet-diagnostics.md)中的步驟 1 和 2。

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>步驟 1：收集和儲存來自效能計數器的資料
加入 hello 診斷檔案 tooyour Visual Studio 方案之後，您可以設定 Azure 應用程式中的 hello 收集和儲存效能計數器資料。 這是藉由新增效能計數器 toohello 診斷檔案。 Hello 執行個體上，會先收集診斷資料，包括效能計數器。 hello 資料則保存的 toohello WADPerformanceCountersTable 資料表 hello Azure 資料表服務中，讓您將也需要 toospecify hello 應用程式中的儲存體帳戶。 如果您要在 hello 計算模擬器在本機測試您的應用程式，您也可以儲存診斷資料在本機中 hello 儲存體模擬器。 儲存診斷資料之前，您必須先前往 toohello [Azure 入口網站](http://portal.azure.com/)並建立傳統儲存體帳戶。 最佳作法是 toolocate 儲存體帳戶中的 hello Azure 應用程式的相同地理位置。 所保留的 hello Azure 應用程式和儲存體帳戶會在 hello 相同的地理位置，您避免支付外部頻寬費用並降低延遲。

### <a name="add-performance-counters-toohello-diagnostics-file"></a>新增效能計數器 toohello 診斷檔案
有許多計數器可供您使用。 hello 下列範例示範為 web 和背景工作角色監視建議的數個效能計數器。

開啟 hello 診斷檔案 （在 SDK 2.4 和以下版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本），並新增下列 toohello DiagnosticMonitorConfiguration 元素 hello:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

hello bufferQuotaInMB 屬性，指定 hello 供 hello 資料集合類型 （Azure 記錄檔、 IIS 記錄檔等） 的檔案系統儲存體數量上限。 hello 預設值為 0。 當達到 hello 配額時，加入新的資料時，會刪除 hello 最舊的資料。 所有的 hello bufferQuotaInMB 屬性 hello 總和必須大於 hello hello OverallQuotaInMB 屬性值。 決定多少儲存空間必須為 hello 收集診斷資料的更詳細討論，請參閱 < 設定 WAD 」 一節的 hello[開發 Azure 應用程式的疑難排解最佳作法](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)。

hello scheduledTransferPeriod 屬性，會指定 hello 資料傳輸的排程間隔，無條件進位 toohello 最接近的分鐘。 在 hello 遵循範例，它會設定 tooPT30M （30 分鐘）。 設定 hello 傳輸週期 tooa 小的值，例如 1 分鐘，將會對在生產環境中的應用程式的效能造成負面影響，但可以是適合用來查看快速使用，當您正在測試的診斷。 hello 排程的傳輸期間應該夠小，tooensure 診斷資料不是覆寫在 hello 的執行個體，但夠大，它不會影響應用程式的 hello 效能。

hello counterSpecifier 屬性會指定 hello 效能計數器 toocollect。 hello sampleRate 屬性會指定 hello 的 hello 效能計數器應該取樣，在此情況下 30 秒的速率。

一旦您已經新增 hello 效能計數器的 toocollect，儲存變更 toohello 診斷檔案。 接下來，您需要 hello 診斷資料會保存到 toospecify hello 儲存體帳戶。

### <a name="specify-hello-storage-account"></a>指定 hello 儲存體帳戶
您的診斷資訊 tooyour Azure 儲存體帳戶，您必須指定的 toopersist 您服務組態檔 (ServiceConfiguration.cscfg) 中的連接字串。

Azure SDK 2.5，則可以指定 hello diagnostics.wadcfgx 檔案中的 hello 儲存體帳戶。

> [!NOTE]
> 這些說明僅適用於 tooAzure SDK 2.4 和以下。 Azure SDK 2.5，則可以指定 hello diagnostics.wadcfgx 檔案中的 hello 儲存體帳戶。
>
>

tooset hello 連接字串：

1. 開啟您的儲存體使用您慣用的文字編輯器和設定 hello 連接字串 hello ServiceConfiguration.Cloud.cscfg 檔案。 hello *AccountName*和*AccountKey*值中找到 hello hello 儲存體帳戶儀表板中，在存取金鑰 底下的 Azure 入口網站。

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. 儲存 hello ServiceConfiguration.Cloud.cscfg 檔案。
3. 開啟 hello ServiceConfiguration.Local.cscfg 檔案，並確認 UseDevelopmentStorage 設定 tootrue。

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   既然 hello 連接字串已設定，您的應用程式將會在您的應用程式部署時保存診斷資料 tooyour 儲存體帳戶。
4. 儲存並建置您的專案，然後部署應用程式。

## <a name="step-2-optional-create-custom-performance-counters"></a>步驟 2：(選擇性) 建立自訂效能計數器
此外 toohello 預先定義的效能計數器，您可以加入您自己的自訂效能計數器 toomonitor web 或背景工作角色。 自訂效能計數器可能會使用的 tootrack 並監視特定應用程式的行為，可建立或刪除中啟動工作、 web 角色或背景工作角色，以更高權限。

hello Azure 診斷代理程式重新整理 hello 效能計數器組態 hello.wadcfg 檔案從一分鐘之後啟動。  如果您建立自訂效能計數器 hello OnStart 方法中，啟動工作花費超過一分鐘 tooexecute 自訂效能計數器將尚未建立時 hello Azure 診斷代理程式會嘗試 tooload 它們。  在此情況下，您會看到 Azure 診斷正確地擷取自訂效能計數器以外的所有診斷資料。  tooresolve 這個問題，請在啟動工作中建立 hello 效能計數器，或移動啟動工作的某些工作 toohello OnStart 方法之後建立 hello 效能計數器。

執行下列步驟 toocreate 簡單自訂效能計數器名為"\MyCustomCounterCategory\MyButton1Counter"hello:

1. 開啟 hello 服務定義檔 (CSDEF) 應用程式。
2. 加入 hello Runtime 項目 toohello WebRole 或 WorkerRole 元素 tooallow 執行具有提高權限：

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. 儲存 hello 檔案。
4. 開啟 hello 診斷檔案 （在 SDK 2.4 和以下版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本），並新增下列 toohello DiagnosticMonitorConfiguration hello

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. 儲存 hello 檔案。
6. 建立您的角色中的 hello OnStart 方法中的 hello 自訂效能計數器分類之前叫用基底。OnStart。 hello 下列 C# 範例會建立自訂的類別目錄中，如果不存在：

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. 更新您的應用程式中的 hello 計數器。 下列範例中的 hello 更新 Button1_Click 事件中的自訂效能計數器：

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. 儲存 hello 檔案。  

現在將由 hello Azure 診斷監視器收集自訂效能計數器資料。

## <a name="step-3-query-performance-counter-data"></a>步驟 3：查詢效能計數器資料
一旦應用程式部署和執行，hello 診斷監視器會開始收集效能計數器和保存該資料 tooAzure 存放裝置。 您在 Visual Studio 中，使用伺服器總管之類的工具[Azure 儲存體總管](http://azurestorageexplorer.codeplex.com/)，或[Azure 診斷管理員](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx)cerebrata tooview hello 效能計數器 hello 中的資料WADPerformanceCountersTable 資料表。 您可以也以程式設計方式查詢 hello 資料表服務使用[C#](../cosmos-db/table-storage-how-to-use-dotnet.md)， [Java](../cosmos-db/table-storage-how-to-use-java.md)， [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md)， [Python](../cosmos-db/table-storage-how-to-use-python.md)， [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md)，或[PHP](../cosmos-db/table-storage-how-to-use-php.md)。

hello 下列 C# 範例會顯示針對 hello WADPerformanceCountersTable 資料表的基本查詢並儲存 hello 診斷資料 tooa CSV 檔案。 一旦 hello 效能計數器儲存 tooa CSV 檔案，您可以使用 hello 繪圖 Microsoft Excel 或某些其他工具 toovisualize hello 資料中的功能。 為確定 tooadd 參考 tooMicrosoft.WindowsAzure.Storage.dll，隨附於 hello Azure SDK for.NET 年 10 月 2012年及更新版本。 hello 組件是已安裝的 toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\ 目錄。

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

實體對應 tooC # 物件使用自訂的類別衍生自**TableEntity**。 hello 下列程式碼會定義實體類別，代表效能計數器中 hello **WADPerformanceCountersTable**資料表。

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>後續步驟
[檢視有關 Azure 診斷的其他文章](../azure-diagnostics.md)
