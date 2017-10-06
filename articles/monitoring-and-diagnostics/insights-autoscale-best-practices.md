---
title: "自動調整規模 aaaBest 作法 |Microsoft 文件"
description: "在 Azure 中自動調整 Web 應用程式、虛擬機器擴展集和雲端服務的規模模式。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>自動調整規模的最佳做法
本文將說明在 Azure 中的最佳作法 tooautoscale。 Azure 監視的自動調整規模太只適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)，[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。 其他 Azure 服務使用不同的調整方法。

## <a name="autoscale-concepts"></a>自動調整的概念
* 資源可以只有「一項」  自動調整設定。
* 自動調整設定可有一或多個設定檔，而且每個設定檔都能有一或多項自動調整規則。
* 自動調整規模設定可調整執行個體的水平即*出*藉由增加 hello 執行個體和*中*藉由降低 hello 的執行個體的數目。
  自動調整設定可設定執行個體數的最大值、最小值及預設值。
* 自動調整規模作業一定會讀取 hello 相關聯的度量 tooscale 藉由檢查若它已越過 hello 為向外延展或向中設定的閾值。 您可以在 [Azure 監視器自動調整的常見度量](insights-autoscale-common-metrics.md)中，檢視自動調整據以調整的度量清單。
* 所有臨界值都是在執行個體層級計算。 比方說，「 逾時依 1 個執行個體調整當執行個體計數是 2 的平均 CPU > 80%"，當 hello 所有執行個體的平均 CPU 高於 80%時，表示向外延展。
* 您一律會從電子郵件收到失敗通知。 具體來說，hello 擁有者、 參與者與讀者 hello 目標資源會收到電子郵件。 當自動調整從失敗復原並開始正常運作時，您也一律會收到「復原」電子郵件。
* 您可以選擇加入的 tooreceive 成功延展動作通知電子郵件和 webhook。

## <a name="autoscale-best-practices"></a>自動調整最佳做法
使用下列最佳作法，當您使用自動調整規模的 hello。

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>請 hello 最大和最小值不同，兩者之間有足夠的臨界值
如果您有設定具有最小值 = 2，最大值 = 2，而 hello 目前執行個體計數為 2，可能會發生任何調整規模動作。 保留足夠的邊界之間 hello 最大和最小執行個體計數，都包含在內。 在這些限制之間，一定律會自動調整。

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>自動調整的最小值與最大值會重設手動調整
如果您手動更新 hello 執行個體計數 tooa 值上方或下方 hello 上限 hello 自動調整引擎自動縮放後 toohello 最小值 （如果下方） 或 hello 最大值 （如果上方）。 例如，您可以設定 hello 範圍介於 3 到 6 之間。 如果您有一個執行執行個體，hello 自動調整引擎會在下次執行縮放 too3 執行個體。 同樣地，它會向單元 8 個執行個體在下次執行備份 too6。  手動調整是非常暫時性的除非您重設 hello 自動調整規模規則。

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>請一律使用相應放大和相應縮小規則的組合來執行增加與減少。
如果您使用只有一個 hello 組合的一部分時，自動調整規模規模單元單一 out 或，直到 hello 上限或最小值、 為止。

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>請勿在管理自動調整規模時不 hello Azure 入口網站和 hello Azure 傳統入口網站之間切換
雲端服務和應用程式服務 （Web 應用程式），使用 hello Azure 入口網站 (portal.azure.com) toocreate 和管理自動調整規模設定。 虛擬機器擴展集，請使用 PowerShell、 CLI 或 REST API toocreate 和管理自動調整規模設定。 不會轉換 hello Azure 傳統入口網站 (manage.windowsazure.com) 與 hello Azure 入口網站 (portal.azure.com) 之間時管理自動調整規模設定。 hello Azure 傳統入口網站，而且其基礎的後端有限制。 移動 toohello Azure 入口網站 toomanage 自動調整規模使用圖形化使用者介面。 hello 的選項為 toouse hello 自動調整規模 PowerShell、 CLI 或 REST API （透過 Azure 資源總管）。

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>選擇診斷度量 hello 適當統計資料
診斷度量，您可以在選擇*平均*，*最小值*，*最大*和*總*為根據度量 tooscale。 hello 最常見的統計資料是*平均*。

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>選擇仔細 hello 所有度量類型臨界值
建議您根據實際情況，小心選擇不同的相應放大與相應縮小臨界值。

我們*不建議*自動調整規模設定，例如下方的 hello 範例與 hello 相同或相似的臨界值外，並在條件中：

* 當執行緒計數 <= 600 時，增加 1 個執行個體
* 當執行緒計數 >= 600 時，減少 1 個執行個體

讓我們看看什麼可能會導致可能令人混淆的 tooa 行為的範例。 請考慮下列順序的 hello。

1. 假設有與 2 的執行個體 toobegin，然後 hello 平均每個執行個體的執行緒數目成長 too625。
2. 自動調整會隨之相應放大，加入第 3 個執行個體。
3. 接下來，假設 hello 平均執行緒計數，跨執行個體落 too575。
4. 向下調整，之前，先自動調整規模會嘗試 tooestimate 哪些 hello 最終狀態將會是如果它以進行縮放。 例如，575 x 3 (目前的執行個體計數) = 1,725 / 2 (相應減少後的最終執行個體數) = 862.5 個執行緒。 這表示自動調整規模會有向外延展 tooimmediately 再次即使它在中，調整 hello 平均執行緒計數會維持為 hello 相同或甚至落只有少量。 不過，如果它向上同樣地，請重複 hello 整個程序，導致 tooan 無限迴圈。
5. tooavoid 這種情況下 （稱為 「 拍打"），自動調整規模並不向下調整完全。 相反地，它會略過，並會重新評估 hello 條件一次執行 hello 下一個時間 hello 服務的作業。 這可能會因為 575 hello 平均執行緒計數時，自動調整不會出現 toowork 感到困惑許多人。

小數位數在期間的估計是預定的 tooavoid"出現 flapping 的現象 」 的情況下，在標尺和向外延展動作持續在哪裡來回。 當您選擇 hello 向外延展且有相同的臨界值時，請記住這種行為。

我們建議您選擇適當的邊界，向外延展 hello 與在臨界值。 例如，請考慮下列更好的規則組合的 hello。

* 當 CPU% >= 80 時，增加 1 個執行個體
* 當 CPU% <= 60 時，減少 1 個執行個體

在此案例中  

1. 假設有與 2 的執行個體 toostart。
2. 如果在執行個體之間 hello 平均 CPU %too80，自動調整縮放出加入的第三個執行個體。
3. 現在，假設一段時間 hello CPU %落 too60。
4. 自動調整規模的小數位數的規則評估 hello 最終狀態 tooscale 中一樣。 例如 60x3 (目前的執行個體計數) = 180/2 (相應減少時的最終執行個體數) = 90。 因此自動調整規模不小數位數在因為它會立即再次有 tooscale 外。 而會略過相應減少。
5. 檢查 hello 下一次自動調整規模，hello CPU 繼續 toofall too50。 它會評估一次-50 x 3 執行個體類別 = 150 / 2 執行個體 = 75，低於 hello 向外延展的臨界值為 80，所以它縮放成功 too2 執行個體中。

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>調整特殊度量之臨界值時的注意事項
 針對特殊度量資訊，例如儲存體或服務匯流排佇列長度 」 指標，hello 臨界值會是 hello 訊息平均數目使用每個執行個體的目前數目。 請小心選擇 hello 選擇 hello 臨界值，此度量。

讓我們將其說明您了解與範例 tooensure hello 行為更好。

* 當儲存體佇列訊息計數 >= 50 時，增加 1 個執行個體
* 當儲存體佇列訊息計數 <= 10 時，減少 1 個執行個體

請考慮下列順序的 hello:

1. 有 2 個儲存體佇列執行個體。
2. 訊息保留下來，當您檢閱 hello 儲存體佇列，hello 總計數讀取 50。 您可能認為自動調整應執行相應放大動作。 但請注意，自動調整仍然是每個執行個體 50/2 =  25 則訊息， 因此不會進行相應放大。 第一個向外延展 toohappen hello，hello 儲存體佇列中的 hello 訊息總數應該是 100。
3. 接下來，假設 hello 的總訊息計數達到 100。
4. 由於 tooa 向外延展動作加入的第 3 個儲存體佇列執行個體。  hello 下一個向外延展動作就不會進行直到 hello 總 hello 佇列中的訊息計數達到 150，因為 150/3 = 50。
5. 現在 hello hello 佇列中的訊息數目會變小。 3 個執行個體，與 hello 第一個標尺的動作時發生 hello 中所有佇列的訊息總數相加 too30 因為 30/3 = 每個執行個體，也就是 hello 小數位數的臨界值的 10 個訊息。

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>當自動調整設定中設有多個設定檔時的調整注意事項
您可以在自動調整設定中選擇預設設定檔 (當沒有任何項目取決於排程或時間時套用)，也可以選擇週期性設定檔或期間固定的設定檔 (設有日期與時間範圍)。

當自動調整規模服務處理它們時，它一定會檢查在 hello 順序：

1. 固定日期設定檔
2. 週期性設定檔
3. 預設 (一律) 設定檔

如果設定檔條件符合時，自動調整不會檢查其下的 hello 下一個設定檔條件。 自動調整一次只會處理一個設定檔。 這表示如果您想 tooalso 包括處理條件，從較低層設定檔，您必須在 hello 目前的設定檔，以及包含這些規則。

請參考下列示範範例︰

hello 圖顯示自動調整規模設定具有預設的設定檔的最小執行個體 = 2 和最大執行個體 = 10。 在此範例中，規則時設定的 tooscale 外 hello 佇列中的 hello 訊息計數大於 10，小數位數在 hello 佇列中的 hello 訊息計數小於 3 時。 因此，現在 hello 資源可以調整 2 到 10 個執行個體之間。

此外，星期一設定成使用週期性設定檔， 其中最小執行個體數 = 2，最大執行個體數 = 12。 這表示在星期一，hello 第一次自動調整規模會檢查這個條件，如果 hello 執行個體計數為 2，擴充為 3 toohello 新的最小。 只要自動調整規模繼續進行此設定檔狀況比對 (Monday) toofind，它只會處理 hello CPU 型標尺出/入規則設定此設定檔。 此時，它不會檢查 hello 佇列長度。 不過，如果您也想 hello 佇列長度條件 toobe 檢查，您應該包含這些規則從 hello 預設設定檔以及星期一設定檔中。

同樣地，當自動調整規模切換後 toohello 預設設定檔時，它會先檢查是否 hello 最小和最大值符合條件的情況。 如果在 hello 階段的執行個體的 hello 數目為 12，它縮放中 too10，hello 最大允許 hello 預設設定檔。

![自動調整設定](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>當設定檔中設有多項規則時的調整注意事項
有可能 tooset 多個規則中有一個設定檔的情況。 服務會使用設定多個規則時，會使用下列一組自動調整規模規則的 hello。

對於「相應放大」，自動調整會在符合任何規則時執行。
在*標尺中*，自動調整規模要求 toobe 符合的所有規則。

tooillustrate，假設您有下列 4 的自動調整規模規則的 hello:

* 當 CPU < 30% 時相應縮小 1
* 當記憶體 < 50% 時相應縮小 1​
* 當 CPU > 75% 時相應放大 1
* 當記憶體 > 75% 時相應放大 1​

然後就會發生 hello 遵循：

* 當 CPU 為 76%，記憶體為 50% 時，會相應放大。
* 當 CPU 為 50%，記憶體為 76% 時，會相應放大。

如果 CPU 是 25%且記憶體 51%的自動調整規模並在 hello 相反地，**不**小數位數中。 為了 tooscale 中，CPU 必須 29%和記憶體 49%。

### <a name="always-select-a-safe-default-instance-count"></a>請一律選取安全的預設執行個體計數
hello 預設執行個體計數是重要度量都無法使用時，自動調整規模調整您服務 toothat 計數。 因此，請選取對您工作負載而言最安全的預設執行個體計數。

### <a name="configure-autoscale-notifications"></a>設定自動調整通知
自動調整規模通知 hello 系統管理員和參與者的 hello 資源以電子郵件如果發生任何 hello 下列條件：

* 自動調整規模服務失敗 tootake 動作。
* 度量不適用於自動調整規模服務 toomake 標尺決策。
* 度量資訊是可用 （復原） 再次 toomake 標尺決策。
  除了上述 toohello 條件，您可以設定電子郵件或 webhook 通知 tooget 收到成功的調整動作的通知。
  
您也可以使用 hello 自動調整引擎的活動記錄檔警示 toomonitor hello 健全狀況。 以下是範例太[訂用帳戶上的所有自動調整引擎作業建立活動記錄警示 toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)或太[建立活動記錄警示 toomonitor 所有無法在自動調整規模 / 上縮放作業您的訂用帳戶](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。

## <a name="next-steps"></a>後續步驟
- [建立活動記錄警示 toomonitor 訂用帳戶上的所有自動調整引擎作業。](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [建立活動記錄警示 toomonitor 所有無法在自動調整規模 / 調整您的訂用帳戶的作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
