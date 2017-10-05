---
title: "發生影響 Azure 金鑰保存庫的 Azure 服務中斷事件時該怎麼辦 | Microsoft Docs"
description: "了解發生影響「Azure 金鑰保存庫」的 Azure 服務中斷事件時該怎麼辦。"
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="4eda4-103">Azure 金鑰保存庫的可用性與備援</span><span class="sxs-lookup"><span data-stu-id="4eda4-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="4eda4-104">Azure 金鑰保存庫具備多層備援功能，以確保您的金鑰和密碼會保持可供應用程式使用，甚至在服務的個別元件失敗時也是如此。</span><span class="sxs-lookup"><span data-stu-id="4eda4-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="4eda4-105">金鑰保存庫的內容會在區域內複寫，以及複寫到至少距離 150 英哩但位於相同地理位置內的次要區域。</span><span class="sxs-lookup"><span data-stu-id="4eda4-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="4eda4-106">這可維持您金鑰和密碼的高持久性。</span><span class="sxs-lookup"><span data-stu-id="4eda4-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="4eda4-107">請參閱 [Azure 配對的區域](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions)文件，以取得特定區域配對的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4eda4-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="4eda4-108">如果金鑰保存庫服務內的個別元件失敗，則區域內的替代元件會接替來處理您的要求，以確保不會導致功能的效能降低。</span><span class="sxs-lookup"><span data-stu-id="4eda4-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="4eda4-109">您不需要採取任何動作以觸發這項功能。</span><span class="sxs-lookup"><span data-stu-id="4eda4-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="4eda4-110">它會以您無法察覺的方式自動發生。</span><span class="sxs-lookup"><span data-stu-id="4eda4-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="4eda4-111">在整個 Azure 區域都無法供使用的罕見情況下，您在該區域中所發出的「Azure 金鑰保存庫」要求會自動路由傳送 (容錯移轉) 到次要地區。</span><span class="sxs-lookup"><span data-stu-id="4eda4-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="4eda4-112">當主要區域再次可用時，要求就會路由傳送回 (容錯回復) 主要區域。</span><span class="sxs-lookup"><span data-stu-id="4eda4-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="4eda4-113">同樣地，您不需要採取任何動作，因為這會自動發生。</span><span class="sxs-lookup"><span data-stu-id="4eda4-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="4eda4-114">有一些要注意的警告事項：</span><span class="sxs-lookup"><span data-stu-id="4eda4-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="4eda4-115">發生區域容錯移轉時，可能需要幾分鐘讓服務進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4eda4-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="4eda4-116">在這段時間直到容錯移轉完成之前所發出的要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4eda4-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="4eda4-117">容錯移轉完成之後，您的金鑰保存庫會處於唯讀模式。</span><span class="sxs-lookup"><span data-stu-id="4eda4-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="4eda4-118">在此模式中支援的要求是：</span><span class="sxs-lookup"><span data-stu-id="4eda4-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="4eda4-119">列出金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="4eda4-119">List key vaults</span></span>
  * <span data-ttu-id="4eda4-120">取得金鑰保存庫的屬性</span><span class="sxs-lookup"><span data-stu-id="4eda4-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="4eda4-121">列出密碼</span><span class="sxs-lookup"><span data-stu-id="4eda4-121">List secrets</span></span>
  * <span data-ttu-id="4eda4-122">取得密碼</span><span class="sxs-lookup"><span data-stu-id="4eda4-122">Get secrets</span></span>
  * <span data-ttu-id="4eda4-123">列出金鑰</span><span class="sxs-lookup"><span data-stu-id="4eda4-123">List keys</span></span>
  * <span data-ttu-id="4eda4-124">取得金鑰 (的屬性)</span><span class="sxs-lookup"><span data-stu-id="4eda4-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="4eda4-125">加密</span><span class="sxs-lookup"><span data-stu-id="4eda4-125">Encrypt</span></span>
  * <span data-ttu-id="4eda4-126">解密</span><span class="sxs-lookup"><span data-stu-id="4eda4-126">Decrypt</span></span>
  * <span data-ttu-id="4eda4-127">包裝</span><span class="sxs-lookup"><span data-stu-id="4eda4-127">Wrap</span></span>
  * <span data-ttu-id="4eda4-128">解除包裝</span><span class="sxs-lookup"><span data-stu-id="4eda4-128">Unwrap</span></span>
  * <span data-ttu-id="4eda4-129">Verify</span><span class="sxs-lookup"><span data-stu-id="4eda4-129">Verify</span></span>
  * <span data-ttu-id="4eda4-130">簽署</span><span class="sxs-lookup"><span data-stu-id="4eda4-130">Sign</span></span>
  * <span data-ttu-id="4eda4-131">備份</span><span class="sxs-lookup"><span data-stu-id="4eda4-131">Backup</span></span>
* <span data-ttu-id="4eda4-132">在容錯移轉進行容錯回復之後，所有要求類型 (包括讀取「和」寫入要求) 都會可供使用。</span><span class="sxs-lookup"><span data-stu-id="4eda4-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

