---
title: "aaaI 使用行動服務、 如何協助應用程式服務？"
description: "了解哪些優點沒有應用程式服務將 tooyour 現有行動服務專案。"
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
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="bc5cc-103"><a name="getting-started"> </a>我使用行動服務，App Service 有何幫助？</span><span class="sxs-lookup"><span data-stu-id="bc5cc-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="bc5cc-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bc5cc-104">Overview</span></span>
<span data-ttu-id="bc5cc-105">您現有的行動服務很安全並將繼續提供支援。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="bc5cc-106">不過有數字的優點 hello *Azure App Service*平台提供您不使用 Mobile Services 目前可用的行動裝置應用程式：</span><span class="sxs-lookup"><span data-stu-id="bc5cc-106">However there are number of advantages hello *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="bc5cc-107">針對包含 Web 和行動用戶端的應用程式，提供更簡單、更容易且更符合成本效益的功能</span><span class="sxs-lookup"><span data-stu-id="bc5cc-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="bc5cc-108">新的主機功能包括 Web 工作、自訂 CName、更完善的監視</span><span class="sxs-lookup"><span data-stu-id="bc5cc-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="bc5cc-109">與流量管理員的周全整合</span><span class="sxs-lookup"><span data-stu-id="bc5cc-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="bc5cc-110">連線 tooyour 在內部部署資源和使用 VNet 中新增 tooHybrid 連線的 Vpn</span><span class="sxs-lookup"><span data-stu-id="bc5cc-110">Connectivity tooyour on-premises resources and VPNs using VNet in addition tooHybrid Connections</span></span>
* <span data-ttu-id="bc5cc-111">使用 NewRelic 或 AppInsights 針對您的應用程式進行監視、警示和疑難排解</span><span class="sxs-lookup"><span data-stu-id="bc5cc-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="bc5cc-112">更豐富的廣泛的 hello 基礎運算資源和定價</span><span class="sxs-lookup"><span data-stu-id="bc5cc-112">Richer spectrum of hello underlying compute resources and pricing</span></span>
* <span data-ttu-id="bc5cc-113">內建自動調整、負載平衡，以及效能監視。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="bc5cc-114">內建預備、備份、回復和實際環境測試功能</span><span class="sxs-lookup"><span data-stu-id="bc5cc-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="bc5cc-115">新的裝載功能</span><span class="sxs-lookup"><span data-stu-id="bc5cc-115">New hosting features</span></span>
<span data-ttu-id="bc5cc-116">在*Azure App Service* hello*行動裝置應用程式*後端中的程式碼執行 hello 相同容器做為 Web 應用程式及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-116">In *Azure App Service* hello *Mobile App* backend code runs in hello same container as Web App and API App.</span></span> <span data-ttu-id="bc5cc-117">因此您也可以利用此容器，包括那些不是目前在行動服務中的某些中的所有 hello 功能：</span><span class="sxs-lookup"><span data-stu-id="bc5cc-117">As such you can take advantage of all hello features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="bc5cc-118">透過 Web 工作加入連續執行的後端邏輯</span><span class="sxs-lookup"><span data-stu-id="bc5cc-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="bc5cc-119">確保您的後端程式碼持續不斷執行</span><span class="sxs-lookup"><span data-stu-id="bc5cc-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="bc5cc-120">使用好記的自訂 Cname tooprovide 與穩定名稱 tooyour 行動後端端點</span><span class="sxs-lookup"><span data-stu-id="bc5cc-120">Use custom CNames tooprovide friendly and stable names tooyour mobile backend endpoints</span></span>
* <span data-ttu-id="bc5cc-121">使用流量管理員，異地擴充您的 app</span><span class="sxs-lookup"><span data-stu-id="bc5cc-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="bc5cc-122">包含任何您想要的程式庫和封裝。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="bc5cc-123">(適用於 .NET) 運用 ASP.NET 的任何功能，包括 MVC</span><span class="sxs-lookup"><span data-stu-id="bc5cc-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="bc5cc-124">（適用於 Node.js)利用 hello 節點生態系統，包括一般 MVC 文件庫的任何純 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-124">(For Node.js) Leverage any pure JavaScript library of hello Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="bc5cc-125">使用 VNet 存取內部部署資料</span><span class="sxs-lookup"><span data-stu-id="bc5cc-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="bc5cc-126">使用行動服務已經可以使用混合式連線 tooaccess 現今內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-126">With Mobile Services today you can already use Hybrid Connections tooaccess on-premises resources.</span></span> <span data-ttu-id="bc5cc-127">不過，有些情況還是慣用 VPN 解決方案。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="bc5cc-128">透過 *Azure App Service* ，您可以將 Azure VNet 用於您的行動應用程式後端程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="bc5cc-129">使用您最愛的後端語言</span><span class="sxs-lookup"><span data-stu-id="bc5cc-129">Use your favorite backend language</span></span>
<span data-ttu-id="bc5cc-130">*Azure App Service*更廣泛的優惠和更豐富的支援，ASP.NET 和 Node.js 平台，包括存取 toohello 最新的執行階段。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access toohello latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="bc5cc-131">設定自動調整</span><span class="sxs-lookup"><span data-stu-id="bc5cc-131">Set up automatic scale</span></span>
<span data-ttu-id="bc5cc-132">有了行動服務，後端程式碼的所有執行個體都已在小型 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="bc5cc-133">*Azure App Service*可讓您從一組更豐富的選項 Vm tooselect hello 大小。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-133">*Azure App Service* enables you tooselect hello size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="bc5cc-134">您可以快速相應增加或 toohandle 出任何連入的客戶負載，根據各種效能度量。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-134">You can also  quickly scale up or out toohandle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-hello-know"></a><span data-ttu-id="bc5cc-135">會在 hello 「 知道 」</span><span class="sxs-lookup"><span data-stu-id="bc5cc-135">Be in hello “know”</span></span>
<span data-ttu-id="bc5cc-136">回應 tooissues 中即時監視及警示 tooautomatically 通知您和小組。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-136">React tooissues in real-time with monitoring and alerts tooautomatically notify you and your team.</span></span> <span data-ttu-id="bc5cc-137">將進階的應用程式分析和 New Relic 和 AppInsights tooget 更豐富深入了解如何執行您的行動裝置應用程式的監視功能的整合。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights tooget even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="bc5cc-138">與*Azure App Service*您現在可以設定警示依照各種效能度量，以程式設計方式或透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via hello Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="bc5cc-139">讓您的資產安全無虞</span><span class="sxs-lookup"><span data-stu-id="bc5cc-139">Keep your assets safe</span></span>
<span data-ttu-id="bc5cc-140">自動備份您的後端和資料庫。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="bc5cc-141">您的程式碼和資料已安全地防範災害和輕鬆還原的可讓您 toorun 有信心地業務。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-141">Your code and data is secure from disaster and easily restored, allowing you toorun your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="bc5cc-142">準備上場 ！</span><span class="sxs-lookup"><span data-stu-id="bc5cc-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="bc5cc-143">利用 *Azure App Service* ，您現在可以為行動應用程式建立多個私人測試和預備環境。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="bc5cc-144">在部署之前測試 tooperform 使用它們。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-144">Use them tooperform testing before you deploy.</span></span> <span data-ttu-id="bc5cc-145">交換 tooproduction 不需停機。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-145">Swap tooproduction with no downtime.</span></span> <span data-ttu-id="bc5cc-146">預先載入了 web 應用程式，確保 hello 最佳的客戶經驗。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-146">Web apps are pre-loaded, ensuring hello best customer experience.</span></span>

<span data-ttu-id="bc5cc-147">您可以藉由遵循此 *教學課程* ，開始將 [App Service](app-service-mobile-migrating-from-mobile-services.md)運用於您現有的行動服務。</span><span class="sxs-lookup"><span data-stu-id="bc5cc-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>
