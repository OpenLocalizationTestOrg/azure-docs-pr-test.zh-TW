---
title: "Azure Batch 的服務配額和限制 | Microsoft Docs"
description: "了解預設的 Azure Batch 配額、限制和條件約束，以及如何要求增加配額"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a>Batch 服務配額和限制

如同使用其他 Azure 服務，對於與 Batch 服務相關聯的特定資源有一些限制。 這其中有許多限制是 Azure 在訂用帳戶或帳戶層級上所套用的預設配額。 本文將討論這些預設值，以及如何申請加大配額。

當您設計和相應增加您的 Batch 工作負載時，請記住這些配額。 例如，如果您的集區未觸達您所指定的計算節點目標數目，您可能已達到 Batch 帳戶的核心配額限制，或是您訂用帳戶的地區 VM 核心配額。

您可以在單一 Batch 帳戶中執行多個 Batch 工作負載，或在相同訂用帳戶 (但不同 Azure 區域) 的 Batch 帳戶之間散佈工作負載。

如果您計劃在 Batch 中執行生產工作負載，您可能需要增加一或多個高於預設值的配額。 若要加大配額，您可以開啟線上 [客戶支援要求](#increase-a-quota) ，不另外加收費用。

> [!NOTE]
> 配額是一種信用限制，不是容量保證。 如果您有大規模的容量需求，請連絡 Azure 支援。
> 
> 

## <a name="resource-quotas"></a>資源配額
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>使用者訂用帳戶模式中的配額

針對集區配置模式設定為**使用者訂用帳戶**的 Batch 帳戶，當集區建立時，Batch VM 和其他資源 (例如儲存體帳戶) 會直接建立在訂用帳戶中。 Azure Batch 核心配額不適用於在此模式中建立的帳戶。 相反地，會套用您在地區計算核心和其他資源之訂用帳戶中的配額。 深入了解 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)中的配額。

在規劃以使用者訂用帳戶模式所建立的帳戶之資源使用狀況時，請注意每 40 個 Linux VM 或 20 個 Windows VM 就需要下列 Batch 資源 (除了計算核心)：

| 資源 | 配額 | 提供者 |
| --- | ---| --- |
| 一個儲存體帳戶 | 儲存體帳戶 | Microsoft.Storage |
| 一個公用 IP 位址 | 公用 IP 位址 | Microsoft.Network | 
| 一個虛擬網路 | 虛擬網路 | Microsoft.Network | 
| 一個網路安全性群組 | 網路安全性群組 | Microsoft.Network | 
| 一個虛擬機器擴展集 | 虛擬機器擴展集 | Microsoft.Compute | 
| 一個負載平衡器 | 負載平衡器 | Microsoft.Network | 

區域層級或每個 VM 系列的核心配額應根據您的 Batch 集區或集區所需的 VM 大小來設定︰

| 配額 | 提供者 |
| --- | ---- |
| 地區核心總數 | Microsoft.Compute |
| … 系列的核心 | Microsoft.Compute |



## <a name="other-limits"></a>其他限制
| **Resource** | **上限** |
| --- | --- |
| [並行工作](batch-parallel-node-tasks.md)  |4 x 節點的核心數目 |
| [應用程式](batch-application-packages.md)  |20 |
| 每個應用程式的應用程式封裝 |40 |
| 應用程式封裝大小 (每一個) |大約 195 GB<sup>1</sup> |
| 最大啟動工作大小 | 32768 個字元<sup>2</sup> |

<sup>1</sup> 對於區塊 Blob 大小上限的 Azure 儲存體限制<br />
<sup>2</sup> 包含資源檔案和環境變數

## <a name="view-batch-quotas"></a>檢視 Batch 配額
在 [Azure 入口網站][portal]中檢視您的 Batch 帳戶配額。

1. 在入口網站中選取 [Batch 帳戶]  ，然後選取您感興趣的 Batch 帳戶。
2. 在 Batch 帳戶的功能表刀鋒視窗上選取 [屬性]。
3. [屬性] 刀鋒視窗會顯示目前套用至 Batch 帳戶的「配額」 
   
    ![Batch 帳戶配額][account_quotas]

針對在使用者訂用帳戶模式中建立的 Batch 帳戶，可在 Azure 入口網站中檢視相關的訂用帳戶配額。

1. 選取 [訂用帳戶]，然後選取您要用於 Batch 帳戶的訂用帳戶。

2. 在 [訂用帳戶] 刀鋒視窗中，選取 [使用量 + 配額]。



## <a name="increase-a-quota"></a>增加配額
使用 [Azure 入口網站][portal]，遵循下列步驟來要求增加您 Batch 帳戶或訂用帳戶的配額。 增加配額的類型取決於您 Batch 帳戶的集區配置模式。

### <a name="increase-a-batch-cores-quota"></a>增加 Batch 的核心配額 

如果您是在 **Batch 服務**模式中建立 Batch 帳戶，請遵循下列步驟來要求增加 Batch 的核心配額︰

1. 選取入口網站儀表板上的 [說明 + 支援] 圖格或入口網站右上角的問號 (**？**)。
2. 選取 [新增支援要求] > [基本]。
3. 在 [基本]  刀鋒視窗上：
   
    a. **問題類型** > **配額**
   
    b. 選取您的訂用帳戶。
   
    c. **配額類型** > **批次**
   
    d. **支援方案** > **配額支援 - 已包含**
   
    按一下 [下一步] 。
4. 在 [問題]  刀鋒視窗上：
   
    a. 根據[商業影響][support_sev]選取 [嚴重性]。
   
    b.這是另一個 C# 主控台應用程式。 在 [詳細資料] 中，指定每個您想要變更的配額、Batch 帳戶名稱和新限制。
   
    按一下 [下一步] 。
5. 在 [連絡資訊]  刀鋒視窗上：
   
    a. 選取 [偏好的連絡方式]。
   
    b. 確認並輸入必要的連絡人詳細資料。
   
    按一下 [建立]  提交支援要求。

一旦您上傳支援要求，Azure 支援會與您連絡。 請注意，完成要求最多需要花費 2 個工作天。

### <a name="increase-a-subscription-cores-quota"></a>增加訂用帳戶核心配額

如果您是在**使用者訂用帳戶**模式中建立 Batch 帳戶，而且您需要其他地區或 VM 系列核心，請要求增加您訂用帳戶中的配額。 如需步驟，請參閱 [Resource Manager 核心配額增加要求](../azure-supportability/resource-manager-core-quotas-request.md)。



## <a name="related-topics"></a>相關主題
* [使用 Azure 入口網站建立 Azure Batch 帳戶](batch-account-create-portal.md)
* [Azure Batch 功能概觀](batch-api-basics.md)
* [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
