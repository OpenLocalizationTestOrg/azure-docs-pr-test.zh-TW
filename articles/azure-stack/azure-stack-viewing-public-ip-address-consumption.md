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
ms.date: 7/18/2017
ms.author: scottnap
ms.openlocfilehash: 6b7da3c1b4e9bcaa302d4c763eb73d0dd1832124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a><span data-ttu-id="20b06-103">檢視 Azure Stack 中的公用 IP 位址使用</span><span class="sxs-lookup"><span data-stu-id="20b06-103">View public IP address consumption in Azure Stack</span></span>
<span data-ttu-id="20b06-104">身為雲端系統管理員，您可以檢視配置給租用戶的公用 IP 位址數目、仍可供配置的公用 IP 位址數目，以及已在該位置配置的公用 IP 位址百分比。</span><span class="sxs-lookup"><span data-stu-id="20b06-104">As a cloud administrator, you can view the number of public IP addresses that have been allocated to tenants, the number of public IP addresses that are still available for allocation, and the percentage of public IP addresses that have been allocated in that location.</span></span>

<span data-ttu-id="20b06-105">[公用 IP 集區使用方式] 磚會顯示網狀架構上所有公用 IP 位址集區中已使用的公用 IP 位址總數，無論其是否已用於租用戶 IaaS VM 執行個體、網狀架構基礎結構服務，或由租用戶所明確建立的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="20b06-105">The **Public IP pools usage** tile shows the total number of public IP addresses that have been consumed across all public IP address pools on the fabric, whether they have been used for tenant IaaS VM instances, fabric infrastructure services, or public IP address resources that were explicitly created by tenants.</span></span>

<span data-ttu-id="20b06-106">此磚的目的是要讓 Azure Stack 系統管理員檢視在此位置中已使用的公用 IP 位址總數。</span><span class="sxs-lookup"><span data-stu-id="20b06-106">The purpose of this tile is to give Azure Stack administrators a sense of the overall number of public IP addresses that have been consumed in this location.</span></span> <span data-ttu-id="20b06-107">這可協助系統管理員判斷其是否即將耗盡此資源。</span><span class="sxs-lookup"><span data-stu-id="20b06-107">This helps administrators determine whether they are running low on this resource.</span></span>

<span data-ttu-id="20b06-108">在 [資源提供者] 的 [網路] 刀鋒視窗上，[租用戶資源] 下的 [公用 IP 位址] 功能表項目僅會列出租用戶所明確建立的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="20b06-108">On the **Resource providers**, **Network** blade, the **Public IP addresses** menu item under **Tenant Resources** lists only those public IP addresses that have been *explicitly created by tenants*.</span></span> <span data-ttu-id="20b06-109">例如，[公用 IP 集區使用方式] 磚上的 [已使用] 公用 IP 位址數目，永遠不同於 (大於) 在 [租用戶資源] 下 [公用 IP 位址] 磚上的數目。</span><span class="sxs-lookup"><span data-stu-id="20b06-109">As such, the number of **Used** public IP addresses on the **Public IP pools usage** tile is always different from (larger than) the number on the **Public IP Addresses** tile under **Tenant Resources**.</span></span>

## <a name="view-the-public-ip-address-usage-information"></a><span data-ttu-id="20b06-110">檢視公用 IP 位址使用方式資訊</span><span class="sxs-lookup"><span data-stu-id="20b06-110">View the public IP address usage information</span></span>
<span data-ttu-id="20b06-111">若要檢視區域中已使用的公用 IP 位址總數：</span><span class="sxs-lookup"><span data-stu-id="20b06-111">To view the total number of public IP addresses that have been consumed in the region:</span></span>

1. <span data-ttu-id="20b06-112">在 Azure Stack 系統管理員入口網站中，按一下 [更多服務]，然後在 [管理資源] 下方按一下 [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="20b06-112">In the Azure Stack administrator portal, click **More services**, under **Administrative Resources**, click **Resource providers**.</span></span>
2. <span data-ttu-id="20b06-113">從 [資源提供者] 清單中，選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="20b06-113">From the list of **Resource Providers**, select **Network**.</span></span>
3. <span data-ttu-id="20b06-114">[網路] 刀鋒視窗會在 [概觀] 區段中顯示 [公用 IP 集區使用方式]磚。</span><span class="sxs-lookup"><span data-stu-id="20b06-114">The **Network** blade displays the **Public IP pools usage** tile in the **Overview** section.</span></span>

![網路資源提供者刀鋒視窗](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

<span data-ttu-id="20b06-116">請注意，[已使用] 數字代表已指派的該位置中來自所有公用 IP 位址集區的公用 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="20b06-116">Keep in mind that the **Used** number represents the number of public IP addresses from all public IP address pools in that location that are assigned.</span></span> <span data-ttu-id="20b06-117">[可用] 數字代表來自所有尚未指派，且仍可供使用之公用 IP 位址集區的公用 IP 數目。</span><span class="sxs-lookup"><span data-stu-id="20b06-117">The **Free** number represents the number of public IP addresses from all public IP address pools that have not been assigned and are still available.</span></span> <span data-ttu-id="20b06-118">[% 已使用] 數字代表該位置內所有公用 IP 位址集區中已使用或已指派公用 IP 位址總數的百分比數目。</span><span class="sxs-lookup"><span data-stu-id="20b06-118">The **% Used** number represents the number of used or assigned addresses as a percentage of the total number of public IP addresses in all public IP address pools in that location.</span></span>

## <a name="view-the-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a><span data-ttu-id="20b06-119">檢視租用戶訂用帳戶所建立的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="20b06-119">View the public IP addresses that were created by tenant subscriptions</span></span>
<span data-ttu-id="20b06-120">若要查看特定區域中租用戶訂用帳戶所明確建立的公用 IP 位址清單，請按一下 [租用戶資源] 下的 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="20b06-120">To see a list of public IP addresses that were explicitly created by tenant subscriptions in a specific region, click **Public IP addresses** under **Tenant Resources**.</span></span>

![租用戶公用 IP 位址](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

<span data-ttu-id="20b06-122">您可能會注意到某些已動態配置的公用 IP 位址會顯示在清單中，但尚未具有與其相關聯的位址。</span><span class="sxs-lookup"><span data-stu-id="20b06-122">You might notice that some public IP addresses that have been dynamically allocated appear in the list but do not have an address associated with them yet.</span></span> <span data-ttu-id="20b06-123">這是因為位址資源已在網路資源提供者中建立，但尚未在網路控制卡中建立。</span><span class="sxs-lookup"><span data-stu-id="20b06-123">This is because the address resource has been created in the Network Resource Provider, but not in the Network Controller yet.</span></span>

<span data-ttu-id="20b06-124">網路控制卡在位址實際繫結至介面、網路介面卡 (NIC)、負載平衡器或虛擬網路閘道之前，不會將位址指派給此資源。</span><span class="sxs-lookup"><span data-stu-id="20b06-124">The Network Controller does not assign an address to this resource until it is actually bound to an interface, a network interface card (NIC), a load balancer, or a virtual network gateway.</span></span> <span data-ttu-id="20b06-125">當公用 IP 位址繫結至介面時，網路控制卡會將 IP 位址配置給它，使其顯示在 [位址] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="20b06-125">When the public IP address is bound to an interface, the Network Controller allocates an IP address to it, and it appears in the **Address** field.</span></span>

## <a name="view-the-public-ip-address-information-summary-table"></a><span data-ttu-id="20b06-126">檢視公用 IP 位址資訊摘要資料表</span><span class="sxs-lookup"><span data-stu-id="20b06-126">View the public IP address information summary table</span></span>
<span data-ttu-id="20b06-127">指派公用 IP 位址時具有數種不同案例，可判斷位址是否顯示在一個 (或其他) 清單中。</span><span class="sxs-lookup"><span data-stu-id="20b06-127">There are a number of different cases in which public IP addresses are assigned that determine whether the address appears in one list or another.</span></span>

| <span data-ttu-id="20b06-128">**公用 IP 位址指派案例**</span><span class="sxs-lookup"><span data-stu-id="20b06-128">**Public IP address assignment case**</span></span> | <span data-ttu-id="20b06-129">**顯示於使用方式摘要**</span><span class="sxs-lookup"><span data-stu-id="20b06-129">**Appears in usage summary**</span></span> | <span data-ttu-id="20b06-130">**顯示於租用戶公用 IP 位址清單**</span><span class="sxs-lookup"><span data-stu-id="20b06-130">**Appears in tenant public IP addresses list**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20b06-131">尚未指派給 NIC 或負載平衡器 (暫時) 的動態公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="20b06-131">Dynamic public IP address not yet assigned to an NIC or load balancer (temporary)</span></span> |<span data-ttu-id="20b06-132">否</span><span class="sxs-lookup"><span data-stu-id="20b06-132">No</span></span> |<span data-ttu-id="20b06-133">是</span><span class="sxs-lookup"><span data-stu-id="20b06-133">Yes</span></span> |
| <span data-ttu-id="20b06-134">已指派給 NIC 或負載平衡器的動態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="20b06-134">Dynamic public IP address assigned to an NIC or load balancer.</span></span> |<span data-ttu-id="20b06-135">是</span><span class="sxs-lookup"><span data-stu-id="20b06-135">Yes</span></span> |<span data-ttu-id="20b06-136">是</span><span class="sxs-lookup"><span data-stu-id="20b06-136">Yes</span></span> |
| <span data-ttu-id="20b06-137">已指派給租用戶 NIC 或負載平衡器的靜態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="20b06-137">Static public IP address assigned to a tenant NIC or load balancer.</span></span> |<span data-ttu-id="20b06-138">是</span><span class="sxs-lookup"><span data-stu-id="20b06-138">Yes</span></span> |<span data-ttu-id="20b06-139">是</span><span class="sxs-lookup"><span data-stu-id="20b06-139">Yes</span></span> |
| <span data-ttu-id="20b06-140">已指派給網狀架構基礎結構服務端點的靜態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="20b06-140">Static public IP address assigned to a fabric infrastructure service endpoint.</span></span> |<span data-ttu-id="20b06-141">是</span><span class="sxs-lookup"><span data-stu-id="20b06-141">Yes</span></span> |<span data-ttu-id="20b06-142">否</span><span class="sxs-lookup"><span data-stu-id="20b06-142">No</span></span> |
| <span data-ttu-id="20b06-143">公用 IP 位址會以隱含方式針對 IaaS VM 執行個體而建立，並用於虛擬網路上的輸出 NAT。</span><span class="sxs-lookup"><span data-stu-id="20b06-143">Public IP address implicitly created for IaaS VM instances and used for outbound NAT on the virtual network.</span></span> <span data-ttu-id="20b06-144">每當租用戶建立 VM 執行個體，讓 VM 可以將資訊送出到網際網路時，這些位址便會在幕後建立。</span><span class="sxs-lookup"><span data-stu-id="20b06-144">These are created behind the scenes whenever a tenant creates a VM instance so that VMs can send information out to the Internet.</span></span> |<span data-ttu-id="20b06-145">是</span><span class="sxs-lookup"><span data-stu-id="20b06-145">Yes</span></span> |<span data-ttu-id="20b06-146">否</span><span class="sxs-lookup"><span data-stu-id="20b06-146">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20b06-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20b06-147">Next steps</span></span>
[<span data-ttu-id="20b06-148">在 Azure Stack 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="20b06-148">Manage Storage Accounts in Azure Stack</span></span>](azure-stack-manage-storage-accounts.md)