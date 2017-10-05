---
title: "Azure 中 Linux VM 的訂用帳戶和帳戶 | Microsoft Docs"
description: "了解 Azure 上訂用帳戶和帳戶的關鍵設計和實作指導方針。"
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
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="a1f96-103">適用於 Linux VM 的 Azure 訂用帳戶和帳戶指導方針</span><span class="sxs-lookup"><span data-stu-id="a1f96-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="a1f96-104">本文著重於了解在環境和使用者群增加的情況下，管理訂用帳戶和帳戶的方法。</span><span class="sxs-lookup"><span data-stu-id="a1f96-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="a1f96-105">訂用帳戶和帳戶的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="a1f96-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="a1f96-106">决策：</span><span class="sxs-lookup"><span data-stu-id="a1f96-106">Decisions:</span></span>

* <span data-ttu-id="a1f96-107">您需要裝載 IT 工作負載或基礎結構的是哪種訂用帳戶與帳戶的組合？</span><span class="sxs-lookup"><span data-stu-id="a1f96-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="a1f96-108">如何分解階層以使其符合您的組織？</span><span class="sxs-lookup"><span data-stu-id="a1f96-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="a1f96-109">工作：</span><span class="sxs-lookup"><span data-stu-id="a1f96-109">Tasks:</span></span>

* <span data-ttu-id="a1f96-110">將您的邏輯組織階層定義為您想從訂用帳戶層級管理它的方式。</span><span class="sxs-lookup"><span data-stu-id="a1f96-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="a1f96-111">若要符合此邏輯階層，請定義所需的帳戶及每個帳戶下的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1f96-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="a1f96-112">使用您的命名慣例來建立訂用帳戶與帳戶的組合。</span><span class="sxs-lookup"><span data-stu-id="a1f96-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="a1f96-113">訂用帳戶與帳戶</span><span class="sxs-lookup"><span data-stu-id="a1f96-113">Subscriptions and accounts</span></span>
<span data-ttu-id="a1f96-114">若要使用 Azure，您需要一個以上的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1f96-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="a1f96-115">虛擬機器 (VM) 或虛擬網路等資源存在於這些訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a1f96-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="a1f96-116">企業客戶通常會有 Enterprise 註冊，這是階層中最上層的資源，而且會與一或多個帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="a1f96-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="a1f96-117">對於消費者與不具 Enterprise 註冊的客戶來說，最上層的資源是帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1f96-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="a1f96-118">訂用帳戶會關聯至帳戶，而且每個帳戶可以有一或多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1f96-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="a1f96-119">Azure 會在訂用帳戶層級記錄計費資訊。</span><span class="sxs-lookup"><span data-stu-id="a1f96-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="a1f96-120">由於帳戶/訂用帳戶關係中有兩個階層層級的限制，因此，請務必將帳戶和訂用帳戶的命名慣例與計費需求保持一致。</span><span class="sxs-lookup"><span data-stu-id="a1f96-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="a1f96-121">舉例來說，如果有一家全球性公司使用 Azure，他們可能選擇針對每個區域擁有一個帳戶，並在區域層級管理訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="a1f96-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="a1f96-122">例如，您可以使用下列結構：</span><span class="sxs-lookup"><span data-stu-id="a1f96-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="a1f96-123">如果某個區域決定擁有一個以上與特定群組相關聯的訂用帳戶，則命名慣例必須包括在帳戶或訂用帳戶名稱上為額外資料進行編碼的方式。</span><span class="sxs-lookup"><span data-stu-id="a1f96-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="a1f96-124">這個組織允許訊息傳遞計費資料在計費報告期間產生新的階層層級：</span><span class="sxs-lookup"><span data-stu-id="a1f96-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="a1f96-125">組織應看起來如下範例所示：</span><span class="sxs-lookup"><span data-stu-id="a1f96-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="a1f96-126">我們會透過可下載的檔案，針對單一帳戶或企業合約中的所有帳戶提供詳細的計費資訊。</span><span class="sxs-lookup"><span data-stu-id="a1f96-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1f96-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1f96-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

