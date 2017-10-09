---
title: "aaaOptimize System Center Operations Manager 環境與 Azure Log Analytics |Microsoft 文件"
description: "您可以使用 hello 系統 Center Operations Manager 評估解決方案 tooassess hello 定期的風險和伺服器環境的健全狀況。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>利用 hello System Center Operations Manager 評估 （預覽） 解決方案最佳化環境

![System Center Operations Manager 評定符號](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

您可以使用 hello 系統 Center Operations Manager 評估解決方案 tooassess hello 風險和 System Center Operations Manager 伺服器環境的健全狀況規則的間隔。 這篇文章可協助您安裝、 設定和使用 hello 解決方案，讓您可以採取修正動作，可能的問題。

此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。 hello 建議是跨四個焦點區域，幫助您快速了解 hello 風險並採取更正措施分類。

hello 所提供的建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。 每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。

您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。

焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **System Center Operations Manager 評估**儀表板為您的基礎結構。 hello 下列各節說明如何 toouse hello 有關 hello **System Center Operations Manager 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 SCOM 基礎結構。

![System Center Operations Manager 解決方案圖格](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 評估儀表板](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案

hello 解決方案適用於 Microsoft System Operations Manager 2012 R2 和 2012 SP1。

使用下列資訊 tooinstall hello 並設定 hello 方案。

 - 您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。 安裝從 hello 解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview)或依照中的 hello 指示[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

 - 加入工作區中的方案 toohello hello 之後, hello hello 儀表板上的 System Center Operations Manager 評估磚會顯示 hello 額外的設定必要的訊息。 Hello 磚上按一下，然後遵循 hello 頁面中所述的 hello 設定步驟

 ![System Center Operations Manager 儀表板圖格](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Hello System Center Operations Manager 的設定可以透過 hello 指令碼，依照 hello hello 的 hello 在 OMS 中的方案組態 頁面中所述的步驟。

 相反地，透過 SCOM 主控台中，依照以下的 hello tooconfigure hello 評估中的步驟 hello 相同順序
1. [設定 System Center Operations Manager 評估 hello 執行身分帳戶](#operations-manager-run-as-accounts-for-oms)  
2. [設定 hello System Center Operations Manager 評估規則](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>收集 System Center Operations Manager 評定資料的詳細資料

System Center Operations Manager 評估 hello 收集 WMI 資料、 登錄資料、 事件記錄檔資料，透過 Windows PowerShell、 SQL 查詢、 使用您已啟用的 hello 伺服器的檔案資訊收集器的 Operations Manager 資料。

hello 下表顯示資料收集方法的 System Center Operations Manager 評估及頻率收集資料的代理程式。

| 平台 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | 7 天 |

## <a name="operations-manager-run-as-accounts-for-oms"></a>OMS 的 Operations Manager 執行身分帳戶

OMS 會建立工作負載 tooprovide 的管理組件具有附加價值的服務。 每個工作負載需要在不同的安全性內容中，例如網域帳戶的工作負載特定權限 toorun 管理組件。 設定 Operations Manager 執行身分帳戶 tooprovide 認證資訊。

使用下列資訊 tooset hello Operations Manager 執行身分帳戶的 System Center Operations Manager 評估 hello。

### <a name="set-hello-run-as-account"></a>設定 hello 執行身分帳戶

1. 在 [hello Operations Manager 主控台，移 toohello**管理**] 索引標籤。
2. 在 hello**執行身分設定**，按一下 **帳戶**。
3. 建立執行身分帳戶，遵循精靈中，建立 Windows 帳戶 hello hello。 hello 帳戶 toouse 是其中一個識別 hello 和具有下列所有 hello 必要條件：

    >[!NOTE]
    hello 執行身分帳戶必須符合下列需求：
    - Hello 環境 （所有 Operations Manager 角色的管理伺服器、 OpsMgr 資料庫、 資料倉儲、 報表、 Web 主控台、 閘道） 中的所有伺服器 hello 本機 Administrators 群組的網域帳戶成員
    - 要評估的 hello 管理群組的作業管理員 」 系統管理員角色
    - 執行 hello[指令碼](#sql-script-to-grant-granular-permissions-to-the-run-as-account)toogrant 細微的權限 toohello 帳戶，Operations Manager 所使用的 SQL 執行個體上。
      注意： 如果此帳戶已經有 sysadmin 權限，請略過 hello 指令碼執行。

4. 在 [散發安全性] 下，選取 [較安全]。
5. 指定 hello 管理伺服器 hello 帳戶發佈的位置。
3. 請返回 toohello 執行設定，並按一下**設定檔**。
4. 搜尋 hello *SCOM 評估設定檔*。
5. hello 設定檔名稱應該是： *Microsoft System Center Advisor SCOM 評估執行身分設定檔*。
6. 以滑鼠右鍵按一下並更新其屬性，新增 hello 最近建立執行身分帳戶為您在步驟 3 中建立。

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL 指令碼 toogrant 細微的權限 toohello 執行身分帳戶

執行下列 SQL 指令碼 toogrant 所需的權限 toohello 執行身分帳戶 hello Operations Manager 所使用的 SQL 執行個體上的 hello。

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>設定 hello 評估規則

hello 系統 Center Operations Manager 評估解決方案的管理組件包含名為的規則*Microsoft System Center Advisor SCOM 評估執行評估規則*。 此規則會負責執行 hello 評估。 tooenable hello 規則，並設定 hello 頻率，以下的使用 hello 程序。

根據預設，會停用 hello Microsoft System Center Advisor SCOM 評估執行評估規則。 toorun hello 評估，您必須啟用管理伺服器上的 hello 規則。 使用下列步驟的 hello。

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>啟用特定管理伺服器的 hello 規則

1. 在 hello**製作**工作區中的 hello Operations Manager 主控台中，搜尋 hello 規則*Microsoft System Center Advisor SCOM 評估執行評估規則*hello 中**規則**窗格。
2. 在 hello 搜尋結果中，選取 hello 包含 hello 文字*類型： 管理伺服器*。
3. Hello 規則上按一下滑鼠右鍵，然後按一下**會覆寫** > **類別的特定物件： 管理伺服器**。
4.  在 hello 可用的管理伺服器清單中，選取應在何處執行 hello 規則 hello 管理伺服器。
5.  請確定您也變更覆寫值**True** hello**啟用**參數值。  
    ![override parameter](./media/log-analytics-scom-assessment/rule.png)

雖然仍在這個視窗中，設定 hello 頻率的 hello 使用 hello 下一個程序執行。

#### <a name="configure-hello-run-frequency"></a>設定執行 hello 頻率

hello 評估是每個 10,080 分鐘 （或七天），設定的 toorun hello 預設間隔。 您可以覆寫 hello 值 tooa 最小值為 1440 分鐘 （或一天）。 hello 值代表執行後續評估之間所需的 hello 最小時間間隔。 使用下列的 hello 步驟 toooverride hello 間隔。

1. 在 hello**製作**工作區中的 hello Operations Manager 主控台中，搜尋 hello 規則*Microsoft System Center Advisor SCOM 評估執行評估規則*hello 中**規則**窗格。
2. 在 hello 搜尋結果中，選取 hello 包含 hello 文字*類型： 管理伺服器*。
3. Hello 規則上按一下滑鼠右鍵，然後按一下**覆寫 hello 規則** > **類別的所有物件： 管理伺服器**。
4. 變更 hello**間隔**參數值 tooyour 所需的時間間隔值。 在 hello 下列範例中，hello 值設定 too1440 分鐘 （1 天）。  
    ![interval parameter](./media/log-analytics-scom-assessment/interval.png)  
    如果設定 hello 值 tooless 1440 分鐘以上，hello 規則就會執行一天的間隔。 在此範例中，hello 規則會忽略 hello 間隔值，並執行一天的頻率。


## <a name="understanding-how-recommendations-are-prioritized"></a>了解建議的排列方式

每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。 只有 hello 10 最重要的建議會出現。

### <a name="how-weights-are-calculated"></a>加權的計算方式

加權是彙集以下三個重要因素的值：

- hello*機率*識別之疑難引發問題。 較高的機率等同 tooa 的整體分數較 hello 建議。
- hello*影響*hello 問題如果確實引發問題對您組織。 較高的影響等同 tooa 的整體分數較 hello 建議。
- hello*投入時間*需要 tooimplement hello 建議。 勞力較高 tooa 整體分數較低的 hello 建議。

每個建議的加權 hello hello 總分每個焦點區域的百分比表示。 例如，如果 hello 可用性和業務持續性的焦點區域建議的分數為 5%，實作該項建議會增加您整體的可用性和業務持續性分數 5%。

### <a name="focus-areas"></a>焦點區域

**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。

**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。

**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 SQL Server tooyour 現有基礎結構。

**作業和監視**-這個焦點區域會顯示建議 toohelp 簡化 IT 作業，實作的預防性維護，並將效能最大化。

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>您的目標應該 tooscore 100%中每個焦點區域？

不一定。 hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。 不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。 例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。 對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。 重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。 您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。

每項建議都包含其重要性的指引。 當實作 hello 建議是適合您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質，請使用本指引 tooevaluate。

## <a name="use-assessment-focus-area-recommendations"></a>使用評估焦點區域建議

您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。 tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 安裝之後，您可以使用 OMS hello 概觀 頁面上的 hello System Center Operations Manager 評估磚檢視建議 hello 摘要。

檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview 焦點區域，並採取修正動作的建議

1. 在 hello**概觀**頁面上，按一下 hello **System Center Operations Manager 評估**磚。
2. 在 hello **System Center Operations Manager 評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。
3. 在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。 按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。  
    ![focus area](./media/log-analytics-scom-assessment/focus-area.png)
4. 您可以採取 [建議動作] 中所建議的更正動作。 Hello 項目已獲得解決之後，後續評估會記錄的建議動作並提高法務遵循分數。 更正後的項目將以**通過的物件**呈現。

## <a name="ignore-recommendations"></a>忽略建議

如果您有想 tooignore 的建議，您可以建立 OMS 使用您的評估結果中出現 tooprevent 建議的文字檔。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>您想 tooignore tooidentify 建議

1. 登入 tooyour 工作區，並開啟 記錄搜尋。 使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：  
    ![log search](./media/log-analytics-scom-assessment/scom-log-search.png)

2. 選擇您想 tooignore 的建議。 您會在 hello 下一個程序中使用 RecommendationId hello 值。

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate 及使用 IgnoreRecommendations.txt 文字檔

1. 建立名為 IgnoreRecommendations.txt 的檔案。
2. 貼上或輸入您要 OMS tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。
3. 將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。
4. Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server。

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify 建議已忽略

1. 執行下一個排程評估 hello，預設每隔七天之後, hello 指定建議會標示忽略，而且不會出現在 hello 評估儀表板上。
2. 您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. 如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。

## <a name="system-center-operations-manager-assessment-solution-faq"></a>System Center Operations Manager 評定解決方案常見問題集

*我加入 hello 評估解決方案 toomy OMS 工作區。但我沒看到 hello 建議。為什麼？* 加入之後 hello 方案，請使用下列步驟檢視 hello 建議 hello OMS 儀表板上的 hello。  

- [設定 System Center Operations Manager 評估 hello 執行身分帳戶](#operations-manager-run-as-accounts-for-oms)  
- [設定 hello System Center Operations Manager 評估規則](#configure-the-assessment-rule)


*有方法 tooconfigure 頻率 hello 評估執行嗎？* 是。 請參閱[執行頻率設定 hello](#configure-the-run-frequency)。

*如果在我新增 hello System Center Operations Manager 評估解決方案之後探索到另一部伺服器，它會受到評估嗎？* 是，在探索之後，從那時起也會評估它 -- 預設是每隔 7 天。

*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？* AdvisorAssessment.exe

*Hello AdvisorAssessment.exe 程序執行的位置為何？* AdvisorAssessment.exe 執行 hello hello management server 的 HealthService hello 評估規則啟用的位置。 使用這個程序時，將會透過遠端資料收集來探索您的整個環境。

收集資料需要花費多少時間？ Hello 伺服器上的資料收集需費時約一小時。 在有許多 Operations Manager 執行個體或資料庫的環境中可能更久。

*設定 hello hello 評估 tooless 1440 分鐘以上的時間間隔該怎麼辦？* hello 評估是在每日一次最多的預先設定的 toorun。 如果您覆寫 hello 間隔值 tooa 值小於 1440 分鐘，然後 hello 評估使用 1440 分鐘做為 hello 間隔值。

*如何 tooknow 如果先決條件失敗？* 如果 hello 評估執行，而您沒有看到結果，則可能部分之 hello 評估 hello 先決條件失敗。 您可以執行查詢：`Type=Operation Solution=SCOMAssessment`和`Type=SCOMAssessmentRecommendation FocusArea=Prerequisites`記錄搜尋 toosee hello 中失敗的必要元件。

*必要條件未通過中出現 `Failed tooconnect toohello SQL Instance (….).` 訊息。什麼是 hello 問題？* AdvisorAssessment.exe，hello 處理程序收集資料，會執行 hello hello management server 的 HealthService。 Hello 評估的一部分，hello 處理序嘗試 tooconnect toohello 存在 hello Operations Manager 資料庫所在的 SQL Server。 當防火牆規則封鎖 hello 連接 toohello SQL Server 執行個體時，會發生此錯誤。

*收集的資料類型為何？* hello 下列類型的資料收集： WMI 資料登錄資料-事件記錄檔資料-Operations Manager 資料透過 Windows PowerShell，SQL 查詢檔案資訊的收集器。

*為什麼我必須 tooconfigure 執行身分帳戶？* Operations Manager 伺服器上會執行各種 SQL 查詢。 為了讓它們 toorun，您必須使用執行身分帳戶具有必要的權限。 此外，本機系統管理員認證是必要的 tooquery WMI。

*為什麼只顯示 hello 前 10 項建議？* 與其提供詳盡、 非常龐大的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。 解決後，智慧套件將會提供其他建議。 如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用記錄搜尋。

*是否有方法 tooignore 建議？* 是，請參閱 hello[忽略建議](#Ignore-recommendations)。


## <a name="next-steps"></a>後續步驟

- [搜尋記錄](log-analytics-log-searches.md)tooview 詳細的 System Center Operations Manager 評估資料和建議。
