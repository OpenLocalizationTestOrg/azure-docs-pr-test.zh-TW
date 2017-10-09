---
title: "aaaUsing New Relic 與 Azure |Microsoft 文件"
description: "了解如何 toouse hello New Relic 服務 toomanage 和監視 Azure 應用程式。"
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
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="f4b70-103">Azure 上的 New Relic 應用程式效能管理</span><span class="sxs-lookup"><span data-stu-id="f4b70-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="f4b70-104">您可以將 New Relic 的世界級的效能監視 tooyour Azure 託管應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4b70-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="f4b70-105">除了獲得對 Azure 應用程式進行監視、疑難排解及微調的全面功能外，您還有資格使用 Azure 來享有 New Relic 產品的折扣價格。</span><span class="sxs-lookup"><span data-stu-id="f4b70-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="f4b70-106">什麼是 New Relic？</span><span class="sxs-lookup"><span data-stu-id="f4b70-106">What is New Relic?</span></span>
<span data-ttu-id="f4b70-107">與[New Relic 產品](https://newrelic.com/products)，您可以解決應用程式錯誤、 保持潛在的問題，並了解整個環境的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="f4b70-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="f4b70-108">它是設計的 toosave 時用來識別及診斷效能問題的時間，而且會將您在您可以需要 toosolve 這些問題的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f4b70-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="f4b70-109">新的 Relic 曲目 hello 載入時間以及您 web 的交易，同時從 hello 伺服器和使用者的瀏覽器的輸送量。</span><span class="sxs-lookup"><span data-stu-id="f4b70-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="f4b70-110">它會顯示在 hello 資料庫中，您花多少時間分析過慢的查詢，並執行時間監視與警示、 追蹤應用程式例外狀況，以及一大堆多個 web 要求時，提供。</span><span class="sxs-lookup"><span data-stu-id="f4b70-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="f4b70-111">優惠價格</span><span class="sxs-lookup"><span data-stu-id="f4b70-111">Special pricing</span></span>
<span data-ttu-id="f4b70-112">新標準 Relic 是免費 tooAzure 使用者。</span><span class="sxs-lookup"><span data-stu-id="f4b70-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="f4b70-113">New Relic Pro 是依據 Azure 雲端服務的執行個體大小提供。</span><span class="sxs-lookup"><span data-stu-id="f4b70-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="f4b70-114">如需定價資訊，請參閱 hello [New Relic 頁面](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/)在 hello Azure Marketplace 或連絡 New Relic (sales@newrelic.com) 如需定價的企業層級。</span><span class="sxs-lookup"><span data-stu-id="f4b70-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="f4b70-115">在部署 hello New Relic 代理程式時，azure 客戶會接收兩週新 Relic Pro 的試用版訂閱。</span><span class="sxs-lookup"><span data-stu-id="f4b70-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="f4b70-116">登入 New Relic 使用 hello Azure 存放區</span><span class="sxs-lookup"><span data-stu-id="f4b70-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="f4b70-117">New Relic 與 Azure Web 角色和背景工作角色緊密整合。</span><span class="sxs-lookup"><span data-stu-id="f4b70-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="f4b70-118">您可以快速且輕鬆地登入 New relic 直接從 hello Azure 存放區。</span><span class="sxs-lookup"><span data-stu-id="f4b70-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="f4b70-119">如需指示，請參閱 hello [Azure 儲存註冊指示](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup)從 New Relic。</span><span class="sxs-lookup"><span data-stu-id="f4b70-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="f4b70-120">檢視資料</span><span class="sxs-lookup"><span data-stu-id="f4b70-120">View your data</span></span>
<span data-ttu-id="f4b70-121">註冊好後，您可以利用 New Relic 令人讚嘆的應用程式監視和資料驅動分析。</span><span class="sxs-lookup"><span data-stu-id="f4b70-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="f4b70-122">toocheck New Relic 的應用程式的效能：</span><span class="sxs-lookup"><span data-stu-id="f4b70-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="f4b70-123">從 hello Azure 入口網站，選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="f4b70-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="f4b70-124">以您的 New Relic 帳戶電子郵件和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="f4b70-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="f4b70-125">選取您的應用程式從 hello 應用程式索引 tooview 所有您的應用程式中的資料 hello [APM 概觀頁面](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page)。</span><span class="sxs-lookup"><span data-stu-id="f4b70-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="f4b70-126">將 New Relic 與 Azure 搭配使用</span><span class="sxs-lookup"><span data-stu-id="f4b70-126">Using New Relic with Azure</span></span>
<span data-ttu-id="f4b70-127">如需使用 New Relic 與 Azure 的詳細資訊，請參閱 [New Relic 的文件網站](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)，包括︰</span><span class="sxs-lookup"><span data-stu-id="f4b70-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="f4b70-128">適用於 .NET 的 New Relic</span><span class="sxs-lookup"><span data-stu-id="f4b70-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="f4b70-129">在 Azure 雲端服務上檢測 .NET 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="f4b70-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="f4b70-130">新 Relic hello Microsoft Azure 雲端平台</span><span class="sxs-lookup"><span data-stu-id="f4b70-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="f4b70-131">新 Relic hello Microsoft Azure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="f4b70-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="f4b70-132">New Relic/Azure 疑難排解</span><span class="sxs-lookup"><span data-stu-id="f4b70-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

