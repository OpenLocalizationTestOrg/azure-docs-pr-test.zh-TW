---
title: "aaaTroubleshooting 沒有資料-適用於.NET 的 Application Insights"
description: "在 Azure Application Insights 中看不到資料？ 試試這裡。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>沒有要進行疑難排解的資料 - Application Insights for .NET
## <a name="some-of-my-telemetry-is-missing"></a>我遺失了部分遙測
*在 Application Insights 我只能看見 hello 事件我的應用程式所產生的一部分。*

* 如果您持續看見 hello 相同比例、 其可能到期 tooadaptive[取樣](app-insights-sampling.md)。 tooconfirm，開啟 [搜尋] （從 hello 概觀刀鋒視窗），並查看執行個體的要求或其他事件。 在 hello hello 屬性區段底部按一下"…"tooget 完整的屬性詳細資料。 如果要求計數 > 1，則表示取樣正在運作中。 
* 否則，有可能是您已達到定價方案的 [資料速率限制](app-insights-pricing.md#limits-summary) 。 每分鐘都會套用這些限制。

## <a name="no-data-from-my-server"></a>沒有來自我的伺服器的資料
我已在 Web 伺服器上安裝我的應用程式，而我現在沒看到任何來自於它的遙測。它在我的開發電腦上運作正常。

* 可能是防火牆問題。 [設定防火牆例外狀況的 Application Insights toosend 資料](app-insights-ip-addresses.md)。

*我[安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)我 web 伺服器 toomonitor 現有應用程式。我沒有看到任何結果。*

* 請參閱 [疑難排解狀態監視器](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)。 

## <a name="q01"></a>在 Visual Studio 中沒有「新增 Application Insights」選項
當我以滑鼠右鍵按一下 [方案總管] 中的現有專案時，沒有看到任何 Application Insights 選項。

* 並非所有類型的.NET 專案都受到 hello 工具。 支援 Web 和 WCF 專案。 例如，桌面或服務應用程式的其他專案類型，您仍然可以[手動加入 Application Insights SDK tooyour 專案](app-insights-windows-desktop.md)。
* 請確定您有 [Visual Studio 2013 Update 3 或更新版本](http://go.microsoft.com/fwlink/?LinkId=397827)。 它是使用開發人員分析工具提供 hello Application Insights SDK 會預先安裝。
* 選取 [工具]、[擴充功能和更新]，檢查 [開發人員分析工具] 是否已安裝並啟用。 如果是的話，按一下**更新**toosee 如果沒有可用的更新。
* 開啟 hello 新增專案] 對話方塊，然後選擇 [ASP.NET Web 應用程式。 如果您看到 hello Application Insights 選項，則會安裝 hello 工具。 如果沒有，請嘗試解除安裝再重新安裝 hello Application Insights 工具。

## <a name="q02"></a>新增 Application Insights 失敗
*當我嘗試 tooadd Application Insights tooan 現有專案時，我看到一則錯誤訊息。*

可能的原因：

* 與 hello Application Insights 入口網站的通訊失敗;或
* 您的 Azure 帳戶發生問題；
* 您只需要[讀取權限 toohello 訂用帳戶或您已在此嘗試 toocreate hello 新資源群組](app-insights-resources-roles-access-control.md)。

修正：

* 請檢查您所提供的登入認證用於 hello 權限的 Azure 帳戶。 
* 在瀏覽器中，確認您擁有存取 toohello [Azure 入口網站](https://portal.azure.com)。 開啟 [設定] 並查看是否有任何限制。
* [加入 Application Insights tooyour 現有專案](app-insights-asp-net.md)： 在方案總管中，以滑鼠右鍵按一下您的專案，然後選擇 新增 Application Insights。
* 如果仍然無法運作，請遵循 hello[手動程序](app-insights-windows-services.md)tooadd hello 入口網站中的資源，然後新增 hello SDK tooyour 專案。 

## <a name="emptykey"></a>我收到「檢測金鑰不能是空白」的錯誤
可能是您在安裝 Application Insights 或記錄配接器時發生問題。

在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [Application Insights] > [設定 Application Insights]。 就會顯示一個對話方塊，邀請您 toosign tooAzure 中，然後建立 Application Insights 資源，或重複使用現有的我的最愛。

## <a name="NuGetBuild"></a> 我的組建伺服器上「NuGet 封裝遺失」
*我正在電腦上偵錯我開發，不過，NuGet 錯誤 hello 組建伺服器上時，所有項目就會建立 [確定]。*

請參閱 [NuGet 套件還原](http://docs.nuget.org/Consume/Package-Restore)和[自動套件還原](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore)。

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>遺失的功能表命令 tooopen Application Insights 從 Visual Studio
*當我以滑鼠右鍵按一下專案 [方案總管] 時，我沒有看到任何 Application Insights 命令，或沒有看到開啟 Application Insights 命令。*

可能的原因：

* 如果您手動建立 hello Application Insights 資源或 hello 專案是 hello Application Insights 工具不支援的型別。
* hello 開發人員分析工具會在您的 Visual Studio 中停用。 
* 您的 Visual Studio 版本比 2013 Update 3 還舊。

修正：

* 請確定您的 Visual Studio 版本是 2013 Update 3 或更新版本。
* 選取 [工具]、[擴充功能和更新]，檢查 [開發人員分析工具] 是否已安裝並啟用。 如果是的話，按一下**更新**toosee 如果沒有可用的更新。
* 以滑鼠右鍵按一下 [方案總管] 中的專案。 如果您看到 hello 命令**Application Insights > 設定 Application Insights**，並用 tooconnect 專案 toohello 資源在 hello Application Insights 服務。

否則，您的專案類型不直接支援 hello Application Insights 工具。 toosee 您遙測，登入 toohello [Azure 入口網站](https://portal.azure.com)、 選擇在 hello 左側的導覽列上的 Application Insights 和選取您的應用程式。

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>從 Visual Studio 開啟 Application Insights 時「拒絕存取」
*hello ' 開啟 Application Insights' 功能表命令會讓我 toohello Azure 入口網站，但我收到 「 拒絕存取 」 錯誤。*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

hello Microsoft 登入上一次使用預設的瀏覽器上沒有存取權限太[hello Application Insights 加入 toothis 應用程式時所建立的資源](app-insights-asp-net.md)。 有兩個可能的原因： 

* 您有一個以上的 Microsoft 帳戶-可能是工作和個人的 Microsoft 帳戶嗎？hello 已登入上一次使用預設的瀏覽器上為不同的帳戶比 hello 可存取太[加入 Application Insights toohello 專案](app-insights-asp-net.md)。 
  
  * 修正： 按一下您在名稱右上角的 hello 瀏覽器視窗，並登出。然後使用 hello 擁有存取權的帳戶登入。 Hello 左的導覽列中，按一下 Application Insights 然後選取您的應用程式。
* 其他人加入 Application Insights toohello 專案，而且他們忘了 toogive 您[存取 toohello 資源群組](app-insights-resources-roles-access-control.md)中建立此。 
  
  * 修正： 如果它們使用組織帳戶，他們可以將您加入 toohello 小組;或者，他們可以 grant 您個別存取 toohello 資源群組。

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>從 Visual Studio 開啟 Application Insights 時「找不到資產」
*hello ' 開啟 Application Insights' 功能表命令會讓我 toohello Azure 入口網站，但我收到 「 找不到資產' 錯誤。*

可能的原因：

* hello 應用程式的 Application Insights 資源已被刪除。或
* hello 檢測機碼設定或變更 ApplicationInsights.config 中直接編輯而不更新 hello 專案檔。 

ApplicationInsights.config 控制項傳送嗨遙測的位置中的 hello 檢測金鑰。 Hello 專案檔中的資料行控制當您使用 Visual Studio 中的 hello 命令開啟的資源。 

修正：

* 在 方案總管 hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights，設定 Application Insights。 在 [hello] 對話方塊中，您可以選擇 toosend 遙測 tooan 現有的資源，或另外新建一個。 或：
* 直接開啟 hello 資源。 登入太[hello Azure 入口網站](https://portal.azure.com)，請按一下 Application Insights hello 左側的導覽列上，，，然後選取您的應用程式。

## <a name="where-do-i-find-my-telemetry"></a>哪裡可以找到我的遙測？
*我登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)，以及我查看 hello Azure 首頁儀表板。那麼我可以在哪裡找到我的 Application Insights 資料？*

* 在 hello 左的導覽列中，按一下 Application Insights，然後您的應用程式名稱。 如果您那里沒有任何專案，您需要太[新增，或在您的 web 專案中設定 Application Insights](app-insights-asp-net.md)。
  
    您可以從中看到一些摘要圖表。 您可以按一下這些 toosee 更詳細說明。
* 在 Visual Studio 中，當您偵錯您的應用程式時，按一下 hello Application Insights 按鈕。

## <a name="q03"></a> 沒有任何伺服器資料 (或根本沒有資料)
*我已執行我的應用程式，然後再開啟 Microsoft Azure 中的 hello Application Insights 服務，但所有 hello 圖表顯示 ' 深入了解如何 toocollect...' 或 '未設定'。* 或者，只有頁面檢視和使用者資料，但卻沒有任何伺服器資料。

* 在 Visual Studio 中以偵錯模式執行您的應用程式 (F5)。 做為 hello 應用程式因此 toogenerate 某些遙測。 您可以查看事件記錄 hello Visual Studio 輸出 視窗中的核取。 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* 在 hello Application Insights 入口網站中，開啟[診斷搜尋](app-insights-diagnostic-search.md)。 這裡通常會先顯示資料。
* 按一下 hello 重新整理 按鈕。 hello 刀鋒視窗定期重新整理，本身，但您也可以執行它以手動方式。 hello 重新整理間隔的長度為較大的時間範圍。
* 請檢查 hello 檢測金鑰相符。 您的應用程式在 hello Application Insights 入口網站中 hello hello 主要的刀鋒視窗上**Essentials**下拉式清單中，查看**檢測金鑰**。 接著，在 Visual studio 專案中，開啟 ApplicationInsights.config，然後尋找 hello `<instrumentationkey>`。 請檢查 hello 兩個索引鍵相等。 如果不是：
  
  * 在 hello 入口網站中，按一下 Application Insights，尋找 hello 應用程式資源與 hello 右邊的索引鍵;或
  * 在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello 專案並選擇 Application Insights，設定。 重設 hello 應用程式 toosend 遙測 toohello 適當的資源。
  * 找不到相符的索引鍵的 hello，如果您使用的核取 hello 相同登入認證在 Visual Studio 中的如 toohello 入口網站所示。
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* 在 hello [Microsoft Azure 首頁儀表板](https://portal.azure.com)，看看 hello 服務健全狀況的對應。 如果有某些警示的指示，請等到它們都傳回 tooOK 然後關閉再重新開啟 Application Insights 的應用程式刀鋒視窗。
* 也請查閱 [我們的狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。
* 這是您撰寫任何程式碼的 hello[伺服器端 SDK](app-insights-api-custom-events-metrics.md) ，可能會變更中的 hello 檢測金鑰`TelemetryClient`執行個體或`TelemetryContext`嗎？ 或者您撰寫的 [篩選或取樣組態](app-insights-api-filtering-sampling.md) 可能會篩選出過多項目？
* 如果您編輯 ApplicationInsights.config，請仔細檢查 hello 組態[TelemetryInitializers 和 TelemetryProcessors](app-insights-api-filtering-sampling.md)。 未正確命名類型或參數可能會不導致 hello SDK toosend 任何資料。

## <a name="q04"></a>頁面檢視、瀏覽器、使用量上沒有任何資料
*我看到伺服器回應時間和圖表中資料的伺服器要求，但是沒有資料或 hello 瀏覽器或使用方式的刀鋒視窗中檢視的頁面載入時間。*

hello 資料來自於 hello web 網頁中的指令碼。 

* 如果您加入現有的 web 專案的 Application Insights tooan[您尚未 tooadd hello 指令碼以手動方式](app-insights-javascript.md)。
* 確定 Internet Explorer 並非以相容性模式顯示您的網站。
* 使用 hello 瀏覽器的偵錯功能 （按 F12，在某些瀏覽器，然後選擇網路），正在傳送的資料太 tooverify`dc.services.visualstudio.com`。

## <a name="no-dependency-or-exception-data"></a>沒有相依性或例外狀況資料
請參閱[相依性遙測](app-insights-asp-net-dependencies.md)和[例外狀況遙測](app-insights-asp-net-exceptions.md)。

## <a name="no-performance-data"></a>沒有效能資料
效能資料 (CPU、IO 速率等等) 適用於 [Java Web 服務](app-insights-java-collectd.md)、[Windows 傳統型應用程式](app-insights-windows-desktop.md)、[IIS Web 應用程式和服務 (若您安裝狀態監視器)](app-insights-monitor-performance-live-website-now.md) 和 [Azure 雲端服務](app-insights-azure.md)。 您將會在 [設定]、[伺服器] 之下看到該資料。

它不適用於 Azure 網站。

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>由於發佈 hello 應用程式 toomy 伺服器沒有 （伺服器） 資料
* 請檢查您實際複製所有 hello Microsoft。 連同 Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll ApplicationInsights Dll toohello 伺服器
* 在您的防火牆，您可能有太[開啟某些 TCP 通訊埠](app-insights-ip-addresses.md#data-access-api)。
* 如果您有 toouse proxy toosend 超出您的公司網路，設定[defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) Web.config 中
* Windows Server 2008： 請確定您已安裝下列更新的 hello: [KB2468871](https://support.microsoft.com/kb/2468871)， [KB2533523](https://support.microsoft.com/kb/2533523)， [KB2600217](https://support.microsoft.com/kb/2600217)。

## <a name="i-used-toosee-data-but-it-has-stopped"></a>我使用 toosee 資料，但它已停止
* 檢查 hello[狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。
* 您有達到資料點的每月配額嗎？ 開啟 hello 設定/配額和定價 toofind 出。若有達到配額，您可以升級您的方案，或付費取得額外容量。 請參閱 hello[定價配置](https://azure.microsoft.com/pricing/details/application-insights/)。

## <a name="i-dont-see-all-hello-data-im-expecting"></a>我看不到我預期的所有 hello 資料
如果您的應用程式傳送大量資料，而您使用 ASP.NET 版本 2.0.0-beta3 hello Application Insights SDK，或更新版本中，hello[調整取樣](app-insights-sampling.md)功能可能會運作，並傳送您遙測的百分比表示。 

您可以停用它，但是這不是建議的作法。 取樣經過設計，以便能正確傳輸相關的遙測，供診斷之用。 

## <a name="wrong-geographical-data-in-user-telemetry"></a>使用者遙測中錯誤的地理資料
hello 城市、 區域和國家 （地區） 的維度衍生自 IP 位址，而且不一定正確。

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>在 Azure 雲端服務中執行時發生的「找不到方法」例外狀況
您是否已針對 .NET 4.6 組建？ Azure 雲端服務角色不自動支援 4.6。 [在每個角色上安裝 4.6](../cloud-services/cloud-services-dotnet-install-dotnet.md) ，再執行您的 App。

## <a name="still-not-working"></a>仍然無法運作...
* [Application Insights 論壇](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

