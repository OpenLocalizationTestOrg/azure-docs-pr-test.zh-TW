---
title: "HYPER-V VM （不含 System Center VMM) 的複寫 tooAzure 與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "摘要說明複寫 HYPER-V Vm tooAzure 儲存體時，需要建立複寫原則 tooset hello 步驟"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>步驟 9： 設定 HYPER-V 虛擬機器複寫 tooAzure 的複寫原則

本文說明如何建立複寫原則，當您要複寫使用 hello （不含 System Center VMM) 的 HYPER-V Vm tooAzure tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="about-snapshots"></a>關於快照集

HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。
    - 應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。
    - 如果您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。 確定您設定的 hello 值小於 hello 您設定其他復原點數目。

## <a name="set-up-a-replication-policy"></a>設定複寫原則

1. toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。

    ![網路](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. 在 [建立及關聯原則] 中指定原則名稱。
3. 在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。

    > [!NOTE]
    > 複寫 toopremium 存放裝置時，不支援第二個頻率為 30。 hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。 [深入了解](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)。

4. 在**復原點保留**，指定以小時多久 hello 保留週期是每個復原點。 Vm 就能復原 tooany 視窗內的點。
5. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。
6. 在**初始複寫開始時間**，指定當 toostart hello 初始複寫。 hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。 然後按一下 [確定] 。

    ![複寫原則](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

當您建立新的原則時，它會自動與相關聯 hello HYPER-V 站台。 您可以將 HYPER-V 站台 （和中的 hello Vm） 中的多個複寫原則與**複寫**> 原則名稱 >**關聯 HYPER-V 站台**。



## <a name="next-steps"></a>後續步驟

跳過[步驟 10： 啟用複寫](hyper-v-site-walkthrough-enable-replication.md)
