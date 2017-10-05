---
title: "Azure Stack 中的區域管理 | Microsoft Docs"
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
ms.openlocfilehash: 15a3bc9dce3cc76f98816ba5c88066fdc23cdbe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="region-management-in-azure-stack"></a>Azure Stack 中的區域管理
Azure Stack 具有區域概念，也就是由邏輯實體組成硬體資源以形成 Azure Stack 基礎結構。 在區域管理內，您可以找到成功操作 Azure Stack 基礎結構生命週期所需的所有資源。

Azure Stack 開發套件屬於單一節點部署，且等於一個區域。 如果您在不同硬體上設定 Azure Stack 開發套件的另一個執行個體，則此執行個體屬於不同的區域。

## <a name="information-available-through-the-region-management-tile"></a>您可以透過 [區域管理] 磚取得資訊
Azure Stack 具有一組可用於 [區域管理] 磚的區域管理功能。 雲端系統管理員可以在系統管理員入口網站中的預設儀表板上存取此磚。 您可以透過此磚來監視和更新特定區域的 Azure Stack 區域及其元件。

 ![區域管理磚](media/azure-stack-manage-region/image1.png)

 如果您按一下 [區域管理] 磚中的區域，則可以存取下列資訊：

  ![[區域管理] 刀鋒視窗上的窗格說明](media/azure-stack-manage-region/image2.png)

1. [資源功能表]。 您可以在這裡存取特定的基礎結構管理領域，以及檢視和管理租用戶資源，例如儲存體帳戶和虛擬網路。

2. **警示**。 此磚會列出全系統警示，並提供每個警示的詳細資料。

3. **更新**。 在此磚中，您可以檢視 Azure Stack 基礎結構的目前版本。

4. **資源提供者**。 資源提供者是可讓您管理執行 Azure Stack 時所需元件所提供之租用戶功能的位置。 每個資源提供者皆隨附系統管理體驗。 這項體驗可能包含特定提供者的警示、度量以及其他資源提供者專屬的管理功能。
 
5. **基礎結構角色**。 基礎結構角色是執行 Azure Stack 時所需的元件。 僅報告警示的基礎結構角色會列出。 您可以按一下角色來檢視與特定角色相關聯的警示，以及此角色執行所在的角色執行個體。 儘管包含啟動、重新啟動，或關閉基礎結構角色執行個體的功能，請**勿**在開發套件環境中執行這項操作。 這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。 重新啟動開發套件中的角色執行個體 (特別是 AzS-Xrp01) 會導致系統不穩定。

## <a name="next-steps"></a>後續步驟
[在 Azure Stack 中監視健康情況和警示](azure-stack-monitor-health.md)

[在 Azure Stack 中管理更新](azure-stack-updates.md)






