---
title: "在 Azure 堆疊 aaaQuota 類型 |Microsoft 文件"
description: "檢閱 hello 不同的配額類型之服務和 Azure 堆疊中的資源。"
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
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: e05870603526a3e0e65d536cff98b9033524017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="bc04d-103">Azure Stack 中的配額類型</span><span class="sxs-lookup"><span data-stu-id="bc04d-103">Quota types in Azure Stack</span></span>
<span data-ttu-id="bc04d-104">[配額](azure-stack-plan-offer-quota-overview.md#plans)定義 hello 使用者訂用帳戶可以佈建或取用之資源的限制。</span><span class="sxs-lookup"><span data-stu-id="bc04d-104">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define hello limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="bc04d-105">例如，配額可能允許使用者 toocreate toofive Vm 上。</span><span class="sxs-lookup"><span data-stu-id="bc04d-105">For example, a quota might allow a user toocreate up toofive VMs.</span></span> <span data-ttu-id="bc04d-106">每個資源都可以有自己的配額類型。</span><span class="sxs-lookup"><span data-stu-id="bc04d-106">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="bc04d-107">計算配額類型</span><span class="sxs-lookup"><span data-stu-id="bc04d-107">Compute quota types</span></span>
| <span data-ttu-id="bc04d-108">**類型**</span><span class="sxs-lookup"><span data-stu-id="bc04d-108">**Type**</span></span> | <span data-ttu-id="bc04d-109">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bc04d-109">**Default value**</span></span> | <span data-ttu-id="bc04d-110">**說明**</span><span class="sxs-lookup"><span data-stu-id="bc04d-110">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc04d-111">虛擬機器的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-111">Max number of virtual machines</span></span> |<span data-ttu-id="bc04d-112">50</span><span class="sxs-lookup"><span data-stu-id="bc04d-112">50</span></span> | <span data-ttu-id="bc04d-113">hello 訂用帳戶可以在這個位置中建立的虛擬機器的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-113">hello maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-114">虛擬機器核心的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-114">Max number of virtual machine cores</span></span> |<span data-ttu-id="bc04d-115">100</span><span class="sxs-lookup"><span data-stu-id="bc04d-115">100</span></span> | <span data-ttu-id="bc04d-116">hello 的訂用帳戶可以在這個位置中建立的核心數目上限 （例如，A3 VM 有四個核心）。</span><span class="sxs-lookup"><span data-stu-id="bc04d-116">hello maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="bc04d-117">可用性設定組的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-117">Max number of availability sets</span></span> |<span data-ttu-id="bc04d-118">10</span><span class="sxs-lookup"><span data-stu-id="bc04d-118">10</span></span> | <span data-ttu-id="bc04d-119">hello，可以在這個位置建立可用性設定組的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-119">hello maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="bc04d-120">虛擬機器擴展集的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-120">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="bc04d-121">100</span><span class="sxs-lookup"><span data-stu-id="bc04d-121">100</span></span> | <span data-ttu-id="bc04d-122">hello 可以在這個位置建立的虛擬機器規模集的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-122">hello maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="bc04d-123">此 Technical Preview 中未限制計算配額。</span><span class="sxs-lookup"><span data-stu-id="bc04d-123">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="bc04d-124">儲存體配額類型</span><span class="sxs-lookup"><span data-stu-id="bc04d-124">Storage quota types</span></span>
| <span data-ttu-id="bc04d-125">**Item**</span><span class="sxs-lookup"><span data-stu-id="bc04d-125">**Item**</span></span> | <span data-ttu-id="bc04d-126">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bc04d-126">**Default value**</span></span> | <span data-ttu-id="bc04d-127">**說明**</span><span class="sxs-lookup"><span data-stu-id="bc04d-127">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc04d-128">最大容量 (GB)</span><span class="sxs-lookup"><span data-stu-id="bc04d-128">Maximum capacity (GB)</span></span> |<span data-ttu-id="bc04d-129">500</span><span class="sxs-lookup"><span data-stu-id="bc04d-129">500</span></span> |<span data-ttu-id="bc04d-130">訂用帳戶可以在這個位置取用的總儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="bc04d-130">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="bc04d-131">儲存體帳戶的總數</span><span class="sxs-lookup"><span data-stu-id="bc04d-131">Total number of storage accounts</span></span> |<span data-ttu-id="bc04d-132">20</span><span class="sxs-lookup"><span data-stu-id="bc04d-132">20</span></span> |<span data-ttu-id="bc04d-133">hello 的訂用帳戶可以在這個位置中建立的儲存體帳戶數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-133">hello maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="bc04d-134">網路配額類型</span><span class="sxs-lookup"><span data-stu-id="bc04d-134">Network quota types</span></span>
| <span data-ttu-id="bc04d-135">**Item**</span><span class="sxs-lookup"><span data-stu-id="bc04d-135">**Item**</span></span> | <span data-ttu-id="bc04d-136">**預設值**</span><span class="sxs-lookup"><span data-stu-id="bc04d-136">**Default value**</span></span> | <span data-ttu-id="bc04d-137">**說明**</span><span class="sxs-lookup"><span data-stu-id="bc04d-137">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc04d-138">公用 IP 的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-138">Max public IPs</span></span> |<span data-ttu-id="bc04d-139">50</span><span class="sxs-lookup"><span data-stu-id="bc04d-139">50</span></span> |<span data-ttu-id="bc04d-140">hello 的訂用帳戶可以在這個位置中建立的公用 Ip 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-140">hello maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-141">虛擬網路的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-141">Max virtual networks</span></span> |<span data-ttu-id="bc04d-142">50</span><span class="sxs-lookup"><span data-stu-id="bc04d-142">50</span></span> |<span data-ttu-id="bc04d-143">hello 的訂用帳戶可以在這個位置中建立的虛擬網路的最大數目。</span><span class="sxs-lookup"><span data-stu-id="bc04d-143">hello maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-144">虛擬網路閘道的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-144">Max virtual network gateways</span></span> |<span data-ttu-id="bc04d-145">1</span><span class="sxs-lookup"><span data-stu-id="bc04d-145">1</span></span> |<span data-ttu-id="bc04d-146">hello 訂用帳戶可以在這個位置中建立的虛擬網路閘道 （VPN 閘道） 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-146">hello maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-147">網路連線的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-147">Max network connections</span></span> |<span data-ttu-id="bc04d-148">2</span><span class="sxs-lookup"><span data-stu-id="bc04d-148">2</span></span> |<span data-ttu-id="bc04d-149">hello 訂用帳戶可以建立在這個位置中的所有虛擬網路閘道的網路連線 （點對點或站台對站台） 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-149">hello maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="bc04d-150">負載平衡器的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-150">Max load balancers</span></span> |<span data-ttu-id="bc04d-151">50</span><span class="sxs-lookup"><span data-stu-id="bc04d-151">50</span></span> |<span data-ttu-id="bc04d-152">hello 訂用帳戶可以在這個位置中建立的負載平衡器的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-152">hello maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-153">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="bc04d-153">Max NICs</span></span> |<span data-ttu-id="bc04d-154">100</span><span class="sxs-lookup"><span data-stu-id="bc04d-154">100</span></span> |<span data-ttu-id="bc04d-155">hello 訂用帳戶可以在這個位置中建立的網路介面的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-155">hello maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="bc04d-156">網路安全性群組的數目上限</span><span class="sxs-lookup"><span data-stu-id="bc04d-156">Max network security groups</span></span> |<span data-ttu-id="bc04d-157">50</span><span class="sxs-lookup"><span data-stu-id="bc04d-157">50</span></span> |<span data-ttu-id="bc04d-158">hello 訂用帳戶可以在這個位置中建立的網路安全性群組的數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc04d-158">hello maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="bc04d-159">檢視現有的配額</span><span class="sxs-lookup"><span data-stu-id="bc04d-159">View an existing quota</span></span>
1. <span data-ttu-id="bc04d-160">按一下 [更多服務] > [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="bc04d-160">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="bc04d-161">選取您想 tooview hello 配額與 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="bc04d-161">Select hello service with hello quota that you want tooview.</span></span>
3. <span data-ttu-id="bc04d-162">按一下**配額**，和您想要 tooview 選取 hello 配額。</span><span class="sxs-lookup"><span data-stu-id="bc04d-162">Click **Quotas**, and select hello quota you want tooview.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc04d-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc04d-163">Next steps</span></span>
[<span data-ttu-id="bc04d-164">深入了解方案、供應項目與配額。</span><span class="sxs-lookup"><span data-stu-id="bc04d-164">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="bc04d-165">建立方案時建立配額。</span><span class="sxs-lookup"><span data-stu-id="bc04d-165">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
