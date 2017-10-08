---
title: "取得 ARP 表格：傳統：Azure ExpressRoute 疑難排解 | Microsoft Docs"
description: "此頁面提供指示取得 hello ARP 表格的 ExpressRoute 電路。"
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="afd38-103">取得 ARP hello 傳統部署模型中的資料表</span><span class="sxs-lookup"><span data-stu-id="afd38-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afd38-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="afd38-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="afd38-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="afd38-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="afd38-106">這篇文章會引導您 hello 步驟為您的 Azure ExpressRoute 電路取得 hello 位址解析通訊協定 (ARP) 的資料表。</span><span class="sxs-lookup"><span data-stu-id="afd38-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afd38-107">本文件是預定的 toohelp 您診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="afd38-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="afd38-108">它不是預期的 toobe Microsoft 支援的取代項目。</span><span class="sxs-lookup"><span data-stu-id="afd38-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="afd38-109">如果您無法使用下列指導方針的 hello 解決 hello 問題，開啟支援要求使用[Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="afd38-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="afd38-110">位址解析通訊協定 (ARP) 和 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="afd38-111">ARP 是在 [RFC 826](https://tools.ietf.org/html/rfc826)中定義的第 2 層通訊協定。</span><span class="sxs-lookup"><span data-stu-id="afd38-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="afd38-112">ARP 是使用的 toomap 乙太網路位址 （MAC 位址） tooan IP 位址。</span><span class="sxs-lookup"><span data-stu-id="afd38-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="afd38-113">ARP 表格提供 hello IPv4 位址和 MAC 位址的特定的對等互連的對應。</span><span class="sxs-lookup"><span data-stu-id="afd38-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="afd38-114">hello 的 ExpressRoute 電路對等體的 ARP 表格提供下列資訊為每個介面 （主要和次要） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="afd38-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="afd38-115">在內部部署路由器介面 IP 位址 tooa MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="afd38-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="afd38-116">ExpressRoute 路由器介面 IP 位址 tooa MAC 位址的對應</span><span class="sxs-lookup"><span data-stu-id="afd38-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="afd38-117">hello hello 對應存留期</span><span class="sxs-lookup"><span data-stu-id="afd38-117">hello age of hello mapping</span></span>

<span data-ttu-id="afd38-118">ARP 表格可協助您驗證第 2 層組態，並針對基本的第 2 層連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="afd38-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="afd38-119">以下是 ARP 表格的範例：</span><span class="sxs-lookup"><span data-stu-id="afd38-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="afd38-120">hello 之後 > 一節提供有關如何 tooview hello 看到 hello ExpressRoute 邊緣路由器的 ARP 資料表資訊。</span><span class="sxs-lookup"><span data-stu-id="afd38-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="afd38-121">使用 ARP 表格的必要條件</span><span class="sxs-lookup"><span data-stu-id="afd38-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="afd38-122">請確定您擁有 hello 下列，才能繼續進行：</span><span class="sxs-lookup"><span data-stu-id="afd38-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="afd38-123">至少使用一個對等互連設定的有效 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="afd38-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="afd38-124">hello 電路必須完全設定 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="afd38-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="afd38-125">您 （或您連線服務提供者） 必須至少一個 hello 對等互連 （Azure 的私用、 Azure 公用或 Microsoft） 上設定這個循環。</span><span class="sxs-lookup"><span data-stu-id="afd38-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="afd38-126">用來設定 hello 對等互連 （Azure 的私用、 Azure 公用和 Microsoft） 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="afd38-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="afd38-127">檢閱在 hello hello IP 位址指派範例[ExpressRoute 路由需求 頁面](expressroute-routing.md)tooget 了解 IP 位址的方式對應 toointerfaces 您 aise 和 hello ExpressRoute 端上。</span><span class="sxs-lookup"><span data-stu-id="afd38-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="afd38-128">您可以藉由檢閱 hello 取得 hello 對等組態資訊[ExpressRoute 對等組態 頁面上](expressroute-howto-routing-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="afd38-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="afd38-129">從您網路的小組或連線提供者的相關資訊 hello MAC 位址 hello 用的介面，這些 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="afd38-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="afd38-130">hello 最新的 Windows PowerShell 模組 Azure （1.50 或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="afd38-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="afd38-131">適用於 ExpressRoute 線路的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="afd38-132">本節提供有關如何 tooview hello ARP 資料表的每一種使用 PowerShell 對等互連的指示。</span><span class="sxs-lookup"><span data-stu-id="afd38-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="afd38-133">在繼續之前，您或您連線服務提供者會需要 tooconfigure hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="afd38-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="afd38-134">每個線路都有兩個路徑 (主要和次要)。</span><span class="sxs-lookup"><span data-stu-id="afd38-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="afd38-135">您可以獨立檢查 hello ARP 表格的每個路徑。</span><span class="sxs-lookup"><span data-stu-id="afd38-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="afd38-136">適用於 Azure 私用對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="afd38-137">下列指令程式的 hello 提供用於 Azure 私人互連 hello ARP 資料表：</span><span class="sxs-lookup"><span data-stu-id="afd38-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="afd38-138">以下是其中一個 hello 路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="afd38-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="afd38-139">適用於 Azure 公用對等互連的 ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="afd38-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="afd38-140">下列指令程式的 hello 提供 Azure 公用對等 hello ARP 表格：</span><span class="sxs-lookup"><span data-stu-id="afd38-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="afd38-141">以下是其中一個 hello 路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="afd38-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="afd38-142">以下是其中一個 hello 路徑的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="afd38-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="afd38-143">適用於 Microsoft 對等互連的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="afd38-144">下列指令程式的 hello 提供的 Microsoft 對等互連 hello ARP 資料表：</span><span class="sxs-lookup"><span data-stu-id="afd38-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="afd38-145">範例輸出如下所示的其中一個 hello 路徑：</span><span class="sxs-lookup"><span data-stu-id="afd38-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="afd38-146">如何 toouse 這項資訊</span><span class="sxs-lookup"><span data-stu-id="afd38-146">How toouse this information</span></span>
<span data-ttu-id="afd38-147">hello 對等互連的 ARP 表格可以使用的 toovalidate 第 2 層設定與連線能力。</span><span class="sxs-lookup"><span data-stu-id="afd38-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="afd38-148">本節提供在不同狀況下 ARP 表格呈現方式的概觀。</span><span class="sxs-lookup"><span data-stu-id="afd38-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="afd38-149">當線路處於運作 (預期) 狀態時的 ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="afd38-150">hello ARP 表格有 hello 內部端具有有效 IP 和 MAC 位址，項目，而且 hello Microsoft 側邊的類似項目。</span><span class="sxs-lookup"><span data-stu-id="afd38-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="afd38-151">hello hello 內部 IP 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="afd38-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="afd38-152">hello Microsoft IP 位址的最後一個八位元一律是 hello 的偶數。</span><span class="sxs-lookup"><span data-stu-id="afd38-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="afd38-153">相同的 MAC 位址會出現在所有三個互連 （主要/次要） 的 Microsoft 戶端 hello hello。</span><span class="sxs-lookup"><span data-stu-id="afd38-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="afd38-154">在內部部署或當 hello 連線服務提供者端有問題時，ARP 表格</span><span class="sxs-lookup"><span data-stu-id="afd38-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="afd38-155">只有一個項目會出現在 hello ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="afd38-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="afd38-156">它會顯示 hello hello MAC 位址與 hello hello Microsoft 端使用的 IP 位址之間的對應。</span><span class="sxs-lookup"><span data-stu-id="afd38-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="afd38-157">如果您遇到像這樣的問題，請開啟支援要求與您的連線提供者 tooresolve 它。</span><span class="sxs-lookup"><span data-stu-id="afd38-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="afd38-158">ARP 表格時 hello Microsoft 側邊有問題</span><span class="sxs-lookup"><span data-stu-id="afd38-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="afd38-159">您不會看到顯示對等互連 hello Microsoft 端上有問題時 ARP 表格。</span><span class="sxs-lookup"><span data-stu-id="afd38-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="afd38-160">向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="afd38-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="afd38-161">指出您發生第 2 層連線的問題。</span><span class="sxs-lookup"><span data-stu-id="afd38-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afd38-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afd38-162">Next steps</span></span>
* <span data-ttu-id="afd38-163">驗證 ExpressRoute 線路的第 3 層組態：</span><span class="sxs-lookup"><span data-stu-id="afd38-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="afd38-164">取得路由摘要 toodetermine hello 狀態的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="afd38-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="afd38-165">取得路由表 toodetermine 的前置詞會透過 ExpressRoute 通告。</span><span class="sxs-lookup"><span data-stu-id="afd38-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="afd38-166">檢閱輸入和輸出的位元組來驗證資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="afd38-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="afd38-167">如果問題持續發生，請向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="afd38-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

