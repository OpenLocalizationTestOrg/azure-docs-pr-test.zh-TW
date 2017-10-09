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
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="b9879-104">設定 Azure 串流分析工作的警示</span><span class="sxs-lookup"><span data-stu-id="b9879-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="b9879-105">簡介：監視頁面</span><span class="sxs-lookup"><span data-stu-id="b9879-105">Introduction: Monitor page</span></span>
<span data-ttu-id="b9879-106">您可以設定警示 tootrigger 警示時度量達到您所指定的條件。</span><span class="sxs-lookup"><span data-stu-id="b9879-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="b9879-107">比方說，您可能設定的警示類似 hello 下列條件：</span><span class="sxs-lookup"><span data-stu-id="b9879-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="b9879-108">規則可透過 hello 入口網站中，度量上設定，或者也可以設定[以程式設計方式](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a)作業記錄資料。</span><span class="sxs-lookup"><span data-stu-id="b9879-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="b9879-109">設定在 hello Azure 入口網站中的警示</span><span class="sxs-lookup"><span data-stu-id="b9879-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="b9879-110">在 hello Azure 入口網站，開啟您要的警示 toocreate hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="b9879-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="b9879-111">在 hello**作業**刀鋒視窗中，按一下 hello**監視**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b9879-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="b9879-112">在 hello**度量**刀鋒視窗中，按一下 hello**新增警示**命令。</span><span class="sxs-lookup"><span data-stu-id="b9879-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Azure 入口網站設定](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="b9879-114">輸入名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="b9879-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="b9879-115">使用 hello 選取器 toodefine hello 條件下哪些 hello 會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="b9879-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="b9879-116">提供有關應 hello 警示資訊。</span><span class="sxs-lookup"><span data-stu-id="b9879-116">Provide information about where hello alert should go.</span></span>

      ![設定 Azure 串流分析作業的警示](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="b9879-118">如需在 hello Azure 入口網站中設定警示的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b9879-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="b9879-119">取得說明</span><span class="sxs-lookup"><span data-stu-id="b9879-119">Get help</span></span>
<span data-ttu-id="b9879-120">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b9879-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9879-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9879-121">Next steps</span></span>
* [<span data-ttu-id="b9879-122">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="b9879-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b9879-123">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b9879-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="b9879-124">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="b9879-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b9879-125">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="b9879-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b9879-126">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="b9879-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

