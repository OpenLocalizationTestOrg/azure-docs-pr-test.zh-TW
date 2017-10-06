---
title: "開始使用 Web 應用程式的生產環境中測試 aaaGet"
description: "深入了解 Azure App Service Web 應用程式中的實際執行環境 (TiP) 功能中的 hello 測試。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>開始使用 Web Apps 的生產測試
在生產環境中測試，或使用實際的客戶流量實測您的 Web 應用程式，是應用程式開發人員逐漸整合至其[靈活式開發](https://en.wikipedia.org/wiki/Agile_software_development)方法的測試策略。 它可讓您 tootest hello 品質的應用程式與即時的使用者流量在實際執行環境中，做為相對於的 toosynthesized 在測試環境中的資料。 藉由公開您新的應用程式 tooreal 使用者，您可以通知 hello 真正的問題，一旦部署之後，您的應用程式可能會面臨上。 您可以確認 hello 功能、 效能及針對 hello 磁碟區、 速度，以及各種不同的真正的使用者流量，您可以在測試環境中永遠不會近似您應用程式更新的值。

## <a name="traffic-routing-in-app-service-web-apps"></a>App Service Web Apps 中的流量路由
以 hello 流量路由功能[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，您可以直接使用即時的使用者流量 tooone 或多個部分[部署位置](web-sites-staged-publishing.md)，然後分析應用程式與[Azure 應用程式Insights](/services/application-insights/)或[Azure HDInsight](/services/hdinsight/)，或是協力廠商工具，像是[New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate 您的變更。 例如，您可以實作下列案例與應用程式服務的 hello:

* 探索功能的 bug，或找出效能瓶頸的更新先前 toosite 全部署
* 藉由測量可用性度量 hello beta 應用程式上的執行"受到控制的測試班機 」 您的變更
* 逐漸增加 tooa 新的更新，並依正常程序向 toohello 目前版本，如果發生錯誤 
* 在多個部署位置中執行 [A/B 測試](https://en.wikipedia.org/wiki/A/B_testing)或[多變量測試](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing)，以最佳化應用程式的商務成果

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>在 Web Apps 中使用流量路由的需求
* 您的 Web 應用程式必須在**標準**或**進階**層執行，因為多個部署位置有此需求。
* 在訂單 toowork 流量路由需要正常運作，cookie toobe hello 使用者的瀏覽器中啟用。 流量路由會使用 hello 生命 hello 用戶端工作階段 cookie toopin 用戶端瀏覽器 tooa 部署位置。
* 流量路由可透過 Azure PowerShell Cmdlet 支援進階的TiP 案例。

## <a name="route-traffic-segment-tooa-deployment-slot"></a>路由流量區段 tooa 部署位置
在 hello 基本層級中每個提示的情況，您要路由即時流量 tooa 非生產環境部署您的位置預先定義的百分比的表示。 toodo，後續 hello 步驟：

> [!NOTE]
> hello 以下步驟假設您已經具備[非生產環境部署位置](web-sites-staged-publishing.md)和該 hello 所需的 web 應用程式內容已經是[部署](web-sites-deploy.md)tooit。
> 
> 

1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [流量路由]。
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. 您想 tooroute 流量 tooand hello 百分比 hello 總流量您想要然後按一下 選取 hello 插槽**儲存**。
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. 移 toohello 部署位置的刀鋒視窗。 您現在應該會看到被路由的 tooit 的即時流量。
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

流量路由設定之後，hello 指定百分比的用戶端會隨機路由的 tooyour 非生產環境位置。 不過，它是重要 toonote 一旦用戶端會自動路由的 tooa 特定位置，它會是 「 固定 」 toothat hello 該用戶端工作階段的存留期間的位置。 完成上述使用 cookie toopin hello 使用者工作階段。 如果您檢查 hello HTTP 要求時，您會發現`TipMix`中每個後續要求的 cookie。

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>強制用戶端要求 tooa 特定位置
加法 tooautomatic 流量路由傳送中，應用程式服務會是能 tooroute 要求 tooa 特定位置。 當您想您使用者 toobe 無法 tooopt 時這非常有用-成或退出集 beta 應用程式。 toodo，使用 hello`x-ms-routing-name`查詢參數。

tooreroute 使用者 tooa 特定位置使用`x-ms-routing-name`，您必須確定該 hello 位置已新增 toohello 流量路由清單。 因為要明確 tooroute tooa 位置，並不重要 hello 實際路由您設定的百分比。 如果您想，您就可以建立 「 beta 連結 」 的使用者可以按一下 tooaccess hello beta 應用程式。

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>讓使用者選擇退出 beta 應用程式
toolet 使用者退出 beta 應用程式，例如，您可以將此連結放在網頁中：

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

hello 字串`x-ms-routing-name=self`指定 hello 生產位置。 一旦 hello 用戶端瀏覽器存取 hello 連結不只是它重新導向 toohello 生產位置，但每個後續的要求將會包含 hello`x-ms-routing-name=self`釘選 hello 工作階段 toohello 生產位置的 cookie。

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>選擇 toobeta 應用程式中的使用者
toolet 使用者參加 tooyour beta 應用程式、 設定 hello 相同查詢參數 toohello 名稱 hello 非生產位置，例如：

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>其他資源
* [針對 Azure App Service 中的 Web 應用程式設定預備環境](web-sites-staged-publishing.md)
* [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)
* [敏捷式軟體開發 (Agile Software Development) 與 Azure App Service](app-service-agile-software-development.md)
* [為 Web 應用程式有效地使用 DevOps 環境](app-service-web-staged-publishing-realworld-scenarios.md)

