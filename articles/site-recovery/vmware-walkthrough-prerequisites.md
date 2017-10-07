---
title: "使用 Azure Site Recovery 的 VMware tooAzure 複寫 aaaPrerequisites |Microsoft 文件"
description: "摘要說明複寫 VMware Vm tooAzure，使用 hello Azure Site Recovery 服務上執行工作負載的 hello 的必要條件。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>步驟 2： 檢閱 VMware tooAzure 複寫 hello 必要條件

讀取 hello 必要條件 hello 下表中摘要說明。

**必要條件** | **詳細資料**
--- | ---
**Azure** | 了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)
**內部部署組態伺服器** | 您需要有執行 Windows Server 2012 R2 或更新版本的 VMware VM。 您在 Site Recovery 部署期間設定此伺服器。<br/><br/> 預設 hello 處理序伺服器與主要目標伺服器也會安裝此 VM 上。 當您向上延展，您可能需要不同的處理序伺服器，並且具有 hello 與 hello 組態伺服器相同的需求。<br/><br/> 在[這裡](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)深入了解這些元件
**內部部署 VMware 伺服器** | 一個或多個 VMware vSphere 伺服器 (執行具有最新更新的 6.5、6.0、5.5 或 5.1)。 伺服器應該位於相同網路 hello 組態伺服器 （或不同的處理序伺服器） 的 hello。<br/><br/> 我們建議的 vCenter 伺服器 toomanage 主控件以 hello 最新的更新執行 6.5、 6.0 或 5.5。
**內部部署 VM** | 您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。 VM 應該執行 VMware 工具。
**URL** | hello 組態伺服器需要存取 toothese Url:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。<br/></br> 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。<br/></br> 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。<br/><br/> 允許 hello MySQL 下載此 URL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi。
**行動服務** | 安裝在每個複寫的 VM 上。




## <a name="limitations"></a>限制

請確定您了解 hello 限制 hello 表將摘要說明您在部署之前。

**限制** | **詳細資料**
--- | ---
**Azure** | 儲存體和網路的帳戶必須在 hello 與 hello 保存庫相同的區域<br/><br/> 如果您使用進階儲存體帳戶，您也需要標準儲存帳戶 toostore 複寫記錄檔<br/><br/> 您無法複寫在中部和印度南部及印度 toopremium 帳戶。
**內部部署組態伺服器** | VMware VM 配接器類型應該是 VMXNET3。 如果不是，請[安裝此更新](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> 應該安裝 vSphere PowerCLI 6.0。<br/><br> hello 機器不應該是網域控制站。 hello 電腦應該具有靜態 IP 位址。<br/><br/> hello 主機名稱必須是 15 個字元或更少，而且作業系統應該是英文。
**VMware** | Site Recovery 不支援新的 vCenter 和 vSphere 6.5 和 6.0 功能，例如跨 vCenter vMotion、虛擬磁碟區和儲存體 DRS。
**VM** | 確認 [Azure VM 限制](site-recovery-prereq.md#azure-requirements)<br/><br/> 您無法複寫具有加密磁碟的 VM 或具有 UEFI/EFI 開機的 VM。<br/><br> 不支援共用磁碟叢集。 如果 NIC 小組 hello 來源 VM，則會轉換 tooa 容錯移轉之後的單一 NIC。<br/><br/> 如果 Vm 有 iSCSI 磁碟時，站台復原將它轉換 tooa VHD 檔案在容錯移轉之後。 如果 hello iSCSI 目標可到達的 hello Azure VM，將它連接 tooit，並會查看它並 hello VHD。 如果發生這種情況，先中斷 hello iSCSI 目標。<br/><br/> 如果您 tooenable 多重 VM 一致性，可讓 Vm 執行相同工作負載 toobe 復原的 hello 一起 tooa 一致的資料點，請開啟連接埠 20004 hello VM 上。<br/><br/> 必須安裝 Windows hello C 磁碟機上。 hello OS 磁碟應該是基本功能，而非動態。 hello 資料磁碟可以是動態的。<br/><br/> Linux Vm 上的 /etc/hosts 檔案應該包含所有網路介面卡相關都聯的 hello 本機主機名稱 tooIP 位址對應的項目。 hello 主機名稱、 掛接點、 裝置名稱、 系統路徑和檔案名稱 (/ 等等; libodbc) 只應該是英文。<br/><br/> 支援特定類型的 [Linux 儲存體](site-recovery-support-matrix-to-azure.md#support-for-storage)。<br/><br/>建立或設定**disk.enableUUID=true** hello VM 設定中。 這提供一致的 UUID toohello VMDK，，讓它正確掛載，並確保容錯回復，但沒有完整的複寫期間所傳送後 tooon 單位唯一的差異變更。


## <a name="next-steps"></a>後續步驟

- 如果您進行完整部署，請移至太[步驟 3： 規劃容量](vmware-walkthrough-capacity.md)
- 如果您所做的簡單測試部署，請移至太[步驟 4： 規劃網路](vmware-walkthrough-network.md)。
