---
title: "aaaScale 配額和限制您的實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何 tooscale 的實驗室中 Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>在 DevTest Labs 中調整配額和限制
DevTest 實驗室中工作時，您可能會注意到有特定的預設限制 toosome Azure 資源，這可能會影響 hello DevTest Labs 服務。 這些限制會參照的 tooas**配額**。

> [!NOTE]
> hello DevTest Labs 服務不會強制執行任何的配額。 您可能會遇到任何配額是 hello 整體 Azure 訂用帳戶的預設條件約束。

您可以使用每個 Azure 資源直到您達到其配額。 每個訂用帳戶都有個別配額，並且會追蹤每個訂用帳戶的使用量。

例如，每個訂用帳戶都有預設配額 20 個核心。 因此，如果您在具有四個核心的實驗室中建立 VM，則您只能建立五個 VM。 

[Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)列出一些 hello Azure 資源的最常見的配額。 hello 在實驗室中，最常使用的資源，並為您可能會遇到配額，加入 VM 核心、 公用 IP 位址、 網路介面、 受管理的磁碟、 RBAC 角色指派和 ExpressRoute 電路。

## <a name="view-your-usage-and-quotas"></a>檢視使用量和配額
這些步驟顯示如何 tooview 會 hello 目前配額的訂用帳戶特定的 Azure 資源，與 toosee 中您已使用的每個配額百分比。

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**計費**從 hello 清單。
1. 在 hello 帳單 刀鋒視窗中，選取 訂用帳戶。
4. 選取 [使用量 + 配額]。

   ![使用量和配額按鈕](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   hello 使用量 + 配額刀鋒視窗中隨即顯示，列出該訂用帳戶與 hello 的百分比表示每個資源正在使用的 hello 配額不同的資源。

   ![配額和使用量](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>要求訂用帳戶中的更多資源
如果達到配額上限，增加 tooa 最大限制，向上的 hello 預設限制的訂用帳戶中的資源中所述[Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)。

這些步驟會告訴您如何 toorequest 配額增加透過 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. 選取 [更多服務]，選取 [計費]，然後選取 [使用量 + 配額]。
1. 在 hello 使用量 + 配額刀鋒視窗中，選取 hello**要求增加** 按鈕。

   ![要求增加按鈕](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete 和提交 hello 要求，請填寫所有的三個索引標籤上的 hello 所需資訊的 hello**新增支援要求**表單。

   ![要求增加表單](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[了解 Azure 限制並增加](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/)提供詳細資訊連絡 Azure 支援 toorequest 配額增加。



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>後續步驟
* 瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。
