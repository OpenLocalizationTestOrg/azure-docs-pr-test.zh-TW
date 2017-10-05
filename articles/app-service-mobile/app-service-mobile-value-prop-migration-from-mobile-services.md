---
title: "我使用行動服務，App Service 有何幫助？"
description: "了解 App Service 為您現有的行動服務專案帶來哪些優勢。"
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 22397b6b448b418d5b54a457c3bafaf5c68ecc7b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="80e78-103"><a name="getting-started"> </a>我使用行動服務，App Service 有何幫助？</span><span class="sxs-lookup"><span data-stu-id="80e78-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="80e78-104">概觀</span><span class="sxs-lookup"><span data-stu-id="80e78-104">Overview</span></span>
<span data-ttu-id="80e78-105">您現有的行動服務很安全並將繼續提供支援。</span><span class="sxs-lookup"><span data-stu-id="80e78-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="80e78-106">不過， *Azure App Service* 平台為您的行動應用程式提供了行動服務目前所沒有的數個優點：</span><span class="sxs-lookup"><span data-stu-id="80e78-106">However there are number of advantages the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="80e78-107">針對包含 Web 和行動用戶端的應用程式，提供更簡單、更容易且更符合成本效益的功能</span><span class="sxs-lookup"><span data-stu-id="80e78-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="80e78-108">新的主機功能包括 Web 工作、自訂 CName、更完善的監視</span><span class="sxs-lookup"><span data-stu-id="80e78-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="80e78-109">與流量管理員的周全整合</span><span class="sxs-lookup"><span data-stu-id="80e78-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="80e78-110">除了混合式連線以外，還會使用 VNet 連線至內部部署資源和 VPN</span><span class="sxs-lookup"><span data-stu-id="80e78-110">Connectivity to your on-premises resources and VPNs using VNet in addition to Hybrid Connections</span></span>
* <span data-ttu-id="80e78-111">使用 NewRelic 或 AppInsights 針對您的應用程式進行監視、警示和疑難排解</span><span class="sxs-lookup"><span data-stu-id="80e78-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="80e78-112">更廣泛的基礎計算資源與定價</span><span class="sxs-lookup"><span data-stu-id="80e78-112">Richer spectrum of the underlying compute resources and pricing</span></span>
* <span data-ttu-id="80e78-113">內建自動調整、負載平衡，以及效能監視。</span><span class="sxs-lookup"><span data-stu-id="80e78-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="80e78-114">內建預備、備份、回復和實際環境測試功能</span><span class="sxs-lookup"><span data-stu-id="80e78-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="80e78-115">新的裝載功能</span><span class="sxs-lookup"><span data-stu-id="80e78-115">New hosting features</span></span>
<span data-ttu-id="80e78-116">在 AzureApp Service 中，「行動應用程式」後端程式碼會在與 Web 應用程式和 API 應用程式相同的容器中執行。</span><span class="sxs-lookup"><span data-stu-id="80e78-116">In *Azure App Service* the *Mobile App* backend code runs in the same container as Web App and API App.</span></span> <span data-ttu-id="80e78-117">因此，您可以利用此容器中的所有功能，包括行動服務中目前不存在的功能：</span><span class="sxs-lookup"><span data-stu-id="80e78-117">As such you can take advantage of all the features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="80e78-118">透過 Web 工作加入連續執行的後端邏輯</span><span class="sxs-lookup"><span data-stu-id="80e78-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="80e78-119">確保您的後端程式碼持續不斷執行</span><span class="sxs-lookup"><span data-stu-id="80e78-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="80e78-120">使用自訂 CName，為您的行動裝置後端端點提供易記且穩定的名稱</span><span class="sxs-lookup"><span data-stu-id="80e78-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span></span>
* <span data-ttu-id="80e78-121">使用流量管理員，異地擴充您的 app</span><span class="sxs-lookup"><span data-stu-id="80e78-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="80e78-122">包含任何您想要的程式庫和封裝。</span><span class="sxs-lookup"><span data-stu-id="80e78-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="80e78-123">(適用於 .NET) 運用 ASP.NET 的任何功能，包括 MVC</span><span class="sxs-lookup"><span data-stu-id="80e78-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="80e78-124">(適用於 Node.js) 運用 Node 生態系統的任何純 JavaScript 程式庫，包含一般 MVC 程式庫。</span><span class="sxs-lookup"><span data-stu-id="80e78-124">(For Node.js) Leverage any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="80e78-125">使用 VNet 存取內部部署資料</span><span class="sxs-lookup"><span data-stu-id="80e78-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="80e78-126">現今有了行動服務，您已可使用混合式連線來存取內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="80e78-126">With Mobile Services today you can already use Hybrid Connections to access on-premises resources.</span></span> <span data-ttu-id="80e78-127">不過，有些情況還是慣用 VPN 解決方案。</span><span class="sxs-lookup"><span data-stu-id="80e78-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="80e78-128">透過 *Azure App Service* ，您可以將 Azure VNet 用於您的行動應用程式後端程式碼。</span><span class="sxs-lookup"><span data-stu-id="80e78-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="80e78-129">使用您最愛的後端語言</span><span class="sxs-lookup"><span data-stu-id="80e78-129">Use your favorite backend language</span></span>
<span data-ttu-id="80e78-130">*Azure App Service* 提供對 ASP.NET 與 Node.js 平台更廣泛、更豐富的支援，包含對最新執行階段的存取。</span><span class="sxs-lookup"><span data-stu-id="80e78-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="80e78-131">設定自動調整</span><span class="sxs-lookup"><span data-stu-id="80e78-131">Set up automatic scale</span></span>
<span data-ttu-id="80e78-132">有了行動服務，後端程式碼的所有執行個體都已在小型 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="80e78-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="80e78-133">*Azure App Service* 可讓您從更豐富的選項中選取 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="80e78-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="80e78-134">您可以根據各種效能計量，快速相應增加或相應放大，以處理任何傳入的客戶負載。</span><span class="sxs-lookup"><span data-stu-id="80e78-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-the-know"></a><span data-ttu-id="80e78-135">處於「知情」狀態</span><span class="sxs-lookup"><span data-stu-id="80e78-135">Be in the “know”</span></span>
<span data-ttu-id="80e78-136">利用監視及警示即時對問題做出反應，以自動通知您和您的團隊。</span><span class="sxs-lookup"><span data-stu-id="80e78-136">React to issues in real-time with monitoring and alerts to automatically notify you and your team.</span></span> <span data-ttu-id="80e78-137">整合 New Relic 和 AppInsights 的進階應用程式分析和監視功能，更深入了解如何執行您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="80e78-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights to get even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="80e78-138">使用 *Azure App Service* ，您現在可以根據多種效能度量 (以程式設計方式或透過 Azure 入口網站) 設定警示。</span><span class="sxs-lookup"><span data-stu-id="80e78-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via the Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="80e78-139">讓您的資產安全無虞</span><span class="sxs-lookup"><span data-stu-id="80e78-139">Keep your assets safe</span></span>
<span data-ttu-id="80e78-140">自動備份您的後端和資料庫。</span><span class="sxs-lookup"><span data-stu-id="80e78-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="80e78-141">您的程式碼和資料可免於遭受災害並可輕鬆還原，讓您有信心地執行您的業務。</span><span class="sxs-lookup"><span data-stu-id="80e78-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="80e78-142">準備上場 ！</span><span class="sxs-lookup"><span data-stu-id="80e78-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="80e78-143">利用 *Azure App Service* ，您現在可以為行動應用程式建立多個私人測試和預備環境。</span><span class="sxs-lookup"><span data-stu-id="80e78-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="80e78-144">您可以在部署之前，使用這些環境來執行測試。</span><span class="sxs-lookup"><span data-stu-id="80e78-144">Use them to perform testing before you deploy.</span></span> <span data-ttu-id="80e78-145">不需停機即可切換至生產環境。</span><span class="sxs-lookup"><span data-stu-id="80e78-145">Swap to production with no downtime.</span></span> <span data-ttu-id="80e78-146">Web 應用程式已預先載入，可確保最佳的客戶體驗。</span><span class="sxs-lookup"><span data-stu-id="80e78-146">Web apps are pre-loaded, ensuring the best customer experience.</span></span>

<span data-ttu-id="80e78-147">您可以藉由遵循此 *教學課程* ，開始將 [App Service](app-service-mobile-migrating-from-mobile-services.md)運用於您現有的行動服務。</span><span class="sxs-lookup"><span data-stu-id="80e78-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>
