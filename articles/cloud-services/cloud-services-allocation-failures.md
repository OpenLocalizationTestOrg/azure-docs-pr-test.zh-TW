---
title: "針對雲端服務配置失敗進行疑難排解 | Microsoft Docs"
description: "疑難排解在 Azure 中部署雲端服務時發生的配置失敗"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 3379b6d9bea874abecae7e56d30cfb15e6b0c2fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a><span data-ttu-id="d2181-103">疑難排解在 Azure 中部署雲端服務時發生的配置失敗</span><span class="sxs-lookup"><span data-stu-id="d2181-103">Troubleshooting allocation failure when you deploy Cloud Services in Azure</span></span>
## <a name="summary"></a><span data-ttu-id="d2181-104">摘要</span><span class="sxs-lookup"><span data-stu-id="d2181-104">Summary</span></span>
<span data-ttu-id="d2181-105">當您部署執行個體至雲端服務或加入新的 Web 或背景工作角色執行個體時，Microsoft Azure 會配置計算資源。</span><span class="sxs-lookup"><span data-stu-id="d2181-105">When you deploy instances to a Cloud Service or add new web or worker role instances, Microsoft Azure allocates compute resources.</span></span> <span data-ttu-id="d2181-106">執行這些作業時，即使尚未達到 Azure 訂用帳戶限制，也可能偶爾發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d2181-106">You may occasionally receive errors when performing these operations even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="d2181-107">本文說明一些常見配置失敗的原因，並建議可能的補救方法。</span><span class="sxs-lookup"><span data-stu-id="d2181-107">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="d2181-108">規劃服務的部署時，本資訊可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="d2181-108">The information may also be useful when you plan the deployment of your services.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a><span data-ttu-id="d2181-109">背景 – 配置的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2181-109">Background – How allocation works</span></span>
<span data-ttu-id="d2181-110">Azure 資料中心的伺服器分割成叢集。</span><span class="sxs-lookup"><span data-stu-id="d2181-110">The servers in Azure datacenters are partitioned into clusters.</span></span> <span data-ttu-id="d2181-111">在多個叢集中嘗試新的雲端服務配置要求。</span><span class="sxs-lookup"><span data-stu-id="d2181-111">A new cloud service allocation request is attempted in multiple clusters.</span></span> <span data-ttu-id="d2181-112">當第一個執行個體部署至雲端服務 (在預備或生產環境) 後，該雲端服務會釘選至某個叢集。</span><span class="sxs-lookup"><span data-stu-id="d2181-112">When the first instance is deployed to a cloud service(in either staging or production), that cloud service gets pinned to a cluster.</span></span> <span data-ttu-id="d2181-113">雲端服務的任何進一步的部署會發生在相同的叢集中。</span><span class="sxs-lookup"><span data-stu-id="d2181-113">Any further deployments for the cloud service will happen in the same cluster.</span></span> <span data-ttu-id="d2181-114">在本文中，這種情況稱為「釘選到叢集」。</span><span class="sxs-lookup"><span data-stu-id="d2181-114">In this article, we'll refer to this as "pinned to a cluster".</span></span> <span data-ttu-id="d2181-115">下圖 1 說明在多個叢集中嘗試一般配置的情況。圖 2 說明釘選到叢集 2 來配置的情況，因為現有的雲端服務 CS_1 裝載於此處。</span><span class="sxs-lookup"><span data-stu-id="d2181-115">Diagram 1 below illustrates the case of a normal allocation which is attempted in multiple clusters; Diagram 2 illustrates the case of an allocation that's pinned to Cluster 2 because that's where the existing Cloud Service CS_1 is hosted.</span></span>

![配置圖表](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a><span data-ttu-id="d2181-117">配置失敗的原因</span><span class="sxs-lookup"><span data-stu-id="d2181-117">Why allocation failure happens</span></span>
<span data-ttu-id="d2181-118">當配置要求已釘選到叢集時，由於可用的資源集區僅限於某個叢集，很可能找不到可用的資源。</span><span class="sxs-lookup"><span data-stu-id="d2181-118">When an allocation request is pinned to a cluster, there's a higher chance of failing to find free resources since the available resource pool is limited to a cluster.</span></span> <span data-ttu-id="d2181-119">此外，如果配置要求已釘選到叢集，但該叢集不支援您所要求的資源類型，即使叢集有可用的資源，您的要求仍會失敗。</span><span class="sxs-lookup"><span data-stu-id="d2181-119">Furthermore, if your allocation request is pinned to a cluster but the type of resource you requested is not supported by that cluster, your request will fail even if the cluster has free resource.</span></span> <span data-ttu-id="d2181-120">下圖 3 說明由於唯一候選叢集沒有可用的資源，導致已釘選的配置失敗的情況。</span><span class="sxs-lookup"><span data-stu-id="d2181-120">Diagram 3 below illustrates the case where a pinned allocation fails because the only candidate cluster does not have free resources.</span></span> <span data-ttu-id="d2181-121">圖 4 說明因唯一候選叢集不支援所要求的 VM 大小 (雖然叢集有可用的資源)，而導致已釘選的配置失敗的情況。</span><span class="sxs-lookup"><span data-stu-id="d2181-121">Diagram 4 illustrates the case where a pinned allocation fails because the only candidate cluster does not support the requested VM size, even though the cluster has free resources.</span></span>

![釘選配置失敗](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a><span data-ttu-id="d2181-123">雲端服務配置失敗的疑難排解</span><span class="sxs-lookup"><span data-stu-id="d2181-123">Troubleshooting allocation failure for cloud services</span></span>
### <a name="error-message"></a><span data-ttu-id="d2181-124">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d2181-124">Error Message</span></span>
<span data-ttu-id="d2181-125">您可能會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="d2181-125">You may see the following error message:</span></span>

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable to satisfy constraints in request. The requested new service deployment is bound to an Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains the new deployment to specific Azure resources. Please retry later or try reducing the VM size or number of role instances. Alternatively, if possible, remove the aforementioned constraints or try deploying to a different region."

### <a name="common-issues"></a><span data-ttu-id="d2181-126">常見問題</span><span class="sxs-lookup"><span data-stu-id="d2181-126">Common Issues</span></span>
<span data-ttu-id="d2181-127">以下是造成配置要求釘選到單一叢集的常見配置案例。</span><span class="sxs-lookup"><span data-stu-id="d2181-127">Here are the common allocation scenarios that cause an allocation request to be pinned to a single cluster.</span></span>

* <span data-ttu-id="d2181-128">部署至預備位置 - 如果某個雲端服務在任一位置含有部署，則整個雲端服務都會釘選到特定的叢集。</span><span class="sxs-lookup"><span data-stu-id="d2181-128">Deploying to Staging Slot - If a cloud service has a deployment in either slot, then the entire cloud service is pinned to a specific cluster.</span></span>  <span data-ttu-id="d2181-129">這表示如果某個部署已存在生產位置，則新的預備部署只能配置在與生產位置相同的叢集中。</span><span class="sxs-lookup"><span data-stu-id="d2181-129">This means that if a deployment already exists in the production slot, then a new staging deployment can only be allocated in the same cluster as the production slot.</span></span> <span data-ttu-id="d2181-130">如果叢集逼近容量上限，則要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="d2181-130">If the cluster is nearing capacity, the request may fail.</span></span>
* <span data-ttu-id="d2181-131">調整 - 將新的執行個體加入現有的雲端服務必須配置到相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="d2181-131">Scaling - Adding new instances to an existing cloud service must allocate in the same cluster.</span></span>  <span data-ttu-id="d2181-132">小型的調整要求通常可配置，但並不盡然。</span><span class="sxs-lookup"><span data-stu-id="d2181-132">Small scaling requests can usually be allocated, but not always.</span></span> <span data-ttu-id="d2181-133">如果叢集逼近容量上限，則要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="d2181-133">If the cluster is nearing capacity, the request may fail.</span></span>
* <span data-ttu-id="d2181-134">同質群組 - 部署到空的雲端服務的新部署可經由該區域中任一叢集的網狀架構配置，除非雲端服務已釘選到某個同質群組。</span><span class="sxs-lookup"><span data-stu-id="d2181-134">Affinity Group - A new deployment to an empty cloud service can be allocated by the fabric in any cluster in that region, unless the cloud service is pinned to an affinity group.</span></span> <span data-ttu-id="d2181-135">將在相同的叢集中嘗試部署到相同的同質群組。</span><span class="sxs-lookup"><span data-stu-id="d2181-135">Deployments to the same affinity group will be attempted on the same cluster.</span></span> <span data-ttu-id="d2181-136">如果叢集逼近容量上限，則要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="d2181-136">If the cluster is nearing capacity, the request may fail.</span></span>
* <span data-ttu-id="d2181-137">同質群組 vNet - 較舊的虛擬網路是繫結至同質群組而不是區域，而這些虛擬網路中的雲端服務會釘選到該同質群組叢集。</span><span class="sxs-lookup"><span data-stu-id="d2181-137">Affinity Group vNet - Older Virtual Networks were tied to affinity groups instead of regions, and cloud services in these Virtual Networks would be pinned to the affinity group cluster.</span></span> <span data-ttu-id="d2181-138">將在釘選的叢集中嘗試部署到這種類型的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d2181-138">Deployments to this type of virtual network will be attempted on the pinned cluster.</span></span> <span data-ttu-id="d2181-139">如果叢集逼近容量上限，則要求可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="d2181-139">If the cluster is nearing capacity, the request may fail.</span></span>

## <a name="solutions"></a><span data-ttu-id="d2181-140">解決方案</span><span class="sxs-lookup"><span data-stu-id="d2181-140">Solutions</span></span>
1. <span data-ttu-id="d2181-141">重新部署到新的雲端服務 - 此解決方案可能是最成功的，因為它可讓平台從該區域的所有叢集中選擇。</span><span class="sxs-lookup"><span data-stu-id="d2181-141">Redeploy to a new cloud service - This solution is likely to be most successful as it allows the platform to choose from all clusters in that region.</span></span>

   * <span data-ttu-id="d2181-142">將工作負載部署到新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="d2181-142">Deploy the workload to a new cloud service</span></span>  
   * <span data-ttu-id="d2181-143">更新 CNAME 或 A 記錄，以將流量指向新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="d2181-143">Update the CNAME or A record to point traffic to the new cloud service</span></span>
   * <span data-ttu-id="d2181-144">一旦流向舊網站的流量為零，您就可以刪除舊的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d2181-144">Once zero traffic is going to the old site, you can delete the old cloud service.</span></span> <span data-ttu-id="d2181-145">此解決方案不需要停機。</span><span class="sxs-lookup"><span data-stu-id="d2181-145">This solution should incur zero downtime.</span></span>
2. <span data-ttu-id="d2181-146">刪除生產和預備位置 - 這個解決方案將會保留現有的 DNS 名稱，但會造成您的應用程式的停機時間。</span><span class="sxs-lookup"><span data-stu-id="d2181-146">Delete both production and staging slots - This solution will preserve your existing DNS name, but will cause downtime to your application.</span></span>

   * <span data-ttu-id="d2181-147">刪除現有雲端服務的生產和預備位置，讓雲端服務是空白的，然後</span><span class="sxs-lookup"><span data-stu-id="d2181-147">Delete the production and staging slots of an existing cloud service so that the cloud service is empty, and then</span></span>
   * <span data-ttu-id="d2181-148">在現有的雲端服務中建立新的部署。</span><span class="sxs-lookup"><span data-stu-id="d2181-148">Create a new deployment in the existing cloud service.</span></span> <span data-ttu-id="d2181-149">這會重新嘗試在區域中的所有叢集上配置。</span><span class="sxs-lookup"><span data-stu-id="d2181-149">This will re-attempt to allocation on all clusters in the region.</span></span> <span data-ttu-id="d2181-150">請確定雲端服務未繫結至同質群組。</span><span class="sxs-lookup"><span data-stu-id="d2181-150">Ensure the cloud service is not tied to an affinity group.</span></span>
3. <span data-ttu-id="d2181-151">保留的 IP - 此方案將會保留現有的 IP 位址，但是會導致您的應用程式停止運作。</span><span class="sxs-lookup"><span data-stu-id="d2181-151">Reserved IP -  This solution will preserve your existing IP address, but will cause downtime to your application.</span></span>  

   * <span data-ttu-id="d2181-152">使用 Powershell 為您現有的部署建立 ReservedIP</span><span class="sxs-lookup"><span data-stu-id="d2181-152">Create a ReservedIP for your existing deployment using Powershell</span></span>

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * <span data-ttu-id="d2181-153">請遵循上述的 #2，務必在服務的 CSCFG 中指定新 ReservedIP。</span><span class="sxs-lookup"><span data-stu-id="d2181-153">Follow #2 from above, making sure to specify the new ReservedIP in the service's CSCFG.</span></span>
4. <span data-ttu-id="d2181-154">移除新部署中的同質群組 - 不再建議使用同質群組。</span><span class="sxs-lookup"><span data-stu-id="d2181-154">Remove affinity group for new deployments - Affinity Groups are no longer recommended.</span></span> <span data-ttu-id="d2181-155">請遵循上述 #1 的步驟以部署新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d2181-155">Follow steps for #1 above to deploy a new cloud service.</span></span> <span data-ttu-id="d2181-156">請確定雲端服務不在同質群組中。</span><span class="sxs-lookup"><span data-stu-id="d2181-156">Ensure cloud service is not in an affinity group.</span></span>
5. <span data-ttu-id="d2181-157">轉換至區域虛擬網路 - 請參閱 [如何從同質群組移轉至區域虛擬網路 (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d2181-157">Convert to a Regional Virtual Network - See [How to migrate from Affinity Groups to a Regional Virtual Network (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
