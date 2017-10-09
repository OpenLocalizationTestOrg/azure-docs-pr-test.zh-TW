---
title: "取得 ARP 表格：Resource Manager：Azure ExpressRoute 疑難排解 | Microsoft Docs"
description: "此頁面提供指示取得 hello ARP 表格的 ExpressRoute 電路"
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="9826c-103">取得 ARP hello Resource Manager 部署模型中的資料表</span><span class="sxs-lookup"><span data-stu-id="9826c-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9826c-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="9826c-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="9826c-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="9826c-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="9826c-106">這篇文章會引導您 hello 步驟 toolearn hello ARP 資料表的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9826c-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9826c-107">本文件是預定的 toohelp 您診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="9826c-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="9826c-108">它不是預期的 toobe Microsoft 支援的取代項目。</span><span class="sxs-lookup"><span data-stu-id="9826c-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="9826c-109">您必須開啟支援票證給[Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)如果您是使用如下所述的 hello 指引無法 toosolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="9826c-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="9826c-110">位址解析通訊協定 (ARP) 和 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="9826c-111">位址解析通訊協定 (ARP) 是 [RFC 826](https://tools.ietf.org/html/rfc826)中定義的第 2 層通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9826c-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="9826c-112">ARP 是使用的 toomap hello 的 ip 位址的乙太網路位址 （MAC 位址）。</span><span class="sxs-lookup"><span data-stu-id="9826c-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="9826c-113">hello ARP 表格提供 hello ipv4 位址和 MAC 位址的特定的對等互連的對應。</span><span class="sxs-lookup"><span data-stu-id="9826c-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="9826c-114">hello 的 ExpressRoute 電路對等體的 ARP 表格提供下列資訊為每個介面 （主要和次要） 的 hello</span><span class="sxs-lookup"><span data-stu-id="9826c-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="9826c-115">在內部部署路由器介面 ip 位址 toohello MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="9826c-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="9826c-116">ExpressRoute 路由器介面 ip 位址 toohello MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="9826c-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="9826c-117">Hello 對應的存留期</span><span class="sxs-lookup"><span data-stu-id="9826c-117">Age of hello mapping</span></span>

<span data-ttu-id="9826c-118">ARP 表格可協助您驗證第 2 層組態，並為第 2 層的基礎連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9826c-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="9826c-119">範例 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="9826c-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="9826c-120">hello 下列章節提供有關如何檢視 hello 看到 hello ExpressRoute 邊緣路由器的 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="9826c-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="9826c-121">了解 ARP 表格的必要條件</span><span class="sxs-lookup"><span data-stu-id="9826c-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="9826c-122">請確定您有 hello 遵循您繼續升級之前</span><span class="sxs-lookup"><span data-stu-id="9826c-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="9826c-123">至少使用一個對等互連設定的有效 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="9826c-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="9826c-124">hello 電路必須完全設定 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="9826c-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="9826c-125">您 （或您連線服務提供者） 必須有至少一個 hello 對等互連 （Azure 私用、 Azure 公用和 Microsoft） 上設定這個循環。</span><span class="sxs-lookup"><span data-stu-id="9826c-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="9826c-126">用來設定 hello 對等互連 （Azure 私用、 Azure 公用和 Microsoft） 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="9826c-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="9826c-127">檢閱在 hello hello ip 位址指派範例[ExpressRoute 路由需求 頁面](expressroute-routing.md)tooget 了解 ip 位址的方式對應 toointerfaces 您身邊和 hello ExpressRoute 端上。</span><span class="sxs-lookup"><span data-stu-id="9826c-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="9826c-128">您可以取得 hello 對等設定的詳細資訊，藉由檢閱 hello [ExpressRoute 對等組態 頁面上](expressroute-howto-routing-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="9826c-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="9826c-129">從網路團隊資訊 / hello MAC 位址的介面上的連線服務提供者搭配這些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9826c-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="9826c-130">您必須擁有最新 PowerShell 模組 hello azure （1.50 或較新版本）。</span><span class="sxs-lookup"><span data-stu-id="9826c-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="9826c-131">取得資料表 hello ARP ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="9826c-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="9826c-132">本節提供有關如何檢視 hello ARP 資料表每個對等互連使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9826c-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="9826c-133">您或您連線服務提供者必須已設定之前進行進一步的 hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="9826c-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="9826c-134">每個線路都有兩個路徑 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="9826c-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="9826c-135">您可以獨立檢查 hello ARP 表格的每個路徑。</span><span class="sxs-lookup"><span data-stu-id="9826c-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="9826c-136">適用於 Azure 私用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="9826c-137">下列 cmdlet 的 hello 提供 hello ARP 表格用於 Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="9826c-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="9826c-138">範例輸出如下所示的其中一個 hello 路徑</span><span class="sxs-lookup"><span data-stu-id="9826c-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="9826c-139">適用於 Azure 公用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="9826c-140">下列指令程式的 hello 提供 hello ARP 表格 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="9826c-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="9826c-141">範例輸出如下所示的其中一個 hello 路徑</span><span class="sxs-lookup"><span data-stu-id="9826c-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="9826c-142">適用於 Microsoft 對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="9826c-143">下列 cmdlet 的 hello 提供 hello ARP 表格的 Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="9826c-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="9826c-144">範例輸出如下所示的其中一個 hello 路徑</span><span class="sxs-lookup"><span data-stu-id="9826c-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="9826c-145">如何 toouse 這項資訊</span><span class="sxs-lookup"><span data-stu-id="9826c-145">How toouse this information</span></span>
<span data-ttu-id="9826c-146">hello ARP 表格的對等互連可用 toodetermine 驗證第 2 層設定與連線能力。</span><span class="sxs-lookup"><span data-stu-id="9826c-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="9826c-147">本節將概述 ARP 表格在不同狀況下的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="9826c-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="9826c-148">當線路處於運作狀態 (預期狀態) 時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="9826c-149">hello ARP 資料表必須使用有效的 IP 位址和 MAC 位址的 hello 內部端項目，而且 hello Microsoft 側邊的類似項目。</span><span class="sxs-lookup"><span data-stu-id="9826c-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="9826c-150">hello hello 內部 ip 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="9826c-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="9826c-151">hello Microsoft ip 位址的最後一個八位元一定是 hello 的偶數。</span><span class="sxs-lookup"><span data-stu-id="9826c-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="9826c-152">相同的 MAC 位址會出現在 hello 所有 3 對等互連 （主要 / 次要） 的 Microsoft 戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="9826c-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="9826c-153">當內部部署 / 連線提供者端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="9826c-154">如果有與 hello 內部的問題或您可能會看到，可能是只有一個項目會出現在 hello ARP 表格或 hello 內部 MAC 位址的連線服務提供者將會顯示不完整。</span><span class="sxs-lookup"><span data-stu-id="9826c-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="9826c-155">這會顯示 hello hello MAC 位址和 IP 位址用於 hello Microsoft 側邊之間的對應。</span><span class="sxs-lookup"><span data-stu-id="9826c-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="9826c-156">或</span><span class="sxs-lookup"><span data-stu-id="9826c-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="9826c-157">開啟支援要求與您的連線提供者 toodebug 這類問題。</span><span class="sxs-lookup"><span data-stu-id="9826c-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="9826c-158">如果沒有 hello ARP 表格 hello 介面的 IP 位址對應 tooMAC 位址，檢閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="9826c-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="9826c-159">如果 hello/30 子網路的 hello 第一個 IP 位址指派 hello 連結之間 hello MSEE PR 並用 MSEE MSEE PR hello 介面上</span><span class="sxs-lookup"><span data-stu-id="9826c-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="9826c-160">Azure 一律使用 MSEEs hello 第二個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9826c-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="9826c-161">請確認是否 hello 客戶 （C-已標記） 和服務 （S 已標記） 的 VLAN 標記符合二者 MSEE PR 和 MSEE 組。</span><span class="sxs-lookup"><span data-stu-id="9826c-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="9826c-162">當 Microsoft 端發生問題時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="9826c-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="9826c-163">您不會看到顯示對等互連 hello Microsoft 端上有問題時 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="9826c-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="9826c-164">向 [Microsoft 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="9826c-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="9826c-165">指出您發生第 2 層連線的問題。</span><span class="sxs-lookup"><span data-stu-id="9826c-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9826c-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9826c-166">Next Steps</span></span>
* <span data-ttu-id="9826c-167">針對您的 ExpressRoute 線路驗證第 3 層組態</span><span class="sxs-lookup"><span data-stu-id="9826c-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="9826c-168">取得路由的 BGP 工作階段的摘要 toodetermine hello 狀態</span><span class="sxs-lookup"><span data-stu-id="9826c-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="9826c-169">取得的前置詞會透過 ExpressRoute 通告的路由表 toodetermine</span><span class="sxs-lookup"><span data-stu-id="9826c-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="9826c-170">檢閱輸入 / 輸出的位元組來驗證資料傳輸</span><span class="sxs-lookup"><span data-stu-id="9826c-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="9826c-171">如果仍會發生問題，請向 [Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="9826c-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

