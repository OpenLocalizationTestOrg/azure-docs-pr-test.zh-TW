---
title: "網路與 Azure Site Recovery 的 HYPER-V (withSystem Center VMM) tooAzure 複寫 aaaPlan |Microsoft 文件"
description: "本文將討論網路計劃所需的複寫 （使用 VMM) 的 HYPER-V Vm tooAzure 時"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 51ca8b939b6f96880f83599ea8009eb0bfa5b957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-tooazure-replication"></a>步驟 4： 規劃 （使用 VMM) 的 HYPER-V tooAzure 複寫的網路功能

在執行之後[容量規劃](vmm-to-azure-walkthrough-capacity.md)（如果您進行完整部署），閱讀有關網路複寫在內部部署 HYPER-V Vm 中 System Center Virtual Machine Manager (VMM) 時的規劃考量此發行項 toolearn雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。

張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="network-mapping-for-replication-tooazure"></a>複寫 tooAzure 網路對應

當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooAzure 時，會使用網路對應。 網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 Azure 網路。 對應未 hello 遵循：

- **網路連線**— 容錯移轉之後，所有複寫的 Azure Vm 就會連接的 toohello 對應的 Azure 網路。 容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，即使它們在不同的復原計劃中容錯移轉。
- **網路閘道**-Vm 網路閘道已設定 hello 目標 Azure 網路上，如果可以 tooother 在內部部署內部 hello 對應中的虛擬機器網路連線。

### <a name="prepare-vmm-for-network-mapping"></a>準備 VMM 以進行網路對應

準備 VMM 以進行網路對應，如下所示：

1. 如果您沒有的話，請準備[VMM 邏輯網路](https://docs.microsoft.com/system-center/vmm/network-logical)hello 雲端中的 hello HYPER-V 主機位於與關聯。
2. 如果您沒有的話，請建立[VM 網路](https://docs.microsoft.com/system-center/vmm/network-virtual)連結的 toohello 您備妥以上的邏輯網路。
3. 連接 Vm 上 hello HYPER-V 主機伺服器/叢集 hello VMM 雲端，toohello VM 網路中。

 
請注意： 
- 新的 Vm 新增 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。
- 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。
- 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。
- 您準備 Azure 網路，並設定網路對應，為您部署的 hello 案例。

## <a name="connecting-tooazure-vms-after-failover"></a>在容錯移轉之後連接 tooAzure Vm

規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello Azure VM。 設計複本 Azure VM 的網路策略時，有兩種選擇：

- **使用不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址範圍的 hello 複寫 Azure VM 網路。 在此案例 hello VM 容錯移轉之後，取得新的 IP 位址，DNS 更新為必要項。
- **保留相同的 IP 位址的 hello**： 您可能會想 toouse hello 相同 IP 位址範圍，在主要在內部網路，如 hello Azure 網路容錯移轉之後。  可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。 不過，當您要複寫 tooAzure，您必須 tooupdate hello 新位置的 hello IP 位址的路由在容錯移轉之後。


## <a name="retain-ip-addresses"></a>保留 IP 位址

容錯移轉 tooAzure，具有子網路容錯移轉時，站台復原提供 hello 功能 tooretain 固定 IP 位址。

藉由子網路容錯移轉，特定的子網路會存在於站台 1 或站台 2 中，但絕不會同時存在於這兩個站台中。 順序 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，在您以程式設計的方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。 容錯移轉期間，以 hello hello 子網路移動相關的受保護的 Vm。 hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。



### <a name="failover-example"></a>容錯移轉範例

讓我們看看 tooAzure 容錯移轉的範例。

- Woodgrove Bank 是一家虛構的公司，擁有裝載其商務應用程式的內部部署基礎結構。 它們的行動應用程式裝載在 Azure 上。
- Woodgrove Bank Vm 在 Azure 和內部部署伺服器之間的連線是由站台對站台 (VPN) 連線 hello 在內部部署邊緣網路與 hello Azure 虛擬網路之間提供。
- 這個 hello 公司的 Azure 虛擬網路的 VPN 表示會顯示為其內部部署網路的延伸。
- Woodgrove 想 toouse Site Recovery tooreplicate 內部工作負載 tooAzure。
 - Woodgrove 有 toodeal 應用程式與組態的硬式編碼的 IP 位址，而定，因此在容錯移轉 tooAzure 之後的應用程式需要 tooretain IP 位址。
 - Woodgrove 已指派的 IP 位址範圍 172.16.1.0/24 從 172.16.2.0/24 tooits 資源在 Azure 中執行。


Woodgrove toobe 無法 tooreplicate 其 Vm tooAzure 時保留 hello IP 位址，如以下是何種 hello 公司需要 toodo:

1. 建立 Azure 虛擬網路。 它應該 hello 的延伸模組為內部網路，使應用程式可以順暢地進行容錯移轉。
2. Azure 可讓您 tooadd 站對站 VPN 連線能力，此外 toopoint 對站連線能力 toohello 虛擬網路在 Azure 中建立。
3. 設定 hello 站對站連線，請在 hello Azure 網路，只有 hello IP 位址範圍是不同 hello 內部 IP 位址範圍內，您可以路由傳送流量 toohello 在內部部署位置 （區域網路）。
    - 這是因為 Azure 不支援延伸的子網路。 因此如果您有子網路 192.168.1.0/24 內部部署，您無法加入本機網路 192.168.1.0/24 hello Azure 網路。
    - 這是預期行為，因為 Azure 不知道 hello 的子網路中有沒有作用中的 Vm，並只災害復原正在建立 hello 子網路。
    - toobe toocorrectly 無法路由傳送網路流量超出 hello 網路和 hello 本機網路中的 Azure 網路 hello 子網路不得發生衝突。

![子網路容錯移轉之前](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>容錯移轉之前

1. 建立額外的網路 (例如「復原網路」)。 這是 hello 網路中的容錯移轉的 Vm 會建立。
2. 容錯移轉之後，在 hello VM 屬性仍會保留 hello vm 的 IP 位址的 tooensure >**設定**，指定相同的 IP 位址 VM 內部，並按一下該 hello hello**儲存**。
3. 當 hello VM 容錯移轉時，Azure Site Recovery 會指派提供 IP 位址 tooit hello。

    ![網路屬性](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. 容錯移轉觸發程序會觸發，並 hello Vm 在 Azure 中建立具有所需的 hello IP 位址之後，您可以連接 toohello 網路使用[Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。 此動作可以編寫指令碼。
5. 路由需要適當地修改，toobe tooreflect 該 192.168.1.0/24 現在已移 tooAzure。

    ![子網路容錯移轉之後](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>容錯移轉之後

如果您還沒有如上所示的 Azure 網路，可以在容錯移轉之後，建立主要站台與 Azure 之間的站對站 VPN 連線。

## <a name="change-ip-addresses"></a>變更 IP 位址

這[部落格文章](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)說明如何 tooset 向上 hello Azure 網路基礎結構時您不需要 tooretain IP 位址在容錯移轉之後。 它會啟動應用程式描述、 查看如何 tooset 網路內部部署，以及在 Azure 中，並於結尾提供執行容錯移轉的相關資訊。  

## <a name="next-steps"></a>後續步驟

跳過[步驟 5： 準備 Azure](vmm-to-azure-walkthrough-prepare-azure.md)
