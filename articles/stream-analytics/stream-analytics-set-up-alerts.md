---
title: "Stream Analytics 中查詢的警示 aaaSet |Microsoft 文件"
description: "了解串流分析警示"
keywords: "設定警示"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>設定 Azure 串流分析工作的警示
## <a name="introduction-monitor-page"></a>簡介：監視頁面
您可以設定警示 tootrigger 警示時度量達到您所指定的條件。 比方說，您可能設定的警示類似 hello 下列條件：

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

規則可透過 hello 入口網站中，度量上設定，或者也可以設定[以程式設計方式](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a)作業記錄資料。

## <a name="set-up-alerts-in-hello-azure-portal"></a>設定在 hello Azure 入口網站中的警示
1. 在 hello Azure 入口網站，開啟您要的警示 toocreate hello 資料流分析工作。 

2. 在 hello**作業**刀鋒視窗中，按一下 hello**監視**> 一節。  

3. 在 hello**度量**刀鋒視窗中，按一下 hello**新增警示**命令。

      ![Azure 入口網站設定](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. 輸入名稱和描述。

5. 使用 hello 選取器 toodefine hello 條件下哪些 hello 會傳送警示。

6. 提供有關應 hello 警示資訊。

      ![設定 Azure 串流分析作業的警示](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

如需在 hello Azure 入口網站中設定警示的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。  


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-get-started.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

