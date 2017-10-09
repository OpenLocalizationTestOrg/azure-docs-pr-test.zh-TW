---
title: "aaaPrepare System Center VMM 的 HYPER-V 複寫 tooAzure |Microsoft 文件"
description: "描述如何為 HYPER-V 複寫 tooAzure，使用 Azure Site Recovery 的 tooprepare System Center VMM 伺服器"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>步驟 6： 準備 HYPER-V 複寫 tooAzure 的 VMM 伺服器和 HYPER-V 主機

設定好後[Azure 元件](vmm-to-azure-walkthrough-prepare-azure.md)hello 部署，請使用本文章 tooprepare 在內部部署 VMM 伺服器和 HYPER-V 主機 toointeract 中的 hello 指示與 Azure Site Recovery。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="prepare-vmm-servers"></a>準備 VMM 伺服器

- 您需要至少一個 VMM 伺服器符合 hello 支援需求的站台復原複寫 (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)。
- 請確定您已備妥 VMM 伺服器 hello[網路對應](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)。
- 請確定該 hello VMM 伺服器可以存取這些 Url

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- 如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。
- 允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。
- 允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。

Site Recovery 部署期間，您下載 hello Site Recovery 提供者，並將它安裝在每部 VMM 伺服器。 hello 復原服務保存庫中登錄 hello VMM 伺服器。




## <a name="next-steps"></a>後續步驟

跳過[步驟 7： 建立保存庫](vmm-to-azure-walkthrough-create-vault.md)

