---
title: "aaaAzure Mobile Engagement 實作遊戲應用程式"
description: "遊戲應用程式案例 tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>對遊戲應用程式實作 Mobile Engagement
## <a name="overview"></a>Overview
某家新創遊戲公司推出了一款新的釣魚角色扮演/策略遊戲應用程式。 6 個月已啟動並執行 hello 遊戲。 這個遊戲是大型成功時，它有數百萬個下載且 hello 保留是非常高的比較的 tooother 啟動遊戲應用程式。 在 hello 每季檢閱會議，專案關係人同意 tooincrease 每位使用者 (ARPU) 的平均營收。 他們在遊戲中提供高階套件做為特殊優惠。 這些遊戲的組件可讓使用者 tooupgrade hello 外觀和效能其釣魚線條和 lures 或 tackles hello 遊戲中。 不過，這些套件的銷售成績非常差。 因此他們決定第一個 tooanalyze hello 客戶體驗的分析工具，而且然後 toodevelop engagement 程式 tooincrease 銷售使用進階分割。

根據 hello [Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)他們建置 engagement 策略。

## <a name="objectives-and-kpis"></a>目標和 KPI
符合索引鍵的專案關係人 hello 遊戲。 所有同意上一個主要目標-15%tooincrease premium 封裝銷售。 他們建立商務關鍵效能指標 (Kpi) toomeasure 和磁碟機此目標

* 這些封裝購買 hello 遊戲的層級上？
* 每個使用者、 每個工作階段、 每週和每個月的 hello 營收是什麼？
* Hello 最愛的採購類型為何？

第 1 部分 hello[入門指南](mobile-engagement-getting-started-best-practices.md)說明如何 toodefine hello 目標和 Kpi。 

現在已經定義了商務 Kpi hello，hello Mobile 產品 Manager 建立 Engagement Kpi toodetermine 新使用者趨勢和保留。

* 監視保留，並使用跨 hello 下列間隔： 每日、 每 2 天、 週、 每月和每 3 個月
* 活躍使用者人數
* 儲存在 hello hello 應用程式分級

根據從 hello IT 團隊的建議，下列技術 Kpi hello 已加入 tooanswer hello 下列問題：

* 我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)
* 每個工作階段發生當機或錯誤的次數
* 我的使用者執行哪些作業系統版本？
* Hello 畫面的 我的使用者的平均大小為何？
* 我的使用者擁有哪種網際網路連線？

針對每一個 KPI hello 行動產品管理員會指定需要而且會位於她腳本中的 hello 資料。

## <a name="engagement-program-and-integration"></a>業務開發計劃和整合
之前建立進階的 engagement 程式，負責 hello 專案 hello 行動專案導向器應該先深入了解如何及何時 hello 使用者所使用的產品。

3 個月後 hello 行動專案導向器收集的足夠資料 tooenhance 他在應用程式的推播通知銷售。 他發現到：

* hello 第一個訂單通常會發生在 hello 層級 14。 90%，這種情況下，針對 hello 採購是 $3 新傳奇武器。
* 在 80%的這種情況下，使用者已購買與 hello 產品繼續並讓多個購買。
* 使用者已通過 hello 層級 20，請啟動 toospend 多個 $10/週。
* 使用者通常 toobuy premium 封裝層級 16、 24 及 32。

謝謝 hello 行動專案導向器決定 toocreate 特定的推播通知的應用程式銷售的序列 tooincrease toothis 分析。 他建立了三個他稱為「歡迎計劃」、「銷售計劃」和「無活動計劃」的推播順序。 如需詳細資訊，請參閱 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
