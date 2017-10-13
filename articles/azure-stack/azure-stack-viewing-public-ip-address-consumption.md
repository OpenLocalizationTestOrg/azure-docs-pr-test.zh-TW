---
title: "檢視 Azure Stack 中的公用 IP 位址使用 |Microsoft Docs"
description: "系統管理員可以檢視區域中的公用 IP 位址使用"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 0f77be49-eafe-4886-8c58-a17061e8120f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: scottnap
ms.openlocfilehash: 7651565eebf6272f307a4ce4790ca19b41bfa826
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a><span data-ttu-id="b4024-103">檢視 Azure Stack 中的公用 IP 位址使用</span><span class="sxs-lookup"><span data-stu-id="b4024-103">View public IP address consumption in Azure Stack</span></span>

<span data-ttu-id="b4024-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="b4024-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b4024-105">身為雲端系統管理員，您可以檢視配置給租用戶的公用 IP 位址數目、仍可供配置的公用 IP 位址數目，以及已在該位置配置的公用 IP 位址百分比。</span><span class="sxs-lookup"><span data-stu-id="b4024-105">As a cloud administrator, you can view the number of public IP addresses that have been allocated to tenants, the number of public IP addresses that are still available for allocation, and the percentage of public IP addresses that have been allocated in that location.</span></span>

<span data-ttu-id="b4024-106">[公用 IP 集區使用方式] 磚會顯示網狀架構上所有公用 IP 位址集區中已使用的公用 IP 位址總數，無論其是否已用於租用戶 IaaS VM 執行個體、網狀架構基礎結構服務，或由租用戶所明確建立的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="b4024-106">The **Public IP pools usage** tile shows the total number of public IP addresses that have been consumed across all public IP address pools on the fabric, whether they have been used for tenant IaaS VM instances, fabric infrastructure services, or public IP address resources that were explicitly created by tenants.</span></span>

<span data-ttu-id="b4024-107">此磚的目的是要讓 Azure Stack 系統管理員檢視在此位置中已使用的公用 IP 位址總數。</span><span class="sxs-lookup"><span data-stu-id="b4024-107">The purpose of this tile is to give Azure Stack administrators a sense of the overall number of public IP addresses that have been consumed in this location.</span></span> <span data-ttu-id="b4024-108">這可協助系統管理員判斷其是否即將耗盡此資源。</span><span class="sxs-lookup"><span data-stu-id="b4024-108">This helps administrators determine whether they are running low on this resource.</span></span>

<span data-ttu-id="b4024-109">在 [資源提供者] 的 [網路] 刀鋒視窗上，[租用戶資源] 下的 [公用 IP 位址] 功能表項目僅會列出租用戶所明確建立的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b4024-109">On the **Resource providers**, **Network** blade, the **Public IP addresses** menu item under **Tenant Resources** lists only those public IP addresses that have been *explicitly created by tenants*.</span></span> <span data-ttu-id="b4024-110">例如，[公用 IP 集區使用方式] 磚上的 [已使用] 公用 IP 位址數目，永遠不同於 (大於) 在 [租用戶資源] 下 [公用 IP 位址] 磚上的數目。</span><span class="sxs-lookup"><span data-stu-id="b4024-110">As such, the number of **Used** public IP addresses on the **Public IP pools usage** tile is always different from (larger than) the number on the **Public IP Addresses** tile under **Tenant Resources**.</span></span>

## <a name="view-the-public-ip-address-usage-information"></a><span data-ttu-id="b4024-111">檢視公用 IP 位址使用方式資訊</span><span class="sxs-lookup"><span data-stu-id="b4024-111">View the public IP address usage information</span></span>
<span data-ttu-id="b4024-112">若要檢視區域中已使用的公用 IP 位址總數：</span><span class="sxs-lookup"><span data-stu-id="b4024-112">To view the total number of public IP addresses that have been consumed in the region:</span></span>

1. <span data-ttu-id="b4024-113">在 Azure Stack 系統管理員入口網站中，按一下 [更多服務]，然後在 [管理資源] 下方按一下 [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="b4024-113">In the Azure Stack administrator portal, click **More services**, under **Administrative Resources**, click **Resource providers**.</span></span>
2. <span data-ttu-id="b4024-114">從 [資源提供者] 清單中，選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="b4024-114">From the list of **Resource Providers**, select **Network**.</span></span>
3. <span data-ttu-id="b4024-115">[網路] 刀鋒視窗會在 [概觀] 區段中顯示 [公用 IP 集區使用方式]磚。</span><span class="sxs-lookup"><span data-stu-id="b4024-115">The **Network** blade displays the **Public IP pools usage** tile in the **Overview** section.</span></span>

![網路資源提供者刀鋒視窗](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

<span data-ttu-id="b4024-117">請注意，[已使用] 數字代表已指派的該位置中來自所有公用 IP 位址集區的公用 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="b4024-117">Keep in mind that the **Used** number represents the number of public IP addresses from all public IP address pools in that location that are assigned.</span></span> <span data-ttu-id="b4024-118">[可用] 數字代表來自所有尚未指派，且仍可供使用之公用 IP 位址集區的公用 IP 數目。</span><span class="sxs-lookup"><span data-stu-id="b4024-118">The **Free** number represents the number of public IP addresses from all public IP address pools that have not been assigned and are still available.</span></span> <span data-ttu-id="b4024-119">[% 已使用] 數字代表該位置內所有公用 IP 位址集區中已使用或已指派公用 IP 位址總數的百分比數目。</span><span class="sxs-lookup"><span data-stu-id="b4024-119">The **% Used** number represents the number of used or assigned addresses as a percentage of the total number of public IP addresses in all public IP address pools in that location.</span></span>

## <a name="view-the-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a><span data-ttu-id="b4024-120">檢視租用戶訂用帳戶所建立的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b4024-120">View the public IP addresses that were created by tenant subscriptions</span></span>
<span data-ttu-id="b4024-121">若要查看特定區域中租用戶訂用帳戶所明確建立的公用 IP 位址清單，請按一下 [租用戶資源] 下的 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="b4024-121">To see a list of public IP addresses that were explicitly created by tenant subscriptions in a specific region, click **Public IP addresses** under **Tenant Resources**.</span></span>

![租用戶公用 IP 位址](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

<span data-ttu-id="b4024-123">您可能會注意到某些已動態配置的公用 IP 位址會顯示在清單中，但尚未具有與其相關聯的位址。</span><span class="sxs-lookup"><span data-stu-id="b4024-123">You might notice that some public IP addresses that have been dynamically allocated appear in the list but do not have an address associated with them yet.</span></span> <span data-ttu-id="b4024-124">這是因為位址資源已在網路資源提供者中建立，但尚未在網路控制卡中建立。</span><span class="sxs-lookup"><span data-stu-id="b4024-124">This is because the address resource has been created in the Network Resource Provider, but not in the Network Controller yet.</span></span>

<span data-ttu-id="b4024-125">網路控制卡在位址實際繫結至介面、網路介面卡 (NIC)、負載平衡器或虛擬網路閘道之前，不會將位址指派給此資源。</span><span class="sxs-lookup"><span data-stu-id="b4024-125">The Network Controller does not assign an address to this resource until it is actually bound to an interface, a network interface card (NIC), a load balancer, or a virtual network gateway.</span></span> <span data-ttu-id="b4024-126">當公用 IP 位址繫結至介面時，網路控制卡會將 IP 位址配置給它，使其顯示在 [位址] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="b4024-126">When the public IP address is bound to an interface, the Network Controller allocates an IP address to it, and it appears in the **Address** field.</span></span>

## <a name="view-the-public-ip-address-information-summary-table"></a><span data-ttu-id="b4024-127">檢視公用 IP 位址資訊摘要資料表</span><span class="sxs-lookup"><span data-stu-id="b4024-127">View the public IP address information summary table</span></span>
<span data-ttu-id="b4024-128">指派公用 IP 位址時具有數種不同案例，可判斷位址是否顯示在一個 (或其他) 清單中。</span><span class="sxs-lookup"><span data-stu-id="b4024-128">There are a number of different cases in which public IP addresses are assigned that determine whether the address appears in one list or another.</span></span>

| <span data-ttu-id="b4024-129">**公用 IP 位址指派案例**</span><span class="sxs-lookup"><span data-stu-id="b4024-129">**Public IP address assignment case**</span></span> | <span data-ttu-id="b4024-130">**顯示於使用方式摘要**</span><span class="sxs-lookup"><span data-stu-id="b4024-130">**Appears in usage summary**</span></span> | <span data-ttu-id="b4024-131">**顯示於租用戶公用 IP 位址清單**</span><span class="sxs-lookup"><span data-stu-id="b4024-131">**Appears in tenant public IP addresses list**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4024-132">尚未指派給 NIC 或負載平衡器 (暫時) 的動態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b4024-132">Dynamic public IP address not yet assigned to an NIC or load balancer (temporary)</span></span> |<span data-ttu-id="b4024-133">否</span><span class="sxs-lookup"><span data-stu-id="b4024-133">No</span></span> |<span data-ttu-id="b4024-134">是</span><span class="sxs-lookup"><span data-stu-id="b4024-134">Yes</span></span> |
| <span data-ttu-id="b4024-135">已指派給 NIC 或負載平衡器的動態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b4024-135">Dynamic public IP address assigned to an NIC or load balancer.</span></span> |<span data-ttu-id="b4024-136">是</span><span class="sxs-lookup"><span data-stu-id="b4024-136">Yes</span></span> |<span data-ttu-id="b4024-137">是</span><span class="sxs-lookup"><span data-stu-id="b4024-137">Yes</span></span> |
| <span data-ttu-id="b4024-138">已指派給租用戶 NIC 或負載平衡器的靜態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b4024-138">Static public IP address assigned to a tenant NIC or load balancer.</span></span> |<span data-ttu-id="b4024-139">是</span><span class="sxs-lookup"><span data-stu-id="b4024-139">Yes</span></span> |<span data-ttu-id="b4024-140">是</span><span class="sxs-lookup"><span data-stu-id="b4024-140">Yes</span></span> |
| <span data-ttu-id="b4024-141">已指派給網狀架構基礎結構服務端點的靜態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b4024-141">Static public IP address assigned to a fabric infrastructure service endpoint.</span></span> |<span data-ttu-id="b4024-142">是</span><span class="sxs-lookup"><span data-stu-id="b4024-142">Yes</span></span> |<span data-ttu-id="b4024-143">否</span><span class="sxs-lookup"><span data-stu-id="b4024-143">No</span></span> |
| <span data-ttu-id="b4024-144">公用 IP 位址會以隱含方式針對 IaaS VM 執行個體而建立，並用於虛擬網路上的輸出 NAT。</span><span class="sxs-lookup"><span data-stu-id="b4024-144">Public IP address implicitly created for IaaS VM instances and used for outbound NAT on the virtual network.</span></span> <span data-ttu-id="b4024-145">每當租用戶建立 VM 執行個體，讓 VM 可以將資訊送出到網際網路時，這些位址便會在幕後建立。</span><span class="sxs-lookup"><span data-stu-id="b4024-145">These are created behind the scenes whenever a tenant creates a VM instance so that VMs can send information out to the Internet.</span></span> |<span data-ttu-id="b4024-146">是</span><span class="sxs-lookup"><span data-stu-id="b4024-146">Yes</span></span> |<span data-ttu-id="b4024-147">否</span><span class="sxs-lookup"><span data-stu-id="b4024-147">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4024-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4024-148">Next steps</span></span>
[<span data-ttu-id="b4024-149">在 Azure Stack 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b4024-149">Manage Storage Accounts in Azure Stack</span></span>](azure-stack-manage-storage-accounts.md)