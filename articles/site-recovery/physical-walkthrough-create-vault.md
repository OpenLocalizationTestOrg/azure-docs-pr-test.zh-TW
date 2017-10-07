---
title: "為實體伺服器複寫 tooAzure 使用 Azure Site Recovery 保存庫註冊 aaaSet |Microsoft 文件"
description: "摘要說明您需要使用 Azure Site Recovery 保存庫 tooreplicate 實體伺服器 tooAzure 向上 tooset hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>步驟 6： 設定實體伺服器複寫 tooAzure 的保存庫


本文說明如何 tooset 保存庫註冊。 您建立 hello 保存庫，並指定您想要從內部部署位置 tooAzure，使用 hello tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。




## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>選取保護目標

選取您想 tooreplicate，而且想要 tooreplicate。

1. 按一下 [復原服務保存庫] > 保存庫。
2. 在 hello 資源功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**。
3. 在**保護目標**，選取**tooAzure** > **未虛擬化/其他**。


## <a name="next-steps"></a>後續步驟

跳過[步驟 7： 設定來源和目標](physical-walkthrough-source-target.md)
