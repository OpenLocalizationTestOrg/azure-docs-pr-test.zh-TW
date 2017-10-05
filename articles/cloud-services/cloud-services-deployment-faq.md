---
title: "Microsoft Azure 雲端服務之部署問題的常見問題集 | Microsoft Docs"
description: "本文列出 Microsoft Azure 雲端服務之部署的相關常見問題集。"
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
ms.openlocfilehash: cb62cd4c4635d9e837dff81a9c4543781dd11adb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="0869a-103">Azure 雲端服務之部署問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="0869a-103">Deployment issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="0869a-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之部署問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="0869a-104">This article includes frequently asked questions about deployment issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="0869a-105">您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。</span><span class="sxs-lookup"><span data-stu-id="0869a-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-to-the-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-the-production-slot"></a><span data-ttu-id="0869a-106">如果生產位置中已經有現有的部署，為什麼將雲端服務部署至暫存位置時有時候會失敗，並出現資源配置錯誤？</span><span class="sxs-lookup"><span data-stu-id="0869a-106">Why does deploying a cloud service to the staging slot sometimes fail with a resource allocation error if there is already an existing deployment in the production slot?</span></span>
<span data-ttu-id="0869a-107">如果某個雲端服務在任一位置具有部署，整個雲端服務就會釘選到特定的叢集。</span><span class="sxs-lookup"><span data-stu-id="0869a-107">If a cloud service has a deployment in either slot, the entire cloud service is pinned to a specific cluster.</span></span> <span data-ttu-id="0869a-108">這表示如果某個部署已存在生產位置，新的預備部署就只能配置在與生產位置相同的叢集中。</span><span class="sxs-lookup"><span data-stu-id="0869a-108">This means that if a deployment already exists in the production slot, a new staging deployment can only be allocated in the same cluster as the production slot.</span></span>

<span data-ttu-id="0869a-109">當您雲端服務所在的叢集中沒有足夠的實體計算資源可滿足您的部署要求時，就會發生配置失敗。</span><span class="sxs-lookup"><span data-stu-id="0869a-109">Allocation failures occur when the cluster where your cloud service is located does not have enough physical compute resources to satisfy your deployment request.</span></span>

<span data-ttu-id="0869a-110">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="0869a-110">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a><span data-ttu-id="0869a-111">為什麼將雲端服務部署向上擴充或相應放大有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="0869a-111">Why does scaling up or scaling out a cloud service deployment sometimes result in allocation failure?</span></span>
<span data-ttu-id="0869a-112">部署雲端服務時，通常會釘選到特定的叢集。</span><span class="sxs-lookup"><span data-stu-id="0869a-112">When a cloud service is deployed, it usually gets pinned to a specific cluster.</span></span> <span data-ttu-id="0869a-113">這表示向上擴充/相應放大現有的雲端服務必須將新的執行個體配置在相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="0869a-113">This means scaling up/out an existing cloud service must allocate new instances in the same cluster.</span></span> <span data-ttu-id="0869a-114">如果叢集已接近其容量，或無法使用所需的 VM 大小/類型，要求可能就會失敗。</span><span class="sxs-lookup"><span data-stu-id="0869a-114">If the cluster is nearing capacity or the desired VM size/type is not available, the request may fail.</span></span>

<span data-ttu-id="0869a-115">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="0869a-115">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a><span data-ttu-id="0869a-116">為什麼將雲端服務部署至同質群組時，有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="0869a-116">Why does deploying a cloud service into an affinity group sometimes result in allocation failure?</span></span>
<span data-ttu-id="0869a-117">部署到空白雲端服務的新部署可經由該區域中任一叢集的網狀架構配置，除非雲端服務已釘選到某個同質群組。</span><span class="sxs-lookup"><span data-stu-id="0869a-117">A new deployment to an empty cloud service can be allocated by the fabric in any cluster in that region, unless the cloud service is pinned to an affinity group.</span></span> <span data-ttu-id="0869a-118">將在相同的叢集中嘗試部署到相同的同質群組。</span><span class="sxs-lookup"><span data-stu-id="0869a-118">Deployments to the same affinity group will be attempted on the same cluster.</span></span> <span data-ttu-id="0869a-119">如果叢集逼近容量上限，則要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="0869a-119">If the cluster is nearing capacity, the request may fail.</span></span>

<span data-ttu-id="0869a-120">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="0869a-120">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-to-an-existing-cloud-service-sometimes-result-in-allocation-failure"></a><span data-ttu-id="0869a-121">為什麼變更 VM 大小或將新的 VM 新增至現有雲端服務時，有時會造成配置失敗？</span><span class="sxs-lookup"><span data-stu-id="0869a-121">Why does changing VM size or adding a new VM to an existing cloud service sometimes result in allocation failure?</span></span>
<span data-ttu-id="0869a-122">資料中心內的叢集可能會有電腦類型的不同設定 (例如，A 系列、Av2 系列、D 系列、Dv2 系列、G 系列、H 系列等)。</span><span class="sxs-lookup"><span data-stu-id="0869a-122">The clusters in a datacenter may have different configurations of machine types (e.g., A series, Av2 series, D series, Dv2 series, G series, H series, etc.).</span></span> <span data-ttu-id="0869a-123">但並非所有的叢集都一定會有所有種類的 VM。</span><span class="sxs-lookup"><span data-stu-id="0869a-123">But not all the clusters would necessarily have all the kinds of VMs.</span></span> <span data-ttu-id="0869a-124">例如，如果您嘗試新增到雲端服務的 D 系列 VM 已部署在僅限 A 系列的叢集中，就會發生配置失敗。</span><span class="sxs-lookup"><span data-stu-id="0869a-124">For example, if you try to add a D series VM to a cloud service that is already deployed in an A series-only cluster, you will experience an allocation failure.</span></span> <span data-ttu-id="0869a-125">如果您嘗試變更 VM SKU 大小 (例如，從 A 系列切換至 D 系列)，也會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="0869a-125">This will also happen if you try to change VM SKU sizes (for example, switching from an A series to a D series).</span></span>

<span data-ttu-id="0869a-126">如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。</span><span class="sxs-lookup"><span data-stu-id="0869a-126">For help mitigating such allocation failures, see [Cloud Service allocation failure: Solutions](cloud-services-allocation-failures.md#solutions).</span></span>

<span data-ttu-id="0869a-127">若要檢查您地區中可用的大小，請參閱 [Microsoft Azure：依區域提供的產品](https://azure.microsoft.com/regions/services)。</span><span class="sxs-lookup"><span data-stu-id="0869a-127">To check the sizes available in your region, see [Microsoft Azure: Products available by region](https://azure.microsoft.com/regions/services).</span></span>

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-to-limitsquotasconstraints-on-my-subscription-or-service"></a><span data-ttu-id="0869a-128">為什麼部署雲端服務有時會因為我訂用帳戶或服務的限制/配額/條件約束而失敗？</span><span class="sxs-lookup"><span data-stu-id="0869a-128">Why does deploying a cloud service sometime fail due to limits/quotas/constraints on my subscription or service?</span></span>
<span data-ttu-id="0869a-129">如果配置所需的資源超過預設值，或超過您區域/資料中心層級所允許的最大配額，雲端服務部署就可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="0869a-129">Deployment of a cloud service may fail if the resources that are required to be allocated exceed the default or maximum quota allowed for your service at the region/datacenter level.</span></span> <span data-ttu-id="0869a-130">如需詳細資訊，請參閱[雲端服務限制](../azure-subscription-service-limits.md#cloud-services-limits)。</span><span class="sxs-lookup"><span data-stu-id="0869a-130">For more information, see [Cloud Services limits](../azure-subscription-service-limits.md#cloud-services-limits).</span></span>

<span data-ttu-id="0869a-131">您也可以在入口網站追蹤訂用帳戶目前的使用量/配額：Azure 入口網站  => 訂用帳戶  => \<適當的訂用帳戶 > => 使用方式 + 配額。</span><span class="sxs-lookup"><span data-stu-id="0869a-131">You could also track the current usage/quota for your subscription at the portal: Azure Portal => Subscriptions => \<appropriate subscription> => “Usage + quota”.</span></span>

<span data-ttu-id="0869a-132">也可以透過 Azure 計費 API 擷取資源使用量/耗用量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0869a-132">Resource usage/consumption-related information can also be retrieved via the Azure Billing APIs.</span></span> <span data-ttu-id="0869a-133">請參閱 [Azure 資源使用情況 API (預覽)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview)。</span><span class="sxs-lookup"><span data-stu-id="0869a-133">See [Azure Resource Usage API (Preview)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).</span></span>

## <a name="how-can-i-change-the-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a><span data-ttu-id="0869a-134">如何在不重新部署的情況下變更已部署之雲端服務 VM 的大小？</span><span class="sxs-lookup"><span data-stu-id="0869a-134">How can I change the size of a deployed cloud service VM without redeploying it?</span></span>
<span data-ttu-id="0869a-135">您無法在不重新部署的情況下變更已部署之雲端服務的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="0869a-135">You cannot change the VM size of a deployed cloud service without redeploying it.</span></span> <span data-ttu-id="0869a-136">VM 大小已內建於 CSDEF，只可使用重新部署來進行更新。</span><span class="sxs-lookup"><span data-stu-id="0869a-136">The VM size is built into the CSDEF, which can only be updated with a redeploy.</span></span>

<span data-ttu-id="0869a-137">如需詳細資訊，請參閱[如何更新雲端服務](cloud-services-update-azure-service.md)。</span><span class="sxs-lookup"><span data-stu-id="0869a-137">For more information, see [How to update a cloud service](cloud-services-update-azure-service.md).</span></span>

 
