---
title: "使用 Azure Site Recovery aaaPrepare Azure 資源 tooreplicate （不含 System Center VMM) 的 HYPER-V Vm tooAzure |Microsoft 文件"
description: "說明您需要在 Azure 中的位置複寫使用 「 Azure 站台復原的 HYPER-V Vm (沒有 VMM) tooAzure 開始之前"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>步驟 5： 準備 HYPER-V 複寫 tooAzure Azure 資源

使用 hello 指示中此發行項 tooprepare Azure 資源，讓您可以將複寫在內部部署 HYPER-V Vm （不含 System Center VMM) 使用 hello tooAzure [Azure Site Recovery](site-recovery-overview.md)服務。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="before-you-start"></a>開始之前

請確定您已閱讀 hello[必要條件](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>設定 Azure 帳戶

- 取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。
- 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
- 檢查網站復原，在各地區上市中支援的 hello 區域[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
- 深入了解[站台復原定價](site-recovery-faq.md#pricing)，並取得 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。


## <a name="set-up-an-azure-network"></a>設定 Azure 網路

- 設定 Azure 網路。 在容錯移轉之後建立的 Azure VM 會置於這個網路。
- hello 網路應位於 hello hello 與相同的區域復原服務保存庫
- 站台復原 hello Azure 入口網站中的可以使用在中設定網路[資源管理員](../resource-manager-deployment-model.md)，或以傳統模式。
- 建議您在開始之前先設定網路。 如果沒有，您需要 toodo Site Recovery 部署期間它。
- 深入了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。


## <a name="set-up-an-azure-storage-account"></a>設定 Azure 儲存體帳戶

- Site Recovery 會複寫在內部部署機器 tooAzure 存放裝置。 容錯移轉發生後，會建立 hello 儲存體從 azure Vm。
- 設定標準/優質[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)toohold 資料複寫 tooAzure。
- [高階儲存體](../storage/common/storage-premium-storage.md)通常用於需要一直居高 IO 效能和低度延遲 toohost IO 密集工作負載的虛擬機器。
- 如果您想要 toouse premium 帳戶 toostore 複寫的資料，您也需要標準儲存體帳戶 toostore 複寫記錄檔擷取進行中變更 tooon 內部部署資料。
- Hello 資源模型，根據您想 toouse 容錯移轉 Azure Vm，您在設定帳戶[Resource Manager 模式](../storage/common/storage-create-storage-account.md)，或[傳統模式](../storage/common/storage-create-storage-account.md)。
- 建議您在開始之前先設定儲存體帳戶。 如果您需要 toodo Site Recovery 部署期間它。 hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。
- 儲存體帳戶之間所使用的站台復原 hello 內的資源群組相同，則無法移動訂用帳戶，或跨不同的訂用帳戶。


## <a name="next-steps"></a>後續步驟

跳過[步驟 6： 準備 HYPER-V 資源](hyper-v-site-walkthrough-prepare-hyper-v.md)
