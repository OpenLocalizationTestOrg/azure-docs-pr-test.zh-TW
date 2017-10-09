---
title: "aaaPrepare Azure 資源 tooreplicate 內部部署實體伺服器 tooAzure 使用 Azure Site Recovery |Microsoft 文件"
description: "說明您需要在 Azure 中的位置開始之前複寫在內部部署伺服器 tooAzure，使用 hello Azure Site Recovery 服務"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>步驟 5： 為實體伺服器複寫 tooAzure 準備 Azure 資源


使用此發行項 tooprepare Azure hello 指示資源，以便您可以將複寫在內部部署伺服器 tooAzure 使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="before-you-start"></a>開始之前

請確定您已閱讀 hello[必要條件](physical-walkthrough-prerequisites.md)。

## <a name="set-up-an-azure-account"></a>設定 Azure 帳戶

- 取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。
- 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
- 在站台復原檢查 hello 支援區域**各地區上市**中[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
- 深入了解[站台復原定價](site-recovery-faq.md#pricing)，並取得 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。



## <a name="set-up-an-azure-network"></a>設定 Azure 網路

- 設定 Azure 網路。 在容錯移轉之後建立的 Azure VM 會置於這個網路。
- 站台復原 hello Azure 入口網站中的可以使用在中設定網路[資源管理員](../resource-manager-deployment-model.md)，或以傳統模式。
- hello 網路應位於 hello hello 與相同的區域復原服務保存庫。
- 深入了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。
- 深入了解容錯移轉後的 [Azure VM 連線](physical-walkthrough-network.md)。


## <a name="set-up-an-azure-storage-account"></a>設定 Azure 儲存體帳戶

- Site Recovery 會複寫在內部部署伺服器 tooAzure 儲存體。 容錯移轉發生後，會建立 hello 儲存體從 azure Vm。
- 為複寫的資料設定 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。
- 站台復原 hello Azure 入口網站中的可以使用資源管理員 中，或在傳統模式中設定的儲存體帳戶。
- hello 儲存體帳戶可以是標準或[premium](../storage/common/storage-premium-storage.md)。
- 如果您設定的是進階帳戶，則也需要一個額外的標準帳戶來記錄資料。


## <a name="next-steps"></a>後續步驟

跳過[步驟 6： 設定保存庫](physical-walkthrough-create-vault.md)
