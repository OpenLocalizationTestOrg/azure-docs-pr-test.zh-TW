---
title: "HYPER-V 複寫 （而不使用 System Center VMM) tooAzure 使用 Azure Site Recovery 保存庫註冊 aaaSet |Microsoft 文件"
description: "摘要說明您需要 HYPER-V 複寫 tooAzure 使用 Azure Site Recovery 保存庫註冊 tooset hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>步驟 7：設定 Hyper-V 複寫的保存庫

本文說明如何 tooset 保存庫，並指定您想要從您的內部部署位置，使用 hello tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>選取保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 按一下 [復原服務保存庫] > 保存庫。
2. 在 hello 資源功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**。
3. 在**保護目標**，選取**tooAzure** > **是的含 HYPER-V**。 選取**否**tooconfirm 您未使用 VMM。 

    ![選擇目標](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>後續步驟

跳過[步驟 8： 設定來源和目標](hyper-v-site-walkthrough-source-target.md)
