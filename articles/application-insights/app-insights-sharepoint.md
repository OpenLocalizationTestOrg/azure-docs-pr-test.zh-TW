---
title: "aaaMonitor SharePoint 網站使用 Application Insights"
description: "開始使用新的檢測金鑰監視新的應用程式"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>使用 Application Insights 監視 SharePoint 網站
Azure 的 Application Insights 監視 hello 可用性、 效能和您的應用程式的使用方式。 這裡您將學習如何 tooset 針對 SharePoint 網站。

## <a name="create-an-application-insights-resource"></a>建立 Application Insights 資源
在 hello [Azure 入口網站](https://portal.azure.com)，建立新的 Application Insights 資源。 選擇 ASP.NET 做為 hello 應用程式類型。

![按一下 內容選取 hello 金鑰，請按 ctrl + C](./media/app-insights-sharepoint/01-new.png)

hello 刀鋒視窗中開啟的是，您會看到效能和使用方式資料有關應用程式的 hello 位置。 tooget 後 tooit 下次登入時 tooAzure，您應該尋找磚 hello [開始] 畫面上。 或者按一下 瀏覽 toofind 它。

## <a name="add-our-script-tooyour-web-pages"></a>新增指令碼 tooyour 網頁
在 快速入門中，取得網頁 hello 指令碼：

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

插入 hello 指令碼之前 hello &lt;/前端&gt;標記要 tootrack 的每一頁。 如果您的網站有主版頁面，您可以那里出 hello 指令碼。 例如，在 ASP.NET MVC 專案中，可放在 View\Shared\_Layout.cshtml 中

hello 指令碼包含 hello 將導向 hello 遙測 tooyour Application Insights 資源的檢測金鑰。

### <a name="add-hello-code-tooyour-site-pages"></a>新增 hello 程式碼 tooyour 網站頁面
#### <a name="on-hello-master-page"></a>在 hello 主版頁面
如果您可以編輯 hello 站台的主版頁面，會提供監視 hello 站台中每個頁面。

簽出 hello 主版頁面，並使用 SharePoint Designer 或任何其他編輯器進行編輯。

![](./media/app-insights-sharepoint/03-master.png)

加入 hello 程式碼之前 hello</head>標記。 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>或在個別的頁面上
toomonitor 一組有限的頁面，將另外新增 hello 指令碼 tooeach 頁面。 

插入 web 組件和嵌入 hello 程式碼片段。

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>檢視應用程式相關的資料
重新部署您的應用程式。

傳回 tooyour 應用程式 刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。

hello 第一個事件會出現在搜尋中。 

![](./media/app-insights-sharepoint/09-search.png)

如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。

從 hello 概觀刀鋒視窗中，按一下 **流量分析**toosee toocharts 使用者、 工作階段及頁面檢視：

![](./media/app-insights-sharepoint/06-usage.png)

按一下任何圖 toosee 更多詳細資料-例如頁面檢視：

![](./media/app-insights-sharepoint/07-pages.png)

或使用者：

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>擷取使用者識別碼
hello 標準網頁程式碼片段不會擷取 hello 使用者識別碼，從 SharePoint，但是您可以進行，以小小的修改。

1. 複製 hello Essentials Application Insights 中的下拉式清單中的應用程式的檢測金鑰。 

    ![](./media/app-insights-sharepoint/02-props.png)

1. 'XXXX' hello 檢測金鑰替換在 hello 以下程式碼片段中。 
2. 嵌入您的 SharePoint 應用程式，而不是您從 hello 入口網站取得的 hello 程式碼片段中的 hello 指令碼。

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>後續步驟
* [Web 測試](app-insights-monitor-web-app-availability.md)toomonitor hello 可用性，您的網站。
* [Application Insights](app-insights-overview.md) 。

<!--Link references-->


