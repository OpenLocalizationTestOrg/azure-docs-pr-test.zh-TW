---
title: "初步了解：使用備份保存庫備份 Azure VM | Microsoft Docs"
description: "使用 hello 傳統入口網站的 tooback Azure Vm tooa 備份保存庫註冊。 本教學課程說明包括建立 hello 備份保存庫、 註冊 hello Vm、 建立備份原則，以及執行 hello 初始備份作業的所有階段。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>先睹為快：備份 Azure 虛擬機器
> [!div class="op_single_selector"]
> * [使用復原服務保存庫保護 VM](backup-azure-vms-first-look-arm.md)
> * [使用備份保存庫保護 Azure VM](backup-azure-vms-first-look.md)
>
>

本教學課程會帶領您完成備份 Azure 虛擬機器 (VM) tooa 備份保存庫在 Azure 中的 hello 步驟。 本文說明 hello 傳統模型或 Service Manager 部署模型，來備份 Vm。 hello 下列步驟適用於只能在 hello 傳統入口網站中建立的 tooBackup 保存庫。 Microsoft 建議針對新部署使用 hello 資源管理員的模型。

如果您有興趣 VM tooa 復原服務保存庫所屬 tooa 資源群組的備份，請參閱[第一印象： 保護與復原服務保存庫的 Vm](backup-azure-vms-first-look-arm.md)。

toosuccessfully 完成 hello 下列教學課程中，必須具有下列必要條件：

* 您已在 Azure 訂用帳戶中建立 VM。
* hello VM 有連線能力 tooAzure 公用 IP 位址。 如需其他資訊，請參閱[網路連線](backup-azure-vms-prepare.md#network-connectivity)。


> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本教學課程適用於與 hello 傳統入口網站中建立的虛擬機器。
>
>

## <a name="create-a-backup-vault"></a>建立備份保存庫
備份保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。 hello 備份保存庫也包含 hello 套用的 toohello 虛擬機器進行備份的備份原則。

> [!IMPORTANT]
> 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
> 您可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="discover-and-register-azure-virtual-machines"></a>探索及註冊 Azure 虛擬機器
向保存庫中的 hello VM，在執行之前 hello 探索程序 tooidentify 任何新的 Vm。 這會傳回 hello 訂用帳戶，以及其他資訊，例如 hello 雲端服務名稱和 hello 區域中的虛擬機器的清單。

1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)
2. 在 hello Azure 傳統入口網站，按一下 **復原服務**tooopen hello 清單的 復原服務保存庫。
    ![選取工作負載](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. 從保存庫的 hello 清單中選取 hello 保存庫 tooback 將 vm。

    當您選取您的保存庫時，會開啟 hello**快速入門**頁面
4. 從 hello 保存庫功能表上，按一下 **註冊的項目**。

    ![選取工作負載](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. 從 hello**類型**功能表上，選取**Azure 虛擬機器**。

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. 按一下**探索**hello hello 頁底端。
    ![探索按鈕](./media/backup-azure-vms/discover-button-only.png)

    hello 探索程序可能需要幾分鐘的時間 hello 虛擬機器會被製成資料表。 沒有在 hello 可讓您知道 hello 處理序正在執行的 hello 畫面下方的通知。

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    hello 程序完成時，就會變更 hello 通知。

    ![探索完成](./media/backup-azure-vms-first-look/discovery-complete.png)
7. 按一下**註冊**hello hello 頁底端。
    ![註冊按鈕](./media/backup-azure-vms-first-look/register-icon.png)
8. 在 hello**登錄項目**快顯功能表中，您想 tooregister 選取 hello 虛擬機器。

   > [!TIP]
   > 您可以同時註冊多個虛擬機器。
   >
   >

    系統會為您所選取的每個虛擬機器建立一個工作。
9. 按一下**檢視工作**在 hello 通知 toogo toohello**作業**頁面。

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    hello 虛擬機器也會出現在 hello 註冊項目清單，以及 hello 的 hello 註冊作業的狀態。

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    Hello 狀態 hello 作業完成時，變更 tooreflect hello*註冊*狀態。

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 虛擬機器上安裝 VM 代理程式 hello
hello Azure VM 代理程式必須安裝在 Azure 虛擬機器以 hello 備份副檔名 toowork hello。 如果您的 VM 建立從 hello Azure 組件庫，hello VM 代理程式已經存在於 hello VM;您可以再跳過[保護您的 Vm](backup-azure-vms-first-look.md#create-the-backup-policy)。

如果您的 VM 從內部部署資料中心，移轉 hello VM 可能沒有安裝 VM 代理程式的 hello。 您必須安裝 VM 代理程式 hello hello 之前繼續 tooprotect hello VM 的虛擬機器上。 如需安裝的詳細的步驟 hello VM 代理程式，請參閱 < hello [hello 備份 Vm 文章的 「 VM 代理程式 」 一節](backup-azure-vms-prepare.md#vm-agent)。

## <a name="create-hello-backup-policy"></a>建立 hello 備份原則
產生備份快照集時，觸發 hello 初始備份作業之前，設定 hello 排程。 hello 排程備份快照集所使用，以及這些快照集 hello 的時間長度會保留下來，為 hello 備份原則。 hello 保留資訊會取決於祖父-父親-son 備份旋轉配置。

1. 瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 傳統入口網站，然後按一下**註冊的項目**。
2. 選取**Azure 虛擬機器**從 hello 下拉式選單。

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. 按一下**保護**hello hello 頁底端。
    ![按一下 [保護]](./media/backup-azure-vms-first-look/protect-icon.png)

    hello**保護的項目 」 精靈**隨即出現，並列出*只*註冊和未受保護的虛擬機器。

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)
4. 選取您想 tooprotect hello 虛擬機器。

    如果有兩個或多個虛擬機器以 hello 相同名稱、 使用 hello 雲端服務 toodistinguish hello 的虛擬機器之間。
5. 在 hello**設定保護**功能表選取現有的原則，或建立新的原則 tooprotect hello 虛擬機器，您所識別。

    新的備份保存庫具有與 hello 保存庫相關聯的預設原則。 這項原則會每日快照集每個晚上，並會保留 30 天 hello 每日快照集。 每一個備份原則可以有多個相關聯的虛擬機器。 不過，hello 虛擬機器只能與一個原則相關聯一次。

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > 備份原則包括 hello 排程備份的保留配置。 如果您選取現有的備份原則，您會無法 toomodify hello 保留選項 hello 下一個步驟中。
   >
   >
6. 在**保留範圍**定義 hello hello 特定備份點的每日、 每週、 每月和每年的範圍。

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    保留原則指定 hello 長度儲存備份的時間。 您可以指定 hello 備份時，根據不同的保留原則。
7. 按一下**作業**tooview hello 清單**設定保護**作業。

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

    現在，您已建立 hello 原則，請移 toohello 下一個步驟，並執行 hello 初始備份。

## <a name="initial-backup"></a>初始備份
一旦將虛擬機器已受保護原則，您可以檢視該關聯性上 hello**受保護項目** 索引標籤。Hello 初始備份發生之前，hello**保護狀態**顯示為**（暫止的初始備份） 的受保護-**。 根據預設，hello 第一個排定的備份是 hello*初始備份*。

![待備份](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello 初始備份現在：

1. 在 hello**受保護項目**頁面上，按一下**立即備份**hello hello 頁底端。
    ![[立即備份] 圖示](./media/backup-azure-vms-first-look/backup-now-icon.png)

    hello Azure 備份服務會建立 hello 初始備份作業的備份工作。
2. 按一下 hello**作業**工作 索引標籤 tooview hello 清單。

    ![備份進行中](./media/backup-azure-vms-first-look/protect-inprogress.png)

    當初始備份完成時，hello 虛擬機器在 hello hello 狀態**受保護項目** 索引標籤是*保護*。

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > 備份虛擬機器是本機的程序。 您無法備份虛擬機器從一個區域 tooa 備份保存庫中另一個區域。 因此，為具有 Vm 需要 toobe 備份的每個 Azure 區域，必須建立至少一個備份保存庫在該區域中。
   >
   >

## <a name="next-steps"></a>後續步驟
現在您已成功備份 VM，接下來有幾個可能相關的步驟。 hello 最具邏輯步驟是 toofamiliarize 自行還原資料 tooa VM。 不過，有管理工作，協助您了解如何 tookeep 安全資料和降低成本。

* [管理和監視虛擬機器](backup-azure-manage-vms.md)
* [還原虛擬機器](backup-azure-restore-vms.md)
* [疑難排解指引](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。
