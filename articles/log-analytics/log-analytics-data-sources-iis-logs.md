---
title: "Log Analytics 中的 IIS 記錄檔 | Microsoft Docs"
description: "Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  本文說明如何設定收集 IIS 記錄檔，以及它們在 OMS 儲存機制中建立的記錄詳細資料。"
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
ms.openlocfilehash: 2114bdafb3b9fe2eb0632271840b8b70a76d10f1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="iis-logs-in-log-analytics"></a>Log Analytics 中的 IIS 記錄檔
Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  

![IIS 記錄檔](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>設定 IIS 記錄檔
Log Analytics 會從 IIS 建立的記錄檔收集項目，因此您必須[設定 IIS 記錄](https://technet.microsoft.com/library/hh831775.aspx)。

Log Analytics 只支援以 W3C 格式儲存的 IIS 記錄檔，不支援自訂欄位或 IIS 進階記錄。  
Log Analytics 不會收集 NCSA 或 IIS 原生格式的記錄。

從 [Log Analytics [設定] 中的 [資料] 功能表](log-analytics-data-sources.md#configuring-data-sources)來設定 Log Analytics 中的 IIS 記錄檔。  您只需選取 [Collect W3C format IIS log files]\(收集 W3C 格式的 IIS 記錄檔) 即可完成設定。

當您啟用 IIS 記錄檔收集時，建議您在每部伺服器上設定 IIS 記錄檔換用設定。

## <a name="data-collection"></a>資料收集
Log Analytics 會從每個連接的來源收集 IIS 記錄檔項目，間隔大約為每 15 分鐘。  代理程式會在它收集的每個事件記錄檔中記錄它的位置。  如果代理程式離線，Log Analytics 會從上次離開的地方收集事件，即使這些事件是在代理程式離線時所建立亦同。

## <a name="iis-log-record-properties"></a>IIS 記錄檔記錄屬性
IIS 記錄檔記錄都具有 **W3CIISLog** 類型以及下表中的屬性：

| 屬性 | 說明 |
|:--- |:--- |
| 電腦 |收集事件的來源電腦名稱。 |
| cIP |用戶端的 IP 位址。 |
| csMethod |要求的方法，例如 GET 或 POST。 |
| csReferer |使用者連結至目前網站的來源網站。 |
| csUserAgent |用戶端的瀏覽器類型。 |
| csUserName |存取伺服器之已驗證的使用者名稱。 匿名使用者會以連字號表示。 |
| csUriStem |要求的目標，例如網頁。 |
| csUriQuery |用戶端正在嘗試執行的查詢 (如果有的話)。 |
| ManagementGroupName |Operations Manager 代理程式的管理群組名稱。  若為其他代理程式，此為 AOI-\<工作區 ID\> |
| RemoteIPCountry |用戶端 IP 位址的國家/地區。 |
| RemoteIPLatitude |用戶端 IP 位址的緯度。 |
| RemoteIPLongitude |用戶端 IP 位址的經度。 |
| scStatus |HTTP 狀態碼。 |
| scSubStatus |子狀態錯誤碼。 |
| scWin32Status |Windows 狀態碼。 |
| sIP |Web 伺服器的 IP 位址。 |
| SourceSystem |OpsMgr |
| sPort |用戶端連接之伺服器上的連接埠。 |
| sSiteName |IIS 網站名稱。 |
| TimeGenerated |記錄項目的日期和時間。 |
| TimeTaken |處理要求的時間長度 (以毫秒為單位)。 |

## <a name="log-searches-with-iis-logs"></a>使用 IIS 記錄檔的記錄搜尋
下表提供擷取 IIS 記錄檔記錄的不同記錄查詢範例。

| 查詢 | 說明 |
|:--- |:--- |
| Type=W3CIISLog |所有 IIS 記錄檔記錄。 |
| Type=W3CIISLog scStatus=500 |具有傳回狀態 500 的所有 IIS 記錄。 |
| Type=W3CIISLog &#124; Measure count() by cIP |依據用戶端 IP 位址的 IIS 記錄項目計數。 |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |依據主機 www.contoso.com 之 URL 的 IIS 記錄項目計數。 |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |每部 IIS 電腦所接收的位元組總數。 |

>[!NOTE]
> 如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。

> | 查詢 | 說明 |
|:--- |:--- |
| W3CIISLog |所有 IIS 記錄檔記錄。 |
| W3CIISLog &#124; where scStatus==500 |具有傳回狀態 500 的所有 IIS 記錄。 |
| W3CIISLog &#124; summarize count() by cIP |依據用戶端 IP 位址的 IIS 記錄項目計數。 |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |依據主機 www.contoso.com 之 URL 的 IIS 記錄項目計數。 |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |每部 IIS 電腦所接收的位元組總數。 |

## <a name="next-steps"></a>後續步驟
* 設定 Log Analytics 以收集其他 [資料來源](log-analytics-data-sources.md) 進行分析。
* 了解 [記錄檔搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。
* 設定 Log Analytics 中的警示，以主動通知您在 IIS 記錄檔中找到的重要狀況。
