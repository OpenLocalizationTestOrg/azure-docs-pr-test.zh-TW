---
title: "HYPER-V 複寫 tooa 次要 VMM 站台與 Azure Site Recovery 的 aaaReview hello 必要條件 |Microsoft 文件"
description: "說明複寫 HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery hello 必要條件。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>步驟 2： 檢閱 HYPER-V 虛擬機器複寫 tooa 次要 VMM 站台的 hello 必要條件和限制


您已檢閱過 hello 之後[案例架構](vmm-to-vmm-walkthrough-architecture.md)，閱讀此文章 toomake 確定當您了解 hello 部署必要條件，在 系統中心虛擬複寫在內部部署 HYPER-V 虛擬機器 (Vm) 管理Machine Manager (VMM) 雲端，tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="prerequisites-and-limitations"></a>必要條件和限制

**需求** | **詳細資料**
--- | ---
**Azure** | [Microsoft Azure](http://azure.microsoft.com/) 訂用帳戶。<br/><br/> 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。<br/><br/> [深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。<br/><br/> 檢查網站復原，在各地區上市中支援的 hello 區域[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。
**VMM 伺服器** | 我們建議您有兩部 VMM 伺服器在 hello 主要站台，一個次要的 hello 中。<br/><br/> 支援在單一 VMM 伺服器上的雲端之間進行複寫。<br/><br/> VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新的更新。<br/><br/> VMM 伺服器需要網際網路存取。
**VMM 雲端** | 每一部 VMM 伺服器必須在一個或多個雲端，而所有雲端必須都具有 hello HYPER-V 容量設定檔集合。 <br/><br/>雲端必須包含一或多個 VMM 主機群組。<br/><br/> 如果您只有一部 VMM 伺服器，它需要至少兩個雲端、 tooact 為主要和次要資料庫。
**Hyper-V** | HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。<br/><br/> Hyper-V 伺服器應該包含一或多部 VM。<br/><br/>  HYPER-V 主機伺服器應該位於 hello 主要和次要 VMM 雲端中的主機群組。<br/><br/> 如果您在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，請安裝[更新 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> 如果您在 Windows Server 2012 上的叢集中執行 Hyper-V，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集訊息代理程式。 手動設定 hello 叢集代理人。 [閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。<br/><br/> Hyper-V 伺服器需要網際網路存取。




## <a name="next-steps"></a>後續步驟

跳過[步驟 3： 規劃網路](vmm-to-vmm-walkthrough-network.md)。
