---
title: "在 Azure 金鑰保存庫會影響 Azure 服務中斷的 hello 事件 aaaWhat toodo |Microsoft 文件"
description: "了解哪些 toodo hello 事件的 Azure 服務中斷影響 Azure 金鑰保存庫中。"
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="b5eaf-103">Azure 金鑰保存庫的可用性與備援</span><span class="sxs-lookup"><span data-stu-id="b5eaf-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="b5eaf-104">Azure 金鑰保存庫功能備援性 toomake 確保您的金鑰和密碼保持可用 tooyour 應用程式即使 hello 的個別元件服務失敗的多個圖的層。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="b5eaf-105">hello 金鑰保存庫的內容都會複寫 hello 區域與 tooa 次要區域內至少 150 英哩離開但 hello 內相同的地理位置。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="b5eaf-106">這可維持您金鑰和密碼的高持久性。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="b5eaf-107">請參閱 hello [Azure 配對區域](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions)如需詳細資訊，針對特定區域對文件。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="b5eaf-108">如果 hello 金鑰保存庫服務內的個別元件失敗，hello 區域內的其他元件中的步驟 tooserve 您要求 toomake 確定沒有任何功能降低。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="b5eaf-109">您不需要 tootake 任何動作 tootrigger 這。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="b5eaf-110">它會自動發生，且將透明 tooyou。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="b5eaf-111">自動路由在 hello 罕見事件中的整個 Azure 區域，就無法使用，您對 Azure 金鑰保存庫，在該區域中的 hello 要求 (*容錯*) tooa 次要區域。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="b5eaf-112">Hello 主要區域再次可用時，要求會路由回到 (*無法回*) toohello 主要區域。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="b5eaf-113">同樣地，您不需要 tootake 任何動作因為這會自動發生。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="b5eaf-114">有幾個警告 toobe 留意：</span><span class="sxs-lookup"><span data-stu-id="b5eaf-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="b5eaf-115">在 hello 事件中的區域容錯移轉，可能需要幾分鐘，讓 hello 服務 toofail。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="b5eaf-116">在這段期間發出的要求可能會失敗，直到 hello 容錯移轉完成為止。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="b5eaf-117">容錯移轉完成之後，您的金鑰保存庫會處於唯讀模式。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="b5eaf-118">在此模式中支援的要求是：</span><span class="sxs-lookup"><span data-stu-id="b5eaf-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="b5eaf-119">列出金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="b5eaf-119">List key vaults</span></span>
  * <span data-ttu-id="b5eaf-120">取得金鑰保存庫的屬性</span><span class="sxs-lookup"><span data-stu-id="b5eaf-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="b5eaf-121">列出密碼</span><span class="sxs-lookup"><span data-stu-id="b5eaf-121">List secrets</span></span>
  * <span data-ttu-id="b5eaf-122">取得密碼</span><span class="sxs-lookup"><span data-stu-id="b5eaf-122">Get secrets</span></span>
  * <span data-ttu-id="b5eaf-123">列出金鑰</span><span class="sxs-lookup"><span data-stu-id="b5eaf-123">List keys</span></span>
  * <span data-ttu-id="b5eaf-124">取得金鑰 (的屬性)</span><span class="sxs-lookup"><span data-stu-id="b5eaf-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="b5eaf-125">加密</span><span class="sxs-lookup"><span data-stu-id="b5eaf-125">Encrypt</span></span>
  * <span data-ttu-id="b5eaf-126">解密</span><span class="sxs-lookup"><span data-stu-id="b5eaf-126">Decrypt</span></span>
  * <span data-ttu-id="b5eaf-127">包裝</span><span class="sxs-lookup"><span data-stu-id="b5eaf-127">Wrap</span></span>
  * <span data-ttu-id="b5eaf-128">解除包裝</span><span class="sxs-lookup"><span data-stu-id="b5eaf-128">Unwrap</span></span>
  * <span data-ttu-id="b5eaf-129">Verify</span><span class="sxs-lookup"><span data-stu-id="b5eaf-129">Verify</span></span>
  * <span data-ttu-id="b5eaf-130">簽署</span><span class="sxs-lookup"><span data-stu-id="b5eaf-130">Sign</span></span>
  * <span data-ttu-id="b5eaf-131">備份</span><span class="sxs-lookup"><span data-stu-id="b5eaf-131">Backup</span></span>
* <span data-ttu-id="b5eaf-132">在容錯移轉進行容錯回復之後，所有要求類型 (包括讀取「和」寫入要求) 都會可供使用。</span><span class="sxs-lookup"><span data-stu-id="b5eaf-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

