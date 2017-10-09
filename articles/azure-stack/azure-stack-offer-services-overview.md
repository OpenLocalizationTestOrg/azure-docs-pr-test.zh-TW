---
title: "在 Azure 堆疊 aaaOffering 服務 |Microsoft 文件"
description: "雲端操作員，您可以提供服務 tooyour 使用者。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 47cff8bfb202527ae4c930c7d1b9eb3998bee85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="aaa85-103">Azure Stack 中的服務供應項目概觀</span><span class="sxs-lookup"><span data-stu-id="aaa85-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="aaa85-104">Microsoft Azure Stack 是混合式雲端平台，可讓您的資料中心提供服務。</span><span class="sxs-lookup"><span data-stu-id="aaa85-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="aaa85-105">做為服務提供者，您可以提供服務 tooyour 租用戶。</span><span class="sxs-lookup"><span data-stu-id="aaa85-105">As a service provider, you can offer services tooyour tenants.</span></span> <span data-ttu-id="aaa85-106">在企業或政府機構中，您可以提供在內部部署服務 tooyour 員工。</span><span class="sxs-lookup"><span data-stu-id="aaa85-106">Within a business or government agency, you can offer on-premises services tooyour employees.</span></span> <span data-ttu-id="aaa85-107">hello 服務，以便您可以將包括但不限於：</span><span class="sxs-lookup"><span data-stu-id="aaa85-107">hello services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="aaa85-108">平台即服務 (PaaS) 服務，例如應用程式服務、行動應用程式、API Apps、API 函式、SQL、MySQL。</span><span class="sxs-lookup"><span data-stu-id="aaa85-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="aaa85-109">軟體即服務 (SaaS) 服務，例如 Sharepoint。</span><span class="sxs-lookup"><span data-stu-id="aaa85-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="aaa85-110">您甚至可以結合服務 toointegrate 並建置複雜的解決方案，針對不同的使用者。</span><span class="sxs-lookup"><span data-stu-id="aaa85-110">You can even combine services toointegrate and build complex solutions for different users.</span></span>

<span data-ttu-id="aaa85-111">toodeliver 這些服務 tooyour 的使用者，您必須建立[計劃、 提議，與配額](azure-stack-plan-offer-quota-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="aaa85-111">toodeliver these services tooyour users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="aaa85-112">然後，您的使用者可以訂閱 tooyour 優惠 toouse hello 服務。</span><span class="sxs-lookup"><span data-stu-id="aaa85-112">Your users can then subscribe tooyour offers toouse hello services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="aaa85-113">規劃服務產品</span><span class="sxs-lookup"><span data-stu-id="aaa85-113">Plan your service offers</span></span>

<span data-ttu-id="aaa85-114">當您計劃您的優惠時，請遵循要點牢記在心的 hello:</span><span class="sxs-lookup"><span data-stu-id="aaa85-114">When you’re planning your offers, keep hello following points in mind:</span></span>

<span data-ttu-id="aaa85-115">**試用優惠**： 您可以使用試用優惠 tooattract 新使用者，可以接著升級 tooadditional 服務。</span><span class="sxs-lookup"><span data-stu-id="aaa85-115">**Trial offers**: You can use trial offers tooattract new users, who can then upgrade tooadditional services.</span></span> <span data-ttu-id="aaa85-116">toocreate 試用優惠，建立一個小型[基本方案](azure-stack-plan-offer-quota-overview.md#base-plan)與選擇性大附加元件的方案。</span><span class="sxs-lookup"><span data-stu-id="aaa85-116">toocreate a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="aaa85-117">**容量規劃**： 您可能會擔心抓取大量的資源，然後繼續 hello 系統的所有使用者的使用者。</span><span class="sxs-lookup"><span data-stu-id="aaa85-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging hello system for all users.</span></span> <span data-ttu-id="aaa85-118">toohelp 效能，您可以[配額設定您的計劃](azure-stack-plan-offer-quota-overview.md#plans)toocap 使用量。</span><span class="sxs-lookup"><span data-stu-id="aaa85-118">toohelp performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) toocap usage.</span></span>

<span data-ttu-id="aaa85-119">**提供者的委派**： 您可以授與其他人 hello 能力 toocreate 提供您的環境中。</span><span class="sxs-lookup"><span data-stu-id="aaa85-119">**Delegated providers**: You can grant others hello ability toocreate offers in your environment.</span></span> <span data-ttu-id="aaa85-120">例如，如果您的服務提供者，您可以[委派](azure-stack-delegated-provider.md)這個能力 tooyour 轉售商。</span><span class="sxs-lookup"><span data-stu-id="aaa85-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability tooyour resellers.</span></span> <span data-ttu-id="aaa85-121">或者，如果您的組織，您可以將委派 tooother 部門/分公司。</span><span class="sxs-lookup"><span data-stu-id="aaa85-121">Or, if you’re an organization, you can delegate tooother divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa85-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aaa85-122">Next steps</span></span>
[<span data-ttu-id="aaa85-123">深入瞭解產品、方案、配額和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aaa85-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

