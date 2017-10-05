---
title: "Azure 的堆疊中的配額 |Microsoft 文件"
description: "系統管理員可設定配額以限制租用戶有存取權的資源的最大數量。"
services: azure-stack
documentationcenter: 
author: mattmcg
manager: byronr
editor: 
ms.assetid: 955c6dd8-cefe-42f3-af88-e11d17d22725
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: mattmcg
ms.openlocfilehash: bbefca1a60f38f18838ee6563bd26b934cd02172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a><span data-ttu-id="bb50f-103">設定與檢視 Azure 堆疊中的配額</span><span class="sxs-lookup"><span data-stu-id="bb50f-103">Set and view quotas in Azure Stack</span></span>
<span data-ttu-id="bb50f-104">配額會定義租用戶的訂用帳戶可以佈建或取用之資源的限制。</span><span class="sxs-lookup"><span data-stu-id="bb50f-104">Quotas define the limits of resources that a tenant subscription can provision or consume.</span></span> <span data-ttu-id="bb50f-105">例如，配額可能會讓租用戶，以建立最多五個 Vm。</span><span class="sxs-lookup"><span data-stu-id="bb50f-105">For example, a quota might allow a tenant to create up to five VMs.</span></span> <span data-ttu-id="bb50f-106">若要加入至方案的服務，系統管理員必須設定該服務的配額設定。</span><span class="sxs-lookup"><span data-stu-id="bb50f-106">To add a service to a plan, the administrator must configure the quota settings for that service.</span></span>

<span data-ttu-id="bb50f-107">配額是可設定每個服務，以及每個位置，讓系統管理員提供更精確地控制的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="bb50f-107">Quotas are configurable per service and per location, enabling administrators to provide granular control over the resource consumption.</span></span> <span data-ttu-id="bb50f-108">系統管理員可以建立一或多個配額資源並將它們關聯計劃，這表示它們可提供不同的供應項目對其服務。</span><span class="sxs-lookup"><span data-stu-id="bb50f-108">Administrators can create one or more quota resources and associate them with plans, which means they can provide differentiated offerings for their services.</span></span> <span data-ttu-id="bb50f-109">指定服務的配額可以從建立**資源提供者**管理刀鋒視窗，該服務。</span><span class="sxs-lookup"><span data-stu-id="bb50f-109">Quotas for a given service can be created from the **Resource Provider** administration blade for that service.</span></span>

<span data-ttu-id="bb50f-110">租用戶訂閱方案包含多個計劃可以使用每個計劃中可用的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bb50f-110">A tenant that subscribes to an offer that contains multiple plans can use all resources that are available in each plan.</span></span>

## <a name="to-create-an-iaas-quota"></a><span data-ttu-id="bb50f-111">若要建立的 IaaS 配額</span><span class="sxs-lookup"><span data-stu-id="bb50f-111">To create an IaaS quota</span></span>
1. <span data-ttu-id="bb50f-112">在瀏覽器，移至[https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/)。</span><span class="sxs-lookup"><span data-stu-id="bb50f-112">In a browser, go to [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).</span></span>
   
   <span data-ttu-id="bb50f-113">Azure 堆疊入口網站管理員身分登入 （透過使用您在部署期間所提供的認證）。</span><span class="sxs-lookup"><span data-stu-id="bb50f-113">Sign in to the Azure Stack portal as an administrator (by using the credentials that you provided during deployment).</span></span>
2. <span data-ttu-id="bb50f-114">選取**新增**，然後**租用戶提供 + 計劃**，然後選取**配額**。</span><span class="sxs-lookup"><span data-stu-id="bb50f-114">Select **New**, then **Tenant Offers + Plans**, and select **Quota**.</span></span>
3. <span data-ttu-id="bb50f-115">選取您要建立配額的第一個服務。</span><span class="sxs-lookup"><span data-stu-id="bb50f-115">Select the first service for which you want to create a quota.</span></span> <span data-ttu-id="bb50f-116">針對 IaaS 配額，請針對計算、網路與儲存體服務依照這些步驟執行。</span><span class="sxs-lookup"><span data-stu-id="bb50f-116">For an IaaS quota, follow these steps for the Compute, Network, and Storage services.</span></span>
   <span data-ttu-id="bb50f-117">在此範例中，我們先為計算服務建立配額。</span><span class="sxs-lookup"><span data-stu-id="bb50f-117">In this example, we first create a quota for the Compute service.</span></span> <span data-ttu-id="bb50f-118">在**命名空間**清單中，選取**Microsoft.Compute**命名空間。</span><span class="sxs-lookup"><span data-stu-id="bb50f-118">In the **Namespace** list, select the **Microsoft.Compute** namespace.</span></span>
   
   > ![建立新的計算配額](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. <span data-ttu-id="bb50f-120">選擇配額 （例如，'local'） 的定義所在的位置。</span><span class="sxs-lookup"><span data-stu-id="bb50f-120">Choose the location where the quota is defined (for example, 'local').</span></span>
5. <span data-ttu-id="bb50f-121">在**配額設定**項目，該處會指示**設定容量配額**。</span><span class="sxs-lookup"><span data-stu-id="bb50f-121">On the **Quota Settings** item, it says **Set the Capacity of Quota**.</span></span> <span data-ttu-id="bb50f-122">按一下此項目可設定配額設定。</span><span class="sxs-lookup"><span data-stu-id="bb50f-122">Click this item to configure the quota settings.</span></span>
6. <span data-ttu-id="bb50f-123">在**設定配額**刀鋒視窗中，您會看到所有您可以設定限制的計算資源。</span><span class="sxs-lookup"><span data-stu-id="bb50f-123">On the **Set Quotas** blade, you see all the Compute resources for which you can configure limits.</span></span> <span data-ttu-id="bb50f-124">每個類型都有與它相關聯的預設值。</span><span class="sxs-lookup"><span data-stu-id="bb50f-124">Each type has a default value that's associated with it.</span></span> <span data-ttu-id="bb50f-125">您可以變更這些值，或者您可以選取**確定**接受預設值 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb50f-125">You can change these values or you can select the **Ok** button at the bottom of the blade to accept the defaults.</span></span>
   
   > ![設定計算配額](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. <span data-ttu-id="bb50f-127">您已設定的值，並按下之後**確定**、**配額設定**項目顯示為**設定**。</span><span class="sxs-lookup"><span data-stu-id="bb50f-127">After you have configured the values and clicked **Ok**, the **Quota Settings** item appears as **Configured**.</span></span> <span data-ttu-id="bb50f-128">按一下**確定**建立**配額**資源。</span><span class="sxs-lookup"><span data-stu-id="bb50f-128">Click **Ok** to create the **Quota** resource.</span></span>
   
   <span data-ttu-id="bb50f-129">您應該會看到通知，指出正在建立配額資源。</span><span class="sxs-lookup"><span data-stu-id="bb50f-129">You should see a notification indicating that the quota resource is being created.</span></span>
8. <span data-ttu-id="bb50f-130">已成功建立的配額集之後，您會收到第二個通知。</span><span class="sxs-lookup"><span data-stu-id="bb50f-130">After the quota set has been successfully created, you receive a second notification.</span></span> <span data-ttu-id="bb50f-131">計算服務配額現在已準備好要與方案產生關聯。</span><span class="sxs-lookup"><span data-stu-id="bb50f-131">The Compute service quota is now ready to be associated with a plan.</span></span> <span data-ttu-id="bb50f-132">重複上述步驟與 網路和儲存體服務，您準備好要建立的 IaaS 方案 ！</span><span class="sxs-lookup"><span data-stu-id="bb50f-132">Repeat these steps with the Network and Storage services, and you are ready to create an IaaS plan!</span></span>
   
   > ![配額建立成功時的通知](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a><span data-ttu-id="bb50f-134">計算配額類型</span><span class="sxs-lookup"><span data-stu-id="bb50f-134">Compute quota types</span></span>
| <span data-ttu-id="bb50f-135">**類型**</span><span class="sxs-lookup"><span data-stu-id="bb50f-135">**Type**</span></span> | <span data-ttu-id="bb50f-136">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bb50f-136">**Default value**</span></span> | <span data-ttu-id="bb50f-137">**說明**</span><span class="sxs-lookup"><span data-stu-id="bb50f-137">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb50f-138">虛擬機器的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-138">Max number of virtual machines</span></span> |<span data-ttu-id="bb50f-139">50</span><span class="sxs-lookup"><span data-stu-id="bb50f-139">50</span></span> |<span data-ttu-id="bb50f-140">訂用帳戶可以在這個位置建立的虛擬機器數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-140">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-141">虛擬機器核心的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-141">Max number of virtual machine cores</span></span> |<span data-ttu-id="bb50f-142">100</span><span class="sxs-lookup"><span data-stu-id="bb50f-142">100</span></span> |<span data-ttu-id="bb50f-143">訂用帳戶可以在這個位置建立的核心數目上限 (例如，A3 VM 有四個核心)。</span><span class="sxs-lookup"><span data-stu-id="bb50f-143">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="bb50f-144">虛擬機器記憶體 (GB) 的最大數量</span><span class="sxs-lookup"><span data-stu-id="bb50f-144">Max amount of virtual machine memory (GB)</span></span> |<span data-ttu-id="bb50f-145">150</span><span class="sxs-lookup"><span data-stu-id="bb50f-145">150</span></span> |<span data-ttu-id="bb50f-146">RAM 可佈建以 mb 為單位的最大數量 （例如，A1 VM 使用 1.75 GB 記憶體）。</span><span class="sxs-lookup"><span data-stu-id="bb50f-146">The maximum amount of RAM that can be provisioned in megabytes (for example, an A1 VM consumes 1.75 GB of RAM).</span></span> |

> [!NOTE]
> <span data-ttu-id="bb50f-147">此 Technical Preview 中未限制計算配額。</span><span class="sxs-lookup"><span data-stu-id="bb50f-147">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="bb50f-148">儲存體配額類型</span><span class="sxs-lookup"><span data-stu-id="bb50f-148">Storage quota types</span></span>
| <span data-ttu-id="bb50f-149">**Item**</span><span class="sxs-lookup"><span data-stu-id="bb50f-149">**Item**</span></span> | <span data-ttu-id="bb50f-150">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bb50f-150">**Default value**</span></span> | <span data-ttu-id="bb50f-151">**說明**</span><span class="sxs-lookup"><span data-stu-id="bb50f-151">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb50f-152">最大容量 (GB)</span><span class="sxs-lookup"><span data-stu-id="bb50f-152">Maximum capacity (GB)</span></span> |<span data-ttu-id="bb50f-153">500</span><span class="sxs-lookup"><span data-stu-id="bb50f-153">500</span></span> |<span data-ttu-id="bb50f-154">訂用帳戶可以在這個位置取用的總儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="bb50f-154">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="bb50f-155">儲存體帳戶的總數</span><span class="sxs-lookup"><span data-stu-id="bb50f-155">Total number of storage accounts</span></span> |<span data-ttu-id="bb50f-156">20</span><span class="sxs-lookup"><span data-stu-id="bb50f-156">20</span></span> |<span data-ttu-id="bb50f-157">訂用帳戶可以在這個位置建立的儲存體帳戶數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-157">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="bb50f-158">網路配額類型</span><span class="sxs-lookup"><span data-stu-id="bb50f-158">Network quota types</span></span>
| <span data-ttu-id="bb50f-159">**Item**</span><span class="sxs-lookup"><span data-stu-id="bb50f-159">**Item**</span></span> | <span data-ttu-id="bb50f-160">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bb50f-160">**Default value**</span></span> | <span data-ttu-id="bb50f-161">**說明**</span><span class="sxs-lookup"><span data-stu-id="bb50f-161">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb50f-162">公用 IP 的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-162">Max public IPs</span></span> |<span data-ttu-id="bb50f-163">50</span><span class="sxs-lookup"><span data-stu-id="bb50f-163">50</span></span> |<span data-ttu-id="bb50f-164">訂用帳戶可以在這個位置建立的公用 IP 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-164">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-165">虛擬網路的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-165">Max virtual networks</span></span> |<span data-ttu-id="bb50f-166">50</span><span class="sxs-lookup"><span data-stu-id="bb50f-166">50</span></span> |<span data-ttu-id="bb50f-167">訂用帳戶可以在這個位置建立的虛擬網路數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-167">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-168">虛擬網路閘道的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-168">Max virtual network gateways</span></span> |<span data-ttu-id="bb50f-169">1</span><span class="sxs-lookup"><span data-stu-id="bb50f-169">1</span></span> |<span data-ttu-id="bb50f-170">訂用帳戶可以在這個位置建立的虛擬網路閘道 (VPN 閘道) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-170">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-171">網路連線的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-171">Max network connections</span></span> |<span data-ttu-id="bb50f-172">2</span><span class="sxs-lookup"><span data-stu-id="bb50f-172">2</span></span> |<span data-ttu-id="bb50f-173">訂用帳戶可以在這個位置所有虛擬網路閘道上建立的網路連線 (點對點或站台對站台) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-173">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="bb50f-174">負載平衡器的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-174">Max load balancers</span></span> |<span data-ttu-id="bb50f-175">50</span><span class="sxs-lookup"><span data-stu-id="bb50f-175">50</span></span> |<span data-ttu-id="bb50f-176">訂用帳戶可以在這個位置建立的負載平衡器數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-176">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-177">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="bb50f-177">Max NICs</span></span> |<span data-ttu-id="bb50f-178">100</span><span class="sxs-lookup"><span data-stu-id="bb50f-178">100</span></span> |<span data-ttu-id="bb50f-179">訂用帳戶可以在這個位置建立的網路介面數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-179">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bb50f-180">網路安全性群組的數目上限</span><span class="sxs-lookup"><span data-stu-id="bb50f-180">Max network security groups</span></span> |<span data-ttu-id="bb50f-181">50</span><span class="sxs-lookup"><span data-stu-id="bb50f-181">50</span></span> |<span data-ttu-id="bb50f-182">訂用帳戶可以在這個位置建立的網路安全性群組數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb50f-182">The maximum number of network security groups that a subscription can create in this location.</span></span> |

##<a name="view-an-existing-quota"></a><span data-ttu-id="bb50f-183">檢視現有的配額</span><span class="sxs-lookup"><span data-stu-id="bb50f-183">View an existing quota</span></span>
<span data-ttu-id="bb50f-184">若要檢視現有的配額，請按一下**更多服務**>**資源提供者**和選取與您想要檢視的配額相關聯的服務。</span><span class="sxs-lookup"><span data-stu-id="bb50f-184">To view an existing quota, click **More services**>**Resource Providers** and select the service with which the quota you want to view is associated.</span></span> <span data-ttu-id="bb50f-185">接下來，按一下**配額**，然後選取您想要檢視的配額。</span><span class="sxs-lookup"><span data-stu-id="bb50f-185">Next, click **Quotas**, and select the Quota you want to view.</span></span>
   > ![檢視現有的配額](./media/azure-stack-setting-quota/ExistingQuota.PNG)
