---
title: "aaaPrepare 機器 tooset 之間移轉 tooAzure 使用站台復原後的 Azure 地區的災害復原 |Microsoft 文件"
description: "本文說明如何 tooprepare 機器 tooset 之間之後移轉 tooAzure 使用 Azure Site Recovery 的 Azure 地區的災害復原。"
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
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>使用 Azure Site Recovery 將 Azure Vm tooanother 區域複寫之後移轉 tooAzure

>[!NOTE]
> Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。

## <a name="overview"></a>概觀

這篇文章可協助您準備這些機器已從內部部署環境 tooAzure 移轉使用 Azure 站台復原後的兩個 Azure 區域間複寫的 Azure 虛擬機器。

## <a name="disaster-recovery-and-compliance"></a>災害復原和合規性
現在，越來越多企業要移動其工作負載 tooAzure。 移動內部任務關鍵性生產環境的企業工作負載 tooAzure，設定這些工作負載的災害復原是必要的符合性與 toosafeguard 對 Azure 的區域中的任何干擾。

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>準備移轉後的機器以進行複寫的步驟
tooprepare 移轉機器的複寫 tooanother Azure 地區設定：

1. 完成移轉。
2. 安裝 Azure 代理程式視 hello。
3. 移除 hello 行動服務。  
4. 重新啟動 hello VM。

在 hello 下列各節中詳細說明這些步驟。

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>步驟 1： 移轉 HYPER-V Vm、 VMware Vm 和 Azure Vm 上的實體伺服器 toorun 上執行的工作負載

tooset 複寫並移轉您在內部部署 HYPER-V 和 VMware 及實體工作負載 tooAzure 後續 hello 中的步驟 hello[移轉 Azure IaaS 虛擬機器與 Azure Site Recovery 的 Azure 區域之間](site-recovery-migrate-to-azure.md)發行項。 

移轉之後，您不需要 toocommit 或刪除容錯移轉。 相反地，選取 hello**完成移轉**選項要為每一部機器 toomigrate:
1. 在**複寫的項目**，以滑鼠右鍵按一下 hello VM，然後按一下**完成移轉**。 按一下**確定**toocomplete hello 步驟。 您可以藉由監視 hello 完成移轉作業中的追蹤 hello VM 屬性中的進度**站台復原工作**。
2. hello**完成移轉**動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止 hello 機器的 Site Recovery 計費。

   ![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>步驟 2: Hello 虛擬機器上安裝 hello Azure VM 代理程式
hello Azure [VM 代理程式](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)必須 hello 虛擬機器上安裝的 hello Site Recovery 延伸 toowork 和 toohelp 保護 hello VM。

>[!IMPORTANT]
>開頭為 Windows 虛擬機器上的版本 9.7.0.0，hello 行動服務安裝程式也會安裝 hello 最新可用 Azure VM 代理程式。 在移轉，hello 虛擬機器符合必要條件使用任何 VM 擴充功能，包括 hello Site Recovery 擴充功能的代理程式安裝。 hello Azure VM 代理程式需求 toobe 手動安裝 hello hello 上安裝行動服務移轉的機器時，才是 9.6 或更早版本。

hello 下表提供有關安裝 hello VM 代理程式和驗證已安裝的其他資訊：

| **作業** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 代理程式安裝 |下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。 |安裝最新的 hello [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md)。 您需要系統管理員權限 toocomplete hello 安裝。 我們建議您發佈的儲存機制從安裝 hello 代理程式。 我們*不建議*直接從 GitHub 安裝 hello Linux VM 代理程式。  |
| 正在驗證 hello VM 代理程式安裝 |1.瀏覽 toohello C:\WindowsAzure\Packages 資料夾 hello Azure VM 中。 您應該會看見 hello WaAppAgent.exe 檔案。 <br>2.以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，，然後選取 [hello**詳細資料**] 索引標籤 hello**產品版本**欄位應該是 2.6.1198.718 或更高版本。 |N/A |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>步驟 3： 移除 hello hello 從行動服務移轉的虛擬機器

如果您已移轉您的內部部署 VMware 機器或實體 Windows/Linux 上的伺服器，您需要從 hello 已移轉的虛擬機器 toomanually 移除/解除安裝 hello 行動服務。

>[!IMPORTANT]
>這個步驟不需要 HYPER-V Vm 移轉 tooAzure。

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>解除安裝 Windows Server VM 上的 hello 行動服務
使用其中一個 Windows Server 電腦上遵循方法 toouninstall hello 行動服務的 hello。

##### <a name="uninstall-by-using-hello-windows-ui"></a>使用 hello Windows UI 解除安裝
1. 在 hello 控制台中，選取 **程式**。
2. 選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。

##### <a name="uninstall-at-a-command-prompt"></a>在命令提示字元中解除安裝
1. 以系統管理員身分開啟 [命令提示字元] 視窗。
2. toouninstall hello 行動服務，請執行下列命令的 hello:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>解除安裝 hello Linux 電腦上的行動服務
1. 在 Linux 伺服器上，以 **root** 使用者登入。
2. 在終端機中，移太/使用者/本機/ASR。
3. toouninstall hello 行動服務，請執行下列命令的 hello:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>步驟 4： 重新啟動 VM hello

您解除安裝 hello 行動服務後，才能重新啟動 hello VM 設定複寫 tooanother Azure 區域。


## <a name="next-steps"></a>後續步驟
- [複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。
- 深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。
