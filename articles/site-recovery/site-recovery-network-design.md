---
title: "aaaDesigning 網路基礎結構的災害復原 |Microsoft 文件"
description: "這篇文章討論 Azure Site Recovery 的網路設計考量"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>設計用於災害復原的網路

這篇文章會導向的 tooIT 專業人員負責架構、 實作和支援業務續航力和災害復原 (BCDR) 基礎結構，且需要 tooleverage Microsoft Azure 站台復原 (ASR) toosupport 和加強其 BCDR 服務。 本文討論在災害復原網站建構網路 (無論是 Azure 或其他內部部署網站) 的實際考量。 

## <a name="overview"></a>概觀
[Azure 站台復原 (ASR)](https://azure.microsoft.com/services/site-recovery/)是協調 hello 保護與復原您虛擬化應用程式供商務持續性災害復原 (BCDR) 的 Microsoft Azure 服務。 本文件是預定的 tooguide hello 讀取器的設計 hello 網路 hello 程序透過將焦點放在複寫虛擬機器 (Vm) 使用站台復原時，架構 IP 範圍和 hello 災害復原站台上的子網路。

此外，本文將示範站台復原可讓架構與實作多站台的虛擬資料中心 toosupport BCDR 服務時的測試或損毀。

在每個人都必須有 24/7 連線世界中，會比以往 tookeep 更重要基礎結構和應用程式啟動並執行。 hello 目的業務續航力和災害復原 (BCDR) 是 toorestore 失敗的元件，因此 hello 組織可以快速地恢復正常的作業。 開發不太可能、 破壞力事件與災害復原策略 toodeal 是非常具有挑戰性的。 這是因為 toohello 預測 hello 未來的固有的難度，特別與 tooimprobable 事件和 hello 高成本 tooprovide 防護深遠的災難事件的適當的量值。

BCDR 規劃的關鍵在於必須為災害復原計畫定義復原時間目標 (RTO) 和復原點目標 (RPO)。 當發生災害事件 hello 客戶的資料中心，請使用 Azure Site Recovery，客戶可以快速地 (低 RTO) 上線其複寫的虛擬機器位於 hello 次要資料中心或 Microsoft Azure 中最小的資料遺失 (低 RPO)。

容錯移轉即可進行 ASR 這一開始從 hello 主要資料中心 toohello 次要資料中心或 tooAzure （hello 視案例而定），會複製指定之的虛擬機器，然後定期更新 hello 複本。 規劃基礎結構時，應將網路設計視為潛在瓶頸，可能會讓您無法達成公司的 RTO 和 RPO 目標。  

當系統管理員計劃 toodeploy 災害復原解決方案時，脫離 hello 主要問題的其中一個是如何 hello 虛擬機器連線到 hello 容錯移轉完成之後。 ASR 可讓 hello 管理員 toochoose hello 網路 toowhich 虛擬機器會連接的 tooafter 容錯移轉。 如果 hello 主要站台位於 Azure 或其為受 VMM 伺服器，則這藉由使用網路對應，在內部部署網站。 深入了解[網路對應，在 Azure tooAzure DR](site-recovery-network-mapping-azure-to-azure.md)和[網路對應，從 VMM](site-recovery-network-mapping.md)


設計時 hello 復原站台的 hello 網路，hello 系統管理員具有兩個選擇：

* 在復原站台的 hello 網路使用不同的 IP 位址範圍。 在此案例中 hello 虛擬機器在容錯移轉之後會收到新的 IP 位址，hello 系統管理員必須 toodo DNS 更新。 
* 在 hello 復原站台的 hello 網路使用相同的 IP 位址範圍。 在某些案例中系統管理員會偏好 hello 容錯移轉之後，即使 hello 主要站台他們擁有的 tooretain hello IP 位址。 在正常實例中系統管理員必須 tooupdate hello 路由 tooindicate hello 新位置的 hello IP 位址。 但是在 hello 案例延展的子網路之間主要的 hello 和 hello 復原站台的部署位置中，保留 hello hello 虛擬機器的 IP 位址會變成的理想選擇。 自動縮放的子網路，從內部部署網路 tooan Azure 網路，或兩個 Azure 網路之間不可能。  

系統管理員計劃 toodeploy 災害復原解決方案，其記住 hello 主要問題的其中一個時如何 hello 應用程式將會連線到 hello 容錯移轉完成之後。 現代應用程式幾乎一律會相依於網路 toosome 程度，因此實際移動一個站台 tooanother 服務代表網路挑戰的。 在災害復原解決方案中，解決這個問題有兩種主要方法。 hello 第一種方法是 toomaintain 固定 IP 位址。 儘管 hello 服務移動和 hello 主控伺服器的不同實體位置中，應用程式會將 hello IP 位址設定，且它們 toohello 新位置。 hello 第二種方法牽涉到完全 hello 復原的站台的 hello 轉換期間變更 hello IP 位址。 每一種方法有數個實作變化，摘要說明如下。

設計時 hello 復原站台的 hello 網路，hello 系統管理員具有兩個選擇：

## <a name="option-1-retain-ip-addresses"></a>選項 1：保留 IP 位址
從嚴重損壞修復程序觀點來看，使用固定 IP 位址會出現 toobe hello 最簡單方法 tooimplement，但是它有可能的一些挑戰這實際上會讓 hello 最不常用的方法。 Azure Site Recovery 提供 hello 功能 tooretain hello IP 位址在所有案例。 其中一個決定 tooretain IP 之前，請適當思考應該具備 toohello 條件約束，它會施加在 hello 容錯移轉功能。 讓我們看看，可協助您決定 tooretain IP 位址，或不 toomake hello 因素。 可以透過兩種方式來達成，使用延伸的子網路，或執行完整的子網路容錯移轉。

### <a name="stretched-subnet"></a>延伸的子網路
這裡 hello 子網路可同時在主要位置與 DR 位置。 簡單地說，這表示您可以移動伺服器並與其 IP (第 3 層) 組態 toohello 第二個網站和 hello 網路會自動將路由傳送 hello 流量 toohello 新位置。 這是簡單式 toodeal 與從伺服器的觀點來看，但有一些挑戰：

* 從第 2 層 (資料連結層) 觀點來看，它將需要可以管理延伸的 VLAN 的網路設備，不過這不成問題，因為它現在已普遍使用。 hello 第二個和更加困難的問題是縮放 hello VLAN hello 潛在容錯網域就會延伸 tooboth 站台，基本上成為單一失敗點。 雖然不太可能，過去曾經發生過廣播風暴但無法隔離。 關於這個問題我們得到各種意見，看過許多成功的實作，也遇過「我們永遠不會實作這種技術」的人。
* 延展的子網路不可能，如果您使用 Microsoft Azure 時，因為 hello DR 網站。

### <a name="subnet-failover"></a>子網路容錯移轉
很可能 tooimplement 子網路容錯移轉 tooobtain hello 的優點上面所述但不在多個站台之間自動縮放 hello 子網路的延展 hello 子網路解決方案。 若採取此做法，任何給定的子網路會出現在網站 1 或網站 2 中，但永遠不會同時出現在這兩個網站。 在訂單 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，可能會針對 hello 路由器基礎結構 toomove hello 的子網路從一個站台 tooanother 排列 tooprogrammatically。 在子網路會容錯移轉案例 hello 以 hello 移動相關的受保護的 Vm。 hello 失敗事件中的 hello 主要缺點 toothis 的方法是，您具有 toomove hello 整個子網路，可能是 [確定]，但它可能會影響 hello 容錯移轉的資料粒度考量。

讓我們來檢查名為 Contoso 的虛構企業的方式可以 tooreplicate 時容錯移轉 hello 整個子網路的 Vm tooa 復原位置。 我們將先探討如何 Contoso 是能 toomanage 它們子網路時複寫 Vm 兩個內部部署位置，然後我們將討論的子網路容錯移轉如何運作時[Azure 做為 hello 災害復原站台](#failover-to-azure)。

#### <a name="failover-from-on-premises-tooazure"></a>從內部部署 tooAzure 容錯移轉 
Azure 站台復原 (ASR) 可讓您的虛擬機器做為災害復原站台的 Azure toobe。  

讓我們看看這個案例，虛構公司 Woodgrove Bank 的內部部署基礎結構裝載了企業營運系統應用程式，其行動裝置應用程式則裝載在 Azure 之上。 Azure 中的 Woodgrove Bank VM 以及內部部署伺服器之間的連線能力，由站對站 (S2S) 虛擬私人網路 (VPN) 或 ExpressRoute 提供。 S2S VPN 允許 Azure toobe 視為 Woodgrove Bank 的延伸模組為內部網路中的 Woodgrove Bank 的虛擬網路。 這項通訊由 Woodgrove Bank 邊緣和 Azure 虛擬網路之間的 S2S VPN 實現。 現在 Woodgrove 想 toouse ASR tooreplicate 其執行主要 Azure 地區 tooanother Azure 區域的工作負載。 此選項會符合 hello Woodgrove 想經濟的 DR 選項及公用雲端環境中的無法 toostore 資料需求。 Woodgrove toodeal 與應用程式和相依於硬式編碼的 IP 位址組態，因此他們對應用程式的需求 tooretain IP 位址失敗之後 tooanother 在 Azure 中的區域。

Woodgrove 已決定在 Azure 中執行的 IP 位址範圍 （172.16.1.0/24，172.16.2.0/24） tooits 資源 tooassign IP 位址。

Woodgrove toobe 無法 tooreplicate 同時保留 hello IP 位址，其虛擬機器 tooAzure Azure 虛擬網路必須 toobe 建立。 它應該 hello 在內部部署網路的延伸，讓應用程式可以順暢地從 hello 在內部部署站台 tooAzure 容錯移轉。 Azure 可讓您 tooadd 站對站和點對站 VPN 連線能力 toohello 虛擬網路在 Azure 中建立。 設定站對站連線，請 Azure 網路您 tooroute 流量 toohello 在內部部署位置 （Azure 會呼叫它本機網路） 時才允許 hello IP 位址範圍是不同於 hello 內部 IP 位址範圍，因為 Azure 不支援自動縮放的子網路。  這表示，如果您有子網路 192.168.1.0/24 內部，您無法加入本機網路 192.168.1.0/24 hello Azure 網路中。 這是預期行為，因為 Azure 不知道 hello 子網路中有任何作用中的 Vm，以及正在建立 hello 子網路只適用於 DR 用途。 toobe toocorrectly 無法路由傳送網路流量超出 hello 網路和 hello 本機網路中的 Azure 網路 hello 子網路必須不會發生衝突。

![子網路容錯移轉之前](./media/site-recovery-network-design/network-design7.png)

容錯移轉之前

toohelp Woodgrove 滿足其商業需求，我們需要 tooimplement hello 下列工作流程：

* 建立額外的網路，讓我們呼叫會在其中建立 hello 容錯虛擬機器的復原網路。
* VM 的 hello IP 會容錯移轉之後，保留 tooensure toohello VM 屬性底下的設定 索引標籤，指定的 hello hello VM 的相同 IP 已在內部，然後按一下儲存。 當 hello VM 容錯移轉時，Azure Site Recovery 會指派 hello 提供 IP toohello 虛擬機器。

![網路屬性](./media/site-recovery-network-design/network-design8.png)

一旦觸發 hello 容錯移轉時，並在 hello 復原所需的 hello IP 網路中建立 hello 虛擬機器，可以使用建立連線 toothis 網路[Vnet tooVnet 連接](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。 如果需要，此動作可以編寫指令碼。  如前述 hello 前一節中有關子網路容錯移轉，即使在 hello 情況下，容錯移轉 tooAzure 的路由，會有 toobe 適當地修改 tooreflect 該 192.168.1.0/24 現在已移 tooAzure。

![子網路容錯移轉之後](./media/site-recovery-network-design/network-design9.png)

容錯移轉之後

如果您沒有 Azure 網路 ' hello 如上圖所示。 Hello 容錯移轉之後，您可以建立您的 '主要站台' 和 ' Recovery 網路 」 之間的站台 toosite vpn 連線。  


#### <a name="failover-tooa-secondary-on-premises-site"></a>容錯移轉 tooa 次要內部部署站台
讓我們看看案例，我們想要保留每個 hello Vm 的 hello IP 和容錯移轉 hello 一起完成子網路。 hello 主要站台的子網路 192.168.1.0/24 中執行的應用程式。 當 hello 容錯移轉發生時，所有屬於這個子網路的 hello 虛擬機器的容錯移轉 toohello 復原站台，並保留其 IP 位址。 路由會有 toobe 適當地修改 tooreflect hello 事實所有 hello 虛擬機器屬於 toosubnet 192.168.1.0/24 現已都移 toohello 復原站台。

在 hello 下列圖例 hello 將主要站台和復原站台、 第三個網站和主要站台之間路由，而第三個網站和復原站台 toobe 適當修改。

下列圖片顯示 hello 子網路 hello 容錯移轉之前的 hello。 子網路 192.168.0.1/24 hello 容錯移轉之前 hello 主要站台上為作用中和 hello 容錯移轉之後會變成作用中的 hello 復原站台

![容錯移轉之前](./media/site-recovery-network-design/network-design2.png)

容錯移轉之前

hello 圖會顯示網路和子網路容錯移轉之後。

![容錯移轉之後](./media/site-recovery-network-design/network-design3.png)

容錯移轉之後

次要站台是在內部部署，而且您正在使用 VMM 伺服器 toomanage 然後時啟用保護特定的虛擬機器，ASR 將配置根據 toohello 下列工作流程的網路功能資源：

* ASR 從 hello 靜態 IP 位址集區 hello 相關網路，每個 System Center VMM 執行個體上定義每個網路介面 hello 虛擬機器上配置的 IP 位址。
* 如果 hello 系統管理員定義相同的 IP 位址為 hello 復原站台上的 hello 網路集區，hello 主要站台上，在配置 hello IP 位址 toohello 複本虛擬機器 ASR 時的網路會 hello hello 的 IP 位址集區配置，hello hello 相同Hello 主要虛擬機器的 IP 位址。  hello IP 已保留在 VMM 中，但未設定為容錯移轉 IP hello hyper-v 主機上。 Hyper-v 主機上的容錯移轉 IP 設定之前 hello 容錯移轉。


如果 hello 相同 IP 無法使用，ASR 會從 hello 定義 IP 位址集區配置一些其他可用的 IP 位址。

Hello VM 已啟用保護之後，您可以使用下列範例指令碼 tooverify hello IP 已配置 toohello 虛擬機器。 會設定為容錯移轉 IP 和容錯移轉的 hello 次指派 toohello VM 相同的 IP hello:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> 在 hello 案例中，虛擬機器使用 DHCP，hello 管理的 IP 位址超出完全 ASR hello 控制。 系統管理員具有 tooensure hello DHCP 伺服器服務 hello IP 位址 hello 復原站台上的可從 hello 做相同的 hello 主要站台的範圍。
>
>



## <a name="option-2-changing-ip-addresses"></a>選項 2：變更 IP 位址
這種方法看起來 toobe hello 最普遍根據我們已經看到。 它會採用 hello 形式變更 hello 的 hello 容錯移轉中涉及的每個 VM 的 IP 位址。 這個方法的缺點需要連入網路 too'learn hello' hello 應用程式時的 IPx 現在位於 IPy。 即使 IPx 和 IPy 邏輯名稱，DNS 項目通常會有 toobe 變更或清除整個 hello 網路，而且網路資料表中的快取項目具有 toobe 更新或排清，因此停機時間可能出現具有 hello DNS 基礎結構的方式而定已安裝。 使用低 TTL 值在內部網路應用程式的 hello 案例中，並使用可減輕這些問題[ASR 與 Azure Traffic Manger](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/)以網際網路為基礎的應用程式

### <a name="changing-hello-ip-addresses---illustration"></a>變更圖例的 hello IP 位址-
讓我們看看 hello 案例規劃 toouse 在 hello 主要與 hello 復原站台的不同 Ip。 在下列範例中的 hello 我們也會有主要或復原站台上裝載的 hello 應用程式可以存取其中的第三個站台。

![不同的 IP - 容錯移轉之前](./media/site-recovery-network-design/network-design10.png)


在上面的 hello 圖片有某些 hello 主要站台上的子網路 192.168.1.0/24 子網路中裝載的應用程式，並已設定的 toocome 向上 172.16.1.0/24 子網路中的 hello 復原站台上的容錯移轉之後。 已適當地設定 VPN 連線/網路路由，讓所有的三個站台可以互相存取。

為 hello 圖片所示，容錯移轉一或多個應用程式之後它們將會還原 hello 復原子網路中。 在此情況下我們並未限制的 toofailover hello 整個子網路 hello 在相同的時間。 不不需要的 tooreconfigure VPN 或網路路由的任何變更。 容錯移轉和某些 DNS 更新會確定應用程式可供存取。 如果 hello DNS 設定的 tooallow 動態更新然後 hello 虛擬機器會自行註冊使用 hello 新 IP，一旦他們在容錯移轉之後啟動。

![不同的 IP - 容錯移轉之後](./media/site-recovery-network-design/network-design11.png)


容錯移轉 hello 複本虛擬機器可能有不是 IP 位址之後 hello 相同 hello hello 主要虛擬機器的 IP 位址。 虛擬機器將會更新他們使用的 hello DNS 伺服器啟動之後。 DNS 項目通常有 toobe 變更或清除整個 hello 網路，網路資料表中的快取項目有 toobe 更新或排清，因此並不常見 toobe 面臨這些狀態變更發生時的停機時間。 減輕這個問題的方法有：

* 對內部網路應用程式使用低 TTL 值。
* 對網際網路架構應用程式使用 Azure 流量管理員與 ASR。
* 使用 hello 下列指令碼中您的復原計劃 tooupdate hello DNS 伺服器 tooensure 及時更新 （hello 指令碼不需要如果 hello 動態 DNS 登錄設定）

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>變更 hello IP 位址 – DR tooAzure
hello[作為災害復原站台的 Microsoft azure 網路基礎結構安裝](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)部落格文章說明如何 toosetup hello 需要 Azure 網路基礎結構時保留的 IP 位址不需要。 開頭描述 hello 應用程式，然後查看如何 toosetup 網路內部部署在 Azure 上的 如何 toodo 測試容錯移轉和已規劃的容錯移轉。

## <a name="next-steps"></a>後續步驟
[深入了解](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping)當 VMM 伺服器使用的 toomanage hello 主要站台站台復原對應來源及目標網路的方式。
