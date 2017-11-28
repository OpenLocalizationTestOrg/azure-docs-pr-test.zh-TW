---
title: "aaaUsing APP-V 應用程式與 Azure RemoteApp |Microsoft 文件"
description: "深入了解如何在 Azure RemoteApp toouse APP-V 應用程式。"
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
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="97e63-103">在 Azure RemoteApp 使用 App-V 應用程式</span><span class="sxs-lookup"><span data-stu-id="97e63-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97e63-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="97e63-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="97e63-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="97e63-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="97e63-106">您可以需要加入網域的 Azure RemoteApp 混合式集合中，使用 App-V 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97e63-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="97e63-107">開始之前，請確定 tooinstall hello APP-V 5.1 的用戶端 hello 最新的更新。</span><span class="sxs-lookup"><span data-stu-id="97e63-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="97e63-108">您將需要 toocreate[自訂映像](remoteapp-create-custom-image.md)包含 hello APP-V 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97e63-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="97e63-109">它是簡單 toouse Azure RemoteApp 在您現有的 APP-V 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="97e63-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="97e63-110">由於混合式集合部署到 Azure VNET 具有存取 tooyour 網域控制站，而且 hello Vm 是已加入網域，您可以利用您現有的 app-v 基礎架構和部署方法 tooeasyily APP-V 應用程式中主應用程式 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="97e63-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="97e63-111">以下是您應該留意根據您目前沒有的 APP-V 應用程式部署的 hello 類型的一些考量：</span><span class="sxs-lookup"><span data-stu-id="97e63-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="97e63-112">組態選項</span><span class="sxs-lookup"><span data-stu-id="97e63-112">Configuration options</span></span> |  | <span data-ttu-id="97e63-113">Positive</span><span class="sxs-lookup"><span data-stu-id="97e63-113">Positive</span></span> | <span data-ttu-id="97e63-114">Neutral</span><span class="sxs-lookup"><span data-stu-id="97e63-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97e63-115">傳遞方法</span><span class="sxs-lookup"><span data-stu-id="97e63-115">Delivery method</span></span> |<span data-ttu-id="97e63-116">串流 (隨選)</span><span class="sxs-lookup"><span data-stu-id="97e63-116">Streaming (on-demand)</span></span> |<span data-ttu-id="97e63-117">應用程式一律為最新和最新狀態的 hello</span><span class="sxs-lookup"><span data-stu-id="97e63-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="97e63-118">第一次的延遲</span><span class="sxs-lookup"><span data-stu-id="97e63-118">First time latency</span></span> |
| <span data-ttu-id="97e63-119">裝載</span><span class="sxs-lookup"><span data-stu-id="97e63-119">Mounted</span></span> |<span data-ttu-id="97e63-120">最快。應用程式已存在於 hello VM 上</span><span class="sxs-lookup"><span data-stu-id="97e63-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="97e63-121">膨脹 - 佔據映像空間 (127 GB 限制)</span><span class="sxs-lookup"><span data-stu-id="97e63-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="97e63-122">應用程式位置儲存體</span><span class="sxs-lookup"><span data-stu-id="97e63-122">App location storage</span></span> |<span data-ttu-id="97e63-123">共用的內容</span><span class="sxs-lookup"><span data-stu-id="97e63-123">Shared content</span></span> |<span data-ttu-id="97e63-124">在 Azure RemoteApp 執行個體的記憶體中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="97e63-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="97e63-125">會吞掉記憶體和良好連線 toostreaming （檔案） 伺服器 hello 應用程式所在的位置</span><span class="sxs-lookup"><span data-stu-id="97e63-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="97e63-126">磁碟 (快取)</span><span class="sxs-lookup"><span data-stu-id="97e63-126">Disk (Cached)</span></span> |<span data-ttu-id="97e63-127">快速執行。</span><span class="sxs-lookup"><span data-stu-id="97e63-127">Fast execution.</span></span> <span data-ttu-id="97e63-128">應用程式不相依於內容來源的可用性</span><span class="sxs-lookup"><span data-stu-id="97e63-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="97e63-129">膨脹 - 佔據映像空間 (127 GB 限制)</span><span class="sxs-lookup"><span data-stu-id="97e63-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="97e63-130">目標</span><span class="sxs-lookup"><span data-stu-id="97e63-130">Targeting</span></span> |<span data-ttu-id="97e63-131">User</span><span class="sxs-lookup"><span data-stu-id="97e63-131">User</span></span> |<span data-ttu-id="97e63-132">需要完整獨立的 App-V 基礎結構</span><span class="sxs-lookup"><span data-stu-id="97e63-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="97e63-133">全域 (電腦)</span><span class="sxs-lookup"><span data-stu-id="97e63-133">Global (machine)</span></span> |<span data-ttu-id="97e63-134">預先發佈或使用發佈伺服器做為目標</span><span class="sxs-lookup"><span data-stu-id="97e63-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="97e63-135">如果您想 tooupdate hello 應用程式 （大型），需要 tooupdate Azure 映像。</span><span class="sxs-lookup"><span data-stu-id="97e63-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="97e63-136">會佔用映像的一些空間。</span><span class="sxs-lookup"><span data-stu-id="97e63-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="97e63-137">您建立自訂映像和混合式集合之後，發佈您的應用程式，請將使用者指派並享受裝載於 Azure RemoteApp 傳遞 tooany 裝置、 任何現有的 APP-V 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97e63-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

