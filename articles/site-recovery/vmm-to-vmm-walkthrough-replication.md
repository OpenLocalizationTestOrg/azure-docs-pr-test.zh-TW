---
title: "HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "描述如何建立 HYPER-V 虛擬機器複寫 tooa 的原則 tooset 次要 VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>步驟 8：設定複寫原則

設定之後[網路對應](vmm-to-vmm-walkthrough-network-mapping.md)，HYPER-V 虛擬機器 (VM) 複寫 tooa 次要站台上，使用此複寫原則的發行項 tooset 使用[Azure Site Recovery](site-recovery-overview.md)。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

- 當您建立的複寫原則時，使用 hello 原則的所有主機必須有都 hello 相同的作業系統。 hello VMM 雲端可以包含執行不同版本的 Windows Server HYPER-V 主機，但在此情況下，您需要多個複寫原則。
- 您可以執行 hello 的離線初始複寫。

## <a name="configure-replication-settings"></a>設定複寫設定

1. toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。 hello 來源和目標型別應該是**HYPER-V**。
3. 在**HYPER-V 主機版本**，選取 hello 主機上執行的作業系統。
4. 在**驗證類型**和**驗證連接埠**，指定如何驗證主要 hello 和復原 HYPER-V 主機伺服器之間的流量。 除非您有有效的 Kerberos 環境，否則請選取 [憑證]。 Azure Site Recovery 會自動設定用於 HTTPS 驗證的憑證。 您不需要 toodo 任何項目以手動方式。 根據預設，將 hello HYPER-V 主機伺服器上的 hello Windows 防火牆中開啟連接埠 8083 和 8084 （用於憑證）。 如果您選取**Kerberos**，將會進行相互驗證的 hello 主機伺服器使用 Kerberos 票證。 請注意，這項設定只有在 Hyper-V 主機伺服器是執行於 Windows Server 2012 R2 時才有重要性。
5. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。
6. 在**復原點保留**，以小時為單位指定多久 hello 保留時間將會針對每個復原點。 受保護的電腦可以是復原 tooany 視窗內的點。
7. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。 HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 如果您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。
8. 在 [資料傳輸壓縮] 中，指定是否應該將傳輸的已複寫資料壓縮。
9. 選取**刪除複本 VM**，應該刪除 hello 複本虛擬機器的 toospecify，如果您停用 hello 來源 VM 的保護。 如果您啟用此設定，當您停用保護 hello 來源會從 hello Site Recovery 主控台中移除的 VM，hello VMM 站台復原設定移除了 hello VMM 主控台中，並刪除 hello 複本。
10. 在**初始複寫方法**，如果您要複寫 hello 網路上指定是否 toostart hello 初始複寫，或者排程它。 toosave 網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。 然後按一下 [確定] 。

     ![複寫原則](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. 當您建立新的原則會自動對 hello VMM 雲端與其相關。 在 [複寫原則] 中，按一下 [確定]。 您可以將其他 VMM 雲端 （和它們的 hello Vm），與在此複寫原則**複寫**> 原則名稱 >**關聯 VMM 雲端**。

     ![複寫原則](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>準備進行離線初始複寫

您可以進行離線複寫 hello 初始資料複本。 您可以如下所示方式進行準備︰

* Hello 來源伺服器上，您可以指定從哪個 hello 資料匯出，就會進行的路徑位置。 指派 「 完整控制 NTFS 和共用權限 toohello hello 匯出路徑上的 VMM 服務。 在 hello 目標伺服器上，指定從中 hello 資料匯入的路徑位置就會發生。 指派 hello 這個匯入路徑上的相同權限。
* 如果 hello 匯入或匯出路徑共用，指派 hello 遠端電腦上的 hello VMM 服務帳戶的系統管理員、 Power User、 列印操作員或伺服器操作員群組成員資格位於上共用的 hello。
* 如果您使用的任何執行身分帳戶 tooadd 主機，hello 上匯入和匯出路徑、 指派讀取和寫入權限 toohello 執行身分帳戶在 VMM 中。
* hello 匯入和匯出共用應該位於任何做為 HYPER-V 主機伺服器的電腦因為 HYPER-V 不支援回送設定。
* 在每個包含您想 tooprotect，虛擬機器的 HYPER-V 主機伺服器上的 Active Directory 中啟用及設定限制的委派 tootrust hello 遠端電腦上的 hello 匯入和匯出路徑，如下：
  1. 在 hello 網域控制站上開啟**Active Directory 使用者和電腦**。
  2. 在 hello 主控台樹狀目錄中，按一下  **DomainName** > **電腦**。
  3. 以滑鼠右鍵按一下 hello HYPER-V 主機伺服器名稱 >**屬性**。
  4. 在 hello**委派**索引標籤上，按一下 **信任這台電腦所委派 toospecified 服務只**。
  5. 按一下 [使用任何驗證通訊協定] 。
  6. 按一下 [新增]  > 提出技術問題。
  7. 型別 hello 裝載 hello 匯出路徑的 hello 電腦名稱 >**確定**。 從 hello 的可用服務清單，請在按住 hello CTRL 鍵，然後按一下  **cifs** > **確定**。 Hello 電腦名稱的 hello 重複該主機 hello 匯入路徑。 視需要為其他 Hyper-V 主機伺服器重複動作。



## <a name="next-steps"></a>後續步驟

跳過[步驟 9： 啟用複寫](vmm-to-vmm-walkthrough-enable-replication.md)。
