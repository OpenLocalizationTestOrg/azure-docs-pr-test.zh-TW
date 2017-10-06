---
title: "aaaAzure 應用程式服務，它對現有的 Azure 服務的影響"
description: "說明如何 hello 新的 Azure 應用程式服務和其功能會影響在 Azure 中現有的服務。"
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="2c8d5-103">Azure App Service 和現有的 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="2c8d5-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="2c8d5-104">本文概述 Azure 服務的 hello 變更 toobring 一起一部分到數個 Azure 服務的 hello 變更 tooexisting [Azure App Service](https://azure.microsoft.com/services/app-service/)，新的整合式供應項目。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="2c8d5-105">概觀</span><span class="sxs-lookup"><span data-stu-id="2c8d5-105">Overview</span></span>
<span data-ttu-id="2c8d5-106">[Azure App Service](https://azure.microsoft.com/services/app-service/)是新的且唯一的雲端服務，可讓開發人員 toocreate web 和行動應用程式的任何平台和任何裝置。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="2c8d5-107">應用程式服務是設計的整合式的解決方案 toostreamline 重複程式碼撰寫函式、 整合企業和 SaaS 系統並自動化商務程序，同時滿足您需求的安全性、 可靠性和延展性。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="2c8d5-108">結合 hello 遵循現有的 Azure 應用程式服務。 服務-[網站](https://azure.microsoft.com/services/websites/)，[行動服務](https://azure.microsoft.com/services/mobile-services/)，和[Biztalk 服務](https://azure.microsoft.com/services/biztalk-services/)到單一組合服務時加入功能強大的新功能。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="2c8d5-109">應用程式服務可讓您 toohost hello 下列應用程式類型：</span><span class="sxs-lookup"><span data-stu-id="2c8d5-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="2c8d5-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-110">Web Apps</span></span>
* <span data-ttu-id="2c8d5-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-111">Mobile Apps</span></span>
* <span data-ttu-id="2c8d5-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-112">API Apps</span></span>
* <span data-ttu-id="2c8d5-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-113">Logic Apps</span></span>

<span data-ttu-id="2c8d5-114">hello 下表說明如何在現有的 Azure 服務對應 tooApp Service 和 hello 應用程式類型中可用。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="2c8d5-115">現有 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="2c8d5-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="2c8d5-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2c8d5-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="2c8d5-117">變更內容</span><span class="sxs-lookup"><span data-stu-id="2c8d5-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="2c8d5-118">Azure 網站</span><span class="sxs-lookup"><span data-stu-id="2c8d5-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="2c8d5-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="2c8d5-120">Azure 網站的應用程式服務是嚴格限制的 toochanging hello 名稱網站 tooWeb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="2c8d5-121">所有您的現有網站執行個體現在都是 App Service 中的 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="2c8d5-122">您可以存取您現有的網站，透過 hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure 入口網站</a>，其中您會發現下的所有現有站台<em>Web 應用程式</em>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="2c8d5-123"><em>Web 主控方案</em>現在<em>App Service 方案</em>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="2c8d5-124"><em>App Service 方案</em>可以裝載 App Service 類型的任何應用程式，例如 Web、行動、邏輯或 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="2c8d5-125">Azure App Service Web Apps 已正式推出。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="2c8d5-126"><a href="http://azure.microsoft.com/services/app-service/web/">深入了解 Web 應用程式</a>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="2c8d5-127">Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="2c8d5-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="2c8d5-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="2c8d5-129">行動服務繼續 toobe 可用為獨立服務，並保留完整支援。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="2c8d5-130">行動應用程式是在應用程式服務中，以便將所有的行動服務等等的 hello 功能整合的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="2c8d5-131">它也很簡單<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">從行動服務 tooMobile 應用程式移轉</a>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="2c8d5-132">由於隸屬於 App Service，Mobile Apps 可以取得行動服務以外的新功能，例如與內部部署和 SaaS 系統整合、預備位置、更好的縮放選項，以及其他。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="2c8d5-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">深入了解行動應用程式</a>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="2c8d5-134">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c8d5-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2c8d5-135">應用程式開發介面應用程式是在應用程式服務，可讓您輕鬆地建立和使用 hello 雲端中的應用程式開發介面中的新應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="2c8d5-136"><a href="http://azure.microsoft.com/services/app-service/api/">深入了解 API Apps</a>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="2c8d5-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2c8d5-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2c8d5-138">Logic Apps 是 App Service 中的新應用程式類型，可讓您輕鬆地自動化商務程序。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="2c8d5-139"><a href="http://azure.microsoft.com/services/app-service/logic/">深入了解 Logic Apps</a>。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="2c8d5-140">Azure BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="2c8d5-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="2c8d5-141">BizTalk API 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c8d5-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="2c8d5-142">BizTalk 服務繼續 toobe 可用為獨立服務，並保留完整支援。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="2c8d5-143">API 應用程式啟用使用者 tooperform 企業應用程式整合以及 B2B 整合案例的任何 App Service 中的 hello 應用程式類型，所有的 BizTalk 服務的 hello 功能已整合到應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="2c8d5-144">您現在可以使用邏輯應用程式，自動化商務程序使用視覺化設計體驗 toocreate 工作流程。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="2c8d5-145">toolearn 詳細資訊，請瀏覽[應用程式服務文件](https://azure.microsoft.com/documentation/services/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="2c8d5-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

