---
title: "Azure Stack 中的配額類型 | Microsoft Docs"
description: "檢閱在 Azure Stack 中可用於服務和資源的不同配額類型。"
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
ms.openlocfilehash: 9c65abd596b1a67175a4f91558c318f16ddbb11f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="6e1e0-103">Azure Stack 中的配額類型</span><span class="sxs-lookup"><span data-stu-id="6e1e0-103">Quota types in Azure Stack</span></span>
<span data-ttu-id="6e1e0-104">[配額](azure-stack-plan-offer-quota-overview.md#plans)會定義使用者訂用帳戶可以佈建或取用的資源限制。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-104">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="6e1e0-105">例如，配額可能會允許使用者建立最多五個 VM。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-105">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="6e1e0-106">每個資源都可以有自己的配額類型。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-106">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="6e1e0-107">計算配額類型</span><span class="sxs-lookup"><span data-stu-id="6e1e0-107">Compute quota types</span></span>
| <span data-ttu-id="6e1e0-108">**類型**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-108">**Type**</span></span> | <span data-ttu-id="6e1e0-109">**預設值**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-109">**Default value**</span></span> | <span data-ttu-id="6e1e0-110">**說明**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-110">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e1e0-111">虛擬機器的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-111">Max number of virtual machines</span></span> |<span data-ttu-id="6e1e0-112">50</span><span class="sxs-lookup"><span data-stu-id="6e1e0-112">50</span></span> | <span data-ttu-id="6e1e0-113">訂用帳戶可以在這個位置建立的虛擬機器數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-113">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-114">虛擬機器核心的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-114">Max number of virtual machine cores</span></span> |<span data-ttu-id="6e1e0-115">100</span><span class="sxs-lookup"><span data-stu-id="6e1e0-115">100</span></span> | <span data-ttu-id="6e1e0-116">訂用帳戶可以在這個位置建立的核心數目上限 (例如，A3 VM 有四個核心)。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-116">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="6e1e0-117">可用性設定組的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-117">Max number of availability sets</span></span> |<span data-ttu-id="6e1e0-118">10</span><span class="sxs-lookup"><span data-stu-id="6e1e0-118">10</span></span> | <span data-ttu-id="6e1e0-119">可以在這個位置建立的可用性設定組數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-119">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="6e1e0-120">虛擬機器擴展集的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-120">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="6e1e0-121">100</span><span class="sxs-lookup"><span data-stu-id="6e1e0-121">100</span></span> | <span data-ttu-id="6e1e0-122">可以在這個位置建立的虛擬機器擴展集數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-122">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="6e1e0-123">此 Technical Preview 中未限制計算配額。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-123">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="6e1e0-124">儲存體配額類型</span><span class="sxs-lookup"><span data-stu-id="6e1e0-124">Storage quota types</span></span>
| <span data-ttu-id="6e1e0-125">**Item**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-125">**Item**</span></span> | <span data-ttu-id="6e1e0-126">**預設值**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-126">**Default value**</span></span> | <span data-ttu-id="6e1e0-127">**說明**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-127">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e1e0-128">最大容量 (GB)</span><span class="sxs-lookup"><span data-stu-id="6e1e0-128">Maximum capacity (GB)</span></span> |<span data-ttu-id="6e1e0-129">500</span><span class="sxs-lookup"><span data-stu-id="6e1e0-129">500</span></span> |<span data-ttu-id="6e1e0-130">訂用帳戶可以在這個位置取用的總儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-130">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="6e1e0-131">儲存體帳戶的總數</span><span class="sxs-lookup"><span data-stu-id="6e1e0-131">Total number of storage accounts</span></span> |<span data-ttu-id="6e1e0-132">20</span><span class="sxs-lookup"><span data-stu-id="6e1e0-132">20</span></span> |<span data-ttu-id="6e1e0-133">訂用帳戶可以在這個位置建立的儲存體帳戶數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-133">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="6e1e0-134">網路配額類型</span><span class="sxs-lookup"><span data-stu-id="6e1e0-134">Network quota types</span></span>
| <span data-ttu-id="6e1e0-135">**Item**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-135">**Item**</span></span> | <span data-ttu-id="6e1e0-136">**預設值**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-136">**Default value**</span></span> | <span data-ttu-id="6e1e0-137">**說明**</span><span class="sxs-lookup"><span data-stu-id="6e1e0-137">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e1e0-138">公用 IP 的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-138">Max public IPs</span></span> |<span data-ttu-id="6e1e0-139">50</span><span class="sxs-lookup"><span data-stu-id="6e1e0-139">50</span></span> |<span data-ttu-id="6e1e0-140">訂用帳戶可以在這個位置建立的公用 IP 數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-140">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-141">虛擬網路的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-141">Max virtual networks</span></span> |<span data-ttu-id="6e1e0-142">50</span><span class="sxs-lookup"><span data-stu-id="6e1e0-142">50</span></span> |<span data-ttu-id="6e1e0-143">訂用帳戶可以在這個位置建立的虛擬網路數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-143">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-144">虛擬網路閘道的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-144">Max virtual network gateways</span></span> |<span data-ttu-id="6e1e0-145">1</span><span class="sxs-lookup"><span data-stu-id="6e1e0-145">1</span></span> |<span data-ttu-id="6e1e0-146">訂用帳戶可以在這個位置建立的虛擬網路閘道 (VPN 閘道) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-146">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-147">網路連線的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-147">Max network connections</span></span> |<span data-ttu-id="6e1e0-148">2</span><span class="sxs-lookup"><span data-stu-id="6e1e0-148">2</span></span> |<span data-ttu-id="6e1e0-149">訂用帳戶可以在這個位置所有虛擬網路閘道上建立的網路連線 (點對點或站台對站台) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-149">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="6e1e0-150">負載平衡器的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-150">Max load balancers</span></span> |<span data-ttu-id="6e1e0-151">50</span><span class="sxs-lookup"><span data-stu-id="6e1e0-151">50</span></span> |<span data-ttu-id="6e1e0-152">訂用帳戶可以在這個位置建立的負載平衡器數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-152">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-153">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="6e1e0-153">Max NICs</span></span> |<span data-ttu-id="6e1e0-154">100</span><span class="sxs-lookup"><span data-stu-id="6e1e0-154">100</span></span> |<span data-ttu-id="6e1e0-155">訂用帳戶可以在這個位置建立的網路介面數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-155">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="6e1e0-156">網路安全性群組的數目上限</span><span class="sxs-lookup"><span data-stu-id="6e1e0-156">Max network security groups</span></span> |<span data-ttu-id="6e1e0-157">50</span><span class="sxs-lookup"><span data-stu-id="6e1e0-157">50</span></span> |<span data-ttu-id="6e1e0-158">訂用帳戶可以在這個位置建立的網路安全性群組數目上限。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-158">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="6e1e0-159">檢視現有的配額</span><span class="sxs-lookup"><span data-stu-id="6e1e0-159">View an existing quota</span></span>
1. <span data-ttu-id="6e1e0-160">按一下 [更多服務] > [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-160">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="6e1e0-161">選取您要檢視的服務及其配額。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-161">Select the service with the quota that you want to view.</span></span>
3. <span data-ttu-id="6e1e0-162">按一下 [配額]，然後選取要檢視的配額。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-162">Click **Quotas**, and select the quota you want to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e1e0-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e1e0-163">Next steps</span></span>
[<span data-ttu-id="6e1e0-164">深入了解方案、供應項目與配額。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-164">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="6e1e0-165">建立方案時建立配額。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-165">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
