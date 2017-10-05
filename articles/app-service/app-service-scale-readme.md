---
title: "Azure App Service：調整 App Service 應用程式"
description: "了解在 App Service 中調整應用程式的優缺點。"
keywords: "App Service, Azure App Service, 級別, 可調整, App Service方案, App Service 成本"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="154af-104">Azure App Service：調整 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="154af-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="154af-105">在 Azure App Service 中裝載的應用程式可以達到最大規模 [Canadian Broadcasting Corporation/Radio-Canada leverage Azure for smooth election coverage (加拿大廣播公司/加拿大廣播電台運用 Azure 處理大選新聞)](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)。</span><span class="sxs-lookup"><span data-stu-id="154af-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="154af-106">不過，調整應用程式是很複雜的問題，沒有所謂的「一體適用」方案。</span><span class="sxs-lookup"><span data-stu-id="154af-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="154af-107">若要正確調整您的應用程式，下列 3 項要點可協助您順利進行：</span><span class="sxs-lookup"><span data-stu-id="154af-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="154af-108">了解您的應用程式架構和其缺點。</span><span class="sxs-lookup"><span data-stu-id="154af-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="154af-109">您的應用程式是否可設定狀態？</span><span class="sxs-lookup"><span data-stu-id="154af-109">Is your Application Stateful?</span></span> <span data-ttu-id="154af-110">沒有狀態？</span><span class="sxs-lookup"><span data-stu-id="154af-110">Stateless?</span></span>
   * <span data-ttu-id="154af-111">您的應用程式有哪些元件？</span><span class="sxs-lookup"><span data-stu-id="154af-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="154af-112">應用程式的瓶頸在哪裡？</span><span class="sxs-lookup"><span data-stu-id="154af-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="154af-113">當負載套用至您的應用程式時，會最先中斷哪個項目？</span><span class="sxs-lookup"><span data-stu-id="154af-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="154af-114">了解預期的負載和效能需求。</span><span class="sxs-lookup"><span data-stu-id="154af-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="154af-115">應用程式需要為一千個使用者或一百萬個使用者提供服務？</span><span class="sxs-lookup"><span data-stu-id="154af-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="154af-116">流量是來自單一地區或全球？</span><span class="sxs-lookup"><span data-stu-id="154af-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="154af-117">是否有季節性變化及流量尖峰？</span><span class="sxs-lookup"><span data-stu-id="154af-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="154af-118">應用程式回應速度如何？</span><span class="sxs-lookup"><span data-stu-id="154af-118">How fast should the app respond?</span></span> <span data-ttu-id="154af-119">1 秒？</span><span class="sxs-lookup"><span data-stu-id="154af-119">1 second?</span></span> <span data-ttu-id="154af-120">1 毫秒？</span><span class="sxs-lookup"><span data-stu-id="154af-120">1 millisecond?</span></span>
3. <span data-ttu-id="154af-121">了解及正確運用裝載您的應用程式的平台。</span><span class="sxs-lookup"><span data-stu-id="154af-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="154af-122">為了達到我的規模的目標，應該利用哪些功能？</span><span class="sxs-lookup"><span data-stu-id="154af-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="154af-123">本節將有助您了解所有因素，並協助您設計可利用必要的 App Service 功能的策略，以達到延展性目標。</span><span class="sxs-lookup"><span data-stu-id="154af-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

