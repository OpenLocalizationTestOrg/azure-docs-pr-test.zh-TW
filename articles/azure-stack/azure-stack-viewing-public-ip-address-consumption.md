---
title: "aaaView 公用 IP 位址消耗 Azure 堆疊 |Microsoft 文件"
description: "系統管理員可以檢視區域中的 hello 耗用量的公用 IP 位址"
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
ms.openlocfilehash: 771c011d133a030218b011cf94bbb8055f8996ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a><span data-ttu-id="c1fd4-103">檢視 Azure Stack 中的公用 IP 位址使用</span><span class="sxs-lookup"><span data-stu-id="c1fd4-103">View public IP address consumption in Azure Stack</span></span>
<span data-ttu-id="c1fd4-104">是雲端系統管理員，您可以檢視 hello tootenants hello 仍然可供配置的公用 IP 位址的數目和中的已配置的公用 IP 位址的 hello 百分比已配置的公用 IP 位址數目位置。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-104">As a cloud administrator, you can view hello number of public IP addresses that have been allocated tootenants, hello number of public IP addresses that are still available for allocation, and hello percentage of public IP addresses that have been allocated in that location.</span></span>

<span data-ttu-id="c1fd4-105">hello**公用 IP 集區使用量**磚會顯示 hello 總數已取用所有公用的 IP 位址集區，在 hello 光纖上的公用 IP 位址是否已用過的租用戶 IaaS VM 執行個體，網狀架構基礎結構服務或所明確建立的租用戶的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-105">hello **Public IP pools usage** tile shows hello total number of public IP addresses that have been consumed across all public IP address pools on hello fabric, whether they have been used for tenant IaaS VM instances, fabric infrastructure services, or public IP address resources that were explicitly created by tenants.</span></span>

<span data-ttu-id="c1fd4-106">hello 這個磚的目的是 toogive Azure 堆疊 administrators 的 hello 已耗用在這個位置的公用 IP 位址的總次數。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-106">hello purpose of this tile is toogive Azure Stack administrators a sense of hello overall number of public IP addresses that have been consumed in this location.</span></span> <span data-ttu-id="c1fd4-107">這可協助系統管理員判斷其是否即將耗盡此資源。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-107">This helps administrators determine whether they are running low on this resource.</span></span>

<span data-ttu-id="c1fd4-108">在 hello**資源提供者**，**網路**刀鋒視窗，hello**公用 IP 位址**下的功能表項目**租用戶資源**只列出公用 IP 位址已*明確建立租用戶*。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-108">On hello **Resource providers**, **Network** blade, hello **Public IP addresses** menu item under **Tenant Resources** lists only those public IP addresses that have been *explicitly created by tenants*.</span></span> <span data-ttu-id="c1fd4-109">因此，hello 數目**用於**hello 上的公用 IP 位址**公用 IP 集區使用量**磚永遠是不同 （大於） hello hello 上的數字**公用 IP 位址**下圖格**租用戶資源**。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-109">As such, hello number of **Used** public IP addresses on hello **Public IP pools usage** tile is always different from (larger than) hello number on hello **Public IP Addresses** tile under **Tenant Resources**.</span></span>

## <a name="view-hello-public-ip-address-usage-information"></a><span data-ttu-id="c1fd4-110">檢視 hello 公用 IP 位址使用狀況資訊</span><span class="sxs-lookup"><span data-stu-id="c1fd4-110">View hello public IP address usage information</span></span>
<span data-ttu-id="c1fd4-111">tooview hello 的總數已取用 hello 區域中的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="c1fd4-111">tooview hello total number of public IP addresses that have been consumed in hello region:</span></span>

1. <span data-ttu-id="c1fd4-112">在 hello Azure 堆疊管理員入口網站，按一下 **更多服務**下**管理資源**，按一下**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-112">In hello Azure Stack administrator portal, click **More services**, under **Administrative Resources**, click **Resource providers**.</span></span>
2. <span data-ttu-id="c1fd4-113">從 hello 清單**資源提供者**，選取**網路**。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-113">From hello list of **Resource Providers**, select **Network**.</span></span>
3. <span data-ttu-id="c1fd4-114">hello**網路**刀鋒視窗會顯示 hello**公用 IP 集區使用量**磚中 hello**概觀**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-114">hello **Network** blade displays hello **Public IP pools usage** tile in hello **Overview** section.</span></span>

![網路資源提供者刀鋒視窗](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

<span data-ttu-id="c1fd4-116">請記住該 hello**用於**數字代表 hello 的公用 IP 位址數目，從所有公用 IP 位址集區的位置指派。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-116">Keep in mind that hello **Used** number represents hello number of public IP addresses from all public IP address pools in that location that are assigned.</span></span> <span data-ttu-id="c1fd4-117">hello**免費**數字代表 hello 的所有公用 IP 位址集區未指派，而且仍然可以使用從公用 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-117">hello **Free** number represents hello number of public IP addresses from all public IP address pools that have not been assigned and are still available.</span></span> <span data-ttu-id="c1fd4-118">hello **%used**數字代表 hello 數目，使用或指派位址的所有公用的 IP 位址集區，在該位置中的公用 IP 位址的 hello 總數的百分比。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-118">hello **% Used** number represents hello number of used or assigned addresses as a percentage of hello total number of public IP addresses in all public IP address pools in that location.</span></span>

## <a name="view-hello-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a><span data-ttu-id="c1fd4-119">檢視 hello 公用 IP 位址所建立的租用戶訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c1fd4-119">View hello public IP addresses that were created by tenant subscriptions</span></span>
<span data-ttu-id="c1fd4-120">toosee 清單的公用 IP 位址所明確建立的租用戶訂用帳戶，在特定區域中，按一下**公用 IP 位址**下**租用戶資源**。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-120">toosee a list of public IP addresses that were explicitly created by tenant subscriptions in a specific region, click **Public IP addresses** under **Tenant Resources**.</span></span>

![租用戶公用 IP 位址](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

<span data-ttu-id="c1fd4-122">您可能會注意到某些已動態配置的公用 IP 位址會出現在 hello 清單，但沒有尚未與其相關聯的位址。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-122">You might notice that some public IP addresses that have been dynamically allocated appear in hello list but do not have an address associated with them yet.</span></span> <span data-ttu-id="c1fd4-123">這是因為 hello 位址資源網路資源提供者，但不是在 hello 網路控制卡尚未建立。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-123">This is because hello address resource has been created in the Network Resource Provider, but not in hello Network Controller yet.</span></span>

<span data-ttu-id="c1fd4-124">hello 網路控制卡不會指派一個位址 toothis 資源，直到實際繫結的 tooan 介面、 網路介面卡 (NIC)、 負載平衡器或虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-124">hello Network Controller does not assign an address toothis resource until it is actually bound tooan interface, a network interface card (NIC), a load balancer, or a virtual network gateway.</span></span> <span data-ttu-id="c1fd4-125">Hello 公用 IP 位址是繫結的 tooan 介面、 hello 網路控制卡配置 IP 位址 tooit，並出現在 hello**位址**欄位。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-125">When hello public IP address is bound tooan interface, hello Network Controller allocates an IP address tooit, and it appears in hello **Address** field.</span></span>

## <a name="view-hello-public-ip-address-information-summary-table"></a><span data-ttu-id="c1fd4-126">檢視 hello 公用 IP 位址資訊摘要表格</span><span class="sxs-lookup"><span data-stu-id="c1fd4-126">View hello public IP address information summary table</span></span>
<span data-ttu-id="c1fd4-127">有不同的案例數目的公用 IP 位址會指派判斷 hello 位址是否出現在一個清單，或另一個。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-127">There are a number of different cases in which public IP addresses are assigned that determine whether hello address appears in one list or another.</span></span>

| <span data-ttu-id="c1fd4-128">**公用 IP 位址指派案例**</span><span class="sxs-lookup"><span data-stu-id="c1fd4-128">**Public IP address assignment case**</span></span> | <span data-ttu-id="c1fd4-129">**顯示於使用方式摘要**</span><span class="sxs-lookup"><span data-stu-id="c1fd4-129">**Appears in usage summary**</span></span> | <span data-ttu-id="c1fd4-130">**顯示於租用戶公用 IP 位址清單**</span><span class="sxs-lookup"><span data-stu-id="c1fd4-130">**Appears in tenant public IP addresses list**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1fd4-131">動態公用 IP 位址尚未指派 tooan NIC 或負載平衡器 （暫時）</span><span class="sxs-lookup"><span data-stu-id="c1fd4-131">Dynamic public IP address not yet assigned tooan NIC or load balancer (temporary)</span></span> |<span data-ttu-id="c1fd4-132">否</span><span class="sxs-lookup"><span data-stu-id="c1fd4-132">No</span></span> |<span data-ttu-id="c1fd4-133">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-133">Yes</span></span> |
| <span data-ttu-id="c1fd4-134">動態公用 IP 位址指派 tooan NIC 或負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-134">Dynamic public IP address assigned tooan NIC or load balancer.</span></span> |<span data-ttu-id="c1fd4-135">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-135">Yes</span></span> |<span data-ttu-id="c1fd4-136">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-136">Yes</span></span> |
| <span data-ttu-id="c1fd4-137">靜態公用 IP 位址指派 tooa 租用戶 NIC 或負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-137">Static public IP address assigned tooa tenant NIC or load balancer.</span></span> |<span data-ttu-id="c1fd4-138">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-138">Yes</span></span> |<span data-ttu-id="c1fd4-139">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-139">Yes</span></span> |
| <span data-ttu-id="c1fd4-140">靜態公用 IP 位址指派 tooa 網狀架構基礎結構服務端點。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-140">Static public IP address assigned tooa fabric infrastructure service endpoint.</span></span> |<span data-ttu-id="c1fd4-141">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-141">Yes</span></span> |<span data-ttu-id="c1fd4-142">否</span><span class="sxs-lookup"><span data-stu-id="c1fd4-142">No</span></span> |
| <span data-ttu-id="c1fd4-143">公用 IP 位址以隱含方式建立 IaaS VM 執行個體，並用於 hello 虛擬網路上的輸出 NAT。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-143">Public IP address implicitly created for IaaS VM instances and used for outbound NAT on hello virtual network.</span></span> <span data-ttu-id="c1fd4-144">這些被建立 hello 幕後每當租用戶建立 VM 執行個體，讓 Vm 可以傳送出 toohello 網際網路的資訊。</span><span class="sxs-lookup"><span data-stu-id="c1fd4-144">These are created behind hello scenes whenever a tenant creates a VM instance so that VMs can send information out toohello Internet.</span></span> |<span data-ttu-id="c1fd4-145">是</span><span class="sxs-lookup"><span data-stu-id="c1fd4-145">Yes</span></span> |<span data-ttu-id="c1fd4-146">否</span><span class="sxs-lookup"><span data-stu-id="c1fd4-146">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1fd4-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1fd4-147">Next steps</span></span>
[<span data-ttu-id="c1fd4-148">在 Azure Stack 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c1fd4-148">Manage Storage Accounts in Azure Stack</span></span>](azure-stack-manage-storage-accounts.md)