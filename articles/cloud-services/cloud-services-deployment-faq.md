---
title: "Microsoft Azure 雲端服務的常見問題集 aaaDeployment 問題 |Microsoft 文件"
description: "本文列出 Microsoft Azure 雲端服務的部署有關的常見問題集 hello。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="3ddd7-103">Azure 雲端服務之部署問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="3ddd7-103">Deployment issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="3ddd7-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之部署問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-104">This article includes frequently asked questions about deployment issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="3ddd7-105">此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a><span data-ttu-id="3ddd7-106">為什麼部署雲端服務 toohello 有時 staging 位置失敗，資源配置錯誤如果已經有 hello 生產位置中的現有部署？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-106">Why does deploying a cloud service toohello staging slot sometimes fail with a resource allocation error if there is already an existing deployment in hello production slot?</span></span>
<span data-ttu-id="3ddd7-107">如果雲端服務中任一位置部署，hello 整個雲端服務是已釘選的 tooa 特定叢集。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-107">If a cloud service has a deployment in either slot, hello entire cloud service is pinned tooa specific cluster.</span></span> <span data-ttu-id="3ddd7-108">這表示，如果部署已經存在於 hello 生產位置，新的預備環境部署只可配置在 hello 相同叢集為 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-108">This means that if a deployment already exists in hello production slot, a new staging deployment can only be allocated in hello same cluster as hello production slot.</span></span>

<span data-ttu-id="3ddd7-109">您的雲端服務所在的 hello 叢集沒有足夠實體計算資源 toosatisfy 部署要求時，就會發生配置失敗。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-109">Allocation failures occur when hello cluster where your cloud service is located does not have enough physical compute resources toosatisfy your deployment request.</span></span>

<span data-ttu-id="3ddd7-110">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-110">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a><span data-ttu-id="3ddd7-111">為什麼將雲端服務部署向上擴充或相應放大有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-111">Why does scaling up or scaling out a cloud service deployment sometimes result in allocation failure?</span></span>
<span data-ttu-id="3ddd7-112">部署雲端服務時，它通常會取得已釘選的 tooa 特定叢集。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-112">When a cloud service is deployed, it usually gets pinned tooa specific cluster.</span></span> <span data-ttu-id="3ddd7-113">這表示向上延展/出現有雲端服務必須配置 hello 中的新執行個體相同的叢集。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-113">This means scaling up/out an existing cloud service must allocate new instances in hello same cluster.</span></span> <span data-ttu-id="3ddd7-114">如果 hello 叢集已接近其容量或 hello 所需的 VM 大小/類型無法使用，hello 要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-114">If hello cluster is nearing capacity or hello desired VM size/type is not available, hello request may fail.</span></span>

<span data-ttu-id="3ddd7-115">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-115">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a><span data-ttu-id="3ddd7-116">為什麼將雲端服務部署至同質群組時，有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-116">Why does deploying a cloud service into an affinity group sometimes result in allocation failure?</span></span>
<span data-ttu-id="3ddd7-117">可以由任何在該區域中，叢集中的 hello 網狀架構配置新的部署 tooan 空的雲端服務，除非 hello 雲端服務是已釘選的 tooan 同質群組。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-117">A new deployment tooan empty cloud service can be allocated by hello fabric in any cluster in that region, unless hello cloud service is pinned tooan affinity group.</span></span> <span data-ttu-id="3ddd7-118">部署 toohello 相同同質群組將會在 hello 嘗試相同的叢集。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-118">Deployments toohello same affinity group will be attempted on hello same cluster.</span></span> <span data-ttu-id="3ddd7-119">如果 hello 叢集已接近其容量，hello 要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-119">If hello cluster is nearing capacity, hello request may fail.</span></span>

<span data-ttu-id="3ddd7-120">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-120">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a><span data-ttu-id="3ddd7-121">為什麼沒有變更 VM 大小或新增新 VM tooan 現有的雲端服務，有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-121">Why does changing VM size or adding a new VM tooan existing cloud service sometimes result in allocation failure?</span></span>
<span data-ttu-id="3ddd7-122">在資料中心的 hello 群集可能會有不同的電腦類型 （例如，系列、 Av2 系列、 D 系列、 Dv2 數列、 G 系列、 H 數列等） 的設定。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-122">hello clusters in a datacenter may have different configurations of machine types (e.g., A series, Av2 series, D series, Dv2 series, G series, H series, etc.).</span></span> <span data-ttu-id="3ddd7-123">但是並非所有的 hello 叢集一定會有所有的 hello 種類的 Vm。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-123">But not all hello clusters would necessarily have all hello kinds of VMs.</span></span> <span data-ttu-id="3ddd7-124">例如，如果您嘗試 tooadd D 系列中的數列僅限叢集已部署的 VM tooa 雲端服務時，就會發生配置失敗。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-124">For example, if you try tooadd a D series VM tooa cloud service that is already deployed in an A series-only cluster, you will experience an allocation failure.</span></span> <span data-ttu-id="3ddd7-125">這將也會發生如果您嘗試 toochange VM SKU 大小 （例如，從 A tooa D 數列切換）。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-125">This will also happen if you try toochange VM SKU sizes (for example, switching from an A series tooa D series).</span></span>

<span data-ttu-id="3ddd7-126">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-126">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

<span data-ttu-id="3ddd7-127">toocheck hello 可用的大小在區域中，請參閱[Microsoft Azure： 依地區可用的產品](https://azure.microsoft.com/regions/services)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-127">toocheck hello sizes available in your region, see [Microsoft Azure: Products available by region](https://azure.microsoft.com/regions/services).</span></span>

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a><span data-ttu-id="3ddd7-128">為什麼部署雲端服務有時失敗到期 toolimits/配額/條件約束我的訂用帳戶或服務？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-128">Why does deploying a cloud service sometime fail due toolimits/quotas/constraints on my subscription or service?</span></span>
<span data-ttu-id="3ddd7-129">如果配置需要的 toobe hello 資源超過 hello 預設值或允許您的服務在 hello 區域/資料中心層級的最大配額，雲端服務部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-129">Deployment of a cloud service may fail if hello resources that are required toobe allocated exceed hello default or maximum quota allowed for your service at hello region/datacenter level.</span></span> <span data-ttu-id="3ddd7-130">如需詳細資訊，請參閱[雲端服務限制](../azure-subscription-service-limits.md#cloud-services-limits)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-130">For more information, see [Cloud Services limits](../azure-subscription-service-limits.md#cloud-services-limits).</span></span>

<span data-ttu-id="3ddd7-131">您也可以在 hello 入口網站訂用帳戶在追蹤 hello 目前使用量/配額： Azure 入口網站 = > 訂用帳戶 = >\<適當的訂用帳戶 > = > [使用方式 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-131">You could also track hello current usage/quota for your subscription at hello portal: Azure Portal => Subscriptions => \<appropriate subscription> => “Usage + quota”.</span></span>

<span data-ttu-id="3ddd7-132">也可以透過 hello Azure 計費 Api 擷取資源使用量/耗用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-132">Resource usage/consumption-related information can also be retrieved via hello Azure Billing APIs.</span></span> <span data-ttu-id="3ddd7-133">請參閱 [Azure 資源使用情況 API (預覽)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-133">See [Azure Resource Usage API (Preview)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).</span></span>

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a><span data-ttu-id="3ddd7-134">如何變更已部署的雲端服務 VM 的 hello 大小必須重新部署它？</span><span class="sxs-lookup"><span data-stu-id="3ddd7-134">How can I change hello size of a deployed cloud service VM without redeploying it?</span></span>
<span data-ttu-id="3ddd7-135">您無法變更已部署的雲端服務的 hello VM 大小，必須重新部署它。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-135">You cannot change hello VM size of a deployed cloud service without redeploying it.</span></span> <span data-ttu-id="3ddd7-136">hello VM 大小是內建 hello CSDEF，只可使用重新部署更新。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-136">hello VM size is built into hello CSDEF, which can only be updated with a redeploy.</span></span>

<span data-ttu-id="3ddd7-137">如需詳細資訊，請參閱[如何 tooupdate 雲端服務](cloud-services-update-azure-service.md)。</span><span class="sxs-lookup"><span data-stu-id="3ddd7-137">For more information, see [How tooupdate a cloud service](cloud-services-update-azure-service.md).</span></span>

 
