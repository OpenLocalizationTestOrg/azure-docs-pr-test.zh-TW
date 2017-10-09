---
title: "記錄分析 aaaAnalyze 資料使用量 |Microsoft 文件"
description: "使用多少資料正在傳送 toohello 記錄分析服務，及進行疑難排解，傳送大量資料的記錄分析 tooview hello 使用量儀表板。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>在 Log Analytics 中分析資料使用量
記錄分析包含 hello 收集的資料量，電腦會傳送 hello 資料和 hello 不同類型的資料傳送的資訊。  使用 hello**記錄分析使用量**儀表板 toosee hello 資料量傳送 toohello 記錄分析服務。 hello 儀表板顯示每個解決方案收集資料量和資料量您的電腦所傳送。

## <a name="understand-hello-usage-dashboard"></a>了解 hello 使用量儀表板
hello**記錄分析使用狀況**儀表板會顯示下列資訊的 hello:

- 資料量
    - 一段時間 (根據您目前的時間範圍) 的資料量
    - 依方案分類的資料量
    - 與電腦不相關的資料
- 電腦
    - 傳送資料的電腦
    - 過去 24 小時內沒有資料的電腦
- 供應項目
    - 深入解析和分析節點
    - 自動化和控制節點
    - 安全性節點
- 效能
    - 時間 toocollect 和索引的資料
- 查詢清單

![使用量儀表板](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork 與使用量資料
1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 訂用帳戶。
2. 在 hello**中樞**功能表上，按一下 [**更多服務**hello] 清單中的資源，在輸入**記錄分析**。 當您開始輸入 hello 清單會篩選根據您的輸入。 按一下 [Log Analytics]。  
    ![Azure 中樞](./media/log-analytics-usage/hub.png)
3. hello**記錄分析**儀表板會顯示您的工作區的清單。 選取工作區。
4. 在 hello*工作區*儀表板，按一下**記錄分析使用狀況**。
5. 在 hello**記錄分析使用量**儀表板，按一下**時間： 過去 24 小時**toochange hello 時間間隔。  
    ![時間間隔](./media/log-analytics-usage/time.png)
6. 檢視 hello 使用量類別刀鋒視窗的顯示區域您感興趣。 選擇在刀鋒視窗，然後按一下的 tooview 更多詳細資料中的項目[記錄搜尋](log-analytics-log-searches.md)。  
    ![範例資料使用量刀鋒視窗](./media/log-analytics-usage/blade.png)
7. Hello 記錄搜尋儀表板上檢閱 hello 結果所傳回的 hello 搜尋。  
    ![範例使用量記錄檔搜尋](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>當資料收集高於預期時建立警示
本章節描述如何 toocreate 警示時：
- 資料量超出指定的數量。
- 資料磁碟區是預測的 tooexceed 指定的數量。

Log Analytics [警示](log-analytics-alerts-creating.md)會使用搜尋查詢。 hello 下列查詢的結果沒有超過 100 GB hello 過去 24 小時所收集的資料時：

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

hello 下列查詢會使用簡單公式 toopredict 超過 100 GB 的資料會傳送一天中時： 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert 上不同的資料磁碟區，變更 hello 100 hello 查詢 toohello 您想要 tooalert GB 數。

使用中所述的 hello 步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)toobe 超過預期資料收集時收到通知。

在 24 小時內沒有超過 100 GB 的資料時，請建立 hello 警示 hello 第一個查詢，設定:
- **名稱**太*大於 24 小時內的 100 GB 資料磁碟區*
- **嚴重性**太*警告*
- **搜尋查詢**太`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **時間間隔**太*24 小時*。
- **警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。
- **產生警示根據**toobe*的結果數目*
- **結果數目**toobe*大於 0*

使用中所述的 hello 步驟[新增動作 tooalert 規則](log-analytics-alerts-actions.md)設定電子郵件、 webhook 或 runbook hello 警示規則的動作。

當 hello 第二個查詢建立 hello 警示時預測 24 小時內，將會超過 100 GB 資料的設定:
- **名稱**太*資料磁碟區中必須要有 100 GB 以上 toogreater 24 小時*
- **嚴重性**太*警告*
- **搜尋查詢**太`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **時間間隔**太*過去 3 小時內*。
- **警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。
- **產生警示根據**toobe*的結果數目*
- **結果數目**toobe*大於 0*

當您收到警示時，請使用下列區段 tootroubleshoot 為什麼使用量會超過預期的 hello hello 步驟。

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>針對使用量高於預期的原因進行疑難排解
hello 使用量儀表板可幫助您 tooidentify 為什麼使用量 （並因此成本） 高於您預期。

較高的使用量是由下列一個或兩個原因所造成：
- 超過預期傳送 tooLog 分析的資料
- 更多的節點比預期傳送資料 tooLog 分析

### <a name="check-if-there-is-more-data-than-expected"></a>檢查是否有比預期更多的資料 
有兩個主要區段 hello 方式 頁面，協助您識別造成大多數資料 toobe 收集的 hello。

hello*經過一段時間的資料量*圖表可顯示 hello 總傳送的資料量和 hello 電腦傳送 hello 大部分的資料。 hello hello 頂端的圖表可讓您 toosee 如果整體資料使用量成長，剩餘穩定或遞減。 hello 的電腦清單會顯示 hello 10 電腦傳送嗨大部分的資料。

hello*解決方案的資料量*圖表可顯示 hello 磁碟區的每個方案和大部分的資料傳送嗨 hello 解決方案所傳送的資料。 在 hello 最上方的 hello 圖表可顯示 hello 總每個方案所傳送的一段時間的資料量。 這項資訊可讓您 tooidentify 是否方案傳送的 hello 相同數量的資料，或小於資料一段時間相關的詳細資料。 解決方案 hello 清單顯示 hello 10 解決方案傳送嗨大部分的資料。 

這兩個圖表顯示了所有資料。 某些資料已可計費，其他資料則為免費。 只在資料也會列入計費上, toofocus 修改 hello 搜尋頁面 tooinclude hello 查詢`IsBillable=true`。  

![資料量圖表](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

查看 hello*經過一段時間的資料量*圖表。 toosee hello 方案及傳送 hello 的特定電腦，大部分資料的資料型別按一下 hello hello 電腦名稱。 按一下 hello 的 hello hello 清單中的第一部電腦的名稱。

在下列螢幕擷取畫面的 hello，hello*記錄管理 / 效能*資料型別傳送 hello hello 電腦大部分的資料。 

![電腦的資料磁碟區](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

接下來，請返回 toohello*使用量*儀表板並查看 hello*解決方案的資料量*圖表。 hello hello 清單中的 hello 方案名稱按一下 toosee hello 電腦傳送嗨解決方案，大部分的資料。 按一下 hello hello hello 清單中的第一個方案名稱。 

在下列螢幕擷取畫面的 hello，它會確認該 hello *acmetomcat*電腦傳送嗨 hello 記錄管理解決方案的大部分資料。

![解決方案的資料量](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

如有需要請執行其他分析 tooidentify 大型磁碟區中的方案或資料類型。 查詢範例包括：

+ **安全性**解決方案
  - `Type=SecurityEvent | measure count() by EventID`
+ **記錄管理**解決方案
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ **Perf** 資料類型
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ **Event** 資料類型
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ **Syslog** 資料類型
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ **AzureDiagnostics** 資料類型
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

使用下列步驟 tooreduce hello 磁碟區的記錄檔收集 hello:

| 高資料量的來源 | 如何 tooreduce 資料磁碟區 |
| -------------------------- | ------------------------- |
| 安全性事件            | 選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) <br> 變更 hello 安全性稽核原則只需要 toocollect 事件。 特別是，檢閱 hello 需要 toocollect 事件 <br> - [a稽核篩選平台](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [稽核登錄](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [稽核檔案系統](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [稽核核心物件](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [稽核控制代碼操作](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [稽核抽取式存放裝置 ](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| 效能計數器       | 變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)以： <br> -減少收集頻率 hello <br> - 減少效能計數器的數目 |
| 事件記錄檔                 | 變更[事件記錄組態](log-analytics-data-sources-windows-events.md)以： <br> -Hello 的減少所收集的事件記錄檔 <br> - 只收集必要的事件層級。 例如，不要收集「資訊」層級事件 |
| syslog                     | 變更 [Syslog 組態](log-analytics-data-sources-syslog.md)以： <br> -減少收集設備的 hello 數目 <br> - 只收集必要的事件層級。 例如，不要收集「資訊」和「偵錯」層級事件 |
| AzureDiagnostics           | 變更資源記錄集合： <br> -Hello 的減少資源傳送記錄檔 tooLog 分析 <br> - 只收集必要的記錄 |
| 不需要 hello 解決方案的電腦中的方案資料 | 使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦。 |

### <a name="check-if-there-are-more-nodes-than-expected"></a>檢查是否有比預期更多的節點
如果您在 hello*每個節點 (OMS)*定價層，然後向您收費根據 hello 數目節點和您使用的方案。 您可以看到 hello 中正使用多少個節點的每個優惠*供應項目*hello 使用量儀表板的區段。

![使用量儀表板](./media/log-analytics-usage/log-analytics-usage-offerings.png)

按一下**查看所有...** tooview hello 電腦的完整清單傳送 hello 選供應項目的資料。

使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦。


## <a name="next-steps"></a>後續步驟
* 請參閱[記錄中記錄分析搜尋](log-analytics-log-searches.md)toolearn toouse hello 如何搜尋語言。 您可以使用 搜尋查詢 tooperform 其他分析 hello 使用量資料。
* 使用中所述的 hello 步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)符合搜尋條件時收到通知的 toobe
* 使用[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)toocollect 資料只需要群組中的電腦
* 選取[一般或最小安全性事件](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)
* 變更[效能計數器組態](log-analytics-data-sources-performance-counters.md)
* 變更[事件記錄組態](log-analytics-data-sources-windows-events.md)
* 變更 [Syslog 組態](log-analytics-data-sources-syslog.md)
