---
title: "Azure Site Recovery 中的 aaaTest 容錯移轉 (VMM tooVMM) |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解容錯移轉 tooAzure 或次要資料中心。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>在站台復原中測試容錯移轉 (VMM tooVMM)


針對以 Azure Site Recovery 保護的虛擬機器 (VM) 與實體伺服器所執行的測試容錯移轉或災害復原 (DR) 訓練，本文提供相關資訊和指示。 您將使用 System Center Virtual Machine Manager VMM 受管理內部部署站台作為 hello 復原站台。

您執行測試容錯移轉 toovalidate 複寫策略，或執行不含任何資料遺失或停機時間的 DR 訓練。 測試容錯移轉不會影響任何 hello 進行中的複寫或實際執行環境。 您可以在虛擬機器上執行測試容錯移轉，或依[復原方案](site-recovery-create-recovery-plans.md)執行。 當您正在觸發測試容錯移轉時，您會需要 toospecify hello hello 測試虛擬機器會連線到網路的。 您可以在 hello 追蹤 hello hello 測試容錯移轉的進度**作業**頁面。  

如果您有任何意見或疑問，張貼在 hello 下方這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="prepare-hello-infrastructure-for-test-failover"></a>測試容錯移轉的準備 hello 基礎結構
如果您想 toorun 測試容錯移轉使用現有的網路時，準備該網路中 Active Directory、 DHCP 及 DNS。

如果您想 toorun 測試容錯移轉會自動使用 hello 選項 toocreate VM 網路，將群組 1 之前的手動步驟要 toouse hello 測試容錯移轉的 hello 復原方案中。 然後，加入 hello 基礎結構資源 toohello 自動建立在執行 hello 測試容錯移轉之前的網路。

### <a name="things-toonote"></a>項目 toonote
當您要複寫 tooa 次要站台，hello hello 複本機器會使用不需要 toomatch hello 做為測試容錯移轉的邏輯網路類型，但某些組合可能無法運作的網路類型。 如果 hello 複本會使用 DHCP 和 VLAN 架構隔離，hello hello 複本的 VM 網路不需要靜態 IP 位址集區。 使用 Windows 網路虛擬化的 hello 測試容錯移轉將無法運作，因為沒有位址集區可供使用。 

此外，如果 hello 複本網路使用無隔離且 hello 測試網路使用 Windows 網路虛擬化，將無法運作 hello 測試容錯移轉。 這是因為 hello 無隔離網路沒有 hello 子網路需要的 toocreate Windows 網路虛擬化網路。

容錯移轉主要取決 hello VM 網路 hello VMM 主控台中的設定方式之後，如何複本虛擬機器會連接的 toomapped VM 網路。

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>設定為未隔離或 VLAN 隔離的 VM 網路
Hello VM 網路定義 DHCP，hello 複本虛擬機器連接的 toohello VLAN ID，透過 hello 設定所指定的 hello hello 相關聯的邏輯網路中的網站。 hello 虛擬機器從 hello 可用的 DHCP 伺服器接收其 IP 位址。 

您不需要 toodefine 靜態的 IP 位址集區的 hello 目標 VM 網路。 如果靜態 IP 位址集區用於 hello VM 網路，hello 複本虛擬機器是透過 hello 設定所指定的 hello 相關聯的邏輯網路中的 hello 網站的連線的 toohello VLAN ID。

hello 虛擬機器從 hello VM 網路所定義的 hello 集區接收其 IP 位址。 如果靜態 IP 位址集區不定義於 hello 目標 VM 網路，IP 位址配置將會失敗。 在這兩個 hello 來源和目標 VMM 伺服器將用於保護和復原工作 hello IP 位址集區。

#### <a name="vm-network-with-windows-network-virtualization"></a>採用 Windows 網路虛擬化的 VM 網路
如果使用 Windows 網路虛擬化設定的 VM 網路，您應該定義靜態集區 hello 目標 VM 網路，無論 hello 來源 VM 網路是設定的 toouse DHCP 或靜態的 IP 位址集區。 

如果您定義 DHCP，hello 目標 VMM 伺服器做為 DHCP 伺服器，並提供 hello 目標 VM 網路中所定義的 hello 集區的 IP 位址。 如果使用靜態 IP 位址集區定義 hello 來源伺服器，hello 目標 VMM 伺服器會從 hello 集區配置 IP 位址。 在這兩種情況下，如果未定義靜態 IP 位址集區，IP 位址配置將會失敗。


### <a name="prepare-dhcp"></a>準備 DHCP
如果 hello 虛擬機器相關的測試容錯移轉會使用 DHCP，建立測試 DHCP 伺服器 hello hello 目的是要測試容錯移轉的隔離網路內。

### <a name="prepare-active-directory"></a>準備 Active Directory
toorun 應用程式測試的測試容錯移轉，您會需要 hello 生產 Active Directory 環境的複本在您的測試環境中。 如需詳細資訊，請檢閱 hello[測試 Active Directory 的容錯移轉考量](site-recovery-active-directory.md#test-failover-considerations)。

### <a name="prepare-dns"></a>準備 DNS
準備 DNS 伺服器 hello 測試容錯移轉，如下所示：

* **DHCP**: hello 的 hello 測試 DNS 的 IP 位址的虛擬機器使用 DHCP，如果應該更新 hello 測試 DHCP 伺服器上。 如果您使用 Windows 網路虛擬化的網路類型，hello VMM 伺服器將充當 hello DHCP 伺服器。 因此，DNS hello IP 位址應更新 hello 測試容錯移轉網路中。 在此情況下，hello 虛擬機器自我登錄 toohello 相關的 DNS 伺服器。
* **靜態位址**： 如果虛擬機器使用靜態 IP 位址，hello hello 測試 DNS 伺服器應該更新測試容錯移轉網路中的 IP 位址。 您可能需要 tooupdate DNS hello hello 測試虛擬機器 IP 位址。 您可以使用下列範例指令碼，針對此用途的 hello:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>執行測試容錯移轉
此程序描述如何 toorun 測試容錯移轉的復原計劃。 或者，您可以執行 hello 容錯移轉的單一虛擬機器上 hello**虛擬機器** 索引標籤。

![測試容錯移轉刀鋒視窗](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. 選取 [復原方案]  >  *recoveryplan_name*。 按一下 [容錯移轉] **容錯移轉** > **Test 容錯移轉**中張貼意見或問題。
1. 在 hello**測試容錯移轉**刀鋒視窗中，指定虛擬機器應該如何連接的 toonetworks hello 測試容錯移轉之後。 如需詳細資訊，請參閱 hello[網路選項](#network-options-in-site-recovery)。
1. Hello 上追蹤容錯移轉的進度**作業** 索引標籤。
1. 容錯移轉已完成之後，請確認 hello 虛擬機器成功啟動。
1. 當您完成時，按一下**清除測試容錯移轉**hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 此步驟會刪除 hello 虛擬機器和測試容錯移轉期間所建立的網路。


## <a name="network-options-in-site-recovery"></a>Site Recovery 中的網路選項

當您執行測試容錯移轉時，詢問您的測試複本機器 tooselect 網路設定。 您可以很多選擇。  

| **測試容錯移轉選項** | **說明** | **容錯移轉檢查** | **詳細資料** |
| --- | --- | --- | --- |
| **容錯移轉 tooa 次要 VMM 站台-沒有網路** |請勿選取 VM 網路。 |容錯移轉會檢查測試機器是否已建立。<br/><br/>hello hello 複本虛擬機器所在的主機上建立 hello 測試虛擬機器。 它不會加入 toohello 雲端 hello 複本虛擬機器所在的位置。 |<p>hello 容錯機器未連接的 tooany 網路。<br/><br/>一旦建立後 hello 電腦可以連線的 tooa VM 網路。 |
| **容錯移轉 tooa 次要 VMM 站台-使用網路** |選取現有的 VM 網路。 |容錯移轉會檢查虛擬機器是否已建立。 |hello hello 複本虛擬機器所在的主機上建立 hello 測試虛擬機器。 它不會加入 toohello 雲端 hello 複本虛擬機器所在的位置。<br/><br/>建立與您的生產網路隔離的 VM 網路。<br/><br/>如果您是使用 VLAN 網路，建議您在 VMM 中另外建立未用於生產網路的測試專用邏輯網路。 此邏輯網路是使用的 toocreate 中測試容錯移轉的 VM 網路。<br/><br/>hello 邏輯網路應該至少一個 hello 裝載虛擬機器的所有 hello HYPER-V 伺服器的網路介面卡與相關聯。<br/><br/>若為 VLAN 邏輯網路，hello 您加入 toohello 邏輯網路應該位於隔離網路網站。<br/><br/>如果您是使用 Windows 網路虛擬化型邏輯網路，Azure Site Recovery 會自動建立隔離的 VM 網路。 |
| **無法透過次要 VMM 站台 tooa-建立網路** |根據您指定中的 hello 設定自動建立暫時性測試網路**邏輯網路**及其相關的網路站台。 |容錯移轉會檢查虛擬機器是否已建立。 |如果 hello 復原計劃使用一個以上的 VM 網路，請使用此選項。 如果您使用 Windows 網路虛擬化網路，這個選項可以自動建立 VM 網路以 hello （子網路和 IP 位址集區） 的相同設定 hello 網路中的 hello 複本虛擬機器。 這些 VM 網路會自動清除 hello 測試容錯移轉完成之後。</p><p>hello hello 複本虛擬機器所在的主機上建立 hello 測試虛擬機器。 它不會加入 toohello 雲端 hello 複本虛擬機器所在的位置。 |

> [!TIP]
> hello tooa 虛擬機器指定測試容錯移轉期間的 IP 位址為 hello 規劃或未規劃的容錯移轉 （假設 hello IP 位址可供 hello 測試容錯移轉網路中） 將會收到 hello 虛擬機器的相同 IP 位址。 如果 hello 相同的 IP 位址不可用在 hello 測試容錯移轉網路，hello 虛擬機器都會收到另一個用於 hello 測試容錯移轉網路的 IP 位址。
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>測試容錯移轉 tooa 復原站台上的實際執行網路
當您進行測試容錯移轉時，建議您選擇與在 [網路對應](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping) 中提供的生產復原網站網路不同的網路。 但是，如果您真的想 toovalidate 容錯虛擬機器中的端對端網路連線，請注意下列點 hello:

* 請確定您要執行 hello 測試容錯移轉時，關閉該 hello 主要虛擬機器。 如果沒有，兩部虛擬機器，以相同的身分識別將會執行您在相同網路的 hello hello hello 相同的時間。 這種情況下可能會導致 tooundesired 後果。
* 當您清除 hello 測試容錯移轉虛擬機器時，您進行 toohello 測試容錯移轉虛擬機器的任何變更都會遺失。 這些變更不是複寫後 toohello 主要虛擬機器。
* 如此一來，執行這項測試會導致 toodowntime 實際執行應用程式。 要求正在進行中的 hello 應用程式時 hello DR 向下切入 hello 應用程式不 toouse 的使用者。  


## <a name="next-steps"></a>後續步驟
成功執行測試容錯移轉之後，您就可以嘗試執行[容錯移轉](site-recovery-failover.md)。
