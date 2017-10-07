---
title: "aaaScale 手動或透過 Azure 入口網站的自動調整執行個體計數 |Microsoft 文件"
description: "深入了解如何 tooscale Azure 服務。"
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
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>手動或自動調整執行個體計數
在 [hello [Azure 入口網站](https://portal.azure.com/)、 您可以手動設定 hello 執行個體計數，您的服務，或您可以設定自動調整規模的 toohave 根據需求的參數。 這是通常參照的 tooas*向外延展*或*縮放*。

調整執行個體計數為基礎之前，您應該考慮的縮放比例會受到**定價層**加法 tooinstance 計數中。 不同的定價層可以有不同數量的核心和記憶體，並且因此會有較佳效能 hello 相同數目的執行個體 (也就是*向上延展*或*向下調整*)。 本文特別涵蓋了相應縮小和相應放大。

您可以調整在 hello 入口網站，而且您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust 在手動或自動調整規模。

> [!NOTE]
> 本文說明如何自動調整設定在 hello 入口網站的 toocreate [http://portal.azure.com](http://portal.azure.com)。在此入口網站中建立的自動調整規模設定無法編輯它 hello 傳統入口網站 ([http://manage.windowsazure.com](http://manage.windowsazure.com))。
> 
> 

## <a name="scaling-manually"></a>手動調整
1. 在 [hello [Azure 入口網站](https://portal.azure.com/)，按一下 [**瀏覽**，然後瀏覽 toohello 想資源 tooscale，例如**應用程式服務方案**。
2. 按一下 [設定] > [相應放大 (App Service 方案)]。
3. 頂端的 hello hello**標尺**刀鋒視窗，您可以看到 hello 服務的自動調整規模動作的歷程記錄。
   
    ![Scale blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > 這個圖表僅會顯示自動調整所執行的動作。 如果您手動調整 hello 執行個體計數，hello 變更將不會反映在此圖表中。
   > 
   > 
4. 您可以手動調整 hello 數目**執行個體**使用滑桿。
5. 按一下 hello**儲存**命令，而且將會是幾乎立即調整 toothat 執行個體數目。

## <a name="scaling-based-on-a-pre-set-metric"></a>根據預先設定的計量進行調整
如果您想要的執行個體的 tooautomatically 調整根據度量的 hello 數字，選取 hello hello 中您要的度量**縮放**下拉式清單。 例如在 [App Service 方案]，您可以根據 [CPU 百分比] 進行調整。

1. 當選取度量，得到滑桿，及/或，您想要的 tooscale 之間文字方塊 tooenter hello 執行個體數目：
   
    ![Scale blade with CPU Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    自動調整規模絕對不會接受服務低於或高於 hello 界限的設定，無論您的負載。
2. 第二，您可以選擇 hello hello 度量的目標範圍。 例如，如果您選擇**CPU 百分比**，您可以設定目標 hello 平均 CPU hello 執行個體的所有服務中。 Hello 平均 CPU 超過 hello 您定義的最大值時，將會發生向外的延展，同樣地，每當 hello 平均 CPU 必須低於最小的 hello 將會發生在標尺。
3. 按一下 hello**儲存**命令。 自動調整規模將會檢查確定您在您的度量是在 hello 執行個體範圍和目標每隔幾分鐘的時間 toomake。 當服務收到額外流量時，無需執行任何動作，您就會獲到更多個執行個體。

## <a name="scale-based-on-other-metrics"></a>根據其他計量進行調整
您可以調整根據度量資訊會出現在 hello 的 hello 預設以外**縮放**下拉式清單中，並可以即使有一組複雜的向外延展並調整規模規則中。

### <a name="adding-or-changing-a-rule"></a>新增或變更規則
1. 選擇 hello**排程和效能規則**在 hello**縮放**下拉式清單中：![效能規則](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. 如果您先前已自動調整規模，在您會看到您所擁有的 hello 確切規則的檢視。
3. tooscale 根據另一個公制按一下 hello**加入規則**資料列。 您也可以按一下其中一個的 hello 現有資料列 toochange 從 hello 度量，您先前必須要由 tooscale toohello 度量。
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. 現在您需要的 tooselect 要由 tooscale 的度量。 當選擇度量有幾件事 tooconsider:
   
   * hello*資源*hello 度量來源。 一般而言，這會是 hello 與 hello 資源會擴充相同。 不過，如果您想要的儲存體佇列的 hello 深度 tooscale，hello 資源是您想要依 tooscale 的 hello 佇列。
   * hello*衡量標準名稱*本身。
   * hello*時間彙總*hello 標準。 這是 hello 資料如何透過 hello 是結合*持續時間*。
5. 選擇您的度量之後，您會選擇 hello 度量和 hello 運算子 hello 臨界值。 例如，假設 [大於] 設為 [80%]。
6. 然後選擇 [hello 動作的 tootake。 共有幾種不同的動作類型：
   
   * 增加或減少-這會加入或移除 hello**值**您定義的執行個體的數目
   * 增加或減少百分比-這會以百分比變更 hello 執行個體計數。 例如，您可以將 25 放在 hello**值**] 欄位中，而且如果您目前有 8 個執行個體時，會加入 2。
   * 增加或減少太-這會將 hello 執行個體計數 toohello**值**您定義。
7. 最後，您可以選擇關閉-之後 hello 先前延展動作 tooscale 一次這項規則應等待多久 cool。
8. 設定規則之後，請按 [ **確定**]。
9. 一旦您已設定的所有您想要的 hello 規則，可確定 toohit hello**儲存**命令。

### <a name="scaling-with-multiple-steps"></a>使用多個步驟進行調整
上述的 hello 範例是相當基本。 不過，如果您想 toobe 更積極的調整規模 （上下），您甚至可以將加入多個小數位數的規則 hello 相同度量。 例如，您可以在 CPU 百分比上定義兩項調整規則：

1. 如果 CPU 百分比高於 60%，則相應增加 1 個執行個體
2. 如果 CPU 百分比高於 85%，則相應增加 3 個執行個體

![Multiple scale rules](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

透過這項附加規則，如果您的負載在調整動作之前超過 85%，您將會增加兩個執行個體，而不是一個。

## <a name="scale-based-on-a-schedule"></a>根據排程進行調整
根據預設，當您建立調整規則時，它會一律套用。 您可以看到，當您按一下 hello 設定檔的標頭：

![設定檔](./media/insights-how-to-scale/Insights_Profile.png)

不過，您可能想 toohave 更積極的縮放比例 hello 天或 hello 週期間比 hello 週末。 您甚至可以在下班時間完全關閉您的服務。

1. toodo，在 hello 設定檔，選取**循環**而不是**一定**選擇 hello 時間的 hello 設定檔 tooapply。
2. 例如，toohave hello 週 hello 期間套用的設定檔**天**下拉式清單中取消選取**星期六**和**星期日**。
3. toohave hello 白天，將 hello 期間套用的設定檔**開始時間**toohello 當日時間，您想要在 toostart。
   
    ![預設週期](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. 按一下 [確定] 。
5. 接下來，您將需要您在其他時候想 tooapply tooadd hello 設定檔。 按一下 hello**新增設定檔**資料列。
    ![下班](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. 為您的第二個新設定檔命名，例如，您可以把它叫做 **下班**。
7. 然後選取**循環**一次，然後選擇您想要在這段期間的 hello 執行個體計數範圍。
8. 以 hello 預設設定檔，選擇 [hello**天**您希望此設定檔 tooapply，和 hello**開始時間**hello 一天。
   
   > [!NOTE]
   > 自動調整規模會使用 hello 日光節約規則為準**時區**您選取。 不過，在 hello UTC 位移會顯示 hello 基底的時區位移，不 hello 日光節約 UTC 位移的日光節約時間期間。
   > 
   > 
9. 按一下 [確定] 。
10. 現在，您將需要 tooadd 任何規則您想 tooapply 期間您的第二個設定檔。 按一下**加入規則**，然後您可以建構 hello 相同規則您擁有 hello 預設設定檔期間。
    
    ![新增規則 toooff 工作](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. 要確定 toocreate 這兩個向外的延展和規則中的小數位數，否則期間 hello 設定檔 hello 執行個體計數將只成長 （或減少）。
12. 最後，按一下 [ **儲存**]。

## <a name="next-steps"></a>後續步驟
* [監視服務計量](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
* [啟用監視和診斷](insights-how-to-use-diagnostics.md)toocollect 詳細高頻率度量，您的服務。
* 每當發生作業事件或計量超過臨界值時，[接收警示通知](insights-receive-alert-notifications.md)。
* [監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。
* [檢視事件和活動記錄檔](insights-debugging-with-events.md)toolearn 所有發生在您的服務中的項目。
* [監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。

