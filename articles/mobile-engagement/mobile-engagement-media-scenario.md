---
title: "aaaAzure Mobile Engagement 應用程式的實作"
description: "媒體應用程式案例 tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>對媒體應用程式實作 Mobile Engagement
## <a name="overview"></a>Overview
John 是一家大型媒體公司的行動裝置專案經理。 他最近推出了一款新的應用程式，並獲得很高的下載次數。 他已達成預定的下載次數目標，但從每位使用者身上所獲得的投資回報 (ROI) 卻未達要求。 

John 已找到 ROI 太低的原因。 使用者經常在短短 2 週後就停止使用他的應用程式，而且大多不會再回頭使用。 他希望他的應用程式的 tooincrease hello 保留。

某些初始測試之後，他已取得他必須由他的使用者使用推播通知，他們傾向 toocontinue 使用他的應用程式。 也非使用中的使用者通常會傳回 toohello 根據他將傳送的通知的應用程式。 John 會決定 tooinvest 某種 Engagement 程式中的使用進階的目標使用推播通知其應用程式。

John 具有最近讀取 hello [Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)，決定 hello 指南 tooimplement hello 建議。

## <a name="objectives-and-kpis"></a>目標和 KPI
John 所推出的應用程式的重要關係人聚在一起。 當使用者使用他的媒體時，其中的廣告便會為他們帶來生意。 所以只要增加每位使用者使用的內容，John 就能增加營收。 所有同意上一個主要目標： tooincrease 銷售 25%的廣告。 他們建立商務關鍵效能指標 (Kpi) toomeasure 和磁碟機此目標

* 每位使用者點按的廣告數目
* (每位使用者/每個工作階段/每週/每月...) 瀏覽過多少文章頁面
* 最愛的類別有哪些

John 根據他與重要關係人的會面結果，定義了他的業務 KPI。 他會遵循 hello 的第 1 部分[Azure Mobile Engagement 入門指南最佳做法](mobile-engagement-getting-started-best-practices.md)。 

接下來，他會建立下列達到目標的 Engagement Kpi tooensure hello:

* 監視保留跨 hello 下列間隔： 每日、 每週、 隔週和每月。
* 活躍使用者人數
* 儲存在 hello 應用程式中的 hello 應用程式分級

根據從 hello IT 團隊的建議，下列技術 Kpi hello 已加入 tooanswer hello 下列問題：

* 我的使用者路徑為何 (所瀏覽的頁面、使用者在其中所花的時間長短)
* 每個工作階段發生當機或錯誤的次數？
* 我的使用者執行哪些作業系統版本？
* Hello 畫面的 我的使用者的平均大小為何？
* 我的使用者擁有哪種網際網路連線？

針對每一個 KPI，他複製 hello 資料所需的分類，他會加以記錄他腳本 hello 適當位置中。

## <a name="engagement-program-and-integration"></a>業務開發計劃和整合
現在 John 已定義好 KPI，於是他開始進行業務開發策略階段，他定義 4 個業務開發計劃和計劃目標：![][1]

然後 John 更進一步，詳細說明每個計劃的推播通知。 推播通知是由五個項目所定義而成：

1. 目標： hello hello 通知目標為何
2. 如何將到達 hello 目標
3. 目標： 將會收到 hello 通知的人員？
4. 何謂 hello 用語和 hello hello 通知 （在 App/Out 的應用程式） 格式的內容:
5. 當： 什麼是 hello 最佳時刻 toosend 此推播通知
   
    ![][2]

如需詳細資訊，請參閱 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)。

Toocollect 和寫入其標記共同計劃與 IT 小組 tooimplement hello 方案，請根據 toohello 第 2 部分的 hello John 會使用目標區段 toodefine 他有哪些資料的技術白皮書。 經過一星期的實作和使用者接受度測試後，John 終於可以啟動他的計劃。

## <a name="program-results"></a>計劃結果
四個月之後，John 檢閱計劃的成效。 hello  褖畫惎程式與 hello 每週程式達成其目標。 減少 hello 與只有一個工作階段的使用者數目、 hello 應用程式的多個功能的使用和 hello 每週的連線數目加倍。

hello**非作用中的程式**協助了解使用者勤者傾向 John。 它會顯示 hello 非作用中使用者的 15%回來 toohello 應用程式。 不過，這些人大多不會持續使用超過 1 個月。 John 預計在透過其他通知並擴大其內容的選擇性後，應該可以讓這個順序變成最好的情況。

hello**探索程式**不正常運作。 它就會增加交叉銷售，但沒有足夠 tooreach 他的目標。 John 會識別他不具有足夠資料 toomake 相關目標，並提議適當的內容。 於是他停止這個計劃，並將重心放在使用 Azure Mobile Engagement 傳送「評論推播通知」。 他記者已經 CMS 解決方案 toosend 推播通知，而且它們不想 toochange。

John 會決定 toouse hello 觸達 API 也就是 HTTP 的 REST API，可讓您管理觸達活動，而不需要 toouse AZME Web 介面。 透過這種方式 John 可以收集 hello 資料他需要並讓他的寫入器 tookeep 使用 hello CMS 解決方案。

正確功能如何運作的 tooensure，John 詢問 IT 小組 toobe 警覺 hello 遵循點上：

1. **作業系統**： 它們具有自己的規則 tooadministrate 推播通知 」，所以 John 決定 toolist 所有情況下，檢查是否 hello Api 處理它。
   例如： Android 推播系統可讓不是使用 iOS 的 hello 情況大圖片。
2. **時間範圍**: John 想要的 API，以設定 hello 的時間範圍，並設定結束 toocampaigns。 他想從任何具有干擾性通知擊 toopreserve 使用者。
3. **類別**：行銷小組準備了每種警示類型的範本。 John 會詢問 IT 小組 tooset 類別內 hello 應用程式開發介面。

在做過一些測試之後，John 感到非常滿意。 感謝您 toothis API，記者仍然可以傳送推播通知，以其 CMS 和 Azure Mobile Engagement 會為其收集行為的所有資料

在經過最初四個月後，所得到的結果顯示整體成效良好，這讓 John 和他的董事會成員深具信心，每個使用者的 ROI 增加 15%，行動銷售佔總銷售量 17.5%，僅僅四個月就增加了 7.5%。

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
