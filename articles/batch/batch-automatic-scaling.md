---
title: "aaaAutomatically 小數位數中的計算節點的 Azure Batch 集區 |Microsoft 文件"
description: "啟用自動調整上雲端的集區 toodynamically 調整 hello hello 集區中的運算節點數目。"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>建立自動調整公式來調整 Batch 集區中的計算節點

Azure Batch 可以根據您定義的參數自動調整集區。 自動縮放，批次以動態方式新增節點 tooa 集區做為工作需求增加，並移除計算節點，它們會降低。 您可以節省時間和金錢自動調整 hello 批次應用程式所使用的運算節點數目。 

您可讓您定義的「自動調整公式」與計算節點的集區產生關聯，以在該集區上啟用自動調整。 hello 批次服務會使用您的工作負載的運算節點所需的 tooexecute hello 自動調整公式 toodetermine hello 數目。 計算節點可以是專用節點或[低優先順序節點](batch-low-pri-vms.md)。 批次回應 tooservice 定期收集的度量資料。 使用此度量資料時，批次會調整運算節點，根據您的公式，並可設定的間隔 hello 集區中的 hello 的數目。

您可以在建立集區時或在現有的集區上啟用自動調整。 您也可以變更已針對自動調整設定之集區上的現有公式。 批次，可讓您執行之前將其指派 toopools 和 toomonitor hello 狀態自動調整公式的 tooevaluate。

這篇文章討論 hello 構成您的自動調整公式，包括變數、 運算子、 作業和函式的各種實體。 我們將討論如何 tooobtain 各種計算資源和工作批次內的度量。 您可以使用這些度量 tooadjust，集區的節點計數根據資源使用量和工作的狀態。 我們接著說明如何 tooconstruct 公式，並啟用自動調整集區上同時使用 hello 批次 REST 和.NET 應用程式開發介面。 最後，我們會完成幾個範例公式。

> [!IMPORTANT]
> 當您建立的批次帳戶時，您可以指定 hello[帳戶組態](batch-api-basics.md#account)，以決定是否將集區，配置在批次服務訂用帳戶 （hello 預設值），或您使用者訂用帳戶中。 如果您建立您的 Batch 帳戶與 hello 預設批次服務組態，您的帳戶是有限的 tooa 可以用於處理的核心數目上限。 hello 批次服務縮放只向上 toothat 核心限制的計算節點。 基於這個理由，hello 批次服務可能無法到達自動調整公式所指定的運算節點的 hello 目標的數目。 請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)的檢視，並增加您的帳戶配額的詳細資訊。
>
>如果您建立您的帳戶與 hello 使用者訂用帳戶設定，然後您的帳戶中的共用 hello hello 訂用帳戶的核心配額。 如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)中的 [虛擬機器限制](../azure-subscription-service-limits.md#virtual-machines-limits)。
>
>

## <a name="automatic-scaling-formulas"></a>自動調整公式
自動調整公式是您定義的字串值，其中包含一或多個陳述式。 hello 自動調整公式會指派集區 tooa [autoScaleFormula] [ rest_autoscaleformula]元素 (批次 REST) 或[CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula]屬性 (批次.NET)。 hello 批次服務會使用您公式 toodetermine hello 目標數目計算節點 hello 集區中的 hello 下一個處理間隔。 hello 公式字串不能超過 8 KB 的可以包括安裝 too100 陳述式，以分號分隔，而且可包含分行符號及註解。

您可以將自動調整公式視為 Batch 自動調整「語言」。 公式的陳述式是自由格式的運算式，可以包括服務定義的變數 （hello 批次服務所定義的變數） 及使用者定義的變數 （您所定義的變數）。 它們可以使用內建類型、運算子和函式對這些值執行各種作業。 例如，陳述式可能會接受下列表單的 hello:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

公式通常包含多個陳述式，其可對在先前陳述式中取得的值執行作業。 例如，在我們取得的值第一次`variable1`，然後將它傳遞 tooa 函式 toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

在您的自動調整公式 tooarrive 在計算節點的目標中包含這些陳述式。 專用節點與低優先順序節點各有自己的目標設定，因此您可以為每個節點類型定義目標。 自動調整公式可以包含專用節點目標值、低優先順序節點目標值，或同時包含兩者。

節點的 hello 目標數目可能較高、 低，或 hello 與 hello 目前的 hello 集區中的該類型的節點數目相同。 Batch 服務會在特定間隔評估集區的自動調整公式 (請參閱[自動調整間隔](#automatic-scaling-interval))。 批次調整每個 hello 評估 hello 時指定自動調整公式的集區 toohello 號碼中的節點類型的 hello 目標數目。

### <a name="sample-autoscale-formula"></a>自動調整公式範例

以下是可在大部分情況下的調整的 toowork 自動調整公式的範例。 hello 變數`startingNumberOfVMs`和`maxNumberofVMs`在 hello 範例公式可調整的 tooyour 需求。 這個公式縮放專用的節點，但是可以修改的 tooapply tooscale 低優先權的節點。 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

使用此自動調整公式的單一 VM 一開始建立 hello 集區。 hello`$PendingTasks`度量定義 hello 執行或佇列工作數目。 hello 公式 hello 的平均數目暫止工作在找到 hello 過去 180 秒，並設定 hello`$TargetDedicatedNodes`變數據此。 hello 公式可確保 hello 目標數目專用的節點永遠不會超過 25 的 Vm。 當提交新的工作，hello 集區自動成長。 做為工作完成，Vm 會變成可用逐一和 hello 自動調整公式壓縮 hello 集區。

## <a name="variables"></a>變數
您可以在自動調整公式中同時使用**服務定義**和**使用者定義**的變數。 hello 服務定義的變數是內建的 toohello 批次服務。 有些服務定義的變數是讀寫，有些是唯讀。 使用者定義的變數是您定義的變數。 在顯示 hello 前一節中的 hello 範例公式`$TargetDedicatedNodes`和`$PendingTasks`是服務定義的變數。 `startingNumberOfVMs` 和 `maxNumberofVMs` 變數是使用者定義的變數。

> [!NOTE]
> 服務定義的變數前面一律會加上貨幣符號 ($)。 針對使用者自訂變數，hello 貨幣符號是選擇性的。
>
>

下表中的 hello 顯示同時讀寫和唯讀變數所定義的 hello 批次服務。

您可以取得及設定 hello 這些變數的值定義服務集區中的運算節點 toomanage hello 數目：

| 讀寫服務定義變數 | 說明 |
| --- | --- |
| $TargetDedicatedNodes |hello 目標數目專用計算 hello 集區的節點。 hello 專用的節點數目被指定做為目標，因為集區可能無法永遠達成 hello 預期的節點數目。 比方說，如果 hello 目標專用的節點已修改的自動調整規模評估 hello 之前由集區已達到 hello 初始目標，然後 hello 集區可能無法到達 hello 目標。 <br /><br /> 如果 hello 目標超過批次帳戶節點或核心配額，與 hello 批次服務組態建立的帳戶中的集區可能無法達成其目標。 建立與 hello 使用者訂用帳戶設定的帳戶中的集區可能無法達成其目標，如果 hello 目標超過 hello hello 訂用帳戶的共用的核心配額。|
| $TargetLowPriorityNodes |低優先順序的 hello 目標數目計算 hello 集區的節點。 hello 低優先權的節點數目被指定做為目標，因為集區可能無法永遠達成 hello 預期的節點數目。 比方說，如果修改 hello 目標數目低優先權的節點，便自動調整規模評估 hello 之前由集區已達到 hello 初始目標，然後 hello 集區可能無法到達 hello 目標。 如果 hello 目標超過批次帳戶節點或核心配額，則集區可能也無法達成其目標。 <br /><br /> 如需有關低優先順序計算節點的詳細資訊，請參閱[搭配 Batch 使用低優先順序 VM (預覽)](batch-low-pri-vms.md)。 |
| $NodeDeallocationOption |hello 從集區移除運算節點時，就會發生的動作。 可能的值包括：<ul><li>**排入佇列**-會立即終止工作並將它們放入 hello 工作佇列，以便重新排定它們。<li>**終止**-會立即終止工作並將其從 hello 工作佇列中移除。<li>**taskcompletion**-等候目前正在執行工作 toofinish，然後從 hello 集區中移除 hello 節點。<li>**retaineddata**-所有 hello 上的本機工作保留資料 hello 節點 toobe 等候清除之前移除 hello 集區中的 hello 節點。</ul> |

您可以取得服務定義的變數 toomake 調整 hello 批次服務的度量資訊為基礎的 hello 的值：

| 唯讀服務定義變數 | 說明 |
| --- | --- |
| $CPUPercent |hello 平均 CPU 使用量百分比。 |
| $WallClockSeconds |hello 耗用的秒數。 |
| $MemoryBytes |hello 平均 mb 數使用。 |
| $DiskBytes |hello 平均 gb 數 hello 本機磁碟上使用。 |
| $DiskReadBytes |hello 讀取的位元組數目。 |
| $DiskWriteBytes |hello 寫入的位元組數目。 |
| $DiskReadOps |執行 hello 讀取的磁碟操作次數。 |
| $DiskWriteOps |執行的寫入磁碟作業的 hello 計數。 |
| $NetworkInBytes |hello 輸入位元組數。 |
| $NetworkOutBytes |hello 輸出的位元組數目。 |
| $SampleNodeCount |hello 的運算節點的計數。 |
| $ActiveTasks |hello 準備 tooexecute 但還未執行的工作數目。 hello $ActiveTasks 計數包含 hello 作用中狀態以及已滿足其相依性的所有工作。 Hello 作用中狀態，但未滿足其相依性的工作會排除 hello $ActiveTasks 計數。|
| $RunningTasks |hello 處於執行中狀態的工作數目。 |
| $PendingTasks |$ActiveTasks 和 $RunningTasks hello 總和。 |
| $SucceededTasks |hello 已順利完成的工作數目。 |
| $FailedTasks |hello 失敗的工作數目。 |
| $CurrentDedicatedNodes |hello 目前數目專用計算節點。 |
| $CurrentLowPriorityNodes |hello 目前數目低優先順序的計算節點，包括任何已插播的節點。 |
| $PreemptedNodeCount | hello hello 集區中就會處於插播的節點數目。 |

> [!TIP]
> hello hello 上表所示的唯讀、 服務定義的變數是*物件*tooaccess 每個相關聯的資料提供各種方法。 如需詳細資訊，請參閱本文稍後的[取得範例資料](#getsampledata)。
>
>

## <a name="types"></a>類型
公式中支援以下類型：

* double
* doubleVec
* doubleVecList
* 字串
* 時間戳記-時間戳記是一種複合結構包含下列成員的 hello:

  * 年
  * month (1-12)
  * day (1-31)
  * 週間日 (hello 格式的數字，例如，1 代表星期一)
  * hour (以 24 小時制數字格式表示，例如 13 代表下午 1:00)
  * minute (00-59)
  * second (00-59)
* timeinterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>作業
列出 hello 前一節中的 hello 類型都允許這些作業。

| 作業 | 支援的運算子 | 結果類型 |
| --- | --- | --- |
| double 運算子  double |+、-、*、/ |double |
| double 運算子  timeinterval |* |timeinterval |
| doubleVec 運算子  double |+、-、*、/ |doubleVec |
| doubleVec 運算子  doubleVec |+、-、*、/ |doubleVec |
| timeinterval 運算子  double |*、/ |timeinterval |
| timeinterval 運算子  timeinterval |+、- |timeinterval |
| timeinterval 運算子  timestamp |+ |timestamp |
| timestamp 運算子  timeinterval |+ |timestamp |
| timestamp  timestamp |- |timeinterval |
| double |-、! |double |
| timeinterval |- |timeinterval |
| double 運算子  double |<、<=、==、>=、>、!= |double |
| string  string |<、<=、==、>=、>、!= |double |
| timestamp  timestamp |<、<=、==、>=、>、!= |double |
| timeinterval 運算子  timeinterval |<、<=、==、>=、>、!= |double |
| double 運算子  double |&&, &#124;&#124; |double |

測試具有三元運算子的雙精準數 (`double ? statement1 : statement2`) 時，非零為 **true**，而零則為 **false**。

## <a name="functions"></a>Functions
這些預先定義**函式**可供您 toouse 定義自動調整公式。

| 函式 | 傳回類型 | 說明 |
| --- | --- | --- |
| avg(doubleVecList) |double |傳回 hello hello doubleVecList 中所有值的平均值。 |
| len(doubleVecList) |double |傳回 hello 從 hello doubleVecList 建立 hello 向量的長度。 |
| lg(double) |double |傳回 hello 記錄檔基底 2 的 hello double。 |
| lg(doubleVecList) |doubleVec |會傳回基底 2 的 hello doubleVecList hello component-wise 記錄檔。 Hello 參數必須明確傳遞 vec(double)。 否則，會假定 hello double lg （double） 版本。 |
| ln(double) |double |傳回 hello hello double 的自然對數。 |
| ln(doubleVecList) |doubleVec |會傳回基底 2 的 hello doubleVecList hello component-wise 記錄檔。 Hello 參數必須明確傳遞 vec(double)。 否則，會假定 hello double lg （double） 版本。 |
| log(double) |double |傳回 hello 記錄 10 為底數 hello double。 |
| log(doubleVecList) |doubleVec |傳回 hello component-wise 記錄 hello doubleVecList 的基底 10。 Vec(double) hello 單一 double 參數必須明確地傳遞。 否則，會假定 hello double log(double) 版本。 |
| max(doubleVecList) |double |傳回 hello hello doubleVecList 中的最大值。 |
| min(doubleVecList) |double |傳回 hello hello doubleVecList 中的最小值。 |
| norm(doubleVecList) |double |傳回 hello 2 範數從 hello doubleVecList 建立的 hello 向量。 |
| percentile(doubleVec v, double p) |double |傳回 hello hello 向量 v 的百分位數元素。 |
| rand() |double |傳回介於 0.0 到 1.0 之間的隨機值。 |
| range(doubleVecList) |double |傳回 hello doubleVecList 中的 hello hello 最小和最大值之間的差異。 |
| std(doubleVecList) |double |傳回 hello hello doubleVecList 中的 hello 值的樣本標準差。 |
| stop() | |停止 hello 自動調整運算式的評估。 |
| sum(doubleVecList) |double |傳回 hello 的 hello doubleVecList 的所有 hello 元件的總和。 |
| time(string dateTime="") |timestamp |如果沒有參數傳遞，或 hello hello dateTime 字串的時間戳記，如果它通過，傳回 hello 時間戳記的 hello 目前時間。 支援的 dateTime 格式為 W3C-DTF 和 RFC 1123。 |
| val(doubleVec v, double i) |double |傳回 hello hello 元素位於位置 i 向量 v 中以零起始索引值。 |

一些 hello 上表所述的 hello 函式可接受清單做為引數。 hello 以逗號分隔清單是任何組合*double*和*doubleVec*。 例如：

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

hello *doubleVecList*值是單一轉換的 tooa *doubleVec*之前評估。 例如，如果`v = [1,2,3]`，然後呼叫`avg(v)`是相等的 toocalling `avg(1,2,3)`。 呼叫`avg(v, 7)`是相等的 toocalling `avg(1,2,3,7)`。

## <a name="getsampledata"></a>取得樣本資料
自動調整公式會作用於 hello 批次服務所提供的度量資料 （範例）。 公式成長或壓縮根據 hello 值，它會從 hello 服務取得的集區大小。 hello 服務定義的變數所描述的先前是提供各種方法 tooaccess 資料，該物件相關聯的物件。 例如，hello 下列運算式會顯示要求 tooget hello 的 CPU 使用量的前五分鐘：

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| 方法 | 說明 |
| --- | --- |
| GetSample() |hello`GetSample()`方法傳回的資料樣本的向量。<br/><br/>一個樣本有 30 秒的度量資料。 換句話說，每隔 30 秒會取得範例。 但是，如以下所述，沒有收集樣本時與時使用 tooa 公式之間的延遲。 因此，並非一段指定時間內的所有樣本都可供公式評估。<ul><li>`doubleVec GetSample(double count)`<br/>指定 hello 範例 tooobtain hello 所收集的最新樣本數目。<br/><br/>`GetSample(1)`傳回 hello 最後一個可用的範例。 針對度量類似`$CPUPercent`，不過，這應該不能因為它是不可能 tooknow*時*收集 hello 樣本。 此範例可能是最新的，也可能因為系統問題，是更舊的。 最好是在這種情況下 toouse 如下所示的時間間隔。<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>指定收集樣本資料的時間範圍。 （選擇性），它也指定 hello 百分比的 hello 中必須有的範例要求的時間範圍。<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`如果 hello 過去 10 分鐘內的所有範例都都存在於 hello CPUPercent 歷程記錄時，就會傳回 20 的範例。 如果 hello 過去一分鐘的記錄無法使用，不過，只有 18 箱範例則會傳回。 在此案例中：<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`就會失敗，因為只有 90%的 hello 範例可供使用。<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` 會成功。<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>指定收集資料的時間範圍 (含開始時間和結束時間)。<br/><br/>如上面所述，沒有收集樣本時與時使用 tooa 公式之間的延遲。 請考慮此延遲時間，當您使用 hello`GetSample`方法。 請參閱下文中的 `GetSamplePercent`。 |
| GetSamplePeriod() |傳回 hello 的期間所執行的範例中的歷程記錄的範例資料集。 |
| Count() |傳回 hello hello 度量歷程記錄中的樣本總數。 |
| HistoryBeginTime() |傳回 hello hello 最早可用的資料範例 hello 度量的時間戳記。 |
| GetSamplePercent() |傳回 hello 百分比在指定的時間間隔內所提供的範例。 例如：<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>因為 hello`GetSample`方法失敗的傳回的樣本 hello 百分比是否小於 hello`samplePercent`指定，您可以使用 hello`GetSamplePercent`方法 toocheck 第一次。 然後您可以執行替代的動作，如果沒有足夠的樣本不存在，而不暫停 hello 自動縮放評估。 |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>範例、 範例百分比和 hello *GetSample()*方法
自動調整公式 hello 核心作業 tooobtain 工作和資源計量資料，然後再調整集區的大小，根據該資料。 因此，很重要的 toohave 清楚了解如何自動調整公式互動度量資料 （範例）。

**範例**

hello 批次服務會定期接受的工作和資源度量的範例，並使其可用 tooyour 自動調整公式。 這些範例 hello 批次服務會記錄每隔 30 秒。 不過，則通常延遲之間時記錄這些樣本數，且它們可供使用太 （且可讀取） 時，自動調整公式。 此外，由於 toovarious 因素，例如網路或其他基礎結構問題，範例就不會記錄特定的間隔。

**樣本百分比**

當`samplePercent`傳遞 toohello`GetSample()`方法或 hello`GetSamplePercent()`呼叫方法時，_百分比_參考 tooa hello 可能的樣本總數 hello 批次服務所記錄的比較和hello 是可用 tooyour 自動調整公式的樣本數目。

讓我們以 10 分鐘的時間範圍為例。 範例會記錄在 10 分鐘的時間範圍內每隔 30 秒，因為 hello 最大的樣本總數所記錄的批次，就會是 20 範例 (每分鐘 2)。 不過，由於 toohello 固有延遲的 hello 報告機制，並在 Azure 中的其他問題，可能有只 15 會讀取可用 tooyour 自動調整公式的範例。 因此，比方說，該 10 分鐘期間內，只有 75%的 hello 樣本總數記錄可能是可用 tooyour 公式。

**GetSample() 和樣本範圍**

自動調整公式會進行 toobe 擴張和縮小您的集區&mdash;加入節點或移除節點。 因為節點需付費，您會想 tooensure 公式使用一種智慧型的足夠資料為基礎的分析方法。 因此，建議您在公式中使用趨勢類型分析。 此類型會根據所收集樣本的範圍來擴大和縮減集區。

因此，使用 toodo `GetSample(interval look-back start, interval look-back end)` tooreturn 向量的範例：

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

批次所評估 hello 線條上方時，它會傳回範圍的範例為值的向量。 例如：

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

一旦您已收集的樣本 hello 向量，您可以使用函式，例如`min()`， `max()`，和`avg()`tooderive 有意義的值從 hello 收集的範圍。

為了增加安全性，您可以強制公式評估 toofail 如果某個範例百分比小於可用的特定時間週期。 當您強制評估公式 toofail 時，您可以指示批次 toocease 進一步評估 hello 公式如果 hello 指定百分比的樣本就無法使用。 在此情況下，不會變更 toohello 集區大小。 toospecify 的 hello 評估 toosucceed，如範例所需的百分比指定它，如太 hello 第三個參數`GetSample()`。 以下指定了 75% 的樣本需求：

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

因為範例可用性可能會有延遲，務必 tooalways 指定時間範圍超過一分鐘的外觀後開始時間。 花費大約一分鐘的 hello 範圍中的範例 toopropagate 透過 hello 系統，因此範例`(0 * TimeInterval_Second, 60 * TimeInterval_Second)`可能無法使用。 同樣地，您可以使用 hello 百分比參數`GetSample()`tooforce 特定範例百分比需求。

> [!IMPORTANT]
> 我們**強烈建議**您***避免「只」*`GetSample(1)`依賴自動調整公式中的** 。 這是因為`GetSample(1)`基本上是說： toohello 批次服務，「 讓我 hello 最後一個範例，無論擷取多久以前。 」 由於它是單一樣本，而且可能是較舊的範例，它可能無法代表 hello 放大圖片的最新的工作或資源狀態。 如果您使用`GetSample(1)`，請確定它是較大的陳述式的一部分，並不 hello 公式依賴資料點。
>
>

## <a name="metrics"></a>度量
您可以在定義公式時使用資源和工作計量。 您調整專用的節點，根據 hello 度量資料所取得，並評估 hello 集區中的 hello 目標數目。 請參閱 hello[變數](#variables)節，如需有關每個度量。

<table>
  <tr>
    <th>計量</th>
    <th>說明</th>
  </tr>
  <tr>
    <td><b>Resource</b></td>
    <td><p>資源計量根據 hello CPU、 hello 頻寬、 hello 的運算節點的記憶體使用量和 hello 的節點數目。</p>
        <p> 這些服務定義的變數適合用於根據節點計數進行調整：</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>這些服務定義的變數適合用於根據節點資源使用量進行調整：</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Task</b></td>
    <td><p>工作度量資訊為基礎的工作，例如作用中的 hello 狀態暫止狀態，且在完成。 hello 下列服務定義的變數可用於進行根據工作度量的集區大小調整：</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>撰寫自動調整公式
您藉由形成使用 hello 元件，上面的陳述式來建置自動調整公式，然後合併這些陳述式完成公式。 在本節中，我們會建立可以執行一些真實世界調整決策的範例自動調整公式。

首先，讓我們來定義新的自動調整公式的 hello 需求。 應該 hello 公式：

1. 如果 CPU 使用率偏高，請增加集區中的專用的運算節點的 hello 目標數目。
2. CPU 使用率較低時，請減少集區中的專用的運算節點的 hello 目標數目。
3. 永遠限制 hello too400 專用的節點數目上限。

在高 CPU 使用量，節點的 tooincrease hello 數目定義填入使用者定義變數的 hello 陳述式 (`$totalDedicatedNodes`) 的值，如果是 110%的 hello 目標的目前專用節點數目，但僅限於 hello 最小值的平均 CPU 使用量期間 hello 過去 10 分鐘內為百分之 70。 否則，請使用 hello 值 hello 目前專用的節點數目。

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

太*減少*hello 低 CPU 使用率在專用的節點數目，在我們的公式集 hello 的下一個陳述式相同的 hello`$totalDedicatedNodes`變數 too90 百分比的專用的節點，如果 hello hello 目前目標數目的平均 CPU 使用量在 hello 過去的 60 分鐘底下是 20%。 否則，請使用 hello 目前值`$totalDedicatedNodes`我們 hello 上面的陳述式中擴展。

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

現在限制專用的運算節點 tooa 最大值為 400 hello 目標數目：

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

以下是 hello 完整的公式：

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>使用 .NET 建立已啟用自動調整的集區

toocreate 在.NET 中，啟用自動調整集區，請遵循下列步驟：

1. 建立具有 hello 集區[BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool)。
2. 設定 hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled)屬性太`true`。
3. 設定 hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula)具有自動調整公式的內容。
4. （選擇性）設定 hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval)屬性 （預設為 15 分鐘）。
5. 認可 hello 集區與[CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit)或[CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync)。

hello 下列程式碼片段會建立啟用自動調整集區在.NET 中。 hello 集區的自動調整公式集 hello 目標數目，從星期一，專用的節點 too5 和 1 hello 當週的一天。 hello[自動調整間隔](#automatic-scaling-interval)是設定 too30 分鐘。 在此與其他 C# 程式碼片段在本文中的 hello `myBatchClient` hello 的正確初始化執行個體[BatchClient] [ net_batchclient]類別。

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> 當您建立啟用自動調整集區時，請勿指定 hello _targetDedicatedComputeNodes_參數或 hello _targetLowPriorityComputeNodes_ hello 參數呼叫太**CreatePool**。 請改為指定 hello **AutoScaleEnabled**和**AutoScaleFormula** hello 集區上的屬性。 這些屬性的 hello 值決定每個節點類型的 hello 目標數目。 另外，toomanually 調整啟用自動調整集區 (比方說，使用[BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync])、 第一個**停用**上的自動調整hello 集區，然後調整其大小。
>
>

此外 tooBatch.NET 中，您可以使用任何其他 hello[批次 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development)，[批次 REST](https://docs.microsoft.com/rest/api/batchservice/)，[批次的 PowerShell cmdlet](batch-powershell-cmdlets-get-started.md)，和 hello[批次 CLI](batch-cli-get-started.md)tooconfigure 自動調整。


### <a name="automatic-scaling-interval"></a>自動調整間隔
根據預設，hello 批次服務會調整集區的大小根據 tooits 自動調整公式每隔 15 分鐘。 此間隔是可設定使用下列屬性集區的 hello:

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)

hello 最小間隔為 5 分鐘，並 hello 最大值為 168 小時。 如果指定的間隔，在這個範圍之外，hello 批次服務會傳回不正確的要求 (400) 錯誤。

> [!NOTE]
> 自動調整在少於一分鐘內，不是目前預期的 toorespond toochanges 但而不是為您執行工作負載時逐漸適合 tooadjust hello 大小的集區。
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>在現有集區啟用自動調整

每個批次 SDK 提供方式 tooenable 自動調整。 例如：

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)
* [在自動調整中啟用集區][rest_enableautoscale] (REST API)

當您啟用自動調整現有的集區上時，請遵循點注意 hello:

* 如果自動調整為目前已停用 hello 集區上發出 hello 要求 tooenable 自動調整時，您必須指定有效的自動調整公式，當發出 hello 要求。 您可以選擇性地指定自動調整評估間隔。 如果您未指定間隔，則會使用 hello 預設值 15 分鐘。
* 如果目前 hello 集區上啟用自動調整規模，您可以指定自動調整公式、 評估間隔，或兩者。 您必須至少指定其中一個屬性。

  * 如果您指定新的自動調整規模評估間隔，然後 hello 現有評估排程就會停止並啟動新的排程。 hello 新排程的開始時間是哪些 hello 要求 tooenable 自動調整的發出 hello 時間。
  * 如果您省略任一 hello 自動調整公式或評估間隔，hello 批次服務會繼續 toouse hello 目前的設定值。

> [!NOTE]
> 如果您指定的值為 hello *targetDedicatedComputeNodes*或*targetLowPriorityComputeNodes* hello 參數**CreatePool**方法，當您建立 hello評估 hello 自動調整公式時，會忽略在.NET 中，或另一種語言，則這些值中的 hello 比較參數集區。
>
>

此 C# 程式碼片段會使用 hello[批次.NET] [ net_api]現有集區上的 [程式庫 tooenable 自動調整：

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>更新自動調整公式

現有啟用自動調整集區上，呼叫 hello 作業 tooenable 自動調整一次與 hello 新公式 tooupdate hello 公式。 例如，如果已啟用自動調整`myexistingpool`hello 下列.NET 程式碼執行時，其自動調整公式會取代 hello 內容`myNewFormula`。

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>更新 hello 自動調整間隔

tooupdate hello 自動調整規模評估間隔的現有啟用自動調整集區，呼叫 hello 作業 tooenable 自動調整一次與 hello 新的間隔。 例如，tooset hello 自動調整規模評估間隔 too60 分鐘數已在.NET 中啟用自動調整集區：

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>評估自動調整公式

您可以評估公式之後才套用 tooa 集區。 如此一來，您可以測試 hello 公式 toosee hello 公式進入生產環境之前，其陳述式如何評估。

tooevaluate 自動調整公式，您必須先啟用 hello 與有效的公式的集區上的自動調整。 啟用 tootest 上還沒有自動調整集區的公式，使用 hello 一行公式`$TargetDedicatedNodes = 0`當您第一次啟用自動調整。 然後，使用其中一種 hello 下列想 tootest tooevaluate hello 公式：

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 或 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    這些批次.NET 方法需要現有的集區和包含 hello 自動調整公式 tooevaluate 字串 hello 識別碼。

* [評估自動調整公式](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    在 REST API 要求中，指定在 hello URI 中的 hello 集區識別碼和 hello hello 中的自動調整公式*autoScaleFormula* hello 要求本文的元素。 hello 回應 hello 作業包含可能是相關的 toohello 公式任何錯誤資訊。

在這個 [Batch .NET][net_api] 程式碼片段中，我們會評估自動調整公式。 如果 hello 集區並沒有啟用自動調整，我們先將啟用它。

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

成功評估 hello 這個程式碼片段所示的公式會產生類似的結果：

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>取得自動調整執行的相關資訊

預期 tooensure 做為執行您的公式，我們建議您定期查看 hello hello 自動調整執行批次執行您的集區的結果。 toodo，get （或重新整理） 參考 toohello 集區，並檢查其執行的最後一個自動調整規模的 hello 屬性。

在批次.NET hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun)屬性具有可提供 hello 最新自動調整規模資訊 hello 集區執行執行數個屬性：

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

在 hello REST API，hello[取得集區的相關資訊](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool)要求傳回 hello 集區，其中包括 hello 最新自動縮放比例在 hello 中執行資訊的相關資訊[autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun)屬性。

hello 下列 C# 程式碼片段會使用 hello 批次.NET 程式庫 tooprint 相關資訊 hello 最後一個自動調整集區執行_myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

上述程式碼片段的 hello 範例輸出：

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>自動調整公式範例
讓我們看看顯示不同的方式 tooadjust hello 數量的計算資源集區中的幾個公式。

### <a name="example-1-time-based-adjustment"></a>範例 1：以時間為基礎的調整
假設您想要根據 hello hello 週間日和時間 tooadjust hello 集區大小。 這個範例會示範如何 tooincrease 或減少 hello 中節點數目 hello 集據以區。

hello 公式會先取得 hello 目前的時間。 如果它是一週工作日期 (1-5) 和工作小時內 (上午 8 點 too6 PM)，設定 too20 節點 hello 目標集區大小。 否則，它已設定 too10 節點。

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>範例 2：以工作為基礎的調整
在此範例中，hello 集區大小是根據調整 hello hello 佇列中的工作數目。 公式字串中接受註解和換行。

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>範例 3：考量平行工作
這個範例會調整 hello 工作數目為基礎的 hello 集區大小。 這個公式也會列入帳戶 hello [MaxTasksPerComputeNode] [ net_maxtasks] hello 集區已設定的值。 已在集區上啟用[平行工作執行](batch-parallel-node-tasks.md)的情況下，這個方法很有用。

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>範例 4：設定初始集區大小
此範例顯示 C# 程式碼片段，以設定自動調整公式 hello 集區大小 tooa 第一段時間針對指定節點的數目。 然後它就會調整根據執行的 hello 數目 hello 集區的大小並經過 hello 初始時間週期之後，作用中工作。

在下列程式碼片段的 hello hello 公式：

* 設定 hello 初始集區大小 toofour 節點。
* 不需要調整 hello 集區的大小內 hello hello 集區的生命週期的第一個 10 分鐘。
* 在 10 分鐘之後, 會取得 hello 最大值內 hello 工作執行的數字和作用中的 hello 過去 60 分鐘的時間。
  * 如果這兩個值是 0 （表示中的任何工作已執行或作用中的 hello 過去的 60 分鐘），hello 集區大小是設定 too0。
  * 如果其中一個值大於零，則不進行任何變更。

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>後續步驟
* [Azure Batch 計算資源使用率與並行節點工作最大化](batch-parallel-node-tasks.md)包含有關如何您可以執行多個工作同時在集區中的 hello 計算節點上的詳細資料。 此外 tooautoscaling，這項功能可能有助於 toolower 某些工作負載，節省您的工作持續時間。
* 另一個的效率提升器，請確定您的批次應用程式查詢 hello hello 大部分的最佳方式中的批次服務。 請參閱[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)toolearn toolimit hello 跨越 hello 網路時，查詢可能數千個 hello 狀態的資料數量如何計算節點或工作。

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
