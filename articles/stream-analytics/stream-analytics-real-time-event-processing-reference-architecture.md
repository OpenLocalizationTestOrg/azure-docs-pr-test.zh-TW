---
title: "處理資料流分析的事件處理 aaaReal 時間事件 |Microsoft 文件"
description: "了解一組 Azure 服務可如何交互操作以啟用即時事件處理與分析。"
keywords: "即時處理, 事件處理, 參考架構"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>參考架構：使用 Microsoft Azure 串流分析的即時事件處理
使用 Azure Stream Analytics 處理即時事件的 hello 參考架構是預定的 tooprovide 部署即時平台即服務 (PaaS) 資料流處理解決方案使用 Microsoft Azure 的泛型藍圖。

## <a name="summary"></a>摘要
傳統上，分析解決方案已根據擁有功能，例如 ETL （擷取、 轉換、 載入） 和資料倉儲資料的預存的先前 tooanalysis 所在。 多變的需求，包括更多快速抵達的資料，會將此現有的模型 toohello 限制推送。 hello 能力 tooanalyze 資料內移動資料流之前 toostorage 是一種解決方案，而且不是一項新功能，而 hello 方法已不被廣泛採用跨所有產業有關。 

Microsoft Azure 提供分析技術的全面目錄，可以支援一系列不同的解決方案案例和要求。 選取的端對端方案的 Azure 服務 toodeploy 可以 hello 廣度的供應項目是項挑戰。 這份文件設計的 toodescribe hello 功能並不互通的 hello 支援事件資料流的解決方案的各種 Azure 服務。 它也會說明一些 hello 案例，客戶可以受益此類型的方法。

## <a name="contents"></a>內容
* 執行摘要
* 簡介 tooReal 時間分析
* 在 Azure 中的即時資料價值定位
* 即時分析的常見案例
* 架構與元件
  * 資料來源
  * 資料整合層
  * 即時分析層
  * 資料儲存層
  * 展示/使用層
* 結論

**作者：** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation

**發行日期：** 2015 年 1 月

**修訂版本：** 1.0

**下載：** [使用 Microsoft Azure 串流分析的即時事件處理](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

