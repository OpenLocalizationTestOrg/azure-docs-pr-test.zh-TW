---
title: "Azure Site Recovery：常見問題集 | Microsoft Docs"
description: "本文討論 Azure Site Recovery 的相關熱門問題。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery：常見問題集 (FAQ)
本文包含有關 Azure Site Recovery 的常見問題集。 如果您閱讀本文之後有問題，張貼在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)。

## <a name="general"></a>一般
### <a name="what-does-site-recovery-do"></a>Site Recovery 的功能是什麼？
站台復原提供 tooyour 業務續航力和災害復原 (BCDR) 策略，來協調及自動化 Azure Vm 的區域、 在內部部署虛擬機器和實體伺服器 tooAzure 之間的複寫和內部部署機器 tooa次要資料中心。 [深入了解](site-recovery-overview.md)。

### <a name="what-can-site-recovery-protect"></a>Site Recovery 可以保護什麼？
* **Azure VM**：Site Recovery 可複寫在支援的 Azure VM 上執行的任何工作負載。
* **Hyper-V 虛擬機器**：Site Recovery 可以保護 Hyper-V VM 上執行的任何工作負載。
* **實體伺服器**：Site Recovery 可以保護執行 Windows 或 Linux 的實體伺服器。
* **VMware 虛擬機器**：Site Recovery 可以保護 VMware VM 上執行的任何工作負載。

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>站台復原支援 hello Azure Resource Manager 模型？
Hello 與支援資源管理員的 Azure 入口網站使用站台復原。 站台復原支援舊版部署 hello Azure 傳統入口網站中。 您無法在 hello 傳統入口網站，建立新的保存庫並不支援新功能。

### <a name="can-i-replicate-azure-vms"></a>我可以複寫 Azure VM 嗎？
是，您可以在 Azure 區域之間複寫支援的 Azure VM。 [深入了解](site-recovery-azure-to-azure.md)。

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>我需要 HYPER-V tooorchestrate 複寫與站台復原中？
Hello HYPER-V 主機伺服器配備取決於 hello 部署案例。 簽出 hello HYPER-V 中的先決條件：

* [複寫 （無 VMM) 的 HYPER-V Vm tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [複寫 （使用 VMM) 的 HYPER-V Vm tooAzure](site-recovery-vmm-to-azure.md)
* [複寫 HYPER-V Vm tooa 次要資料中心](site-recovery-vmm-to-vmm.md)
* 如果您要複寫 tooa 次要資料中心，閱讀有關[支援客體作業系統的 HYPER-V Vm](https://technet.microsoft.com/library/mt126277.aspx)。
* 如果您要複寫 tooAzure，站台復原支援所有 hello 客體作業系統的[Azure 支援](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx)。

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>當 Hyper-V 在用戶端作業系統上執行時，我可以保護 VM 嗎？
不能，VM 所在的 Hyper-V 主機伺服器必須在支援的 Windows 伺服器機器上執行。 如果您需要 tooprotect 用戶端電腦無法複製為實體機器太[Azure](site-recovery-vmware-to-azure.md)或[次要資料中心](site-recovery-vmware-to-vmware.md)。

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>我可以使用 Site Recovery 來保護哪些工作負載？
您可以使用站台復原 tooprotect 大部分支援的 VM 或實體伺服器上執行的工作負載。 站台復原提供支援應用程式感知的複寫，使應用程式可以復原 tooan 智慧型狀態。 除了與 Microsoft 應用程式 (例如 SharePoint、Exchange、Dynamics、SQL Server 及 Active Directory) 整合之外，它還與產業龍頭 (包括 Oracle、SAP、IBM 及 Red Hat) 密切合作。 [深入了解](site-recovery-workload.md) 工作負載保護。

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>HYPER-V 主機需要 toobe VMM 雲端中的嗎？
如果您想 tooreplicate tooa 次要資料中心，則 HYPER-V Vm 必須是在 HYPER-V 裝載位於 VMM 雲端中的伺服器。 如果您想 tooreplicate tooAzure，您可以在 VMM 雲端，不論 HYPER-V 主機伺服器上複寫 Vm。 [閱讀更多資訊](site-recovery-hyper-v-site-to-azure.md)。

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>如果我只有一部 VMM 伺服器，可以部署 Site Recovery 搭配 VMM 嗎？

是。 您可以將 Vm 複寫在 hello VMM 雲端 tooAzure 中的 HYPER-V 伺服器或您可以將複寫 hello 上的 VMM 雲端之間相同伺服器。 在內部部署 tooon 內部部署複寫，我們建議您將 VMM 伺服器有兩個 hello 主要和次要網站中。  

### <a name="what-physical-servers-can-i-protect"></a>我可以保護哪些實體伺服器？
您可以將執行 Windows 和 Linux tooAzure 或 tooa 次要站台的實體伺服器複寫。 [了解](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 作業系統需求。  相同的需求都適用於您要複寫的實體伺服器 tooAzure 或 tooa 次要站台是否 hello。


請注意，如果您的內部部署伺服器當機，實體伺服器將會在 Azure 中以 VM 的身分執行。 容錯回復 tooan 內部部署實體伺服器，目前不支援。 實體的受保護的機器，您可以只容錯回復 tooa VMware 虛擬機器。

### <a name="what-vmware-vms-can-i-protect"></a>我可以保護哪些 VMware VM？

VMware Vm tooprotect 您將需要 vSphere hypervisor 和虛擬機器執行 VMware 工具。 我們也建議您有 VMware vCenter server toomanage hello hypervisor。 [進一步了解](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)有關複寫 VMware 伺服器和 Vm tooAzure 或 tooa 次要站台的正確需求。


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>我可以使用 Site Recovery 來管理分公司的災害復原嗎？
是。 當您使用站台復原 tooorchestrate 複寫和容錯移轉，分公司中時，您會取得儲存在集中位置的統一的協調流程並檢視所有分公司辦公室工作負載。 您可以輕鬆地執行容錯移轉，且管理的所有分支的災害復原，從總公司，不需要造訪 hello 分支。

## <a name="pricing"></a>價格

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>使用 Azure Site Recovery 時有哪些費用？
當您使用站台復原時，您就會產生 hello Site Recovery 授權、 Azure 儲存體、 儲存體交易和傳出資料傳輸費用。 [深入了解](https://azure.microsoft.com/pricing/details/site-recovery)。

hello Site Recovery 授權是每個受保護的執行個體，其中執行個體是 VM 或實體伺服器。

- 如果 VM 磁碟複寫 tooa 標準儲存體帳戶，hello Azure 儲存體費用就是 hello 存放裝置耗用量。 比方說，如果 hello 來源磁碟大小是使用 1 TB 和 400 GB，站台復原會將 1 TB VHD 建立在 Azure 中，但收費的 hello 儲存體是 400 GB （加上 hello 複寫記錄檔所使用的儲存空間）。
- 如果 VM 磁碟複寫 tooa 進階儲存體帳戶，hello Azure 儲存體費用就是 hello 佈建儲存體大小，四捨五入 hello 最接近的 premium 儲存體磁碟的選項。 例如，如果 hello 來源磁碟大小是 50 GB，站台復原會在 Azure 中，建立 50 GB 磁碟和 Azure 對應此 toohello 最接近的 premium 儲存體磁碟 (P10)。  Hello 50 GB 磁碟大小 P10，而非計算成本。  [深入了解](https://aka.ms/premium-storage-pricing)。  如果您使用進階儲存體，複寫記錄的標準儲存體帳戶也是必要項，，且這些記錄檔所使用的標準儲存體空間的 hello 數量也計費。
- 在測試容錯移轉或容錯移轉發生之前，不會建立任何磁碟。 Hello 複寫狀態，在儲存體費用的 「 分頁 blob 和磁碟 」 的 hello 類別下根據 hello[儲存體定價計算機](https://azure.microsoft.com/en-in/pricing/calculator/)所造成。 這些費用根據 hello premium/standard 和 hello 資料備援的儲存類型輸入-LRS、 GRS，RA-GRS 等等。
- 選取在容錯移轉時如果 hello 選項 toouse 管理上的磁碟，[的受管理的磁碟計費](https://azure.microsoft.com/en-in/pricing/details/managed-disks/)測試容錯移轉/容錯移轉後套用。 在複寫期間不會套用受控磁碟的費用。
- 根據 hello 如果未選取 hello 選項 toouse 管理磁碟容錯移轉，儲存體費用的 「 分頁 blob 和磁碟 」 的 hello 類別下[儲存體定價計算機](https://azure.microsoft.com/en-in/pricing/calculator/)容錯移轉之後所造成。 這些費用根據 hello premium/standard 和 hello 資料備援的儲存類型輸入-LRS、 GRS，RA-GRS 等等。
- 在穩定狀態複寫期間，以及容錯移轉/測試容錯移轉之後的一般 VM 操作，均會收取儲存體交易費用。 不過，這些費用微乎其微。

測試容錯移轉期間，將會套用 hello VM、 儲存體、 輸出和儲存體交易成本，也會產生成本。



## <a name="security"></a>安全性
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>複寫資料傳送 toohello Site Recovery 服務嗎？
否，Site Recovery 不會攔截複寫的資料，也不會擁有任何關於您虛擬機器或實體伺服器上執行哪些項目的資訊。
內部部署 Hyper-V 主機、VMware Hypervisor 或實體伺服器，會與 Azure 儲存體或次要站台交換複寫資料。 Site Recovery 有沒有能力 toointercept 該資料。 只有 hello 中繼資料所需 tooorchestrate 複寫和容錯移轉會傳送 toohello Site Recovery 服務。  

站台復原是 ISO 27001: 2013，27018、 HIPAA、 DPA 認證，及為 hello SOC2 和 JAB fedramp 是評估程序。

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>基於相容性因素，即使我們在內部部署的中繼資料必須保留在 hello 相同地理區域。 Site Recovery 可以幫助我們嗎？
是。 當您在區域中建立站台復原保存庫時，我們就會確保我們需要 tooenable 以及協調複寫和容錯移轉會保留該區域內的所有中繼資料的地理界限。

### <a name="does-site-recovery-encrypt-replication"></a>Site Recovery 會將複寫加密嗎？
就虛擬機器和實體伺服器而言，在內部部署站台之間進行複寫時，支援傳輸中加密。 虛擬機器和實體伺服器複寫 tooAzure，這兩個加密傳輸中和[加密靜止 （在 Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)支援。

## <a name="replication"></a>複寫

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>我可以透過站對站 VPN tooAzure 複寫嗎？
Azure Site Recovery 會將資料 tooan Azure 儲存體帳戶，複寫會透過公用端點。 複寫不是透過站對站 VPN。 您可以透過 Azure 虛擬網路建立站對站 VPN。 這並不會影響 Site Recovery 複寫。

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>可以使用 ExpressRoute tooreplicate 虛擬機器 tooAzure 嗎？
是，ExpressRoute 可以使用的 tooreplicate 虛擬機器 tooAzure。 Azure Site Recovery 會將複寫資料 tooan Azure 儲存體帳戶會透過公用端點。 您需要 tooset 向上[公用對等互連](../expressroute/expressroute-circuit-peerings.md#public-peering)toouse ExpressRoute Site Recovery 的複寫。 Hello 虛擬機器已容錯 tooan Azure 虛擬網路之後，您可以存取這些使用 hello[私人互連](../expressroute/expressroute-circuit-peerings.md#private-peering)hello Azure 虛擬網路設定。

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>有任何複寫的虛擬機器 tooAzure 必要條件嗎？
您想 tooreplicate tooAzure 虛擬機器應該符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>可複寫 HYPER-V 層代 2 的虛擬機器 tooAzure 嗎？
是。 在容錯移轉期間，從第 2 代 toogeneration 1 轉換站台復原。 在容錯回復 hello 機器是轉換後 toogeneration 2。 [閱讀更多資訊](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)。

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>如果複製的 tooAzure 我該如何購買 Azure Vm？
規則在複寫期間，資料會複寫的 toogeo 備援的 Azure 儲存體，您不需要 toopay 任何 Azure IaaS 虛擬機器的費用，提供更大的優點。 當您執行容錯移轉 tooAzure，Site Recovery 會自動建立 Azure IaaS 虛擬機器，並後，您將支付 hello 您在 Azure 中使用的計算資源。

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>我是否可以透過 SDK 自動化 Site Recovery 案例？
是。 您可以自動使用 Rest API hello、 PowerShell 或 hello Azure SDK 的站台復原工作流程。 針對使用 PowerShell 來部署 Site Recovery，目前支援的案例包括︰

* [HYPER-V Vm 複寫 Vmm 雲端 tooAzure PowerShell 資源管理員](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [HYPER-V Vm 複寫沒有 VMM tooAzure PowerShell 資源管理員](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>如果複製 tooAzure 我需要何種儲存體帳戶？
* **Azure 傳統入口網站**： 如果您要部署站台復原 hello Azure 傳統入口網站中，您將需要[標準異地備援儲存體帳戶](../storage/common/storage-redundancy.md#geo-redundant-storage)。 目前不支援進階儲存體。 hello 帳戶必須在 hello 與 hello Site Recovery 保存庫相同的區域。
* **Azure 入口網站**： 如果您要部署站台復原 hello Azure 入口網站中，您必須為 LRS 或 GRS 的儲存體帳戶。 我們建議 GRS，使資料彈性地區的中斷發生，或如果 hello 主要區域無法復原。 hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。 高階儲存體現在支援 VMware VM、 HYPER-V VM 和實體伺服器複寫，當您將站台復原部署 hello Azure 入口網站中。

### <a name="how-often-can-i-replicate-data"></a>我可以多久複寫一次資料？
* **Hyper-V：**可以每隔 30 秒、5 分鐘或 15 分鐘複寫一次 Hyper-V VM (進階儲存體除外)。 如果您已設定 SAN 複寫，則複寫會是同步的。
* **VMware 與實體伺服器：** 複寫頻率在此處並不相關。 複寫是連續的。

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>可以延伸從現有復原站台 tooanother 第 3 的站台的複寫嗎？
不支援延伸的或鏈結的複寫。 請在 [意見反應論壇](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication)中提出這項功能的要求。

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>可以進行離線複寫 hello tooAzure 複製的第一次？
不支援此做法。 要求這項功能在 hello[意見反應論壇](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from)。

### <a name="can-i-exclude-specific-disks-from-replication"></a>我可以從複寫中排除特定的磁碟嗎？
當您使用支援這種[複寫 VMware Vm 和 HYPER-V Vm](site-recovery-exclude-disk.md) tooAzure，使用 hello Azure 入口網站。

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>我可以使用動態磁碟來複寫虛擬機器嗎？
複寫 Hyper-V 虛擬機器時，支援使用動態磁碟。 它們也支援 VMware Vm 和實體機器 tooAzure 複寫時。 hello 作業系統磁碟必須是基本磁碟。

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>可以加入新機器 tooan 現有複寫群組嗎？
將新的機器 tooexisting 複寫群組新增支援。 toodo，選取 hello （從 [複寫項目] 刀鋒視窗） 的複寫群組 」 和 「 hello 複寫群組上的按一下滑鼠右鍵，選擇內容功能表，然後選取 hello 適當的選項。

![新增 tooreplication 群組](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>我可以調節為 Hyper-V 複寫流量配置的頻寬嗎？
是。 閱讀更多關於節流的頻寬以 hello 部署文件：

* [適用於複寫 VMware VM 和實體伺服器的容量規劃](site-recovery-plan-capacity-vmware.md)
* [適用於複寫 VMM 雲端中 Hyper-V VM 的容量規劃](site-recovery-vmm-to-azure.md#capacity-planning)
* [適用於複寫不使用 VMM 之 Hyper-V VM 的容量規劃](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>容錯移轉
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>如果我在容錯移轉 tooAzure，如何存取 hello Azure 容錯移轉後的虛擬機器？
您可以存取 hello Azure Vm 上安全的網際網路連線、 透過站對站 VPN，或透過 Azure ExpressRoute。 您將需要 tooprepare 幾項工作順序 tooconnect。 [深入了解](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>如果我容錯移轉如何 Azure 對確定 tooAzure 我的資料是具有恢復功能？
Azure 是針對復原能力而設計的。 容錯移轉 tooa 次要 Azure 資料中心，依據 Azure SLA 如果 hello 需要就會發生的 hello 已經工程設計站台復原。 如果發生這種情況，我們會先確認您的中繼資料和保存庫內 hello 您選擇您的保存庫的相同地理區域。  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>如果我在兩個資料中心之間進行複寫，當我的主要資料中心發生意外中斷時，會發生什麼情況？
您可以觸發非計劃性容錯移轉從 hello 次要站台。 Site Recovery 並不需要從 hello 主要站台 tooperform hello 容錯移轉的連線。

### <a name="is-failover-automatic"></a>容錯移轉是自動發生的嗎？
容錯移轉並非自動發生。 起始容錯移轉，只按一下在 hello 入口網站，或者您可以使用[站台復原 PowerShell](/powershell/module/azurerm.siterecovery) tootrigger 容錯移轉。 傳回不是 hello Site Recovery 入口網站的簡單動作。

您可以使用的 tooautomate 內部 Orchestrator 或 Operations Manager toodetect 虛擬機器失敗，以及然後觸發程序 hello 容錯移轉使用 hello SDK。

* [閱讀更多](site-recovery-create-recovery-plans.md) 復原方案的相關資訊。
* [深入了解](site-recovery-failover.md) 容錯移轉。
* [深入了解](site-recovery-failback-azure-to-vmware.md) 如何容錯回復 VMware VM 和實體伺服器

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>如果我在內部部署的主機未回應或損毀，我可以容錯移轉後 tooa 不同的主機嗎？
是，您可以使用 hello 替代位置復原 toofailback tooa 不同主機從 Azure。 深入了解有關 hello 下方連結中的 hello 選項針對 VMware 和 hyper-v 虛擬機器。

* [針對 VMware 虛擬機器](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [針對 Hyper-V 虛擬機器](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>服務提供者
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>我是服務提供者。 Site Recovery 是否適用於專用和共用基礎結構模型？
是，Site Recovery 同時支援專用與共用的基礎結構模型。

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>為服務提供者，是 hello 識別與 hello Site Recovery 服務共用我的租用戶嗎？
否。 租用戶身分識別會保持匿名。 您的租用戶不需要存取 toohello Site Recovery 入口網站。 只有 hello 服務提供者的管理員互動 hello 入口網站。

### <a name="will-tenant-application-data-ever-go-tooazure"></a>將租用戶應用程式資料曾經尋求 tooAzure？
當服務提供者所擁有的站台間複寫，應用程式資料永遠不會 tooAzure。 在傳輸中和 hello 服務提供者站台之間的直接複寫加密資料。

如果您要複寫 tooAzure，應用程式資料會傳送 tooAzure 存放裝置，但 toohello Site Recovery 服務。 資料會在傳輸中加密並在 Azure 中繼續維持加密狀態。

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>我的租用戶會收到來自 Azure 服務的帳單嗎？
否。 Azure 的計費的關聯性是直接與 hello 服務提供者。 服務提供者負責為其租用戶產生特定的帳單。

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>如果我正在複寫 tooAzure，我們需要 toorun 在 Azure 虛擬機器隨時都能？
否，資料會複寫的 tooan 您訂用帳戶中的 Azure 儲存體帳戶。 當您執行測試容錯移轉 (DR 演練) 或實際容錯移轉時，Site Recovery 會自動在您的訂用帳戶中建立虛擬機器。

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>複製 tooAzure 時確保租用戶層級隔離嗎？
是。

### <a name="what-platforms-do-you-currently-support"></a>目前支援哪些平台？
我們支援「Azure 套件」、「雲端平台系統」及 System Center 架構 (2012 及更新版本) 的部署。 [深入了解](https://technet.microsoft.com/library/dn850370.aspx) 「Azure 套件」和 Site Recovery 整合

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>您支援單一 Azure 套件與單一 VMM 伺服器部署嗎？
是，您可以將複寫 HYPER-V 虛擬機器 tooAzure，或服務提供者站台之間。  請注意，如果您是在服務提供者站台之間進行複寫，將無法使用 Azure Runbook 整合。

## <a name="next-steps"></a>後續步驟
* 讀取 hello[站台復原概觀](site-recovery-overview.md)
* 了解 [Site Recovery 架構](site-recovery-components.md)  
