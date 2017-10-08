---
title: "復原服務保存庫的 aaaOverview |Microsoft 文件"
description: "復原服務保存庫和 Azure 備份保存庫之間的概觀與比較。"
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>復原服務保存庫概觀

本文說明復原服務保存庫的 hello 的功能。 復原服務保存庫是 Azure 中裝載資料的儲存體實體。 hello 資料通常是資料或虛擬機器 (Vm)、 工作負載、 伺服器或工作站的組態資訊的複本。 復原服務保存庫是備份保存庫 hello 資源管理員版本。 Microsoft 會鼓勵您 toouse 復原服務保存庫和 tooconvert 任何備份保存庫 tooRecovery 服務保存庫。

## <a name="what-is-a-recovery-services-vault"></a>什麼是復原服務保存庫？

復原服務保存庫是在 Azure 中的線上存放區實體使用 toohold 資料，例如備份、 復原點，以及備份原則。 您可以使用 復原服務保存庫 toohold 備份資料的各種 Azure 服務，例如 IaaS Vm （Linux 或 Windows） 和 Azure SQL database。 復原服務保存庫支援 System Center DPM、Windows Server、Azure 備份伺服器等等。 復原服務保存庫讓您輕鬆 tooorganize 備份資料，可能降低管理負擔降到最低。

您可以在訂用帳戶內建立所需數量的復原服務保存庫。

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>比較復原服務保存庫與備份保存庫

復原服務保存庫會 hello Azure Resource Manager 以模型為基礎的 Azure，而以 hello Azure Service Manager 模型為基礎的備份保存庫。 當您升級備份保存庫 tooa 復原服務保存庫時，hello 備份資料期間和之後 hello 升級程序會保持不變。 復原服務保存庫可提供備份保存庫無法使用的功能，例如︰

- **增強功能 toohelp 安全備份資料**： 與復原服務保存庫中，Azure 備份提供的安全性功能 tooprotect 雲端備份。 這些安全性功能可確保您能保護您的備份，並安全地從雲端備份將資料復原，即使生產和備份伺服器遭到入侵也一樣。 [深入了解](backup-azure-security-feature.md)

- **將您的混合式 IT 環境集中監視**︰透過復原服務保存庫，您不只可以監視 [Azure IaaS VM](backup-azure-manage-vms.md)，還可以從中央入口網站監視[內部部署資產](backup-azure-manage-windows-server.md#manage-backup-items)。 [深入了解](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **角色型存取控制 (RBAC)**：RBAC 提供 Azure 中的更細緻存取權管理。 [Azure 提供的各種內建角色](../active-directory/role-based-access-built-in-roles.md)，且 Azure 備份具有三個[內建角色 toomanage 復原點](backup-rbac-rs-vault.md)。 復原服務保存庫相容於 RBAC，限制備份和還原的使用者角色存取 toohello 定義集合。 [深入了解](backup-rbac-rs-vault.md)

- **保護 Azure 虛擬機器的所有設定**︰復原服務保存庫會保護以 Resource Manager 為基礎的 VM，包括進階磁碟、受控磁碟及加密的 VM。 升級備份保存庫 tooa 復原服務保存庫可讓您的 Service Manager Vm tooResource Manager Vm hello 機會 tooupgrade。 升級 hello 保存庫，您可以保留您 Service Manager 架構的 VM 的復原點，並設定保護 hello 升級 （資源管理員已啟用） Vm。 [深入了解](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **IaaS Vm 的立即還原**： 使用 復原服務保存庫、 還原檔案和資料夾從 IaaS VM 而不還原 hello 整個 VM，可讓更快速的還原時間。 IaaS VM 的立即還原適用於 Windows 和 Linux VM。 [深入了解](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>管理您的復原服務保存庫在 hello 入口網站
建立及管理在 hello Azure 入口網站中的 [復原服務保存庫的很簡單，因為 hello 備份服務已整合至 hello Azure 設定] 刀鋒視窗。 此整合意味著您可以建立或管理復原服務保存庫*hello hello 目標服務內容中*。 例如，tooview hello 復原點的 vm，加以選取，然後按一下**備份**hello 設定 刀鋒視窗中。 hello 備份資訊的特定 toothat VM 會出現。 在下列範例，hello **ContosoVM** hello hello 虛擬機器名稱。 **ContosoVM demovault** hello hello 復原服務保存庫名稱。 您不需要 tooremember hello hello 復原服務保存庫名稱，儲存 hello 復原點，您可以從 hello 虛擬機器存取這項資訊。  

![復原服務保存庫詳細資料 VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

如果使用 hello 保護多個伺服器相同的復原服務保存庫，它可能會在 hello 復原服務保存庫的多個邏輯 toolook。 您可以搜尋 hello 訂閱中的所有復原服務保存庫，並選擇 hello 清單其中一個。

hello 以下各節包含說明如何 toouse 復原服務保存庫中每一種活動的連結 tooarticles。

### <a name="back-up-data"></a>備份資料
- [備份 Azure VM](backup-azure-vms-first-look-arm.md)
- [備份 Windows Server 或 Windows 工作站](backup-try-azure-backup-in-10-mins.md)
- [備份 DPM 工作負載 tooAzure](backup-azure-dpm-introduction.md)
- [準備使用 Azure 備份伺服器的工作負載備份 tooback](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>管理復原點
- [管理 Azure VM 備份](backup-azure-manage-vms.md)
- [管理檔案和資料夾](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>從 hello 保存庫還原資料
- [復原 Azure VM 中的個別檔案](backup-azure-restore-files-from-vm.md)
- [還原 Azure VM](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>安全 hello 保存庫
- [保護復原服務保存庫中的雲端備份資料](backup-azure-security-feature.md)



## <a name="next-steps"></a>後續步驟
使用下列文章的 hello:</br>
[備份 IaaS VM](backup-azure-arm-vms-prepare.md)</br>
[備份 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)</br>
[備份 Windows Server](backup-configure-vault.md)
