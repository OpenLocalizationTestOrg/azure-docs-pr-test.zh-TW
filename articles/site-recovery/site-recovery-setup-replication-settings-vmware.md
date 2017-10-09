---
title: "Azure Site Recovery 的複寫設定 aaaSet |Microsoft 文件"
description: "描述如何 toodeploy Site Recovery tooorchestrate 複寫、 容錯移轉和復原 VMM 中的 HYPER-V Vm 的雲端 tooAzure。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>管理 VMware tooAzure 的複寫的原則


## <a name="create-a-replication-policy"></a>建立複寫原則

1. 選取 [管理] > [Site Recovery 基礎結構]。
2. 在 [VMware 和實體機器] 下選取 [複寫原則]。
3. 選取 [+複寫原則]。

    ![建立複寫原則](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. 輸入 hello 原則名稱。

5. 在**RPO 臨界值**，指定 hello RPO 上限。 連續複寫超過此限制時，會產生警示。
6. 在**復原點保留**，指定 （以小時為單位） hello hello 保留期間的每個復原點的持續時間。 受保護的電腦可以是復原 tooany 點內的保留週期。

    > [!NOTE]
    > Too24 小時保留的總機器複寫的 toopremium 存放裝置的支援。 Too72 小時保留的總機器複寫的 toostandard 存放裝置的支援。

    > [!NOTE]
    > 系統會自動建立容錯回復的複寫原則。

7. 在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。

8. 按一下 [確定] 。 應該在 30 too60 秒內建立 hello 原則。

![產生複寫原則](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>使組態伺服器與複寫原則產生關聯
1. 選擇 hello 複寫原則 toowhich 想 tooassociate hello 組態伺服器。
2. 按一下 [關聯]。
![關聯組態伺服器](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. 從伺服器 hello 清單中選取 hello 組態伺服器。
4. 按一下 [確定] 。 hello 組態伺服器應該與其相關以一個 tootwo 分鐘為單位。

![關聯組態伺服器](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>編輯複寫原則
1. 選擇您想要的 tooedit 複寫設定的 hello 複寫原則。
![編輯複寫原則](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. 按一下 [編輯設定] 。
![編輯複寫原則設定](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. 變更您的需求為基礎的 hello 設定。
4. 按一下 [儲存] 。 hello 原則應該儲存在兩個 toofive 分鐘，視多少 Vm 會使用該複寫原則。

![儲存複寫原則](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>使組態伺服器與複寫原則中斷關聯
1. 選擇 hello 複寫原則 toowhich 想 tooassociate hello 組態伺服器。
2. 按一下 [中斷關聯]。
3. 從伺服器 hello 清單中選取 hello 組態伺服器。
4. 按一下 [確定] 。 hello 組態伺服器應該取消關聯，以一個 tootwo 分鐘為單位。

    > [!NOTE]
    > 如果沒有至少一個複寫的項目使用 hello 原則，無法中斷與組態伺服器。 請確定沒有使用 hello 原則之前中斷與 hello 組態伺服器的複寫項目。

## <a name="delete-a-replication-policy"></a>刪除複寫原則

1. 選擇 hello 複寫原則的 toodelete。
2. 按一下 [刪除] 。 hello 原則應該刪除 30 too60 （秒）。

    > [!NOTE]
    > 如果有至少一個組態相關聯伺服器 tooit，您無法刪除的複寫原則。 請確定沒有任何複寫的項目，使用 hello 原則並刪除 hello 原則之前，先刪除所有 hello 相關聯設定伺服器。
