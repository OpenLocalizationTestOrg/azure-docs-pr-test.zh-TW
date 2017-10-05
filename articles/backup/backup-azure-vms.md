---
title: "將傳統型部署的 Azure 虛擬機器備份到備份保存庫| Microsoft Docs"
description: "利用 Azure 虛擬機器備份的這些程序來探索、註冊及備份您的虛擬機器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "虛擬機器備份; 備份虛擬機器; 備份和災害復原; vm 備份"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>備份 Azure 虛擬機器 (傳統入口網站)
> [!div class="op_single_selector"]
> * [將 VM 備份到復原服務保存庫](backup-azure-arm-vms.md)
> * [將 VM 備份到備份保存庫](backup-azure-vms.md)
>
>

本文提供將傳統部署的 Azure 虛擬機器 (VM) 備份到備份保存庫的程序。 您必須先處理幾件工作，才能備份 Azure 虛擬機器。 如果您尚未這樣做，請完成 [必要條件](backup-azure-vms-prepare.md) ，讓您的環境準備好進行備份 VM 的工作。

如需詳細資訊，請參閱[在 Azure 中規劃 VM 備份基礎結構](backup-azure-vms-introduction.md)和 [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)的文件。

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 備份保存庫只能保護傳統部署的 VM。 您無法使用備份保存庫保護 Resource Manager 部署的 VM。 如需使用復原服務保存庫的詳細資訊，請參閱 [將 VM 備份到復原服務保存庫](backup-azure-arm-vms.md) 。
>
>

備份 Azure 虛擬機器需要三個主要步驟：

![備份 Azure IaaS VM 的三個步驟](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> 備份虛擬機器是本機的程序。 您無法將某一個區域中的虛擬機器備份到另一個區域中的備份保存庫。 因此，您必須在每個 Azure 區域中建立備份保存庫，其中含有將備份的 VM。
>
> [!IMPORTANT]
> 從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。
> 您現在可以將備份保存庫升級至復原服務保存庫。 如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。 Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。<br/> 在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有其餘的備份保存庫都會自動升級至復原服務保存庫。
>- 您將無法在傳統入口網站中存取您的備份資料。 相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。
>

## <a name="step-1---discover-azure-virtual-machines"></a>步驟 1 - 探索 Azure 虛擬機器
若要在註冊前確保能夠識別任何已加入至訂用帳戶的新虛擬機器 (VM)，請執行探索程序。 此程序會在 Azure 中查詢訂用帳戶中的虛擬機器清單，以及其他資訊，例如雲端服務名稱、區域等。

1. 登入 [傳統入口網站](http://manage.windowsazure.com/)
2. 在 Azure 傳統服務清單中，按一下 [復原服務]  以開啟備份和 Site Recovery 保存庫清單。
    ![開啟保存庫清單](./media/backup-azure-vms/choose-vault-list.png)
3. 在備份保存庫清單中，選取要備份 VM 的保存庫。

    如果這是新的保存庫，則入口網站會開啟至 [快速啟動]  頁面。

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-quick-start.png)

    如果先前已設定此保存庫，則入口網站會開啟至最近使用的功能表。
4. 在保存庫功能表 (位於頁面頂端) 中，按一下 [已註冊的項目] 。

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-menu.png)
5. 在 [類型] 功能表中選取 [Azure 虛擬機器]。

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. 按一下頁面底部的 [ **探索** ]。
    ![探索按鈕](./media/backup-azure-vms/discover-button-only.png)

    在列表顯示虛擬機器時，探索程序可能需花費幾分鐘的時間。 畫面底部會有通知讓您知道程序正在執行中。

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    程序完成時，通知隨即變更。 如果探索程序找不到虛擬機器，請先確定 VM 存在。 如果 VM 存在，請確定 VM 位於與備份保存庫相同的區域。 如果 VM 存在且位於相同區域中，請確定 VM 尚未註冊到備份保存庫。 如果 VM 已指派給備份保存庫，便無法指派給其他備份保存庫。

    ![探索完成](./media/backup-azure-vms/discovery-complete.png)

    一旦找到新的項目，請移至步驟 2 並註冊您的 VM。

## <a name="step-2---register-azure-virtual-machines"></a>步驟 2 - 註冊 Azure 虛擬機器
您必須註冊 Azure 虛擬機器，使其與 Azure 備份服務相關聯。 這通常是一次性活動。

1. 在 Azure 入口網站中，瀏覽至 [復原服務] 下的備份保存庫，然後按一下 [註冊的項目]。
2. 從下拉式選單中選取 [Azure 虛擬機器]  。

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
3. 按一下頁面底部的 [註冊]  。
    ![註冊按鈕](./media/backup-azure-vms/register-button-only.png)
4. 在 [註冊項目]  捷徑功能表中，選取您想要註冊的虛擬機器。 如果有兩個以上同名的虛擬機器，請使用雲端服務加以區別。

   > [!TIP]
   > 您可以同時註冊多個虛擬機器。
   >
   >

    系統會為您所選取的每個虛擬機器建立一個工作。
5. 按一下通知中的 [檢視作業]，以移至 [作業] 頁面。

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    虛擬機器也會連同註冊作業的狀態，出現在已註冊的項目清單中。

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    作業完成時，狀態會改變以反映「已註冊」  狀態。

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>步驟 3 - 保護 Azure 虛擬機器
現在，您可以設定虛擬機器的備份和保留原則。 使用單一保護動作可以保護多個虛擬機器。

2015 年 5 月之後建立的 Azure 備份保存庫，會隨附內建於保存庫的預設原則。 這項預設原則會隨附 30 天預設保留和每日一次的備份排程。

1. 在 Azure 入口網站中，瀏覽至 [復原服務] 下的備份保存庫，然後按一下 [註冊的項目]。
2. 從下拉式選單中選取 [Azure 虛擬機器]  。

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. 按一下頁面底部的 [保護]  。

    [保護項目]  精靈隨即出現。 此精靈只會列出已註冊且不受保護的虛擬機器。 選取您要保護的虛擬機器。

    如果有兩個以上同名的虛擬機器，請使用雲端服務來區別虛擬機器。

   > [!TIP]
   > 您可以同時保護多個虛擬機器。
   >
   >

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)

4. 選擇 [備份排程]  ，以備份您所選取的虛擬機器。 您可以從現有的一組原則中挑選，或定義新的原則。

    每一個備份原則可以有多個相關聯的虛擬機器。 但無論何時，虛擬機器只能與一個原則相關聯。

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > 備份原則中包含排定備份的保留配置。 如果您選取現有的備份原則，就無法在下一個步驟中修改保留選項。
   >
   >

5. 選擇要與備份相關聯的 [保留範圍]  。

    ![使用彈性保留來保護](./media/backup-azure-vms/policy-retention.png)

    保留期原則會指定儲存備份的時間長度。 您可以根據進行備份的時間指定不同的保留原則。 例如，每日取得的備份點 (可充當作業復原點) 可能會保留 90 天。 相較之下，在每一季結尾所取得的備份點 (供稽核之用) 可能需要保留數個月或數年。

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    在此範例影像中：

   * **每日的保留原則**：每日所進行的備份會儲存 30 天。
   * **每週的保留原則**：每個星期日所進行的備份會保留 104 週。
   * **每月的保留原則**：每月最後一個星期日所進行的備份會保留 120 個月。
   * **每年的保留原則**：每年一月第一個星期日所進行的備份會保留 99 年。

     建立的工作可設定保護原則，並將虛擬機器與您所選取的每個虛擬機器的該項原則相關聯。
6. 若要檢視 [設定保護] 作業的清單，可按一下保存庫功能表中的 [作業]，然後從 [作業] 篩選器選取 [設定保護]。

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>初始備份
虛擬機器受到原則保護之後，就會出現在 [受保護的項目] 索引標籤下，狀態為 [受保護 - (擱置中的初始備份)]。 根據預設，第一個排定的備份是 *初始備份*。

若要在設定保護之後立即觸發初始備份：

1. 在 [受保護的項目] 頁面底部，按一下 [立即備份]。

    Azure 備份服務會初始備份作業建立備份工作。
2. 按一下 [工作]  索引標籤來檢視工作清單。

    ![備份進行中](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> 在備份作業期間，Azure 備份服務會發出命令給每個虛擬機器中的備份擴充功能，以排清所有寫入工作並取得一致的快照。
>
>

初始備份完成後，[受保護的項目] 索引標籤中的虛擬機器狀態會顯示為 [受保護]。

![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>檢視備份狀態和詳細資料
虛擬機器受到保護後，[ **儀表板** ] 頁面摘要中的虛擬機器計數也會遞增。 [儀表板] 頁面也會顯示過去 24 小時內「成功」、「失敗」及「進行中」的作業數目。 在 [作業] 頁面上，使用 [狀態]、[作業]，或 [從] 和 [至] 功能表來篩選作業。

![儀表板頁面中的備份狀態](./media/backup-azure-vms/dashboard-protectedvms.png)

儀表板中的值會每隔 24 小時重新整理一次。

## <a name="troubleshooting-errors"></a>錯誤疑難排解
如果您在備份虛擬機器時遇到問題，請參閱 [VM 疑難排解文章](backup-azure-vms-troubleshoot.md) 以取得說明。

## <a name="next-steps"></a>後續步驟
* [管理和監視虛擬機器](backup-azure-manage-vms.md)
* [還原虛擬機器](backup-azure-restore-vms.md)
