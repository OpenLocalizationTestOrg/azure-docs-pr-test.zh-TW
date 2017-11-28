---
title: "在 Azure 堆疊 aaaQuotas |Microsoft 文件"
description: "系統管理員設定租用戶有存取權的資源的配額 toorestrict hello 最大的數量。"
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
ms.openlocfilehash: 9770802960af102a6d497b47d95cd6ec63ce219c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a><span data-ttu-id="d39b1-103">設定與檢視 Azure 堆疊中的配額</span><span class="sxs-lookup"><span data-stu-id="d39b1-103">Set and view quotas in Azure Stack</span></span>
<span data-ttu-id="d39b1-104">配額會定義租用戶的訂用帳戶可以佈建或取用之資源的 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="d39b1-104">Quotas define hello limits of resources that a tenant subscription can provision or consume.</span></span> <span data-ttu-id="d39b1-105">例如，配額可能會讓 toofive Vm 上建立租用戶。</span><span class="sxs-lookup"><span data-stu-id="d39b1-105">For example, a quota might allow a tenant to create up toofive VMs.</span></span> <span data-ttu-id="d39b1-106">tooadd 服務 tooa 計劃，系統管理員必須設定該服務的 hello 配額設定。</span><span class="sxs-lookup"><span data-stu-id="d39b1-106">tooadd a service tooa plan, the administrator must configure hello quota settings for that service.</span></span>

<span data-ttu-id="d39b1-107">配額是可設定每個服務，以及每個位置，讓系統管理員 tooprovide 更精確地控制 hello 資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="d39b1-107">Quotas are configurable per service and per location, enabling administrators tooprovide granular control over hello resource consumption.</span></span> <span data-ttu-id="d39b1-108">系統管理員可以建立一或多個配額資源並將它們關聯計劃，這表示它們可提供不同的供應項目對其服務。</span><span class="sxs-lookup"><span data-stu-id="d39b1-108">Administrators can create one or more quota resources and associate them with plans, which means they can provide differentiated offerings for their services.</span></span> <span data-ttu-id="d39b1-109">指定服務的配額可以建立從 hello**資源提供者**管理刀鋒視窗，該服務。</span><span class="sxs-lookup"><span data-stu-id="d39b1-109">Quotas for a given service can be created from hello **Resource Provider** administration blade for that service.</span></span>

<span data-ttu-id="d39b1-110">訂閱 tooan 供應項目，其中包含多個計劃的租用戶可以使用每個計劃中可用的所有資源。</span><span class="sxs-lookup"><span data-stu-id="d39b1-110">A tenant that subscribes tooan offer that contains multiple plans can use all resources that are available in each plan.</span></span>

## <a name="toocreate-an-iaas-quota"></a><span data-ttu-id="d39b1-111">toocreate IaaS 配額</span><span class="sxs-lookup"><span data-stu-id="d39b1-111">toocreate an IaaS quota</span></span>
1. <span data-ttu-id="d39b1-112">在瀏覽器，移至[https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/)。</span><span class="sxs-lookup"><span data-stu-id="d39b1-112">In a browser, go to [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).</span></span>
   
   <span data-ttu-id="d39b1-113">Toohello 堆疊 Azure 入口網站管理員身分登入 （透過使用您在部署期間所提供的 hello 認證）。</span><span class="sxs-lookup"><span data-stu-id="d39b1-113">Sign in toohello Azure Stack portal as an administrator (by using hello credentials that you provided during deployment).</span></span>
2. <span data-ttu-id="d39b1-114">選取**新增**，然後**租用戶提供 + 計劃**，然後選取**配額**。</span><span class="sxs-lookup"><span data-stu-id="d39b1-114">Select **New**, then **Tenant Offers + Plans**, and select **Quota**.</span></span>
3. <span data-ttu-id="d39b1-115">選取您想要的 toocreate 配額 hello 第一個服務。</span><span class="sxs-lookup"><span data-stu-id="d39b1-115">Select hello first service for which you want toocreate a quota.</span></span> <span data-ttu-id="d39b1-116">IaaS 配額，請遵循下列步驟 hello 運算、 網路和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="d39b1-116">For an IaaS quota, follow these steps for hello Compute, Network, and Storage services.</span></span>
   <span data-ttu-id="d39b1-117">在此範例中，我們會先建立 hello 計算服務的配額。</span><span class="sxs-lookup"><span data-stu-id="d39b1-117">In this example, we first create a quota for hello Compute service.</span></span> <span data-ttu-id="d39b1-118">在 hello**命名空間**清單中，選取 hello **Microsoft.Compute**命名空間。</span><span class="sxs-lookup"><span data-stu-id="d39b1-118">In hello **Namespace** list, select hello **Microsoft.Compute** namespace.</span></span>
   
   > ![建立新的計算配額](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. <span data-ttu-id="d39b1-120">選擇 hello hello 配額 （例如，'local'） 的定義所在的位置。</span><span class="sxs-lookup"><span data-stu-id="d39b1-120">Choose hello location where hello quota is defined (for example, 'local').</span></span>
5. <span data-ttu-id="d39b1-121">在 hello**配額設定**項目，該處會指示**設定容量配額**。</span><span class="sxs-lookup"><span data-stu-id="d39b1-121">On hello **Quota Settings** item, it says **Set the Capacity of Quota**.</span></span> <span data-ttu-id="d39b1-122">按一下此項目 tooconfigure hello 配額設定。</span><span class="sxs-lookup"><span data-stu-id="d39b1-122">Click this item tooconfigure hello quota settings.</span></span>
6. <span data-ttu-id="d39b1-123">在 hello**設定配額**刀鋒視窗中，您會看到所有的 hello 計算資源，您可以設定限制。</span><span class="sxs-lookup"><span data-stu-id="d39b1-123">On hello **Set Quotas** blade, you see all hello Compute resources for which you can configure limits.</span></span> <span data-ttu-id="d39b1-124">每個類型都有與它相關聯的預設值。</span><span class="sxs-lookup"><span data-stu-id="d39b1-124">Each type has a default value that's associated with it.</span></span> <span data-ttu-id="d39b1-125">您可以變更這些值，或者您可以選取 hello**確定**底部 hello hello 刀鋒視窗 tooaccept hello 預設值 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d39b1-125">You can change these values or you can select hello **Ok** button at hello bottom of hello blade tooaccept hello defaults.</span></span>
   
   > ![設定計算配額](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. <span data-ttu-id="d39b1-127">您已設定的 hello 值並按下之後**確定**，hello**配額設定**項目顯示為**設定**。</span><span class="sxs-lookup"><span data-stu-id="d39b1-127">After you have configured hello values and clicked **Ok**, hello **Quota Settings** item appears as **Configured**.</span></span> <span data-ttu-id="d39b1-128">按一下**確定**建立 hello**配額**資源。</span><span class="sxs-lookup"><span data-stu-id="d39b1-128">Click **Ok** to create hello **Quota** resource.</span></span>
   
   <span data-ttu-id="d39b1-129">您應該會看到通知，指出正在建立 hello 配額資源。</span><span class="sxs-lookup"><span data-stu-id="d39b1-129">You should see a notification indicating that hello quota resource is being created.</span></span>
8. <span data-ttu-id="d39b1-130">已成功建立 hello 配額集之後，您會收到第二個通知。</span><span class="sxs-lookup"><span data-stu-id="d39b1-130">After hello quota set has been successfully created, you receive a second notification.</span></span> <span data-ttu-id="d39b1-131">準備好 toobe 與方案關聯的現在 hello 計算服務配額。</span><span class="sxs-lookup"><span data-stu-id="d39b1-131">hello Compute service quota is now ready toobe associated with a plan.</span></span> <span data-ttu-id="d39b1-132">重複這些步驟以 hello 網路和儲存體服務，而且您準備好 toocreate IaaS 方案 ！</span><span class="sxs-lookup"><span data-stu-id="d39b1-132">Repeat these steps with hello Network and Storage services, and you are ready toocreate an IaaS plan!</span></span>
   
   > ![配額建立成功時的通知](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a><span data-ttu-id="d39b1-134">計算配額類型</span><span class="sxs-lookup"><span data-stu-id="d39b1-134">Compute quota types</span></span>
| <span data-ttu-id="d39b1-135">**類型**</span><span class="sxs-lookup"><span data-stu-id="d39b1-135">**Type**</span></span> | <span data-ttu-id="d39b1-136">**預設值**</span><span class="sxs-lookup"><span data-stu-id="d39b1-136">**Default value**</span></span> | <span data-ttu-id="d39b1-137">**說明**</span><span class="sxs-lookup"><span data-stu-id="d39b1-137">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d39b1-138">虛擬機器的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-138">Max number of virtual machines</span></span> |<span data-ttu-id="d39b1-139">50</span><span class="sxs-lookup"><span data-stu-id="d39b1-139">50</span></span> |<span data-ttu-id="d39b1-140">hello 訂用帳戶可以在這個位置中建立的虛擬機器的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-140">hello maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-141">虛擬機器核心的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-141">Max number of virtual machine cores</span></span> |<span data-ttu-id="d39b1-142">100</span><span class="sxs-lookup"><span data-stu-id="d39b1-142">100</span></span> |<span data-ttu-id="d39b1-143">hello 的訂用帳戶可以在這個位置中建立的核心數目上限 （例如，A3 VM 有四個核心）。</span><span class="sxs-lookup"><span data-stu-id="d39b1-143">hello maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="d39b1-144">虛擬機器記憶體 (GB) 的最大數量</span><span class="sxs-lookup"><span data-stu-id="d39b1-144">Max amount of virtual machine memory (GB)</span></span> |<span data-ttu-id="d39b1-145">150</span><span class="sxs-lookup"><span data-stu-id="d39b1-145">150</span></span> |<span data-ttu-id="d39b1-146">hello 可以佈建，以 mb 為單位的 RAM 數量最大值 （例如，A1 VM 使用 1.75 GB 記憶體）。</span><span class="sxs-lookup"><span data-stu-id="d39b1-146">hello maximum amount of RAM that can be provisioned in megabytes (for example, an A1 VM consumes 1.75 GB of RAM).</span></span> |

> [!NOTE]
> <span data-ttu-id="d39b1-147">此 Technical Preview 中未限制計算配額。</span><span class="sxs-lookup"><span data-stu-id="d39b1-147">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="d39b1-148">儲存體配額類型</span><span class="sxs-lookup"><span data-stu-id="d39b1-148">Storage quota types</span></span>
| <span data-ttu-id="d39b1-149">**Item**</span><span class="sxs-lookup"><span data-stu-id="d39b1-149">**Item**</span></span> | <span data-ttu-id="d39b1-150">**預設值**</span><span class="sxs-lookup"><span data-stu-id="d39b1-150">**Default value**</span></span> | <span data-ttu-id="d39b1-151">**說明**</span><span class="sxs-lookup"><span data-stu-id="d39b1-151">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d39b1-152">最大容量 (GB)</span><span class="sxs-lookup"><span data-stu-id="d39b1-152">Maximum capacity (GB)</span></span> |<span data-ttu-id="d39b1-153">500</span><span class="sxs-lookup"><span data-stu-id="d39b1-153">500</span></span> |<span data-ttu-id="d39b1-154">訂用帳戶可以在這個位置取用的總儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="d39b1-154">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="d39b1-155">儲存體帳戶的總數</span><span class="sxs-lookup"><span data-stu-id="d39b1-155">Total number of storage accounts</span></span> |<span data-ttu-id="d39b1-156">20</span><span class="sxs-lookup"><span data-stu-id="d39b1-156">20</span></span> |<span data-ttu-id="d39b1-157">hello 的訂用帳戶可以在這個位置中建立的儲存體帳戶數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-157">hello maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="d39b1-158">網路配額類型</span><span class="sxs-lookup"><span data-stu-id="d39b1-158">Network quota types</span></span>
| <span data-ttu-id="d39b1-159">**Item**</span><span class="sxs-lookup"><span data-stu-id="d39b1-159">**Item**</span></span> | <span data-ttu-id="d39b1-160">**預設值**</span><span class="sxs-lookup"><span data-stu-id="d39b1-160">**Default value**</span></span> | <span data-ttu-id="d39b1-161">**說明**</span><span class="sxs-lookup"><span data-stu-id="d39b1-161">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d39b1-162">公用 IP 的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-162">Max public IPs</span></span> |<span data-ttu-id="d39b1-163">50</span><span class="sxs-lookup"><span data-stu-id="d39b1-163">50</span></span> |<span data-ttu-id="d39b1-164">hello 的訂用帳戶可以在這個位置中建立的公用 Ip 數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-164">hello maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-165">虛擬網路的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-165">Max virtual networks</span></span> |<span data-ttu-id="d39b1-166">50</span><span class="sxs-lookup"><span data-stu-id="d39b1-166">50</span></span> |<span data-ttu-id="d39b1-167">hello 的訂用帳戶可以在這個位置中建立的虛擬網路的最大數目。</span><span class="sxs-lookup"><span data-stu-id="d39b1-167">hello maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-168">虛擬網路閘道的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-168">Max virtual network gateways</span></span> |<span data-ttu-id="d39b1-169">1</span><span class="sxs-lookup"><span data-stu-id="d39b1-169">1</span></span> |<span data-ttu-id="d39b1-170">hello 訂用帳戶可以在這個位置中建立的虛擬網路閘道 （VPN 閘道） 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-170">hello maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-171">網路連線的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-171">Max network connections</span></span> |<span data-ttu-id="d39b1-172">2</span><span class="sxs-lookup"><span data-stu-id="d39b1-172">2</span></span> |<span data-ttu-id="d39b1-173">hello 訂用帳戶可以建立在這個位置中的所有虛擬網路閘道的網路連線 （點對點或站台對站台） 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-173">hello maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="d39b1-174">負載平衡器的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-174">Max load balancers</span></span> |<span data-ttu-id="d39b1-175">50</span><span class="sxs-lookup"><span data-stu-id="d39b1-175">50</span></span> |<span data-ttu-id="d39b1-176">hello 訂用帳戶可以在這個位置中建立的負載平衡器的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-176">hello maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-177">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="d39b1-177">Max NICs</span></span> |<span data-ttu-id="d39b1-178">100</span><span class="sxs-lookup"><span data-stu-id="d39b1-178">100</span></span> |<span data-ttu-id="d39b1-179">hello 訂用帳戶可以在這個位置中建立的網路介面的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-179">hello maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d39b1-180">網路安全性群組的數目上限</span><span class="sxs-lookup"><span data-stu-id="d39b1-180">Max network security groups</span></span> |<span data-ttu-id="d39b1-181">50</span><span class="sxs-lookup"><span data-stu-id="d39b1-181">50</span></span> |<span data-ttu-id="d39b1-182">hello 訂用帳戶可以在這個位置中建立的網路安全性群組的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39b1-182">hello maximum number of network security groups that a subscription can create in this location.</span></span> |

##<a name="view-an-existing-quota"></a><span data-ttu-id="d39b1-183">檢視現有的配額</span><span class="sxs-lookup"><span data-stu-id="d39b1-183">View an existing quota</span></span>
<span data-ttu-id="d39b1-184">tooview 現有的配額，請按一下**更多服務**>**資源提供者**，並選取 hello 與哪些 hello 想 tooview 配額相關聯的服務。</span><span class="sxs-lookup"><span data-stu-id="d39b1-184">tooview an existing quota, click **More services**>**Resource Providers** and select hello service with which hello quota you want tooview is associated.</span></span> <span data-ttu-id="d39b1-185">接下來，按一下**配額**，然後選取您想要 tooview 配額 hello。</span><span class="sxs-lookup"><span data-stu-id="d39b1-185">Next, click **Quotas**, and select hello Quota you want tooview.</span></span>
   > ![檢視現有的配額](./media/azure-stack-setting-quota/ExistingQuota.PNG)
