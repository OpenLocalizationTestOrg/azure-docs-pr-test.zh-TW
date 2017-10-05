---
title: "搭配 Azure RemoteApp 使用 App-V 應用程式 | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中使用 App-V 應用程式"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="e2558-103">在 Azure RemoteApp 使用 App-V 應用程式</span><span class="sxs-lookup"><span data-stu-id="e2558-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e2558-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e2558-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e2558-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="e2558-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e2558-106">您可以需要加入網域的 Azure RemoteApp 混合式集合中，使用 App-V 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2558-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="e2558-107">開始之前，請務必使用最新的更新安裝 App-V 5.1 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e2558-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="e2558-108">您必須建立包含 App-V 用戶端的 [自訂映像](remoteapp-create-custom-image.md) 。</span><span class="sxs-lookup"><span data-stu-id="e2558-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="e2558-109">搭配 Azure RemoteApp 使用現有的 App-V 基礎結構很容易。</span><span class="sxs-lookup"><span data-stu-id="e2558-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="e2558-110">由於混合式集合是部署到 Azure VNET，它可以存取您的網域控制站，而且 VM 已加入網域，所以您可以利用您現有的 App-V 基礎架構和部署方法，輕易地在 Azure RemoteApp 內裝載 App-V 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2558-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="e2558-111">以下是您應該根據您目前擁有的 App-V 部署類型，注意的一些考量：</span><span class="sxs-lookup"><span data-stu-id="e2558-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="e2558-112">組態選項</span><span class="sxs-lookup"><span data-stu-id="e2558-112">Configuration options</span></span> |  | <span data-ttu-id="e2558-113">Positive</span><span class="sxs-lookup"><span data-stu-id="e2558-113">Positive</span></span> | <span data-ttu-id="e2558-114">Neutral</span><span class="sxs-lookup"><span data-stu-id="e2558-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2558-115">傳遞方法</span><span class="sxs-lookup"><span data-stu-id="e2558-115">Delivery method</span></span> |<span data-ttu-id="e2558-116">串流 (隨選)</span><span class="sxs-lookup"><span data-stu-id="e2558-116">Streaming (on-demand)</span></span> |<span data-ttu-id="e2558-117">應用程式永遠是最新和全新</span><span class="sxs-lookup"><span data-stu-id="e2558-117">App is always the latest and fresh</span></span> |<span data-ttu-id="e2558-118">第一次的延遲</span><span class="sxs-lookup"><span data-stu-id="e2558-118">First time latency</span></span> |
| <span data-ttu-id="e2558-119">裝載</span><span class="sxs-lookup"><span data-stu-id="e2558-119">Mounted</span></span> |<span data-ttu-id="e2558-120">最快；應用程式已存在於 VM 上</span><span class="sxs-lookup"><span data-stu-id="e2558-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="e2558-121">膨脹 - 佔據映像空間 (127 GB 限制)</span><span class="sxs-lookup"><span data-stu-id="e2558-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="e2558-122">應用程式位置儲存體</span><span class="sxs-lookup"><span data-stu-id="e2558-122">App location storage</span></span> |<span data-ttu-id="e2558-123">共用的內容</span><span class="sxs-lookup"><span data-stu-id="e2558-123">Shared content</span></span> |<span data-ttu-id="e2558-124">在 Azure RemoteApp 執行個體的記憶體中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="e2558-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="e2558-125">會耗用記憶體和與應用程式所在的串流 (檔案) 伺服器的良好連線</span><span class="sxs-lookup"><span data-stu-id="e2558-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="e2558-126">磁碟 (快取)</span><span class="sxs-lookup"><span data-stu-id="e2558-126">Disk (Cached)</span></span> |<span data-ttu-id="e2558-127">快速執行。</span><span class="sxs-lookup"><span data-stu-id="e2558-127">Fast execution.</span></span> <span data-ttu-id="e2558-128">應用程式不相依於內容來源的可用性</span><span class="sxs-lookup"><span data-stu-id="e2558-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="e2558-129">膨脹 - 佔據映像空間 (127 GB 限制)</span><span class="sxs-lookup"><span data-stu-id="e2558-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="e2558-130">目標</span><span class="sxs-lookup"><span data-stu-id="e2558-130">Targeting</span></span> |<span data-ttu-id="e2558-131">User</span><span class="sxs-lookup"><span data-stu-id="e2558-131">User</span></span> |<span data-ttu-id="e2558-132">需要完整獨立的 App-V 基礎結構</span><span class="sxs-lookup"><span data-stu-id="e2558-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="e2558-133">全域 (電腦)</span><span class="sxs-lookup"><span data-stu-id="e2558-133">Global (machine)</span></span> |<span data-ttu-id="e2558-134">預先發佈或使用發佈伺服器做為目標</span><span class="sxs-lookup"><span data-stu-id="e2558-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="e2558-135">如果您想要更新應用程式 (大) 則需要更新您的 Azure 映像。</span><span class="sxs-lookup"><span data-stu-id="e2558-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="e2558-136">會佔用映像的一些空間。</span><span class="sxs-lookup"><span data-stu-id="e2558-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="e2558-137">您建立自訂映像和混合式集合之後，發佈您的應用程式、指派使用者並享受裝載於傳遞至任何位置任何裝置的 Azure RemoteApp 中的現有 App-V 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2558-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

