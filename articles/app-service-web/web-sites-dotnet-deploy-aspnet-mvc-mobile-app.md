---
title: "Azure App Service 中的 ASP.NET MVC 5 aaaDeploy 行動 web 應用程式"
description: "此教學課程將教導您如何使用行動應用程式服務的 web 應用程式 tooAzure toodeploy 功能在 ASP.NET MVC 5 web 應用程式。"
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>在 Azure App Service 中部署 ASP.NET MVC 5 行動 Web 應用程式
本教學課程將教導您 hello toobuild ASP.NET MVC 5 web 應用程式是行動設備友善的基本概念，並將其部署 tooAzure 應用程式服務。 此教學課程中，您需要[Visual Studio Express 2013 for Web] [ Visual Studio Express 2013]或 hello professional 版的 Visual Studio，如果您已經有的。 您可以使用[Visual Studio 2015]但 hello 螢幕擷取畫面會不同，而且您必須使用 hello ASP.NET 4.x 範本。

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>您要建置的內容
此教學課程中，您將新增 mobile 功能 toohello 簡單會議清單的應用程式提供中 hello[入門專案][StarterProject]。 hello 下列螢幕擷取畫面顯示 hello ASP.NET 工作階段中完成的 hello 應用程式，Internet Explorer 11 F12 開發人員工具中的 hello 瀏覽器模擬器中所見。

![][FixedSessionsByTag]

您可以使用 hello Internet Explorer 11 F12 開發者工具與 hello [Fiddler 工具][ Fiddler] toohelp 偵錯應用程式。 

## <a name="skills-youll-learn"></a>您要學習的技術
以下是您要學習的內容：

* 如何 toouse Visual Studio 2013 toopublish web 應用程式直接 tooa web 應用程式在 Azure App Service 中的。
* ASP.NET MVC 5 hello 範本若要改善顯示行動裝置上的所使用的 hello CSS 啟動安裝程式架構
* 如何 toocreate 行動特定檢視 tootarget 特定行動瀏覽器，例如 hello iPhone 和 Android
* 如何 toocreate 回應的檢視表 （跨裝置回應 toodifferent 瀏覽器的檢視）

## <a name="set-up-hello-development-environment"></a>設定 hello 開發環境
設定您的開發環境，藉由安裝 hello Azure SDK for.net 2.5.1 或更新版本。 

1. tooinstall hello Azure SDK for.NET 中，按一下下方的 hello 連結。 如果您沒有 Visual Studio 2013 尚未安裝，它將會安裝 hello 連結。 本教學課程需要 Visual Studio 2013。 [Azure SDK for Visual Studio 2013][AzureSDKVs2013]
2. 在 hello Web Platform Installer 視窗中，按一下 **安裝**並繼續進行 hello 安裝。

您還需要一個行動瀏覽器模擬器。 Hello 下列任何一項工作將會：

* [Internet Explorer 11 F12 開發人員工具][EmulatorIE11]中的瀏覽器模擬器 (使用於所有行動瀏覽器螢幕擷取畫面中)。 它具有 Windows Phone 8、Windows Phone 7 和 Apple iPad 的使用者代理程式字串預設項目。
* [Google Chrome DevTools][EmulatorChrome] (英文) 中的瀏覽器模擬器。 它包含許多 Android 裝置，以及 Apple iPhone、Apple iPad 和 Amazon Kindle Fire 的預設項目。 它也會模擬觸控事件。
* [Opera Mobile 模擬器][EmulatorOpera]

Visual Studio 專案以 C\#原始碼是本主題提供 tooaccompany:

* [入門專案下載][StarterProject]
* [完成專案下載][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>部署 hello 入門專案 tooan Azure web 應用程式
1. 下載 hello 會議清單應用程式[入門專案][StarterProject]。
2. 在 Windows 檔案總管中，以滑鼠右鍵按一下 hello 下載 ZIP 檔案，然後選擇 *屬性*。
3. 在 [hello**屬性**對話方塊方塊中，選擇 hello**解除封鎖**] 按鈕。 (解除封鎖可避免安全性警告，發生於您嘗試 toouse *.zip*您已經從 hello web 下載的檔案。)
4. Hello ZIP 檔案上按一下滑鼠右鍵，然後選取**全部解壓縮**解壓縮 hello 檔案。 
5. 在 Visual Studio 中，開啟 hello *C#\Mvc5Mobile.sln*檔案。
6. 在 方案總管 hello 專案上按一下滑鼠右鍵，然後按一下**發行**。
   
   ![][DeployClickPublish]
7. 在 [發佈 Web] 中，按一下 [Microsoft Azure App Service] 。
   
   ![][DeployClickWebSites]
8. 如果您尚未登入 Azure，請按一下 [新增帳戶] 。
   
   ![][DeploySignIn]
9. 遵循 hello 提示 toolog 到您的 Azure 帳戶。
10. hello 應用程式服務 對話方塊應顯示您為登入。 按一下 [新增] 。
    
    ![][DeployNewWebsite]  
11. 在 hello **Web 應用程式名稱**欄位中，指定唯一的應用程式名稱前置詞。 您的完整 Web 應用程式名稱將是 &lt;prefix>.azurewebsites.net。 另外，請在 [資源群組] 中選取或指定新的資源群組名稱。 然後，按一下 **新增**toocreate 新的應用程式服務方案。
    
    ![][DeploySiteSettings]
12. 設定 hello 新的 App Service 方案，按一下**確定**。 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. 在 hello 建立應用程式服務 對話方塊中，按一下 **建立**。
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Hello Azure 資源建立之後，hello 發行 Web 對話方塊將會填入您新的應用程式的 hello 設定。 按一下 [發行] 。
    
    ![][DeployPublishSite]
    
    Visual Studio 完成發行 hello 入門專案 toohello Azure web 應用程式時，一旦 hello 桌面瀏覽器會開啟 toodisplay hello 即時 web 應用程式。
15. 啟動您的行動電話瀏覽器模擬器，複製 hello hello 會議應用程式的 URL (*<prefix>*。 名稱是.azurewebsites.net) 到 hello 模擬器，然後按一下右上方按鈕並選取**標記瀏覽**. 如果您使用 Internet Explorer 11 和 hello 的預設瀏覽器，您只需要 tootype `F12`，然後`Ctrl+8`，然後將變更 hello 瀏覽器的設定檔太**Windows Phone**。 下圖顯示 hello *AllTags*直向模式中的檢視 (從選擇**標記來瀏覽**)。
    
    ![][AllTags]

> [!TIP]
> 雖然您可以將 MVC 5 應用程式與 Visual Studio 內偵錯，您可以發佈您的 web 應用程式 tooAzure 再次 tooverify hello 即時 web 應用程式直接從您的行動瀏覽器或瀏覽器模擬器。
> 
> 

hello 顯示是很容易閱讀，行動裝置上。 您也已經可以看見 hello hello Bootstrap CSS framework 所套用的視覺效果的部分。
按一下 hello **ASP.NET**連結。

![][SessionsByTagASP.NET]

hello ASP.NET 標記檢視是縮放納入 toohello 畫面上，啟動程序會為您自動執行。 不過，您也可以改善這個檢視 toobetter 勝利 hello 行動瀏覽器。 例如，hello**日期**資料行是難以閱讀。 稍後在 hello 教學課程中，您要變更 hello *AllTags*檢視 toomake 它行動設備友善。

## <a name="bkmk_bootstrap"></a> Bootstrap CSS 架構
新增在 hello MVC 5 範本是內建的啟動程序支援。 您已看到它立即改善 hello 應用程式中的不同檢視的方式。 比方說，hello hello 頂端的巡覽列時，會自動摺疊 hello 瀏覽器寬度是較小。 在 hello 桌面瀏覽器，請嘗試調整大小 hello 瀏覽器視窗中，查看 hello 導覽列如何變更其外觀與風格。 這是啟動安裝程式已內建的 hello 回應的 web 設計。

toosee hello Web 應用程式看起來沒有啟動程序，會如何開啟*應用程式\_啟動\\BundleConfig.cs*和註解包含的 hello 行*bootstrap.js*和*bootstrap.css*。 hello 下列程式碼顯示 hello 最後兩個陳述式的 hello `RegisterBundles` hello 變更之後的方法：

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

按`Ctrl+F5`toorun hello 應用程式。

觀察該 hello 可摺疊導覽列是現在只有一般的未排序的清單。 再按一下 [依標籤瀏覽]，然後按一下 [ASP.NET]。
在 hello 行動模擬器檢視中，您可以看到它不再縮放納入 toohello 畫面上，且您必須在順序 toosee hello 右邊 hello 資料表側邊捲動。

![][SessionsByTagASP.NETNoBootstrap]

復原您的變更，並重新整理 hello 行動瀏覽器 tooverify hello 行動設備友善顯示已還原。

啟動載入器不是特定 tooASP.NET MVC 5，您可在任何 web 應用程式中使用這些功能。 但它目前內建於 ASP.NET MVC 5 專案範本中，所以 MVC 5 Web 應用程式可根據預設利用 Bootstrap。

如需有關啟動程序的詳細資訊，請移至 toothe [Bootstrap] [ BootstrapSite]站台。

Hello 下一節中，您會看到如何 tooprovide mobile 瀏覽器中的特定檢視。

## <a name="bkmk_overrideviews"></a>覆寫 hello 檢視、 配置和部分檢視
您可以覆寫大多數的行動瀏覽器、個別行動瀏覽器或任何特定瀏覽器的所有檢視，包含配置及部分檢視。 tooprovide 行動特定檢視中，您可以複製檢視檔案，並新增*。Mobile* toohello 檔案名稱。 例如，toocreate 行動*索引* 檢視中，您可以複製*檢視\\首頁\\Index.cshtml*來*檢視\\首頁\\Index.Mobile.cshtml*。

本節將建立行動裝置專屬的配置檔案。

toostart，複製*檢視\\共用\\\_Layout.cshtml*至*檢視\\共用\\\_Layout.Mobile.cshtml*. 開啟 *\_Layout.Mobile.cshtml*並將變更從 hello 標題**MVC5 應用程式**太**MVC5 應用程式 （行動裝置版）**。

在每個`Html.ActionLink`呼叫 hello 導覽列中，移除 瀏覽方式 」 中每個連結*ActionLink*。 hello 下列程式碼顯示 hello 完成`<ul class="nav navbar-nav">`hello 行動配置檔案標記。

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

複製 hello*檢視\\首頁\\AllTags.cshtml*檔案*檢視\\首頁\\AllTags.Mobile.cshtml*。 開啟 hello 新檔案，並變更`<h2>`"Tags"中的項目太"標記 (M)":

    <h2>Tags (M)</h2>

瀏覽 toohello 標記頁面使用桌面瀏覽器，並使用行動電話瀏覽器模擬器。 hello 行動瀏覽器模擬器顯示 hello 兩個您所做的變更 (hello 標題與 *\_Layout.Mobile.cshtml*和從 hello 標題*AllTags.Mobile.cshtml*)。

![][AllTagsMobile_LayoutMobile]

相反地，未變更 hello 桌面顯示 (其標題中從 *\_Layout.cshtml*和*AllTags.cshtml*)。

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> 建立瀏覽器專用的檢視
此外 toomobile 專屬和桌面特定檢視中，您可以建立個別的瀏覽器的檢視。 例如，您可以建立專門用於 hello iPhone 或 hello Android 瀏覽器的檢視。 在本節中，您要建立 hello iPhone 瀏覽器和 iPhone 版的 hello 的版面配置*AllTags*檢視。

開啟 hello *Global.asax*檔案，然後加入下列程式碼 toohello 底部 hello`Application_Start`方法。

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

此程式碼會定義要比對每個連入要求且名為 "iPhone" 的新顯示模式。 如果 hello 傳入要求符合您定義 （亦即，如果 hello 使用者代理程式包含 hello 字串"iPhone"） 的條件，ASP.NET MVC 會尋找其名稱中包含"iPhone"後置詞的檢視。

> [!NOTE]
> 當新增行動裝置的特定瀏覽器顯示模式，例如適用於 iPhone 和 Android，是確定 tooset hello 第一個引數太`0`（hello hello 清單頂端插入） toomake 確定該 hello 瀏覽器特定模式的優先順序高於 hello 行動範本(*.Mobile.cshtml)。 如果 hello 行動範本 hello hello 清單頂端相反地，它會選取透過您想要的顯示模式 （hello 第一個相符項目 wins，以及 hello 行動範本符合所有的行動瀏覽器）。 
> 
> 

Hello 程式碼中，以滑鼠右鍵按一下`DefaultDisplayMode`，選擇**解決**，然後選擇  `using System.Web.WebPages;`。 這會將參考 toothe`System.Web.WebPages`命名空間，這是 where`DisplayModeProvider`和`DefaultDisplayMode`類型定義。

![][ResolveDefaultDisplayMode]

或者，您可以只手動加入下列行 toothe hello `using` hello 檔案區段。

    using System.Web.WebPages;

儲存 hello 的變更。 將 Views\\Shared\\\_Layout.Mobile.cshtml 檔案複製到 Views\\Shared\\\_Layout.iPhone.cshtml。 開啟 hello 新檔案，然後變更 從 hello 標題`MVC5 Application (Mobile)`至`MVC5 Application (iPhone)`。

複製 hello*檢視\\首頁\\AllTags.Mobile.cshtml*檔案*檢視\\首頁\\AllTags.iPhone.cshtml*。 在 hello 新檔案，變更 hello`<h2>`項目從 「 標記 (M) 」 太 」 標記 (iPhone) 」。

執行 hello 應用程式。 執行行動瀏覽器模擬器，請確定其使用者代理程式設定得 「 iPhone"，並瀏覽 toohello *AllTags*檢視。 如果您使用 Internet Explorer 11 F12 開發人員工具中的 hello 模擬器，請設定模擬 toohello 下列：

* 瀏覽器設定檔 = **Windows Phone**
* 使用者代理程式字串 =  **Custom**
* 自訂字串 = **Apple-iPhone5C1/1001.525**

hello 下列螢幕擷取畫面顯示 hello *AllTags*檢視呈現在 Internet Explorer 11 F12 開發人員工具與 hello 自訂使用者代理字串中的模擬器 （此為 iPhone 5 C 使用者代理字串）。

![][AllTagsIPhone_LayoutIPhone]

在 hello 行動瀏覽器中，選取 hello**喇叭**連結。 因為不是行動檢視 (*AllSpeakers.Mobile.cshtml*)，檢視 hello 預設喇叭 (*AllSpeakers.cshtml*) 呈現使用 hello 行動版面配置檢視 ( *\_Layout.Mobile.cshtml*)。 如下所示 hello 標題**MVC5 應用程式 （行動裝置版）**中定義 *\_Layout.Mobile.cshtml*。

![][AllSpeakers_LayoutMobile]

您可以藉由設定全域停用預設的 （非行動電話） 檢視行動配置內呈現`RequireConsistentDisplayMode`至`true`在 hello*檢視\\\_ViewStart.cshtml*檔案，就像這樣：

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

當`RequireConsistentDisplayMode`設定得`true`，hello 行動配置 (*\_Layout.Mobile.cshtml*) 只適用於行動檢視 (也就是當檢視表檔案是 hello 表單 ***ViewName**.Mobile.cshtml*)。 您可能會想 tooset`RequireConsistentDisplayMode`太`true`如果您的行動配置效果不佳非行動檢視。 hello 螢幕擷取畫面所示方式 hello*喇叭*頁面轉譯時`RequireConsistentDisplayMode`設定得`true`（不含 hello hello 頂端導覽列中的 hello 字串 」 （行動裝置版） 」）。

![][AllSpeakers_LayoutMobileOverridden]

您可以藉由設定停用特定檢視中的一致的顯示模式`RequireConsistentDisplayMode`太`false`hello 檢視檔案中。 下列標記中 hello*檢視\\首頁\\AllSpeakers.cshtml*檔案集`RequireConsistentDisplayMode`太`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

本節中，我們已看到如何 toocreate 行動版面配置和檢視與 toocreate 版面配置和特定裝置，例如檢視 hello iPhone。
不過，hello hello Bootstrap CSS framework 主要優點是回應式配置，這表示單一樣式表可以套桌面、 電話和平板電腦瀏覽器 toocreate 一致的外觀及操作。 Hello 下一節中您會看到 tooleverage 啟動 toocreate 行動設備友善的載入檢視。

## <a name="bkmk_Improvespeakerslist"></a>改善 hello 喇叭清單
如您剛才所見，hello*喇叭*檢視是可讀取，但 hello 連結都很小，而且難以 tootap 行動裝置上的。 在本節中，您要進行 hello *AllSpeakers*檢視行動設備友善，其中顯示大型、 簡單點選連結，並包含搜尋方塊 tooquickly 尋找喇叭。

您可以使用啟動程序 hello[連結的清單群組][ linked list group]樣式以改善 hello*喇叭*檢視。 在*檢視\\首頁\\AllSpeakers.cshtml*，hello hello Razor 檔案的內容取代 hello 的下列程式碼。

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

hello`class="list-group"`中 hello 屬性`<div>`標記，套用的啟動程序清單樣式和 hello`class="input-group-item"`屬性適用於啟動程序的清單項目樣式 tooeach 連結。

重新整理 hello 行動瀏覽器。 hello 更新檢視看起來像這樣：

![][AllSpeakersFixed]

啟動程序 hello[連結的清單群組][ linked list group]樣式使 hello 整個方塊的每個連結點選，也就是更好的使用者經驗。 切換 toothe 桌面檢視，並觀察 hello 一致的外觀及操作。

![][AllSpeakersFixedDesktop]

雖然 hello 行動瀏覽器檢視已經改善，很難瀏覽 hello 長串喇叭。 Bootstrap 並沒有現成的搜尋篩選功能，但您可以用數行程式碼來新增此功能。 您第一次會新增搜尋方塊 toohello 檢視，然後以 hello hello 篩選函數的 JavaScript 程式碼連結。 在*檢視\\首頁\\AllSpeakers.cshtml*，新增\<表單\>標記後方 hello \<h2\>標記，如下所示：

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

請注意該 hello`<form>`和`<input>`這兩個標記有 hello 啟動程序所套用的樣式 toothem。 hello`<span>`項目會新增啟動載入器[glyphicon] [ glyphicon] toothe [搜尋] 方塊。

在 hello*指令碼*資料夾中，加入 JavaScript 檔案，稱為*filter.js*。 開啟 hello 檔案並貼上下列程式碼中的 hello:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

您也需要 tooinclude filter.js 中您已註冊的組合。 開啟*應用程式\_啟動\\BundleConfig.cs*並變更 hello 第一個組合。 變更第一個`bundles.Add`陳述式 (hello **jquery**組合) tooinclude*指令碼\\filter.js*、，如下所示：

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

hello **jquery**配套已呈現 hello 預設*\_配置*檢視。 稍後，您可以利用 hello 相同的 JavaScript 程式碼 tooapply 篩選功能 tooother 清單檢視。

重新整理 hello 行動瀏覽器並移 toohello *AllSpeakers*檢視。 在搜尋方塊中，輸入 "sc"。 hello 喇叭清單應立即篩選根據 tooyour 搜尋字串。

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>改善 hello 標籤清單
像 hello*喇叭*檢視，hello*標記* 檢視來得容易讀懂，但 hello 連結是小型且難度增加 tootap 行動裝置上的。 您可以修正 hello*標記*檢視 hello 相同方式修正 hello*喇叭*檢視時，如果您使用更早版本，但 hello 下列所述的 hello 程式碼變更`Html.ActionLink`方法語法中的*檢視\\首頁\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

hello 重新整理桌面瀏覽器的外觀，如下所示：

![][AllTagsFixedDesktop]

與 hello 重新整理行動瀏覽器的外觀，如下所示： 

![][AllTagsFixed]

> [!NOTE]
> 如果您注意到 hello 原始清單格式處於仍有 hello 行動瀏覽器並不知道哪種情形的 tooyour nice 啟動載入器樣式，這是您先前動作 toocreate 行動特定檢視的成品。 不過，現在您要使用 hello Bootstrap CSS framework toocreate 回應的 web 設計，回到並移除這些行動裝置的特定檢視和 hello 行動特定版面配置檢視。 一旦您這樣做，hello 重新整理行動瀏覽器會顯示 hello 啟動程序的樣式。
> 
> 

## <a name="bkmk_improvedates"></a>改善 hello 日期 清單
您可以改善 hello*日期*檢視像改善 hello*喇叭*和*標記*檢視如果使用 hello 程式碼變更描述更早版本，但以 hello 遵循`Html.ActionLink`方法語法中的*檢視\\首頁\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

重新整理後，您會獲得如下的行動瀏覽器檢視：

![][AllDatesFixed]

您可以進一步改善 hello*日期*檢視依日期組織 hello 日期時間值。 這可以使用 hello 啟動程序來完成[面板][ panels]樣式設定。 取代 hello hello 內容*檢視\\首頁\\AllDates.cshtml*以下列程式碼檔案：

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

此程式碼會建立個別`<div class="panel panel-primary">`標記每個不同日期 hello 清單，並使用 hello[連結的清單群組][ linked list group]與之前的各個連結。 以下是 hello 行動瀏覽器時執行此程式碼看起來像：

![][AllDatesFixed2]

切換 toohello 桌面瀏覽器。 同樣地，請注意 hello 一致的外觀。

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>改善 hello SessionsTable 檢視
在本節中，您要進行 hello *SessionsTable*檢視更多的行動設備友善。 這項變更是更廣泛的 hello 先前的變更。

在 hello 行動瀏覽器中，點選 hello**標記**按鈕，然後輸入`asp`搜尋 方塊中。

![][AllTagsFixedSearchByASP]

點選 hello **ASP.NET**連結。

![][SessionsTableTagASP.NET]

如您所見，hello 顯示會格式化為資料表，也就是目前設計的 toobe hello 桌面瀏覽器中檢視。 不過，它會有點困難 tooread 行動瀏覽器上。 toofix，開啟*檢視\\首頁\\SessionsTable.cshtml* ，然後將檔案的 hello 內容取代下列程式碼的 hello:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

hello 程式碼會執行 3 件事：

* 使用 hello Bootstrap[自訂連結的清單群組][ custom linked list group] tooformat hello 工作階段資訊，使這項資訊可在行動裝置瀏覽器 （例如使用類別讀取清單群組的項目-文字）
* 適用於 hello[方格系統][ grid system] toothe 版面配置，因此該 hello 工作階段的項目 hello 桌面瀏覽器中水平及垂直 hello 行動瀏覽器 （使用 hello col-md-4 類別） 中的資料流程
* 使用 hello[回應公用程式][ responsive utilities]隱藏 hello 工作階段標記時 （使用 hello 隱藏 xs 類別） 的 hello 行動瀏覽器中檢視

您也可以點選標題連結 toogo toohello 個別工作階段。 hello 圖會反映 hello 程式碼變更。

![][FixedSessionsByTag]

您在自動套用的 hello 啟動程序的方格系統排列垂直在 hello 行動瀏覽器工作階段。 另外而且請注意，不會顯示 hello 標記。 切換 toohello 桌面瀏覽器。

![][SessionsTableFixedTagASP.NETDesktop]

在 hello 桌面瀏覽器，請注意，現在會顯示 hello 標記。 此外，您可以看到您所套用的 hello 啟動程序的方格系統排列 hello 兩個資料行中的工作階段項目。 如果您放大瀏覽器，您會看到 hello 排列方式變更 toothree 資料行。

## <a name="bkmk_improvesessionbycode"></a>改善 hello SessionByCode 檢視
最後，您將會修正 hello *SessionByCode*檢視 toomake 它行動設備友善。

在 hello 行動瀏覽器中，點選 hello**標記**按鈕，然後輸入`asp`搜尋 方塊中。

![][AllTagsFixedSearchByASP]

點選 hello **ASP.NET**連結。 會顯示 hello ASP.NET 標記的工作階段。

![][FixedSessionsByTag]

選擇 hello**建置單一頁面應用程式使用 ASP.NET 和 AngularJS**連結。

![][SessionByCode3-644]

hello 預設桌面檢視沒有問題，但您可以輕鬆地改善 hello 外觀，使用一些啟動安裝程式 GUI 元件。

開啟*檢視\\首頁\\SessionByCode.cshtml*並且 hello 內容取代 hello 下列標記：

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

hello 新標記會使用啟動程序的面板樣式 tooimprove hello 行動檢視。 

重新整理 hello 行動瀏覽器。 hello 圖會反映 hello 您剛建立的程式碼變更：

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>總結與複習
本教學課程示範了如何 toouse ASP.NET MVC 5 toodevelop 行動設備友善 Web 應用程式。 其中包含：

* 部署 ASP.NET MVC 5 應用程式 tooan App Service web 應用程式
* 用於 MVC 5 應用程式的啟動程序 toocreate 回應 web 版面配置
* 以全域方式覆寫個別檢視的配置、檢視和部分檢視
* 使用 `RequireConsistentDisplayMode` 屬性，控制配置和部分覆寫的強制執行
* 建立目標特定瀏覽器，例如 hello iPhone 瀏覽器的檢視
* 在 Razor 程式碼中套用 Boostrap 樣式

## <a name="see-also"></a>另請參閱
* [回應性 Web 設計的 9 個基本原則](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [官方 Bootstrap 部落格][Official Bootstrap Blog]
* [Tutorial Republic 的 Twitter Bootstrap 教學課程][Twitter Bootstrap Tutorial from Tutorial Republic]
* [啟動程序遊樂場 hello][hello Bootstrap Playground]
* [W3C 推薦的行動 Web 應用程式最佳做法][W3C Recommendation Mobile Web Application Best Practices]
* [W3C 針對媒體查詢的候選推薦做法][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

