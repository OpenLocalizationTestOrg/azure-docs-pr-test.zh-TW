---
title: "aaaBest 作法和疑難排解指南的 node 應用程式，Azure Web 應用程式"
description: "了解 hello 最佳作法和疑難排解步驟的 node 應用程式，Azure Web 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Azure Web Apps 上節點應用程式的最佳作法和疑難排解指南
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

在本文中，您將學習 hello 最佳作法和疑難排解步驟[node 應用程式](app-service-web-get-started-nodejs.md)Azure Webapps 上執行 (與[iisnode](https://github.com/azure/iisnode))。

> [!WARNING]
> 請小心在您的生產網站上使用疑難排解步驟。 建議是 tootroubleshoot 上的應用程式非實際執行安裝程式，例如您預備位置和 hello 問題固定的當交換生產位置與您預備網站。
> 
> 

## <a name="iisnode-configuration"></a>IISNODE 組態
這[結構描述檔案](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml)顯示所有可設定為 iisnode hello 設定。 適用於您的應用程式的 hello 設定包括：

* nodeProcessCountPerApplication
  
    此設定會控制每個 IIS 應用程式所啟動的節點處理序的 hello 數目。 預設值為 1。 藉由設定此 too0，您可以為您 VM 的核心計數啟動許多 node.exe。 建議的值為 0，大部分的應用程式，讓您可以利用 hello 核心的所有電腦上。 Node.exe 是單一執行緒，因此一個 node.exe 會耗用最多 1 核心及 tooget 最大效能的應用程式節點您會想 tooutilize 所有核心。
* nodeProcessCommandLine
  
    此設定會控制 hello 路徑 toohello node.exe。 您可以設定此值 toopoint tooyour node.exe 版本。
* maxConcurrentRequestsPerProcess
  
    此設定會控制 hello iisnode tooeach node.exe 所傳送的並行要求數目上限。 在 azure 的 webapps hello 這個的預設值為無限。 您不會有 tooworry 有關這項設定。 Azure 的 webapps 外 hello 預設值為 1024年。 您可能想的 tooconfigure 這根據要求數目，您的應用程式會取得和您的應用程式處理每個要求的速度。
* maxNamedPipeConnectionRetry
  
    此設定會控制 hello 的次數 iisnode 會重試上 hello toonode.exe 透過具名管道 toosend hello 要求讓連線數目上限。 搭配 namedPipeConnectionRetryDelay 此設定會決定 hello iisnode 內每個要求的總逾時。 在 Azure Web Apps 上預設值為 200。 總逾時 (秒) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    透過具名管道的 hello 每個重試 toosend 要求 toonode.exe 之間將等候的時間 （毫秒） iisnode 這個設定控制項 hello 量。 預設值為 250 毫秒。
    總逾時 (秒) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    根據預設，在 azure webapps iisnode hello 總逾時是 200 \* 250ms = 50 秒。
* logDirectory
  
    此設定會控制 hello 目錄 iisnode 記錄 stdout/stderr 的位置。 預設值是 iisnode 即相對 toohello 主要指令碼目錄 (directory where 主要立即轉譯 server.js 時)
* debuggerExtensionDll
  
    此設定會控制 iisnode 在進行節點應用程式偵錯時，將使用的節點偵測器版本。 目前 iisnode-偵測器-0.7.3.dll 和 iisnode inspector.dll 有效值 hello 只有 2，這項設定。 預設值為 iisnode-inspector-0.7.3.dll。 iisnode-偵測器-0.7.3.dll 版本會使用節點-偵測器-0.7.3，和使用 websockets，因此您需要 tooenable websockets azure webapp toouse 上這個版本。 請參閱<http://www.ranjithr.com/?p=98>如需有關如何 tooconfigure iisnode toouse hello 新的節點偵測器。
* flushResponse
  
    其會緩衝回應 too4MB 資料之前清除，亦即，或直到 hello 回應 hello 結束，何者較早 hello IIS 的預設行為。 iisnode 提供組態設定 toooverride 這種行為： tooflush hello 回應實體本文的片段項目一旦 iisnode 接收來自 node.exe，您需要 tooset hello iisnode/@flushResponse web.config too'true 中的屬性 ':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    啟用 排清的 hello 回應實體本文的每個片段會將 hello hello 系統輸送量降低 (as of v0.1.13) 的 5%的效能負擔，所以最佳 tooscope 需要回應資料流 （例如使用 hello 這個設定只有 tooendpoints<location> hello web.config 中的項目)
  
    在加法 toothis 串流處理應用程式，您需要 tooalso 組 responseBufferLimit 您 iisnode 處理常式 too0。
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    這是以分號分隔的檔案清單，系統將監看其變更。 變更 tooa 檔案會導致 hello 應用程式 toorecycle。 每個項目包含選擇性的目錄名稱再加上必要的檔案名稱，也就是相對 toohello hello 主應用程式進入點所在的目錄。 中 hello 檔案名稱部分只允許使用萬用字元。 預設值為 “\*.js;web.config”
* recycleSignalEnabled
  
    預設值為 false。 如果啟用，您的 node 應用程式可以連接 tooa 具名管道 (環境變數 IISNODE\_控制項\_管道)，並傳送 「 資源回收 」 訊息。 這會導致 hello w3wp toorecycle 依正常程序。
* idlePageOutTimePeriod
  
    預設值為 0，這表示已停用此功能。 當設定 toosome 值大於 0，iisnode 將移出其所有子分頁處理每隔 'idlePageOutTimePeriod' 毫秒。 toounderstand 頁面外方式套用，請參閱 toothis[文件](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx)。 這項設定將會適用於應用程式會耗用大量的記憶體，而且想要將 toopageout 記憶體 toodisk 偶爾 toofree 向上某些 RAM。

> [!WARNING]
> 啟用 hello 遵循上實際執行應用程式的組態設定時，請務必小心。 建議的做法是 toonot 即時的實際執行應用程式上啟用它們。
> 
> 

* debugHeaderEnabled
  
    hello 預設值為 false。 如果設定 tootrue，iisnode 會將 HTTP 回應標頭 iisnode 偵錯 tooevery HTTP 回應傳送嗨 iisnode 偵錯標頭值會是 URL。 可以證明的診斷資訊的各個部分，藉由查看 hello URL 片段，但更佳的視覺效果達成 hello 瀏覽器中開啟 hello URL。
* loggingEnabled
  
    此設定會控制所 iisnode hello 記錄 stdout 和 stderr。 Iisnode 會擷取 stdout/stderr 從節點處理序，它會啟動，並將寫入 toohello hello 'p' 設定中指定的目錄。 一旦啟用，您的應用程式將會寫入記錄檔 toohello 檔案系統，並根據 hello hello 應用程式所完成的記錄數量，可能是效能的影響。
* devErrorsEnabled
  
    預設值為 false。 當設定 tootrue，iisnode 將會顯示 hello HTTP 狀態碼和 Win32 錯誤碼在您的瀏覽器。 hello win32 程式碼將有助於偵錯特定類型的問題。
* debuggingEnabled (請勿在實際生產網站上啟用)
  
    此設定會控制偵錯功能。 Iisnode 會與節點偵測器整合。 藉由啟用此設定，即可啟用節點應用程式的偵錯功能。 一旦啟用此設定，iisnode 會配置 hello 必要的節點偵測器中的檔案 'debuggerVirtualDir' 目錄 hello 第一個偵錯要求 tooyour node 應用程式。 您可以藉由傳送要求 toohttp://yoursite/server.js/debug 載入 hello 節點偵測器。 您可以使用 'debuggerPathSegment' 設定控制 hello 偵錯 URL 區段。 根據預設，debuggerPathSegment=’debug’。 使其更加困難 toobe 探索到的其他人，您可以設定此 tooa GUID 的範例。
  
    如需偵錯詳細資訊，請查看此 [連結](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) 。

## <a name="scenarios-and-recommendationstroubleshooting"></a>案例和建議/疑難排解
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>我的節點應用程式進行太多的輸出呼叫。
許多應用程式會做為其一般作業的一部分想 toomake 傳出連接。 例如，要求時，節點應用程式會想 toocontact REST API 的其他位置及某些資訊 tooprocess hello 要求。 Http 或 https 的呼叫時，您會想 toouse 保持運作的代理程式。 例如，您可以使用 hello agentkeepalive 模組與您保持運作的代理程式，這些輸出呼叫時。 這可確保 hello 通訊端重複使用在您的 azure webapp VM 及建立新的通訊端，為每個傳出要求的降低 hello 額外負荷。 此外，這可確保您使用許多輸出要求，因此您不超過每個 VM 配置的 hello maxSockets 通訊端 toomake 減少數。 建議的 Azure Webapps 是 tooset hello agentKeepAlive maxSockets 值 tooa 總計的每個 VM 的 160 通訊端。 這表示如果您有 4 node.exe hello VM 上執行，您會想 tooset hello agentKeepAlive maxSockets too40 每也就是每個 VM 的總 160 node.exe。

範例 [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) 設定：

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

這個範例假設您有 4 個 node.exe 在 VM 上執行。 如果您有不同數目的 node.exe hello VM 上執行，您必須 toomodify hello maxSockets 據此設定。

### <a name="my-node-application-is-consuming-too-much-cpu"></a>我的節點應用程式目前耗用太多 CPU。
您可能會在您的入口網站上取得 Azure Web Apps 建議的高 cpu 耗用量。 您也可以安裝監視 toowatch 某些[度量](web-sites-monitor.md)。 當檢查 hello hello CPU 使用量[Azure 入口網站儀表板](../application-insights/app-insights-web-monitor-performance.md)，請檢查 cpu hello 最大值，因此不會錯過出 hello 尖峰值。
在您認為您的應用程式耗用太多的 CPU，您無法解釋的情況下，您需要 tooprofile 應用程式節點。

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>在 Azure Web Apps 上使用 V8 分析工具剖析節點應用程式
例如，假設讓您可擁有您想 tooprofile，如下所示為 hello world 應用程式：

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

移 tooyour scm 網站 https://yoursite.scm.azurewebsites.net/DebugConsole

您會看到命令提示字元，如下所示。 進入 site/wwwroot 目錄

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

執行 npm 安裝 v8 分析工具 」 hello 命令

這應會在 node\_modules 目錄與其所有的相依項目之下安裝 v8 分析工具。
現在，編輯您的應用程式立即轉譯 server.js tooprofile。

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

變更上述 hello 會分析 hello WriteConsoleLog 函式，然後撰寫 hello 設定檔輸出 too'profile.cpuprofile' 站台 wwwroot 下的檔案。 傳送要求 tooyour 應用程式。 您會在您的網站 wwwroot 下看到所建立的 'profile.cpuprofile' 檔案。

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

下載此檔案，而您將需要 tooopen Chrome F12 工具這個檔案。 在 chrome 上叫用 F12，然後按一下 hello 「 設定檔索引標籤 」。 按一下 [載入] 按鈕。 選取您剛下載的 profile.cpuprofile 檔案。 按一下您剛載入的 hello 設定檔。

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

您會看到 95%的 hello 時間所耗用 WriteConsoleLog 函式，如下所示。 這也會顯示 hello 確切的行號和原始程式檔，會造成 hello 問題。

### <a name="my-node-application-is-consuming-too-much-memory"></a>我的節點應用程式目前耗用太多記憶體。
您可能會在您的入口網站上取得 Azure Web Apps 建議的高記憶體耗用量。 您也可以安裝監視 toowatch 某些[度量](web-sites-monitor.md)。 當檢查 hello hello 的記憶體使用量[Azure 入口網站儀表板](../application-insights/app-insights-web-monitor-performance.md)，請檢查 hello 記憶體最大值，因此不會錯過出 hello 尖峰值。

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>node.js 的流失偵測和堆積區分
您可以使用[節點 memwatch](https://github.com/lloyd/node-memwatch) toohelp 識別記憶體流失。
您可以在應用程式中安裝 memwatch 如同 v8 分析工具和編輯您程式碼 toocapture 和差異堆積 tooidentify hello 記憶體流失的問題。

### <a name="my-nodeexes-are-getting-killed-randomly"></a>我的 node.exe 會隨機終止
發生這種情況有幾個原因︰

1. 您的應用程式會擲回無法攔截例外狀況 – 請核取 d:\\家用\\LogFiles\\應用程式\\hello 詳細資料上 hello 擲回的例外狀況記錄 errors.txt 檔案。 此檔案具有 hello 堆疊追蹤，以便修正根據這個應用程式。
2. 您的應用程式耗用太多記憶體，近而讓其他處理序無法開始執行。 如果關閉 too100%hello VM 的記憶體總數，無法清除您 node.exe hello 程序管理員 toolet 由其他處理程序取得機會 toodo 一些工作。 toofix，請確定您的應用程式表示並未流失記憶體，或如果您的應用程式確實需要 toouse 大量的記憶體，請向上擴充 tooa 較大的 VM、 更多 RAM。

### <a name="my-node-application-does-not-start"></a>我的節點應用程式並未啟動
如果您的應用程式在啟動時傳回 500 錯誤，可能有幾個原因︰

1. Node.exe 不存在於 hello 正確的位置。 檢查 nodeProcessCommandLine 設定。
2. 在 hello 正確位置，不存在主要指令碼檔案。 檢查 web.config 並確定 hello 名稱 hello 主要指令碼檔案中進行 hello 處理常式區段相符項目 hello 主要指令碼檔案。
3. Web.config 設定不正確-請檢查 hello 設定名稱/值。
4. 冷啟動-您的應用程式所花費太長 toostartup。 如果您的應用程式所花的時間大於 (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 秒，則 iisnode 會傳回 500 錯誤。 增加您的應用程式啟動時間 tooprevent iisnode 逾時並傳回 hello 500 錯誤從這些設定 toomatch hello 值。

### <a name="my-node-application-crashed"></a>我的節點應用程式毀損
您的應用程式會擲回無法攔截例外狀況 – 請核取 d:\\家用\\LogFiles\\應用程式\\hello 詳細資料上 hello 擲回的例外狀況記錄 errors.txt 檔案。 此檔案具有 hello 堆疊追蹤，以便修正根據這個應用程式。

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>我的 node 應用程式採用 （冷啟動） 太多時間 toostartup
最常見的原因是 hello 應用程式有許多檔案中的 hello 節點\_模組和 hello 應用程式嘗試 tooload 大部分在啟動期間，這些檔案。 根據預設，因為您的檔案位於 hello 網路共用上 Azure Webapps 載入太多檔案可能需要一些時間。
某些解決方案 toomake 這速度是：

1. 請確定您使用 npm3 tooinstall 模組有一般相依性結構，而且沒有重複的相依性。
2. 您的節點再次嘗試 toolazy 負載\_模組，不會載入所有 hello 模組在啟動時。 這表示當您確實需要時，應該完成該 hello 呼叫 toorequire('module') hello 函式內再次嘗試 toouse hello 模組。
3. Azure Web Apps 會提供稱為本機快取的功能。 這項功能將從 hello 網路共用 toohello 本機磁碟上 hello VM 複製您的內容。 由於本機 hello 檔案，所以 hello 的節點載入\_模組會更快。 -此[文件](../app-service/app-service-local-cache.md)說明如何 toouse 本機快取中的更詳細說明。

## <a name="iisnode-http-status-and-substatus"></a>IISNODE http 狀態和子狀態
這[原始程式檔](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h)所有 hello 可能的狀態/子狀態組合 iisnode 可能會發生錯誤時都傳回的清單。

啟用您應用程式 toosee hello win32 錯誤碼 FREB （請確定您啟用 FREB 只在非實際執行的網站，基於效能的考量）。

| Http 狀態 | Http 子狀態 | 可能的原因？ |
| --- | --- | --- |
| 500 |1000 |時發生分派 hello 要求 tooIISNODE 一些問題 – 請檢查 是否啟動 node.exe。 Node.exe 可能在啟動時損毀。 檢查 web.config 組態是否有錯誤。 |
| 500 |1001 |-Win32Error 0x2-應用程式沒有回應 toohello URL。 請檢查 URL 重寫規則，或如果您快速的應用程式必須定義 hello 正確路由。 -Win32Error 0x6d – 具名管道忙碌 – Node.exe 不接受要求，因為 hello 管道忙碌中。 檢查高 CPU 使用量。 - 其他錯誤 – 檢查 node.exe 是否毀損。 |
| 500 |1002 |Node.exe 損毀 – 檢查 d:\\home\\LogFiles\\logging-errors.txt 中的堆疊追蹤。 |
| 500 |1003 |管道組態有問題 – 您絕不應該看見這，但如果您這樣做，hello 具名管道組態不正確。 |
| 500 |1004-1018 |傳送來自 node.exe hello 要求或處理 hello 回應時發生一些錯誤。 檢查 node.exe 是否損毀。 檢查 d:\\home\\LogFiles\\logging-errors.txt 中的堆疊追蹤。 |
| 503 |1000 |沒有足夠的記憶體 tooallocate 更具名管道連接。 檢查您的應用程式為何使用這麼多的記憶體。 檢查 maxConcurrentRequestsPerProcess 設定值。 如果它並不無限的而且您有許多要求，增加此值 tooprevent 這個錯誤。 |
| 503 |1001 |要求無法分派的 toonode.exe 因為 hello 應用程式正在回收處理。 Hello 應用程式已回收之後，要求通常應該會提供服務。 |
| 503 |1002 |核取 win32 錯誤碼的實際原因 – 要求找不到分派的 tooa node.exe。 |
| 503 |1003 |具名管道太忙 – 檢查節點是否正耗用大量的 CPU |

NODE.exe 內有名為 NODE\_PENDING\_PIPE\_INSTANCES 的設定。 根據預設，此值在 Azure Web Apps 外部為 4。 這表示該 node.exe hello 具名管道上一次只能接受 4 的要求。 在 Azure Webapps too5000 設定此值，這個值應該是適用於 azure webapps 上執行的大部分節點應用程式。 您應該不會看到 503.1003 azure webapps 因為我們有較高的值為 hello 節點\_PENDING\_管道\_執行個體。  |

## <a name="more-resources"></a>其他資源
Azure App Service 上，請遵循這些連結 toolearn 更多關於 node.js 應用程式。

* [在 Azure App Service 中開始使用 Node.js Web 應用程式](app-service-web-get-started-nodejs.md)
* [Toodebug Node.js web 應用程式在 Azure App Service 中的方式](web-sites-nodejs-debug.md)
* [使用 Node.js 模組與 Azure 應用程式搭配](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps：Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Node.js 開發人員中心](../nodejs-use-node-modules-azure-apps.md)
* [瀏覽 hello 進階密碼 Kudu 偵錯主控台](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

