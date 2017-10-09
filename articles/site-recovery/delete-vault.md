---
title: "aaaDelete Site Recovery 保存庫"
description: "了解如何 toodelete Azure Site Recovery 保存庫中，根據 hello 站台復原案例。"
service: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a>刪除 Site Recovery 保存庫
相依性會阻擋您刪除 Azure Site Recovery 保存庫。 hello 需要 tootake 動作而異 hello 站台復原案例： VMware tooAzure HYPER-V （含與不含 「 System Center Virtual Machine Manager） tooAzure 和 Azure 備份。 請參閱 toodelete 用於 Azure 備份保存庫[刪除備份保存庫在 Azure 中的](../backup/backup-azure-delete-vault.md)。

>[!Important]
>如果您正在測試 hello 產品，不必擔心資料遺失時，使用 hello 強制刪除方法 toorapidly 移除 hello 保存庫和其所有相依性。

> hello PowerShell 命令會刪除所有 hello 內容 hello 保存庫和之後即無法復原。

## <a name="use-powershell-tooforce-delete-hello-vault"></a>使用 PowerShell tooforce 刪除 hello 保存庫 

站台復原保存庫，即使有 toodelete hello 受保護的項目，請使用下列命令：

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>刪除 Site Recovery 保存庫 
toodelete hello 保存庫，後續 hello 建議用於您案例的步驟。

### <a name="vmware-vms-tooazure"></a>VMware Vm tooAzure

1. 中的 hello 步驟來刪除所有受保護的 Vm[停用保護，適用於 VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。

2. 刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。

3. 刪除的參考中的步驟的下列 hello toovCenter[刪除 vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery)。

4. 刪除 hello 組態伺服器中的 hello 步驟[解除委任的組態伺服器](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server)。

5. 刪除 hello 保存庫。


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>HYPER-V Vm (與 Virtual Machine Manager) tooAzure
1. 中的 hello 步驟來刪除所有受保護的 Vm[停用保護 VMware VM 或實體伺服器](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。

2. 刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。

3.  刪除參考 tooVirtual Machine Manager 伺服器中的 hello 步驟[已連線的 VMM 伺服器取消登錄](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server)。

4.  刪除 hello 保存庫。

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>(不含 Virtual Machine Manager) 的 HYPER-V Vm tooAzure
1. 中的 hello 步驟來刪除所有受保護的 Vm[停用保護 VMware VM 或實體伺服器](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server)。

2. 刪除所有的複寫原則中的 hello 步驟[刪除複寫原則](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy)。

3. 刪除參考 tooHyper APP-V 伺服器中的 hello 步驟[取消註冊 HYPER-V 主機](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site)。

4. 刪除 hello HYPER-V 站台。

5. 刪除 hello 保存庫。
