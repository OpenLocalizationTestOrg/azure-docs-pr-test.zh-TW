---
title: "aaaView hello 每月實驗室估計的成本趨勢 Azure DevTest Labs |Microsoft 文件"
description: "深入了解 hello Azure DevTest Labs 每月估計的成本趨勢圖。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>檢視 hello 每月實驗室估計的成本趨勢 Azure DevTest Labs
DevTest Labs hello 成本管理功能可協助您追蹤您的實驗室 hello 成本。 本文將說明如何 toouse hello**每月估計成本趨勢**圖表 tooview hello 行事曆月份的預估的成本與日期和月份 hello hello 規劃的結束月份的成本。 在本文中，您學會如何 tooview hello hello Azure 入口網站中的每月估計的成本趨勢圖。

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>檢視 hello 每月估計成本趨勢圖表
tooview hello 每月估計成本趨勢圖表，請遵循下列步驟： 

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。   
4. 在 hello 實驗室刀鋒視窗中，選取 **成本設定**。
5. 在 hello 實驗室**成本設定**刀鋒視窗中，選取**實驗室成本趨勢**。
6. hello 下列螢幕擷取畫面顯示成本圖表的範例。 
   
    ![成本圖表](./media/devtest-lab-configure-cost-management/graph.png)

hello**估計成本**值為 hello 行事曆月份的預估的成本與日期。 hello**預計成本**hello 估計的成本 hello 整個目前的日曆月份中，使用計算 hello 實驗室成本 hello 前五天。

hello 成本金額會無條件進位 toohello 下一個整數。 例如： 

* 5.01 會無條件進位 too6 
* 5.50 too6 向上四捨五入
* 5.99 會無條件進位 too6

指出 hello 圖表之上，即在 hello 圖表中的 hello 成本是*估計*成本使用[隨用隨付](https://azure.microsoft.com/offers/ms-azr-0003p/)提供率。
此外，hello 如下*不*納入成本計算 hello:

* CSP 和 Dreamspark 訂用帳戶目前不支援使用作為 Azure DevTest Labs 使用 hello [Azure 計費 Api](../billing/billing-usage-rate-card-overview.md) toocalculate hello 實驗室成本，不支援的 CSP 或 Dreamspark 訂用帳戶。
* 您的優惠費率。 目前，我們不能 toouse （您的訂用帳戶底下顯示），您有與交涉 Microsoft 或 Microsoft 合作夥伴您服務費率。 我們將使用隨用隨付費率。
* 您的稅率
* 您的折扣
* 您的帳單貨幣。 目前，hello 實驗室成本只會顯示在美金貨幣。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章
* [兩個的多個項目 tookeep 上處於 DevTest Labs 追蹤成本](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [為何要設定成本臨界值？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>後續步驟
以下是一些事情 tootry 下一步：

* [定義 lab 原則](devtest-lab-set-lab-policy.md)-了解如何 tooset hello 所使用的各種原則如何使用您的實驗室和其 Vm toogovern。 
* [建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。 本文說明如何 toocreate 自訂映像從 VHD 檔案。
* [設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。 本文將說明如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。
* [在實驗室中建立的 VM](devtest-lab-add-vm-with-artifacts.md) -說明如何 toocreate 將 VM 的基本映像從 (可能是自訂或 Marketplace)，以及如何 toowork 連同成品放在 VM 中。

