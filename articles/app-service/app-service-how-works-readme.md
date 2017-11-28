---
title: "aaaHow Azure App Service 的運作方式"
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
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="4cecb-104">App Service 的運作方式</span><span class="sxs-lookup"><span data-stu-id="4cecb-104">How App Service works</span></span>
<span data-ttu-id="4cecb-105">Azure App Service 是設計的 toosolve hello 實際問題工程師現今面臨的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4cecb-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="4cecb-106">應用程式服務著重於提供更優異的開發人員生產力，而不會危害 hello 需要在雲端規模 toodeliver 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4cecb-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="4cecb-107">應用程式服務也提供 hello 功能和所需的建立企業的特定業務應用程式的架構。</span><span class="sxs-lookup"><span data-stu-id="4cecb-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="4cecb-108">應用程式服務可讓您開發應用程式中最受歡迎的開發語言，包括 Java、 PHP、 Node.js、 Python 和 hello Microsoft.NET 語言。</span><span class="sxs-lookup"><span data-stu-id="4cecb-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="4cecb-109">使用 App Service，您可以：</span><span class="sxs-lookup"><span data-stu-id="4cecb-109">With App Service, you can:</span></span>

* <span data-ttu-id="4cecb-110">建置可高度調整的 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="4cecb-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="4cecb-111">使用一組容易使用的行動功能 (例如資料後端、使用者驗證及推播通知) 快速建置 Mobile Apps 後端。</span><span class="sxs-lookup"><span data-stu-id="4cecb-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="4cecb-112">使用 API Apps 實作、部署和發佈 API。</span><span class="sxs-lookup"><span data-stu-id="4cecb-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="4cecb-113">將商務應用程式結合到工作流程中，並使用 Logic Apps 轉換資料。</span><span class="sxs-lookup"><span data-stu-id="4cecb-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="4cecb-114">所有應用程式類型依賴 hello 可擴充且彈性的 Web 應用程式平台，可讓開發人員 toohave 最佳化的完整生命週期遇到從應用程式的設計 tooapp 維護。</span><span class="sxs-lookup"><span data-stu-id="4cecb-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="4cecb-115">hello 週期功能啟用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4cecb-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="4cecb-116">**快速建立應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-116">**Quick app creation**.</span></span> <span data-ttu-id="4cecb-117">從頭開始，或選取 從 hello Azure Marketplace 的支援作業系統 (OS) 封裝。</span><span class="sxs-lookup"><span data-stu-id="4cecb-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="4cecb-118">**連續部署**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-118">**Continuous deployment**.</span></span> <span data-ttu-id="4cecb-119">從受歡迎的原始檔控制解決方案 (例如 TFS、GitHub 和 Bitbucket) 自動部署新程式碼和從線上儲存服務 (例如 OneDrive 和 Dropbox) 同步處理內容。</span><span class="sxs-lookup"><span data-stu-id="4cecb-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="4cecb-120">**在生產環境中測試**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-120">**Test in production**.</span></span> <span data-ttu-id="4cecb-121">順利建立預先生產環境和管理 hello 數量 toothem 網路流量。</span><span class="sxs-lookup"><span data-stu-id="4cecb-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="4cecb-122">Hello 雲端需要時，請在偵錯及回復時發現任何問題。</span><span class="sxs-lookup"><span data-stu-id="4cecb-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="4cecb-123">**執行非同步工作和批次作業**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="4cecb-124">在背景程序中執行程式碼或根據事件 (例如，訊息登陸在 Azure 儲存體佇列中) 及排定的時間 (CRON) 啟動程式碼。</span><span class="sxs-lookup"><span data-stu-id="4cecb-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="4cecb-125">**調整 hello 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-125">**Scaling hello app**.</span></span> <span data-ttu-id="4cecb-126">使用其中許多選項 tooautomatically 調整水平及垂直根據流量和資源使用量服務。</span><span class="sxs-lookup"><span data-stu-id="4cecb-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="4cecb-127">設定私用環境專用的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4cecb-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="4cecb-128">**維護 hello 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4cecb-128">**Maintaining hello app**.</span></span> <span data-ttu-id="4cecb-129">使用多個 hello 偵錯和診斷功能 toostay 晚於問題和 tooefficiently 即時 （例如自動修復並即時偵錯功能） 在解決這些問題，或之後 hello 事實，藉由分析記錄檔和記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="4cecb-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="4cecb-130">整個應用程式服務功能會啟用程式碼的開發人員 toofocus 和快速達到穩定且具有高擴充性的生產環境的狀態。</span><span class="sxs-lookup"><span data-stu-id="4cecb-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="4cecb-131">使用 hello API 應用程式和 Logic Apps 功能，開發人員可以建置橋接內部 toocloud 整合商務方案之間的障礙的真實世界企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="4cecb-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="4cecb-132">影片</span><span class="sxs-lookup"><span data-stu-id="4cecb-132">Videos</span></span>
* [<span data-ttu-id="4cecb-133">Azure App Service 架構</span><span class="sxs-lookup"><span data-stu-id="4cecb-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="4cecb-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4cecb-134">Next steps</span></span>

<span data-ttu-id="4cecb-135">進一步了解應用程式服務，其中一種 hello 下列主題：</span><span class="sxs-lookup"><span data-stu-id="4cecb-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="4cecb-136">什麼是 Azure 應用程式服務？</span><span class="sxs-lookup"><span data-stu-id="4cecb-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="4cecb-137">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4cecb-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="4cecb-138">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="4cecb-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="4cecb-139">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="4cecb-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="4cecb-140">Azure App Service 架構 (展示)</span><span class="sxs-lookup"><span data-stu-id="4cecb-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="4cecb-141">Azure App Service、雲端服務與虛擬機器之比較</span><span class="sxs-lookup"><span data-stu-id="4cecb-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="4cecb-142">了解 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="4cecb-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="4cecb-143">簡介 tooApp Service 環境</span><span class="sxs-lookup"><span data-stu-id="4cecb-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="4cecb-144">演練：建立 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="4cecb-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="4cecb-145">Azure App Service 開發堆疊支援</span><span class="sxs-lookup"><span data-stu-id="4cecb-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



