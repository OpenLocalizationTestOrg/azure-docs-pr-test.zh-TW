---
title: "Azure 的區域之間 aaaMigrate Azure IaaS Vm |Microsoft 文件"
description: "使用 Azure Site Recovery toomigrate Azure IaaS 虛擬機器從一個 Azure 區域 tooanother。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>使用 Azure Site Recovery 在 Azure 區域之間移轉 Azure IaaS 虛擬機器
## <a name="overview"></a>概觀
歡迎使用 tooAzure Site Recovery ！ 如果您想 toomigrate Azure Vm 之間的 Azure 區域，請使用本文章。 開始之前，請注意：

* Azure 建立和處理資源的部署模型有二種：Azure Resource Manager 和傳統。 Azure 也有兩個入口網站 – hello Azure 傳統入口網站支援 hello 傳統部署模型，與 hello Azure 入口網站支援這兩種部署模型。 hello 基本步驟移轉為 hello 相同是否您在資源管理員 」 或 「 傳統中設定站台復原。 不過 hello UI 指示和本文中的螢幕擷取畫面相關 hello Azure 入口網站。
* **目前您可以只從移轉一個區域 tooanother。您可以從一個 Azure 區域 tooanother，容錯移轉 Vm，但您無法回復它們一次。**

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="prerequisites"></a>必要條件
以下是您針對此部署所需要的項目︰

* **IaaS 虛擬機器**: hello 想 toomigrate 的 Vm。 您可以將那些 VM 視為實體機器來移轉它們。

## <a name="deployment-steps"></a>部署步驟
本章節描述 hello hello 新版 Azure 入口網站中的部署步驟。

1. [建立保存庫](site-recovery-vmware-to-azure.md)。
2. [啟用複寫](site-recovery-vmware-to-azure.md)。 啟用複寫 hello toomigrate，並選擇做為來源的 Azure Vm。 
3. [ 執行非計劃性容錯移轉](site-recovery-failover.md)。 完成初始複寫之後，您可以從一個 Azure 區域 tooanother 執行未規劃的容錯移轉。 （選擇性） 您可以建立復原計劃及執行非計劃性容錯移轉 toomigrate 區域之間的多部虛擬機器。 [深入了解](site-recovery-create-recovery-plans.md) 復原計劃。

## <a name="next-steps"></a>後續步驟
在 [什麼是 Azure Site Recovery？](site-recovery-overview.md)
