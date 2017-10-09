---
title: "（使用 VMM) 的 HYPER-V 虛擬機器複寫 tooAzure 與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "描述如何 tooset （使用 VMM) 的 HYPER-V 虛擬機器複寫 tooAzure 與 Azure Site Recovery 的複寫原則"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>步驟 10： 設定 HYPER-V 虛擬機器的複寫 （VMM) tooAzure 的複寫原則


設定好後[網路對應](vmm-to-azure-walkthrough-network-mapping.md)，使用此發行項 tooconfigure 的複寫原則 T\tooreplicate 內部部署 System Center Virtual Machine Manager (VMM) 雲端 tooAzure 中受管理的 HYPER-V 虛擬機器使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。



## <a name="create-a-policy"></a>建立原則

1. toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。
3. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。

    > [!NOTE]
    >  複寫 toopremium 存放裝置時，不支援第二個頻率為 30。 hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。 [深入了解](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. 在**復原點保留**，以小時為單位指定多久 hello 保留時間將會針對每個復原點。 受保護的電腦可以是復原 tooany 視窗內的點。
5. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。 HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。 請注意，是否您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。
6. 在**初始複寫開始時間**，指出當 toostart hello 初始複寫。 hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。
7. 在**加密資料儲存在 Azure 上**，指定是否在 Azure 儲存體中的其餘資料 tooencrypt。 然後按一下 [確定] 。

    ![複寫原則](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. 當您建立新的原則會自動對 hello VMM 雲端與其相關。 按一下 [確定] 。 您可以將其他 VMM 雲端 （和它們的 hello Vm），與在此複寫原則**複寫**> 原則名稱 >**關聯 VMM 雲端**。

    ![複寫原則](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>後續步驟

跳過[步驟 11： 啟用複寫](vmm-to-azure-walkthrough-enable-replication.md)
