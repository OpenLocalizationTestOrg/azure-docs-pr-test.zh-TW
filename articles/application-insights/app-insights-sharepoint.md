---
title: "使用 Application Insights 監視 SharePoint 網站"
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
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="d429b-103">使用 Application Insights 監視 SharePoint 網站</span><span class="sxs-lookup"><span data-stu-id="d429b-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="d429b-104">Azure Application Insights 會監視應用程式的可用性、效能和使用情況。</span><span class="sxs-lookup"><span data-stu-id="d429b-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="d429b-105">您將在這裡深入了解如何針對 SharePoint 網站進行設定。</span><span class="sxs-lookup"><span data-stu-id="d429b-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="d429b-106">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="d429b-106">Create an Application Insights resource</span></span>
<span data-ttu-id="d429b-107">在 [Azure 入口網站](https://portal.azure.com)中，建立新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="d429b-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="d429b-108">選擇 ASP.NET 做為應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="d429b-108">Choose ASP.NET as the application type.</span></span>

![按一下 [屬性]，選取金鑰，然後按下 CTRL+C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="d429b-110">開啟的刀鋒視窗是您要查看您的應用程式效能和使用量資料的位置。</span><span class="sxs-lookup"><span data-stu-id="d429b-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="d429b-111">若要在下次登入 Azure 時回到此位置，您應該會在開始畫面上發現它的磚。</span><span class="sxs-lookup"><span data-stu-id="d429b-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="d429b-112">或者按一下 [瀏覽] 以尋找它。</span><span class="sxs-lookup"><span data-stu-id="d429b-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="d429b-113">將我們的指令碼加入至您的網頁</span><span class="sxs-lookup"><span data-stu-id="d429b-113">Add our script to your web pages</span></span>
<span data-ttu-id="d429b-114">在快速入門中，取得網頁指令碼：</span><span class="sxs-lookup"><span data-stu-id="d429b-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="d429b-115">在您想要追蹤之每一個頁面的 &lt;/head&gt; 標記前插入指令碼。如果您的網站有主版頁面，您可以那裡放入指令碼。</span><span class="sxs-lookup"><span data-stu-id="d429b-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="d429b-116">例如，在 ASP.NET MVC 專案中，可放在 View\Shared\_Layout.cshtml 中</span><span class="sxs-lookup"><span data-stu-id="d429b-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="d429b-117">指令碼包含檢測金鑰，會將遙測導向您的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="d429b-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="d429b-118">將程式碼加入至網站頁面</span><span class="sxs-lookup"><span data-stu-id="d429b-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="d429b-119">在主要頁面上</span><span class="sxs-lookup"><span data-stu-id="d429b-119">On the master page</span></span>
<span data-ttu-id="d429b-120">如果您可以編輯網站的主要頁面，將會提供網站中每一頁面的監視。</span><span class="sxs-lookup"><span data-stu-id="d429b-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="d429b-121">簽出主要頁面，並且使用 SharePoint Designer 或任何其他編輯器來編輯。</span><span class="sxs-lookup"><span data-stu-id="d429b-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="d429b-122">在 </head> 標記之前加入程式碼。</span><span class="sxs-lookup"><span data-stu-id="d429b-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="d429b-123">或在個別的頁面上</span><span class="sxs-lookup"><span data-stu-id="d429b-123">Or on individual pages</span></span>
<span data-ttu-id="d429b-124">若要監視一組有限的頁面，將指令碼個別加入至每個頁面。</span><span class="sxs-lookup"><span data-stu-id="d429b-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="d429b-125">插入網頁組件並在其中嵌入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="d429b-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="d429b-126">檢視應用程式相關的資料</span><span class="sxs-lookup"><span data-stu-id="d429b-126">View data about your app</span></span>
<span data-ttu-id="d429b-127">重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d429b-127">Redeploy your app.</span></span>

<span data-ttu-id="d429b-128">返回 [Azure 入口網站](https://portal.azure.com)中的應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d429b-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d429b-129">前幾個事件將出現在搜尋中。</span><span class="sxs-lookup"><span data-stu-id="d429b-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="d429b-130">如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="d429b-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="d429b-131">從 [概觀] 刀鋒視窗按一下 [使用情況分析]  以查看使用者、工作階段和頁面檢視次數的圖表：</span><span class="sxs-lookup"><span data-stu-id="d429b-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="d429b-132">按一下任何圖表以查看更多詳細資料 - 例如頁面檢視次數：</span><span class="sxs-lookup"><span data-stu-id="d429b-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="d429b-133">或使用者：</span><span class="sxs-lookup"><span data-stu-id="d429b-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="d429b-134">擷取使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="d429b-134">Capturing User Id</span></span>
<span data-ttu-id="d429b-135">標準網頁程式碼片段不會從 SharePoint 擷取使用者識別碼，但只要稍做修改就能執行此作業。</span><span class="sxs-lookup"><span data-stu-id="d429b-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="d429b-136">從 Application Insights 中的 [Essentials] 下拉式清單複製您應用程式的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="d429b-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="d429b-137">使用檢測金鑰替換下列程式碼片段中的 'XXXX'。</span><span class="sxs-lookup"><span data-stu-id="d429b-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="d429b-138">在您的 SharePoint 應用程式中內嵌指令碼，而非您從入口網站取得的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="d429b-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="d429b-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d429b-139">Next Steps</span></span>
* <span data-ttu-id="d429b-140">[Web 測試](app-insights-monitor-web-app-availability.md) 。</span><span class="sxs-lookup"><span data-stu-id="d429b-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="d429b-141">[Application Insights](app-insights-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="d429b-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


