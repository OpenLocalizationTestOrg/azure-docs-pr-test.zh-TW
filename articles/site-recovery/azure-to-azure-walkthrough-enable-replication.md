---
title: "Azure Vm tooanother 與 Azure Site Recovery 的 Azure 區域的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要 tooenable 複寫 tooanother Azure 地區的 Azure Vm，使用 hello Azure Site Recovery 服務的 hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>步驟 5：啟用 Azure VM 的複寫


設定好後[復原服務保存庫](azure-to-azure-walkthrough-vault.md)，搭配使用的虛擬機器 (Vm)，tooanother Azure 區域，此文章 tooenable 複寫[Azure Site Recovery](site-recovery-overview.md)。 tooenable 複寫，您設定來源和目標設定，確認 hello 複寫原則，，並選取您想要 tooreplicate 的 Vm。

- 當您完成 hello 發行項，您的 Azure Vm 應該複寫 toohello 次要 Azure 地區。
- 張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM 複寫目前為預覽狀態。


## <a name="select-hello-source"></a>選取 hello 來源 

1. 在 復原服務保存庫中，按一下 hello 保存庫名稱 > **+ 複寫**。
2. 在 [來源] 中，選取 [Azure-PREVIEW]。
2. 在**來源位置**，選取 hello 來源 Vm 目前的執行所在的 Azure 區域。
3. 選取 hello **Azure 虛擬機器部署模型**vm:**資源管理員**或**傳統**。
4. 選取 hello**來源資源群組**對於資源管理員的 Vm，或**雲端服務**用於傳統的 Vm。
5. 按一下**確定**toosave hello 設定。

    ![設定 hello 來源](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>選取 hello Vm

Site Recovery 擷取的 hello 與 hello 訂用帳戶和資源群組/雲端服務相關聯的 Vm 清單。

1. 在**虛擬機器**，選取您想要 tooreplicate hello Vm。
2. 按一下 [確定] 。

    ![選取 VM](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>配置設定

Site Recovery 會佈建 hello 目標區域 （根據 hello 來源地區設定），預設設定和 hello 複寫原則：

   - **目標位置**: hello 想 toouse 災害復原的目標區域。 我們建議 hello 目標位置符合 hello hello Site Recovery 保存庫的位置。
   - **目標資源群組**： 容錯移轉之後將屬於的資源群組 toowhich hello 目標區域中的 Azure Vm。 根據預設，站台復原會建立新的資源群組具有"asr"後置詞 hello 目標區域中。 
   - **目標虛擬網路**: hello hello 中哪一個 Azure Vm 中目標區域即將放置在容錯移轉後的網路。 根據預設，站台復原會在"asr"尾碼的 hello 目標區域中建立新的虛擬網路 （和子網路）。 此網路是對應的 tooyour 來源網路。 請注意，您可以指派特定的 IP 位址在虛擬機器的容錯移轉之後，如果您需要 tooretain hello 相同的 IP 位址 hello 來源和目標位置。 
   - **快取儲存體帳戶**： 站台復原 hello 來源範圍中使用的儲存體帳戶。 來源 Vm 上的變更會傳送 toothis 帳戶之前複寫 toohello 目標位置。 
   - **目標儲存體帳戶**： 根據預設，站台復原會建立新的儲存體帳戶在 hello 目標區域中，toomirror hello 來源 VM 儲存體帳戶。
   -  **目標可用性設定組**： 根據預設，站台復原會建立新的可用性設定組與 hello"asr"後置字元的 hello 目標區域中。 
   - **複寫原則名稱**：原則名稱。
   - **復原點保留**：根據預設，Site Recovery 會保留復原點 24 小時。 您可以設定介於 1 與 72 小時之間的值。
   - **應用程式一致性快照的頻率**：根據預設，Site Recovery 會每隔 4 小時製作一份應用程式一致性快照集。 您可以設定介於 1 與 12 小時之間的任何值。 資料會持續複寫：
    - 損毀一致性復原點會在建立時維持一致的資料寫入順序。 這種類型的復原點通常已足夠如果您的應用程式是從損毀不含資料不一致的設計的 toorecover
    - 系統會每隔數分鐘產生損毀一致性復原點。 透過使用這些復原點 toofail 和復原您的 Vm 提供 hello 幾分鐘的復原點目標 (RPO)。
    - 執行應用程式完成所有操作，而排清緩衝區 toodisk （應用程式停止），請確定 （在加法 toowrite 順序一致性） 的應用程式一致的復原點。 建議您對資料庫應用程式 (例如 SQL Server、Oracle 和 Exchange) 使用這些復原點。
        
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>修改設定

如果您想 toomodify 目標與複寫原則設定時，請勿 hello 遵循：

1. tooview 或修改目標設定，請按一下**設定**。
2. toooverride hello 預設目標設定，請按一下**自訂**。 您可以指定目標資源群組、虛擬網路、可用性設定組和目標儲存體帳戶。 如果 Vm 是 hello 來源範圍中的一組的一部分，您只可以加入可用性設定組。

    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. 復原點和應用程式一致快照集，toooverride 複寫設定，請按一下**自訂**下一步太**複寫原則**。
 
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. 按一下 佈建 hello 目標資源 toostart，**建立目標資源**。 佈建約需要一分鐘左右。 不要關閉 hello 刀鋒視窗中，佈建，期間或您必須透過 toostart。




## <a name="enable-replication"></a>啟用複寫

1. 在 [設定] 中，按一下 [啟用複寫]。 這可讓您選取的 Vm hello 的初始複寫。 初始複寫狀態可能需要一些時間 toorefresh。 按一下**重新整理**tooget hello 最新狀態。

2. 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.

3. 在**設定** > **複寫的項目**，您可以檢視 hello 狀態的 Vm 和 hello 初始複寫正在進行。 向下一直按 hello VM toodrill，其設定。



## <a name="next-steps"></a>後續步驟

跳過[步驟 6： 執行測試容錯移轉](azure-to-azure-walkthrough-test-failover.md)
