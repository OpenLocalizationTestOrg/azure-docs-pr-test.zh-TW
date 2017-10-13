---
title: "Azure Stack 方案、供應項目、配額和訂用帳戶概觀 | Microsoft Docs"
description: "身為雲端操作員，我想要了解 Azure Stack 方案、供應項目、配額和訂用帳戶。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/22/2017
ms.author: erikje
ms.openlocfilehash: 083ca2f0a06625810d2f90a682ba0b3110032e60
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="plan-offer-quota-and-subscription-overview"></a><span data-ttu-id="1bba5-103">方案、優惠、配頭和訂用帳戶概觀</span><span class="sxs-lookup"><span data-stu-id="1bba5-103">Plan, offer, quota, and subscription overview</span></span>

<span data-ttu-id="1bba5-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="1bba5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="1bba5-105">[Azure Stack](azure-stack-marketplace-azure-items.md) 可讓您提供各式各樣的服務，例如虛擬機器、SQL Server 資料庫、SharePoint、Exchange，甚至 [Azure Marketplace 項目](azure-stack-poc.md)。</span><span class="sxs-lookup"><span data-stu-id="1bba5-105">[Azure Stack](azure-stack-poc.md) lets you deliver a wide variety of services, like virtual machines, SQL Server databases, SharePoint, Exchange, and even [Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="1bba5-106">身為 Azure Stack 操作員，您可以使用方案、供應項目與配額，在 Azure Stack 中設定並提供這類服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-106">As an Azure Stack operator, you configure and deliver such services in Azure Stack by using plans, offers, and quotas.</span></span>

<span data-ttu-id="1bba5-107">供應項目包含一個或多個方案，而且每個方案包含一個或多個服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-107">Offers contain one or more plans, and each plan includes one or more services.</span></span> <span data-ttu-id="1bba5-108">透過建立方案並將其組合成不同的供應項目，您可以控制</span><span class="sxs-lookup"><span data-stu-id="1bba5-108">By creating plans and combining them into different offers, you control</span></span>
- <span data-ttu-id="1bba5-109">使用者可以存取的服務和資源</span><span class="sxs-lookup"><span data-stu-id="1bba5-109">which services and resources users can access</span></span>
- <span data-ttu-id="1bba5-110">使用者可以取用這些資源的數量</span><span class="sxs-lookup"><span data-stu-id="1bba5-110">the amount of those resources that users can consume</span></span>
- <span data-ttu-id="1bba5-111">可以存取資源的區域</span><span class="sxs-lookup"><span data-stu-id="1bba5-111">which regions have access to the resources</span></span>

<span data-ttu-id="1bba5-112">當您提供服務時，將遵循下列大致步驟：</span><span class="sxs-lookup"><span data-stu-id="1bba5-112">When you deliver a service, you'll follow these high-level steps:</span></span>

1. <span data-ttu-id="1bba5-113">新增您要提供給使用者的服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-113">Add a service that you want to deliver to your users.</span></span>
2. <span data-ttu-id="1bba5-114">建立包含一個或多個服務的方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-114">Create a plan that contains one or more services.</span></span> <span data-ttu-id="1bba5-115">建立方案時，您將會選取或建立配額，以定義方案中每個服務的資源限制。</span><span class="sxs-lookup"><span data-stu-id="1bba5-115">When creating a plan, you will select or create quotas that define the resource limits of each service in the plan.</span></span>
3. <span data-ttu-id="1bba5-116">建立包含一個或多個方案 (包含基本方案及選擇性的附加方案) 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="1bba5-116">Create an offer that contains one or more plans (including base plans and optional add-on plans).</span></span>

<span data-ttu-id="1bba5-117">建立供應項目之後，您的使用者就可以訂閱供應項目，以存取它所提供的服務和資源。</span><span class="sxs-lookup"><span data-stu-id="1bba5-117">After you have created the offer, your users can subscribe to it to access the services and resources it provides.</span></span> <span data-ttu-id="1bba5-118">使用者可以訂閱所需的任意數量供應項目。</span><span class="sxs-lookup"><span data-stu-id="1bba5-118">Users can subscribe to as many offers as they want.</span></span> <span data-ttu-id="1bba5-119">下圖顯示的簡單範例是已訂閱兩個供應項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba5-119">The following diagram shows a simple example of a user who has subscribed to two offers.</span></span> <span data-ttu-id="1bba5-120">每個供應項目都有一個或兩個方案，而且每個方案都能提供對服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="1bba5-120">Each offer has a plan or two, and each plan gives them access to services.</span></span>

![](media/azure-stack-key-features/image4.png)

## <a name="plans"></a><span data-ttu-id="1bba5-121">方案</span><span class="sxs-lookup"><span data-stu-id="1bba5-121">Plans</span></span>

<span data-ttu-id="1bba5-122">方案結合一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-122">Plans are groupings of one or more services.</span></span> <span data-ttu-id="1bba5-123">身為 Azure Stack 操作員，您可以[建立方案](azure-stack-create-plan.md)以提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="1bba5-123">As an Azure Stack operator, you [create plans](azure-stack-create-plan.md) to offer to your users.</span></span> <span data-ttu-id="1bba5-124">使用者接著即可訂閱您的供應項目，以使用其中的方案與服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-124">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="1bba5-125">建立方案時，請務必設定配額、定義基本方案，並考慮包含選擇性的附加方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-125">When creating plans, make sure to set your quotas, define your base plans, and consider including optional add-on plans.</span></span>

### <a name="quotas"></a><span data-ttu-id="1bba5-126">配額</span><span class="sxs-lookup"><span data-stu-id="1bba5-126">Quotas</span></span>

<span data-ttu-id="1bba5-127">為了協助管理雲端容量，您可以在方案中，為每個服務選取或建立配額。</span><span class="sxs-lookup"><span data-stu-id="1bba5-127">To help you manage your cloud capacity, you select or create a quota for each service in a plan.</span></span> <span data-ttu-id="1bba5-128">配額會定義使用者訂用帳戶可以佈建或取用的資源上限。</span><span class="sxs-lookup"><span data-stu-id="1bba5-128">Quotas define the upper resource limits that a user subscription can provision or consume.</span></span> <span data-ttu-id="1bba5-129">例如，配額可能會允許使用者建立最多五部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1bba5-129">For example, a quota might allow a user to create up to five virtual machines.</span></span> <span data-ttu-id="1bba5-130">配額可以限制各種不同的資源，例如虛擬機器、RAM 和 CPU 限制。</span><span class="sxs-lookup"><span data-stu-id="1bba5-130">Quotas can limit a variety of resources, like virtual machines, RAM, and CPU limits.</span></span>

<span data-ttu-id="1bba5-131">配額可依地區設定。</span><span class="sxs-lookup"><span data-stu-id="1bba5-131">Quotas can be configured by region.</span></span> <span data-ttu-id="1bba5-132">例如，包含來自區域 A 計算服務的方案，其配額可能是兩部虛擬機器、4-GB RAM 與 10 個 CPU 核心。</span><span class="sxs-lookup"><span data-stu-id="1bba5-132">For example, a plan containing compute services from Region A could have a quota of two virtual machines, 4-GB RAM, and 10 CPU cores.</span></span> <span data-ttu-id="1bba5-133">在 Azure Stack 開發套件中，只有一個區域 (名為 *local*) 可供使用。</span><span class="sxs-lookup"><span data-stu-id="1bba5-133">In the Azure Stack Development Kit, only one region (named *local*) is available.</span></span>

### <a name="base-plan"></a><span data-ttu-id="1bba5-134">基本方案</span><span class="sxs-lookup"><span data-stu-id="1bba5-134">Base plan</span></span>

<span data-ttu-id="1bba5-135">建立供應項目時，服務系統管理員可以包含基本方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-135">When creating an offer, the service administrator can include a base plan.</span></span> <span data-ttu-id="1bba5-136">當使用者訂閱該供應項目時，預設會包含這些基本方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-136">These base plans are included by default when a user subscribes to that offer.</span></span> <span data-ttu-id="1bba5-137">當使用者訂閱時，即可存取這些基本方案中所指定的所有資源提供者 (同時受到對應的配額限制)。</span><span class="sxs-lookup"><span data-stu-id="1bba5-137">When a user subscribes, they have access to all the resource providers specified in those base plans (with the corresponding quotas).</span></span>

### <a name="add-on-plans"></a><span data-ttu-id="1bba5-138">附加方案</span><span class="sxs-lookup"><span data-stu-id="1bba5-138">Add-on plans</span></span>

<span data-ttu-id="1bba5-139">您也可以在供應項目中包含選擇性的附加方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-139">You can also include optional add-on plans in an offer.</span></span> <span data-ttu-id="1bba5-140">訂用帳戶中預設不會包含加購方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-140">Add-on plans are not included by default in the subscription.</span></span> <span data-ttu-id="1bba5-141">供應項目中提供的附加方案屬於額外的方案 (具有配額)，訂閱者可將其加入其訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1bba5-141">Add-on plans are additional plans (with quotas) available in an offer that a subscriber can add to their subscriptions.</span></span> <span data-ttu-id="1bba5-142">例如，您可以提供資源有限的基本方案以供試用，並為決定採用服務的客戶提供更多實質資源的附加方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-142">For example, you can offer a base plan with limited resources for a trial, and an add-on plan with more substantial resources to customers who decide to adopt the service.</span></span>

## <a name="offers"></a><span data-ttu-id="1bba5-143">優惠</span><span class="sxs-lookup"><span data-stu-id="1bba5-143">Offers</span></span>

<span data-ttu-id="1bba5-144">供應項目是您建立的一個或多個方案的群組，使用者可以訂閱這些供應項目。</span><span class="sxs-lookup"><span data-stu-id="1bba5-144">Offers are groups of one or more plans that you create so that users can subscribe to them.</span></span> <span data-ttu-id="1bba5-145">例如，供應項目 Alpha 可以包含方案 A (其中包含一組計算服務) 與方案 B (其中包含一組儲存體與網路服務)。</span><span class="sxs-lookup"><span data-stu-id="1bba5-145">For example, Offer Alpha can contain Plan A containing a set of compute services and Plan B containing a set of storage and network services.</span></span> 

<span data-ttu-id="1bba5-146">當您[建立供應項目](azure-stack-create-offer.md)時，必須至少包含一個基本方案，但是您也可以建立使用者可以加入至其訂用帳戶的附加方案。</span><span class="sxs-lookup"><span data-stu-id="1bba5-146">When you [create an offer](azure-stack-create-offer.md), you must include at least one base plan, but you can also create add-on plans that users can add to their subscription.</span></span>


## <a name="subscriptions"></a><span data-ttu-id="1bba5-147">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bba5-147">Subscriptions</span></span>

<span data-ttu-id="1bba5-148">訂用帳戶是使用者存取供應項目的方式。</span><span class="sxs-lookup"><span data-stu-id="1bba5-148">A subscription is how users access your offers.</span></span> <span data-ttu-id="1bba5-149">如果您是服務提供者的 Azure Stack 操作員，使用者 (租用戶) 會透過訂閱供應項目的方式來購買您的服務。</span><span class="sxs-lookup"><span data-stu-id="1bba5-149">If you’re an Azure Stack operator at a service provider, your users (tenants) buy your services by subscribing to your offers.</span></span> <span data-ttu-id="1bba5-150">如果您是組織的 Azure Stack 操作員，使用者 (員工) 可以訂閱您提供的服務，而不必付錢。</span><span class="sxs-lookup"><span data-stu-id="1bba5-150">If you’re an Azure Stack operator at an organization, your users (employees) can subscribe to the services you offer without paying.</span></span> <span data-ttu-id="1bba5-151">使用者與供應項目的每個組合都是一個唯一的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bba5-151">Each combination of a user with an offer is a unique subscription.</span></span> <span data-ttu-id="1bba5-152">因此，使用者可以擁有多個供應項目的訂用帳戶，但是每個訂用帳戶都僅適用於一個供應項目。</span><span class="sxs-lookup"><span data-stu-id="1bba5-152">Thus, a user can have subscriptions to multiple offers, but each subscription applies to only one offer.</span></span> <span data-ttu-id="1bba5-153">方案、供應項目與配額僅適用於每個唯一的訂用帳戶，而無法在訂用帳戶之間共用。</span><span class="sxs-lookup"><span data-stu-id="1bba5-153">Plans, offers, and quotas apply only to each unique subscription – they can’t be shared between subscriptions.</span></span> <span data-ttu-id="1bba5-154">使用者建立的每個資源都與一個訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="1bba5-154">Each resource that a user creates is associated with one subscription.</span></span>


### <a name="default-provider-subscription"></a><span data-ttu-id="1bba5-155">預設的提供者訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bba5-155">Default provider subscription</span></span>

<span data-ttu-id="1bba5-156">當您部署 Azure Stack 開發套件時，會自動建立預設的提供者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bba5-156">The Default Provider Subscription is automatically created when you deploy the Azure Stack Development Kit.</span></span> <span data-ttu-id="1bba5-157">此訂用帳戶可用來管理 Azure Stack、部署其他資源提供者，以及為使用者建立方案與供應項目。</span><span class="sxs-lookup"><span data-stu-id="1bba5-157">This subscription can be used to manage Azure Stack, deploy further resource providers, and create plans and offers for users.</span></span> <span data-ttu-id="1bba5-158">基於安全性和授權的緣故，此訂用帳戶不應用於執行客戶工作負載和應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bba5-158">For security and licensing reasons, it should not be used to run customer workloads and applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1bba5-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1bba5-159">Next steps</span></span>

[<span data-ttu-id="1bba5-160">建立方案</span><span class="sxs-lookup"><span data-stu-id="1bba5-160">Create a plan</span></span>](azure-stack-create-plan.md)
