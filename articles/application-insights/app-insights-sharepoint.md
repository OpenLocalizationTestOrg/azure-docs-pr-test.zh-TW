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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="8f9bb-103">使用 Application Insights 監視 SharePoint 網站</span><span class="sxs-lookup"><span data-stu-id="8f9bb-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="8f9bb-104">Azure 的 Application Insights 監視 hello 可用性、 效能和您的應用程式的使用方式。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="8f9bb-105">這裡您將學習如何 tooset 針對 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="8f9bb-106">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="8f9bb-106">Create an Application Insights resource</span></span>
<span data-ttu-id="8f9bb-107">在 hello [Azure 入口網站](https://portal.azure.com)，建立新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="8f9bb-108">選擇 ASP.NET 做為 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-108">Choose ASP.NET as hello application type.</span></span>

![按一下 內容選取 hello 金鑰，請按 ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="8f9bb-110">hello 刀鋒視窗中開啟的是，您會看到效能和使用方式資料有關應用程式的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="8f9bb-111">tooget 後 tooit 下次登入時 tooAzure，您應該尋找磚 hello [開始] 畫面上。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="8f9bb-112">或者按一下 瀏覽 toofind 它。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="8f9bb-113">新增指令碼 tooyour 網頁</span><span class="sxs-lookup"><span data-stu-id="8f9bb-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="8f9bb-114">在 快速入門中，取得網頁 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="8f9bb-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="8f9bb-115">插入 hello 指令碼之前 hello &lt;/前端&gt;標記要 tootrack 的每一頁。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="8f9bb-116">如果您的網站有主版頁面，您可以那里出 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="8f9bb-117">例如，在 ASP.NET MVC 專案中，可放在 View\Shared\_Layout.cshtml 中</span><span class="sxs-lookup"><span data-stu-id="8f9bb-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="8f9bb-118">hello 指令碼包含 hello 將導向 hello 遙測 tooyour Application Insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="8f9bb-119">新增 hello 程式碼 tooyour 網站頁面</span><span class="sxs-lookup"><span data-stu-id="8f9bb-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="8f9bb-120">在 hello 主版頁面</span><span class="sxs-lookup"><span data-stu-id="8f9bb-120">On hello master page</span></span>
<span data-ttu-id="8f9bb-121">如果您可以編輯 hello 站台的主版頁面，會提供監視 hello 站台中每個頁面。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="8f9bb-122">簽出 hello 主版頁面，並使用 SharePoint Designer 或任何其他編輯器進行編輯。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="8f9bb-123">加入 hello 程式碼之前 hello</head>標記。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="8f9bb-124">或在個別的頁面上</span><span class="sxs-lookup"><span data-stu-id="8f9bb-124">Or on individual pages</span></span>
<span data-ttu-id="8f9bb-125">toomonitor 一組有限的頁面，將另外新增 hello 指令碼 tooeach 頁面。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="8f9bb-126">插入 web 組件和嵌入 hello 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="8f9bb-127">檢視應用程式相關的資料</span><span class="sxs-lookup"><span data-stu-id="8f9bb-127">View data about your app</span></span>
<span data-ttu-id="8f9bb-128">重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-128">Redeploy your app.</span></span>

<span data-ttu-id="8f9bb-129">傳回 tooyour 應用程式 刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8f9bb-130">hello 第一個事件會出現在搜尋中。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="8f9bb-131">如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="8f9bb-132">從 hello 概觀刀鋒視窗中，按一下 **流量分析**toosee toocharts 使用者、 工作階段及頁面檢視：</span><span class="sxs-lookup"><span data-stu-id="8f9bb-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="8f9bb-133">按一下任何圖 toosee 更多詳細資料-例如頁面檢視：</span><span class="sxs-lookup"><span data-stu-id="8f9bb-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="8f9bb-134">或使用者：</span><span class="sxs-lookup"><span data-stu-id="8f9bb-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="8f9bb-135">擷取使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="8f9bb-135">Capturing User Id</span></span>
<span data-ttu-id="8f9bb-136">hello 標準網頁程式碼片段不會擷取 hello 使用者識別碼，從 SharePoint，但是您可以進行，以小小的修改。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="8f9bb-137">複製 hello Essentials Application Insights 中的下拉式清單中的應用程式的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="8f9bb-138">'XXXX' hello 檢測金鑰替換在 hello 以下程式碼片段中。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="8f9bb-139">嵌入您的 SharePoint 應用程式，而不是您從 hello 入口網站取得的 hello 程式碼片段中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="8f9bb-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f9bb-140">Next Steps</span></span>
* <span data-ttu-id="8f9bb-141">[Web 測試](app-insights-monitor-web-app-availability.md)toomonitor hello 可用性，您的網站。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="8f9bb-142">[Application Insights](app-insights-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="8f9bb-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


