---
title: "App Service 中的 aaaSlow web 應用程式效能 |Microsoft 文件"
description: "本文可協助您針對 Azure App Service 中 Web 應用程式效能變慢的問題進行疑難排解。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "Web 應用程式效能、變慢的應用程式、應用程式變慢"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>針對 Azure App Service 中 Web 應用程式效能變慢的問題進行疑難排解
本文可協助您針對 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中 Web 應用程式效能變慢的問題進行疑難排解。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)，然後按一下 **取得支援**。

## <a name="symptom"></a>徵狀
當您瀏覽 hello web 應用程式時，hello 頁面載入緩慢和有時逾時。

## <a name="cause"></a>原因
此問題通常是因為應用程式層級問題所造成，例如：

* 網路要求耗費過長的時間
* 應用程式程式碼或資料庫查詢的效率不佳
* 應用程式的記憶體/CPU 使用率過高
* 應用程式當機，因為 tooan 例外狀況

## <a name="troubleshooting-steps"></a>疑難排解步驟
疑難排解可以分成三種不同的工作，依序為：

1. [觀察和監視應用程式行為](#observe)
2. [收集資料](#collect)
3. [減少 hello 問題](#mitigate)

[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1.觀察和監視應用程式行為
#### <a name="track-service-health"></a>追蹤服務健全狀況
每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。 您可以在 hello 追蹤 hello hello 服務健全狀況[Azure 入口網站](https://portal.azure.com/)。 如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。

#### <a name="monitor-your-web-app"></a>監視 Web 應用程式
如果您的應用程式有任何問題，此選項可讓您 toofind 出。 在您的 web 應用程式] 刀鋒視窗中，按一下 [hello**要求與錯誤**磚。 hello**度量**刀鋒視窗會顯示您可以加入所有 hello 度量。

某些您可能希望您的 web 應用程式 toomonitor hello 度量

* 平均記憶體工作集
* 平均回應時間
* CPU 時間
* 記憶體工作集
* 要求

![監視 Web 應用程式效能](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

如需詳細資訊，請參閱：

* [監視 Azure App Service 中的 Web Apps](web-sites-monitor.md)
* [接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>監視 Web 端點狀態
如果您執行您 web 應用程式在 hello**標準**定價層，Web 應用程式可讓您監視兩個端點從三個地理位置。

端點監視能讓您設定從不同地理位置執行，且用來測試 Web URL 之回應時間和運作時間的 Web 測試。 hello 測試會從每個位置中執行 HTTP GET 作業上 hello web URL toodetermine hello 回應時間和執行時間。 各個已設定的位置會每隔五分鐘執行一次測試。

運作時間是透過 HTTP 回應碼來加以監視，而回應時間的測量單位是毫秒。 如果 hello HTTP 回應碼大於或等於 too400 或如果 hello 回應時間超過 30 秒，則監視測試會失敗。 端點視為可用監視測試皆成功從所有 hello 指定位置。

它，請參閱 tooset[監視 Azure App Service 中的應用程式](web-sites-monitor.md)。

同時，亦請參閱 [讓 Azure 網站保持運作以及端點監視 - 對談來賓 Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) 的端點監視影片。

#### <a name="application-performance-monitoring-using-extensions"></a>使用擴充功能的應用程式效能監視
您也可以利用*網站擴充功能*監視應用程式的效能。

每個 App Service web 應用程式提供可延伸管理結束點，可讓您 toouse 一組強大的工具部署為網站擴充功能。 擴充功能包括： 

- 原始程式碼編輯器，例如 [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx)。 
- 適用於已連線的資源，例如 MySQL 資料庫管理工具連線 tooa web 應用程式。

[Azure 的 Application Insights](/services/application-insights/)和[New Relic](/marketplace/partners/newrelic/newrelic/) hello 效能監視站台所提供的擴充功能的兩個。 toouse New Relic，您可以安裝在執行階段代理程式。 toouse Azure Application Insights，重建的 sdk，您的程式碼，您也可以安裝可提供存取 tooadditional 資料延伸模組。 hello SDK 可讓您更詳細地撰寫的程式碼 toomonitor hello 和您的應用程式的效能。

toouse Application Insights，請參閱[監視 web 應用程式中的效能](../application-insights/app-insights-web-monitor-performance.md)。

toouse New Relic，請參閱[新 Relic 應用程式效能在 Azure 上管理](../store-new-relic-cloud-services-dotnet-application-performance-management.md)。

<a name="collect" />

### <a name="2-collect-data"></a>2.收集資料
hello Web 應用程式環境提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷功能。 hello 資訊分成 web 伺服器的診斷和 application diagnostics。

#### <a name="enable-web-server-diagnostics"></a>啟用網頁伺服器診斷
您可以啟用或停用下列種類的記錄檔的 hello:

* **詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。 這可能包含可協助您判斷為什麼 hello 伺服器傳回 hello 錯誤碼的資訊。
* **失敗要求追蹤**-詳細的失敗的要求，包括 hello IIS 使用的元件 tooprocess hello 要求和取得每個元件中的 hello 時間的追蹤資訊。 如果您正嘗試 tooimprove web 應用程式效能或隔離造成特定的 HTTP 錯誤，這可能會很有用。
* **Web 伺服器記錄**-HTTP 交易使用 hello W3C 擴充的記錄檔格式的相關資訊。 決定整體的 web 應用程式度量，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時，這非常有用。

#### <a name="enable-application-diagnostics"></a>啟用應用程式診斷
有數個選項 toocollect 應用程式的效能資料，Web 應用程式、 設定檔的即時應用程式從 Visual Studio 中，或修改您的應用程式程式碼 toolog 的詳細資訊和追蹤。 您可以選擇根據 hello 選項上多少的存取權，您有 toohello 應用程式，而且您從 監視工具的 hello 觀察到。

##### <a name="use-application-insights-profiler"></a>使用 Application Insights Profiler
您可以啟用 hello 應用程式 Insights Profiler toostart 擷取詳細的效能追蹤。 您可以存取的 toofive 天前何時該添 tooinvestigate 問題是發生在過去的 hello 上擷取的追蹤。 您可以選擇此選項，只要您有 Azure 入口網站上的存取 toohello web 應用程式的 Application Insights 資源。

應用程式 Insights 分析工具提供的統計資料指出哪一行程式碼使 hello 回應變慢的回應時間的每個 web 呼叫和追蹤。 有時 hello App Service 應用程式緩慢，是因為某些程式碼不會寫入在高效能的方式。 範例包括可以平行執行以及在不想要的資料庫鎖定爭用中執行的循序程式碼。 Hello 程式碼中移除這些瓶頸增加 hello 應用程式效能，但它們是永久 toodetect 而不需設定詳細追蹤和記錄檔。 應用程式 Insights 分析工具所收集的 hello 追蹤可協助識別 hello hello 應用程式變慢的程式碼行，並克服這項挑戰，App Service 應用程式。

 如需詳細資訊，請參閱[使用 Application Insights 來分析即時 Azure Web 應用程式](../application-insights/app-insights-profiler.md)。

##### <a name="use-remote-profiling"></a>使用遠端分析
您可在 Azure App Service、Web Apps、API Apps 和 WebJobs 進行遠端分析。 如果您擁有存取 toohello web 應用程式資源和您知道如何 tooreproduce hello 問題，或如果您知道 hello 完全發生的時間間隔 hello 效能問題，請選擇此選項。

遠端分析很有用，如果 hello hello 程序的 CPU 使用量過高和您的處理序執行速度比預期慢或 hello 的 HTTP 要求的延遲會超過正常情況，則您可以從遠端設定檔，您的程序並取得 hello CPU 取樣的呼叫堆疊 tooanalyzehello 程序活動和程式碼最忙碌路徑。

如需詳細資訊，請參閱 [Azure App Service 中的遠端分析支援](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service)。

##### <a name="set-up-diagnostic-traces-manually"></a>手動設定診斷追蹤
如果您有存取 toohello web 應用程式的原始程式碼，Application diagnostics 可讓您的 web 應用程式所產生的 toocapture 資訊。 ASP.NET 應用程式可以使用 hello`System.Diagnostics.Trace`類別 toolog 資訊 toohello 應用程式診斷記錄。 不過，您需要 toochange hello 程式碼並重新部署您的應用程式。 如果您的應用程式是在測試環境上執行，建議使用這個方法。

如需有關的詳細指示 tooconfigure 應用程式的記錄，請參閱[啟用 Azure App Service 中的 web 應用程式的診斷記錄](web-sites-enable-diagnostic-log.md)。

#### <a name="use-hello-azure-app-service-support-portal"></a>使用 hello Azure App Service 支援入口網站
Web 應用程式為您提供 hello 能力 tootroubleshoot 問題相關的 tooyour web 應用程式藉由查看 HTTP 記錄檔、 事件記錄檔、 處理序傾印，等等。 您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。

hello Azure App Service 支援入口網站為您提供三個個別索引標籤的常見的疑難排解情況 toosupport hello 三個步驟：

1. 觀察目前的行為
2. 收集診斷資訊及執行 hello 內建的分析器來分析
3. 減輕問題

如果立即發生 hello 問題，請按一下**分析** > **診斷** > **現在診斷**toocreate 為您的診斷工作階段以收集 HTTP 記錄檔、 事件檢視器記錄檔、 記憶體傾印、 PHP 錯誤記錄檔和 PHP 處理序報表。

一旦 hello 資料收集，hello 支援入口網站上 hello 資料執行分析，並提供您的 HTML 報表。

如果您想 toodownload hello 資料，根據預設，它就會儲存在 hello D:\home\data\DaaS 資料夾中。

如需有關 hello Azure App Service 支援入口網站的詳細資訊，請參閱[Azure 網站的網站擴充功能的新更新 tooSupport](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。

#### <a name="use-hello-kudu-debug-console"></a>使用 hello Kudu 偵錯主控台
Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。 此主控台稱為 hello *Kudu 主控台*或 hello *SCM 儀表板*web 應用程式。

您可以將 toohello 連結存取這個儀表板**https://&lt;應用程式名稱 >.scm.azurewebsites.net/**。

Kudu 提供的 hello 事項包括：

* 您的應用程式的環境設定
* 記錄檔串流
* 診斷傾印
* 您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。

Kudu 另一個有用功能是，如果您的應用程式會擲回第一個出現的例外狀況，您可以使用 Kudu 與 hello SysInternals 工具 Procdump toocreate 記憶體傾印。 這些記憶體傾印是 hello 程序的快照集，並經常可協助您疑難排解您 web 應用程式更複雜的問題。

如需 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站 Team Services 工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3.減少 hello 問題
#### <a name="scale-hello-web-app"></a>標尺 hello web 應用程式
在 Azure 應用程式服務，以增加的效能和輸送量，您可以調整 hello 小數位數，執行您的應用程式。 向上擴充 web 應用程式牽涉到兩個相關的動作： 變更您應用程式服務計劃 tooa 較高的定價層，以及設定某些設定之後您切換 toohello 更高的定價層。

如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。

此外，您可以選擇 toorun 多個執行個體上的應用程式。 相應放大不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。 如果上一個執行個體關閉 hello 程序，hello 其他執行個體會繼續 tooserve 要求。

您可以設定 hello toobe 手動或自動縮放比例。

#### <a name="use-autoheal"></a>使用 AutoHeal
AutoHeal 回收 hello 取決於您選擇 （例如組態變更、 要求、 記憶體為基礎的限制或 hello 時間需要 tooexecute 要求） 設定您的應用程式的背景工作處理序。 大部分的 hello 時間回收 hello 程序是 hello 最快方式 toorecover 問題。 您永遠可以重新啟動 hello web 應用程式從直接在 hello Azure 入口網站中的，雖然 AutoHeal 會自動為您。 您只需要 toodo 是 hello web 應用程式的根 web.config 中新增一些觸發程序。 這些設定會在 hello 相同方式即使您的應用程式並不是.Net 應用程式。

如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。

#### <a name="restart-hello-web-app"></a>重新啟動 hello web 應用程式
重新啟動，通常是 hello 最簡單方式 toorecover 從單次發生問題。 在 [hello [Azure 入口網站](https://portal.azure.com/)，在您的 web 應用程式] 刀鋒視窗中，您擁有 hello 選項 toostop 或重新啟動您的應用程式。

 ![重新啟動 web 應用程式 toosolve 效能問題](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

您也可以使用 Azure Powershell 管理 Web 應用程式。 如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。
