---
title: "aaaAutoscaling 與 App Service 環境 v1"
description: "自動調整和 App Service 環境"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>自動調整和 App Service 環境 v1

> [!NOTE]
> 這篇文章是關於 hello App Service 環境 v1。  沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
> 

Azure App Service 環境支援「自動調整」 。 您可以根據度量或排程自動調整個別的背景工作集區。

![背景工作集區的自動調整選項。][intro]

自動調整資源使用率藉由最佳化自動成長和壓縮 App Service 環境 toofit 預算和/或載入設定檔。

## <a name="configure-worker-pool-autoscale"></a>設定背景工作集區自動調整
您可以存取 hello 自動調整規模功能從 hello**設定**hello 背景工作集區 索引標籤。

![Hello 背景工作集區的 [設定] 索引標籤。][settings-scale]

從該處，hello 介面應該相當熟悉，因為它是相同的體驗，您會看到當您調整應用程式服務計劃的 hello。 

![手動調整設定。][scale-manual]

您也可以設定自動調整設定檔。

![自動調整設定。][scale-profile]

自動調整規模設定檔是在您的標尺上的有用 tooset 限制。 如此一來，您可以同時藉由設定下限調整值 (1) 獲得一致的效能體驗和藉由設定上限 (2) 獲得可預測的資本支出。

![設定檔中的調整設定。][scale-profile2]

定義設定檔之後，您可以加入自動調整規模規則 tooscale 向上或向下 hello hello hello hello 設定檔所定義的範圍內的背景工作集區中的執行個體數目。 自動調整規則是以度量為基礎。

![調整規則。][scale-rule]

 任何背景工作集區或前端的度量可以使用的 toodefine 自動調整規模規則。 這些度量資訊是的 hello 的相同度量資訊，您可以在 hello 資源刀鋒視窗圖形中監視或設定警示。

## <a name="autoscale-example"></a>自動調整範例
App Service 環境的自動調整可使用逐步解說一個案例來加以說明。

這篇文章會說明所有 hello 需要考量，當您設定自動調整規模。 hello 文章會引導您進入互動播放時自動調整的因素在 App Service 環境中裝載的應用程式服務環境的 hello。

### <a name="scenario-introduction"></a>案例簡介
Frank 具有企業已移轉的一部分，他會管理 tooan App Service 環境的 hello 工作負載的 sysadmin 權限。

hello App Service 環境設定 toomanual 小數位數，如下所示：

* **前端：** 3
* **背景工作集區 1**：10
* **背景工作集區 2**：5
* **背景工作集區 3**：5

背景工作集區 1 是用於生產工作負載，而背景工作集區 2 和背景工作集區 3 用於品質保證 (QA) 及開發工作負載。

hello 應用程式服務計劃 QA 和開發人員設定 toomanual 小數位數。 hello 生產應用程式服務方案是設定與變化 tooautoscale toodeal 負載和流量。

Frank 是很熟悉 hello 應用程式。 他知道 hello 尖峰負載是上午 9:00 和下午 6:00 之間因為這是在 hello office 時，員工使用的特定業務 (LOB) 應用程式。 之後當使用者下班時，使用量便會下降。 非尖峰時間仍有某些負載因為使用者可以從遠端存取 hello 應用程式，使用其行動裝置或家用電腦。 hello 實際執行應用程式服務方案已設定 tooautoscale 根據 CPU 使用量，以 hello 下列規則：

![LOB 應用程式的特定設定。][asp-scale]

| **自動調整設定檔 - 工作日 - App Service 方案** | **自動調整設定檔 - 週末 - App Service 方案** |
| --- | --- |
| **名稱：** 工作日設定檔 |**名稱：** 週末設定檔 |
| **調整規模：** 排程和效能規則 |**調整規模：** 排程和效能規則 |
| **設定檔：** 工作日 |**設定檔：** 週末 |
| **類型：** 循環 |**類型：** 循環 |
| **以範圍為目標：** 5 too20 執行個體 |**以範圍為目標：** 3 too10 執行個體 |
| **星期幾：** 星期一、星期二、星期三、星期四、星期五 |**星期幾：** 星期六、星期日 |
| **開始時間︰** 上午 9:00 |**開始時間︰** 上午 9:00 |
| **時區：** UTC-08 |**時區：** UTC-08 |
|  | |
| **自動調整規則 (相應增加)** |**自動調整規則 (相應增加)** |
| **資源：** 生產環境 (App Service 環境) |**資源：** 生產環境 (App Service 環境) |
| **度量：** CPU % |**度量：** CPU % |
| **作業：** 大於 60% |**作業：** 大於 80% |
| **持續時間：** 5 分鐘 |**持續時間：** 10 分鐘 |
| **時間彙總：** 平均 |**時間彙總：** 平均 |
| **動作：** 計數增加 2 |**動作：** 計數增加 1 |
| **冷卻時間 (分鐘)：** 15 |**冷卻時間 (分鐘)：** 20 |
|  | |
| **自動調整規則 (相應減少)** |**自動調整規則 (相應減少)** |
| **資源：** 生產環境 (App Service 環境) |**資源：** 生產環境 (App Service 環境) |
| **度量：** CPU % |**度量：** CPU % |
| **作業：** 少於 30 % |**作業：** 少於 20 % |
| **持續時間：** 10 分鐘 |**持續時間：** 15 分鐘 |
| **時間彙總：** 平均 |**時間彙總：** 平均 |
| **動作：** 計數減少 1 |**動作：** 計數減少 1 |
| **冷卻時間 (分鐘)：** 20 |**冷卻時間 (分鐘)：** 10 |

### <a name="app-service-plan-inflation-rate"></a>App Service 方案擴大率
設定的 tooautoscale 應用程式服務計劃進行每小時的最大速率。 此速率可以是根據計算 hello hello 自動調整規模規則上所提供的值。

了解及計算 hello*應用程式服務計劃變大速率*很重要的 App Service 環境的自動調整規模，因為小數位數變更 tooa 背景工作集區不是瞬間完成。

hello 應用程式服務計劃變大率的計算方式如下：

![App Service 方案擴大率計算。][ASP-Inflation]

根據 hello 自動調整規模 – hello 週間日設定檔的 hello 生產應用程式服務方案的向外延展規則：

![根據「自動調整 - 相應增加」規則的工作日 App Service 方案擴大率。][Equation1]

在 hello 案例中的 hello 自動調整規模 – hello 週末設定檔的 hello 生產應用程式服務方案的向外延展規則 hello 公式會解析成：

![根據「自動調整 - 相應增加」規則的週末 App Service 方案擴大率。][Equation2]

此值也可以針對相應減少作業計算。

根據 hello 自動調整規模 – hello 週間日設定檔的 hello 生產應用程式服務方案的向下規則這看起來如下：

![根據「自動調整 - 相應減少」規則的工作日 App Service 方案擴大率。][Equation3]

在 hello 案例中的 hello 自動調整規模 – hello 週末設定檔的 hello 生產應用程式服務方案的向下規則 hello 公式會解析成：  

![根據「自動調整 - 相應減少」規則的週末 App Service 方案擴大率。][Equation4]

hello 生產應用程式服務方案所能成長的八個執行個體/小時 hello 週的最大速率和四個執行個體/小時 hello 週末期間。 它可以釋放執行個體的四個執行個體/小時 hello 週的最大速率和六個執行個體/小時在週末期間。

如果多個應用程式服務計劃裝載於背景工作集區，您必須 toocalculate hello*總擴大速率*所有 hello 應用程式服務計劃正在進行的 hello 擴大速率 hello 總和裝載該背景工作集區中。

![裝載於背景工作集區中的多個 App Service 方案的總擴大率計算。][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>使用 hello 應用程式服務計劃變大速率 toodefine 背景工作集區自動調整規模規則
背景工作集區設定的 tooautoscale 應用程式服務計劃要配置的緩衝區容量該主機。 hello 緩衝區可 hello 自動調整規模作業 toogrow，而且視壓縮應用程式服務方案。 hello 最小緩衝區是 hello 計算總應用程式服務計劃變大率。

由於 App Service 環境調整規模作業會花一些時間 tooapply，進一步指定縮放作業正在進行時可能發生的變更應該考量的任何變更。 tooaccommodate 這樣的延遲，我們建議您使用 hello 計算總應用程式服務計劃變大速率為 hello 加入每個自動調整規模作業的執行個體數目下限。

Frank 可使用這項資訊定義 hello 下列自動調整規模設定檔和規則：

![LOB 範例的自動調整設定檔規則。][Worker-Pool-Scale]

| **自動調整設定檔 - 工作日** | **自動調整設定檔 - 週末** |
| --- | --- |
| **名稱：** 工作日設定檔 |**名稱：** 週末設定檔 |
| **調整規模：** 排程和效能規則 |**調整規模：** 排程和效能規則 |
| **設定檔：** 工作日 |**設定檔：** 週末 |
| **類型：** 循環 |**類型：** 循環 |
| **以範圍為目標：** 13 too25 執行個體 |**以範圍為目標：** 6 too15 個執行個體 |
| **星期幾：** 星期一、星期二、星期三、星期四、星期五 |**星期幾：** 星期六、星期日 |
| **開始時間︰** 上午 7:00 |**開始時間︰** 上午 9:00 |
| **時區：** UTC-08 |**時區：** UTC-08 |
|  | |
| **自動調整規則 (相應增加)** |**自動調整規則 (相應增加)** |
| **資源：** 背景工作集區 1 |**資源：** 背景工作集區 1 |
| **度量：** WorkersAvailable |**度量：** WorkersAvailable |
| **作業：** 少於 8 |**作業：** 少於 3 |
| **持續時間：** 20 分鐘 |**持續時間：** 30 分鐘 |
| **時間彙總：** 平均 |**時間彙總：** 平均 |
| **動作：** 計數增加 8 |**動作：** 計數增加 3 |
| **冷卻時間 (分鐘)：** 180 |**冷卻時間 (分鐘)：** 180 |
|  | |
| **自動調整規則 (相應減少)** |**自動調整規則 (相應減少)** |
| **資源：** 背景工作集區 1 |**資源：** 背景工作集區 1 |
| **度量：** WorkersAvailable |**度量：** WorkersAvailable |
| **作業：** 大於 8 |**作業：** 大於 3 |
| **持續時間：** 20 分鐘 |**持續時間：** 15 分鐘 |
| **時間彙總：** 平均 |**時間彙總：** 平均 |
| **動作：** 計數減少 2 |**動作：** 計數減少 3 |
| **冷卻時間 (分鐘)：** 120 |**冷卻時間 (分鐘)：** 120 |

hello hello 設定檔中定義的目標範圍的計算方式 hello hello 應用程式服務方案的設定檔 + 緩衝區中定義的最小執行個體。

hello 最大範圍是裝載於 hello 背景工作集區的所有應用程式服務方案的 hello 最大範圍的 hello 總和。

hello hello 調整規則的增加計數應該組 tooat X 應用程式服務計劃變大速率，標尺的最少 1 組成。

減少計數可能都已調整的 toosomething 之間 1/2 X 或 1 X hello 標尺的應用程式服務計劃變大速率，向下。

### <a name="autoscale-for-front-end-pool"></a>前端集區的自動調整
前端自動調整規則比背景工作集區規則簡單。 您主要應該  
請確定 hello 測量與 hello cooldown 計時器的持續時間，考慮，App Service 方案上的調整規模作業不是瞬間完成。

此案例中，Frank 知道該 hello 錯誤速率增加之後前端達到 80%的 CPU 使用率，並設定 hello 自動調整規模規則 tooincrease 執行個體，如下所示：

![前端集區的自動調整設定。][Front-End-Scale]

| **自動調整設定檔 - 前端** |
| --- |
| **名稱：** 自動調整 - 前端 |
| **調整規模：** 排程和效能規則 |
| **設定檔：** 每日 |
| **類型：** 循環 |
| **以範圍為目標：** 3 too10 執行個體 |
| **星期幾：** 每日 |
| **開始時間︰** 上午 9:00 |
| **時區：** UTC-08 |
|  |
| **自動調整規則 (相應增加)** |
| **資源：** 前端集區 |
| **度量：** CPU % |
| **作業：** 大於 60% |
| **持續時間：** 20 分鐘 |
| **時間彙總：** 平均 |
| **動作：** 計數增加 3 |
| **冷卻時間 (分鐘)：** 120 |
|  |
| **自動調整規則 (相應減少)** |
| **資源：** 背景工作集區 1 |
| **度量：** CPU % |
| **作業：** 少於 30 % |
| **持續時間：** 20 分鐘 |
| **時間彙總：** 平均 |
| **動作：** 計數減少 3 |
| **冷卻時間 (分鐘)：** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
