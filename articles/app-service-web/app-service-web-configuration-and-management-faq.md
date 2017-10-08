---
title: "Azure web 應用程式的 aaaConfiguration 常見問題集 |Microsoft 文件"
description: "取得要求 hello Azure App Service Web 應用程式功能組態與管理問題的相關問題的答案 toofrequently。"
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
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Azure 中 Web 應用程式的設定和管理常見問題集

這篇文章有解答 toofrequently 集 (Faq) 設定和管理問題的相關 hello [Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>有我應該了解如果想 toomove 應用程式服務資源的限制嗎？

如果您計劃 toomove App Service 資源 tooa 新資源群組或訂用帳戶，有一些限制 toobe 留意。 如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>如何針對 Web 應用程式使用自訂網域名稱？

如需搭配使用的自訂網域名稱與您的 Azure web 應用程式，答案 toocommon 問題，請參閱我們七個分鐘的影片[新增自訂網域名稱](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name)。 hello 視訊提供逐步解說，如何 tooadd 自訂網域名稱。 它會描述如何 toouse 自己的 URL，而不是 hello *。 使用您的 App Service web 應用程式的名稱是.azurewebsites.net URL。 您也可以看到的詳細逐步解說[如何 toomap 自訂網域名稱](web-sites-custom-domain-name.md)。


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>如何為 Web 應用程式購買新的自訂網域？

如何 toopurchase 及設定自訂網域，以您的 App Service web 應用程式，請參閱的 toolearn[購買並設定應用程式服務中的自訂網域名稱](custom-dns-web-site-buydomains-web-app.md)。


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>如何上傳及設定 Web 應用程式的現有 SSL 憑證？

如何 tooupload 及設定現有的自訂 SSL 憑證，請參閱的 toolearn[繫結現有自訂 SSL 憑證 tooan Azure web 應用程式](app-service-web-tutorial-custom-ssl.md#upload)。


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>如何購買 Web 應用程式的新 SSL 憑證並且在 Azure 中設定？

如何 toopurchase 及設定 SSL 憑證的 App Service web 應用程式，請參閱的 toolearn[新增 App Service 應用程式的 SSL 憑證 tooyour](web-sites-purchase-ssl-web-site.md)。


## <a name="how-do-i-move-application-insights-resources"></a>如何移動 Application Insights 資源？

目前，Azure Application Insights 並不支援 hello 移動作業。 如果您的原始資源群組包含 Application Insights 資源，則您無法移動該資源。 如果您包含 hello Application Insights 資源，當您嘗試 toomove App Service 應用程式時，整個 hello 移動操作失敗。 不過，Application Insights 和 hello 應用程式服務計劃不需要在 toobe hello 與 hello 應用程式 toofunction 的 hello 應用程式的相同資源群組正確。

如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>可以在哪裡尋找指引檢查清單及深入了解資源移動作業？

[應用程式服務限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)示範如何 toomove 資源 tooeither 新的訂用帳戶或 tooa 新資源群組中 hello 相同訂用帳戶。 您可以取得 hello 資源移動檢查清單的相關資訊，了解哪些服務支援 hello 移動作業，以及深入了解應用程式服務限制與其他主題。

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>如何在我的 web 應用程式設定 hello 伺服器時區？

tooset hello 伺服器時區 web 應用程式：

1. 在 hello 您應用程式服務的訂閱，在 Azure 入口網站移 toohello**應用程式設定**功能表。
2. 在 [應用程式設定] 底下，新增以下設定：
    * 索引鍵 = WEBSITE_TIME_ZONE
    * 值 =*您想要的 hello 時區*
3. 選取 [ **儲存**]。

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>為什麼我的持續 WebJobs 有時候會失敗？

根據預設，Web 應用程式如果閒置一段時間，就會卸載。 這可讓 hello 系統節省資源。 在基本和標準計畫中，您可以開啟 hello **Always On**設定 tookeep hello web 應用程式載入所有 hello 時間。 如果您的 web 應用程式執行連續 web 工作，您應該開啟**Always On**，或 hello WebJobs 可能無法可靠地執行。 如需詳細資訊，請參閱[建立持續執行 WebJob](web-sites-create-web-jobs.md#CreateContinuous)。

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>如何在我的 web 應用程式取得 hello 輸出的 IP 位址？

tooget hello 的 web 應用程式傳出的 IP 位址的清單：

1. 在 [hello Azure 入口網站，在您 web 應用程式] 刀鋒視窗中，移 toohello**屬性**功能表。
2. 搜尋**輸出 IP 位址**。

hello 輸出的 IP 位址清單隨即出現。

如果您的網站裝載在 App Service 環境 powerapps，toolearn 如何 tooget 輸出的 IP 位址，請參閱[傳出的網路位址](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses)。

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>如何為 Web 應用程式取得保留或專用輸入 IP 位址？

傳入呼叫時進行 tooyour Azure 應用程式網站的專用或保留 IP 位址的 tooset 安裝並設定以 IP 為主的 SSL 憑證。

請注意該 toouse 專用或進行傳入呼叫時的保留的 IP 位址，您的應用程式服務方案必須在基本或更高版本的服務方案中。

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>例如，對於網站裝載其他地方可以匯出外部 Azure 中，我 App Service 憑證 toouse 嗎？ 

App Service 憑證被視為 Azure 資源。 它們不是預期的 toouse 超出您的 Azure 服務。 您無法將它們匯出 toouse Azure 外部。 如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>我可以匯出我與其他 Azure 雲端服務的應用程式服務憑證 toouse 嗎？

hello 入口網站提供部署的 App Service 憑證，透過 Azure 金鑰保存庫 tooApp 服務應用程式第一級的體驗。 不過，我們已經收到來自客戶 toouse 要求外 hello 應用程式服務的平台，這些憑證，例如使用 Azure 虛擬機器。 toolearn 如何 toocreate 應用程式服務的本機複本 PFX 憑證讓您可以使用 hello 憑證與其他 Azure 資源，請參閱[建立本機應用程式服務憑證 PFX 複本](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/)。

如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>為什麼當我嘗試 tooback 設定我的 web 應用程式時看到 「 部分成功 」 的 hello 訊息？

備份失敗的常見原因是，某些檔案正在使用中的 hello 應用程式。 您執行 hello 備份使用中的檔案都會被鎖定。 這樣會避免這些檔案進行備份，因此可能導致「部分成功」狀態。 您可以有可能避免發生此 hello 備份程序從排除的檔案。 您可以選擇 tooback 向上僅需要什麼。 如需詳細資訊，請參閱[備份只 hello 的重要部分您 Azure web 應用程式的站台](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/)。

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>如何移除從 hello HTTP 回應的標頭？

從 HTTP 回應 hello tooremove hello 標頭會更新網站的 web.config 檔。 如需詳細資訊，請參閱[在 Azure 網站上移除標準伺服器標題](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)。

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>App Service 是否符合 PCI 標準 3.0 和 3.1 的規範？

目前，hello Azure App Service Web 應用程式功能是符合 PCI 資料安全標準 (DSS) 版本 3.0 層級 1。 PCI DSS 3.1 版在我們的藍圖中。 規劃已在進行中的採用 hello 最新標準的方式會繼續執行。

PCI DSS 3.1 版憑證需要停用傳輸層安全性 (TLS) 1.0。 目前，停用 TLS 1.0 不是大部分 App Service 方案的選項。 不過，如果您使用 App Service 環境，或不願意 toomigrate 您工作負載 tooApp 服務環境，您可以取得更好的控制，您的環境。 這牽涉到藉由連絡 Azure 支援人員來停用 TLS 1.0。 在靠近未來 hello，我們計劃 toomake 這些設定可存取 toousers。

如需詳細資訊，請參閱 [Microsoft Azure App Service Web 應用程式符合 PCI 標準 3.0 和 3.1 的規範](https://support.microsoft.com/help/3124528)。

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>如何使用 hello 預備環境和部署位置？

在標準和高階應用程式服務計劃，當您部署您的 web 應用程式 tooApp 服務，您可以部署 tooa 不同的部署位置，而不是 toohello 預設生產位置。 部署位置是具有專屬主機名稱的即時 Web 應用程式。 Web 應用程式的內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。

如需有關使用部署位置的詳細資訊，請參閱[在 App Service 中設定預備環境](web-sites-staged-publishing.md)。

## <a name="how-do-i-access-and-review-webjob-logs"></a>如何存取及檢閱 WebJob 記錄？

tooreview WebJob 記錄檔：

1. 登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。
2. 選取 hello WebJob。
3. 選取 hello**切換輸出** 按鈕。
4. toodownload hello 輸出檔中，選取 hello**下載**連結。
5. 針對個別的執行，選取 [個別叫用]。
6. 選取 hello**切換輸出** 按鈕。
7. 選取 hello 下載連結。

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>我試著使用 SQL Server toouse 混合式連線。 為什麼看 hello 訊息 「 System.OverflowException： 數學運算導致溢位 」？

如果您使用混合式連線 tooaccess SQL Server 時，於 2016 年 10 的 Microsoft.NET 更新可能會導致連線 toofail。 您可能會看到下列訊息：

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>解決方案

我們正在 tooupdate 混合式連線管理員 toofix 此問題。 如需因應措施，請參閱[SQL Server 的混合式連線錯誤：System.OverflowException：數學運算導致溢位](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/)。

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>如何新增或編輯 URL 重寫規則？

tooadd 或編輯 URL 重寫規則：

1. 設定網際網路資訊服務 (IIS) 管理員，以便連接 tooyour App Service web 應用程式。 如何 tooconnect IIS 管理員 tooApp 服務，請參閱的 toolearn[使用 IIS 管理員的 Azure 網站的遠端管理](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/)。
2. 在 IIS 管理員中，新增或編輯 URL 重寫規則。 toolearn 如何 tooadd] 或 [編輯 URL 重寫規則，請參閱[建立重寫規則的 hello URL rewrite 模組](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)。

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>我要如何控制輸入的流量 tooApp 服務？

在 hello 網站層級，您有兩個選項來控制輸入的流量 tooApp 服務：

* 開啟動態 IP 限制。 如何 tooturn 上動態 IP 限制，請參閱的 toolearn [Azure 網站的 IP 及網域限制](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/)。
* 開啟模組安全性。 如何 tooturn 模組的安全性，請參閱的 toolearn [ModSecurity web 應用程式防火牆在 Azure 網站上的](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/)。

如果您使用 App Service Environment，您可以使用 [Barracuda 防火牆](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/)。

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>如何封鎖 App Service Web 應用程式中的連接埠？

在 hello 應用程式服務共用的租用戶環境，則不是特定連接埠可能 tooblock 由於 hello 本質之故 hello 基礎結構。 TCP 連接埠 4016、4018 和 4020 也可能已經針對 Visual Studio 遠端偵錯而開啟。

在 App Service Environment 中，您對於輸入與輸出流量有完整控制權。 您可以使用網路安全性群組 toorestrict 或封鎖特定連接埠。 如需 App Service Environment 的詳細資訊，請參閱[App Service Environment 簡介](https://azure.microsoft.com/blog/introducing-app-service-environment/)。

## <a name="how-do-i-capture-an-f12-trace"></a>如何擷取 F12 追蹤？

您有兩個選項可以用來擷取 F12 追蹤：

* F12 HTTP 追蹤
* F12 主控台輸出

### <a name="f12-http-trace"></a>F12 HTTP 追蹤

1. 在 Internet Explorer 中，移 tooyour 網站。 您沒有 hello 接下來的步驟之前，它會在重要 toosign。 否則，hello F12 追蹤會擷取敏感性登入資料。
2. 按下 F12。
3. 請確認該 hello**網路** 索引標籤，並選取然後選取 hello 綠色**播放** 按鈕。
4. 請勿 hello 重現 hello 問題的步驟。
5. 選取 hello 紅色**停止** 按鈕。
6. 選取 hello**儲存**按鈕 （磁片圖示），並將 hello HAR 檔案儲存 （在 Internet Explorer 和邊緣）*或*hello HAR 檔案，以滑鼠右鍵按一下，然後選取**內容另存為 HAR** (在 Chrome 中)。

### <a name="f12-console-output"></a>F12 主控台輸出

1. 選取 hello**主控台** 索引標籤。
2. 每個索引標籤，其中包含零個以上的項目，選取 [hello] 索引標籤 (**錯誤**，**警告**，或**資訊**)。 如果沒有選取 hello 索引標籤，hello 索引標籤的圖示是灰色或黑色移開 hello 資料指標時。
3. Hello 訊息區域中的 hello 窗格中，以滑鼠右鍵按一下，然後選取**複製所有**。
4. 貼上 hello 文字在檔案中，複製並儲存 hello 檔案。

tooview HAR 檔案，您可以使用 hello [HAR 檢視器](http://www.softwareishard.com/har/viewer/)。

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>為什麼我收到錯誤當我嘗試 tooconnect App Service web 應用程式 tooa 虛擬網路，連線的 tooExpressRoute？

如果您嘗試 tooconnect Azure web 應用程式 tooa 連線虛擬網路已 tooAzure ExpressRoute，它會失敗。 hello 會出現下列訊息: 「 閘道 」 不 VPN 閘道。

目前，您不能有點對站 VPN 連線 tooa 虛擬網路，連線的 tooExpressRoute。 點對站 VPN 和 ExpressRoute 不能共存在 hello 相同虛擬網路。 如需詳細資訊，請參閱 [ExpressRoute 和站對站 VPN 連線限制](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations)。

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>如何連接 App Service web 應用程式 tooa 虛擬網路，靜態的路由 （以原則為基礎） 閘道？

目前不支援連接 App Service web 應用程式 tooa 虛擬網路，靜態的路由 （以原則為基礎） 閘道。 如果您的目標虛擬網路已經存在，您必須先啟用，動態路由閘道，才能連接的 tooan 應用程式的點對站 VPN。 如果您的閘道設定 toostatic 路由，您無法啟用點對站 VPN。 

如需詳細資訊，請參閱[將應用程式與 Azure 虛擬網路整合](web-sites-integrate-with-vnet.md#getting-started)。

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>為什麼我就算有 2 個可用的背景工作角色，卻還是只能在 App Service Environment 中建立一個 App Service 方案？

tooprovide 容錯功能，App Service 環境需要每個背景工作集區需要至少一個額外的計算資源。 hello 額外的計算資源不能指定工作負載。

如需詳細資訊，請參閱[如何 toocreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>為什麼當我嘗試 toocreate App Service 環境看到逾時？

有時候，建立 App Service Environment 會失敗。 在此情況下，您會看到下列錯誤 hello 活動記錄檔中的 hello:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve，請確定無 hello 下列條件成立：
* hello 子網路為太小。
* hello 子網路不是空的。
* ExpressRoute 防止 App Service 環境的 hello 網路連線需求。
* 不正確的網路安全性群組可防止您的 App Service 環境的 hello 網路連線需求。
* 強制通道已開啟。

如需詳細資訊，請參閱[部署 (建立) 新的 Azure App Service Environment 時最常遇到的問題](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/)。

## <a name="why-cant-i-delete-my-app-service-plan"></a>為什麼我無法刪除 App Service 方案？

如果任何 App Service 應用程式與 hello 應用程式服務方案相關聯，您無法刪除 App Service 方案。 刪除 App Service 方案之前，請從 hello 應用程式服務方案中移除所有相關聯的應用程式服務應用程式。

## <a name="how-do-i-schedule-a-webjob"></a>如何排程 WebJob？

您可以使用 Cron 運算式建立已排程 WebJob：

1. 建立 settings.job 檔案。
2. 在此 JSON 檔案中，使用 Cron 運算式以包含排程屬性： 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

如需已排程 WebJobs 的詳細資訊，請參閱[使用 Cron 運算式來建立已排程 WebJob](web-sites-create-web-jobs.md#CreateScheduledCRON)。

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>如何執行 App Service 應用程式的滲透測試？

tooperform 滲透測試[提交要求](https://security-forms.azure.com/penetration-testing/terms)。

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>如何針對使用流量管理員的 App Service Web 應用程式設定自訂網域名稱？

如何 toouse 自訂網域名稱與 App Service 應用程式使用 Azure Traffic Manager 負載平衡，請參閱的 toolearn[流量管理員設定 Azure web 應用程式的自訂網域名稱](web-sites-traffic-manager-custom-domain-name.md)。

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>我的 App Service 憑證標示為詐騙。 如何解決這個問題？

App Service 憑證購買 hello 網域驗證，您可能會看到下列訊息的 hello:

「您的憑證已標示為可能詐騙。 hello 要求目前正在進行檢閱。 如果 hello 憑證不會使用 24 小時內，請連絡 Azure 支援。 」

Hello 訊息表示，如這個詐騙驗證程序可能佔用 too24 小時 toocomplete。 在此期間，您將會繼續 toosee hello 訊息。

如果您的應用程式服務的憑證在 24 小時後，此訊息將繼續 tooshow，請執行下列 PowerShell 指令碼的 hello。 hello 指令碼連絡人 hello[憑證提供者](https://www.godaddy.com/)直接 tooresolve hello 問題。

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>驗證和授權如何在 App Service 中運作？

如需 App Service 中驗證和授權的詳細文件，請參閱 [App Service 安全性](../app-service/app-service-security-readme.md)。 hello 文件也具有資訊有關設定應用程式服務 toouse 各種識別提供者登入：
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Microsoft 帳戶](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>如何導向 hello 預設 *。 azurewebsites.net 網域 toomy Azure web 應用程式的自訂網域？

當您建立新的網站透過 Web 應用程式在 Azure 中，預設值*sitename*。 azurewebsites.net 網域 tooyour 站台指派。 如果您新增自訂主機名稱 tooyour 站台並不希望您的預設使用者 toobe 無法 tooaccess *。 azurewebsites.net 網域中，您可以重新導向 hello 預設 URL。 toolearn 如何 tooredirect 所有流量從您的網站預設網域 tooyour 的自訂網域，請參閱[重新導向 hello 預設網域 tooyour 自訂網域在 Azure web 應用程式](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/)。

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>如何判斷安裝在 App Service 中的是哪一個版本的 .NET？

hello 最快方式 toofind hello 新版的 Microsoft.NET 應用程式服務中安裝是使用 hello Kudu 主控台。 您可以從 hello 入口網站或使用 App Service 應用程式的 hello URL 來存取 hello Kudu 主控台。 如需詳細指示，請參閱[判斷 hello 安裝應用程式服務中的.NET 版本](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/)。

## <a name="why-isnt-autoscale-working-as-expected"></a>為什麼自動調整無法如預期般運作？

如果 Azure 自動調整規模尚未在調整或擴充 hello web 應用程式執行個體，如您所預期，您可能執行的情況中，我們刻意選擇不 tooscale tooavoid 無限迴圈因為太"出現 flapping 的現象。 」 當 hello 向外延展和小數位數的臨界值之間沒有足夠的邊界時，就會發生這種情形。 如何 tooavoid"出現 flapping 的現象"和 tooread 有關其他自動調整規模的最佳作法，請參閱的 toolearn[自動調整規模的最佳作法](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices)。

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>為什麼自動調整有時候只會部分調整？

當計量超出預先設定的界限時，會觸發自動調整。 有時候，您可能會注意到 hello 容量只有部分填滿您所預期的比較的 toowhat。 無法使用您想要的執行個體的 hello 數目時，也可能會發生。 在該案例中，自動調整部分填滿入 hello 可用執行個體數目。 自動調整規模則會執行 hello 重新平衡邏輯 tooget 更多容量。 它會配置 hello 剩餘的執行個體。 請注意，這可能需要幾分鐘的時間。

如果您沒有看到預期 hello 的執行個體數幾分鐘後，它可能是因為 hello 部分填滿 hello 界限內足夠 toobring hello 度量。 或者，您也可以自動調整規模可能會有比例縮小，因為它已達到 hello 下限標準。

如果這些條件都不適用，而且 hello 問題持續發生，請提交支援要求。

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>如何針對內容開啟 HTTP 壓縮？

對於靜態和動態的內容類型，壓縮 tooturn 加入下列程式碼 toohello 應用程式層級的 web.config 檔的 hello:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

您也可以指定 hello 特定動態和靜態的 MIME 類型的 toocompress。 如需詳細資訊，請參閱我們回應 tooa 論壇中的問題[httpCompression 設定簡單的 Azure 網站上](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview)。

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>如何將從內部部署環境 tooApp 服務移轉？

從 Windows 和 Linux web 伺服器 tooApp 服務 toomigrate 站台，您可以使用 Azure 應用程式服務移轉小幫手。 hello 移轉工具中如有需要 Azure 中建立 web 應用程式和資料庫，並接著將發佈 hello 內容。 如需詳細資訊，請參閱 [Azure App Service 移轉小幫手](https://www.movemetothecloud.net/)。
