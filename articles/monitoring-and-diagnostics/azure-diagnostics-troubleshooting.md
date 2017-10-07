---
title: "Azure 診斷 aaaTroubleshooting |Microsoft 文件"
description: "針對在 Azure 虛擬機器、Service Fabric 或 雲端服務中使用 Azure 診斷時出現的問題進行疑難排解。"
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure 診斷疑難排解
疑難排解資訊相關 toousing Azure 診斷。 如需有關 Azure 診斷的詳細資訊，請參閱 [Azure 診斷概觀](azure-diagnostics.md)。

## <a name="logical-components"></a>邏輯元件
**診斷外掛程式啟動器 (DiagnosticsPluginLauncher.exe)**： 啟動 hello Azure 診斷擴充功能。 可做為 hello 進入點程序。

**診斷外掛程式 (DiagnosticsPlugin.exe)**: hello 上述的啟動器所啟動並設定 hello 監視 」 代理程式、 啟動及管理其存留期的 Main 程序。 

**監視代理程式 (MonAgent\*.exe 處理序)**： 這些處理程序執行 hello 大量 hello 工作; 也就是監視、 集合和傳送 hello 診斷資料。  

## <a name="logartifact-paths"></a>記錄檔/構件路徑
以下是 hello 路徑 toosome 重要記錄檔和成品。 我們將參考 toothese 其餘 hello 文件的 hello:
### <a name="cloud-services"></a>雲端服務
| 構件 | 路徑 |
| --- | --- |
| **Azure 診斷組態檔** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\Config.txt |
| **記錄檔** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\ |
| **診斷資料的本機存放區** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **監視代理程式組態檔** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Azure 診斷擴充功能套件** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version> |
| **記錄集合公用程式路徑** | %SystemDrive%\Packages\GuestAgent\ |
| **MonAgentHost 記錄檔** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>虛擬機器
| 構件 | 路徑 |
| --- | --- |
| **Azure 診斷組態檔** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\RuntimeSettings |
| **記錄檔** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Logs\ |
| **診斷資料的本機存放區** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Tables |
| **監視代理程式組態檔** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MaConfig.xml |
| **狀態檔案** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Status |
| **Azure 診斷擴充功能套件** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>|
| **記錄集合公用程式路徑** | C:\WindowsAzure\Packages |
| **MonAgentHost 記錄檔** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>計量資料不會出現在 Azure 入口網站
Azure 診斷會提供一些計量資料，這些資料可以在 Azure 入口網站中顯示。 如果您有看到這些資料在入口網站中的問題，請檢查 hello 診斷儲存體帳戶]-> [WADMetrics\* toosee hello 對應度量記錄是否有資料表。 在這裡，hello PartitionKey 的 hello 資料表是 hello 資源 ID 的虛擬機器或虛擬機器規模集，而 hello RowKey hello 衡量標準名稱也就是效能計數器名稱。

如果 hello 資源識別碼不正確，請核取診斷組態]-> [度量]-> [ResourceId toosee 如果 hello 資源識別碼正確設定。

如果沒有針對 hello 特定度量資料，核取診斷組態]-> [PerformanceCounter toosee 包含 hello 公制 （效能計數器） 時。 我們會啟用下列預設計數器 hello。
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET Applications(__Total__)\Requests/Sec
- \ASP.NET Applications(__Total__)\Errors Total/Sec
- \ASP.NET\Requests Queued
- \ASP.NET\Requests Rejected
- \Processor(w3wp)\% Processor Time
- \Process(w3wp)\Private Bytes
- \Process(WaIISHost)\% Processor Time
- \Process(WaIISHost)\Private Bytes
- \Process(WaWorkerHost)\% Processor Time
- \Process(WaWorkerHost)\Private Bytes
- \Memory\Page Faults/sec
- \.NET CLR Memory(_Global_)\% Time in GC
- \LogicalDisk(C:)\Disk Write Bytes/sec
- \LogicalDisk(C:)\Disk Read Bytes/sec
- \LogicalDisk(D:)\Disk Write Bytes/sec
- \LogicalDisk(D:)\Disk Read Bytes/sec

如果 hello 組態已正確設定，但您仍然無法看到 hello 度量資料，請遵循下方的 hello 進一步調查的 hello 指導方針。


## <a name="azure-diagnostics-is-not-starting"></a>Azure 診斷未啟動
查看**DiagnosticsPluginLauncher.log**和**DiagnosticsPlugin.log** hello hello 位置的檔案在上方的原因的資訊診斷失敗 toostart 提供記錄檔。 

如果這些記錄指出 `Monitoring Agent not reporting success after launch`，則表示啟動 MonAgentHost.exe 失敗。 查看 hello 記錄檔的 hello 位置替`MonAgentHost log file`上述 hello 區段中。

hello hello 記錄檔的最後一行包含 hello 結束代碼。  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
如果您發現**負數**結束代碼，請參閱 toohello[結束程式碼資料表](#azure-diagnostics-plugin-exit-codes)在 hello[參考](#references)。

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>診斷資料均不會記錄 tooAzure 儲存體
判斷顯示任何資料，或只是某些 hello 資料未顯示。

### <a name="diagnostics-infrastructure-logs"></a>診斷基礎結構記錄檔
診斷基礎結構記錄檔是 Azure 診斷記錄任何所發生錯誤的所在位置。 請確定您已啟用 ([如何？](#how-to-check-diagnostics-extension-configuration)) 擷取診斷基礎結構記錄檔，您可以在組態和任何相關的錯誤顯示在 hello 中快速尋找`DiagnosticInfrastructureLogsTable`設定的儲存體帳戶中的資料表。

### <a name="no-data-is-showing-up"></a>未顯示任何資料
hello 完全遺失的事件資料的最常見的原因是未正確定義的儲存體帳戶資訊。

解決方法：更正診斷組態，並重新安裝診斷。

Hello 儲存體帳戶是否已正確設定的遠端桌面至 hello 機器，請確定 DiagnosticsPlugin.exe 且 MonAgentCore.exe 正在執行。 如果它們並未執行，請依照 [Azure 診斷未啟動](#azure-diagnostics-is-not-starting)中的說明進行作業。 如果 hello 處理序正在執行、 跳過[會取得在本機擷取資料](#is-data-getting-captured-locally)依本指南從該處。

### <a name="part-of-hello-data-is-missing"></a>遺漏 hello 資料的一部分
如果您正在取得某些資料，但沒有取得其他資料。 這表示 hello 資料收集/傳輸管線已正確設定。 請遵循 hello 小節 toonarrow 下有什麼 hello 問題如下：
#### <a name="is-collection-configured"></a>是否已設定集合： 
診斷組態包含 hello 指示資料 toobe 收集特定類型的組件。 [檢閱您的設定](#how-to-check-diagnostics-extension-configuration)toomake 確定不想要資料您未設定的集合。
#### <a name="is-hello-host-generating-data"></a>Hello 主機會將產生的資料：
- **效能計數器**： 開啟 perfmon，然後檢查 hello 計數器。
- **追蹤記錄檔**： 遠端桌面連接到 hello VM，並加入 TextWriterTraceListener toohello 應用程式的組態檔。  請參閱 http://msdn.microsoft.com/library/sk36c28t.aspx tooset 向上 hello 文字接聽程式。  請確定 hello`<trace>`項目具有`<trace autoflush="true">`。<br />
如果您沒有看到系統正在產生追蹤記錄檔，請依照[關於遺漏追蹤記錄檔的詳細資訊](#more-about-trace-logs-missing)中的說明進行作業。
- **ETW 追蹤**： 遠端桌面連接到 hello VM 並安裝 PerfView。  在 PerfView 中執行 [File] \(檔案\) -> [User Command] \(使用者命令\) -> Listen etwprovder1,etwprovider2,etc。請注意，hello 接聽命令會區分大小寫 hello 以逗號分隔清單中的 ETW 提供者之間不能有空格。  Toorun hello 命令時，您可以按一下 hello 右下方的 hello Perfview 工具 toosee 嘗試的 toorun 和哪些 hello 結果中的 hello 'Log' 按鈕。  假設 hello 輸入正確接著在新視窗會顯示在幾秒鐘的時間和您將開始看到 ETW 追蹤。
- **事件記錄檔**： 遠端桌面連接到 hello VM。 開啟`Event Viewer`，並確定 hello 的事件。
#### <a name="is-data-getting-captured-locally"></a>是否正在本機擷取資料：
接下來請確定取得在本機擷取 hello 資料。
hello 資料會在本機儲存在`*.tsf`檔案[hello 診斷資料的本機存放區](#log-artifacts-path)。 不同的 `.tsf` 檔案會收集不同類型的記錄。 hello 名稱會位於 azure 儲存體中的類似 toohello 資料表名稱。 例如，`PerformanceCountersTable.tsf`中會收集 `Performance Counters`，`WindowsEventLogsTable.tsf` 中會收集事件記錄檔。 使用中的 hello 指示[本機記錄檔擷取](#local-log-extraction)區段 tooopen hello 選本機收集檔案，並確定您會看到它們在磁碟上開始收集。

如果您不要參閱記錄檔以取得在本機收集，並已經有確認 hello 主機會將產生的資料之後，您可能需要在組態問題。 檢閱您仔細的 hello 適當章節的組態。 同時檢閱 hello 組態產生 MonitoringAgent [MaConfig.xml](#log-artifacts-path) ，並確定沒有描述 hello 相關的記錄檔來源，並不會遺失在 azure 診斷組態之間的轉譯區段和監視的代理程式設定。
#### <a name="is-data-getting-transferred"></a>是否正在傳輸資料：
如果您已確認取得在本機擷取 hello 資料，但您仍然看它在儲存體帳戶： 
- 首先和最重要，請確定您已提供正確的儲存體帳戶，而且您有不回復透過指定儲存體帳戶金鑰 etc.for hello。 針對雲端服務，我們發現使用者有時候並未更新他們的 `useDevelopmentStorage=true`。
- 如果提供的儲存體帳戶正確。 請確定您沒有不允許 hello 元件 tooreach 公用儲存體端點一些網路限制。 其中一種方式是 tooremote 桌面連入 hello 的 toodo 電腦並再試一次 toowrite 一些 toohello 相同的儲存體帳戶自己。
- 最後，您可以嘗試及查看監視代理程式報告了哪些失敗項目。 監視代理程式會將其記錄檔`maeventtable.tsf`位於[hello 診斷資料的本機存放區](#log-artifacts-path)。 遵循指示[本機記錄檔擷取](#local-log-extraction)區段 tooopen 這個檔案，再找出是否有`errors`指出失敗 tooread 本機檔案或寫入 toostorage。

### <a name="capturing--archiving-logs"></a>擷取/封存記錄檔
您瀏覽 hello 上述步驟，但是無法了解什麼錯誤而且思考連絡支援人員。 hello 可能會要求您的第一件事是 toocollect 記錄檔從您的電腦。 您可以先自行執行該作業以節省時間。 執行 hello`CollectGuestLogs.exe`公用程式在[記錄集合公用程式路徑](#log-artifacts-path)hello 中產生的所有相關的 azure 記錄檔的 zip 檔案相同的資料夾。

## <a name="diagnostics-data-tables-not-found"></a>找不到診斷資料資料表
使用下列程式碼的 hello 來命名保存 ETW 事件的 Azure 儲存體中的 hello 資料表：

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

下列是一個範例：

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
產生的 4 個資料表如下︰

| Event | 資料表名稱 |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>參考

### <a name="how-toocheck-diagnostics-extension-configuration"></a>如何 toocheck 診斷延伸模組組態
hello 最簡單的方式 toocheck 延伸模組組態是 toonavigate toohttp://resources.azure.com，巡覽 toohello 虛擬機器或雲端服務上的 hello Azure 診斷擴充功能 (IaaSDiagnostics / PaaDiagnostics) 是有問題。

或者，遠端桌面連接到 hello 電腦並查看 hello Azure 診斷組態檔一節所述 hello 適當[這裡](#log-artifacts-path)。

在任一案例搜尋**Microsoft.Azure.Diagnostics**然後 hello **xmlCfg**或**WadCfg**欄位。 

發生虛擬機器，如果 hello WadCfg 欄位已存在，表示已在 JSON 中的 hello 組態。 如果 hello xmlCfg 欄位存在時，它表示 hello 組態是以 XML 格式，而且會 base64 編碼。 您需要[將它解碼](http://www.bing.com/search?q=base64+decoder)toosee hello 診斷所載入的 XML。

雲端服務角色，如果挑選 hello 組態從磁碟 hello 資料是 base64 編碼，因此您需要太[將它解碼](http://www.bing.com/search?q=base64+decoder)toosee hello 診斷所載入的 XML。

### <a name="azure-diagnostics-plugin-exit-codes"></a>Azure 診斷外掛程式結束代碼
hello 外掛程式傳回下列結束代碼的 hello:

| 結束代碼 | 說明 |
| --- | --- |
| 0 |成功。 |
| -1 |一般錯誤。 |
| -2 |無法 tooload hello rcf 檔案。<p>Hello 客體代理程式外掛程式啟動器手動叫用，不正確，hello VM 時，應該才會發生這個內部錯誤。 |
| -3 |無法載入 hello 診斷組態檔。<p><p>解決方法：因組態檔未通過結構描述驗證而造成。 hello 解決方案是 tooprovide 符合 hello 結構描述的組態檔。 |
| -4 |監視代理程式診斷的 hello 的另一個執行個體已在使用 hello 本機資源目錄。<p><p>解決方法：為 **LocalResourceDirectory** 指定其他值。 |
| -6 |hello 客體代理程式外掛程式啟動器嘗試以無效的命令列 toolaunch 診斷。<p><p>Hello 客體代理程式外掛程式啟動器手動叫用，不正確，hello VM 時，應該才會發生這個內部錯誤。 |
| -10 |hello 診斷外掛程式會結束並發生未處理的例外狀況。 |
| -11 |hello 客體代理程式已無法 toocreate hello 程序負責啟動及監視 hello 監視代理程式。<p><p>解決方案： 確認系統資源不足，無法使用 toolaunch 新處理序。<p> |
| -101 |無效的引數呼叫 hello 診斷外掛程式時。<p><p>Hello 客體代理程式外掛程式啟動器手動叫用，不正確，hello VM 時，應該才會發生這個內部錯誤。 |
| -102 |hello 外掛程式程序是無法 tooinitialize 本身。<p><p>解決方案： 確認系統資源不足，無法使用 toolaunch 新處理序。 |
| -103 |hello 外掛程式程序是無法 tooinitialize 本身。 尤其，它是無法 toocreate hello 記錄器物件。<p><p>解決方案： 確認系統資源不足，無法使用 toolaunch 新處理序。 |
| -104 |提供的 hello 客體代理程式無法 tooload hello rcf 檔案。<p><p>Hello 客體代理程式外掛程式啟動器手動叫用，不正確，hello VM 時，應該才會發生這個內部錯誤。 |
| -105 |hello 診斷外掛程式無法開啟 hello 診斷組態檔。<p><p>Hello 診斷外掛程式手動叫用，不正確，hello VM 時，應該才會發生這個內部錯誤。 |
| -106 |無法讀取 hello 診斷組態檔。<p><p>解決方法：因組態檔未通過結構描述驗證而造成。 Hello 方案是 tooprovide 符合 hello 結構描述的組態檔。 請參閱[如何 toocheck 診斷延伸模組組態](#how-to-check-diagnostics-extension-configuration)。 |
| -107 |監視代理程式的 hello 資源目錄傳遞 toohello 無效。<p><p>如果 hello 監視代理程式手動叫用時，不正確，hello VM 上，應該只會發生此內部錯誤。</p> |
| -108 |無法 tooconvert hello 診斷組態檔至 hello 監視代理程式設定檔。<p><p>Hello 診斷外掛程式會使用無效的組態檔手動叫用時，應該才會發生這個內部錯誤。 |
| -110 |一般診斷組態錯誤。<p><p>Hello 診斷外掛程式會使用無效的組態檔手動叫用時，應該才會發生這個內部錯誤。 |
| -111 |無法 toostart hello 監視代理程式。<p><p>解決方法：確認有足夠的系統資源可用。 |
| -112 |一般錯誤 |

### <a name="local-log-extraction"></a>本機記錄檔擷取
hello 監視代理程式收集記錄檔和成品為`.tsf`檔案。 您無法讀取 `.tsf` 檔案，但可以將它轉換成 `.csv`，如下所示： 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
新的檔案稱為`<relevantLogFile>.csv`中就會建立 hello 相同路徑做為對應 hello`.tsf`檔案。

**請注意**： 您只需要 toorun hello 主要 tsf 檔案 (例如 PerformanceCountersTable.tsf) 針對此公用程式。 hello 隨附的檔案 (例如 PerformanceCountersTables_\*\*001.tsf，PerformanceCountersTables_\*\*002.tsf 等) 會自動處理。

### <a name="more-about-trace-logs-missing"></a>關於遺漏追蹤記錄檔的詳細資訊

**注意：**這大部分也適用於 toocloud 服務只除非您已設定 hello DiagnosticsMonitorTraceListener IaaS VM 上執行的應用程式。 

- 請確定已設定 DiagnosticMonitorTraceListener hello web.config 或 app.config 中的 hello。這在雲端服務專案中，預設設定，但有些客戶註解它不足導致 hello 追蹤陳述式 toonot 收集的診斷。 
- 如果記錄檔不會從 hello OnStart] 或 [執行方法來取得寫入請確定 hello DiagnosticMonitorTraceListener 處於 hello app.config。根據預設，它會在 hello web.config 中，但僅適用於的 toocode w3wp.exe; 內執行因此您必須在 app.config toocapture 追蹤 WaIISHost.exe 中執行。
- 請確定您使用的是 Diagnostics.Trace.TraceXXX，而不是 Diagnostics.Debug.WriteXXX。  hello 偵錯陳述式將會移除從發行的組建。
- 請確定 hello 編譯程式碼確實具有 hello Diagnostics.Trace 行 （使用 Reflector、 ildasm 或 ILSpy tooverify）。  Diagnostics.Trace 命令會從 hello 編譯二進位檔中移除，除非您使用 hello 追蹤條件式編譯符號。  如果使用 msbuild toobuild hello 專案這是常見的問題 toorun 到。

## <a name="known-issues-and-mitigations"></a>已知問題與緩解方式
以下是已知問題和緩解方式的清單：

**1. .NET 4.5 相依性：**

WAD 在 .NET 4.5 Framework 或更新版本上具有執行階段相依性。 在撰寫這個 hello 時，佈建雲端服務，以及所有官方 azure 虛擬機器基底映像的所有機器具有.NET 4.5 或上面已安裝。 不過仍可能 tooland 您試著 toorun WAD 在的電腦不需要.NET 4.5 或更新版本的情況下它。 當您從舊映像或快照集建立電腦，或攜帶自己的自訂磁碟時，就可能會發生這個問題。

執行 DiagnosticsPluginLauncher.exe 時，這通常會以結束代碼 **255** 來表示。 失敗發生因為 toohello 未處理的例外狀況： 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**緩解方式：**在電腦上安裝 .NET 4.5 或更新版本。

**2.儲存體中有效能計數器資料，但入口網站中沒有顯示**

虛擬機器入口網站體驗預設會顯示特定效能計數器。 如果您沒有看到它們，而且您知道會取得產生 hello 資料，因為它是用於儲存體。 勾選：
- 如果儲存體中的 hello 資料以英文計數器名稱。 如果 hello 計數器名稱不是英文，入口網站的度量圖表將不會無法 toorecognize 它。
- 如果您使用萬用字元 (\*) 在您的效能計數器的名稱，hello 入口網站將無法能 toocorrelate hello 設定和收集計數器。

**風險降低**： 變更 hello 機器語言 tooEnglish 系統帳戶。 控制台-> 地區-> 系統管理-> 複製設定-> 取消選取 「 歡迎畫面和系統帳戶 」，以便 hello 自訂語言不會套用 toosystem 帳戶。 也請確定您是否入口 toobe 您主要的耗用量的經驗不使用萬用字元。
