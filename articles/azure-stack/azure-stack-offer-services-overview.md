---
title: "在 Azure Stack 中提供服務 | Microsoft Docs"
description: "作為雲端操作員，您可以向使用者提供服務。"
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
ms.openlocfilehash: 785acbeba7eebea5a0414ac8bb9942410bf4252e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="74e5b-103">Azure Stack 中的服務供應項目概觀</span><span class="sxs-lookup"><span data-stu-id="74e5b-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="74e5b-104">Microsoft Azure Stack 是混合式雲端平台，可讓您的資料中心提供服務。</span><span class="sxs-lookup"><span data-stu-id="74e5b-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="74e5b-105">作為服務提供者，您可以提供服務給租用戶。</span><span class="sxs-lookup"><span data-stu-id="74e5b-105">As a service provider, you can offer services to your tenants.</span></span> <span data-ttu-id="74e5b-106">在企業或政府機構中，您可以提供內部部署服務給您的員工。</span><span class="sxs-lookup"><span data-stu-id="74e5b-106">Within a business or government agency, you can offer on-premises services to your employees.</span></span> <span data-ttu-id="74e5b-107">您可以傳遞的服務包括、但不限於：</span><span class="sxs-lookup"><span data-stu-id="74e5b-107">The services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="74e5b-108">平台即服務 (PaaS) 服務，例如應用程式服務、行動應用程式、API Apps、API 函式、SQL、MySQL。</span><span class="sxs-lookup"><span data-stu-id="74e5b-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="74e5b-109">軟體即服務 (SaaS) 服務，例如 Sharepoint。</span><span class="sxs-lookup"><span data-stu-id="74e5b-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="74e5b-110">您甚至可以結合服務，針對不同的使用者整合和建置複雜的解決方案。</span><span class="sxs-lookup"><span data-stu-id="74e5b-110">You can even combine services to integrate and build complex solutions for different users.</span></span>

<span data-ttu-id="74e5b-111">若要將這些服務提供給您的使用者，您必須建立[計劃、產品和配額](azure-stack-plan-offer-quota-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="74e5b-111">To deliver these services to your users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="74e5b-112">您的使用者接著會訂閱您的產品來使用服務。</span><span class="sxs-lookup"><span data-stu-id="74e5b-112">Your users can then subscribe to your offers to use the services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="74e5b-113">規劃服務產品</span><span class="sxs-lookup"><span data-stu-id="74e5b-113">Plan your service offers</span></span>

<span data-ttu-id="74e5b-114">規劃產品時，請記住下列重點：</span><span class="sxs-lookup"><span data-stu-id="74e5b-114">When you’re planning your offers, keep the following points in mind:</span></span>

<span data-ttu-id="74e5b-115">**試用產品**：您可以使用試用產品來吸引新使用者，接著升級到其他服務。</span><span class="sxs-lookup"><span data-stu-id="74e5b-115">**Trial offers**: You can use trial offers to attract new users, who can then upgrade to additional services.</span></span> <span data-ttu-id="74e5b-116">若要建立試用產品，請建立小型的[基本方案](azure-stack-plan-offer-quota-overview.md#base-plan)與選用的大附加元件方案。</span><span class="sxs-lookup"><span data-stu-id="74e5b-116">To create a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="74e5b-117">**容量規劃**：您可能會擔心使用者擷取大量資源，然後阻礙系統的所有使用者使用。</span><span class="sxs-lookup"><span data-stu-id="74e5b-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging the system for all users.</span></span> <span data-ttu-id="74e5b-118">若要協助改善效能，您可以[設定方案與配額](azure-stack-plan-offer-quota-overview.md#plans)來規劃使用方式。</span><span class="sxs-lookup"><span data-stu-id="74e5b-118">To help performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) to cap usage.</span></span>

<span data-ttu-id="74e5b-119">**委派的提供者**：您可將在您的環境中建立產品的能力授與其他人。</span><span class="sxs-lookup"><span data-stu-id="74e5b-119">**Delegated providers**: You can grant others the ability to create offers in your environment.</span></span> <span data-ttu-id="74e5b-120">例如，如果您是服務提供者，您可以將此能力[委派](azure-stack-delegated-provider.md)給您的轉售商。</span><span class="sxs-lookup"><span data-stu-id="74e5b-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability to your resellers.</span></span> <span data-ttu-id="74e5b-121">或者，如果您是組織，您可以委派給其他部門/分公司。</span><span class="sxs-lookup"><span data-stu-id="74e5b-121">Or, if you’re an organization, you can delegate to other divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74e5b-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74e5b-122">Next steps</span></span>
[<span data-ttu-id="74e5b-123">深入瞭解產品、方案、配額和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="74e5b-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

