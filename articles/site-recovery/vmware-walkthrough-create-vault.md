---
title: "上的 VMware 複寫 tooAzure 使用 Azure Site Recovery 保存庫 aaaSet |Microsoft 文件"
description: "摘要說明您需要 VMware 複寫 tooAzure 使用 Azure Site Recovery 保存庫註冊 tooset hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>步驟 7： 設定的 VMware 複寫 tooAzure 保存庫


本文說明如何 tooset 保存庫，並指定您想要從您的內部部署位置，使用 hello tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。




## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>選取保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 按一下 [復原服務保存庫] > 保存庫。
2. 在 hello 資源功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**。
3. 在**保護目標**，選取**tooAzure** > **是的與 VMware vSphere Hypervisor**。



## <a name="next-steps"></a>後續步驟

跳過[步驟 8： 設定來源和目標](vmware-walkthrough-source-target.md)
