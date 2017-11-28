---
title: "取得 ARP 表格：Resource Manager：Azure ExpressRoute 疑難排解 | Microsoft Docs"
description: "此頁面提供相關指示，協助您取得適用於 ExpressRoute 線路的 ARP 表格"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="ac5d3-103">在 Resource Manager 部署模型中取得 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac5d3-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="ac5d3-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="ac5d3-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="ac5d3-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="ac5d3-106">本文將逐步引導您了解適用於 ExpressRoute 線路的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ac5d3-107">本文件旨在協助您診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="ac5d3-108">它無法取代 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="ac5d3-109">如果無法使用如下所述的指引來解決問題，您必須向 [Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="ac5d3-110">位址解析通訊協定 (ARP) 和 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="ac5d3-111">位址解析通訊協定 (ARP) 是 [RFC 826](https://tools.ietf.org/html/rfc826)中定義的第 2 層通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="ac5d3-112">ARP 可用於利用 IP 位址來對應乙太網路位址 (MAC 位址)。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="ac5d3-113">ARP 表格針對特定的對等互連提供 IPv4 位址與 MAC 位址的對應。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="ac5d3-114">適用於 ExpressRoute 線路對等互連的 ARP 表格會針對每個介面 (主要和次要) 提供下列資訊</span><span class="sxs-lookup"><span data-stu-id="ac5d3-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="ac5d3-115">內部部署路由器介面 IP 位址到 MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="ac5d3-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="ac5d3-116">ExpressRoute 路由器介面 IP 位址到 MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="ac5d3-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="ac5d3-117">對應的存留期</span><span class="sxs-lookup"><span data-stu-id="ac5d3-117">Age of the mapping</span></span>

<span data-ttu-id="ac5d3-118">ARP 表格可協助您驗證第 2 層組態，並為第 2 層的基礎連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="ac5d3-119">範例 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="ac5d3-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="ac5d3-120">下一節的資訊能為您說明如何檢視 ExpressRoute 邊緣路由器所看見的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="ac5d3-121">了解 ARP 表格的必要條件</span><span class="sxs-lookup"><span data-stu-id="ac5d3-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="ac5d3-122">進一步了解之前，請確定您符合下列條件</span><span class="sxs-lookup"><span data-stu-id="ac5d3-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="ac5d3-123">至少使用一個對等互連設定的有效 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="ac5d3-124">線路必須由連線提供者完全設定。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="ac5d3-125">您 (或您的連線提供者) 必須在這個線路上至少設定一個對等互連 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="ac5d3-126">用來設定對等互連 (Azure 私用、Azure 公用和 Microsoft) 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="ac5d3-127">檢閱 [ExpressRoute 路由需求頁面](expressroute-routing.md) 中的 IP 位址指派範例，以了解如何將 IP 位址對應到您所在處和 ExpressRoute 端上的介面。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="ac5d3-128">您可以藉由檢閱 [ExpressRoute 對等互連組態頁面](expressroute-howto-routing-arm.md)來取得對等互連組態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="ac5d3-129">在可與這些 IP 位址搭配使用的介面的 MAC 位址上，由網路小組 / 連線提供者所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="ac5d3-130">您必須擁有適用於 Azure 的最新 PowerShell 模組 (版本 1.50 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="ac5d3-131">取得適用於 ExpressRoute 線路的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="ac5d3-132">本節將指示您如何使用 PowerShell 來為每個對等互連檢視 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="ac5d3-133">您或您的連線提供者必須先設定對等互連，才能有進一步的進展。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="ac5d3-134">每個線路都有兩個路徑 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="ac5d3-135">您可以單獨檢查每個路徑的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="ac5d3-136">適用於 Azure 私用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="ac5d3-137">下列 Cmdlet 提供適用於 Azure 私用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="ac5d3-138">針對其中一個路徑的範例輸出如下所示</span><span class="sxs-lookup"><span data-stu-id="ac5d3-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="ac5d3-139">適用於 Azure 公用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="ac5d3-140">下列 Cmdlet 提供適用於 Azure 公用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="ac5d3-141">針對其中一個路徑的範例輸出如下所示</span><span class="sxs-lookup"><span data-stu-id="ac5d3-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="ac5d3-142">適用於 Microsoft 對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="ac5d3-143">下列 Cmdlet 提供適用於 Microsoft 對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="ac5d3-144">針對其中一個路徑的範例輸出如下所示</span><span class="sxs-lookup"><span data-stu-id="ac5d3-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="ac5d3-145">如何使用此資訊</span><span class="sxs-lookup"><span data-stu-id="ac5d3-145">How to use this information</span></span>
<span data-ttu-id="ac5d3-146">對等互連的 ARP 表格可用來決定驗證第 2 層組態與連線。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="ac5d3-147">本節將概述 ARP 表格在不同狀況下的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="ac5d3-148">當線路處於運作狀態 (預期狀態) 時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="ac5d3-149">ARP 表格必須有一個適用於內部部署端的項目，其中具備有效的 IP 位址和 MAC 位址，以及一個適用於 Microsoft 端的類似項目。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="ac5d3-150">內部部署 IP 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="ac5d3-151">Microsoft IP 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="ac5d3-152">同一個 MAC 位址將針對所有 3 個對等互連 (主要 / 次要) 出現在 Microsoft 端。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="ac5d3-153">當內部部署 / 連線提供者端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="ac5d3-154">如果內部部署或連線提供者發生問題，您可能會看到只有一個項目出現在 ARP 資料表中，或顯示的內部部署 MAC 位址不完整。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="ac5d3-155">並為 Microsoft 端所使用的 MAC 位址與 IP 位址顯示其間的對應。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="ac5d3-156">或</span><span class="sxs-lookup"><span data-stu-id="ac5d3-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="ac5d3-157">向連線提供者開啟支援要求，對這類問題進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="ac5d3-158">如果 ARP 表沒有對應到 MAC 位址之介面的 IP 位址，請檢閱下列條件︰</span><span class="sxs-lookup"><span data-stu-id="ac5d3-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="ac5d3-159">針對 MSEE-PR 和 MSEE 之間的連結所指派的 /30 子網路的第一個 IP 位址，是用在 MSEE-PR 的介面上。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="ac5d3-160">Azure 一律為 MSEE 使用第二個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="ac5d3-161">確認客戶 (C 標籤) 和服務 (S 標籤) VLAN 標籤是否都和「MSEE-PR 與 MSEE」對上的相符。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="ac5d3-162">當 Microsoft 端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="ac5d3-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="ac5d3-163">如果 Microsoft 端發生問題，您將不會看見針對對等互連顯示的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="ac5d3-164">向 [Microsoft 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="ac5d3-165">指出您發生第 2 層連線的問題。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ac5d3-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac5d3-166">Next Steps</span></span>
* <span data-ttu-id="ac5d3-167">針對您的 ExpressRoute 線路驗證第 3 層組態</span><span class="sxs-lookup"><span data-stu-id="ac5d3-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="ac5d3-168">取得路由摘要以判斷 BGP 工作階段的狀態</span><span class="sxs-lookup"><span data-stu-id="ac5d3-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="ac5d3-169">取得路由表以判斷哪些首碼是透過 ExpressRoute 來公告的</span><span class="sxs-lookup"><span data-stu-id="ac5d3-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="ac5d3-170">檢閱輸入 / 輸出的位元組來驗證資料傳輸</span><span class="sxs-lookup"><span data-stu-id="ac5d3-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="ac5d3-171">如果仍會發生問題，請向 [Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="ac5d3-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

