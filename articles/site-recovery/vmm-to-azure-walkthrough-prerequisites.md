---
title: "HYPER-V tooAzure 複寫 （搭配 System Center VMM) 使用 Azure Site Recovery 的 aaaReview hello 必要條件 |Microsoft 文件"
description: "說明用於設定複寫、 容錯移轉和復原 VMM 雲端 tooAzure，在內部部署 HYPER-V Vm 與 Azure Site Recovery 的 hello 必要條件"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>步驟 2： 檢閱 HYPER-V (VMM) tooAzure 複寫 hello 必要條件

在檢閱之後 hello[案例架構](vmm-to-azure-walkthrough-architecture.md)，閱讀此文章 toomake 確定您了解 hello 部署必要條件。 

## <a name="prerequisites-and-limitations"></a>必要條件和限制

**需求** | **詳細資料**
--- | ---
**Azure 帳戶** | 您需要 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。
**Azure 儲存體** | 您需要 Azure 儲存體帳戶 toostore 複寫資料。<br/><br/> hello 儲存體帳戶必須在 hello 與 hello 相同區域 Azure 復原服務保存庫。<br/><br/>您可以使用[異地備援儲存體](../storage/common/storage-redundancy.md#geo-redundant-storage)或本地備援儲存體。 建議使用異地備援儲存體。 使用地理備援儲存體，地區的中斷發生時，如果或 hello 主要區域無法復原，就復原資料。<br/><br/> 您可以使用標準的 Azure 儲存體帳戶，或使用 Azure [進階儲存體](../storage/common/storage-premium-storage.md)。 進階儲存體可以裝載需要大量 I/O 的工作負載，且通常用於需要持續有高 I/O 效能和低延遲的 VM。 如果您使用進階儲存體來存放複寫的資料，您也需要標準儲存體帳戶。 標準儲存體帳戶會儲存擷取進行中的變更 tooon 內部部署資料的複寫記錄檔。
**Azure 網路** | 您需要[Azure 網路](../virtual-network/virtual-network-get-started-vnet-subnet.md)，容錯移轉之後連接 toowhich Azure Vm。 hello Azure 網路必須位於 hello hello 與相同的區域復原服務保存庫。
**內部部署 VMM 伺服器** | 您需要一或多部執行 System Center 2012 R2 或更新版本的 VMM 伺服器。<br/><br/> 每一部 VMM 伺服器必須有一或多個私人雲端。 每一個雲端需要一或多個主機群組。<br/><br/> hello VMM 伺服器需要網際網路存取。
**內部部署 Hyper-V** | HYPER-V 主機伺服器必須至少執行 Windows Server 2012 R2 HYPER-V hello 啟用角色或 Microsoft HYPER-V Server 2012 R2。 必須安裝 hello 最新的更新。<br/><br/> hello HYPER-V 主機必須位於 VMM 主機群組 （位於 VMM 雲端中）。<br/><br/> 主機必須具有您想 tooreplicated 的一個或多個 Vm。<br/><br/> HYPER-V 主機必須 toohello 連線的網際網路的複寫 tooAzure，直接或透過 proxy。 HYPER-V 伺服器必須具有本文所述的 hello 修正[2961977](https://support.microsoft.com/kb/2961977)。
**內部部署 Hyper-V VM** | 您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。 啟用複寫後，就可以修改 hello VM 名稱。 




## <a name="next-steps"></a>後續步驟

跳過[步驟 3： 規劃容量](vmm-to-azure-walkthrough-capacity.md)
