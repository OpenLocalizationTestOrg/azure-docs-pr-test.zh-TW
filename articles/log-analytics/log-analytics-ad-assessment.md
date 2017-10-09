---
title: "aaaOptimize Active Directory 環境與 Azure Log Analytics |Microsoft 文件"
description: "您可以使用 Active Directory 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>最佳化您的 Active Directory 環境，以 hello Active Directory 評估記錄分析解決方案

![AD 評定符號](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

您可以使用 Active Directory 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。 這篇文章可協助您安裝及使用 hello 解決方案，讓您可以採取修正動作，可能的問題。

此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。 hello 建議是跨四個焦點區域，幫助您快速了解 hello 風險並採取動作分類。

hello 建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。 每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。

您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。

焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **AD 評估**hello 基礎結構，您的環境中的儀表板。 hello 下列各節說明如何 toouse hello 有關 hello **AD 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 Active Directory 伺服器基礎結構。

![SQL 評估磚的影像](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 解決方案。

* 必須是評估 hello 網域 toobe 的成員的網域控制站上安裝代理程式。
* 解決方案需要.NET Framework 4 的支援的版本的 Active Directory 評估 hello (4.5.2 或更新版本) 內含的 OMS 代理程式的每部電腦上安裝。
* 新增 hello Active Directory 評估解決方案 tooyour OMS 工作區從[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。  不需要進一步的組態。

  > [!NOTE]
  > 您加入 hello 方案之後，hello AdvisorAssessment.exe 檔案加入 tooservers 與代理程式。 讀取組態資料及傳送 toohello OMS 服務進行處理的 hello 雲端中。 邏輯是套用的 toohello 接收資料，而 hello 雲端服務會記錄 hello 資料。
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Active Directory 評估資料收集詳細資訊

Active Directory 評估收集資料，從下列來源使用您已啟用的 hello 代理程式的 hello:

- 登錄收集器
- LDAP 收集器
- .NET Framework
- 事件記錄檔收集器
- Active Directory 服務介面 (ADSI)
- Windows PowerShell
- 檔案資料收集器
- Windows Management Instrumentation (WMI)
- DCDIAG 工具 API
- 檔案複寫服務 (NTFRS) API
- 自訂 C# 程式碼


hello 下表顯示資料收集方法，代理程式是否 Operations Manager (SCOM) 為必要項，以及如何通常資料會收集代理程式。

| 平台 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 天 |

## <a name="understanding-how-recommendations-are-prioritized"></a>了解建議的排列方式
每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。 只有 hello 10 最重要的建議會出現。

### <a name="how-weights-are-calculated"></a>加權的計算方式
加權是彙集以下三個重要因素的值：

* hello*機率*識別問題會造成問題。 較高的機率等同 tooa 的整體分數較 hello 建議。
* hello*影響*hello 問題如果確實引發問題對您組織。 較高的影響等同 tooa 的整體分數較 hello 建議。
* hello*投入時間*需要 tooimplement hello 建議。 勞力較高 tooa 整體分數較低的 hello 建議。

每個建議的加權 hello hello 總分每個焦點區域的百分比表示。 例如，如果 hello 安全性和相容性的焦點區域建議的分數為 5%，實作該項建議會增加您整體安全性和法規遵循分數 5%。

### <a name="focus-areas"></a>焦點區域
**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。

**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。

**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。

**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 Active Directory tooyour 現有基礎結構。

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>您的目標應該 tooscore 100%中每個焦點區域？
不一定。 hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。 不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。 例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。 對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。 重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。 您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。

每項建議都包含其重要性的指引。 您應該使用此指南 tooevaluate 是否實作 hello 建議適用於您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質。

## <a name="use-assessment-focus-area-recommendations"></a>使用評估焦點區域建議
您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。 tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 安裝之後，您就可以使用 OMS hello 概觀 頁面上的 hello 評估磚來檢視建議 hello 摘要。

檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview 焦點區域，並採取修正動作的建議
1. 在 hello**概觀**頁面上，按一下 hello**評估**磚伺服器基礎結構。
2. 在 hello**評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。
3. 在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。 按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。  
    ![評估建議的影像](./media/log-analytics-ad-assessment/ad-focus.png)
4. 您可以採取 [建議動作] 中所建議的更正動作。 Hello 項目已獲得解決之後，已採取建議動作的更新評估記錄，並提高法務遵循分數。 更正後的項目將以**通過的物件**呈現。

## <a name="ignore-recommendations"></a>忽略建議
如果您有想 tooignore 的建議，您可以建立 OMS 將會使用您的評估結果中出現 tooprevent 建議的文字檔。

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>tooidentify，建議您將會忽略
1. 登入 tooyour 工作區，並開啟 記錄搜尋。 使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：![失敗的建議](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. 選擇您想 tooignore 的建議。 您會在 hello 下一個程序中使用 RecommendationId hello 值。

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate 及使用 IgnoreRecommendations.txt 文字檔
1. 建立名為 IgnoreRecommendations.txt 的檔案。
2. 貼上或輸入您想要記錄分析 tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。
3. 將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。
   * 以 hello Microsoft Monitoring Agent （直接或透過 Operations Manager 連線） 的電腦上*SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify 建議已忽略
Hello hello 下一個排程評估執行時，預設每隔 7 天之後, 指定的建議會標示*忽略*並不會出現在 hello 評估儀表板上。

1. 您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. 如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。

## <a name="ad-assessment-solutions-faq"></a>AD 評估方案常見問題集
*評估的執行頻率為何？*

* hello 評估每 7 天執行。

*有方法 tooconfigure 頻率 hello 評估執行嗎？*

* 目前沒有。

*如果我在加入評估方案後探索到另一部伺服器，方案也會評估這部伺服器嗎？*

* 是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。

*如果伺服器除役，何時將它會移除來自 hello 評估？*

* 如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。

*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？*

* AdvisorAssessment.exe

*如何花費時間的資料收集的 toobe？*

* hello hello 伺服器上的實際資料收集需費時約 1 小時。 對於擁有大量 Active Directory 伺服器的伺服器，資料收集可能需要花費更久的時間。

*有方法 tooconfigure 時收集資料嗎？*

* 目前沒有。

*為什麼只顯示 hello 前 10 項建議？*

* 與其提供鉅細靡遺的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。 解決後，智慧套件將會提供其他建議。 如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用記錄搜尋。

*是否有方法 tooignore 建議？*

* 是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 AD 評估資料和建議。
