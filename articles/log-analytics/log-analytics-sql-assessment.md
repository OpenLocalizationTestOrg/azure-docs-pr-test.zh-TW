---
title: "aaaOptimize Azure 記錄分析 SQL Server 環境 |Microsoft 文件"
description: "Azure 記錄分析，您可以使用 hello SQL 評估解決方案 tooassess hello 風險和 SQL server 環境的健全狀況規則的間隔。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>最佳化 SQL Server 環境以 hello 記錄分析中的 SQL 評估解決方案

![SQL 評定符號](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

您可以使用 SQL 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。 本文將協助您安裝 hello 解決方案，讓您可以採取修正動作，可能的問題。

此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。 hello 建議是跨六個焦點領域，它們可以協助您快速了解 hello 風險並採取更正措施分類。

hello 所提供的建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。 每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。

您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。

焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **SQL 評估**hello 基礎結構，您的環境中的儀表板。 hello 下列各節說明如何 toouse hello 有關 hello **SQL 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 SQL server 基礎結構。

![SQL 評估磚的影像](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
SQL 評估適用於所有目前支援的 hello Standard、 Developer 和 Enterprise 版本的 SQL Server 版本。

使用下列資訊 tooinstall hello 並設定 hello 方案。

* 代理程式必須安裝於已安裝 SQL Server 的伺服器上。
* hello SQL 評估解決方案需要內含的 OMS 代理程式的每部電腦上安裝的.NET Framework 4 支援的版本。
* 在訂單 tooinstall hello 解決方案中，hello 使用者 Azure 訂用帳戶系統管理員或參與者 toohello 時必須使用 hello Azure 入口網站。 此外，hello 使用者必須是 hello OMS 工作區參與者或系統管理員角色 hello OMS 入口網站中的成員。
* 當使用 SQL 評估 hello Operations Manager 代理程式，您將需要 toouse Operations Manager Run-As 帳戶。 如需詳細資訊，請參閱底下的 [OMS 的 Operations Manager 執行身分帳戶](#operations-manager-run-as-accounts-for-oms) 。

  > [!NOTE]
  > hello MMA 代理程式不支援 Operations Manager Run-As 帳戶。
  >
  >
* 新增使用 hello 程序的 OMS 工作區中所述的 hello SQL 評估解決方案 tooyour [hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 不需要進一步的組態。

> [!NOTE]
> 您加入 hello 方案之後，hello AdvisorAssessment.exe 檔案加入 tooservers 與代理程式。 讀取組態資料及傳送 toohello OMS 服務進行處理的 hello 雲端中。 邏輯是套用的 toohello 接收資料，而 hello 雲端服務會記錄 hello 資料。

## <a name="sql-assessment-data-collection-details"></a>SQL 評估資料收集詳細資料
SQL 評估收集 WMI 資料、 登錄資料、 效能資料，以及使用您已啟用的 hello 代理程式的 SQL Server 動態管理檢視結果。

hello 下表顯示資料收集方法，代理程式是否 Operations Manager (SCOM) 為必要項，以及如何通常資料會收集代理程式。

| 平台 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 天 |

## <a name="operations-manager-run-as-accounts-for-oms"></a>OMS 的 Operations Manager 執行身分帳戶
在 OMS 中的記錄分析會使用 hello Operations Manager 代理程式和管理群組 toocollect，並傳送資料 toohello OMS 服務。 OMS 會在工作負載 tooprovide 的管理組件時建立具有附加價值的服務。 每個工作負載需要在不同的安全性內容中，例如網域帳戶的工作負載特定權限 toorun 管理組件。 您藉由設定 Operations Manager 執行身分帳戶需要 tooprovide 認證資訊。

使用下列資訊 tooset hello Operations Manager 執行身分帳戶的 SQL 評估 hello。

### <a name="set-hello-run-as-account-for-sql-assessment"></a>設定 hello 執行身分帳戶的 SQL 評估
 如果您已經在使用 hello SQL Server 管理組件，您應該使用該執行身分帳戶。

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>tooconfigure hello hello Operations 主控台中的 SQL 執行身分帳戶
> [!NOTE]
> 如果您使用 hello OMS 直接代理程式，而不是 hello SCOM 代理程式，hello 管理組件一律會 hello 的 hello 本機系統帳戶的安全性內容中執行。 略過步驟 1-5，並執行或是 hello T-SQL 或 Powershell 範例中，指定與 hello 使用者名稱的 NT AUTHORITY\SYSTEM。
>
>

1. 在 Operations Manager 中開啟 hello Operations 主控台，然後**管理**。
2. 在 [執行身分組態] 下方，按一下 [設定檔]，並開啟 [OMS SQL 評估執行身分設定檔]。
3. 在 hello**執行身分帳戶**頁面上，按一下**新增**。
4. 選取包含 SQL Server 所需的 hello 認證的 Windows 執行身分帳戶，或按一下**新增**toocreate 其中一個。

   > [!NOTE]
   > hello 執行身分帳戶類型必須是 Windows。 hello 執行身分帳戶也必須是裝載 SQL Server 執行個體的所有 Windows 伺服器上的本機系統管理員群組的一部分。
   >
   >
5. 按一下 [儲存] 。
6. 修改並執行下列 T-SQL 範例，在每個 SQL Server 執行個體 toogrant 最小權限需要 tooRun 身分帳戶 tooperform SQL 評估 hello。 不過，您不需要 toodo 這如果執行身分帳戶已是 SQL Server 執行個體上的 hello sysadmin 伺服器角色的一部分。

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>tooconfigure hello SQL 執行身分帳戶使用 Windows PowerShell
開啟 PowerShell 視窗並執行下列指令碼，在您已更新成您的資訊之後 hello:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>了解建議的排列方式
每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。 只有 hello 十個最重要的建議會出現。

### <a name="how-weights-are-calculated"></a>加權的計算方式
加權是彙集以下三個重要因素的值：

* hello*機率*識別之疑難引發問題。 較高的機率等同 tooa 的整體分數較 hello 建議。
* hello*影響*hello 問題如果確實引發問題對您組織。 較高的影響等同 tooa 的整體分數較 hello 建議。
* hello*投入時間*需要 tooimplement hello 建議。 勞力較高 tooa 整體分數較低的 hello 建議。

每個建議的加權 hello hello 總分每個焦點區域的百分比表示。 例如，如果 hello 安全性和相容性的焦點區域建議的分數為 5%，實作該項建議將會增加您整體安全性和法規遵循分數 5%。

### <a name="focus-areas"></a>焦點區域
**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。

**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。

**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。

**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 SQL Server tooyour 現有基礎結構。

**作業和監視**-這個焦點區域會顯示建議 toohelp 簡化 IT 作業，實作的預防性維護，並將效能最大化。

**變更和組態管理**-這個焦點區域會顯示建議 toohelp 保護日常作業，確定變更不產生負面影響您的基礎結構、 建立變更控制程序和 tootrack 稽核系統組態。

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>您的目標應該 tooscore 100%中每個焦點區域？
不一定。 hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。 不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。 例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。 對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。 重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。 您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。

每項建議都包含其重要性的指引。 您應該使用此指南 tooevaluate 是否實作 hello 建議適用於您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質。

## <a name="use-assessment-focus-area-recommendations"></a>使用評估焦點區域建議
您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。 tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 安裝之後，您可以使用 OMS hello 概觀 頁面上的 hello SQL 評估磚檢視建議 hello 摘要。

檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview 焦點區域，並採取修正動作的建議
1. 在 hello**概觀**頁面上，按一下 hello **SQL 評估**磚。
2. 在 hello **SQL 評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。
3. 在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。 按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。  
    ![SQL 評定建議圖片](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. 您可以採取 [建議動作] 中所建議的更正動作。 Hello 項目已獲得解決之後，後續評估會記錄的建議動作並提高法務遵循分數。 更正後的項目將以**通過的物件**呈現。

## <a name="ignore-recommendations"></a>忽略建議
如果您有想 tooignore 的建議，您可以建立 OMS 將會使用您的評估結果中出現 tooprevent 建議的文字檔。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>tooidentify，建議您將會忽略
1. 登入 tooyour 工作區，並開啟 記錄搜尋。 使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：![失敗的建議](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. 選擇您想 tooignore 的建議。 您會在 hello 下一個程序中使用 RecommendationId hello 值。

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate 及使用 IgnoreRecommendations.txt 文字檔
1. 建立名為 IgnoreRecommendations.txt 的檔案。
2. 貼上或輸入您要 OMS tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。
3. 將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。
   * 以 hello Microsoft Monitoring Agent （直接或透過 Operations Manager 連線） 的電腦上*SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify 建議已忽略
1. 執行下一個排程評估 hello，預設每隔 7 天之後, hello 指定建議會標示忽略，而且不會出現在 hello 評估儀表板上。
2. 您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. 如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。

## <a name="sql-assessment-solution-faq"></a>SQL 評估方案常見問題集
*評估的執行頻率為何？*

* hello 評估每 7 天執行。

*有方法 tooconfigure 頻率 hello 評估執行嗎？*

* 目前沒有。

*如果在我新增 hello SQL 評估解決方案之後探索到另一部伺服器，它會受到評估嗎？*

* 是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。

*如果伺服器除役，何時將它會移除來自 hello 評估？*

* 如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。

*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？*

* AdvisorAssessment.exe

*如何花費時間的資料收集的 toobe？*

* hello hello 伺服器上的實際資料收集需費時約 1 小時。 對於擁有大量 SQL 執行個體或資料庫的伺服器，資料收集可能需要花費更久的時間。

*收集的資料類型為何？*

* 收集下列類型的資料的 hello:
  * WMI
  * 登錄
  * 效能計數器
  * SQL 動態管理檢視 (DMV)。

*有方法 tooconfigure 時收集資料嗎？*

* 目前沒有。

*為什麼我必須 tooconfigure 執行身分帳戶？*

* 智慧套件會針對 SQL Server 執行少量的 SQL 查詢。 為了讓它們必須使用 toorun，執行身分帳戶與 VIEW SERVER STATE 權限 tooSQL。  此外，在訂單 tooquery WMI，就需要本機系統管理員認證。

*為什麼只顯示 hello 前 10 項建議？*

* 與其提供鉅細靡遺的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。 解決後，智慧套件將會提供其他建議。 如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用 hello OMS 記錄搜尋。

*是否有方法 tooignore 建議？*

* 是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。

## <a name="next-steps"></a>後續步驟
* [搜尋記錄](log-analytics-log-searches.md)tooview 詳細的 SQL 評估資料和建議。
