---
title: "取得 ARP 表格：傳統：Azure ExpressRoute 疑難排解 | Microsoft Docs"
description: "此頁面提供取得適用於 ExpressRoute 線路之 ARP 表格的相關指示。"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="91da4-103">在傳統部署模型中取得 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91da4-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="91da4-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="91da4-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="91da4-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="91da4-106">本文章會引導您逐步完成取得 Azure ExpressRoute 電路之位址解析通訊協定 (ARP) 表格的步驟。</span><span class="sxs-lookup"><span data-stu-id="91da4-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91da4-107">本文件旨在協助您診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="91da4-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="91da4-108">它無法取代 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="91da4-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="91da4-109">如果以下指導方針無法解決問題，請向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="91da4-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="91da4-110">位址解析通訊協定 (ARP) 和 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="91da4-111">ARP 是在 [RFC 826](https://tools.ietf.org/html/rfc826)中定義的第 2 層通訊協定。</span><span class="sxs-lookup"><span data-stu-id="91da4-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="91da4-112">ARP 可用於對應乙太網路位址 (MAC 位址) 與 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="91da4-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="91da4-113">ARP 表格能針對特定的對等互連提供 IPv4 位址與 MAC 位址對應。</span><span class="sxs-lookup"><span data-stu-id="91da4-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="91da4-114">適用於 ExpressRoute 線路對等互連的 ARP 表格能提供各個介面 (主要和次要) 的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="91da4-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="91da4-115">內部部署路由器介面 IP 位址與 MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="91da4-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="91da4-116">ExpressRoute 路由器介面 IP 位址與 MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="91da4-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="91da4-117">對應的存留期</span><span class="sxs-lookup"><span data-stu-id="91da4-117">The age of the mapping</span></span>

<span data-ttu-id="91da4-118">ARP 表格可協助您驗證第 2 層組態，並針對基本的第 2 層連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="91da4-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="91da4-119">以下是 ARP 表格的範例：</span><span class="sxs-lookup"><span data-stu-id="91da4-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="91da4-120">下節提供的資訊有關如何檢視 ExpressRoute 邊緣路由器所見的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="91da4-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="91da4-121">使用 ARP 表格的必要條件</span><span class="sxs-lookup"><span data-stu-id="91da4-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="91da4-122">繼續操作之前，請確定您已備妥以下必要條件：</span><span class="sxs-lookup"><span data-stu-id="91da4-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="91da4-123">至少使用一個對等互連設定的有效 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="91da4-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="91da4-124">線路必須由連線提供者完全設定。</span><span class="sxs-lookup"><span data-stu-id="91da4-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="91da4-125">您 (或您的連線提供者) 必須在這個線路上至少設定一個對等互連 (Azure 私用、Azure 公用或 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="91da4-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="91da4-126">用來設定對等互連 (Azure 私用、Azure 公用和 Microsoft) 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="91da4-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="91da4-127">檢閱 [ExpressRoute 路由需求頁面](expressroute-routing.md) 中的 IP 位址指派範例，以了解如何將 IP 位址對應到您的 aise 和 ExpressRoute 端上的介面。</span><span class="sxs-lookup"><span data-stu-id="91da4-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="91da4-128">您可以藉由檢閱 [ExpressRoute 對等互連組態頁面](expressroute-howto-routing-classic.md)來取得對等互連組態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="91da4-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="91da4-129">由網路團隊或連線提供者所提供的資訊，其與這些 IP 位址搭配使用之介面的 MAC 位址相關。</span><span class="sxs-lookup"><span data-stu-id="91da4-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="91da4-130">適用於 Azure 的最新 Windows PowerShell 模組 (1.50 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="91da4-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="91da4-131">適用於 ExpressRoute 線路的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="91da4-132">本節提供如何使用 PowerShell 檢視各種對等互連之 ARP 表格的指示。</span><span class="sxs-lookup"><span data-stu-id="91da4-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="91da4-133">在繼續之前，您或您的連線提供者需要設定對等互連。</span><span class="sxs-lookup"><span data-stu-id="91da4-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="91da4-134">每個線路都有兩個路徑 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="91da4-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="91da4-135">您可以單獨檢查每個路徑的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="91da4-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="91da4-136">適用於 Azure 私用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="91da4-137">下列 Cmdlet 提供適用於 Azure 私用對等互連的 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="91da4-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="91da4-138">以下是其中一個路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="91da4-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="91da4-139">適用於 Azure 公用對等互連的 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="91da4-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="91da4-140">下列 Cmdlet 提供適用於 Azure 公用對等互連的 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="91da4-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="91da4-141">以下是其中一個路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="91da4-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="91da4-142">以下是其中一個路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="91da4-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="91da4-143">適用於 Microsoft 對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="91da4-144">下列 Cmdlet 提供適用於 Microsoft 對等互連的 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="91da4-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="91da4-145">其中一個路徑的範例輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="91da4-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="91da4-146">如何使用此資訊</span><span class="sxs-lookup"><span data-stu-id="91da4-146">How to use this information</span></span>
<span data-ttu-id="91da4-147">對等互連的 ARP 表格可用來驗證第 2 層組態與連線。</span><span class="sxs-lookup"><span data-stu-id="91da4-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="91da4-148">本節提供在不同狀況下 ARP 表格呈現方式的概觀。</span><span class="sxs-lookup"><span data-stu-id="91da4-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="91da4-149">當線路處於運作 (預期) 狀態時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="91da4-150">ARP 表格有一個適用於內部部署端的項目，其中具備有效的 IP 和 MAC 位址，以及一個適用於 Microsoft 端的類似項目。</span><span class="sxs-lookup"><span data-stu-id="91da4-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="91da4-151">內部部署 IP 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="91da4-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="91da4-152">Microsoft IP 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="91da4-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="91da4-153">同一個 MAC 位址會出現這三個對等互連 (主要 / 次要) 的 Microsoft 端。</span><span class="sxs-lookup"><span data-stu-id="91da4-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="91da4-154">當內部部署 / 連線提供者端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="91da4-155">ARP 表格中只會出現一個項目。</span><span class="sxs-lookup"><span data-stu-id="91da4-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="91da4-156">它會顯示 Microsoft 端使用之 MAC 位址與 IP 位址的對應。</span><span class="sxs-lookup"><span data-stu-id="91da4-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="91da4-157">如果您遇到像這樣的問題，請向連線提供者開啟支援要求以尋求解決。</span><span class="sxs-lookup"><span data-stu-id="91da4-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="91da4-158">當 Microsoft 端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="91da4-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="91da4-159">如果 Microsoft 端發生問題，您將不會看見針對對等互連顯示的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="91da4-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="91da4-160">向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="91da4-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="91da4-161">指出您發生第 2 層連線的問題。</span><span class="sxs-lookup"><span data-stu-id="91da4-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91da4-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91da4-162">Next steps</span></span>
* <span data-ttu-id="91da4-163">驗證 ExpressRoute 線路的第 3 層組態：</span><span class="sxs-lookup"><span data-stu-id="91da4-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="91da4-164">取得路由摘要以判斷 BGP 工作階段的狀態。</span><span class="sxs-lookup"><span data-stu-id="91da4-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="91da4-165">取得路由表以判斷哪些首碼是透過 ExpressRoute 來公告。</span><span class="sxs-lookup"><span data-stu-id="91da4-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="91da4-166">檢閱輸入和輸出的位元組來驗證資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="91da4-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="91da4-167">如果問題持續發生，請向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="91da4-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

