---
title: "aaaService 的 Azure Batch 配額與限制 |Microsoft 文件"
description: "深入了解預設 Azure Batch 配額、 限制和條件約束，及如何 toorequest 配額，以提升"
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
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Batch 服務配額和限制

做為與其他 Azure 服務，會有限制某些 hello 批次服務相關聯的資源。 許多這些限制會套用由 Azure hello 訂用帳戶或帳戶層級的預設配額。 本文將討論這些預設值，以及如何申請加大配額。

當您設計和相應增加您的 Batch 工作負載時，請記住這些配額。 比方說，如果您的集區未達到您所指定的運算節點的 hello 目標數目，您可能已達到 hello 核心配額限制您的 Batch 帳戶或區域的 VM 核心配額訂用帳戶。

您可以在單一批次帳戶，執行多個批次工作負載或散發您的工作負載中 hello 的批次帳戶中相同的訂用帳戶，但位於不同的 Azure 區域。

如果您計劃 toorun 生產工作負載，批次中的，您可能需要 tooincrease 一或多個上述 hello 預設 hello 配額。 如果您想 tooraise 配額時，您可以開啟線上[客戶支援要求](#increase-a-quota)不收費。

> [!NOTE]
> 配額是一種信用限制，不是容量保證。 如果您有大規模的容量需求，請連絡 Azure 支援。
> 
> 

## <a name="resource-quotas"></a>資源配額
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>使用者訂用帳戶模式中的配額

批次帳戶集區配置模式下設定得**使用者訂用帳戶**、 批次 Vm 和其他資源，例如儲存體帳戶、 建立集區時，直接在您的訂用帳戶中建立。 hello Azure 批次核心配額不適用 tooan 帳戶在此模式中建立。 相反地，會套用您地區計算核心和其他資源的訂用帳戶中的 hello 配額。 深入了解 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)中的配額。

在規劃資源使用狀況，在使用者訂用帳戶模式中建立的帳戶時，注意 hello 下列批次 （在加法 toocompute 核心） 的資源所需每 40 Linux Vm 或 20 Windows Vm:

| 資源 | 配額 | 提供者 |
| --- | ---| --- |
| 一個儲存體帳戶 | 儲存體帳戶 | Microsoft.Storage |
| 一個公用 IP 位址 | 公用 IP 位址 | Microsoft.Network | 
| 一個虛擬網路 | 虛擬網路 | Microsoft.Network | 
| 一個網路安全性群組 | 網路安全性群組 | Microsoft.Network | 
| 一個虛擬機器擴展集 | 虛擬機器擴展集 | Microsoft.Compute | 
| 一個負載平衡器 | 負載平衡器 | Microsoft.Network | 

在地區層級或每個 VM 系列 hello 核心配額應該集相應 toohello VM 大小所需的程式批次集區或集區：

| Quota | 提供者 |
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
檢視您的批次帳戶配額在 hello [Azure 入口網站][portal]。

1. 選取**批次帳戶**hello 入口網站，然後選取您感興趣的 hello Batch 帳戶。
2. 選取**屬性**hello 批次帳戶的 [功能表] 刀鋒視窗。
3. hello 屬性刀鋒視窗會顯示 hello**配額**目前套用 toohello 批次帳戶
   
    ![Batch 帳戶配額][account_quotas]

對於批次建立的帳戶使用者訂用帳戶模式中，檢視 hello 與相關 hello Azure 入口網站中的訂用帳戶配額。

1. 選取**訂閱**，選取您要用於 hello 批次帳戶的 hello 訂用帳戶。

2. 在 hello**訂用帳戶**刀鋒視窗中，選取**使用量 + 配額**。



## <a name="increase-a-quota"></a>增加配額
請遵循這些步驟 toorequest，配額增加您的 Batch 帳戶或訂用帳戶使用 hello [Azure 入口網站][portal]。 hello 的類型增加配額取決於您的 Batch 帳戶 hello 集區配置模式。

### <a name="increase-a-batch-cores-quota"></a>增加 Batch 的核心配額 

如果您的 Batch 帳戶中建立**批次服務**模式中，請遵循這些步驟 toorequest 批次核心配額增加：

1. 選取 hello**說明 + 支援**入口網站儀表板、 磚或 hello 問號 (**？**) 中的 hello 入口網站的 hello 右上角。
2. 選取 [新增支援要求] > [基本]。
3. 在 hello**基本概念**刀鋒視窗中：
   
    a. **問題類型** > **配額**
   
    b. 選取您的訂用帳戶。
   
    c. **配額類型** > **批次**
   
    d. **支援方案** > **配額支援 - 已包含**
   
    按一下 [下一步] 。
4. 在 hello**問題**刀鋒視窗中：
   
    a. 選取**嚴重性**根據 tooyour[業務衝擊][support_sev]。
   
    b. 在**詳細資料**，指定您想要 toochange、 hello 批次帳戶名稱和 hello 新限制每個配額。
   
    按一下 [下一步] 。
5. 在 hello**連絡資訊**刀鋒視窗中：
   
    a. 選取 [偏好的連絡方式]。
   
    b. 請確認，然後輸入所需的 hello 連絡人詳細資料。
   
    按一下**建立**toosubmit hello 支援要求。

一旦您上傳支援要求，Azure 支援會與您連絡。 請注意，完成 hello 要求可以佔用 too2 工作日。

### <a name="increase-a-subscription-cores-quota"></a>增加訂用帳戶核心配額

如果您是在**使用者訂用帳戶**模式中建立 Batch 帳戶，而且您需要其他地區或 VM 系列核心，請要求增加您訂用帳戶中的配額。 如需步驟，請參閱 [Resource Manager 核心配額增加要求](../azure-supportability/resource-manager-core-quotas-request.md)。



## <a name="related-topics"></a>相關主題
* [建立使用 hello Azure 入口網站的 Azure Batch 帳戶](batch-account-create-portal.md)
* [Azure Batch 功能概觀](batch-api-basics.md)
* [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
