---
title: "使用 Application Insights 在 Azure 上的 aaaProfiling 即時 web 應用程式 |Microsoft 文件"
description: "低耗用量分析工具找出您的 web 伺服器程式碼中的 hello 最忙碌路徑。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>使用 Application Insights 來分析即時 Azure Web Apps

Application Insights 的這項功能在應用程式服務為 GA，在 Compute 為預覽中。

找出多少時間的即時 web 應用程式中的每個方法中使用程式碼剖析工具的 hello [Azure Application Insights](app-insights-overview.md)。 它會顯示詳細的設定檔的即時應用程式所服務的要求，並反白顯示 hello ' 最忙碌路徑' 使用 hello 最多時間。 它會自動選取具有不同回應時間的範例。 hello 分析工具會使用各種技術 toominimize 額外負荷。

hello 分析工具目前適用於 ASP.NET web 應用程式執行於 Azure 應用程式服務，在至少 hello 基本定價層。 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>啟用 hello 程式碼剖析工具

在程式碼中[安裝 Application Insights](app-insights-asp-net.md)。 如果已安裝，請確定您擁有 hello 最新版本。 (toodo，以滑鼠右鍵按一下方案總管] 中的專案，然後選擇 [管理 NuGet 封裝。 選取 [更新] 並更新所有套件)。重新部署應用程式。

您使用的是 ASP.NET Core 嗎？[請查看這裡](#aspnetcore)。

在[https://portal.azure.com](https://portal.azure.com)，開啟您的 web 應用程式的 hello Application Insights 資源。 開啟 [效能] 然後按一下 [啟用 Application Insights 分析工具...]。

![按一下 在橫幅中 hello 啟用程式碼剖析工具][enable-profiler-banner]

或者，您隨時可以按一下**設定**tooview 狀態、 啟用或停用 hello 程式碼剖析工具。

![在 hello 效能刀鋒視窗中，按一下 設定][performance-blade]

使用 Application Insights 設定的 Web Apps 會列在 [設定] 刀鋒視窗。 請依照下列指示 tooinstall hello 程式碼剖析工具代理程式有需要。 如果尚未使用 Application Insights 設定任何 Web 應用程式，請按一下 [新增連結的應用程式]。

使用 hello*啟用程式碼剖析工具*或*停用分析工具*hello 設定刀鋒視窗 toocontrol 按鈕 hello 所有連結的 web 應用程式的程式碼剖析工具。



![設定刀鋒視窗][linked app services]

toostop 或重新啟動 hello profiler 個別的應用程式服務執行個體，您會發現它**hello App Service 資源中**，請在**Web 工作**。 toodelete 它查看**延伸**。

![停用 web 作業的分析工具][disable-profiler-webjob]

我們建議您擁有 hello 分析工具在所有您 web 應用程式 toodiscover 任何效能問題儘速上啟用。

如果您使用 WebDeploy toodeploy 變更 tooyour web 應用程式，請確定您排除 hello **App_Data**在部署期間刪除的資料夾。 否則 hello 延伸模組程式碼剖析工具檔案將會刪除當您下次部署 hello web 應用程式 tooAzure。

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>使用分析工具搭配 Azure VM 和 Compute 資源 (預覽)

當您[在執行階段啟用 Azure App Service 的 Application Insights](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights) 時，分析工具會自動提供使用。 (如果您已啟用 Application Insights hello 資源，您可能需要透過 hello tooupdate toohello lates 版本**設定**精靈。)

沒有[預覽版的 Azure 計算資源的程式碼剖析工具 hello](https://go.microsoft.com/fwlink/?linkid=848155)。


## <a name="limits"></a>限制

hello 預設資料保留為 5 天。 每日擷取最多 10 GB。

沒有 hello 分析工具服務需付費。 您的 web 應用程式必須裝載在至少 hello 基本層的應用程式服務。

## <a name="viewing-profiler-data"></a>檢視分析工具的資料

開啟 hello 效能刀鋒視窗，然後向下的捲動 toohello 作業清單。




![Application Insights 的 [效能] 刀鋒視窗 [範例] 資料行][performance-blade-examples]

hello hello 資料表中的資料行如下：

* **計數**-hello hello 的 hello 刀鋒視窗的時間範圍中這些要求的數目。
* **中位數**-hello 一般應用程式會採用 toorespond tooa 要求的時間。 在所有的回應中，有一半會快過此時間。
* **第 95 個百分位數** - 95% 的回應會快過此時間。 如果此圖中的 hello 中間值大不相同，可能是您的應用程式發生間歇性問題。 (或者，可能的解釋為有某者設計功能導致此結果，例如快取)。
* **範例**-圖示表示該 hello profiler 擷取這項作業的堆疊追蹤。

按一下 [hello 範例圖示 tooopen hello 追蹤總管]。 hello 總管 中顯示已捕捉 hello 程式碼剖析工具的數個範例，分類依回應時間。

選取範例 tooshow 時間花費在執行 hello 的要求的程式碼層級細分。

![Application Insights 追蹤總管][trace-explorer]

**顯示 最忙碌路徑**開啟 hello 最大的分葉節點，或至少是關閉。 在大部分情況下此節點會相鄰 tooa 效能瓶頸。



* **標籤**: hello 的 hello 函式或事件的名稱。 hello 樹狀會顯示混合的程式碼和 （如 SQL 和 http 的事件） 發生的事件。 hello 最上層事件代表 hello 整體要求持續時間。
* **經過**: hello hello hello 作業開始 hello 結束之間的時間間隔。
* **當**： 顯示 hello 函式/事件執行關聯 tooother 函式中時。

## <a name="how-tooread-performance-data"></a>如何 tooread 效能資料

Microsoft 服務程式碼剖析工具會使用取樣方法和檢測 tooanalyze hello 應用程式效能的組合。
正在進行詳細的集合時，服務程式碼剖析工具範例 hello 指令指標的每個每毫秒中的 hello 機器的 CPU。
每個範例會擷取目前執行中，提供詳細的有用的資訊，該怎麼辦，執行緒做了這兩種最高和最低層級的抽象概念的 hello 執行緒 hello 完整呼叫堆疊。 服務程式碼剖析工具也會收集其他事件，例如內容切換的事件，TPL 事件和執行緒集區事件 tootrack 活動相互關聯及因果。

hello hello 時間表檢視中顯示的呼叫堆疊是 hello 的上述取樣和檢測 hello 結果。 因為每個範例會擷取 hello 執行緒 hello 完整呼叫堆疊，它會包含從 hello.NET framework 中，當您參考其他架構的程式碼。

### <a id="jitnewobj"></a>物件配置 (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1` 是 .NET Framework 內的 Helper 函式，可從 Managed 堆積來配置記憶體。 系統在配置物件時會叫用 `clr!JIT\_New`。 系統在配置物件陣列時則會叫用 `clr!JIT\_Newarr1`。 這兩個函式的速度通常很快，應該不會花上多少時間。 如果您看到`clr!JIT\_New`或`clr!JIT\_Newarr1`製作時間表大量時間，就表示 hello 程式碼可能是配置許多物件和耗用大量的記憶體。

### <a id="theprestub"></a>載入程式碼 (`clr!ThePreStub`)
`clr!ThePreStub`是 helper 函式會準備 hello 程式碼 tooexecute hello 第一次的.NET framework 內。 這通常包括但不限於 JIT (Just In Time) 編譯。 每個 C# 方法`clr!ThePreStub`應叫用的處理序 hello 存留期間最多一次。

如果您看到`clr!ThePreStub`會花費相當大量的要求的時間，它會指出該要求是 hello 執行該方法和.NET framework 執行階段 tooload，方法是重要的 hello 時間的第一個。 您可以考慮執行 hello 程式碼的該部分的使用者存取權，或考慮您的組件上執行 NGen 之前準備程序。

### <a id="lockcontention"></a>鎖定爭用 (`clr!JITutil\_MonContention` 或 `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`或`clr!JITutil\_MonEnterWorker`表示 hello 目前執行緒正在等候釋放鎖定 toobe。 系統在執行 C# 鎖定陳述式、叫用 Monitor.Enter 方法或以 MethodImplOptions.Synchronized 屬性叫用方法時，常會出現此情形。 當執行緒 A 會在取得鎖定，和執行緒 B 會嘗試 tooacquire hello 相同鎖定的執行緒釋放它之前，通常是鎖定爭用。

### <a id="ngencold"></a>載入程式碼 (`[COLD]`)
如果 hello 方法名稱包含`[COLD]`，例如`mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`，則表示該 hello.NET framework 執行階段執行所未最佳化的程式碼<a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">特性指引最佳化</a>hello 第一次。 每個方法，它應該顯示 hello 處理序 hello 存留期間最多一次。

如果載入程式碼會花很長的時間的要求，就表示該要求 hello 第一個 tooexecute hello 最佳化的一部分 hello 方法。 您可以考慮您的使用者存取權限才能執行 hello 程式碼的該部分的程序暖機。

### <a id="httpclientsend"></a>傳送 HTTP 要求
這類方法`HttpClient.Send`表示 hello 程式碼正在等候 HTTP 要求 toocomplete。

### <a id="sqlcommand"></a>資料庫作業
例如 SqlCommand.Execute 方法表示資料庫作業 toocomplete 正在等待 hello 程式碼。

### <a id="await"></a>等候 (`AWAIT\_TIME`)
`AWAIT\_TIME`指出 hello 程式碼等候另一個工作 toocomplete。 這通常會發生在 C# 'await' 陳述式。 Hello 程式碼執行時以 C# 'await'、 hello 執行緒會回溯控制 toohello 執行緒集區，並傳回沒有遭到封鎖而等待 hello 'await' toofinish 沒有執行緒。 不過，以邏輯方式 hello，未 hello await '封鎖' hello 作業 toocomplete 正在等候的執行緒。 `AWAIT\_TIME`表示等候 hello 工作 toocomplete hello 封鎖時間。

### <a id="block"></a> 封鎖的時間
`BLOCKED_TIME`表示可以使用，例如等待同步處理物件、 使用，或等候要求 toofinish 執行緒 toobe 正在等候另一個資源 toobe 正在等待 hello 程式碼。

### <a id="cpu"></a>CPU 時間
hello CPU 忙於執行 hello 指示。

### <a id="disk"></a>磁碟時間
hello 應用程式正在執行磁碟作業。

### <a id="network"></a>網路時間
hello 應用程式正在執行網路作業。

### <a id="when"></a>何時資料行
這是收集節點 hello 內含樣本的會隨著時間的視覺效果。 hello 總 hello 要求的範圍分為 32 時間貯體，而該節點的 hello 內含樣本會累積到這些 32 個值區。 接著，每個值區會以長條來表示，而長條的高度則代表換算後的值。 節點標示`CPU_TIME`或`BLOCKED_TIME`，或當耗用的資源 (cpu、 磁碟、 執行緒) 的明顯關聯性時，hello 列代表 hello 段時間的貯體中使用這些資源的其中一個。 若您耗用多項資源，這些計量會大於 100%。 例如，通常來說，如果您在某個期間內使用兩個 CPU，計量會是 200%。


## <a id="troubleshooting"></a>疑難排解

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>如何知道 Application Insights 分析工具是否有執行？

hello 分析工具會執行以 Web 應用程式中的連續 web 工作。 您可以在 https://portal.azure.com 開啟 hello Web 應用程式資源，並檢查 hello WebJobs 刀鋒視窗中的"ApplicationInsightsProfiler 」 狀態。 如果它不執行中，開啟**記錄**toofind 深入了解。

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>為什麼找不到任何堆疊範例即使 hello 分析工具執行？

您可以檢查以下幾點。

1. 確定 Web App Service 方案服務方案至少是基本層。
2. 確定 Web 應用程式至少已啟用 Application Insights SDK 2.2 Beta 版。
3. 請確定您的 Web 應用程式具有 hello APPINSIGHTS_INSTRUMENTATIONKEY 設定以 hello 使用相同的檢測金鑰的 Application Insights SDK。
4. 確定 Web 應用程式是在 .Net Framework 4.6 上執行。
5. 如果是 ASP.NET Core 應用程式，也請[hello 所需的相依性](#aspnetcore)。

Hello 程式碼剖析工具啟動之後，沒有 hello 分析工具目前正在收集數個效能追蹤簡短熱身期間。 之後，hello 分析工具會收集每個小時內的兩分鐘的效能追蹤。  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>我之前使用的是 Azure Service Profiler。 哪些情形的 tooit？  

當您啟用 Application Insights Profiler 時，Azure Service Profiler 代理程式就會停用。

### <a id="double-counting"></a>平行執行緒重複計算

在某些情況下 hello hello 堆疊檢視器中的總時間度量大於 hello hello 要求的實際持續時間。

當某個要求有兩個以上的關聯執行緒以平行方式運作時，就會發生這種情形。 hello 執行緒總時間大於然後 hello 經過的時間。 在許多情況下一個執行緒可能會等候 hello 其他 toocomplete。 這個 hello 檢視器會嘗試 toodetect 和省略 hello 認為不重要的等候，但顯示太多而不是省略可能重要資訊的 hello 一邊方面會發生錯誤。  

在您的追蹤中看到的平行執行緒，您會需要 toodetermine 的執行緒正在等候，因此您可以判斷 hello hello 要求的關鍵路徑。 在大部分情況下，快速地進入等候狀態是只等待 hello 執行緒 hello 其他執行緒。 一開始可集中在 hello 其他項目，並忽略 hello hello 的等候中執行緒的時間。

### <a id="issue-loading-trace-in-viewer"></a>沒有分析資料

1. 如果您嘗試 hello 資料 tooview 會超過幾週，請嘗試限制時間篩選，再試一次。

2. 核取，proxy 或防火牆沒有封鎖存取 toohttps://gateway.azureserviceprofiler.net。

3. 請檢查您應用程式中使用的檢測金鑰為 Application Insights hello 相同 hello Application Insights 資源，您已啟用透過程式碼剖析為該 hello。 hello 索引鍵通常是 ApplicationInsights.config，但也可以在 web.config 或 app.config 中找到。

### <a name="error-report-in-hello-profiling-viewer"></a>Hello 設定檔檢視器中的錯誤報表

提出支援票證從 hello 入口網站。 請附上 hello 從 hello 錯誤訊息的相互關聯識別碼。

## <a name="manual-installation"></a>手動安裝

當您設定 hello 程式碼剖析工具時，hello 下列更新是作 toohello Web 應用程式的設定。 如果您的環境需要，您能以手動方式自行執行它們，例如，如果應用程式在 Azure App Service Environment (ASE) 中執行︰

1. 在 hello web 應用程式控制項刀鋒視窗中，開啟 設定。
2. 設定 「.Net Framework 版本"toov4.6。
3. 設定 「 永遠開啟 」 tooOn。
4. 新增應用程式設定"__APPINSIGHTS_INSTRUMENTATIONKEY__"和集 hello 值 toohello hello SDK 使用相同的檢測金鑰。
5. 開啟 [進階工具]。
6. 按一下"Go"tooopen hello Kudu 網站。
7. 在 hello Kudu 網站，選取 「 網站擴充功能 」。
8. 從資源庫安裝 "__Application Insights__"。
9. 重新啟動 hello web 應用程式。

## <a id="aspnetcore"></a>ASP.NET Core 支援

ASP.NET Core 應用程式需要 tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget 封裝 2.1.0-beta6 或更高版本 toowork 以 hello 程式碼剖析工具。 我們在 6/27/2017年之後不再支援 hello 較低版本。

## <a name="next-steps"></a>後續步驟

* [在 Visual Studio 中使用 Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
