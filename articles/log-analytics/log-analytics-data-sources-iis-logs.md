---
title: "記錄中記錄分析的 aaaIIS |Microsoft 文件"
description: "Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  這篇文章描述如何 tooconfigure 收集 IIS 記錄檔和詳細資料的 hello 記錄它們建立 hello OMS 儲存機制中。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Log Analytics 中的 IIS 記錄檔
Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  

![IIS 記錄檔](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>設定 IIS 記錄檔
Log Analytics 會從 IIS 建立的記錄檔收集項目，因此您必須[設定 IIS 記錄](https://technet.microsoft.com/library/hh831775.aspx)。

Log Analytics 只支援以 W3C 格式儲存的 IIS 記錄檔，不支援自訂欄位或 IIS 進階記錄。  
Log Analytics 不會收集 NCSA 或 IIS 原生格式的記錄。

設定 IIS 記錄檔中記錄分析，從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。  您只需選取 [Collect W3C format IIS log files]\(收集 W3C 格式的 IIS 記錄檔) 即可完成設定。

我們建議，當您啟用 IIS 記錄檔集合，您應該 hello IIS 記錄檔變換 設定每部伺服器上設定。

## <a name="data-collection"></a>資料收集
Log Analytics 會從每個連接的來源收集 IIS 記錄檔項目，間隔大約為每 15 分鐘。  hello 代理程式會收集每個事件記錄檔中記錄其所在位置。  如果 hello 代理程式離線，然後記錄分析會收集事件從上次停止的地方，即使這些事件在 hello agent 離線期間所建立。

## <a name="iis-log-record-properties"></a>IIS 記錄檔記錄屬性
IIS 記錄檔記錄有一種**W3CIISLog**和 hello 下表中都有 hello 屬性：

| 屬性 | 說明 |
|:--- |:--- |
| 電腦 |從收集 hello hello 事件的電腦名稱。 |
| cIP |Hello 用戶端 IP 位址。 |
| csMethod |Hello 要求，例如 GET 或 POST 方法。 |
| csReferer |站台的 hello 使用者接著再從 toohello 目前網站的連結。 |
| csUserAgent |Hello 用戶端瀏覽器類型。 |
| csUserName |Hello 名稱驗證的使用者存取 hello 伺服器。 匿名使用者會以連字號表示。 |
| csUriStem |例如，網頁的 hello 要求的目標。 |
| csUriQuery |查詢中，如果有的話，該 hello 用戶端已嘗試 tooperform。 |
| ManagementGroupName |Hello 管理群組的 Operations Manager 代理程式的名稱。  若為其他代理程式，此為 AOI-\<工作區 ID\> |
| RemoteIPCountry |國家/地區的 hello hello 用戶端 IP 位址。 |
| RemoteIPLatitude |Hello 用戶端 IP 位址的緯度。 |
| RemoteIPLongitude |Hello 用戶端 IP 位址的經度。 |
| scStatus |HTTP 狀態碼。 |
| scSubStatus |子狀態錯誤碼。 |
| scWin32Status |Windows 狀態碼。 |
| sIP |Hello web 伺服器的 IP 位址。 |
| SourceSystem |OpsMgr |
| sPort |Hello 伺服器 hello 用戶端上的連接埠連接到。 |
| sSiteName |Hello IIS 站台名稱。 |
| TimeGenerated |已記錄的日期和時間的 hello 項目。 |
| TimeTaken |以毫秒為單位，要求的時間 tooprocess hello 長度。 |

## <a name="log-searches-with-iis-logs"></a>使用 IIS 記錄檔的記錄搜尋
hello 下表提供不同的擷取 IIS 記錄檔記錄的記錄檔查詢的範例。

| 查詢 | 說明 |
|:--- |:--- |
| Type=W3CIISLog |所有 IIS 記錄檔記錄。 |
| Type=W3CIISLog scStatus=500 |具有傳回狀態 500 的所有 IIS 記錄。 |
| Type=W3CIISLog &#124; Measure count() by cIP |依據用戶端 IP 位址的 IIS 記錄項目計數。 |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |計數的 IIS 記錄 url hello 主機 www.contoso.com 的項目。 |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |每部 IIS 電腦所接收的位元組總數。 |

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> | 查詢 | 說明 |
|:--- |:--- |
| W3CIISLog |所有 IIS 記錄檔記錄。 |
| W3CIISLog &#124; where scStatus==500 |具有傳回狀態 500 的所有 IIS 記錄。 |
| W3CIISLog &#124; summarize count() by cIP |依據用戶端 IP 位址的 IIS 記錄項目計數。 |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |計數的 IIS 記錄 url hello 主機 www.contoso.com 的項目。 |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |每部 IIS 電腦所接收的位元組總數。 |

## <a name="next-steps"></a>後續步驟
* 設定記錄分析 toocollect 其他[資料來源](log-analytics-data-sources.md)進行分析。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。
* 設定警示 tooproactively 通知您重要的條件，IIS 記錄檔中找到的記錄分析中。
