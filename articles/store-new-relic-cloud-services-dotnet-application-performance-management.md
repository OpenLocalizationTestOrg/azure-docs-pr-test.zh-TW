---
title: "將 New Relic 與 Azure 搭配使用 | Microsoft Docs"
description: "了解如何使用 New Relic 服務來管理與監控 Azure 應用程式。"
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="695f9-103">Azure 上的 New Relic 應用程式效能管理</span><span class="sxs-lookup"><span data-stu-id="695f9-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="695f9-104">您可以將 New Relic 的世界級效能監視新增至 Azure 託管的應用程式。</span><span class="sxs-lookup"><span data-stu-id="695f9-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="695f9-105">除了獲得對 Azure 應用程式進行監視、疑難排解及微調的全面功能外，您還有資格使用 Azure 來享有 New Relic 產品的折扣價格。</span><span class="sxs-lookup"><span data-stu-id="695f9-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="695f9-106">什麼是 New Relic？</span><span class="sxs-lookup"><span data-stu-id="695f9-106">What is New Relic?</span></span>
<span data-ttu-id="695f9-107">使用 [New Relic 產品](https://newrelic.com/products)，您就可以解決應用程式錯誤、早一步處理潛在問題，以及了解整個環境的效能。</span><span class="sxs-lookup"><span data-stu-id="695f9-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="695f9-108">主要是讓您在識別和診斷效能問題時可節省時間，並隨手取得解決這些問題所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="695f9-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="695f9-109">New Relic 會追蹤來自伺服器和使用者瀏覽器的 Web 交易載入時間和輸送量。</span><span class="sxs-lookup"><span data-stu-id="695f9-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="695f9-110">它會顯示您在資料庫中花費多少時間、分析較慢的查詢和 Web 要求、提供運作時間監視和警示、追蹤應用程式例外狀況，還有許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="695f9-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="695f9-111">優惠價格</span><span class="sxs-lookup"><span data-stu-id="695f9-111">Special pricing</span></span>
<span data-ttu-id="695f9-112">New Relic Standard 供 Azure 使用者免費使用。</span><span class="sxs-lookup"><span data-stu-id="695f9-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="695f9-113">New Relic Pro 是依據 Azure 雲端服務的執行個體大小提供。</span><span class="sxs-lookup"><span data-stu-id="695f9-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="695f9-114">如需定價資訊，請參閱[New Relic 頁面](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/)連絡人 New Relic 的 Azure Marketplace 中 (sales@newrelic.com) 如需定價的企業層級。</span><span class="sxs-lookup"><span data-stu-id="695f9-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="695f9-115">Azure 客戶部署 New Relic 代理程式時享有 New Relic Pro 試用訂閱兩週。</span><span class="sxs-lookup"><span data-stu-id="695f9-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="695f9-116">使用 Azure 市集註冊 New Relic</span><span class="sxs-lookup"><span data-stu-id="695f9-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="695f9-117">New Relic 與 Azure Web 角色和背景工作角色緊密整合。</span><span class="sxs-lookup"><span data-stu-id="695f9-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="695f9-118">您可以直接從 Azure 市集輕鬆快速地註冊 New Relic。</span><span class="sxs-lookup"><span data-stu-id="695f9-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="695f9-119">如需指示，請參閱 New Relic 提供的 [Azure 市集註冊指示](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) 。</span><span class="sxs-lookup"><span data-stu-id="695f9-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="695f9-120">檢視資料</span><span class="sxs-lookup"><span data-stu-id="695f9-120">View your data</span></span>
<span data-ttu-id="695f9-121">註冊好後，您可以利用 New Relic 令人讚嘆的應用程式監視和資料驅動分析。</span><span class="sxs-lookup"><span data-stu-id="695f9-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="695f9-122">若要在 New Relic 中檢查您的應用程式效能：</span><span class="sxs-lookup"><span data-stu-id="695f9-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="695f9-123">從 Azure 入口網站選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="695f9-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="695f9-124">以您的 New Relic 帳戶電子郵件和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="695f9-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="695f9-125">從應用程式索引選取您的應用程式以在 [APM 概觀頁面](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page)中檢視您所有應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="695f9-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="695f9-126">將 New Relic 與 Azure 搭配使用</span><span class="sxs-lookup"><span data-stu-id="695f9-126">Using New Relic with Azure</span></span>
<span data-ttu-id="695f9-127">如需使用 New Relic 與 Azure 的詳細資訊，請參閱 [New Relic 的文件網站](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)，包括︰</span><span class="sxs-lookup"><span data-stu-id="695f9-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="695f9-128">適用於 .NET 的 New Relic</span><span class="sxs-lookup"><span data-stu-id="695f9-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="695f9-129">在 Azure 雲端服務上檢測 .NET 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="695f9-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="695f9-130">適用於 Microsoft Azure 雲端平台的 New Relic</span><span class="sxs-lookup"><span data-stu-id="695f9-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="695f9-131">適用於 Microsoft Azure App Service 的 New Relic</span><span class="sxs-lookup"><span data-stu-id="695f9-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="695f9-132">New Relic/Azure 疑難排解</span><span class="sxs-lookup"><span data-stu-id="695f9-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

