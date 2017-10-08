---
title: "aaaRecovery 服務保存庫常見問題集 |Microsoft 文件"
description: "此版的 hello 常見問題集支援 hello 公用預覽版本 hello Azure 備份服務。 Hello 備份代理程式、 備份和保留、 復原、 安全性、 hello Azure 備份解決方案的其他常見問題的相關常見問題的解答 toofrequently。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份解決方案；備份服務"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>復原服務保存庫 - 常見問題集
這篇文章提供資訊特定 tooRecovery 服務保存庫，而且它補充 hello [Azure 備份常見問題集](backup-azure-backup-faq.md)。 hello Azure 備份常見問題集提供 hello 組完整的問與答 hello Azure 備份服務。  

您可以詢問有關 Azure Backup 的問題 hello Disqus > 一節的這篇文章或相關文件中。 您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>復原服務保存庫是以 Resource Manager 為基礎。 備份保存庫 (傳統模式) 是否仍受支援？ <br/>
是，仍然支援備份保存庫。 建立備份保存庫中 hello[傳統入口網站](https://manage.windowsazure.com)。 建立復原服務保存庫中 hello [Azure 入口網站](https://portal.azure.com)。 但是我們強烈建議您 toocreate 復原服務保存庫做為所有未來的增強功能可只在復原服務保存庫中。

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>可以移轉備份保存庫 tooa 復原服務保存庫嗎？ <br/>
不幸的是不可以，此時您無法移轉復原服務保存庫備份保存庫 tooa hello 內容。 我們正著手新增這項功能，但公開預覽中並未提供。

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？ <br/>
復原服務保存庫支援兩種模式。  您可以備份在 hello 傳統入口網站 （此為傳統模式 Vm） 中建立的 VM，或在 hello Azure 入口網站 （此為基礎的資源管理員） 建立 VM tooa 復原服務保存庫。

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>我已在備份保存庫中備份傳統 VM。 現在我想 toomigrate 我 Vm 從傳統模式 tooResource 管理員模式。  如何才能在復原服務保存庫中備份它們？
備份的備份保存庫中的傳統 Vm 將不會移轉自動 toorecovery 服務保存庫傳統 tooResource 管理員模式下從移轉 hello Vm 時。 請遵循下列步驟進行 VM 備份的移轉︰

1. 在備份保存庫，到太**受保護項目**索引標籤並選取 hello VM。 按一下 [停止保護](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。 讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。
2. 在 hello [Azure 入口網站](https://portal.azure.com)，go toohello**延伸**功能表 hello VM 和解除安裝 hello **VMSnapshot/VMSnapshotLinux**延伸模組。
3. 從傳統模式 tooResource 管理員模式移轉 hello 虛擬機器。 請確定儲存體和網路對應 toovirtual 機器是讓同時移轉的 tooResource 管理員模式。
4. 建立復原服務保存庫和設定虛擬機器使用的備份在 hello 移轉**備份**在保存庫儀表板頂端的動作。 進一步了解如何太[啟用復原服務保存庫中的備份](backup-azure-vms-first-look-arm.md)
