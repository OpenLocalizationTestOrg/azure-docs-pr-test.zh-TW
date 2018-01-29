---
title: "在 Azure 成本管理中檢閱使用量和成本 | Microsoft Docs"
description: "檢閱使用量和成本，以追蹤趨勢、偵測效率不足的情況並建立警示。"
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 10/11/2017
ms.topic: tutorial
ms.service: cost-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 363a7e8a5b5be2175cb2f6d3539878673a2b469a
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2017
---
# <a name="review-usage-and-costs"></a>檢閱使用量和成本

Cloudyn 的 Azure 成本管理顯示使用量和成本，讓您可以追蹤趨勢、偵測效率不足的情況並建立警示。 所有使用量和成本資料都會顯示在 Cloudyn 儀表板和報表中。 本教學課程中的範例將引導您使用儀表板和報表來檢閱使用量和成本。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 追蹤使用量和成本趨勢
> * 偵測使用效率不足的情況
> * 針對不尋常的消費或超額消費建立警示



## <a name="open-the-cloudyn-portal"></a>開啟 Cloudyn 入口網站

您可以在 Cloudyn 入口網站中檢閱所有使用量和成本。 從 Azure 入口網站開啟 Cloudyn 入口網站，或瀏覽至 https://azure.cloudyn.com 並登入。

## <a name="track-usage-and-cost-trends"></a>追蹤使用量和成本趨勢

您可以使用不同時間報表來追蹤使用量和成本的實際金額支出，以識別趨勢。 若要開始查看趨勢，請使用不同時間的實際成本報表。 在入口網站頂端的 [報表] 功能表上，按一下 [成本] > [成本分析] > [不同時間的實際成本]。 當您第一次開啟報表時，不會對其套用任何群組或篩選。

以下是範例報表：

![範例報表](./media/tutorial-review-usage/actual-cost01.png)

該報表顯示過去 30 天的所有消費。 若只要檢視 Azure 服務的消費，請套用服務群組，然後篩選出所有 Azure 服務。 下圖顯示經過篩選的服務。

![經過篩選的服務](./media/tutorial-review-usage/actual-cost02.png)

在上述範例中，自 2017年 8 月 31 日起，金額支出會比之前低。 該成本趨勢會在各種服務中持續約 9 天。 接著會如往常一般繼續有更多的消費。 不過，資料行太多可能模糊明顯的趨勢。 您可以將報表檢視變更為折線圖或區域圖，來查看以其他檢視顯示的資料。 下圖可更加清楚地顯示趨勢。

![報表中的趨勢](./media/tutorial-review-usage/actual-cost03.png)

在此範例中，您清楚看到 Azure 儲存體成本自 2017年 8 月 31 日起會降低，而其他 Azure 服務的消費則持平。 造成消費降低的原因為何？ 在此範例中，有些員工休假而未使用儲存體服務。

若要觀看有關追蹤使用量和成本趨勢的教學指導影片，請參閱[使用 Cloudyn 的 Azure 成本管理分析您的雲端計費資料與時間](https://youtu.be/7LsVPHglM0g)。

## <a name="detect-usage-inefficiencies"></a>偵測使用效率不足的情況

最佳化報表會提升效率、最佳化使用方式，並找出節省雲端資源金額支出的方式。 這對於提供符合成本效益的大小調整建議，以協助減少閒置或昂貴的 VM 特別有幫助。

組織首次將資源移入雲端時，一個影響組織的常見問題就是其虛擬化策略。 它們通常使用類似於為內部部署虛擬環境建立虛擬機器所使用的方法。 此外也假設藉由將其內部部署 VM 依現況移至雲端可降低成本。 不過，該方法不太可能會降低成本。

問題在於已支付其現有基礎結構的費用。 如果想要，使用者可建立並執行大量的 VM (這些 VM 可以閒置或不閒置且影響不大)。 將大量或閒置的 VM 移至雲端可能會「增加」成本。 當您與雲端服務提供者簽訂合約時，資源的成本配置很重要。 您必須針對是否完整使用資源的認可來支付費用。

符合成本效益的大小調整建議報表藉由比對 VM 執行個體類型容量與其 CPU 和記憶體使用量歷程記錄資料，來識別每年可能省下的費用。  

在入口網站頂端的 [報表] 功能表上，按一下 [Optimizer] \(最佳化工具) > [Pricing Optimization] \(價格最佳化) > [Cost Effective Sizing Recommendations] \(符合成本效益的大小調整建議)。 將提供者篩選到 Azure，只查看 Azure VM。 以下是範例影像。

![Azure VM](./media/tutorial-review-usage/sizing01.png)

在此範例中，藉由遵循變更 VM 執行個體類型的建議，即可省下美金 $3,114 元。 按一下 [詳細資料] 下的加號 (+)，以展開第一個建議。 以下是第一個建議的相關詳細資料。

![建議的詳細資料](./media/tutorial-review-usage/sizing02.png)

按一下 [List of Candidates] \(候選項目清單) 旁的加號，以檢視 VM 執行個體識別碼。

![候選項目清單](./media/tutorial-review-usage/sizing03.png)

若要觀看有關偵測使用效益不彰情形的教學指導影片，請參閱[在 Cloudyn 的 Azure 成本管理中最佳化 VM 大小](https://youtu.be/1xaZBNmV704)。

## <a name="create-alerts-for-unusual-spending"></a>針對不尋常的消費建立警示

您可以在出現異常消費和超額消費風險時自動向專案關係人發出警示。 您可以輕鬆快速地使用支援根據預算和成本閾值發出警示的報表來建立警示。

您可以使用任何成本報表針對任何消費建立警示。 在此範例中，使用不同時間的成本報表在 Azure VM 的消費接近總預算時通知您。 在入口網站頂端的 [報表] 功能表上，按一下 [成本] > [成本分析] > [不同時間的實際成本]。 將 [群組] 設定為 [服務]，並將 [Filter on the service] \(服務上的篩選) 設定為 [Azure/VM]。 在報表的右上方，按一下 [動作]，然後選取 [排程報表]。

使用 [排程] 索引標籤，以您想要的頻率傳送報表電子郵件給自己。 您所使用的任何標記、群組和篩選都會包含在以電子郵件傳送的報表中。 按一下 [閾值] 索引標籤，然後選取 [Actual Cost vs. Threshold] \(實際成本與閾值)。 如果您的總預算為美金 $500,000 元，而且想要在成本接近大約一半時收到通知，請在美金 $250,000 元處建立**紅色警示**，並在美金 $240,000 元處建立**黃色警示**。 然後，選擇連續警示數目。 當您收到所指定的警示總數時，不會再傳送其他警示。 儲存排程報表。

![範例報表](./media/tutorial-review-usage/schedule-alert01.png)

您也可以選擇 [Cost Percentage vs.Budget] \(成本百分比與預算) 閾值計量來建立警示。 透過該計量，您就可以使用預算百分比，而不是貨幣值。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 追蹤使用量和成本趨勢
> * 偵測使用效率不足的情況
> * 針對不尋常的消費或超額消費建立警示


請前進到下一個教學課程，以了解如何控制資料的存取。

> [!div class="nextstepaction"]
> [控制資料的存取](tutorial-user-access.md)
