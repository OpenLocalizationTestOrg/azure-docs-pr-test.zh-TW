---
title: "Azure 訂用帳戶限制與配額 | Microsoft Docs"
description: "提供通用的 Azure 訂用帳戶和服務限制、配額和條件約束的清單。 這包括如何增加限制和最大值的詳細資訊。"
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a76acd67e9ba7822f2837b3c08e2ede389047f11
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="0e45b-104">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="0e45b-105">本文件列出一些最常見的 Microsoft Azure 限制，有時也稱為配額。</span><span class="sxs-lookup"><span data-stu-id="0e45b-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="0e45b-106">本文件目前未涵蓋所有 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="0e45b-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="0e45b-107">清單將隨著時間擴展並更新以涵蓋更多平台。</span><span class="sxs-lookup"><span data-stu-id="0e45b-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="0e45b-108">請瀏覽 [Azure 定價一覽](https://azure.microsoft.com/pricing/) 以深入了解 Azure 定價。</span><span class="sxs-lookup"><span data-stu-id="0e45b-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="0e45b-109">您可以在那裡使用[定價計算機](https://azure.microsoft.com/pricing/calculator/)或透過瀏覽服務 (例如，[Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)) 的定價詳細資料頁面來估計成本。</span><span class="sxs-lookup"><span data-stu-id="0e45b-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="0e45b-110">如需協助您管理成本的祕訣，請參閱[使用 Azure 計費與成本管理避免非預期的成本](billing/billing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0e45b-111">如果您想要將限制或配額提升到**預設限制**以上，您可以[免費提出線上客戶支援要求](azure-supportability/resource-manager-core-quotas-request.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="0e45b-112">您無法將限制提升到高於下表中所示的**上限**值。</span><span class="sxs-lookup"><span data-stu-id="0e45b-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="0e45b-113">如果沒有**上限**欄，資源即沒有可調整的限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="0e45b-114">免費試用訂用帳戶無法增加限制或配額。</span><span class="sxs-lookup"><span data-stu-id="0e45b-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="0e45b-115">如果您有免費試用，則可以升級到 [隨用隨付](https://azure.microsoft.com/offers/ms-azr-0003p/) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e45b-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="0e45b-116">如需詳細資訊，請參閱[將 Azure 免費試用版升級至隨收隨付](billing/billing-upgrade-azure-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="0e45b-117">限制和 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="0e45b-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="0e45b-118">現在您可以結合多個 Azure 中的資源到單一的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="0e45b-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="0e45b-119">使用資源群組時的限制是，在全域時會使用 Azure 資源管理員在地區層級管理。</span><span class="sxs-lookup"><span data-stu-id="0e45b-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="0e45b-120">如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="0e45b-121">在以下的限制中，已加入了新資料表，以反映在使用 Azure 資源管理員時的限制方面的任何差異。</span><span class="sxs-lookup"><span data-stu-id="0e45b-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="0e45b-122">例如，有**訂用帳戶限制**資料表和**訂用帳戶限制 - Azure Resource Manager** 資料表。</span><span class="sxs-lookup"><span data-stu-id="0e45b-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="0e45b-123">當某個限制同時適用於這兩個案例時，只會顯示在第一個資料表中。</span><span class="sxs-lookup"><span data-stu-id="0e45b-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="0e45b-124">除非另有說明，限制在所有區域中全域適用。</span><span class="sxs-lookup"><span data-stu-id="0e45b-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="0e45b-125">請務必強調 Azure 資源群組中資源的配額是基於您的訂閱可以存取的每一區域，而不是每一訂閱 (服務管理配額則是)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="0e45b-126">讓我們以核心配額為例。</span><span class="sxs-lookup"><span data-stu-id="0e45b-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="0e45b-127">如果您需要要求增加配額以支援核心，您必須決定您想要在哪些區域中使用多少個核心，然後提出 Azure 資源群組核心配額的特定要求，以取得您想要的數量和區域。</span><span class="sxs-lookup"><span data-stu-id="0e45b-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="0e45b-128">因此，如果您需要在西歐使用 30 個核心以在該處執行應用程式，您應該在西歐特別要求 30 個核心。</span><span class="sxs-lookup"><span data-stu-id="0e45b-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="0e45b-129">但是您在任何其他區域中的核心配額將不會增加 -- 僅西歐會有 30 個核心配額。</span><span class="sxs-lookup"><span data-stu-id="0e45b-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="0e45b-130">因此，考慮決定每個區域中您的工作負載所需的 Azure 資源群組配額，並在要考慮部署的每個區域中要求該數量可能會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="0e45b-130">As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="0e45b-131">請參閱 [移難排解部署問題](resource-manager-common-deployment-errors.md) ，以取得探索您特定區域目前的配額的其他說明。</span><span class="sxs-lookup"><span data-stu-id="0e45b-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="0e45b-132">特定服務的限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-132">Service-specific limits</span></span>
* [<span data-ttu-id="0e45b-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e45b-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="0e45b-134">API 管理</span><span class="sxs-lookup"><span data-stu-id="0e45b-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="0e45b-135">App Service</span><span class="sxs-lookup"><span data-stu-id="0e45b-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="0e45b-136">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="0e45b-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="0e45b-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="0e45b-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="0e45b-138">自動化</span><span class="sxs-lookup"><span data-stu-id="0e45b-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="0e45b-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0e45b-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="0e45b-140">事件格線</span><span class="sxs-lookup"><span data-stu-id="0e45b-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="0e45b-141">Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="0e45b-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="0e45b-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0e45b-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="0e45b-143">備份</span><span class="sxs-lookup"><span data-stu-id="0e45b-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="0e45b-144">批次</span><span class="sxs-lookup"><span data-stu-id="0e45b-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="0e45b-145">BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="0e45b-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="0e45b-146">CDN</span><span class="sxs-lookup"><span data-stu-id="0e45b-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="0e45b-147">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0e45b-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="0e45b-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="0e45b-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="0e45b-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="0e45b-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="0e45b-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0e45b-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="0e45b-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e45b-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="0e45b-152">DNS</span><span class="sxs-lookup"><span data-stu-id="0e45b-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="0e45b-153">事件中樞</span><span class="sxs-lookup"><span data-stu-id="0e45b-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="0e45b-154">IoT 中心</span><span class="sxs-lookup"><span data-stu-id="0e45b-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="0e45b-155">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0e45b-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="0e45b-156">Log Analytics / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="0e45b-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="0e45b-157">媒體服務</span><span class="sxs-lookup"><span data-stu-id="0e45b-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="0e45b-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0e45b-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="0e45b-159">行動服務</span><span class="sxs-lookup"><span data-stu-id="0e45b-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="0e45b-160">監視</span><span class="sxs-lookup"><span data-stu-id="0e45b-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="0e45b-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0e45b-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="0e45b-162">網路功能</span><span class="sxs-lookup"><span data-stu-id="0e45b-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="0e45b-163">網路監看員</span><span class="sxs-lookup"><span data-stu-id="0e45b-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="0e45b-164">通知中樞服務</span><span class="sxs-lookup"><span data-stu-id="0e45b-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="0e45b-165">資源群組</span><span class="sxs-lookup"><span data-stu-id="0e45b-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="0e45b-166">排程器</span><span class="sxs-lookup"><span data-stu-id="0e45b-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="0e45b-167">Search</span><span class="sxs-lookup"><span data-stu-id="0e45b-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="0e45b-168">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="0e45b-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="0e45b-169">站台復原</span><span class="sxs-lookup"><span data-stu-id="0e45b-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="0e45b-170">SQL Database</span><span class="sxs-lookup"><span data-stu-id="0e45b-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="0e45b-171">儲存體</span><span class="sxs-lookup"><span data-stu-id="0e45b-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="0e45b-172">StorSimple 系統</span><span class="sxs-lookup"><span data-stu-id="0e45b-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="0e45b-173">串流分析</span><span class="sxs-lookup"><span data-stu-id="0e45b-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="0e45b-174">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0e45b-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="0e45b-175">流量管理員</span><span class="sxs-lookup"><span data-stu-id="0e45b-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="0e45b-176">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0e45b-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="0e45b-177">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="0e45b-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="0e45b-178">訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="0e45b-179">訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="0e45b-180">訂用帳戶限制 - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0e45b-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="0e45b-181">使用 Azure 資源管理員和 Azure 資源群組時，適用下列限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-181">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="0e45b-182">使用 Azure 資源管理員時未變更的限制不會在以下列出。</span><span class="sxs-lookup"><span data-stu-id="0e45b-182">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="0e45b-183">請參閱先前的資料表來瞭解這些限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-183">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="0e45b-184">如需處理限制 Resource Manager 要求的資訊，請參閱[節流 Resource Manager 要求](resource-manager-request-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="0e45b-185">資源群組限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="0e45b-186">虛擬機器限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="0e45b-187">虛擬機器限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="0e45b-188">虛擬機器限制 - Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="0e45b-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="0e45b-189">使用 Azure 資源管理員和 Azure 資源群組時，適用下列限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-189">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="0e45b-190">使用 Azure 資源管理員時未變更的限制不會在以下列出。</span><span class="sxs-lookup"><span data-stu-id="0e45b-190">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="0e45b-191">請參閱先前的資料表來瞭解這些限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-191">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="0e45b-192">虛擬機器擴展集限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="0e45b-193">容器執行個體限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="0e45b-194">網路限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="0e45b-195">網路限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="0e45b-196">應用程式閘道限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="0e45b-197">網路監看員限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="0e45b-198">流量管理員限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="0e45b-199">DNS 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="0e45b-200">儲存體限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-200">Storage limits</span></span>
<span data-ttu-id="0e45b-201">如需儲存體帳戶限制的其他詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage/common/storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="0e45b-202">儲存體服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="0e45b-203">虛擬機器磁碟限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="0e45b-204">如需其他詳細資訊，請參閱 [虛擬機器大小](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="0e45b-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="0e45b-205">受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="0e45b-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="0e45b-206">未受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="0e45b-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="0e45b-207">儲存體資源提供者限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="0e45b-208">雲端服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="0e45b-209">應用程式服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-209">App Service limits</span></span>
<span data-ttu-id="0e45b-210">下列應用程式服務限制包含 Web 應用程式、行動應用程式、API 應用程式和邏輯應用程式的限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-210">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="0e45b-211">排程器限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="0e45b-212">Batch 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="0e45b-213">BizTalk 服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-213">BizTalk Services limits</span></span>
<span data-ttu-id="0e45b-214">下表顯示 Azure Biztalk 服務的限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-214">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="0e45b-215">Azure Cosmos DB 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="0e45b-216">Azure Cosmos DB 是一個全域調整資料庫，可以調整輸送量和儲存體來因應您應用程式的需要。</span><span class="sxs-lookup"><span data-stu-id="0e45b-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="0e45b-217">如果您有關於 Azure Cosmos DB 調整的問題，請傳送電子郵件給 askcosmosdb@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="0e45b-217">If you have any questions about the scale Azure Cosmos DB provides, please send email to askcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="0e45b-218">Mobile Engagement 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="0e45b-219">搜尋限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-219">Search limits</span></span>
<span data-ttu-id="0e45b-220">定價層會決定搜尋服務的容量和限制。</span><span class="sxs-lookup"><span data-stu-id="0e45b-220">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="0e45b-221">層級包括：</span><span class="sxs-lookup"><span data-stu-id="0e45b-221">Tiers include:</span></span>

* <span data-ttu-id="0e45b-222"> 多租用戶服務，與其他 Azure 訂戶共用，適用於評估及小型開發專案。</span><span class="sxs-lookup"><span data-stu-id="0e45b-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="0e45b-223"> 可針對規模較小的生產工作負載提供專用的計算資源，以及針對高可用性的查詢工作負載提供最多 3 個複本。</span><span class="sxs-lookup"><span data-stu-id="0e45b-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="0e45b-224"> 適用於較大型生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="0e45b-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="0e45b-225">標準層內具有多個層級，如此就能讓您選擇最符合工作負載設定檔的資源設定。</span><span class="sxs-lookup"><span data-stu-id="0e45b-225">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="0e45b-226">**每一訂用帳戶的限制**</span><span class="sxs-lookup"><span data-stu-id="0e45b-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="0e45b-227">**每個搜尋服務的限制**</span><span class="sxs-lookup"><span data-stu-id="0e45b-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="0e45b-228">若要深入了解更細微的限制，例如文件大小、每秒的查詢數、金鑰、要求和回應，請參閱 [Azure 搜尋服務的服務限制](search/search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-228">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="0e45b-229">媒體服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="0e45b-230">CDN 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="0e45b-231">行動服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="0e45b-232">監視限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="0e45b-233">通知中樞服務限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="0e45b-234">事件中樞限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="0e45b-235">服務匯流排限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="0e45b-236">IoT 中樞限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="0e45b-237">Data Factory 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="0e45b-238">Data Lake Analytics 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="0e45b-239">Data Lake Store 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="0e45b-240">串流分析限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="0e45b-241">Active Directory 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="0e45b-242">Azure Event Grid 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="0e45b-243">Azure RemoteApp 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="0e45b-244">StorSimple 系統限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="0e45b-245">Log Analytics 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="0e45b-246">備份限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="0e45b-247">Site Recovery 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="0e45b-248">Application Insights 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="0e45b-249">API 管理限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="0e45b-250">Azure Redis 快取限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="0e45b-251">金鑰保存庫限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="0e45b-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0e45b-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="0e45b-253">自動化限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="0e45b-254">SQL Database 限制</span><span class="sxs-lookup"><span data-stu-id="0e45b-254">SQL Database limits</span></span>
<span data-ttu-id="0e45b-255">如需 SQL Database 的限制，請參閱 [SQL Database 資源限制](sql-database/sql-database-resource-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="0e45b-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0e45b-256">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0e45b-256">See also</span></span>
[<span data-ttu-id="0e45b-257">了解 Azure 限制和增加</span><span class="sxs-lookup"><span data-stu-id="0e45b-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="0e45b-258">Azure 的虛擬機器和雲端服務大小</span><span class="sxs-lookup"><span data-stu-id="0e45b-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="0e45b-259">雲端服務的大小</span><span class="sxs-lookup"><span data-stu-id="0e45b-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

