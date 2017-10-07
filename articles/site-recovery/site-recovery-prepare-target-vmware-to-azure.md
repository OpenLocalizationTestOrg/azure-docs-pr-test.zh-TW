---
title: "準備目標 (VMware tooAzure) |Microsoft 文件"
description: "本文說明如何 tooprepare 複寫 VMware 虛擬機器 tooAzure 您 Azure 環境 toostart。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>準備目標 (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [實體 tooAzure](./site-recovery-prepare-target-physical-to-azure.md)

本文說明如何 tooprepare 複寫 VMware 虛擬機器 tooAzure 您 Azure 環境 toostart。

## <a name="prerequisites"></a>必要條件

hello 文章假設 hello 下列：
- 您已建立復原服務保存庫 tooprotect VMware 虛擬機器。 您可以建立復原服務保存庫，從 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。
- 您有[安裝程式在內部部署環境](./site-recovery-set-up-vmware-to-azure.md)tooreplicate VMware 虛擬機器 tooAzure。

## <a name="prepare-target"></a>準備目標

完成 hello 之後**步驟 1:Select 保護目標**和**步驟 2： 準備來源**，會將您導向太**步驟 3： 目標**

![準備目標](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **訂用帳戶：** hello 從下拉式清單選取 hello 您想 tooreplicate 訂用帳戶 功能表，您的虛擬機器。
2. **部署模型：**選取 hello 部署模型 （Classic 或資源管理員）

根據 hello 選擇部署模型，會執行驗證，您有至少一個相容的儲存體帳戶和虛擬網路中 hello 目標訂用帳戶 tooreplicate 和容錯移轉虛擬機器以 tooensure。

一旦 hello 驗證順利完成，請按一下 [確定] toogo toohello 下一個步驟。

如果您沒有相容的資源管理員儲存體帳戶或虛擬網路，或想要更多的 tooadd，您可以按一下 hello **+ 儲存體帳戶**或**+ 網路**上 hello hello 頂端的按鈕刀鋒視窗。

## <a name="next-steps"></a>後續步驟
[設定複寫設定](./site-recovery-setup-replication-settings-vmware.md)。
