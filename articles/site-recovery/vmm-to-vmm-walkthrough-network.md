---
title: "HYPER-V 複寫 tooa 次要 VMM 站台與 Azure Site Recovery 的網路功能的 aaaPlan |Microsoft 文件"
description: "本文將討論網路時複寫 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery 的規劃。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>步驟 3： 規劃 HYPER-V 虛擬機器複寫 tooa 次要 VMM 站台的網路功能

檢閱部署必要條件，讀取網路複寫管理 System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器 (Vm) 時這個發行項 tooplan 之後 tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。 

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="network-mapping-overview"></a>網路對應概觀

當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooa 次要資料中心時，會使用網路對應。 網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 VMM 伺服器上的 VM 網路。 對應未 hello 遵循：

- **網路連線**— 容錯移轉之後連接 Vm tooappropriate 網路。 hello 複本 VM 將會是對應的 toohello 來源網路的連線的 toohello 目標網路。
- **最佳的放置**— 數位 hello HYPER-V 主機伺服器上的複本 Vm 的最佳方式。 複本 Vm 會放置在主機上，可以存取 hello 對應 VM 網路。
- **任何網路對應**— 如果您未設定網路對應，複本 Vm 容錯移轉之後將無法連接的 tooany VM 網路。


### <a name="example"></a>範例

以下是範例 tooillustrate 這項機制。 讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。

**位置** | **VMM 伺服器** | **VM 網路** | **對應至**
---|---|---|---
紐約 | VMM-NewYork| VMNetwork1-NewYork | 對應的 tooVMNetwork1 芝加哥
 |  | VMNetwork2-NewYork | 未對應
芝加哥 | VMM-Chicago| VMNetwork1-Chicago | 對應的 tooVMNetwork1 紐約
 | | VMNetwork1-Chicago | 未對應

在此範例中：

- 針對已連線的 tooVMNetwork1 紐約任何虛擬機器建立複本虛擬機器時，就會連接的 tooVMNetwork1 芝加哥。
- VMNetwork2 紐約或 VMNetwork2 芝加哥建立複本虛擬機器時，它將無法連接的 tooany 網路。

以下是如何在我們的範例組織中，與 hello 與 hello 雲端相關聯的邏輯網路中設定 VMM 雲端。

#### <a name="cloud-protection-settings"></a>雲端保護設定

**受保護的雲端** | **保護雲端** | **邏輯網路 (紐約)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>邏輯和 VM 網路設定

**位置** | **邏輯網路** | **相關聯的 VM 網路**
---|---|---
紐約 | LogicalNetwork1-NewYork | VMNetwork1-NewYork
芝加哥 | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>目標網路設定

根據這些設定，當您選取 hello 目標 VM 網路，hello 下表顯示的 hello 選項可供使用。

**選取** | **受保護的雲端** | **保護雲端** | **可用的目標網路**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | 可用
 | GoldCloud1 | GoldCloud2 | 可用
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | 尚未提供
 | GoldCloud1 | GoldCloud2 | 可用


如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。


#### <a name="failback-behavior"></a>容錯回復行為

toosee 怎樣 hello 案例容錯回復 （反向複寫），讓我們假設 VMNetwork1 紐約對應的 tooVMNetwork1-芝加哥，以下列設定的 hello。


**虛擬機器** | **連接的 tooVM 網路**
---|---
VM1 | VMNetwork1-Network
VM2 (VM1 的複本) | VMNetwork1-Chicago

讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。

**案例** | **結果**
---|---
Vm-2 的容錯移轉之後的 hello 網路屬性沒有變更。 | Vm-1 依然連接的 toohello 來源網路。
在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。 | VM-1 已中斷連線。
Vm-2 的網路屬性會變更容錯移轉之後，並且已連線的 tooVMNetwork2 芝加哥。 | 如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。
VMNetwork1-Chicago 的網路對應已變更。 | Vm-1 將會連接的 toohello 現在對應的網路 tooVMNetwork1 芝加哥。



## <a name="prepare-for-network-mapping"></a>準備網路對應

1. Hello 來源和目標 VMM 伺服器上，您應該與 hello 來源與目標雲端相關聯的邏輯網路。 
2. Hello 來源和目標伺服器，您必須具備的 VM 網路連結的 toohello 邏輯網路。
3. 在 hello 來源位置中的 HYPER-V 主機上的 Vm 應該連結的 toohello 來源 VM 網路。 如果您只使用單一 VMM 伺服器，您可以設定之間的對應 hello 上的 VM 網路相同伺服器。

在 Site Recovery 部署期間設定網路對應時，會發生下列情況：

- 當您設定網路對應，並選取目標 VM 網路時，使用 hello 來源 VM 網路的 hello VMM 來源雲端將會顯示，以及在 hello 目標雲端上的 hello 可用目標 VM 網路。
- - 當對應已正確設定和啟用複寫時，來源 VM 將會連接的 tooits 來源 VM 網路，而它在 hello 目標位置的複本將會連接 tooits 對應 VM 網路。
- 如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello VM 將會連接的 toohello hello 網路中的第一個子網路。

## <a name="connect-toovms-after-failover"></a>容錯移轉之後連接 tooVMs

規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello 複本。 其中有幾個選項： 

- **使用不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址的 hello 複寫 VM。 在此案例 hello VM 容錯移轉之後，取得新的 IP 位址，DNS 更新為必要項。
- **保留相同的 IP 位址的 hello**： 您可能會想 toouse hello hello 複本 VM 相同的 IP 位址。 可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。 

## <a name="retain-ip-addresses"></a>保留 IP 位址

如果您想 tooretain hello IP 位址從 hello 主要站台容錯移轉 toohello 次要站台之後，您可以執行完整的子網路容錯移轉，，並更新 hello IP 位址的路由 tooindicate hello 新位置或替代方案部署的延展的子網路之間 hello主要和 hello 復原站台。

### <a name="stretched-subnet"></a>延伸的子網路

在延展的子網路，hello 子網路，同時在 hello 主要和次要站台。 如果您移動伺服器和其 IP (第 3 層) 組態 toohello 次要站台，hello 網路就會自動路由 hello 流量 toohello 新位置。 

從第 2 層 (資料連結層) 的觀點而言，您需要可以管理延伸的 VLAN 的網路設備。 此外，由延伸 hello VLAN，hello 潛在容錯網域延伸 tooboth 站台，基本上成為單一失敗點。 雖然機率不高，但有可能發生廣播風暴，而且無法隔離。 


### <a name="subnet-failover"></a>子網路容錯移轉

您可以執行的子網路容錯移轉 tooobtain hello hello 延展的子網路的優點，而不實際自動縮放。 在此解決方案中，子網路將可在 hello 來源或目標站台中，但不是能在兩者同時。 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，您可以透過程式設計方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。 子網路容錯移轉發生時，都會隨之移動後 hello 相關聯的 Vm。 hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。

### <a name="example"></a>範例

以下是完整的子網路容錯移轉範例。 hello 主要站台的子網路 192.168.1.0/24 中執行的應用程式。 在容錯移轉時，此子網路中的所有 hello Vm 已容錯移轉 toohello 次要站台，而會保留其 IP 位址。 路由需要 toobe 修改 tooreflect hello 事實的所有 hello VM 虛擬機器屬於 toosubnet 192.168.1.0/24 現在已經都移動 toohello 次要站台。

hello 下列圖形顯示 hello 子網路容錯移轉的前後：

- 容錯移轉之前，子網路 192.168.0.1/24 而作用於 hello 來源站台，成為作用中 hello 次要站台容錯移轉之後。
- 主要站台和復原站台、 第三個網站和主要站台之間路由傳送的 hello，而第三個網站和復原站台 toobe 適當修改。

**容錯移轉之前**

![容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**容錯移轉之後**

![容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

容錯移轉之後，會發生下列情況：

- Site Recovery 從 hello 靜態 IP 位址集區 hello 相關網路，每個 VMM 執行個體中每個網路介面上 hello VM，配置的 IP 位址。
- 如果 hello IP 位址集區中 hello 次要站台是相同的 hello 來源站台，站台復原上配置的 hello hello 相同的 IP 位址 （hello 來源 VM） toohello 複本 VM。 hello IP 位址已保留在 VMM 中，但未設定為 hello 容錯移轉 IP 位址 hello HYPER-V 主機上。 hello 容錯移轉 IP 位址的 hyper-v 主機上設定之前 hello 容錯移轉。
- 如果 hello 相同的 IP 位址無法使用，Site Recovery 會從 hello 集區配置另一個可用的 IP 位址。
- 如果 Vm 使用 DHCP，Site Recovery 並不管理 hello IP 位址。 您需要 hello DHCP 的 toocheck hello 次要站台上的伺服器可以從 hello 做 hello 來源站台相同的範圍配置位址。

### <a name="validate-hello-ip-address"></a>驗證 hello IP 位址

啟用 vm 保護之後，您可以使用下列範例指令碼 tooverify hello 指派位址 toohello VM。 相同的 IP 位址會設定為 hello 容錯移轉 IP 位址，並在 hello 容錯移轉期間指派 toohello VM hello:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>變更 IP 位址

在此案例中，會變更 hello 的容錯移轉的 Vm 的 IP 位址。 此解決方案的 hello 缺點是需要 hello 維護動作。 通常在複本 VM 啟動後會更新 DNS。 DNS 項目，可能需要變更 toobe 或 fluster thenetwork 和更新的快取項目中。 這可能會導致停機時間。 透過下列方式可以避免停機時間：

- 對內部網路應用程式使用低 TTL 值。
- 使用下列指令碼的站台復原復原方案，tooupdate hello DNS 伺服器 tooensure 及時更新中的 hello。 如果您使用動態 DNS 登錄，您不需要 hello 指令碼。

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>範例 

讓我們看看計劃跨 hello 主要 toouse 不同 IP 位址和 hello 復原站台的案例。在此範例中有不同的 IP 位址在主要和次要站台之間，而且那里; s 協力廠商網站，從 hello 主要或復原站台上裝載的應用程式可以存取。

- 容錯移轉之前，應用程式是託管的子網路 192.168.1.0/24 hello 主要站台上，設定在 hello 次要站台上的子網路 172.16.1.0/24 toobe 容錯移轉之後。
- 已適當地設定 VPN 連線/網路路由，讓所有的三個站台可以互相存取。
- 容錯移轉之後，應用程式將會還原 hello 復原子網路中。 在此案例中有任何需要 toofail 透過 hello 整個子網路，且不不需要的 tooreconfigure VPN 或網路路由的任何變更。 hello 容錯移轉和某些 DNS 更新，請確定應用程式仍然可以存取。
- 若 DNS 設定的 tooallow 動態更新，然後 hello Vm 會自行註冊方式容錯移轉後啟動時使用 hello 新的 IP 位址。

**容錯移轉之前**

![不同的 IP - 容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**容錯移轉之後**

![不同的 IP - 容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>後續步驟

跳過[步驟 4： 準備 VMM 和 HYPER-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。


