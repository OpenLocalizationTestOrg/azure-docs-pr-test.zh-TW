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
ms.openlocfilehash: 33906514955b76a3d6587b19899a0c76a09018a2
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="21fb9-103">Azure Stack 中的配額類型</span><span class="sxs-lookup"><span data-stu-id="21fb9-103">Quota types in Azure Stack</span></span>

<span data-ttu-id="21fb9-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="21fb9-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="21fb9-105">[配額](azure-stack-plan-offer-quota-overview.md#plans)會定義使用者訂用帳戶可以佈建或取用的資源限制。</span><span class="sxs-lookup"><span data-stu-id="21fb9-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="21fb9-106">例如，配額可能會允許使用者建立最多五個 VM。</span><span class="sxs-lookup"><span data-stu-id="21fb9-106">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="21fb9-107">每個資源都可以有自己的配額類型。</span><span class="sxs-lookup"><span data-stu-id="21fb9-107">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="21fb9-108">計算配額類型</span><span class="sxs-lookup"><span data-stu-id="21fb9-108">Compute quota types</span></span>
| <span data-ttu-id="21fb9-109">**類型**</span><span class="sxs-lookup"><span data-stu-id="21fb9-109">**Type**</span></span> | <span data-ttu-id="21fb9-110">**預設值**</span><span class="sxs-lookup"><span data-stu-id="21fb9-110">**Default value**</span></span> | <span data-ttu-id="21fb9-111">**說明**</span><span class="sxs-lookup"><span data-stu-id="21fb9-111">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21fb9-112">虛擬機器的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-112">Max number of virtual machines</span></span> |<span data-ttu-id="21fb9-113">50</span><span class="sxs-lookup"><span data-stu-id="21fb9-113">50</span></span> | <span data-ttu-id="21fb9-114">訂用帳戶可以在這個位置建立的虛擬機器數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-114">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-115">虛擬機器核心的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-115">Max number of virtual machine cores</span></span> |<span data-ttu-id="21fb9-116">100</span><span class="sxs-lookup"><span data-stu-id="21fb9-116">100</span></span> | <span data-ttu-id="21fb9-117">訂用帳戶可以在這個位置建立的核心數目上限 (例如，A3 VM 有四個核心)。</span><span class="sxs-lookup"><span data-stu-id="21fb9-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="21fb9-118">可用性設定組的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-118">Max number of availability sets</span></span> |<span data-ttu-id="21fb9-119">10</span><span class="sxs-lookup"><span data-stu-id="21fb9-119">10</span></span> | <span data-ttu-id="21fb9-120">可以在這個位置建立的可用性設定組數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-120">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="21fb9-121">虛擬機器擴展集的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-121">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="21fb9-122">100</span><span class="sxs-lookup"><span data-stu-id="21fb9-122">100</span></span> | <span data-ttu-id="21fb9-123">可以在這個位置建立的虛擬機器擴展集數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-123">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="21fb9-124">此 Technical Preview 中未限制計算配額。</span><span class="sxs-lookup"><span data-stu-id="21fb9-124">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="21fb9-125">儲存體配額類型</span><span class="sxs-lookup"><span data-stu-id="21fb9-125">Storage quota types</span></span>
| <span data-ttu-id="21fb9-126">**Item**</span><span class="sxs-lookup"><span data-stu-id="21fb9-126">**Item**</span></span> | <span data-ttu-id="21fb9-127">**預設值**</span><span class="sxs-lookup"><span data-stu-id="21fb9-127">**Default value**</span></span> | <span data-ttu-id="21fb9-128">**說明**</span><span class="sxs-lookup"><span data-stu-id="21fb9-128">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21fb9-129">最大容量 (GB)</span><span class="sxs-lookup"><span data-stu-id="21fb9-129">Maximum capacity (GB)</span></span> |<span data-ttu-id="21fb9-130">500</span><span class="sxs-lookup"><span data-stu-id="21fb9-130">500</span></span> |<span data-ttu-id="21fb9-131">訂用帳戶可以在這個位置取用的總儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="21fb9-131">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="21fb9-132">儲存體帳戶的總數</span><span class="sxs-lookup"><span data-stu-id="21fb9-132">Total number of storage accounts</span></span> |<span data-ttu-id="21fb9-133">20</span><span class="sxs-lookup"><span data-stu-id="21fb9-133">20</span></span> |<span data-ttu-id="21fb9-134">訂用帳戶可以在這個位置建立的儲存體帳戶數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-134">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="21fb9-135">網路配額類型</span><span class="sxs-lookup"><span data-stu-id="21fb9-135">Network quota types</span></span>
| <span data-ttu-id="21fb9-136">**Item**</span><span class="sxs-lookup"><span data-stu-id="21fb9-136">**Item**</span></span> | <span data-ttu-id="21fb9-137">**預設值**</span><span class="sxs-lookup"><span data-stu-id="21fb9-137">**Default value**</span></span> | <span data-ttu-id="21fb9-138">**說明**</span><span class="sxs-lookup"><span data-stu-id="21fb9-138">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21fb9-139">公用 IP 的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-139">Max public IPs</span></span> |<span data-ttu-id="21fb9-140">50</span><span class="sxs-lookup"><span data-stu-id="21fb9-140">50</span></span> |<span data-ttu-id="21fb9-141">訂用帳戶可以在這個位置建立的公用 IP 數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-141">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-142">虛擬網路的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-142">Max virtual networks</span></span> |<span data-ttu-id="21fb9-143">50</span><span class="sxs-lookup"><span data-stu-id="21fb9-143">50</span></span> |<span data-ttu-id="21fb9-144">訂用帳戶可以在這個位置建立的虛擬網路數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-144">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-145">虛擬網路閘道的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-145">Max virtual network gateways</span></span> |<span data-ttu-id="21fb9-146">1</span><span class="sxs-lookup"><span data-stu-id="21fb9-146">1</span></span> |<span data-ttu-id="21fb9-147">訂用帳戶可以在這個位置建立的虛擬網路閘道 (VPN 閘道) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-148">網路連線的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-148">Max network connections</span></span> |<span data-ttu-id="21fb9-149">2</span><span class="sxs-lookup"><span data-stu-id="21fb9-149">2</span></span> |<span data-ttu-id="21fb9-150">訂用帳戶可以在這個位置所有虛擬網路閘道上建立的網路連線 (點對點或站台對站台) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="21fb9-151">負載平衡器的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-151">Max load balancers</span></span> |<span data-ttu-id="21fb9-152">50</span><span class="sxs-lookup"><span data-stu-id="21fb9-152">50</span></span> |<span data-ttu-id="21fb9-153">訂用帳戶可以在這個位置建立的負載平衡器數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-153">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-154">最大 NIC</span><span class="sxs-lookup"><span data-stu-id="21fb9-154">Max NICs</span></span> |<span data-ttu-id="21fb9-155">100</span><span class="sxs-lookup"><span data-stu-id="21fb9-155">100</span></span> |<span data-ttu-id="21fb9-156">訂用帳戶可以在這個位置建立的網路介面數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-156">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="21fb9-157">網路安全性群組的數目上限</span><span class="sxs-lookup"><span data-stu-id="21fb9-157">Max network security groups</span></span> |<span data-ttu-id="21fb9-158">50</span><span class="sxs-lookup"><span data-stu-id="21fb9-158">50</span></span> |<span data-ttu-id="21fb9-159">訂用帳戶可以在這個位置建立的網路安全性群組數目上限。</span><span class="sxs-lookup"><span data-stu-id="21fb9-159">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="21fb9-160">檢視現有的配額</span><span class="sxs-lookup"><span data-stu-id="21fb9-160">View an existing quota</span></span>
1. <span data-ttu-id="21fb9-161">按一下 [更多服務] > [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="21fb9-161">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="21fb9-162">選取您要檢視的服務及其配額。</span><span class="sxs-lookup"><span data-stu-id="21fb9-162">Select the service with the quota that you want to view.</span></span>
3. <span data-ttu-id="21fb9-163">按一下 [配額]，然後選取要檢視的配額。</span><span class="sxs-lookup"><span data-stu-id="21fb9-163">Click **Quotas**, and select the quota you want to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21fb9-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21fb9-164">Next steps</span></span>
[<span data-ttu-id="21fb9-165">深入了解方案、供應項目與配額。</span><span class="sxs-lookup"><span data-stu-id="21fb9-165">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="21fb9-166">建立方案時建立配額。</span><span class="sxs-lookup"><span data-stu-id="21fb9-166">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
