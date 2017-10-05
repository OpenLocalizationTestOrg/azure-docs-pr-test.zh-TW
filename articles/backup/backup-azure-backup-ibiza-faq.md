---
title: "復原服務保存庫常見問題集 | Microsoft Docs"
description: "此版本的常見問題集支援公開預覽版本的 Azure 備份服務。 關於備份代理程式、備份和保留、復原、安全性，以及 Azure 備份解決方案其他常見問題的常見問題集答案。"
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
ms.openlocfilehash: e5ef305d926a57e32cdebd44f3dbe2185c735dd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="recovery-services-vault---faq"></a>復原服務保存庫 - 常見問題集
本文提供復原服務保存庫特有資訊，並補充說明 [Azure 備份常見問題集](backup-azure-backup-faq.md)。 Azure 備份常見問題集提供一組關於 Azure 備份服務的完整問答。  

您可以在本文件或相關文件的 Disqus 一節中詢問有關 Azure 備份的問題。 您也可以在 [論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)中張貼有關 Azure 備份服務的問題。

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>復原服務保存庫是以 Resource Manager 為基礎。 備份保存庫 (傳統模式) 是否仍受支援？ <br/>
是，仍然支援備份保存庫。 在 [傳統入口網站](https://manage.windowsazure.com)中建立備份保存庫。 在 [Azure 入口網站](https://portal.azure.com)中建立復原服務保存庫。 不過，強烈建議您建立復原服務保存庫，因為所有未來的增強功能僅可用於復原服務保存庫中。

## <a name="can-i-migrate-a-backup-vault-to-a-recovery-services-vault-br"></a>是否可以將備份保存庫移轉至復原服務保存庫？ <br/>
很遺憾，不行，目前無法將備份保存庫的內容移轉至復原服務保存庫。 我們正著手新增這項功能，但公開預覽中並未提供。

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？ <br/>
復原服務保存庫支援兩種模式。  您可以將傳統入口網站中建立的 VM (傳統模式 VM) 或 Azure 入口網站中建立的 VM (以 Resource Manager 為基礎) 備份至復原服務保存庫。

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-to-migrate-my-vms-from-classic-mode-to-resource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>我已在備份保存庫中備份傳統 VM。 我現在想要將 VM 從傳統模式移轉至 Resource Manager 模式。  如何才能在復原服務保存庫中備份它們？
當您將 VM 從傳統移轉至 Resource Manager 模式，備份保存庫中傳統 VM 的備份將不會自動移轉至復原服務保存庫。 請遵循下列步驟進行 VM 備份的移轉︰

1. 在備份保存庫中，請移至 [受保護的項目]  索引標籤並選取 VM。 按一下 [停止保護](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。 讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。
2. 在 [Azure 入口網站](https://portal.azure.com)中，移至 VM 的[擴充] 功能表並將 **VMSnapshot/VMSnapshotLinux** 擴充功能解除安裝。
3. 將虛擬機器從傳統模式移轉至 Resource Manager 模式。 確定虛擬機器對應的儲存體和網路也會移轉至 Resource Manager 模式。
4. 建立復原服務保存庫，並利用保存庫儀表板上的 [備份]  動作，在移轉的虛擬機器上設定備份。 深入了解如何 [在復原服務保存庫中啟用備份](backup-azure-vms-first-look-arm.md)
