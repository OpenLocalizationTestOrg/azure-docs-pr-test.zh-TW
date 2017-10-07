---
title: "使用 Azure Site Recovery 的多層式 Citrix XenDesktop 和 XenApp 部署 aaaReplicate |Microsoft 文件"
description: "本文說明如何 tooprotect 和復原 Citrix XenDesktop 和 XenApp 部署使用 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>使用 Azure Site Recovery 複寫多層式 Citrix XenApp 和 XenDesktop 部署

## <a name="overview"></a>概觀

Citrix XenDesktop 是身為 ondemand 服務 tooany 使用者，任何位置提供桌面與應用程式的桌面虛擬化解決方案。 FlexCast 傳遞技術，XenDesktop 可以快速且安全的方式傳遞應用程式和桌面 toousers。
現在，Citrix XenApp 不提供任何災害復原功能。

理想的災害復原解決方案，應該上方複雜的應用程式架構允許 hello 周圍的復原方案的模型，而且也具有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應因此提供的各層單鍵確定 hello 開頭 tooa 災害事件中擷取畫面方案降低 RTO。

對於為 Hyper-V 和 VMware vSphere 平台上的內部部署 Citrix XenApp 部署建置災害復原方案，本文提供逐步指引。 本文也說明如何 tooperform 測試容錯移轉 （災害復原訓練） 和非計劃的容錯移轉 tooAzure 使用復原計劃、 支援的 hello 組態和必要條件。


## <a name="prerequisites"></a>必要條件

開始之前，請確定您了解 hello 下列：

1. [複寫虛擬機器 tooAzure](site-recovery-vmware-to-azure.md)
1. 如何太[設計與復原網路](site-recovery-network-design.md)
1. [執行測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)
1. [執行容錯移轉 tooAzure](site-recovery-failover.md)
1. 如何太[複寫的網域控制站](site-recovery-active-directory.md)
1. 如何太[複寫 SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>部署模式

Citrix XenApp 和 XenDesktop 的伺服器陣列通常具有下列部署模式的 hello:

**部署模式**

AD DNS 伺服器、SQL 資料庫伺服器、Citrix 傳遞控制站、StoreFront 伺服器，XenApp Master (VDA)、Citrix XenApp 授權伺服器的 Citrix XenApp 和 XenDesktop 部署

![部署模式 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Site Recovery 支援

Hello 本文的目的，在 VMware 虛擬機器的 Citrix 部署管理的 vSphere 6.0/System Center VMM 2012 R2 已使用的 toosetup DR。

### <a name="source-and-target"></a>來源與目標

**案例** | **tooa 次要站台** | **tooAzure**
--- | --- | ---
**Hyper-V** | 不在範圍中 | 是
**VMware** | 不在範圍中 | 是
**實體伺服器** | 不在範圍中 | 是

### <a name="versions"></a>版本
客戶可以部署 XenApp 元件成為 Hyper-V 或 VMware 上執行的虛擬機器，或成為實體伺服器。 Azure Site Recovery 保護這兩個實體和虛擬部署 tooAzure。
因為 XenApp 7.7 或更新版本支援在 Azure 中，只使用這些版本部署可以容錯移轉 tooAzure 嚴重損壞修復或移轉。

### <a name="things-tookeep-in-mind"></a>請注意的事項 tookeep

1. 保護與復原支援內部部署使用 Server OS 機器 toodeliver XenApp 已發佈應用程式和 XenApp 發佈的桌面。

2. 不支援保護和復原的內部部署用戶端虛擬桌面，包括 Windows 10 中，使用桌面 OS 機器 toodeliver 桌面 VDI。 這是因為 ASR 並不支援的電腦桌面 OS'es hello 復原。  此外，某些用戶端虛擬桌面 (例如 Windows 7) 在 Azure 中尚不支援授權。 [深入了解](https://azure.microsoft.com/pricing/licensing-faq/)如何在 Azure 中進行用戶端/伺服器桌面的授權。

3.  Azure Site Recovery 無法複寫和保護現有的內部部署 MCS 或 PV 複製品。
您需要 toorecreate 使用從傳遞控制站的 Azure RM 佈建這些複製品。

4. 無法使用 Azure Site Recovery 保護 NetScaler，因為 NetScaler 是以 FreeBSD 為基礎，而且 Azure Site Recovery 不支援 FreeBSD 作業系統的保護。 您會需要 toodeploy，並在容錯移轉 tooAzure 之後設定新 NetScaler 裝置從 Azure 市場的位置。


## <a name="replicating-virtual-machines"></a>複寫虛擬機器

下列元件的 hello Citrix XenApp 部署的 hello 需要受保護的 toobe tooenable 複寫和復原。

* AD DNS 伺服器的保護
* SQL 資料庫伺服器的保護
* Citrix 傳遞控制站的保護
* StoreFront 伺服器的保護。
* XenApp Master (VDA) 的保護
* Citrix XenApp 授權伺服器的保護


**AD DNS 伺服器複寫**

請參閱太[保護 Active Directory 和 DNS 與 Azure Site Recovery](site-recovery-active-directory.md)上複寫，以及在 Azure 中設定的網域控制站的指引。

**SQL Database 伺服器複寫**

請參閱太[以 SQL Server 嚴重損壞修復及 Azure Site Recovery 保護 SQL Server](site-recovery-sql.md)如需詳細指引技術 hello 建議的選項，來保護 SQL server。

請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫 hello 其他元件的虛擬機器 tooAzure。

![XenApp 元件的保護](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**計算和網路設定**

Hello 機器受到保護之後 （狀態顯示為 「 受保護 」 複寫的項目 下，） hello 運算和網路設定需要 toobe 設定。
在計算與網路 > 計算屬性，您可以指定 hello Azure VM 的名稱和目標大小。
如果您需要，修改 hello 名稱 toocomply Azure 需求。 您也可以檢視和新增 hello 目標網路、 子網路及指派 toohello Azure VM 的 IP 位址資訊。

請注意 hello 下列：

* 您可以設定 hello 目標 IP 位址。 如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。 如果您將無法使用在容錯移轉的位址，將無法運作 hello 容錯移轉。 相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。

* Hello AD/DNS 伺服器，保留 hello 內部位址可讓您指定的 hello 相同位址做為 hello hello Azure 虛擬網路的 DNS 伺服器。

hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：

*   如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。
*   如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。
* 例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。 如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。
*   如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。
*   如果 hello 虛擬機器有多張網路介面卡，然後 hello hello 清單所示的第一個會變成 hello Azure 虛擬機器中的 hello 預設網路介面卡。


## <a name="creating-a-recovery-plan"></a>建立復原計劃

啟用 hello XenApp 元件 Vm 複寫之後，hello 下一個步驟是 toocreate 復原計劃。
復原計畫群組會將有類似需求的虛擬機器分組，以便進行容錯移轉和復原。  

**步驟 toocreate 復原計劃**

1. Hello XenApp 元件中加入虛擬機器復原計劃的 hello。
2. 按一下 [復原計畫] -> [+ 復原計畫]。 提供直覺式 hello 復原計劃的名稱。
3. 對於 VMware 虛擬機器：選取 VMware 處理序伺服器做為來源，選取 Microsoft Azure 做為目標，並選取資源管理員做為部署模型，然後按一下 [選取項目]。
4. HYPER-V 虛擬機器： 選取來源 VMM 伺服器，以目標為 Microsoft Azure，以及部署模型與資源管理員和按一下選取的項目，然後選取 hello XenApp 部署 Vm。

### <a name="adding-virtual-machines-toofailover-groups"></a>新增虛擬機器 toofailover 群組

復原計劃可以是特定的啟動順序、 指令碼或手動動作的自訂的 tooadd 容錯移轉群組。 下列群組的 hello 需要 toobe 加入的 toohello 復原計劃。

1. 容錯移轉群組 1：AD DNS
2. 容錯移轉群組 2：SQL Server VM
2. 容錯移轉群組 3：VDA Master Image VM
3. 容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM


### <a name="adding-scripts-toohello-recovery-plan"></a>加入指令碼 toohello 復原計劃

可以在復原計畫中的特定群組之前或之後執行指令碼。 也可以在容錯移轉期間加入並執行手動動作。

hello 自訂的復原計劃看起來類似下面的 hello:

1. 容錯移轉群組 1：AD DNS
2. 容錯移轉群組 2：SQL Server VM
3. 容錯移轉群組 3：VDA Master Image VM

   >[!NOTE]     
   >步驟 4、 6 和 7 包含手動 」 或 「 指令碼動作都適用 tooonly 內部 XenApp > MCS/PV 目錄的環境。

4. 手動或指令碼動作的群組 3： 關閉主要 VDA VM hello Master VDA VM 容錯移轉 tooAzure 時將會處於執行中狀態。 toocreate 新 MCS 的目錄，使用 Azure ARM 裝載，hello 主機 VDA VM 是處於 已停止 (de 配置) 的必要的 toobe 狀態。 關機 hello VM 從 Azure 入口網站。

5. 容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM
6. 群組 3 手動或指令碼動作 1：

    ***新增 Azure RM 主機連線***

    在傳遞控制站機器 tooprovision 中新 MCS 類別目錄，在 Azure 中的建立 Azure ARM 主機連接。 在此說明，請遵循 hello 步驟[文章](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)。

7. 群組 3 手動或指令碼動作 2：

    ***在 Azure 中重新建立 MCS 目錄***

    hello 現有 MCS 或 PV 複製品 hello 主要站台上的將不會複寫的 tooAzure。 您必須使用 hello 這些複製品會在從傳遞控制站複寫 「 主要 VDA 和佈建的 Azure ARM toorecreate。在此說明，請遵循 hello 步驟[文章](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/)toocreate MCS 目錄在 Azure 中。

![XenApp 元件的復原計畫](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >您可以使用指令碼，於[位置](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts)tooupdate hello DNS 以容錯移轉的 hello 的新 Ip hello > 視虛擬機器或 tooattach hello 上的負載平衡器無法容錯移轉虛擬機器。


## <a name="doing-a-test-failover"></a>執行測試容錯移轉

請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。

![復原方案](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>執行容錯移轉

當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。

## <a name="next-steps"></a>後續步驟

您可以在這份白皮書中[深入了解](https://aka.ms/citrix-xenapp-xendesktop-with-asr)複寫 Citrix XenApp 和 XenDesktop 部署。 查看 hello 指引太[複寫其他應用程式](site-recovery-workload.md)使用站台復原。
