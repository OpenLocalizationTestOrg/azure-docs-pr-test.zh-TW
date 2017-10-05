---
title: "Azure App Service 的運作方式"
description: "了解 App Service 的運作方式"
keywords: "App Service, Azure App Service, 級別, 可調整, App Service方案, App Service 成本"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="2923e-104">App Service 的運作方式</span><span class="sxs-lookup"><span data-stu-id="2923e-104">How App Service works</span></span>
<span data-ttu-id="2923e-105">Azure App Service 是一項雲端服務，設計用來解決現今工程師所面臨的實務問題。</span><span class="sxs-lookup"><span data-stu-id="2923e-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="2923e-106">App Service 著重於提供絕佳的開發人員生產力，而不需妥協於以雲端規模提供應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="2923e-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="2923e-107">App Service 也會提供建立企業營運應用程式所需的功能與架構。</span><span class="sxs-lookup"><span data-stu-id="2923e-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="2923e-108">App Service 可讓您使用最熱門的開發語言 (包括 Java、PHP、Node.js、Python 和 Microsoft.NET 語言) 來開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="2923e-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="2923e-109">使用 App Service，您可以：</span><span class="sxs-lookup"><span data-stu-id="2923e-109">With App Service, you can:</span></span>

* <span data-ttu-id="2923e-110">建置可高度調整的 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="2923e-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="2923e-111">使用一組容易使用的行動功能 (例如資料後端、使用者驗證及推播通知) 快速建置 Mobile Apps 後端。</span><span class="sxs-lookup"><span data-stu-id="2923e-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="2923e-112">使用 API Apps 實作、部署和發佈 API。</span><span class="sxs-lookup"><span data-stu-id="2923e-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="2923e-113">將商務應用程式結合到工作流程中，並使用 Logic Apps 轉換資料。</span><span class="sxs-lookup"><span data-stu-id="2923e-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="2923e-114">所有的應用程式類型均依賴可調整和彈性的 Web Apps 平台，其可讓開發人員擁有從應用程式設計到應用程式維護的最佳化完整生命週期體驗。</span><span class="sxs-lookup"><span data-stu-id="2923e-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="2923e-115">生命週期功能可達到下列各項：</span><span class="sxs-lookup"><span data-stu-id="2923e-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="2923e-116">**快速建立應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2923e-116">**Quick app creation**.</span></span> <span data-ttu-id="2923e-117">從頭開始，或從 Azure Marketplace 選取作業支援系統 (OSS) 套件。</span><span class="sxs-lookup"><span data-stu-id="2923e-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="2923e-118">**連續部署**。</span><span class="sxs-lookup"><span data-stu-id="2923e-118">**Continuous deployment**.</span></span> <span data-ttu-id="2923e-119">從受歡迎的原始檔控制解決方案 (例如 TFS、GitHub 和 Bitbucket) 自動部署新程式碼和從線上儲存服務 (例如 OneDrive 和 Dropbox) 同步處理內容。</span><span class="sxs-lookup"><span data-stu-id="2923e-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="2923e-120">**在生產環境中測試**。</span><span class="sxs-lookup"><span data-stu-id="2923e-120">**Test in production**.</span></span> <span data-ttu-id="2923e-121">順利建立預生產環境及管理通往這些環境的流量。</span><span class="sxs-lookup"><span data-stu-id="2923e-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="2923e-122">需要時在雲端偵錯，並在發現問題時回復。</span><span class="sxs-lookup"><span data-stu-id="2923e-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="2923e-123">**執行非同步工作和批次作業**。</span><span class="sxs-lookup"><span data-stu-id="2923e-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="2923e-124">在背景程序中執行程式碼或根據事件 (例如，訊息登陸在 Azure 儲存體佇列中) 及排定的時間 (CRON) 啟動程式碼。</span><span class="sxs-lookup"><span data-stu-id="2923e-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="2923e-125">**調整應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2923e-125">**Scaling the app**.</span></span> <span data-ttu-id="2923e-126">使用許多選項之一，根據流量和資源使用率自動水平及垂直調整服務。</span><span class="sxs-lookup"><span data-stu-id="2923e-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="2923e-127">設定您的應用程式專用的私人環境。</span><span class="sxs-lookup"><span data-stu-id="2923e-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="2923e-128">**維護應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2923e-128">**Maintaining the app**.</span></span> <span data-ttu-id="2923e-129">運用許多的偵錯和診斷功能防患於未燃並且有效解決問題，無論是即時 (例如自動修復和即時偵錯功能) 或事後 (透過分析記錄檔和記憶體傾印)。</span><span class="sxs-lookup"><span data-stu-id="2923e-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="2923e-130">整體而言，App Service 功能可讓開發人員專注於他們的程式碼，並能快速達到穩定且高調整性的生產狀態。</span><span class="sxs-lookup"><span data-stu-id="2923e-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="2923e-131">使用 API Apps 和 Logic Apps 功能，開發人員可以建置真實的企業應用程式，以將商務解決方案及內部部署之間的障礙銜接至雲端整合。</span><span class="sxs-lookup"><span data-stu-id="2923e-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="2923e-132">影片</span><span class="sxs-lookup"><span data-stu-id="2923e-132">Videos</span></span>
* [<span data-ttu-id="2923e-133">Azure App Service 架構</span><span class="sxs-lookup"><span data-stu-id="2923e-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="2923e-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2923e-134">Next steps</span></span>

<span data-ttu-id="2923e-135">在下列其中一個主題中深入了解 App Service：</span><span class="sxs-lookup"><span data-stu-id="2923e-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="2923e-136">什麼是 Azure 應用程式服務？</span><span class="sxs-lookup"><span data-stu-id="2923e-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="2923e-137">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2923e-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="2923e-138">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="2923e-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="2923e-139">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2923e-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="2923e-140">Azure App Service 架構 (展示)</span><span class="sxs-lookup"><span data-stu-id="2923e-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="2923e-141">Azure App Service、雲端服務與虛擬機器之比較</span><span class="sxs-lookup"><span data-stu-id="2923e-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="2923e-142">了解 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2923e-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="2923e-143">App Service 環境簡介</span><span class="sxs-lookup"><span data-stu-id="2923e-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="2923e-144">演練：建立 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="2923e-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="2923e-145">Azure App Service 開發堆疊支援</span><span class="sxs-lookup"><span data-stu-id="2923e-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



