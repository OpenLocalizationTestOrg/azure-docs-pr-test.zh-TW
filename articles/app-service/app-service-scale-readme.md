---
title: "Azure App Service：調整 App Service 應用程式"
description: "了解 hello 內外的應用程式服務中調整應用程式。"
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
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="f469a-104">Azure App Service：調整 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="f469a-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="f469a-105">在 Azure App Service 中裝載的應用程式可以達到最大規模 [Canadian Broadcasting Corporation/Radio-Canada leverage Azure for smooth election coverage (加拿大廣播公司/加拿大廣播電台運用 Azure 處理大選新聞)](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)。</span><span class="sxs-lookup"><span data-stu-id="f469a-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="f469a-106">不過，調整應用程式是很複雜的問題，沒有所謂的「一體適用」方案。</span><span class="sxs-lookup"><span data-stu-id="f469a-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="f469a-107">toocorrectly 調整應用程式有 3 會導致 tooyour 應用程式成功的主要區域：</span><span class="sxs-lookup"><span data-stu-id="f469a-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="f469a-108">了解您的應用程式架構和其缺點。</span><span class="sxs-lookup"><span data-stu-id="f469a-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="f469a-109">您的應用程式是否可設定狀態？</span><span class="sxs-lookup"><span data-stu-id="f469a-109">Is your Application Stateful?</span></span> <span data-ttu-id="f469a-110">沒有狀態？</span><span class="sxs-lookup"><span data-stu-id="f469a-110">Stateless?</span></span>
   * <span data-ttu-id="f469a-111">應用程式的所有 hello 元件有哪些都？</span><span class="sxs-lookup"><span data-stu-id="f469a-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="f469a-112">Hello 應用程式中的 hello 瓶頸哪裡？</span><span class="sxs-lookup"><span data-stu-id="f469a-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="f469a-113">套用的 tooyour 應用程式負載時，功能將會中斷第一個項目？</span><span class="sxs-lookup"><span data-stu-id="f469a-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="f469a-114">了解 hello 預期負載和效能需求。</span><span class="sxs-lookup"><span data-stu-id="f469a-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="f469a-115">Hello 應用程式需要 tooserve 一千使用者嗎？或一百萬嗎？</span><span class="sxs-lookup"><span data-stu-id="f469a-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="f469a-116">流量是來自單一地區或全球？</span><span class="sxs-lookup"><span data-stu-id="f469a-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="f469a-117">是否有季節性變化及流量尖峰？</span><span class="sxs-lookup"><span data-stu-id="f469a-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="f469a-118">應該多快回應 hello 應用程式？</span><span class="sxs-lookup"><span data-stu-id="f469a-118">How fast should hello app respond?</span></span> <span data-ttu-id="f469a-119">1 秒？</span><span class="sxs-lookup"><span data-stu-id="f469a-119">1 second?</span></span> <span data-ttu-id="f469a-120">1 毫秒？</span><span class="sxs-lookup"><span data-stu-id="f469a-120">1 millisecond?</span></span>
3. <span data-ttu-id="f469a-121">了解及正確運用 hello 平台裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="f469a-122">功能的應該我運用 tooachieve 我小數位數的目標嗎？</span><span class="sxs-lookup"><span data-stu-id="f469a-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="f469a-123">本章節將協助您了解所有 hello 因素以及協助您設計策略，會利用 hello 必要應用程式服務功能 tooachieve 延展性目標。</span><span class="sxs-lookup"><span data-stu-id="f469a-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

