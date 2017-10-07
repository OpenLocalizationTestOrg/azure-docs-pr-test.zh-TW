---
title: "Azure web 應用程式的 aaaApplication 效能常見問題集 |Microsoft 文件"
description: "取得可用性、 效能及 hello Azure App Service Web 應用程式功能的應用程式問題的相關常見問題的解答 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Azure Web 應用程式的應用程式效能常見問題集

這篇文章有集 (Faq) 解答 toofrequently hello 的應用程式效能問題的相關[Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>為何我的應用程式變慢？

多個因素可能會構成 tooslow 應用程式效能。 如需詳細的疑難排解步驟，請參閱[針對緩慢的 Web 應用程式效能進行疑難排解](app-service-web-troubleshoot-performance-degradation.md)。

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>如何針對高 CPU 耗用量案例進行疑難排解？

在某些高 CPU 耗用量案例中，您的應用程式可能真正需要更多運算資源。 在此情況下，請考慮調整 tooa 高服務層，因此 hello 應用程式會取得所有所需的 hello 資源。 若是其他情況，不正確的迴圈或程式碼撰寫慣例可能會造成高 CPU 耗用量。 深入了解什麼觸發增加的 CPU 耗用量是兩部分的處理序。 首先，建立處理序傾印，並接著分析 hello 處理序傾印。 如需詳細資訊，請參閱[擷取及分析 Web 應用程式高 CPU 耗用量的傾印檔案](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/)。

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>如何針對高記憶體耗用量案例進行疑難排解？

在某些高記憶體耗用量案例中，您的應用程式可能真正需要更多運算資源。 在此情況下，請考慮調整 tooa 高服務層，因此 hello 應用程式會取得所有所需的 hello 資源。 其他時候，hello 程式碼中的錯誤可能會導致記憶體流失。 程式碼撰寫慣例也可能會增加記憶體耗用量。 深入了解什麼觸發高記憶體耗用量是兩部分的處理序。 首先，建立處理序傾印，並接著分析 hello 處理序傾印。 從 hello Azure 站台擴充程式庫損毀診斷程式可以有效率地執行這兩個步驟執行。 如需詳細資訊，請參閱[擷取及分析 Web 應用程式間歇高記憶體的傾印檔案](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/)。

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>如何使用 PowerShell 自動化 App Service Web 應用程式？

您可以使用 PowerShell cmdlet toomanage 及維護 App Service web 應用程式。 我們的部落格文章中[自動化使用 PowerShell 在 Azure App Service 中裝載的 web 應用程式](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/)，我們將描述如何 toouse Azure 資源管理員為基礎的 PowerShell cmdlet tooautomate 一般工作。 hello 部落格文章也會有各種 web 應用程式管理工作的範例程式碼。 如需所有 App Service Web 應用程式 Cmdlet 的說明和語法，請參閱 [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0)。

## <a name="how-do-i-view-my-web-apps-event-logs"></a>如何檢視我的 Web 應用程式事件記錄？

tooview 您 web 應用程式事件記錄檔：

1. 登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。
2. 在 hello 功能表中，選取 **偵錯主控台** > **CMD**。
3. 選取 hello **LogFiles**資料夾。
4. tooview 事件記錄檔中，選取 hello 鉛筆圖示旁太**eventlog.xml**。
5. toodownload hello 記錄檔，執行 hello PowerShell cmdlet `Save-AzureWebSiteLog -Name webappname`。

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>如何擷取 Web 應用程式的使用者模式記憶體傾印？

toocapture 您 web 應用程式的使用者模式下記憶體傾印：

1. 登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。
2. 選取 hello**處理序總管**功能表。
3. 以滑鼠右鍵按一下 hello **w3wp.exe**程序或您的 web 工作處理序。
4. 選取 [下載記憶體傾印] >  [完整傾印]。

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>如何檢視 Web 應用程式的處理序層級資訊？

您有兩個選項可以用來檢視 Web 應用程式的處理序層級資訊：

*   在 hello Azure 入口網站：
    1. 開啟 hello**處理序總管**hello web 應用程式。
    2. toosee hello 詳細資料，選取 hello **w3wp.exe**程序。
*   在 hello Kudu 主控台：
    1. 登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。
    2. 選取 hello**處理序總管**功能表。
    3. Hello **w3wp.exe**程序中，選取**屬性**。

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>當我瀏覽 toomy 應用程式時，我看到 「 錯誤 403-此 web 應用程式已停止 」。 如何解決這個問題？

有三個條件會造成這個錯誤：

* hello web 應用程式已達到帳單的限制，並且已停用您的網站。
* hello web 應用程式已停止在 hello 入口網站。
* hello web 應用程式已達到資源配額限制，可能會套用 tooa 免費或共用標尺服務計劃。

toosee 中造成錯誤 hello 和 tooresolve hello 問題、 後續 hello 步驟[Web 應用程式: 「 錯誤 403 – 此 web 應用程式已停止 」](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/)。

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>哪裡可以深入了解各種 App Service 方案的配額和限制？

如需配額和限制的詳細資訊，請參閱 [App Service 限制](../azure-subscription-service-limits.md#app-service-limits)。 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>我要如何減少 hello 回應 hello 第一個要求時間之後閒置時間？

根據預設，Web 應用程式如果閒置一段時間，就會卸載。 如此一來，hello 系統可以節省資源。 hello 選項的缺點是，hello 回應 toohello 第一個要求之後卸載 hello web 應用程式是較長，tooallow hello web 應用程式 tooload 並開始處理回應。 在基本和標準服務計畫中，您可以開啟 hello **Always On**設定 tookeep hello 應用程式一律載入。 這排除了更長的載入時間之後 hello 應用程式處於閒置狀態。 toochange hello **Always On**設定：

1. 在 hello Azure 入口網站，移 tooyour web 應用程式。
2. 選取 [應用程式設定]。
3. 針對 [永遠開啟]，選取 [開啟]。

## <a name="how-do-i-turned-on-failed-request-tracing"></a>如何開啟失敗的要求追蹤？

tooturn 上失敗的要求追蹤：

1. 在 hello Azure 入口網站，移 tooyour web 應用程式。
3. 選取 [所有設定] >  [診斷記錄]。
4. 針對 [失敗的要求追蹤]，選取 [開啟]。
5. 選取 [ **儲存**]。
6. 在 hello web 應用程式刀鋒視窗中，選取 **工具**。
7. 選取 [Visual Studio Online]。
8. 如果未設定 hello**上**，選取**上**。
9. 選取 [執行]。
10. 選取 **Web.config**。
11. 在 system.webServer，加入這項設定 (toocapture 特定 URL):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. tootroubleshoot 緩慢效能問題，加入這項設定 （如果 hello 擷取要求花費超過 30 秒）：
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. toodownload hello 失敗要求的追蹤，在 hello[入口網站](https://portal.azure.com)，移至 tooyour 網站。
15. 選取 [工具] >  [Kudu] >  [執行]。
18. 在 hello 功能表中，選取 **偵錯主控台** > **CMD**。
19. 選取 hello **LogFiles**資料夾，然後再選取 hello 開頭的名稱的資料夾**W3SVC**。
20. toosee hello XML 檔案，選取 hello 鉛筆圖示。

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>我看到 hello 訊息 「 背景工作處理序要求回收到期 too'Percent 記憶體 ' 限制。 」 如何解決這個問題？

hello 最大可用記憶體數量 32 位元處理序 （即使在 64 位元作業系統） 上的是 2 GB。 根據預設，hello 背景工作處理序設定 too32 位元應用程式服務中 （適用於與傳統 web 應用程式的相容性）。

請考慮切換 too64 位元處理序，因此您可以利用 hello 額外的記憶體可用，您的 Web 背景工作角色。 這會觸發 Web 應用程式重新啟動，請據以排程。

另請注意，64 位元環境需要基本或標準服務方案。 [免費] 與 [共用] 方案一律於 32 位元環境中執行。

如需詳細資訊，請參閱 [在 App Service 中設定 Web 應用程式](https://docs.microsoft.com/azure/app-service-web/web-sites-configure)。

## <a name="why-does-my-request-time-out-after-240-seconds"></a>為何我的要求在 240 秒後逾時？

Azure Load Balancer 有預設四分鐘的閒置逾時設定。 這通常對於 Web 要求是合理的回應時間限制。 如果您的 Web 應用程式需要幕後處理，我們建議您使用 Azure WebJobs。 hello Azure web 應用程式可以呼叫 web 工作，並在背景處理完成時收到通知。 您可以從使用 WebJobs 的多個方法中選擇，包括佇列和觸發程序。

WebJobs 是設計用來進行幕後處理。 您可以在 WebJob 中進行您想要的任意數量幕後處理。 如需 WebJobs 的詳細資訊，請參閱[使用 WebJobs 執行背景工作](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs)。

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>裝載於 App Service 中的 ASP.NET Core 應用程式有時候會停止回應。 如何修正此問題？

先前的已知的問題[Kestrel 版本](https://github.com/aspnet/KestrelHttpServer/issues/1182)裝載的 ASP.NET Core 1.0 應用程式可能會導致應用程式服務 toointermittently 停止回應。 您也可能會看到此訊息: 「 hello 指定 CGI 應用程式發生錯誤和 hello 終止伺服器 hello 程序 」。

Kestrel 1.0.2 版已經修正這個問題。 此版本隨附於 hello ASP.NET Core 1.0.3 更新。 tooresolve 這個問題，請確定您更新您的應用程式相依性 toouse Kestrel 1.0.2。 或者，您可以使用兩種因應措施 hello 部落格文章所述的其中一個[App Service web 應用程式中的 ASP.NET Core 1.0 變慢的效能問題](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites)。


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>我在我的 web 應用程式的 hello 檔案結構中找不到我的記錄檔。 如何找到它們？

如果您使用應用程式服務的 hello 本機快取功能，會影響 hello hello LogFiles 資料夾結構和您的應用程式服務執行個體資料的資料夾。 使用本機快取時，hello 儲存記錄檔和資料的資料夾中建立子資料夾。 hello 子資料夾使用 hello 命名模式 「 唯一識別項 」 + 時間戳記。 每個子資料夾對應 tooa VM 執行個體中的 hello web 應用程式正在執行或已執行。

toodetermine 不論您使用本機快取，請檢查您的應用程式服務**應用程式設定** 索引標籤。如果正在使用本機快取，hello 應用程式設定`WEBSITE_LOCAL_CACHE_OPTION`設定得`Always`。 如需有關本機快取的詳細資訊，請參閱 hello[應用程式服務的本機快取概觀](https://docs.microsoft.com/azure/app-service/app-service-local-cache)。

如果您不是使用本機快取，但是也遇到此問題，請提交支援要求。

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>我看到 hello 訊息 」 嘗試已拒絕其存取權限的方式進行 tooaccess 通訊端。 」 如何解決這個問題？

如果 hello 對外 TCP 連線 hello VM 執行個體上的用完，通常就會發生這個錯誤。 App Service 中 hello 可以對每個 VM 執行個體的傳出連線數目上限會強制執行限制。 如需詳細資訊，請參閱[跨 VM 的數值限制](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits)。

如果您嘗試從您的應用程式的本機位址 tooaccess 這項錯誤也可能會發生。 如需詳細資訊，請參閱[本機位址要求](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests)。

如需 web 應用程式中的輸出連線的詳細資訊，請參閱 hello 部落格文章有關[傳出連線 tooAzure 網站](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/)。

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>如何使用 Visual Studio tooremote 偵錯我的 App Service web 應用程式？

如需詳細的逐步解說，為您示範如何 toodebug web 應用程式使用 Visual Studio，請參閱[遠端偵錯您的 App Service web 應用程式](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/)。
