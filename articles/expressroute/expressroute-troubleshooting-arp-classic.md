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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>取得 ARP hello 傳統部署模型中的資料表
> [!div class="op_single_selector"]
> * [PowerShell - 資源管理員](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - 傳統](expressroute-troubleshooting-arp-classic.md)
> 
> 

這篇文章會引導您 hello 步驟為您的 Azure ExpressRoute 電路取得 hello 位址解析通訊協定 (ARP) 的資料表。

> [!IMPORTANT]
> 本文件是預定的 toohelp 您診斷並修正簡單的問題。 它不是預期的 toobe Microsoft 支援的取代項目。 如果您無法使用下列指導方針的 hello 解決 hello 問題，開啟支援要求使用[Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>位址解析通訊協定 (ARP) 和 ARP 表格
ARP 是在 [RFC 826](https://tools.ietf.org/html/rfc826)中定義的第 2 層通訊協定。 ARP 是使用的 toomap 乙太網路位址 （MAC 位址） tooan IP 位址。

ARP 表格提供 hello IPv4 位址和 MAC 位址的特定的對等互連的對應。 hello 的 ExpressRoute 電路對等體的 ARP 表格提供下列資訊為每個介面 （主要和次要） 的 hello:

1. 在內部部署路由器介面 IP 位址 tooa MAC 位址的對應
2. ExpressRoute 路由器介面 IP 位址 tooa MAC 位址的對應
3. hello hello 對應存留期

ARP 表格可協助您驗證第 2 層組態，並針對基本的第 2 層連線問題進行疑難排解。

以下是 ARP 表格的範例：

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


hello 之後 > 一節提供有關如何 tooview hello 看到 hello ExpressRoute 邊緣路由器的 ARP 資料表資訊。

## <a name="prerequisites-for-using-arp-tables"></a>使用 ARP 表格的必要條件
請確定您擁有 hello 下列，才能繼續進行：

* 至少使用一個對等互連設定的有效 ExpressRoute 線路。 hello 電路必須完全設定 hello 連線服務提供者。 您 （或您連線服務提供者） 必須至少一個 hello 對等互連 （Azure 的私用、 Azure 公用或 Microsoft） 上設定這個循環。
* 用來設定 hello 對等互連 （Azure 的私用、 Azure 公用和 Microsoft） 的 IP 位址範圍。 檢閱在 hello hello IP 位址指派範例[ExpressRoute 路由需求 頁面](expressroute-routing.md)tooget 了解 IP 位址的方式對應 toointerfaces 您 aise 和 hello ExpressRoute 端上。 您可以藉由檢閱 hello 取得 hello 對等組態資訊[ExpressRoute 對等組態 頁面上](expressroute-howto-routing-classic.md)。
* 從您網路的小組或連線提供者的相關資訊 hello MAC 位址 hello 用的介面，這些 IP 位址。
* hello 最新的 Windows PowerShell 模組 Azure （1.50 或更新版本）。

## <a name="arp-tables-for-your-expressroute-circuit"></a>適用於 ExpressRoute 線路的 ARP 表格
本節提供有關如何 tooview hello ARP 資料表的每一種使用 PowerShell 對等互連的指示。 在繼續之前，您或您連線服務提供者會需要 tooconfigure hello 對等互連。 每個線路都有兩個路徑 (主要和次要)。 您可以獨立檢查 hello ARP 表格的每個路徑。

### <a name="arp-tables-for-azure-private-peering"></a>適用於 Azure 私用對等互連的 ARP 表格
下列指令程式的 hello 提供用於 Azure 私人互連 hello ARP 資料表：

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

以下是其中一個 hello 路徑的範例輸出：

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>適用於 Azure 公用對等互連的 ARP 表格：
下列指令程式的 hello 提供 Azure 公用對等 hello ARP 表格：

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

以下是其中一個 hello 路徑的範例輸出：

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


以下是其中一個 hello 路徑的範例輸出：

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>適用於 Microsoft 對等互連的 ARP 表格
下列指令程式的 hello 提供的 Microsoft 對等互連 hello ARP 資料表：

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


範例輸出如下所示的其中一個 hello 路徑：

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>如何 toouse 這項資訊
hello 對等互連的 ARP 表格可以使用的 toovalidate 第 2 層設定與連線能力。 本節提供在不同狀況下 ARP 表格呈現方式的概觀。

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>當線路處於運作 (預期) 狀態時的 ARP 表格
* hello ARP 表格有 hello 內部端具有有效 IP 和 MAC 位址，項目，而且 hello Microsoft 側邊的類似項目。
* hello hello 內部 IP 位址的最後一個八位元一律為奇數。
* hello Microsoft IP 位址的最後一個八位元一律是 hello 的偶數。
* 相同的 MAC 位址會出現在所有三個互連 （主要/次要） 的 Microsoft 戶端 hello hello。

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>在內部部署或當 hello 連線服務提供者端有問題時，ARP 表格
 只有一個項目會出現在 hello ARP 表格。 它會顯示 hello hello MAC 位址與 hello hello Microsoft 端使用的 IP 位址之間的對應。

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> 如果您遇到像這樣的問題，請開啟支援要求與您的連線提供者 tooresolve 它。
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>ARP 表格時 hello Microsoft 側邊有問題
* 您不會看到顯示對等互連 hello Microsoft 端上有問題時 ARP 表格。
* 向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)開啟支援要求。 指出您發生第 2 層連線的問題。

## <a name="next-steps"></a>後續步驟
* 驗證 ExpressRoute 線路的第 3 層組態：
  * 取得路由摘要 toodetermine hello 狀態的 BGP 工作階段。
  * 取得路由表 toodetermine 的前置詞會透過 ExpressRoute 通告。
* 檢閱輸入和輸出的位元組來驗證資料傳輸。
* 如果問題持續發生，請向 [Microsoft Azure 說明 + 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援要求。

