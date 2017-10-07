---
title: "啟動 Azure Vm aaaBack |Microsoft 文件"
description: "探索、 註冊及備份 Azure 虛擬機器 tooa 復原服務保存庫。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "虛擬機器備份; 備份虛擬機器; 備份和災害復原; arm vm 備份"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>備份 Azure 虛擬機器 tooa 復原服務保存庫
> [!div class="op_single_selector"]
> * [備份 Vm tooRecovery 服務保存庫](backup-azure-arm-vms.md)
> * [備份 Vm tooBackup 保存庫](backup-azure-vms.md)
>
>

這篇文章說明如何 tooback 向上 （資源管理員部署和傳統部署） 的 Azure Vm tooa 復原服務保存庫。 大部分的 hello 工作來備份 Vm 是 hello 準備。 您可以備份或保護的 VM，您必須先完成 hello[必要條件](backup-azure-arm-vms-prepare.md)tooprepare 環境以保護您的 Vm。 當您完成 hello 必要條件時，您可以起始 hello VM 的備份作業 tootake 快照集。


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

如需詳細資訊，請參閱 hello 文件上[規劃 VM 備份基礎結構在 Azure 中的](backup-azure-vms-introduction.md)和[Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。

## <a name="triggering-hello-backup-job"></a>觸發 hello 備份工作
hello 與 hello 復原服務保存庫相關聯的備份原則會定義 hello 備份作業的執行頻率和時間。 根據預設，hello 第一個排定的備份是 hello 初始備份。 Hello 初始備份，就會發生，直到 hello 上次備份的狀態上 hello**備份工作**刀鋒視窗中顯示為**警告 （已暫止的初始備份）**。

![待備份](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

除非您初始的備份是到期 toobegin 過期，建議您執行**立即備份**。 hello hello 保存庫儀表板中的下列程序啟動。 此程序可在完成所有必要條件之後，執行 hello 初始備份工作。 如果尚未執行 hello 初始備份工作，就無法使用此程序。 hello 相關聯的備份原則會決定 hello 的下一個備份工作。  

toorun hello 初始備份作業：

1. Hello 保存庫儀表板上按一下下的 hello 號碼**備份項目**，或按一下 hello**備份項目**磚。 <br/>
  ![設定圖示](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  hello**備份項目**刀鋒視窗隨即開啟。

  ![備份項目](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. 在 hello**備份項目**刀鋒視窗中，選取 hello 項目。

  ![設定圖示](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  hello**備份項目**清單隨即開啟。 <br/>

  ![備份作業已觸發](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. 在 hello**備份項目**清單中，按一下 hello 省略符號**...** tooopen hello 操作功能表。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu.png)

  hello 操作功能表隨即出現。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Hello 操作功能表上，按一下 **備份現在**。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  hello 立即備份 刀鋒視窗隨即開啟。

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。 根據您的 VM hello 大小，建立 hello 初始備份可能需要一些時間。

6. hello 初始備份，hello 保存庫儀表板上，在 hello tooview 或追蹤 hello 狀態**備份工作**磚按一下**正在**。

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  hello 備份作業 刀鋒視窗隨即開啟。

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  在 hello**備份作業**刀鋒視窗中，您可以查看所有工作的 hello 狀態。 請檢查 VM 的 hello 備份工作是否仍在進行中，或若它已完成。 Hello 狀態的備份工作完成時，是*已完成*。

  > [!NOTE]
  > Hello 備份作業的一部分 hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個 VM tooflush 所有寫入，並採取一致的快照集。
  >
  >

## <a name="troubleshooting-errors"></a>錯誤疑難排解
如果您註冊您的虛擬機器執行備份時的問題，請參閱 hello [VM 疑難排解文章](backup-azure-vms-troubleshoot.md)的說明。

## <a name="next-steps"></a>後續步驟
既然您已保護您的 VM，請參閱下列文章 toolearn 有關 VM 管理工作，hello 和如何 toorestore Vm。

* [管理和監視虛擬機器](backup-azure-manage-vms.md)
* [還原虛擬機器](backup-azure-arm-restore-vms.md)
