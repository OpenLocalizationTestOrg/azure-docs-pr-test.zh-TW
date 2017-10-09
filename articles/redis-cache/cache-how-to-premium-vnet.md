---
title: "aaaConfigure Premium Azure Redis 快取的虛擬網路 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理您的 Premium 層 Azure Redis 快取執行個體的虛擬網路支援"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取
Azure Redis 快取都有不同的快取提供項目，提供有彈性地 hello 選擇的快取大小和功能，包括 Premium 層功能，例如叢集、 持續性和虛擬網路支援。 VNet 是 hello 雲端中的私人網路。 Azure Redis 快取執行個體與 VNet 設定時，它不公開可定址，而且只能從虛擬機器和 hello VNet 中的應用程式存取。 本文說明如何 tooconfigure 虛擬網路支援 premium Azure Redis 快取執行個體。

> [!NOTE]
> Azure Redis Cache 支援傳統與 Resource Manager VNet。
> 
> 

如需其他進階快取功能的資訊，請參閱[簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)。

## <a name="why-vnet"></a>為何使用 VNet？
[Azure 虛擬網路 (VNet)](https://azure.microsoft.com/services/virtual-network/)部署提供增強式的安全性和隔離您的 Azure Redis 快取，以及子網路，存取控制原則，和其他功能 toofurther 限制存取。

## <a name="virtual-network-support"></a>虛擬網路支援
Hello 上設定虛擬網路 (VNet) 支援**新增 Redis 快取**快取建立期間的刀鋒視窗。 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

一旦您選取進階定價層，您可以藉由選取 hello 的 VNet 設定 Redis VNet 整合相同的訂用帳戶和與您的快取的位置。 toouse 新的 VNet，先建立目錄中的 hello 步驟[建立虛擬網路使用 Azure 入口網站 hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)或[使用 hello Azure 入口網站建立虛擬網路 （傳統）](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) ，然後傳回 toohello**新增 Redis 快取**toocreate 刀鋒視窗，並設定您的進階版快取。

按一下 新的快取的 tooconfigure hello VNet**虛擬網路**上 hello**新增 Redis 快取**刀鋒視窗中，並選取 hello 需要 VNet 的 hello 下拉式清單。

![虛擬網路][redis-cache-vnet]

選取 hello 所需的子網路，從 hello**子網路**下拉式清單，並指定所需的 hello**靜態 IP 位址**。 如果您使用傳統的 VNet hello**靜態 IP 位址**欄位為選擇性，而且如果未指定，會選擇一個從 hello 選取子網路。

> [!IMPORTANT]
> 在部署 Azure Redis 快取 tooa 資源管理員的 VNet，hello 快取必須不包含 Azure Redis 快取執行個體以外的任何其他資源的專用子網路。 如果嘗試 toodeploy Azure Redis 快取 tooa 資源管理員 VNet tooa 子網路，其中包含其他資源，hello 部署將會失敗。
> 
> 

![虛擬網路][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure 會在每個子網路中保留一些 IP 位址，但這些位址無法使用。 hello hello 子網路的第一個和最後一個 IP 位址已保留給為了符合的通訊協定，以及三個用於 Azure 服務的多個地址。 如需詳細資訊，請參閱 [在這些子網路內使用 IP 位址是否有任何限制？](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Hello Azure VNET 基礎結構所使用加法 toohello IP 位址，在每個 Redis 執行個體中每個分區有 hello 子網路會使用兩個 IP 位址和一個 hello 負載平衡器的其他 IP 位址。 非叢集的快取會被視為 toohave 一個分區。
> 
> 

建立 hello 快取之後，您可以按一下來檢視 hello hello VNet 組態**虛擬網路**從 hello**資源功能表**。

![虛擬網路][redis-cache-vnet-info]

tooconnect tooyour Azure Redis 快取執行個體時使用 VNet，hello 連接字串中指定快取的 hello 主機的名稱，hello 下列範例所示：

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Azure Redis 快取 VNet 常見問題集
hello 清單後面包含的 hello Azure Redis 快取縮放的相關常見問題的解答 toocommonly。

* [Azure Redis 快取和 VNet 的某些常見錯誤設定有哪些？](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [如何確認我的快取是在 VNET 中運作？](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [可以搭配標準或基本快取使用 VNet 嗎？](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [為什麼無法在某些子網路中建立 Redis 快取，但其他的可以？](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Hello 子網路位址空間需求為何？](#what-are-the-subnet-address-space-requirements)
* [將快取裝載於 VNET 時，所有快取功能都可以正常運作嗎？](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Azure Redis 快取和 VNet 的某些常見錯誤設定有哪些？
Azure Redis 快取裝載在 VNet 中，會使用 hello hello 下表中的連接埠。 

>[!IMPORTANT]
>如果在 hello 下表中的 hello 連接埠遭到封鎖，hello 快取可能無法正常運作。 擁有一或多個封鎖這些連接埠是 hello 最常見的設定錯誤問題，在使用 Azure Redis 快取在 VNet 中。
> 
> 

- [輸出連接埠需求](#outbound-port-requirements)
- [輸入連接埠需求](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>輸出連接埠需求

有七項輸出連接埠需求。

- 如有需要，可以透過用戶端進行網際網路的所有輸出連線 toohello 內部稽核的裝置。
- Hello 連接埠中的三種路由流量 tooAzure 端點，Azure 儲存體和 Azure DNS 服務。
- 剩餘的連接埠範圍的 hello 和 Redis 子網路的內部通訊。 內部 Redis 子網域通訊不需要子網路 NSG 規則。

| 連接埠 | 方向 | 傳輸通訊協定 | 目的 | 本機 IP | 遠端 IP |
| --- | --- | --- | --- | --- | --- |
| 80、443 |輸出 |TCP |Azure 儲存體/PKI 上 Redis 的相依項目 (網際網路) | (Redis 子網路) |* |
| 53 |輸出 |TCP/UDP |DNS 上 Redis 的相依項目 (網際網路/VNet) | (Redis 子網路) |* |
| 8443 |輸出 |TCP |Redis 內部通訊 | (Redis 子網路) | (Redis 子網路) |
| 10221-10231 |輸出 |TCP |Redis 內部通訊 | (Redis 子網路) | (Redis 子網路) |
| 20226 |輸出 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路) |
| 13000-13999 |輸出 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路) |
| 15000-15999 |輸出 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路) |


### <a name="inbound-port-requirements"></a>輸入連接埠需求

有八項輸入連接埠範圍需求。 這些範圍中的傳入的要求是從其他服務裝載於 hello 輸入相同的 VNET 或內部 toohello Redis 子網路通訊。

| 連接埠 | 方向 | 傳輸通訊協定 | 目的 | 本機 IP | 遠端 IP |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |輸入 |TCP |用戶端通訊 tooRedis，Azure 負載平衡 | (Redis 子網路) |虛擬網路，Azure Load Balancer |
| 8443 |輸入 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路) |
| 8500 |輸入 |TCP/UDP |Azure 負載平衡 | (Redis 子網路) |Azure Load Balancer |
| 10221-10231 |輸入 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路)，Azure Load Balancer |
| 13000-13999 |輸入 |TCP |用戶端通訊 tooRedis Azure 負載平衡的叢集 | (Redis 子網路) |虛擬網路，Azure Load Balancer |
| 15000-15999 |輸入 |TCP |用戶端通訊 tooRedis 叢集，Azure 負載平衡 | (Redis 子網路) |虛擬網路，Azure Load Balancer |
| 16001 |輸入 |TCP/UDP |Azure 負載平衡 | (Redis 子網路) |Azure Load Balancer |
| 20226 |輸入 |TCP |Redis 內部通訊 | (Redis 子網路) |(Redis 子網路) |

### <a name="additional-vnet-network-connectivity-requirements"></a>其他 VNET 網路連線需求

在虛擬網路中，可能一開始就不符合 Azure Redis 快取的一些網路連線需求。 Azure Redis 快取需要所有 hello 下列項目 toofunction 用於虛擬網路時，適當地。

* 傳出的網路連線 tooAzure 儲存體端點全球。 這包括端點位於 hello 與 hello Azure Redis 快取執行個體，以及儲存體端點位於相同區域**其他**Azure 區域。 Azure 儲存體端點解決下列 DNS 網域的 hello 下： *.table.core.windows.net*， *account>.blob.core.windows.net*， *queue.core.windows.net*，和*file.core.windows.net*。 
* 傳出的網路連線太*ocsp.msocsp.com*， *mscrl.microsoft.com*，和*crl.microsoft.com*。這種連線能力是需要的 toosupport SSL 功能。
* 必須能夠解析所有 hello 端點 hello hello 虛擬網路的 DNS 設定，且網域中所述 hello 較早的點。 DNS 符合這些需求可確保有效的 DNS 基礎結構並加以設定和維護的 hello 虛擬網路。
* 下列 Azure 監視功能的端點，在 hello 下列 DNS 網域解析的輸出網路連線 toohello: shoebox2 black.shoebox2.metrics.nsatc.net、 north prod2.prod2.metrics.nsatc.net，-azglobal black.azglobal.metrics.nsatc.net 的 shoebox2-red.shoebox2.metrics.nsatc.net 東部 prod2.prod2.metrics.nsatc.net，azglobal red.azglobal.metrics.nsatc.net。

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>如何確認我的快取是在 VNET 中運作？

>[!IMPORTANT]
>當連線 tooan Azure Redis 快取執行個體裝載於 VNET，您必須在用戶端的快取 hello 相同的 VNET，包括任何測試應用程式或執行 ping 的診斷工具。
>
>

一旦 hello 上一節中所述設定 hello 連接埠需求，您可以確認您的快取正在執行下列步驟的 hello。

- [重新啟動](cache-administration.md#reboot)hello 的所有快取節點。 如果所有的 hello 必要無法達到快取相依性 (如中所述[輸入連接埠需求](cache-how-to-premium-vnet.md#inbound-port-requirements)和[輸出連接埠需求](cache-how-to-premium-vnet.md#outbound-port-requirements))，hello 快取將不會無法 toorestart 成功。
- Hello 快取節點必須重新啟動後 （當由 hello Azure 入口網站中的 hello 快取狀態報告），您可以執行下列測試 hello:
  - ping hello 快取端點 （使用連接埠 6380） 從 hello 內的電腦相同的 VNET hello 與快取，請使用[tcping](https://www.elifulkerson.com/projects/tcping.php)。 例如：
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    如果 hello`tcping`工具會報告確認 hello 連接埠已開啟，而且 hello 快取是可供從 hello VNET 中的用戶端的連線。

  - 另一個方式 tootest 是 toocreate 測試快取用戶端 (可能是簡單的主控台應用程式使用 StackExchange.Redis)，連接 toohello 快取新增和擷取 hello 快取中的某些項目。 安裝到 VM 中的 hello 範例用戶端應用程式 hello 做為 hello 快取相同的 VNET，然後執行 tooverify 連線 toohello 快取。


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>可以搭配標準或基本快取使用 VNet 嗎？
VNet 僅適用於進階快取。

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>為什麼無法在某些子網路中建立 Redis 快取，但其他的可以？
如果您要部署的 Azure Redis 快取 tooa 資源管理員的 VNet，hello 快取必須包含其他的資源類型的專用子網路。 如果嘗試 toodeploy Azure Redis 快取 tooa 資源管理員 VNet 子網路，其中包含其他資源，hello 部署將會失敗。 您可以建立新的 Redis 快取之前，您必須刪除 hello hello 子網路內現有的資源。

您可以部署多個類型的資源 tooa 傳統的 VNet，只要您有足夠的 IP 位址可用。

### <a name="what-are-hello-subnet-address-space-requirements"></a>Hello 子網路位址空間需求為何？
Azure 會在每個子網路中保留一些 IP 位址，但這些位址無法使用。 hello hello 子網路的第一個和最後一個 IP 位址已保留給為了符合的通訊協定，以及三個用於 Azure 服務的多個地址。 如需詳細資訊，請參閱 [在這些子網路內使用 IP 位址是否有任何限制？](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Hello Azure VNET 基礎結構所使用加法 toohello IP 位址，在每個 Redis 執行個體中每個分區有 hello 子網路會使用兩個 IP 位址和一個 hello 負載平衡器的其他 IP 位址。 非叢集的快取會被視為 toohave 一個分區。

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>將快取裝載於 VNET 時，所有快取功能都可以正常運作嗎？
當您的快取是 VNET 的一部分時，hello VNET 中的用戶端可以存取 hello 快取。 如此一來，hello 下列快取管理功能無法運作這一次。

* Redis 主控台-Redis 主控台在超出範圍 hello VNET，您本機瀏覽器中執行，因為它無法連線 tooyour 快取。

## <a name="use-expressroute-with-azure-redis-cache"></a>搭配 Azure Redis 快取使用 ExpressRoute
客戶可以連接[Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/)電路 tootheir 虛擬網路基礎結構，進而擴充其內部部署網路 tooAzure。 

根據預設，新建立的 ExpressRoute 循環並不會在 VNET 上執行強制通道 (預設路由的公告 0.0.0.0/0)。 如此一來，輸出的網際網路連線可以直接從 hello VNET，而且用戶端應用程式都可以 tooconnect tooother Azure 端點包括 Azure Redis 快取。

不過常見的客戶設定是強制通道的 toouse （通告預設路由） 可以強制傳出網際網路流量 tooinstead 資料流程在內部。 此流量 hello 輸出流量是否會中斷與 Azure Redis 快取的連線，然後封鎖在內部部署，使得 hello Azure Redis 快取執行個體不能 toocommunicate 具其相依性。

hello 解決方案是 toodefine 一個 （或更多） 使用者定義的路由 (UDRs) 包含 hello Azure Redis 快取的 hello 子網路上。 UDR 定義特定子網路的路由，則會採用而不是 hello 預設路由。

可能的話，我們建議下列組態 toouse hello:

* hello ExpressRoute 組態通告 0.0.0.0/0，並依預設強制通道連接所有輸出流量的內部。
* hello UDR 套用 toohello 子網路包含 hello Azure Redis 快取都會定義與工作路由的 TCP/IP 流量 toohello 0.0.0.0/0 公用網際網路。如需範例所設定的 hello 下個躍點類型 too'Internet'。

hello 聯合的影響這些步驟是，hello 子網路層級 UDR 優先於 hello ExpressRoute 強制通道，以確保從 hello Azure Redis 快取的對外網際網路存取。

從內部部署應用程式使用 ExpressRoute 連線 tooan Azure Redis 快取執行個體不是因為 tooperformance 原因的一般使用案例 (為了達到最佳效能 Azure Redis 快取的用戶端應該在 hello 與 hello Azure Redis 快取相同的區域)。

>[!IMPORTANT] 
>hello UDR 中定義的路由**必須**不夠具體 tootake 優先順序透過通告 hello ExpressRoute 組態的任何路由。 hello 下列範例會使用 hello 廣泛 0.0.0.0/0 位址範圍，並在這種情況可能會不小心覆寫使用更特定的位址範圍的路由通告。

>[!WARNING]  
>Azure Redis 快取不支援使用 ExpressRoute 組態，**不正確地跨通告 hello 公用互連路徑 toohello 私用對等互連路徑路由**。 已設定公用對等互連的 ExpressRoute 組態，會收到來自 Microsoft 的一大組 Microsoft Azure IP 位址範圍的路由通告。 如果這些位址範圍不正確地跨通告 hello 私用對等互連路徑上，hello 結果會是從 hello Azure Redis 快取執行個體的子網路的所有輸出網路封包會不正確地使用強制通道 tooa 客戶的內部部署網路基礎結構。 這個網路流量會中斷 Azure Redis 快取。 hello 方案 toothis 問題是 toostop 跨廣告 hello 公用互連路徑 toohello 私用對等互連路徑路由。


如需使用者定義路由的背景資訊，請參閱此 [概觀](../virtual-network/virtual-networks-udr-overview.md)。

如需 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)。

## <a name="next-steps"></a>後續步驟
了解如何更進階的 toouse 快取功能。

* [簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

