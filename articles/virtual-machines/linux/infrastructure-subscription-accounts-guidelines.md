---
title: "aaaSubscription 和適用於 Linux Vm 在 Azure 中的帳戶 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針訂用帳戶和 Azure 上的帳戶。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="58bba-103">適用於 Linux VM 的 Azure 訂用帳戶和帳戶指導方針</span><span class="sxs-lookup"><span data-stu-id="58bba-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="58bba-104">本文著重在了解如何為您的環境與使用者基底的 tooapproach 訂用帳戶和帳戶管理成長。</span><span class="sxs-lookup"><span data-stu-id="58bba-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="58bba-105">訂用帳戶和帳戶的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="58bba-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="58bba-106">决策：</span><span class="sxs-lookup"><span data-stu-id="58bba-106">Decisions:</span></span>

* <span data-ttu-id="58bba-107">哪些設定訂用帳戶和帳戶您需要 toohost 您的 IT 工作負載或基礎結構？</span><span class="sxs-lookup"><span data-stu-id="58bba-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="58bba-108">如何關閉 hello 階層 toofit toobreak 組織嗎？</span><span class="sxs-lookup"><span data-stu-id="58bba-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="58bba-109">工作：</span><span class="sxs-lookup"><span data-stu-id="58bba-109">Tasks:</span></span>

* <span data-ttu-id="58bba-110">定義邏輯組織階層，您希望 toomanage 從訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="58bba-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="58bba-111">toomatch 此邏輯的階層架構，定義所需的 hello 帳戶和訂用帳戶底下的每個帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="58bba-112">建立 hello 組訂閱和使用您的命名慣例的帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="58bba-113">訂用帳戶與帳戶</span><span class="sxs-lookup"><span data-stu-id="58bba-113">Subscriptions and accounts</span></span>
<span data-ttu-id="58bba-114">使用 Azure toowork，您需要一或多個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="58bba-115">虛擬機器 (VM) 或虛擬網路等資源存在於這些訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="58bba-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="58bba-116">企業客戶通常會有 Enterprise 註冊，這是 hello hello 階層中的最上層資源相關聯的 tooone 或多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="58bba-117">取用者，而不需要企業註冊的客戶 hello 最上層資源是 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="58bba-118">訂用帳戶相關聯的 tooaccounts，而且可以有一或多個訂閱，每個帳戶。</span><span class="sxs-lookup"><span data-stu-id="58bba-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="58bba-119">Azure 帳單 hello 訂用帳戶層級資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="58bba-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="58bba-120">Toohello hello 帳戶/訂用帳戶的關聯性的兩個階層層級的限制，因為它不重要 tooalign hello 命名慣例的帳戶和訂用 toohello 計費的需求。</span><span class="sxs-lookup"><span data-stu-id="58bba-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="58bba-121">比方說，如果全域公司使用 Azure，他們可能會選擇每個區域，toohave 一個帳戶和訂閱管理在 hello 區域層級：</span><span class="sxs-lookup"><span data-stu-id="58bba-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="58bba-122">比方說，您可以使用下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="58bba-122">For instance, you might use hello following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="58bba-123">如果區域決定 toohave 多個訂用帳戶相關聯的 tooa 特定群組，hello 命名慣例應該併入方式 tooencode hello hello 帳戶或 hello 訂用帳戶名稱的額外資料。</span><span class="sxs-lookup"><span data-stu-id="58bba-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="58bba-124">此組織允許 massaging 計費報表期間的計費資料 toogenerate hello 新階層的層級：</span><span class="sxs-lookup"><span data-stu-id="58bba-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="58bba-125">hello 組織可能看起來像下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="58bba-125">hello organization could look like hello following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="58bba-126">我們會透過可下載的檔案，針對單一帳戶或企業合約中的所有帳戶提供詳細的計費資訊。</span><span class="sxs-lookup"><span data-stu-id="58bba-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58bba-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58bba-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

