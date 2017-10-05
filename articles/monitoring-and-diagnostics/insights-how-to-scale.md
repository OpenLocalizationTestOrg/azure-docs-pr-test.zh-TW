---
title: "手動調整執行個體計數或使用 Azure 入口網站自動調整 | Microsoft Docs"
description: "了解如何調整您的 Azure 服務。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: d171538ea57839eccddcc74ca099a39aee34ea10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>手動或自動調整執行個體計數
在 [Azure 入口網站](https://portal.azure.com/)中，您可以手動設定服務的執行個體計數，或是藉由參數設定根據需求自行調整。 這通常稱為「相應放大」或「相應縮小」。

在根據執行個體計數進行調整之前，您應該考慮到調整除了會受到執行個體計數的影響以外，還會受到 **定價層** 的影響。 不同的定價層可以有不同數目的核心和記憶體，因此他們可以為相同數目的執行個體帶來較高的效能 (這就是「相應增加」或「相應減少」)。 本文特別涵蓋了相應縮小和相應放大。

您可以在入口網站中進行調整，並且也可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 來手動或自動調整級別。

> [!NOTE]
> 這篇文章說明如何在入口網站 ([http://portal.azure.com](http://portal.azure.com)) 中建立自動調整設定。 在此入口網站中建立的自動調整設定不能在傳統入口網站 ([http://manage.windowsazure.com](http://manage.windowsazure.com)) 中編輯。
> 
> 

## <a name="scaling-manually"></a>手動調整
1. 在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [瀏覽]，然後瀏覽至您想要調整的資源，例如 [App Service 方案]。
2. 按一下 [設定] > [相應放大 (App Service 方案)]。
3. 您可以在 [級別] 刀鋒視窗的頂端，查看服務的自動調整動作歷程記錄。
   
    ![Scale blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > 這個圖表僅會顯示自動調整所執行的動作。 如果您手動調整執行個體計數，則此變更將不會反映在該圖表中。
   > 
   > 
4. 您可以使用滑桿手動調整 [ **執行個體** ] 數目。
5. 按一下 [ **儲存** ] 命令，您的執行個體便會立即被調整到該數目。

## <a name="scaling-based-on-a-pre-set-metric"></a>根據預先設定的計量進行調整
如果您要讓執行個體數目根據計量自動調整，請在 [ **調整依據** ] 下拉式清單中選取您要的計量。 例如在 [App Service 方案]，您可以根據 [CPU 百分比] 進行調整。

1. 當您選取計量時，您會看到一個滑桿，和/或可輸入您要調整的執行個體數目範圍文字方塊：
   
    ![Scale blade with CPU Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    無論負載為何，自動調整絕對不會將您的服務調整低於或高於您的設定界限。
2. 其次，您可以選擇計量的目標範圍。 例如，如果您選擇 [ **CPU 百分比**]，您可以為服務中的所有執行個體設定平均 CPU 的目標。 當平均 CPU 超過您所定義的最大值時，便會發生相應放大，同樣地，每當平均 CPU 低於最小值時，便會發生相應縮小。
3. 按一下 [ **儲存** ] 命令。 自動調整每隔幾分鐘就會檢查一次，以確定您仍在計量的執行個體範圍和目標內。 當服務收到額外流量時，無需執行任何動作，您就會獲到更多個執行個體。

## <a name="scale-based-on-other-metrics"></a>根據其他計量進行調整
您可以根據出現在 [ **調整依據** ] 下拉式清單中的計量 (預設格式除外) 進行調整，而且甚至可以有一組複雜的相應放大和相應縮小規則。

### <a name="adding-or-changing-a-rule"></a>新增或變更規則
1. 在 [調整依據] 下拉式清單中選擇 [排程和效能規則]：![效能規則](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. 如果您先前有過自動調整，您便會看到先前使用的確切規則的檢視。
3. 若要根據另一個計量進行調整，請按一下 [ **新增規則** ] 資料列。 您也可以按一下其中一個現有資料列，將您先前使用的計量變更為所需的調整依據計量。
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. 現在，您必須選取所需的調整依據計量。 選擇計量時會有幾個考量事項：
   
   * 計量的來源 *資源* 。 一般而言，這會與您要調整的資源相同。 不過，如果您想要根據儲存體佇列的深度進行調整，則資源就會是您的調整依據佇列。
   * 本身的 *計量名稱* 。
   * 計量的 *時間彙總* 。 這是資料在 *持續時間*內組合的方式。
5. 選擇您的計量之後，您會選擇計量的臨界值，以及運算子。 例如，假設 [大於] 設為 [80%]。
6. 然後選擇您要採取的動作。 共有幾種不同的動作類型：
   
   * 增加或減少依據 - 這會新增或移除您所定義執行個體數目的 [ **值** ]
   * 增加或減少百分比 - 這會以百分比來變更執行個體計數。 例如，您可以在 [ **值** ] 欄位中輸入 25，如果您目前有 8 個執行個體，則會增加 2 個執行個體。
   * 增加或減少至 - 這會將執行個體計數設定為您所定義的 [ **值** ]。
7. 最後，您可以選擇等待期間 - 在前次調整動作之後，此規則要再次執行調整前所應等待的時間。
8. 設定規則之後，請按 [ **確定**]。
9. 在設定您所有想要的規則之後，請務必要按 [ **儲存** ] 命令。

### <a name="scaling-with-multiple-steps"></a>使用多個步驟進行調整
以上都是基本範例。 不過，如果您想要更靈活地相應增加 (或減少)，您甚至可以為相同的計量新增多項調整規則。 例如，您可以在 CPU 百分比上定義兩項調整規則：

1. 如果 CPU 百分比高於 60%，則相應增加 1 個執行個體
2. 如果 CPU 百分比高於 85%，則相應增加 3 個執行個體

![Multiple scale rules](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

透過這項附加規則，如果您的負載在調整動作之前超過 85%，您將會增加兩個執行個體，而不是一個。

## <a name="scale-based-on-a-schedule"></a>根據排程進行調整
根據預設，當您建立調整規則時，它會一律套用。 當您按一下 [設定檔標頭] 時會看到：

![設定檔](./media/insights-how-to-scale/Insights_Profile.png)

不過，在一天、一週和週末當中，您可能會想要進行更積極的調整。 您甚至可以在下班時間完全關閉您的服務。

1. 若要這樣做，請在您的設定檔中選取 [週期性] 而不是 [一律使用]，然後選擇您要設定檔套用的時間。
2. 例如，若要準備要在一週當中套用的設定檔，請在 [天] 下拉式清單中取消核取 [星期六] 和 [星期日]。
3. 若要準備要在白天當中套用的設定檔，請將 [ **開始時間** ] 設定為您要開始的當日時間。
   
    ![預設週期](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. 按一下 [確定] 。
5. 接下來，您必須新增您要在其他時候套用的設定檔。 按一下 [ **新增設定檔** ] 資料列。
    ![下班](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. 為您的第二個新設定檔命名，例如，您可以把它叫做 **下班**。
7. 然後再次選取 [ **週期性** ]，並選擇在這段期間您想要的執行個體計數範圍。
8. 和預設設定檔一樣，選擇要設定檔套用的 [天]，以及當天的 [開始時間]。
   
   > [!NOTE]
   > 自動調整會為您所選取的任何 [ **時區** ] 使用日光節約規則。 不過，在日光節約時間期間，UTC 時差會顯示基本的時區時差，而不是日光節約的 UTC 時差。
   > 
   > 
9. 按一下 [確定] 。
10. 現在，您必須新增您要在第二個設定檔期間套用的任何規則。 按一下 [ **新增規則**]，然後您可以在預設設定檔中建構相同的規則。
    
    ![新增規則至下班](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. 請務必建立相應放大和相應縮小這兩個規則，否則在設定檔期間，執行個體計數將只增加 (或減少)。
12. 最後，按一下 [ **儲存**]。

## <a name="next-steps"></a>後續步驟
* [監視服務計量](insights-how-to-customize-monitoring.md) 以確保您的服務可用且可回應。
* [啟用監視和診斷](insights-how-to-use-diagnostics.md) 來在您服務中收集詳細的高頻率計量。
* [接收警示通知](insights-receive-alert-notifications.md) 。
* [監視應用程式效能](../application-insights/app-insights-azure-web-apps.md) 。
* [檢視事件和活動記錄檔](insights-debugging-with-events.md)以了解在您服務內發生的所有內容。
* [監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。

