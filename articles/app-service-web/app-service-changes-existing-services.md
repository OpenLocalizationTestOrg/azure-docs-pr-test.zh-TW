---
title: "Azure App Service 和它對現有 Azure 服務的影響"
description: "說明新的 Azure App Service 和其功能如何影響 Azure 中的現有服務。"
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="02035-103">Azure App Service 和現有的 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="02035-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="02035-104">本文概述現有 Azure 服務的變更做為將數個 Azure 服務一起帶入 [Azure App Service](https://azure.microsoft.com/services/app-service/)(新的整合服務) 的變更一部分。</span><span class="sxs-lookup"><span data-stu-id="02035-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="02035-105">概觀</span><span class="sxs-lookup"><span data-stu-id="02035-105">Overview</span></span>
<span data-ttu-id="02035-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) 是一種新的且唯一的雲端服務，可讓開發人員建立適用於任何平台和任何裝置的 Web 和行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="02035-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="02035-107">App Service 是一種整合解決方案，設計目的是簡化重複的程式碼撰寫函式、整合企業和 SaaS 系統，並自動化商務程序，同時滿足您的安全性、可靠性和延展性需求。</span><span class="sxs-lookup"><span data-stu-id="02035-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="02035-108">App Service 將下列現有 Azure 服務 - [網站](https://azure.microsoft.com/services/websites/)、[行動服務](https://azure.microsoft.com/services/mobile-services/)和 [Biztalk 服務](https://azure.microsoft.com/services/biztalk-services/)整合為單一結合服務，還增加強大的新功能。</span><span class="sxs-lookup"><span data-stu-id="02035-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="02035-109">App Service 可讓您裝載下列應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="02035-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="02035-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="02035-110">Web Apps</span></span>
* <span data-ttu-id="02035-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="02035-111">Mobile Apps</span></span>
* <span data-ttu-id="02035-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="02035-112">API Apps</span></span>
* <span data-ttu-id="02035-113">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="02035-113">Logic Apps</span></span>

<span data-ttu-id="02035-114">下表說明現有 Azure 服務如何對應至應用程式服務和其內可用的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="02035-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="02035-115">現有 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="02035-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="02035-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="02035-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="02035-117">變更內容</span><span class="sxs-lookup"><span data-stu-id="02035-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="02035-118">Azure 網站</span><span class="sxs-lookup"><span data-stu-id="02035-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="02035-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="02035-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="02035-120">針對 Azure 網站，已嚴格限制 App Service 將名稱「網站」變更為 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="02035-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="02035-121">所有您的現有網站執行個體現在都是 App Service 中的 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="02035-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="02035-122">您可以透過 <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure 入口網站</a>存取現有網站，在此入口網站中，您將在 [Web Apps]<em></em> 下找到您的所有現有網站。</span><span class="sxs-lookup"><span data-stu-id="02035-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="02035-123"><em>Web 主控方案</em>現在<em>App Service 方案</em>。</span><span class="sxs-lookup"><span data-stu-id="02035-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="02035-124"><em>App Service 方案</em>可以裝載 App Service 類型的任何應用程式，例如 Web、行動、邏輯或 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="02035-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="02035-125">Azure App Service Web Apps 已正式推出。</span><span class="sxs-lookup"><span data-stu-id="02035-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="02035-126"><a href="http://azure.microsoft.com/services/app-service/web/">深入了解 Web 應用程式</a>。</span><span class="sxs-lookup"><span data-stu-id="02035-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="02035-127">Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="02035-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="02035-128">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="02035-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="02035-129">行動服務繼續可當作獨立服務，並仍提供完整支援。</span><span class="sxs-lookup"><span data-stu-id="02035-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="02035-130">Mobile Apps 是 App Service 中的應用程式類型，整合了行動服務和其他項目的所有功能。</span><span class="sxs-lookup"><span data-stu-id="02035-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="02035-131">可以輕鬆地<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">從行動服務移轉到 Mobile Apps</a>。</span><span class="sxs-lookup"><span data-stu-id="02035-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="02035-132">由於隸屬於 App Service，Mobile Apps 可以取得行動服務以外的新功能，例如與內部部署和 SaaS 系統整合、預備位置、更好的縮放選項，以及其他。</span><span class="sxs-lookup"><span data-stu-id="02035-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="02035-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">深入了解行動應用程式</a>。</span><span class="sxs-lookup"><span data-stu-id="02035-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="02035-134">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="02035-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="02035-135">API 應用程式是 App Service 中的新應用程式類型，可讓您在雲端中輕鬆地建置和使用 API。</span><span class="sxs-lookup"><span data-stu-id="02035-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="02035-136"><a href="http://azure.microsoft.com/services/app-service/api/">深入了解 API Apps</a>。</span><span class="sxs-lookup"><span data-stu-id="02035-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="02035-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="02035-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="02035-138">Logic Apps 是 App Service 中的新應用程式類型，可讓您輕鬆地自動化商務程序。</span><span class="sxs-lookup"><span data-stu-id="02035-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="02035-139"><a href="http://azure.microsoft.com/services/app-service/logic/">深入了解 Logic Apps</a>。</span><span class="sxs-lookup"><span data-stu-id="02035-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="02035-140">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="02035-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="02035-141">BizTalk API 應用程式</span><span class="sxs-lookup"><span data-stu-id="02035-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="02035-142">BizTalk 服務繼續可當作獨立服務，並仍提供完整支援。</span><span class="sxs-lookup"><span data-stu-id="02035-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="02035-143">BizTalk 服務的所有功能都整合到 App Service 中成為 API Apps，可讓使用者執行企業應用程式整合和 B2B 整合案例，與 App Service 中任何應用程式類型整合在一起。</span><span class="sxs-lookup"><span data-stu-id="02035-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="02035-144">現在，透過 Logic Apps，您可以使用視覺化設計體驗，將商務程序自動化來建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="02035-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="02035-145">若要深入了解，請瀏覽 [App Service 文件](https://azure.microsoft.com/documentation/services/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="02035-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

