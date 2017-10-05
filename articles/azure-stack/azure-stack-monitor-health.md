---
title: "在 Azure Stack 中監視健康情況和警示 | Microsoft Docs"
description: "了解如何在 Azure Stack 中監視健康情況和警示。"
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
ms.openlocfilehash: 93835eabcf9622735aada0f5dfa46028553c25bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>在 Azure Stack 中監視健康情況和警示

Azure Stack 包含可監視基礎結構的功能，可讓雲端操作員檢視 Azure Stack 區域的健康情況和警示。

Azure Stack 具有一組可用於 [區域管理] 磚的區域管理功能。 此磚依預設會釘選在預設提供者訂用帳戶的系統管理員入口網站上，可列出 Azure Stack 的所有已部署區域。 它也會顯示每個區域的作用中重要和警告警示計數。 此磚是您進入 Azure Stack 健康情況和警示功能的進入點。

 ![區域管理磚](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a>了解 Azure Stack 中的健康情況

 在 Azure Stack 中健康情況和警示是由健康情況資源提供者來管理。 在 Azure Stack 部署和設定期間，Azure Stack 基礎結構元件會向健康情況資源提供者註冊。 這項註冊讓每個元件的健康情況和警示得以顯示。 在 Azure Stack 中健康情況是個簡單的概念。 如果元件的已註冊執行個體有警示存在，該元件的健康情況狀態會反映出最差的作用中警示嚴重性：警告或重要。
 
 ## <a name="view-and-manage-component-health-state"></a>檢視和管理元件健康情況狀態
 
 您可在 Azure Stack 系統管理員入口網站上檢視元件的健康情況狀態，也可以透過 REST API 和 PowerShell 來檢視。
 
若要在入口網站中檢視健康情況狀態，請在 [區域管理] 磚中按一下您想要檢視的區域。 您可以檢視基礎結構角色和資源提供者的健康情況狀態。 請注意，在此版本中，「計算」資源提供者不會報告健康情況狀態。

![基礎結構角色的清單](media/azure-stack-monitor-health/image2.png)

您可以按一下資源提供者或基礎結構角色，以檢視更詳細的資訊。

> [!WARNING]
>如果您按一下基礎結構角色，然後按一下角色執行個體，在 [角色執行個體] 刀鋒視窗中會有選項可 [啟動]、[重新啟動] 或 [關機]。 **請勿**在 Azure Stack 開發套件環境中使用這些選項。 這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。 重新啟動開發套件中的角色執行個體 (特別是 AzS-Xrp01) 會導致系統不穩定。 如需疑難排解協助，請將您的問題張貼到 [Azure Stack 論壇](https://aka.ms/azurestackforum)。
>
 
## <a name="view-alerts"></a>檢視警示

可直接從 [區域管理] 刀鋒視窗檢視每個 Azure Stack 區域的作用中警示清單。 預設設定下的第一個磚是 [警示] 磚，其中會顯示該區域的重要和警告警示摘要。 就像這個刀鋒視窗中的其他磚一樣，您可以將 [警示] 磚釘選到儀表板上以便快速存取。   

![會顯示警告的 [警示] 磚](media/azure-stack-monitor-health/image3.png)

您可選取 [警示] 磚的上半部，瀏覽至區域的所有作用中警示清單。 如果您選取磚內的 [重要] 或 [警告] 明細項目，就會瀏覽至警示的篩選清單 (重要或警告)。 

![篩選的警告警示](media/azure-stack-monitor-health/image4.png)
  
[警示] 刀鋒視窗支援依狀態 (作用中或已關閉) 和嚴重性 (重要或警告) 進行篩選。 預設檢視會顯示所有作用中警示。 所有已關閉的警示會在七天後從系統中移除。

![依重要或警告狀態進行篩選的篩選器](media/azure-stack-monitor-health/image5.png)

[警示] 刀鋒視窗也會公開 [檢視 API] 動作，可顯示用來產生清單檢視的 REST API。 這個動作可讓您快速熟悉 REST API 語法，可用以查詢警示。 您可用自動化方式使用此 API，或與您現有的資料中心監視、報告及票證解決方案整合。 

![會顯示 REST API 的 [檢視 API] 選項](media/azure-stack-monitor-health/image6.png)

您可以從 [警示] 刀鋒視窗中，選取警示以瀏覽至 [警示詳細資料] 刀鋒視窗。 此刀鋒視窗會顯示與警示相關聯的所有欄位，並可快速瀏覽至受影響的元件和警示的來源。 例如，如果其中一個基礎結構角色執行個體離線或無法存取，就會發生以下警示。  

![[警示詳細資料] 刀鋒視窗](media/azure-stack-monitor-health/image7.png)

基礎結構角色執行個體回到線上之後，會自動關閉此警示。

## <a name="next-steps"></a>後續步驟

[在 Azure Stack 中管理更新](azure-stack-updates.md)

[Azure Stack 中的區域管理](azure-stack-region-management.md)
