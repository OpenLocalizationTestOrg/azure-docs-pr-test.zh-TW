---
title: "使用 Azure 流量管理員來控制 Azure Web 應用程式的流量"
description: "本文提供與 Azure Web 應用程式相關之 Azure 流量管理員的摘要資訊。\""
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: fb7d391e3118a9dccde5501c3f30c6f580932a30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a><span data-ttu-id="6b3b1-103">使用 Azure 流量管理員來控制 Azure Web 應用程式的流量</span><span class="sxs-lookup"><span data-stu-id="6b3b1-103">Controlling Azure web app traffic with Azure Traffic Manager</span></span>
> [!NOTE]
> <span data-ttu-id="6b3b1-104">本文提供與 Azure App Service Web Apps 相關之 Microsoft Azure 流量管理員的摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-104">This article provides summary information for Microsoft Azure Traffic Manager as it relates to Azure App Service Web Apps.</span></span> <span data-ttu-id="6b3b1-105">如需 Azure 流量管理員本身的詳細資訊，請造訪本文結尾的連結。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-105">More information about Azure Traffic Manager itself can be found by visiting the links at the end of this article.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="6b3b1-106">簡介</span><span class="sxs-lookup"><span data-stu-id="6b3b1-106">Introduction</span></span>
<span data-ttu-id="6b3b1-107">您可以使用 Azure 流量管理員，來控制如何將來自 Web 用戶端的要求分散至 Azure App Service 中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-107">You can use Azure Traffic Manager to control how requests from web clients are distributed to web apps in Azure App Service.</span></span> <span data-ttu-id="6b3b1-108">將 Web 應用程式端點新增至 Azure 流量管理員設定檔時，Azure 流量管理員就會持續追蹤您 Web 應用程式的狀態 (執行中、已停止或已刪除)，以判定其中哪些端點應接收流量。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-108">When web app endpoints are added to a Azure Traffic Manager profile, Azure Traffic Manager keeps track of the status of your web apps (running, stopped or deleted) so that it can decide which of those endpoints should receive traffic.</span></span>

## <a name="load-balancing-methods"></a><span data-ttu-id="6b3b1-109">負載平衡方法</span><span class="sxs-lookup"><span data-stu-id="6b3b1-109">Load Balancing Methods</span></span>
<span data-ttu-id="6b3b1-110">Azure 流量管理員使用三種不同的負載平衡方法。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-110">Azure Traffic Manager uses three different load balancing methods.</span></span> <span data-ttu-id="6b3b1-111">下列清單說明 Azure Web 應用程式專屬的這些方法。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-111">These are described  in the following list as they pertain to Azure web apps.</span></span>

* <span data-ttu-id="6b3b1-112">**容錯移轉**：如果您在不同地區有 Web 應用程式複本，就可以使用此方法，將某一個 Web 應用程式設定為服務所有 Web 用戶端流量，並在不同地區設定其他 Web 應用程式，以便在第一個 Web 應用程式無法使用時服務該流量。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-112">**Failover**: If you have web app clones in different regions, you can use this method to configure one web app to service all web client traffic, and configure another web app in a different region to service that traffic in case the first web app becomes unavailable.</span></span>
* <span data-ttu-id="6b3b1-113">**循環配置資源**：如果您在不同地區有 Web 應用程式複本，就可以使用此方法，將流量平均分散於不同地區的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-113">**Round Robin**: If you have web app clones in different regions, you can use this method to distribute traffic equally across the web apps in different regions.</span></span>
* <span data-ttu-id="6b3b1-114">**效能**：效能方法可根據前往用戶端的最短來回時間來分散流量。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-114">**Performance**: The Performance method distributes traffic based on the shortest round trip time to clients.</span></span> <span data-ttu-id="6b3b1-115">效能方法可用於相同地區內或不同地區中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-115">The Performance method can be used for web apps within the same region or in different regions.</span></span>

## <a name="web-apps-and-traffic-manager-profiles"></a><span data-ttu-id="6b3b1-116">Web 應用程式和流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="6b3b1-116">Web Apps and Traffic Manager Profiles</span></span>
<span data-ttu-id="6b3b1-117">若要設定以控制 Web 應用程式流量，可在使用上述三種負載平衡方法的其中一種之 Azure 流量管理員中建立設定檔，然後新增要控制其設定檔流量的端點 (在此案例中為 Web 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-117">To configure the control of web app traffic, you create a profile in Azure Traffic Manager that uses one of the three load balancing methods described previously, and then add the endpoints (in this case, web apps) for which you want to control traffic to the profile.</span></span> <span data-ttu-id="6b3b1-118">系統會定期與設定檔溝通您的 Web 應用程式狀態 (執行中、已停止或已刪除)，讓 Azure 流量管理員可相應地導向流量。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-118">Your web app status (running, stopped or deleted) is regularly communicated to the profile so that Azure Traffic Manager can direct traffic accordingly.</span></span>

<span data-ttu-id="6b3b1-119">搭配使用 Azure 流量管理員與 Azure 時，請牢記下列重點：</span><span class="sxs-lookup"><span data-stu-id="6b3b1-119">When using Azure Traffic Manager with Azure, keep in mind the following points:</span></span>

* <span data-ttu-id="6b3b1-120">若為相同地區內的純 Web 應用程式部署，Web Apps 已經提供與 Web 應用程式模式無關的容錯移轉和循環配置資源功能。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-120">For web app only deployments within the same region, Web Apps already provides failover and round-robin functionality without regard to web app mode.</span></span>
* <span data-ttu-id="6b3b1-121">若是在搭配使用 Web Apps 與其他 Azure 雲端服務的相同地區中進行部署，您可以結合兩種端點類型來啟用混合案例。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-121">For deployments in the same region that use Web Apps in conjunction with another Azure cloud service, you can combine both types of endpoints to enable hybrid scenarios.</span></span>
* <span data-ttu-id="6b3b1-122">在設定檔中，您只能針對每個地區指定一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-122">You can only specify one web app endpoint per region in a profile.</span></span> <span data-ttu-id="6b3b1-123">選取一個 Web 應用程式做為某一個地區的端點時，將無法為該設定檔選擇使用該地區中其餘的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-123">When you select a web app as an endpoint for one region, the remaining web apps in that region become unavailable for selection for that profile.</span></span>
* <span data-ttu-id="6b3b1-124">您在 Azure 流量管理員設定檔中指定的 Web 應用程式端點，將出現在設定檔中該 Web 應用程式之 [設定] 頁面的 [網域名稱]  區段下方，但您無法在該處進行設定。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-124">The web app endpoints that you specify in a Azure Traffic Manager profile will appear under the **Domain Names** section on the Configure page for the web app in the profile, but will not be configurable there.</span></span>
* <span data-ttu-id="6b3b1-125">將 Web 應用程式新增至設定檔後，在該 Web 應用程式之入口網站頁面的 [儀表板] 上，[網站 URL]  將顯示 Web 應用程式的自訂網域 URL (如果已設定一個)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-125">After you add a web app to a profile, the **Site URL** on the Dashboard of the web app's portal page will display the custom domain URL of the web app if you have set one up.</span></span> <span data-ttu-id="6b3b1-126">否則會顯示流量管理員設定檔 URL (例如， `contoso.trafficmgr.com`)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-126">Otherwise, it will display the Traffic Manager profile URL (for example, `contoso.trafficmgr.com`).</span></span> <span data-ttu-id="6b3b1-127">Web 應用程式的直接網域名稱和流量管理員 URL 都會顯示在 Web 應用程式之 [設定] 頁面的 [網域名稱]  區段下方。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-127">Both the direct domain name of the web app and the Traffic Manager URL will be visible on the web app's Configure page under the **Domain Names** section.</span></span>
* <span data-ttu-id="6b3b1-128">您的自訂網域名稱將如預期般運作，但除了將之新增至 Web 應用程式外，您還必須設定 DNS 對應以指向流量管理員 URL。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-128">Your custom domain names will work as expected, but in addition to adding them to your web apps, you must also configure your DNS map to point to the Traffic Manager URL.</span></span> <span data-ttu-id="6b3b1-129">如需有關如何設定 Azure Web 應用程式之自訂網域的詳細資訊，請參閱 [設定 Azure 網站的自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-129">For information on how to set up a custom domain for a Azure web app,  see [Configuring a custom domain name for an Azure web site](app-service-web-tutorial-custom-domain.md).</span></span>
* <span data-ttu-id="6b3b1-130">您只能將標準或進階模式的 Web 應用程式新增至 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-130">You can only add web apps that are in standard or premium mode to a Azure Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b3b1-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b3b1-131">Next Steps</span></span>
<span data-ttu-id="6b3b1-132">如需 Azure 流量管理員的概念和技術概觀，請參閱 [Traffic Manager 概觀](../traffic-manager/traffic-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-132">For a conceptual and technical overview of Azure Traffic Manager, see [Traffic Manager Overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="6b3b1-133">如需將流量管理員與 Web Apps 搭配使用的詳細資訊，請參閱[將 Azure 流量管理員與 Azure 網站搭配使用](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx)和 [Azure 流量管理員現在可以與 Azure 網站整合部落格文章](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="6b3b1-133">For more information about using Traffic Manager with Web Apps, see the blog posts [Using Azure Traffic Manager with Azure Web Sites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) and [Azure Traffic Manager can now integrate with Azure Web Sites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).</span></span>

