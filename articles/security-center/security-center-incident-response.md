---
title: "與 Azure 資訊安全中心 aaaRespond toosecurity 事件 |Microsoft 文件"
description: "本文件說明如何 toouse Azure 安全性中心的事件回應案例。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>使用 Azure 資訊安全中心進行事件回應
許多組織了解如何 toorespond toosecurity 事件之後，才遭受攻擊。 tooreduce 成本和損害，很重要 toohave 之前攻擊會發生事件的回應計劃中的地方。 您可以在不同階段的事件回應使用 Azure 資訊安全中心。

## <a name="incident-response-planning"></a>事件回應計劃
三個的核心功能的有效計劃而定： 所能 tooprotect，偵測，並回應 toothreats。 保護是防止的事件，是關於早期識別威脅的偵測和回應收回 hello 攻擊者，以及還原系統 toomitigate hello 影響有入侵。

此發行項將會使用從 hello hello 安全性事件回應階段[hello 雲端中的 Microsoft Azure 安全性回應](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678)文章 hello 下列圖表所示：

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig1.png)

您可以使用資訊安全中心階段 hello 偵測、 評估和診斷。 以下是範例的如何資訊安全中心功能非常適合在 hello 三個初始事件回應階段期間：

* **偵測**： 檢閱 hello 事件進行調查，第一個指示。
  * 範例： 檢閱 hello 初始驗證的高安全性警示發生 hello 資訊安全中心儀表板中。
* **評估**： 執行 hello 初始評估 tooobtain hello 可疑活動的詳細資訊。
  * 範例： 取得 hello 安全性警示的詳細資訊。
* **診斷**︰進行技術性調查，並找出圍堵、緩和及因應策略。
  * 範例： 請遵循 hello 補救步驟的資訊安全中心述該特定安全性警示。

hello 案例，如下所示顯示您如何 tooleverage 資訊安全中心期間 hello 偵測、 評估，並診斷/回應安全性事件的階段。 在資訊安全中心內，[安全性事件](security-center-incident.md)是符合[攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)模式之資源的所有警示彙總。 事件會出現在 hello[安全性警示](security-center-managing-and-responding-alerts.md)磚和刀鋒視窗。 事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。 資訊安全中心也會提供獨立安全性警示，它也可以使用的 tootrack 關閉可疑的活動。

## <a name="scenario"></a>案例
Contoso 最近移轉某些其內部部署資源 tooAzure，包括一些虛擬機器為基礎的業務工作負載和 SQL 資料庫。 Contoso 的核心電腦安全性事件回應小組 (CSIRT) 目前因為尚未整合與其目前事件回應工具的安全性情報，而無法順利調查安全性問題。 這種欠缺整合期間 hello 偵測階段 （太多誤判），以及評估 hello 和診斷階段期間，也會發生問題。 做為此移轉一部分，其決定 tooopt 中的資訊安全中心 toohelp 它們解決這個問題。

onboarded hello 後第一階段中完成這個移轉的所有資源，並解決所有 hello 資訊安全中心的安全性建議事項。 Contoso CSIRT 是 hello 掌管電腦安全性事件的處理。 hello 小組一群人負責處理任何安全性事件所組成。 hello 小組成員已清楚定義責任 tooensure 保持回應的任何區域未涵蓋範圍。

為了 hello 這種情況下，我們會 toofocus 上的下列角色，屬於 Contoso CSIRT hello hello 角色：

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Judy 負責安全性作業。 她的職責包括︰

* 監視及回應 hello 時鐘周圍 toosecurity 威脅。
* 擴大 toohello 雲端工作負載擁有者或安全性分析師所需。

Sam 是安全性分析師，他的職責包括︰

* 調查攻擊。
* 修復警示。
* 使用工作負載擁有者 toodetermine 並套用防護功能。

如您所見，Judy 與 Sam 有不同的責任，以及必須一起運作 tooshare 資訊安全中心資訊。

## <a name="recommended-solution"></a>建議的解決方案
由於 Judy 與 Sam 有不同的角色，他們將日常活動的使用資訊安全中心 tooobtain 相關資訊的不同區域。 Judy 會在其日常監視中使用 [安全性警示]。

![安全性警示](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Judy 將 hello 偵測和評估階段期間使用安全性警示。 Judy hello 初始評估完成時，她可能會提升 hello 問題 tooSam 是否需要進一步調查。 此時，Sam 將使用 hello 已提供的資訊安全中心，有時搭配其他資料來源，toomove toohello 診斷階段。

## <a name="how-tooimplement-this-solution"></a>如何 tooimplement 此解決方案
toosee 如何在事件回應案例中，您會使用 Azure 資訊安全中心，我們將在 hello 偵測與評估階段中，請遵循 Judy 的步驟，然後就會看到 Sam 用途 toodiagnose hello 問題。

### <a name="detect-and-assess-incident-response-stages"></a>偵測和評估事件回應階段
Judy 登入 toohello Azure 入口網站，並在 hello 資訊安全中心主控台中正常運作。 監視活動其每日的一部分，她開始檢閱執行警示 hello 步驟的高安全性：

1. 按一下 hello**安全性警示**磚和存取 hello**安全性警示**刀鋒視窗。
    ![安全性警示刀鋒視窗](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > 為了 hello 這種情況下，Judy 是進行 tooperform hello 惡意 SQL 活動警示，請評估 hello 前圖所示。
   >
   >
2. 按一下 hello**惡意 SQL 活動**警示，並檢閱 hello 中的 hello 攻擊資源**惡意 SQL 活動**刀鋒視窗：![事件詳細資料](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    在這個刀鋒視窗中，Judy 可以記下 hello 遭受攻擊的資源，如何多次這種攻擊發生，而且當它偵測到。
3. 按一下 hello**攻擊資源**tooobtain 這種攻擊的詳細資訊。

閱讀後 hello 描述，會將 Judy 相信這不是誤判和她應該擴大此案例 tooSam。

### <a name="diagnose-incident-response-stage"></a>診斷事件回應階段
Sam Judy 從收到 hello 案例，並啟動 檢閱建議的資訊安全中心的 hello 修復步驟。

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>其他資源
hello 事件回應小組也可以利用的 hello[安全性中心 Power BI](security-center-powerbi.md)功能 toosee 不同類型的報表。 這些報告可以協助他們進一步調查 toovisualize 期間、 分析和篩選器的建議和安全性警示。 對公司來說，在 hello 調查程序時使用其安全性資訊和事件管理 (SIEM) 解決方案，他們也可以[整合與解決方案的資訊安全中心](security-center-integrating-alerts-with-log-integration.md)。 您也可以使用 hello 整合 Azure 稽核記錄檔和虛擬機器 (VM) 的安全性事件[Azure 記錄檔整合工具](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/)。 tooinvestigate 攻擊，您可以使用這項資訊搭配 hello 資訊安全中心提供。

## <a name="conclusion"></a>結論
事件發生之前，執行組合小組是非常重要的 tooyour 組織和正面影響事件的處理方式。 Hello 適當的工具 toomonitor 資源可協助此小組 tootake 精確步驟 tooremediate 安全性事件。 資訊安全中心[偵測功能](security-center-detection-capabilities.md)可以協助 IT tooquickly 回應 toosecurity 事件並修復安全性問題。
