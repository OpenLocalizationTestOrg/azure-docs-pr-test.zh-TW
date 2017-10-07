---
title: "aaaAzure 偵錯工具 Insights 快照集應用程式的.NET 應用程式 |Microsoft 文件"
description: "在生產環境 .NET 應用程式中擲回例外狀況時，會自動收集偵錯快照集"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>.NET 應用程式中的例外狀況偵錯快照集

發生例外狀況時，您可以自動從即時 Web 應用程式收集偵錯快照集。 hello 快照顯示 hello 狀態的原始程式碼和變數在 hello 時刻 hello 例外狀況已擲回。 hello 快照偵錯工具 （預覽） 中[Azure Application Insights](app-insights-overview.md)監視 web 應用程式的例外狀況遙測。 在頂端擲回的例外狀況中，以便您擁有 hello 您需要在生產環境中的 toodiagnose 問題的資訊，它會收集快照集。 包含 hello[快照集收集器 NuGet 套件](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中，並選擇性地設定集合中的參數[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。快照會顯示在[例外狀況](app-insights-asp-net-exceptions.md)hello Application Insights 入口網站中。

您可以檢視 hello 入口 toosee hello 呼叫堆疊中的偵錯快照集，然後檢查每個呼叫堆疊框架的變數。 tooget 功能更強大的偵錯體驗，與程式碼中，開啟快照集，與 Visual Studio 2017 企業[hello 快照偵錯工具擴充功能下載適用於 Visual Studio](https://aka.ms/snapshotdebugger)。

快照集集合適用於：
* 執行 .NET Framework 4.5 或更新版本的 .NET Framework 和 ASP.NET 應用程式。
* 在 Windows 上執行的 .NET Core 2.0 和 ASP.NET Core 2.0 應用程式。

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>設定 ASP.NET 應用程式的快照集集合

1. 如果您尚未這麼做，請[在 Web 應用程式中啟用 Application Insights](app-insights-asp-net.md)。

2. 包含 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。 

3. 檢閱 hello hello 太加入封裝的預設選項[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. 只有在例外狀況會報告的 tooApplication Insights 收集快照集。 在某些情況下 （例如，hello.NET 平台的較舊版本），您可能需要過[設定例外狀況收集](app-insights-asp-net-exceptions.md#exceptions)toosee 例外狀況，其 hello 入口網站中的快照集。


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>設定 ASP.NET Core 2.0 應用程式的快照集集合

1. 如果您尚未這麼做，請[在 ASP.NET Core Web 應用程式中啟用 Application Insights](app-insights-asp-net-core.md)。

2. 包含 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。

3. 修改 hello`ConfigureServices`應用程式中的方法`Startup`類別 tooadd hello 快照集收集器的遙測處理器。 應加入的 hello 程式碼取決於 hello 參考 hello Microsoft.ApplicationInsights.ASPNETCore NuGet 封裝版本。

   對於 Microsoft.ApplicationInsights.AspNetCore 2.1.0，新增：
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   對於 Microsoft.ApplicationInsights.AspNetCore 2.1.1，新增：
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>設定其他 .NET 應用程式的快照集集合

1. 如果您的應用程式已不使用 Application Insights 檢測，以開始使用[啟用 Application Insights 和設定 hello 檢測金鑰](app-insights-windows-desktop.md)。

2. 新增 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。

3. 只有在例外狀況會報告的 tooApplication Insights 收集快照集。 您可能需要 toomodify 程式碼 tooreport 它們。 hello 例外狀況處理程式碼主要取決於應用程式的 hello 結構，但是範例如下：
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>授與權限

Hello Azure 訂用帳戶的擁有者可以檢查快照集。 其他使用者必須由擁有者授與權限。

toogrant 權限，指派 hello`Application Insights Snapshot Debugger`角色 toousers 人員將會檢查快照集。 Tooindividual 使用者或群組由 hello 目標 Application Insights 資源的訂用帳戶擁有者或其資源群組或訂用帳戶，可以指派這個角色。

1. 開啟 hello 存取控制 (IAM) 分頁。
1. 按一下 hello + 新增 按鈕。
1. 從 hello 角色下拉式清單中選取應用程式 Insights 快照偵錯工具。
1. 搜尋並輸入 hello 使用者 tooadd 的名稱。
1. 按一下 hello 儲存按鈕 tooadd hello 使用者 toohello 角色。


[!IMPORTANT]
    快照集可能會在變數和參數值中包含個人和其他機密資訊。

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>偵錯 hello Application Insights 入口網站中的快照集

如果快照集是用於指定的例外狀況或問題識別碼、**開啟偵錯快照集**按鈕是否出現在 hello[例外狀況](app-insights-asp-net-exceptions.md)hello Application Insights 入口網站中。

![例外狀況的 [開啟偵錯快照集] 按鈕](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

在 [hello 偵錯快照檢視中，您會看到呼叫堆疊] 和 [變數] 窗格。 當您選取在 hello 呼叫堆疊 窗格中堆疊框架的 hello 呼叫、 您可以檢視本機變數和參數，該函式呼叫 hello 變數 窗格中。

![Hello 入口網站中的檢視進行偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

快照集可能包含機密資訊，依預設為不可檢視。 tooview 快照集，您必須擁有 hello `Application Insights Snapshot Debugger` tooyou 指派角色。

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Visual Studio 2017 Enterprise 的偵錯快照集
1. 按一下 hello**下載快照集**按鈕 toodownload`.diagsession`檔案，可以開啟 Visual Studio 2017 Enterprise。 

2. tooopen hello`.diagsession`檔案中，您必須先[下載並安裝 Visual Studio hello 快照 Debugger extension](https://aka.ms/snapshotdebugger)。

3. 開啟 hello 快照集檔案之後，Visual Studio 中的 hello 小型傾印偵錯頁面隨即出現。 按一下**偵錯 Managed 程式碼**toostart 偵錯 hello 快照集。 hello 快照開啟 toohello 其中 hello 擲回例外狀況，讓您可以偵錯 hello hello 程序目前狀態的程式碼行。

    ![檢視 Visual Studio 中的偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

hello 下載快照集包含您的 web 應用程式伺服器找不到任何符號檔。 這些符號檔案是含有原始程式碼的必要的 tooassociate 快照集資料。 當您發行 web 應用程式時，App Service 應用程式，請確定 tooenable 符號部署。

## <a name="how-snapshots-work"></a>快照集運作方式

當您的應用程式啟動時，會建立個別的快照集上傳者程序，可針對快照集要求監視應用程式。 要求快照集時，執行程序的 hello 的陰影複製會以大約 10 個 too20 分鐘為單位。 然後分析 hello 陰影程序，並建立同時 hello 主要處理序會繼續 toorun，及做流量 toousers 快照集。 hello 快照集則以及任何相關符號 (.pdb) 檔上傳的 tooApplication Insights 需要 tooview hello 快照集。

## <a name="current-limitations"></a>目前的限制

### <a name="publish-symbols"></a>發佈符號
hello 快照偵錯工具需要符號檔 hello 實際執行伺服器 toodecode 變數和 tooprovide Visual Studio 中的偵錯經驗。 hello 15.2 版本的 Visual Studio 2017 發佈符號發行組建的預設發佈之後 tooApp 服務。 在舊版中，您需要 tooadd hello 下列行 tooyour 發行設定檔`.pubxml`檔案，所以會發行在發行模式中的符號：

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

針對 Azure 計算和其他類型，請確定 hello 符號檔位於 hello hello 主應用程式.dll 的相同的資料夾 (通常`wwwroot/bin`) 或可用 hello 目前路徑上。

### <a name="optimized-builds"></a>最佳化的組建
在某些情況下，本機變數無法檢視版本 」 組建中因為 hello 建置程序期間套用的最佳化。

## <a name="troubleshooting"></a>疑難排解

這些提示可協助您疑難排解問題 hello 快照偵錯工具。

### <a name="verify-hello-instrumentation-key"></a>確認 hello 檢測金鑰

請確定您在已發行應用程式中使用 hello 正確的檢測金鑰。 通常，Application Insights 會從 hello ApplicationInsights.config 檔案讀取 hello 檢測金鑰。 請確認 hello 值為 hello 相同為 hello Application Insights 資源，請參閱 hello 入口網站中的 hello 檢測金鑰。

### <a name="check-hello-uploader-logs"></a>請檢查 hello 上載程式記錄檔

建立快照集之後，磁碟上會建立小型傾印檔案 (.dmp)。 個別上載程序會採用該小型傾印檔案，並將它，以及任何相關聯的 Pdb tooApplication Insights 快照偵錯工具的儲存體上傳。 Hello 小型傾印已上傳成功之後，它會從磁碟中刪除。 hello hello 小型傾印上載程式記錄檔會保留在磁碟上。 在 App Service 環境中，您可以在 `D:\Home\LogFiles\Uploader_*.log` 中找到這些記錄。 使用 hello Kudu 管理網站的應用程式服務 toofind 這些記錄檔。

1. Hello Azure 入口網站中開啟您的 App Service 應用程式。

2. 選取 hello**進階工具**刀鋒視窗中或搜尋**Kudu**。
3. 按一下 [執行]。
4. 在 hello**偵錯主控台**下拉式清單方塊中，選取**CMD**。
5. 按一下 [LogFiles]。

您應會看到至少有一個檔案的名稱開頭為 `Uploader_` 且副檔名為 `.log`。 按一下 hello 合適的圖示 toodownload 任何記錄檔，或在瀏覽器中開啟它們。
hello 檔案名稱包含 hello 機器名稱。 如果 App Service 執行個體裝載於一部以上的電腦，每部電腦會有個別的記錄檔。 當 hello 上載程式偵測到新的小型傾印檔案時，它會記錄在 hello 記錄檔。 以下是成功上傳的範例︰

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

Hello 前一個範例中的 hello 檢測金鑰是`c12a605e73c44346a984e00000000000`。 這個值應該符合您的應用程式的 hello 檢測金鑰。
hello 小型傾印是相關聯的快照集識別碼 hello `139e411a23934dc0b9ea08a626db16c5`。 您可以使用此識別碼更新 toolocate hello 相關聯的應用程式 Insights 分析中的例外狀況遙測。

hello 上載程式會掃描一次每隔 15 分鐘有關新的 Pdb。 以下是範例：

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

應用程式_不_裝載在 App Service 中，hello 上載程式記錄檔位於 hello hello 小型傾印與相同的資料夾： `%TEMP%\Dumps\<ikey>` (其中`<ikey>`是您的檢測金鑰)。

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>使用 Application Insights 搜尋 toofind 例外狀況，其快照集

建立快照集時，擲回例外狀況的 hello 會標記為快照集識別碼。 報告的 tooApplication Insights hello 例外狀況遙測時，該快照集識別碼會當做自訂屬性。 使用 Application Insights 中的 hello 搜尋刀鋒視窗，您可以找到以 hello 的所有遙測`ai.snapshot.id`自訂屬性。

1. 瀏覽 tooyour hello Azure 入口網站中的 Application Insights 資源。
2. 按一下 [搜尋] 。
3. 型別`ai.snapshot.id`在 hello 搜尋 文字方塊中，然後按 Enter 鍵。

![搜尋具有快照集識別碼 hello 入口網站中的遙測](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

此搜尋會不傳回任何結果，如果沒有快照集已回報的 tooApplication Insights hello 選取時間範圍內的應用程式。

toosearch hello 上載程式記錄檔，從特定的快照集識別碼 hello 搜尋方塊中輸入該識別碼。 如果您找不到已上傳快照集的遙測，請遵循下列步驟：

1. 請仔細檢查您所看到的 hello 右 Application Insights 資源 hello 檢測金鑰進行驗證。

2. 使用 hello 上載程式記錄檔中的 hello 時間戳記，調整的 hello 搜尋 toocover hello 時間範圍篩選該時間範圍。

如果仍然沒有看到該快照集識別碼例外狀況，hello 例外狀況遙測未回報的 tooApplication 深入資訊。 如果您的應用程式當機之後花費 hello 快照集，但 hello 例外狀況遙測報告它之前，可能會發生這種情況。 在此情況下，請檢查應用程式服務會記錄下的 hello `Diagnose and solve problems` toosee 如果發生非預期重新啟動或未處理例外狀況。

## <a name="next-steps"></a>後續步驟

* [在您的程式碼中設定 snappoints](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget 快照集，而不需等待例外狀況。
* [診斷 web 應用程式中的例外狀況](app-insights-asp-net-exceptions.md)說明如何 toomake 詳細例外狀況顯示 tooApplication 深入資訊。 
* [智慧型偵測](app-insights-proactive-diagnostics.md)會自動探索效能異常。
