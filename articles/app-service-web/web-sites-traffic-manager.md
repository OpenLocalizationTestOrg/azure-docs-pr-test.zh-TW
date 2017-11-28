---
title: "aaaControlling Azure web 應用程式流量搭配 Azure 流量管理員"
description: "本文章提供 Azure Traffic Manager 的摘要資訊與相關 tooAzure web 應用程式。"
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
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a><span data-ttu-id="cdbbd-103">使用 Azure 流量管理員來控制 Azure Web 應用程式的流量</span><span class="sxs-lookup"><span data-stu-id="cdbbd-103">Controlling Azure web app traffic with Azure Traffic Manager</span></span>
> [!NOTE]
> <span data-ttu-id="cdbbd-104">本文提供 Microsoft Azure Traffic Manager 的摘要資訊與相關 tooAzure App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-104">This article provides summary information for Microsoft Azure Traffic Manager as it relates tooAzure App Service Web Apps.</span></span> <span data-ttu-id="cdbbd-105">瀏覽 hello 本文結尾處的 hello 連結可以找到有關 Azure Traffic Manager 本身的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-105">More information about Azure Traffic Manager itself can be found by visiting hello links at hello end of this article.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="cdbbd-106">簡介</span><span class="sxs-lookup"><span data-stu-id="cdbbd-106">Introduction</span></span>
<span data-ttu-id="cdbbd-107">您可以使用 Azure Traffic Manager toocontrol 來自 web 用戶端要求的 Azure App Service 中的分散式的 tooweb 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-107">You can use Azure Traffic Manager toocontrol how requests from web clients are distributed tooweb apps in Azure App Service.</span></span> <span data-ttu-id="cdbbd-108">當 web 應用程式端點加入 tooa Azure 流量管理員設定檔時，Azure Traffic Manager 會追蹤的 hello （執行中、 已停止或已刪除） 的 web 應用程式狀態，讓它可以決定這些端點應該接收流量。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-108">When web app endpoints are added tooa Azure Traffic Manager profile, Azure Traffic Manager keeps track of hello status of your web apps (running, stopped or deleted) so that it can decide which of those endpoints should receive traffic.</span></span>

## <a name="load-balancing-methods"></a><span data-ttu-id="cdbbd-109">負載平衡方法</span><span class="sxs-lookup"><span data-stu-id="cdbbd-109">Load Balancing Methods</span></span>
<span data-ttu-id="cdbbd-110">Azure 流量管理員使用三種不同的負載平衡方法。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-110">Azure Traffic Manager uses three different load balancing methods.</span></span> <span data-ttu-id="cdbbd-111">這些都是以 hello 與 tooAzure web 應用程式清單後面所述。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-111">These are described  in hello following list as they pertain tooAzure web apps.</span></span>

* <span data-ttu-id="cdbbd-112">**容錯移轉**： 如果您有 web 應用程式複製程式碼在不同的區域中，您可以使用此方法 tooconfigure 一個 web 應用程式 tooservice 所有的 web 用戶端流量，並在流量案例 hello 第一個 web 應用程式中不同的區域 tooservice 中設定其他 web 應用程式會變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-112">**Failover**: If you have web app clones in different regions, you can use this method tooconfigure one web app tooservice all web client traffic, and configure another web app in a different region tooservice that traffic in case hello first web app becomes unavailable.</span></span>
* <span data-ttu-id="cdbbd-113">**循環配置資源**： 如果您有 web 應用程式複製程式碼在不同的區域中，您可以使用此方法 toodistribute 流量平均跨不同區域中的 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-113">**Round Robin**: If you have web app clones in different regions, you can use this method toodistribute traffic equally across hello web apps in different regions.</span></span>
* <span data-ttu-id="cdbbd-114">**效能**: hello 效能方法會根據 hello 最短的來回行程時間 tooclients 的流量。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-114">**Performance**: hello Performance method distributes traffic based on hello shortest round trip time tooclients.</span></span> <span data-ttu-id="cdbbd-115">hello 效能方法可以用於 hello 內的 web 應用程式相同區域或不同區域。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-115">hello Performance method can be used for web apps within hello same region or in different regions.</span></span>

## <a name="web-apps-and-traffic-manager-profiles"></a><span data-ttu-id="cdbbd-116">Web 應用程式和流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="cdbbd-116">Web Apps and Traffic Manager Profiles</span></span>
<span data-ttu-id="cdbbd-117">tooconfigure hello web 應用程式流量控制，您在 Azure Traffic Manager 中使用其中一個 hello 三個負載平衡方法，建立設定檔，然後再新增想 toocontrol 流量 toohello 的 hello 端點 （在此情況下，web 應用程式）設定檔。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-117">tooconfigure hello control of web app traffic, you create a profile in Azure Traffic Manager that uses one of hello three load balancing methods described previously, and then add hello endpoints (in this case, web apps) for which you want toocontrol traffic toohello profile.</span></span> <span data-ttu-id="cdbbd-118">Web 應用程式狀態 （執行中、 已停止或已刪除） 會定期溝通的 toohello 設定檔，讓 Azure Traffic Manager 可以將流量導向據此。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-118">Your web app status (running, stopped or deleted) is regularly communicated toohello profile so that Azure Traffic Manager can direct traffic accordingly.</span></span>

<span data-ttu-id="cdbbd-119">時搭配 Azure 使用 Azure Traffic Manager，請遵循點注意 hello:</span><span class="sxs-lookup"><span data-stu-id="cdbbd-119">When using Azure Traffic Manager with Azure, keep in mind hello following points:</span></span>

* <span data-ttu-id="cdbbd-120">Web 應用程式僅部署 hello 內相同的區域，Web 應用程式已提供容錯移轉和循環配置資源的功能，而不會考慮 tooweb 應用程式模式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-120">For web app only deployments within hello same region, Web Apps already provides failover and round-robin functionality without regard tooweb app mode.</span></span>
* <span data-ttu-id="cdbbd-121">針對部署在 hello 與另一個 Azure 雲端服務搭配使用 Web 應用程式的相同區域中，您可以結合兩種類型的端點 tooenable 混合式案例。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-121">For deployments in hello same region that use Web Apps in conjunction with another Azure cloud service, you can combine both types of endpoints tooenable hybrid scenarios.</span></span>
* <span data-ttu-id="cdbbd-122">在設定檔中，您只能針對每個地區指定一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-122">You can only specify one web app endpoint per region in a profile.</span></span> <span data-ttu-id="cdbbd-123">當您選取的 web 應用程式為端點，一個區域時，hello 其餘的 web 應用程式在該區域變成無法選取該設定檔中。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-123">When you select a web app as an endpoint for one region, hello remaining web apps in that region become unavailable for selection for that profile.</span></span>
* <span data-ttu-id="cdbbd-124">您在 Azure Traffic Manager 設定檔中指定的 hello web 應用程式端點會出現在 hello**網域名稱**區段 hello hello hello 設定檔中的 web 應用程式設定 頁面上，但不是會設定有。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-124">hello web app endpoints that you specify in a Azure Traffic Manager profile will appear under hello **Domain Names** section on hello Configure page for hello web app in hello profile, but will not be configurable there.</span></span>
* <span data-ttu-id="cdbbd-125">加入 web 應用程式 tooa 設定檔之後，hello**網站 URL** hello 儀表板的 hello web 上應用程式的入口網站頁面會顯示 hello hello web 應用程式的自訂網域 URL 如果您已設定其中一個。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-125">After you add a web app tooa profile, hello **Site URL** on hello Dashboard of hello web app's portal page will display hello custom domain URL of hello web app if you have set one up.</span></span> <span data-ttu-id="cdbbd-126">否則，它會顯示 hello Traffic Manager 設定檔 URL (例如， `contoso.trafficmgr.com`)。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-126">Otherwise, it will display hello Traffic Manager profile URL (for example, `contoso.trafficmgr.com`).</span></span> <span data-ttu-id="cdbbd-127">同時 hello hello web 應用程式的直接的網域名稱，hello 流量管理員 URL 就可以看到在 hello hello web 應用程式的 [設定] 頁面上**網域名稱**> 一節。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-127">Both hello direct domain name of hello web app and hello Traffic Manager URL will be visible on hello web app's Configure page under hello **Domain Names** section.</span></span>
* <span data-ttu-id="cdbbd-128">自訂網域名稱運作正常，但在加法 tooadding 它們 tooyour web 應用程式，您也必須設定您的 DNS 對應 toopoint toohello 流量管理員 URL。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-128">Your custom domain names will work as expected, but in addition tooadding them tooyour web apps, you must also configure your DNS map toopoint toohello Traffic Manager URL.</span></span> <span data-ttu-id="cdbbd-129">如需詳細資訊請參閱 < Azure web 應用程式中，自訂網域 tooset[設定 Azure 網站的自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-129">For information on how tooset up a custom domain for a Azure web app,  see [Configuring a custom domain name for an Azure web site](app-service-web-tutorial-custom-domain.md).</span></span>
* <span data-ttu-id="cdbbd-130">您只能新增標準或進階模式 tooa Azure 流量管理員設定檔中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-130">You can only add web apps that are in standard or premium mode tooa Azure Traffic Manager profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdbbd-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdbbd-131">Next Steps</span></span>
<span data-ttu-id="cdbbd-132">如需 Azure 流量管理員的概念和技術概觀，請參閱 [Traffic Manager 概觀](../traffic-manager/traffic-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-132">For a conceptual and technical overview of Azure Traffic Manager, see [Traffic Manager Overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="cdbbd-133">如需與 Web 應用程式使用 Traffic Manager 的詳細資訊，請參閱 hello 部落格文章[使用 Azure Traffic Manager 與 Azure 網站](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx)和[Azure 流量管理員現在可以整合與 Azure 網站](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="cdbbd-133">For more information about using Traffic Manager with Web Apps, see hello blog posts [Using Azure Traffic Manager with Azure Web Sites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) and [Azure Traffic Manager can now integrate with Azure Web Sites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).</span></span>

