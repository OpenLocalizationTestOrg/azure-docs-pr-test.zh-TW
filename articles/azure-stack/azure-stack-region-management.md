---
title: "aaaRegion 管理 Azure 堆疊中的 |Microsoft 文件"
description: "Azure Stack 中的區域管理概觀。"
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a>Azure Stack 中的區域管理
Azure 的堆疊已 hello 概念的區域，也就是組成 hello hello Azure 堆疊基礎結構所組成的硬體資源的邏輯實體。 內部區域管理中，您可以找到所有資源的必要的 toosuccessfully 都運作 hello Azure 堆疊基礎結構的生命週期。

hello Azure 堆疊開發套件是以單一節點部署，而且等於一個區域。 如果您設定不同的硬體上 Azure 堆疊開發套件的另一個執行個體，這個執行個體是 hello 的不同的區域。

## <a name="information-available-through-hello-region-management-tile"></a>可透過 hello 區域管理並排顯示的資訊
Azure 堆疊都有可用的 hello 的區域管理功能的一組**區域管理**磚。 此磚是可用 tooa hello hello 管理員入口網站中的預設儀表板上的雲端系統管理員。 您可以透過此磚來監視和更新特定區域的 Azure Stack 區域及其元件。

 ![hello 區域管理圖格](media/azure-stack-manage-region/image1.png)

 如果您按一下 hello 區域管理磚中的區域，您可以存取 hello 下列資訊：

  ![描述窗格在 hello 區域管理刀鋒視窗上的](media/azure-stack-manage-region/image2.png)

1. **hello 資源功能表**。 您可以在這裡存取特定的基礎結構管理領域，以及檢視和管理租用戶資源，例如儲存體帳戶和虛擬網路。

2. **警示**。 此磚會列出全系統警示，並提供每個警示的詳細資料。

3. **更新**。 在此磚，您可以檢視 hello Azure 堆疊基礎結構的目前版本。

4. **資源提供者**。 資源提供者是 hello 位置 toomanage hello 租用戶提供的功能 hello 元件需要 toorun Azure 堆疊。 每個資源提供者皆隨附系統管理體驗。 這項體驗可以包含 hello 特定提供者、 度量和其他管理功能特定 toohello 資源提供者的警示。
 
5. **基礎結構角色**。 基礎結構角色是 hello 元件需要 toorun Azure 堆疊。 列出報告警示的唯一 hello 基礎結構角色。 按一下角色，您可以檢視 hello 與 hello 特定角色，此角色執行所在的 hello 角色執行個體相關聯的警示。 雖然 hello 功能 toostart，重新啟動，或關閉基礎結構角色執行個體，執行**不**開發套件環境中執行這項操作。 這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。 Hello 開發套件中重新啟動角色執行個體 (特別是 Xrp01 AzS) 會導致系統不穩定。

## <a name="next-steps"></a>後續步驟
[在 Azure Stack 中監視健康情況和警示](azure-stack-monitor-health.md)

[在 Azure Stack 中管理更新](azure-stack-updates.md)






