---
title: "傳統部署 Azure 虛擬機器 tooa 備份保存庫註冊 aaaBack |Microsoft 文件"
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
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>備份 Azure 虛擬機器 (傳統入口網站)
> [!div class="op_single_selector"]
> * [備份 Vm tooRecovery 服務保存庫](backup-azure-arm-vms.md)
> * [備份 Vm tooBackup 保存庫](backup-azure-vms.md)
>
>

本文章提供 hello 程序來備份傳統部署 Azure 虛擬機器 (VM) tooa 備份保存庫。 有一些工作，您可以將 Azure 虛擬機器之前，需要 tootake 處置。 如果您尚未完成，同時 hello[必要條件](backup-azure-vms-prepare.md)tooprepare 環境以備份您的 Vm。

如需詳細資訊，請參閱 hello 文件上[規劃 VM 備份基礎結構在 Azure 中的](backup-azure-vms-introduction.md)和[Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 備份保存庫只能保護傳統部署的 VM。 您無法使用備份保存庫保護 Resource Manager 部署的 VM。 請參閱[備份 Vm tooRecovery 服務保存庫](backup-azure-arm-vms.md)如需詳細資訊，使用 復原服務保存庫。
>
>

備份 Azure 虛擬機器需要三個主要步驟：

![Azure IaaS vm 的三個步驟 tooback](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> 備份虛擬機器是本機的程序。 您無法備份一個區域 tooa 備份保存庫中另一個區域中的虛擬機器。 因此，您必須在每個 Azure 區域中建立備份保存庫，其中含有將備份的 VM。
>
> [!IMPORTANT]
> 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="step-1---discover-azure-virtual-machines"></a>步驟 1 - 探索 Azure 虛擬機器
tooensure 任何新虛擬機器 (Vm) 加入的 toohello 訂用帳戶後再註冊，識別執行 hello 探索程序。 hello 處理序會查詢 Azure hello hello 訂用帳戶，以及其他資訊中的虛擬機器清單，例如 hello 雲端服務名稱與 hello 區域。

1. 登入 toohello[傳統入口網站](http://manage.windowsazure.com/)
2. 在 hello 清單中的 Azure 服務，按一下 **復原服務**tooopen hello 份備份及 Site Recovery 保存庫。
    ![開啟保存庫清單](./media/backup-azure-vms/choose-vault-list.png)
3. 在備份保存庫的 hello 清單中，選取 hello 保存庫 tooback 將 vm。

    如果這是新的保存庫 hello 入口網站開啟 toohello**快速入門**頁面。

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-quick-start.png)

    如果先前已設定 hello 保存庫，hello 入口網站會開啟 toohello 最近使用的功能表。
4. 從 hello （hello 頁面頂端的 hello） 的保存庫功能表上，按一下 **註冊的項目**。

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-menu.png)
5. 從 hello**類型**功能表上，選取**Azure 虛擬機器**。

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. 按一下**探索**hello hello 頁底端。
    ![探索按鈕](./media/backup-azure-vms/discover-button-only.png)

    hello 探索程序可能需要幾分鐘的時間 hello 虛擬機器會被製成資料表。 沒有在 hello 可讓您知道 hello 處理序正在執行的 hello 畫面下方的通知。

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    hello 程序完成時，就會變更 hello 通知。 如果 hello 探索程序找不到 hello 虛擬機器，先確認 hello Vm 存在。 如果 hello Vm 存在，請確定 hello Vm 會在 hello 相同 hello 備份保存庫與區域。 如果 hello Vm 存在，而且是在 hello 相同的區域，請確定 hello Vm 還不是已註冊的 tooa 備份保存庫。 如果 VM 是指派的 tooa 備份保存庫不是指派的可用 toobe tooother 備份保存庫。

    ![探索完成](./media/backup-azure-vms/discovery-complete.png)

    一旦您已經探索 hello 新項目，請移 tooStep 2，並註冊您的 Vm。

## <a name="step-2---register-azure-virtual-machines"></a>步驟 2 - 註冊 Azure 虛擬機器
註冊 Azure 虛擬機器 tooassociate 它以 hello Azure 備份服務。 這通常是一次性活動。

1. 瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 入口網站，然後按一下**註冊的項目**。
2. 選取**Azure 虛擬機器**從 hello 下拉式選單。

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
3. 按一下**註冊**hello hello 頁底端。
    ![註冊按鈕](./media/backup-azure-vms/register-button-only.png)
4. 在 hello**登錄項目**快顯功能表中，您想 tooregister 選取 hello 虛擬機器。 如果有兩個或多個虛擬機器與 hello 相同名稱，請使用 hello 雲端服務 toodistinguish 兩者之間。

   > [!TIP]
   > 您可以同時註冊多個虛擬機器。
   >
   >

    系統會為您所選取的每個虛擬機器建立一個工作。
5. 按一下**檢視工作**在 hello 通知 toogo toohello**作業**頁面。

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    hello 虛擬機器也會出現在 hello 註冊項目清單，以及 hello 的 hello 註冊作業的狀態。

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    Hello 狀態 hello 作業完成時，變更 tooreflect hello*註冊*狀態。

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>步驟 3 - 保護 Azure 虛擬機器
現在您可以設定 hello 虛擬機器的備份和保留原則。 使用單一保護動作可以保護多個虛擬機器。

隨附於 2015 年之後建立的 azure 備份保存庫 hello 保存庫內建的預設原則。 這項預設原則會隨附 30 天預設保留和每日一次的備份排程。

1. 瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 入口網站，然後按一下**註冊的項目**。
2. 選取**Azure 虛擬機器**從 hello 下拉式選單。

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. 按一下**保護**hello hello 頁底端。

    hello**保護的項目 」 精靈**隨即出現。 hello 精靈只列出註冊和未受保護的虛擬機器。 選取您想 tooprotect hello 虛擬機器。

    如果有兩個或多個虛擬機器與 hello 相同名稱，請使用 hello 雲端服務 toodistinguish hello 的虛擬機器之間。

   > [!TIP]
   > 您可以同時保護多個虛擬機器。
   >
   >

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)

4. 選擇**備份排程**tooback hello 您所選取的虛擬機器。 您可以從現有的一組原則中挑選，或定義新的原則。

    每一個備份原則可以有多個相關聯的虛擬機器。 不過，hello 虛擬機器只能與一個原則，在任何給定時間點相關聯的時間。

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > 備份原則包括 hello 排程備份的保留配置。 如果您選取現有的備份原則，您無法修改 hello 下一個步驟中的 hello 保留選項。
   >
   >

5. 選擇**保留範圍**tooassociate hello 備份。

    ![使用彈性保留來保護](./media/backup-azure-vms/policy-retention.png)

    保留原則指定 hello 長度儲存備份的時間。 您可以指定 hello 備份時，根據不同的保留原則。 例如，每日取得的備份點 (可充當作業復原點) 可能會保留 90 天。 相較之下，在 hello （基於稽核目的） 每季結束時採取的備份點可能需要 toobe 保留多個月或年。

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    在此範例影像中：

   * **每日的保留原則**：每日所進行的備份會儲存 30 天。
   * **每週的保留原則**：每個星期日所進行的備份會保留 104 週。
   * **每月保留原則**: hello 進行每個月的最後一個星期日的備份會保留 120 個月。
   * **每年保留原則**: hello 進行的每個月的第一個星期日的備份保留 99 年。

     作業會建立 tooconfigure hello 保護原則，並將每個您所選取的虛擬機器的 hello 虛擬機器 toothat 原則產生關聯。
6. tooview hello 清單**設定保護**工作，從 hello 保存庫功能表上，按一下**作業**選取**設定保護**從 hello**作業**篩選器。

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>初始備份
一旦原則受到 hello 虛擬機器，就會顯示在 [hello**受保護項目**hello 狀態] 索引標籤*（暫止的初始備份） 的受保護-*。 根據預設，hello 第一個排定的備份是 hello*初始備份*。

tootrigger hello 初始的備份設定保護之後，立即：

1. 在 hello 底部 hello**受保護項目**頁面上，按一下**立即備份**。

    hello Azure 備份服務會建立 hello 初始備份作業的備份工作。
2. 按一下 hello**作業**工作 索引標籤 tooview hello 清單。

    ![備份進行中](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Hello 備份作業期間，hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個虛擬機器 tooflush 所有寫入作業，並採取一致的快照集。
>
>

Hello 初始備份完成時，在 hello hello 虛擬機器 hello 狀態**受保護項目** 索引標籤是*保護*。

![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>檢視備份狀態和詳細資料
受保護，一旦 hello 虛擬機器計數也會增加在 hello**儀表板**摘要頁面。 hello**儀表板**頁面也會顯示 hello 的 hello 過去 24 小時的作業數目*成功*，有*失敗*，而且*正在*. 在 hello**作業**頁面上，使用 hello**狀態**，**作業**，或**從**和**至**功能表 toofilterhello 作業。

![儀表板頁面中的備份狀態](./media/backup-azure-vms/dashboard-protectedvms.png)

Hello 儀表板中的值，就會重新整理一次每隔 24 小時。

## <a name="troubleshooting-errors"></a>錯誤疑難排解
如果您註冊您的虛擬機器執行備份時的問題，請查看 hello [VM 疑難排解文章](backup-azure-vms-troubleshoot.md)的說明。

## <a name="next-steps"></a>後續步驟
* [管理和監視虛擬機器](backup-azure-manage-vms.md)
* [還原虛擬機器](backup-azure-restore-vms.md)
