---
title: "aaaFlighting 部署 （beta） 中測試 Azure 應用程式服務"
description: "了解 tooflight 中應用程式或 beta 版的新功能如何測試您的更新在此端對端教學課程。 它整合了 App Service 功能，例如持續性發佈、位置、流量路由及 Application Insights 整合。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Azure App Service 中的試驗部署 (beta 測試)
本教學課程示範如何 toodo*測試部署*藉由整合 hello 的各種功能[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)和[Azure Application Insights](/services/application-insights/)。

*試驗* 是以有限數量的實際客戶驗證新功能或變更的部署程序，同時也是生產案例中的主要測試。 它是 akin toobeta 測試和有時又稱為 「 受控制的測試途中 」。 許多具有網站空間的大型企業在執行 [靈活開發](https://en.wikipedia.org/wiki/Agile_software_development)時，都採用此方法及早驗證其應用程式更新。 Azure App Service 可讓您使用連續發行生產環境中的 toointegrate 測試和 Application Insights tooimplement hello 相同 DevOps 案例。 此方法的優點包括：

* **取得實際的回饋*之前*更新會發行的 tooproduction** -hello 只有在發行前比您發行時立即取得意見反應好的作法就取得意見反應。 您可以為 hello 產品生命週期的早期測試具有真正的使用者流量與行為的更新。
* **增強[持續性測試導向開發 (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - 透過 Application Insights 的持續性整合和工具整合生產環境中的測試，使用者驗證將可在您的產品生命週期內及早進行。 這有助於減少在手動測試執行上投入的時間。
* **最佳化測試工作流程**-藉由自動化測試使用連續監視檢測生產環境中的，您可以可能完成 hello 目標的各種測試在單一處理序，例如[整合](https://en.wikipedia.org/wiki/Integration_testing)，[迴歸](https://en.wikipedia.org/wiki/Regression_testing)，[可用性](https://en.wikipedia.org/wiki/Usability_testing)，協助工具、 當地語系化、[效能](https://en.wikipedia.org/wiki/Software_performance_testing)，[安全性](https://en.wikipedia.org/wiki/Security_testing)，和[接受](https://en.wikipedia.org/wiki/Acceptance_testing)。

試驗部署牽涉到的不只是路由傳送即時流量而已。 在這類部署中您想 toogain 深入了解儘快，無論意外的錯誤、 效能降低、 使用者經驗的問題。 切記，您面對的是實際的客戶。 因此 toodo 它權限，您必須確定您已設定您 flighting 部署 toogather 所有 hello 資料，您需要在順序 toomake 明智的決策下, 一個步驟。 此教學課程會示範如何 toocollect 資料與 Application Insights，但是您可以使用 New Relic 或其他技術適合您的案例。

## <a name="what-you-will-do"></a>將執行的作業
在此教學課程中，您將學習如何 toobring hello 案例一起 tootest 遵循您在生產環境中的 App Service 應用程式：

* [生產流量路由傳送](app-service-web-test-in-production-get-start.md)tooyour beta 應用程式
* [檢測您的應用程式](../application-insights/app-insights-web-track-usage.md)tooobtain 實用的度量
* 持續部署 beta 應用程式並追蹤即時應用程式計量
* Hello 實際執行應用程式與 hello beta 應用程式 toosee 如何變更程式碼之間的比較度量轉譯 tooresults

## <a name="what-you-will-need"></a>必要元件
* 一個 Azure 帳戶
* 一個 [GitHub](https://github.com/) 帳戶
* Visual Studio 2015-您可以下載 hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)。
* Git 殼層 (隨[GitHub for Windows](https://windows.github.com/))-這可讓您 toorun hello 這兩個 hello Git 和 PowerShell 命令相同的工作階段
* 最新 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) 位元
* Hello 下列的基本了解：
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 範本部署 (請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> 您需要 Azure 帳戶 toocomplete 本教學課程：
>
> * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且它們甚至用完之後，您可以保留 hello 帳戶並使用免費的 Azure 服務，例如 Web 應用程式。
> * 您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。
>
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
>
>

## <a name="set-up-your-production-web-app"></a>設定生產 Web 應用程式
> [!NOTE]
> 本教學課程中使用的 hello 指令碼將會自動設定從 GitHub 儲存機制持續發行。 這會要求您的 GitHub 認證已儲存在 Azure 中，否則 hello 編寫指令碼部署嘗試 tooconfigure 原始檔控制設定 hello web 應用程式時將會失敗。
>
> toostore 您的 GitHub 認證在 Azure 中建立 web 應用程式在 hello [Azure 入口網站](https://portal.azure.com/)和[設定 GitHub 部署](app-service-continuous-deployment.md)。 您只需要 toodo 這一次。
>
>

在典型的 DevOps 案例中，您必須在 Azure 中，即時執行的應用程式而您想 toomake 變更 tooit 透過連續的發佈功能。 在此案例中，您將部署 tooproduction 的範本，您所開發並測試過。

1. 建立您自己的 hello 分岔[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)儲存機制。 如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。 建立分叉之後，即可在瀏覽器中進行查看。

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. 開啟 Git Shell 工作階段。 若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。
3. 建立您分支的本機複本執行下列命令的 hello:

     git clone https://github.com/<your_fork>/ToDoApp.git
4. 您的本機複本之後，瀏覽過*&lt;repository_root >*\ARMTemplates，並執行的 hello deploy.ps1 下列指令碼以唯一的尾碼，如所示：

     .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix>
5. 出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。 請記住您的資料庫認證，因為您將需要 toospecify 它們一次當更新 hello 資源群組。

   您應該會看到 hello 佈建各種不同的 Azure 資源的進度。 當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. 回到 Git Shell 工作階段，並執行：

     .\swap –Name ToDoApp<your_suffix>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Hello 指令碼完成時，請返回 toobrowse toohello 前端的位址 (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello 應用程式在生產環境中執行。
8. 登入 hello [Azure 入口網站](https://portal.azure.com/)，看看建立的內容。

   您應該在 hello 無法 toosee 兩個 web 應用程式相同的資源群組、 具有 hello `Api` hello 名稱中的後置詞。 如果您看一下 hello 資源群組檢視，也會看到 hello SQL 資料庫以及伺服器、 hello 應用程式服務方案及 hello 預備位置 hello web 應用程式。 瀏覽 hello 不同的資源，並比較它們與 *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 範本中的設定方式。

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

您已設定 hello 生產環境應用程式。  現在，我們假設您收到意見反應可用性不佳的 hello 應用程式。 讓您決定 tooinvestigate。 您的應用程式 toogive 將 tooinstrument 您的意見反應。

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>調查：檢測用戶端應用程式的監視/計量
1. 在 Visual Studio 中開啟 *&lt;repository_root>*\src\MultiChannelToDo.sln。
2. 以滑鼠右鍵按一下解決方案 > [管理解決方案的 NuGet 套件] > [還原]，以還原所有的 Nuget 套件。
3. 以滑鼠右鍵按一下**MultiChannelToDo.Web** > **加入 Application Insights 遙測** > **設定**> 變更資源群組tooToDoApp*&lt;your_suffix >* > **加入 Application Insights tooProject**。
4. 在 hello Azure 入口網站，開啟 hello 刀鋒視窗中的 hello **MultiChannelToDo.Web** Application Insight 資源。 接著在 hello**應用程式健全狀況**組件中，按一下**學習 toocollect 瀏覽器頁面載入資料的方式**> 複製程式碼。
5. 新增 hello 複製 JS 檢測程式碼太*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml，hello 結尾之前`<heading>`標記。 它應該包含 Application Insight 資源的 hello 唯一的檢測金鑰。

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. 傳送自訂事件滑鼠按鍵的 tooApplication Insights 加入下列程式碼 toohello 底部主體 hello:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   這個 JavaScript 程式碼片段會傳送自訂事件 tooApplication Insights 每次使用者按一下 hello web 應用程式中的任何位置。
7. 在 Git 命令介面中認可並推送您的變更 tooyour 分叉 GitHub 中。 接著，等到用戶端 toorefresh 瀏覽器。

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. 交換部署的 hello 應用程式變更 tooproduction:

     .\swap –Name ToDoApp<your_suffix>
9. 瀏覽您所設定的 toohello Application Insights 資源。 按一下 [自訂事件]。

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   如果您未看見自訂事件的計量，請等候數分鐘，然後按一下 [重新整理] 。

假設您看見如下的圖表：

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

和其下的 hello 事件方格：

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

根據 tooyour ToDoApp 應用程式程式碼，hello**按鈕**事件對應 toohello 送出按鈕及 hello**輸入**事件對應 toohello 文字方塊。 到目前為止都沒什麼問題。 不過，您似乎沒有理想的按和按非常幾下滑鼠數量 hello 待辦項目上 (hello **LI**事件)。

根據此，您表單 UI 是可點選 hello 的哪個部分，而且是因為 hello 資料指標的樣式的文字選取範圍，它將滑鼠指標停留在 hello 清單項目和它的圖示上時，您是有些使用者的假設產生混淆。

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

您可能會認為此範例是人為的。 不過，您正在進行 toomake 改進 tooyour 應用程式，，然後再執行即時客戶從的 flighting 部署 tooget 可用性的意見反應。

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>檢測伺服器應用程式的監視/計量
由於本教學課程中所示範的 hello 案例只處理 hello 用戶端應用程式，這是一側正切函數。 不過，為求完整起見，您將設定備份 hello 伺服器端應用程式。

1. 以滑鼠右鍵按一下**MultiChannelToDo** > **加入 Application Insights 遙測** > **設定**> 變更資源群組tooToDoApp*&lt;your_suffix >* > **加入 Application Insights tooProject**。
2. 在 Git 命令介面中認可並推送您的變更 tooyour 分叉 GitHub 中。 接著，等到用戶端 toorefresh 瀏覽器。

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. 交換部署的 hello 應用程式變更 tooproduction:

     .\swap –Name ToDoApp<your_suffix>

就這麼簡單！

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>調查： 新增特定位置的標記 tooyour 用戶端應用程式計量
在本節中，您將設定 hello 不同的部署位置 toosend 位置特定遙測 toohello 相同的 Application Insights 資源。 如此一來，您可以比較遙測流量從不同位置 （部署環境） tooeasily 之間的資料，請參閱您的應用程式變更 hello 效果。 在 hello 相同時間，因此您可以繼續 toomonitor 生產應用程式視需要您可以從 hello 其餘部分分離 hello 生產流量。

因為您要收集的資料上的用戶端行為，您將[加入 JavaScript 程式碼的遙測初始設定式 tooyour](../application-insights/app-insights-api-filtering-sampling.md) index.cshtml 中。 如果您想 tootest 伺服器端效能，例如，您也可以執行同樣的伺服器上的程式碼中 (請參閱[應用程式的自訂事件和度量的 Insights API](../application-insights/app-insights-api-custom-events-metrics.md)。

1. 首先，新增 hello 程式碼字 hello 兩`//`註解以下 hello JavaScript 區塊中的，您會加入 toohello`<heading>`稍早標記。

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    這個初始設定式程式碼會造成 hello`appInsights`物件 tooadd hello 呼叫的自訂屬性`Environment`tooevery 片段的遙測資料傳送。
2. 接著，在 Azure 中將此自訂屬性新增為 Web 應用程式的 [位置設定](web-sites-staged-publishing.md#AboutConfiguration) 。 toodo 下列命令，您的 Git 殼層工作階段中，執行的 hello。

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    在您的專案中的 hello Web.config 已經定義了 hello`environment`應用程式設定。 使用此設定，當您測試在本機，hello 應用程式時您的指標會加上`VS Debugger`。 不過，當您變更 tooAzure，Azure 會尋找並使用 hello`environment`相反地，在 hello web 應用程式的組態中設定的應用程式和您的計量會標記為`Production`。
3. 認可並推送您的程式碼變更 tooyour 分叉 github，並等候使用者 toouse hello 新應用程式 （需要 toorefresh hello 瀏覽器）。 因此會佔用大約 15 分鐘的新屬性 tooshow hello Application Insights 中`MultiChannelToDo.Web`資源。

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. 現在，移 toohello**自訂事件**再次刀鋒視窗，然後篩選 hello 度量上`Environment=Production`。 您現在應該能夠 toosee 中的所有 hello 新自訂事件 hello 生產都位置與此篩選條件。

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. 按一下 hello**我的最愛**按鈕 toosave hello 目前計量瀏覽器設定 toosomething 喜歡**自訂事件： 生產**。 後續您可以在此檢視與部署位置檢視之間輕鬆切換。

   > [!TIP]
   > 若要有更強大的分析能力，請考慮 [將 Application Insights 資源與 Power BI 整合](../application-insights/app-insights-export-power-bi.md)。
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>新增特定位置的標記 tooyour 伺服器應用程式計量
同樣地，為求完整起見，您將設定備份 hello 伺服器端應用程式。 不同於檢測在 JavaScript 中的 hello 用戶端應用程式，hello 伺服器應用程式的特定位置的標記已檢測.NET 程式碼。

1. 開啟 *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs。 加入下面 」 之前 hello 左大括號命名空間中的 hello 程式碼區塊。

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. 藉由新增 hello 更正 hello 名稱解析錯誤`using`hello 檔案的下方 toohello 開頭的陳述式：

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. 將程式碼 hello toohello hello 開頭加入`Application_Start()`方法：

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. 認可並推送您的程式碼變更 tooyour 分叉 github，並等候使用者 toouse hello 新應用程式 （需要 toorefresh hello 瀏覽器）。 因此會佔用大約 15 分鐘的新屬性 tooshow hello Application Insights 中`MultiChannelToDo`資源。

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>更新：設定您的 Beta 分支：
1. 開啟 *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json] 和 [尋找 hello`appsettings`資源 (搜尋`"name": "appsettings"`)。 資源共有 4 項，分別用於各個位置。
2. 每個`appsettings`資源，新增`"environment": "[parameters('slotName')]"`應用程式設定的 hello toohello 結尾`properties`陣列。 別忘了以逗點 tooend hello 上的一行。

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    您剛剛加入 hello `environment` hello 範本中設定 tooall hello 位置的應用程式。
3. 在 hello 同一個檔案中尋找 hello`slotconfignames`資源 (搜尋`"name": "slotconfignames"`)。 資源共有 2 項，分別用於各個應用程式。
4. 每個`slotconfignames`資源，新增`"environment"`toohello 結尾 hello`appSettingNames`陣列。 別忘了以逗點 tooend hello 上的一行。

    您剛才 hello`environment`應用程式設定搖桿 tooits 各自的部署位置的兩個應用程式。  
5. 在您的 Git 殼層工作階段中執行的 hello 下列命令以 hello 相同資源群組的後置字元之前使用。

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. 出現提示時，指定與之前 hello 相同 SQL 資料庫認證。 然後，當要求 tooupdate hello 資源群組、 型別`Y`，然後`ENTER`。

    一旦 hello 指令碼完成，就會保留您所有 hello 原始的資源群組中的資源，但名為"beta"的新位置中建立以 hello 相同為 hello 「 預備 」 位置中 hello 開頭所建立的組態。

   > [!NOTE]
   > 這個方法來建立不同的部署環境與不同中的 hello 方法[敏捷式軟體開發使用 Azure App Service](app-service-agile-software-development.md)。 使用此方法時，您會建立具有部署位置的部署環境，而使用該方法時，則建立具有資源群組的部署環境。 管理部署環境與資源群組可讓您 tookeep hello 實際執行環境 off-limits toodevelopers，但並不容易 toodo 測試實際執行環境，您可以輕鬆地使用插槽。
   >
   >

如果需要，也可以藉由下列程式碼建立 alpha 應用程式

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

在本教學課程，只要繼續使用 beta 應用程式即可。

## <a name="update-push-your-updates-toohello-beta-app"></a>更新： Push toohello beta 應用程式更新
備份您想 tooimprove tooyour 應用程式。

1. 確定您此時位於 beta 分支中

        git checkout beta
2. 在 *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml、 尋找 hello`<li>`標記，並新增 hello`style="cursor:pointer"`屬性，如下所示。

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. 認可並推送 tooAzure。
4. 請確認該 hello 變更會立即反映 hello beta 插槽中瀏覽 toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/。 如果您沒有看到 hello 變更尚未重新整理瀏覽器 tooget hello 新 javascript 程式碼。

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

現在您擁有 hello beta 插槽中執行您的變更，您就準備好 tooperform flighting 部署。

## <a name="validate-route-traffic-toohello-beta-app"></a>驗證： 路由流量 toohello beta 應用程式
在本節中，您將會路由傳送流量 toohello beta 應用程式。 為了清楚的示範，您將 tooroute hello 使用者流量 tooit 的重要部分。 事實上，hello tooroute 將取決於您特定的情況下您想要的流量。 比方說，如果您的網站位於 microsoft.com hello 標尺，您可能需要小於您總流量順序 toogain 有用的資料中的一個百分比。

1. 在您的 Git 殼層工作階段，執行下列命令 tooroute hello 一半 hello 生產流量 toohello beta 位置：

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   hello`ReroutePercentage=50`屬性會指定 50%的 hello 生產流量將會路由的 toohello beta 應用程式的 URL (由 hello`ActionHostName`屬性)。
2. 現在瀏覽 toohttp://ToDoApp*&lt;your_suffix >*。 名稱是.azurewebsites.net。 50%的 hello 流量現在應該重新導向的 toohello beta 位置。
3. 在 Application Insights 資源中，篩選環境 hello 度量 ="beta"。

   > [!NOTE]
   > 如果您為另一個的我的最愛儲存此篩選的檢視，您可以輕鬆地翻轉實際伺服器與 beta 檢視之間的 hello 度量資料總管檢視。
   >
   >

在 Application Insights，您會看到類似 toohello 下列假設：

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

這不只顯示有許多詳細 hello 點選`<li>`標記，但上似乎那里 toobe 的點選劇`<li>`標記。 您接著可以推斷人發現新的 hello`<li>`標記可點選而且現在會清除所有先前已完成任務 hello 應用程式中的。

根據 flighting 部署的 hello 資料，您決定您的新 UI 可供生產環境。

## <a name="go-live-move-your-new-code-into-production"></a>實作：將新的程式碼移至生產環境
您要現在準備好 toomove 更新 tooproduction。 很棒的是，現在您已經知道，您的更新已經過驗證*之前*推入 tooproduction。 因此，現在您可以安心地加以部署。 您進行更新 toohello AngularJS 用戶端應用程式時，才會進行驗證 hello 用戶端程式碼。 如果您是 toomake 變更 toohello 後端 Web API 應用程式時，您也可以同樣地，輕鬆地驗證您的變更。

1. 在 Git 命令介面中執行下列命令的 hello 移除 hello 流量路由規則：

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. 執行 hello Git 命令：

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. 等待幾分鐘，讓 hello 新的程式碼部署 toobe toohello 暫存位置，然後啟動 http://ToDoApp*&lt;your_suffix >*-hello 新更新的 staging.azurewebsites.net tooverify 就緒在 hello 預備環境中位置。 請記住分岔的主要分支都是由該 hello 連結 toohello 暫存位置的應用程式。
4. 現在，交換預備位置到實際執行環境的 hello

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>摘要
Azure App Service 方便 toomedium-小型企業 tootest 其客戶對向應用程式在生產環境中，項目具有大型企業中傳統上完成。 希望本教學課程已提供您 hello 您需要 toobring 一起應用程式服務和 Application Insights toomake 可能測試部署和甚至是其他在實際執行的測試案例，DevOps 世界中的知識。

## <a name="more-resources"></a>其他資源
* [敏捷式軟體開發 (Agile Software Development) 與 Azure App Service](app-service-agile-software-development.md)
* [針對 Azure App Service 中的 Web 應用程式設定預備環境](web-sites-staged-publishing.md)
* [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)
* [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint-hello JSON 驗證程式](http://jsonlint.com/)
* [Git 分支 - 基本分支和合併](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [專案 Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
