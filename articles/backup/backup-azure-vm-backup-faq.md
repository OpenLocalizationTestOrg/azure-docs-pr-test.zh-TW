---
title: "aaaAzure VM 備份常見問題集 |Microsoft 文件"
description: "關於回答 toocommon 問題： 如何與 Azure VM 備份的運作方式、 限制和功能會變更 toopolicy 發生的時機"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "azure vm 備份, azure vm 還原, 備份原則"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Hello Azure VM 備份服務有關的問題
這篇文章有解答 toocommon 問題 toohelp 快速了解 hello Azure VM 備份的元件。 在某些 hello 解答，會有連結 toohello 文件具有完整的資訊。 您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。

## <a name="configure-backup"></a>設定備份
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？ <br/>
復原服務保存庫支援兩種模式。  您可以備份傳統 VM （hello 傳統入口網站中建立） 或 （在 hello Azure 入口網站中建立） 的資源管理員 VM tooa 復原服務保存庫。

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Azure VM 備份不支援哪些組態？
請瀏覽[支援的作業系統](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup)和 [VM 備份的限制](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>在設定備份精靈中為何看不到我的 VM？
在「設定備份精靈」中，Azure 備份只會列出下列 VM：
* 尚未保護-您可以確認 hello 的 VM 的備份狀態移 tooVM 刀鋒視窗，然後檢查備份狀態設定 功能表中的 hello 刀鋒視窗上。 進一步了解如何太[檢查 VM 的備份狀態](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* 作為 VM 所屬 toosame 區域

## <a name="backup"></a>備份
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>隨選備份作業是否會遵循與排定備份相同的保留排程？
否。 視備份作業需要 toospecify hello 保留範圍。 根據預設，若從入口網站觸發，將會保留 30 天。 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>我在最近一些 VM 上啟用了 Azure 磁碟加密。 我的備份將會繼續 toowork 嗎？
您需要 toogive 權限的 Azure 備份服務 tooaccess 金鑰保存庫。 您可以使用 [PowerShell](backup-azure-vms-automation.md) 文件的「啟用備份」一節中所述的步驟，在 PowerShell 中提供這些權限。

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>我移轉 VM toomanaged 磁碟的磁碟。 我的備份將會繼續 toowork 嗎？
[是]，備份一起順暢運作時並不需要 toore-設定備份。 

## <a name="restore"></a>還原
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>如何在還原磁碟與完整 VM 還原之間做決定？
將 Azure VM 完整還原視為快速建立已還原 VM 的一個選項。 VM 復原選項會變更 hello 名稱的磁碟、 磁碟、 公用 IP 位址、 網路介面來使用容器名稱的唯一性取得 VM 建立時建立的資源。它也不會加入 hello VM tooavailability 集合。 

使用還原磁碟：
* 自訂 hello 階段組態，例如變更 hello 大小從備份設定中的點，便會建立的 VM
* 加入不存在於 hello 備份時的組態 
* 取得建立資源的控制 hello 命名慣例
* 新增 VM tooavailability 組
* 您擁有只使用 PowerShell/宣告式範本定義即可達成的組態

## <a name="manage-vm-backups"></a>管理 VM 備份
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>變更 VM 的備份原則時會發生什麼狀況？
在 VM 上套用新原則時，將遵守排程和保留 hello 新原則。 現有的復原點如果保留擴充，將會標示 tookeep 它們依據新的原則。 保留會降低，如果它們標示為清除在 hello 下次執行清理工作，並將被刪除。 
