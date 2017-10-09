---
title: "aaaAzure 堆疊計劃、 方案、 配額和訂用帳戶概觀 |Microsoft 文件"
description: "雲端操作員，我想的 toounderstand Azure 堆疊計劃、 提供項目、 配額和訂用帳戶。"
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
ms.openlocfilehash: 67f5bcfda221473b1f397668e2a3186b80d6f43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-offer-quota-and-subscription-overview"></a><span data-ttu-id="e677d-103">方案、優惠、配頭和訂用帳戶概觀</span><span class="sxs-lookup"><span data-stu-id="e677d-103">Plan, offer, quota, and subscription overview</span></span>

<span data-ttu-id="e677d-104">Azure Stack 可讓您提供各式各樣的服務，例如虛擬機器、SQL Server 資料庫、SharePoint、Exchange，甚至 [Azure Marketplace 項目](azure-stack-marketplace-azure-items.md)。</span><span class="sxs-lookup"><span data-stu-id="e677d-104">Azure Stack lets you deliver a wide variety of services, like virtual machines, SQL Server databases, SharePoint, Exchange, and even [Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="e677d-105">身為雲端操作員，您可以使用方案、供應項目與配額，在 Azure Stack 中設定並提供這類服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-105">As a cloud operator, you configure and deliver such services in Azure Stack by using plans, offers, and quotas.</span></span>

<span data-ttu-id="e677d-106">供應項目包含一個或多個方案，而且每個方案包含一個或多個服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-106">Offers contain one or more plans, and each plan includes one or more services.</span></span> <span data-ttu-id="e677d-107">透過建立方案並將其組合成不同的供應項目，您可以控制</span><span class="sxs-lookup"><span data-stu-id="e677d-107">By creating plans and combining them into different offers, you control</span></span>
- <span data-ttu-id="e677d-108">使用者可以存取的服務和資源</span><span class="sxs-lookup"><span data-stu-id="e677d-108">which services and resources users can access</span></span>
- <span data-ttu-id="e677d-109">使用者可以使用這些資源的 hello 數量</span><span class="sxs-lookup"><span data-stu-id="e677d-109">hello amount of those resources that users can consume</span></span>
- <span data-ttu-id="e677d-110">哪些區域可以存取 toohello 資源</span><span class="sxs-lookup"><span data-stu-id="e677d-110">which regions have access toohello resources</span></span>

<span data-ttu-id="e677d-111">當您提供服務時，將遵循下列大致步驟：</span><span class="sxs-lookup"><span data-stu-id="e677d-111">When you deliver a service, you'll follow these high-level steps:</span></span>

1. <span data-ttu-id="e677d-112">新增您要讓 toodeliver tooyour 使用者的服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-112">Add a service that you want toodeliver tooyour users.</span></span>
2. <span data-ttu-id="e677d-113">建立包含一個或多個服務的方案。</span><span class="sxs-lookup"><span data-stu-id="e677d-113">Create a plan that contains one or more services.</span></span> <span data-ttu-id="e677d-114">建立計畫時，您將會選取或建立 hello 計劃中定義的每個服務的 hello 資源限制的配額。</span><span class="sxs-lookup"><span data-stu-id="e677d-114">When creating a plan, you will select or create quotas that define hello resource limits of each service in hello plan.</span></span>
3. <span data-ttu-id="e677d-115">建立包含一個或多個方案 (包含基本方案及選擇性的附加方案) 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="e677d-115">Create an offer that contains one or more plans (including base plans and optional add-on plans).</span></span>

<span data-ttu-id="e677d-116">建立 hello 供應項目之後，您的使用者可以訂閱 tooit tooaccess hello 服務及它所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="e677d-116">After you have created hello offer, your users can subscribe tooit tooaccess hello services and resources it provides.</span></span> <span data-ttu-id="e677d-117">使用者可以訂閱 tooas 許多提供他們想要。</span><span class="sxs-lookup"><span data-stu-id="e677d-117">Users can subscribe tooas many offers as they want.</span></span> <span data-ttu-id="e677d-118">hello 下列圖表顯示的使用者已訂閱 tootwo 優惠的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="e677d-118">hello following diagram shows a simple example of a user who has subscribed tootwo offers.</span></span> <span data-ttu-id="e677d-119">每個供應項目計劃或兩個，且每個計劃可讓他們存取 tooservices。</span><span class="sxs-lookup"><span data-stu-id="e677d-119">Each offer has a plan or two, and each plan gives them access tooservices.</span></span>

![](media/azure-stack-key-features/image4.png)

## <a name="plans"></a><span data-ttu-id="e677d-120">方案</span><span class="sxs-lookup"><span data-stu-id="e677d-120">Plans</span></span>

<span data-ttu-id="e677d-121">方案結合一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-121">Plans are groupings of one or more services.</span></span> <span data-ttu-id="e677d-122">雲端操作員您[建立計劃](azure-stack-create-plan.md)toooffer tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="e677d-122">As a cloud operator, you [create plans](azure-stack-create-plan.md) toooffer tooyour users.</span></span> <span data-ttu-id="e677d-123">接著，您的使用者訂閱 tooyour 優惠 toouse hello 計劃和它們所包含的服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-123">In turn, your users subscribe tooyour offers toouse hello plans and services they include.</span></span> <span data-ttu-id="e677d-124">在建立計畫時，您的配額，請確定 tooset、 定義基底的計劃，並考慮包括選擇性的附加元件計劃。</span><span class="sxs-lookup"><span data-stu-id="e677d-124">When creating plans, make sure tooset your quotas, define your base plans, and consider including optional add-on plans.</span></span>

### <a name="quotas"></a><span data-ttu-id="e677d-125">配額</span><span class="sxs-lookup"><span data-stu-id="e677d-125">Quotas</span></span>

<span data-ttu-id="e677d-126">管理您的雲端容量的 toohelp，選取或建立計劃中的每個服務的配額。</span><span class="sxs-lookup"><span data-stu-id="e677d-126">toohelp you manage your cloud capacity, you select or create a quota for each service in a plan.</span></span> <span data-ttu-id="e677d-127">配額會定義使用者訂用帳戶可以佈建或取用 hello 上層資源限制。</span><span class="sxs-lookup"><span data-stu-id="e677d-127">Quotas define hello upper resource limits that a user subscription can provision or consume.</span></span> <span data-ttu-id="e677d-128">例如，配額可能允許使用者 toocreate toofive 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e677d-128">For example, a quota might allow a user toocreate up toofive virtual machines.</span></span> <span data-ttu-id="e677d-129">配額可以限制各種不同的資源，例如虛擬機器、RAM 和 CPU 限制。</span><span class="sxs-lookup"><span data-stu-id="e677d-129">Quotas can limit a variety of resources, like virtual machines, RAM, and CPU limits.</span></span>

<span data-ttu-id="e677d-130">配額可依地區設定。</span><span class="sxs-lookup"><span data-stu-id="e677d-130">Quotas can be configured by region.</span></span> <span data-ttu-id="e677d-131">例如，包含來自區域 A 計算服務的方案，其配額可能是兩部虛擬機器、4-GB RAM 與 10 個 CPU 核心。</span><span class="sxs-lookup"><span data-stu-id="e677d-131">For example, a plan containing compute services from Region A could have a quota of two virtual machines, 4-GB RAM, and 10 CPU cores.</span></span> <span data-ttu-id="e677d-132">在 hello Azure 堆疊開發套件，只有一個區域 (名為*本機*) 使用。</span><span class="sxs-lookup"><span data-stu-id="e677d-132">In hello Azure Stack Development Kit, only one region (named *local*) is available.</span></span>

### <a name="base-plan"></a><span data-ttu-id="e677d-133">基本方案</span><span class="sxs-lookup"><span data-stu-id="e677d-133">Base plan</span></span>

<span data-ttu-id="e677d-134">當建立提供項目，hello 服務系統管理員可以包含基底的計劃。</span><span class="sxs-lookup"><span data-stu-id="e677d-134">When creating an offer, hello service administrator can include a base plan.</span></span> <span data-ttu-id="e677d-135">當使用者訂閱 toothat 供應項目，則預設會包含這些基底的計劃。</span><span class="sxs-lookup"><span data-stu-id="e677d-135">These base plans are included by default when a user subscribes toothat offer.</span></span> <span data-ttu-id="e677d-136">當使用者訂閱時，他們擁有存取 tooall hello 資源提供者指定的基底的計劃 （與 hello 對應的配額）。</span><span class="sxs-lookup"><span data-stu-id="e677d-136">When a user subscribes, they have access tooall hello resource providers specified in those base plans (with hello corresponding quotas).</span></span>

### <a name="add-on-plans"></a><span data-ttu-id="e677d-137">附加方案</span><span class="sxs-lookup"><span data-stu-id="e677d-137">Add-on plans</span></span>

<span data-ttu-id="e677d-138">您也可以在供應項目中包含選擇性的附加方案。</span><span class="sxs-lookup"><span data-stu-id="e677d-138">You can also include optional add-on plans in an offer.</span></span> <span data-ttu-id="e677d-139">附加元件計劃不會包含的 hello 訂用帳戶中的預設值。</span><span class="sxs-lookup"><span data-stu-id="e677d-139">Add-on plans are not included by default in hello subscription.</span></span> <span data-ttu-id="e677d-140">其他的計劃 （與配額） 可用的訂閱者可以加入 tootheir 訂用帳戶 的項目是附加元件計劃。</span><span class="sxs-lookup"><span data-stu-id="e677d-140">Add-on plans are additional plans (with quotas) available in an offer that a subscriber can add tootheir subscriptions.</span></span> <span data-ttu-id="e677d-141">例如，您可以提供資源有限的試用版，基本方案與附加元件計劃與更多資源 toocustomers 決定 tooadopt hello 服務人員。</span><span class="sxs-lookup"><span data-stu-id="e677d-141">For example, you can offer a base plan with limited resources for a trial, and an add-on plan with more substantial resources toocustomers who decide tooadopt hello service.</span></span>

## <a name="offers"></a><span data-ttu-id="e677d-142">優惠</span><span class="sxs-lookup"><span data-stu-id="e677d-142">Offers</span></span>

<span data-ttu-id="e677d-143">提供項目是的一或多個計劃，好讓使用者可以訂閱 toothem 您建立的群組。</span><span class="sxs-lookup"><span data-stu-id="e677d-143">Offers are groups of one or more plans that you create so that users can subscribe toothem.</span></span> <span data-ttu-id="e677d-144">例如，產品 Alpha 可以包含方案 A (包含一組計算服務) 與方案 B (包含一組儲存體與網路服務)。</span><span class="sxs-lookup"><span data-stu-id="e677d-144">For example, Offer Alpha can contain Plan A containing a set of compute services and Plan B containing a set of storage and network services.</span></span> 

<span data-ttu-id="e677d-145">當您[建立優惠](azure-stack-create-offer.md)，您必須包含至少一個基底的計劃，但您也可以建立使用者可以加入 tootheir 訂用帳戶的附加元件計劃。</span><span class="sxs-lookup"><span data-stu-id="e677d-145">When you [create an offer](azure-stack-create-offer.md), you must include at least one base plan, but you can also create add-on plans that users can add tootheir subscription.</span></span>


## <a name="subscriptions"></a><span data-ttu-id="e677d-146">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e677d-146">Subscriptions</span></span>

<span data-ttu-id="e677d-147">訂用帳戶是使用者存取供應項目的方式。</span><span class="sxs-lookup"><span data-stu-id="e677d-147">A subscription is how users access your offers.</span></span> <span data-ttu-id="e677d-148">如果您是在服務提供者雲端操作員，您的使用者 （租用戶） 會藉由訂閱 tooyour 優惠購買您的服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-148">If you’re a cloud operator at a service provider, your users (tenants) buy your services by subscribing tooyour offers.</span></span> <span data-ttu-id="e677d-149">如果您是組織在雲端操作員，您的使用者 （員工） 可以訂閱 toohello 而不必付出您提供的服務。</span><span class="sxs-lookup"><span data-stu-id="e677d-149">If you’re a cloud operator at an organization, your users (employees) can subscribe toohello services you offer without paying.</span></span> <span data-ttu-id="e677d-150">使用者與供應項目的每個組合都是一個唯一的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e677d-150">Each combination of a user with an offer is a unique subscription.</span></span> <span data-ttu-id="e677d-151">因此，使用者可以擁有訂閱 toomultiple 提供項目，但每個訂閱適 tooonly 一個供應項目。</span><span class="sxs-lookup"><span data-stu-id="e677d-151">Thus, a user can have subscriptions toomultiple offers, but each subscription applies tooonly one offer.</span></span> <span data-ttu-id="e677d-152">計劃、 提議，與配額套用 tooeach 唯一訂閱 – 訂用帳戶之間不共用它們。</span><span class="sxs-lookup"><span data-stu-id="e677d-152">Plans, offers, and quotas apply only tooeach unique subscription – they can’t be shared between subscriptions.</span></span> <span data-ttu-id="e677d-153">使用者建立的每個資源都與一個訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="e677d-153">Each resource that a user creates is associated with one subscription.</span></span>


### <a name="default-provider-subscription"></a><span data-ttu-id="e677d-154">預設的提供者訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e677d-154">Default provider subscription</span></span>

<span data-ttu-id="e677d-155">當您部署的 hello Azure 堆疊開發套件時，會自動建立 hello 預設提供者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e677d-155">hello Default Provider Subscription is automatically created when you deploy hello Azure Stack Development Kit.</span></span> <span data-ttu-id="e677d-156">此訂用帳戶可使用的 toomanage Azure 堆疊、 部署進一步的資源提供者，及建立計劃與提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="e677d-156">This subscription can be used toomanage Azure Stack, deploy further resource providers, and create plans and offers for users.</span></span> <span data-ttu-id="e677d-157">基於安全性和授權的原因，它不應該使用的 toorun 客戶工作負載和應用程式。</span><span class="sxs-lookup"><span data-stu-id="e677d-157">For security and licensing reasons, it should not be used toorun customer workloads and applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e677d-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e677d-158">Next steps</span></span>

[<span data-ttu-id="e677d-159">建立方案</span><span class="sxs-lookup"><span data-stu-id="e677d-159">Create a plan</span></span>](azure-stack-create-plan.md)
