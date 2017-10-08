---
title: "aaaMonitor 健全狀況和 Azure 堆疊中的警示 |Microsoft 文件"
description: "深入了解如何 toomonitor 健全狀況和 Azure 堆疊中的警示。"
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>在 Azure Stack 中監視健康情況和警示

Azure 堆疊包含基礎結構監視功能，可讓雲端操作員 tooview 健全狀況和堆疊 Azure 區域的警示。

Azure 堆疊都有可用的 hello 的區域管理功能的一組**區域管理**磚。 這個 hello hello 預設提供者訂用帳戶的系統管理員入口網站中的預設釘選的磚會列出 Azure 堆疊的所有部署的 hello 區域。 它也會顯示 hello 計數的每個區域的作用中的重大和警告警示。 此磚會進入 hello 健全狀況和 Azure 堆疊的警示功能。

 ![hello 區域管理圖格](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a>了解 Azure Stack 中的健康情況

 健全狀況和警示是由 hello 健全狀況資源提供者管理 Azure 堆疊中。 Azure 堆疊部署和設定期間，與 hello 健全狀況資源提供者註冊 azure 的堆疊基礎結構元件。 這個登錄可讓 hello 顯示健全狀況和每個元件的警示。 在 Azure Stack 中健康情況是個簡單的概念。 如果已註冊的元件存在，執行個體警示 hello 該元件的健全狀況狀態會反映出 hello 最差作用中警示嚴重性;警告或重大。
 
 ## <a name="view-and-manage-component-health-state"></a>檢視和管理元件健康情況狀態
 
 在這兩個 hello Azure 堆疊管理員入口網站，並透過 Rest API 和 PowerShell，您可以檢視 hello 元件健全狀況狀態。
 
tooview hello 健全狀況狀態在 hello 入口網站中，按一下您想在 hello tooview hello 區域**區域管理**磚。 您可以檢視基礎結構角色和資源提供者的 hello 健全狀況狀態。 請注意，在此版本中，hello 計算資源提供者不會報告健全狀況狀態。

![基礎結構角色的清單](media/azure-stack-monitor-health/image2.png)

您可以按一下 tooview 資源提供者或基礎結構角色的詳細資訊。

> [!WARNING]
>如果您按一下 [基礎結構角色]，然後按一下hello 角色執行個體時，有在 hello 選項**角色執行個體**刀鋒視窗 tooStart、 重新啟動或關閉。 **請勿**在 Azure Stack 開發套件環境中使用這些選項。 這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。 Hello 開發套件中重新啟動角色執行個體 (特別是 Xrp01 AzS) 會導致系統不穩定。 如需疑難排解的協助，請張貼問題 toohello [Azure 堆疊論壇](https://aka.ms/azurestackforum)。
>
 
## <a name="view-alerts"></a>檢視警示

針對每個 Azure 堆疊區域的作用中警示的 hello 清單是可以直接從 hello**區域管理**刀鋒視窗。 hello hello 預設組態中的第一個磚為 hello**警示**磚，其中顯示 hello 重大和警告警示 hello 區域的摘要。 您可以釘選 hello 警示圖格，此刀鋒視窗中，讓您快速存取 toohello 儀表板上的任何其他磚。   

![會顯示警告的 [警示] 磚](media/azure-stack-monitor-health/image3.png)

選取頂部 hello hello**警示**磚，您瀏覽 toohello hello 區域的所有作用中警示清單。 如果您選取其中一個 hello**重大**或**警告**hello 磚中的明細項目，您瀏覽 tooa 篩選警示 （重大或警告） 的清單。 

![篩選的警告警示](media/azure-stack-monitor-health/image4.png)
  
hello**警示**刀鋒視窗支援 hello 能力 toofilter （作用中或已關閉） 的狀態和嚴重性 （重大或警告）。 hello 預設檢視會顯示所有作用中警示。 所有已關閉的警示會在 7 天後從 hello 系統移除。

![篩選窗格 toofilter 重大或警告狀態](media/azure-stack-monitor-health/image5.png)

hello 警示刀鋒伺服器也會公開 hello**檢視 API**哪些顯示 hello Rest API 所使用的 toogenerate hello 清單檢視的動作。 這個動作可提供快速 toobecome 熟悉 hello Rest API 語法，您可以使用 tooquery 警示。 您可用自動化方式使用此 API，或與您現有的資料中心監視、報告及票證解決方案整合。 

![hello 顯示 hello Rest API 的 API 檢視選項](media/azure-stack-monitor-health/image6.png)

您可以從 hello 警示刀鋒視窗中，選取警示 toonavigate toohello**警示詳細資料**刀鋒視窗。 此刀鋒視窗會顯示 hello 警示相關聯的所有欄位，並可讓快速瀏覽 toohello 受影響的元件和 hello 警示的來源。 例如，hello 下列警示就會發生如果其中一個 hello 基礎結構角色執行個體離線或無法存取。  

![hello 警示詳細資料 刀鋒視窗](media/azure-stack-monitor-health/image7.png)

Hello 基礎結構角色執行個體回到線上之後，會自動關閉此警示。

## <a name="next-steps"></a>後續步驟

[在 Azure Stack 中管理更新](azure-stack-updates.md)

[Azure Stack 中的區域管理](azure-stack-region-management.md)
