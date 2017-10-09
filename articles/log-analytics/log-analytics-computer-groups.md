---
title: "aaaComputer 群組中記錄分析記錄搜尋 |Microsoft 文件"
description: "記錄分析中的電腦群組可讓您 tooscope 記錄搜尋 tooa 特定一組電腦。  本文說明 hello toocreate 電腦群組，以及這些記錄檔中搜尋 toouse 如何，您可以使用不同的方法。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Log Analytics 記錄檔搜尋中的電腦群組

>[!NOTE]
> 本文說明 hello 使用使用 hello 目前記錄 Anayltics 查詢語言的電腦群組。    如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則電腦群組的運作方式不同。  附註 hello 新的查詢語言提供在本文中與 hello 不同的語法和行為。  


記錄分析中的電腦群組可讓您 tooscope[記錄搜尋](log-analytics-log-searches.md)tooa 特定一組電腦。  使用您所定義的查詢，或從不同來源匯入群組，將電腦填入每個群組中。  Hello 群組包含在記錄搜尋，hello 結果會是有限的 toorecords 符合 hello 群組中的 hello 電腦。

## <a name="creating-a-computer-group"></a>建立電腦群組
您可以建立電腦群組中使用任何 hello 方法 hello 下表中的記錄分析。  Hello 的以下各節提供每個方法的詳細資訊。 

| 方法 | 說明 |
|:--- |:--- |
| 記錄搜尋 |建立會傳回一份電腦的記錄搜尋，並將 hello 結果儲存為電腦群組。 |
| 記錄檔搜尋 API |使用 hello Log Search API tooprogrammatically 建立 hello 結果的記錄搜尋為基礎的電腦群組。 |
| Active Directory |自動掃描 hello 是 Active Directory 網域的成員，且記錄分析中建立群組，針對每個安全性群組的任何代理程式電腦群組成員資格。 |
| WSUS |自動掃描 WSUS 伺服器或用戶端來找出目標群組，並為每個群組在 Log Analytics 中建立一個群組。 |

### <a name="log-search"></a>記錄搜尋
所建立的記錄搜尋的電腦群組包含所有您定義的搜尋查詢所傳回的 hello 電腦。  此查詢會執行每次使用，因此任何 hello 群組建立以來的變更會反映 hello 電腦群組。

使用記錄搜尋中的下列程序 toocreate 電腦群組的 hello。

1. [建立記錄檔搜尋](log-analytics-log-searches.md)來傳回電腦清單。  hello 搜尋必須傳回一組不同的電腦使用類似**相異電腦**或**measure count （) 電腦**hello 查詢中。  
2. 按一下 hello**儲存**在 hello 囉 」 畫面最上方的按鈕。
3. 選取**是**太**將此查詢儲存為電腦群組**。
4. 在中輸入**名稱**和**類別**hello 群組。  如果以搜尋可 hello 相同名稱和類別目錄已經存在，則會被提示的 toooverwrite 它。  您可以有多個不同分類名稱相同的 hello 與搜尋。 

以下是您可以儲存為電腦群組的搜尋範例。

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)則 hello 下列變更會提出的 toohello 程序 toocreate 新電腦群組。
>  
> - hello 電腦群組必須包含查詢 toocreate `distinct Computer`。  以下是查詢 toocreate 電腦群組的範例。<br>`Heartbeat | where Computer contains "srv" `
> - 當您建立新的電腦群組時，您必須新增 toohello 名稱中指定的別名。  當使用在查詢中的 hello 電腦群組，如下所述，您可以使用 hello 別名。  

### <a name="log-search-api"></a>記錄檔搜尋 API
電腦群組以 hello 記錄搜尋 API 是建立 hello 相同為使用記錄搜尋所建立的搜尋。

如需建立使用 hello Log Search API 的電腦群組的詳細資訊，請參閱[記錄分析記錄檔中的電腦群組搜尋 REST API](log-analytics-log-search-api.md#computer-groups)。

### <a name="active-directory"></a>Active Directory
當您設定記錄分析 tooimport Active Directory 群組成員資格時，它會分析 hello hello OMS 代理程式的任何已加入網域電腦群組成員資格。  電腦群組中建立記錄分析的每個安全性群組，在 Active Directory 中，並每一部電腦會加入對應 toohello 安全性群組的成員才 toohello 電腦群組。  此成員資格持續地每 4 小時更新一次。  

設定記錄分析 tooimport Active Directory 安全性群組從 hello**電腦群組**記錄分析中的功能表**設定**。  選取 [自動化]，然後選取 [從電腦匯入 Active Directory 群組成員資格]。  不需要進一步的組態。

![來自 Active Directory 的電腦群組](media/log-analytics-computer-groups/configure-activedirectory.png)

當群組已經匯入時，hello 功能表清單 hello 與群組成員資格的電腦數目偵測到與 hello 匯入的群組數目。  您可以按一下這些連結 tooreturn hello 任一**ComputerGroup**這項資訊的記錄。

### <a name="windows-server-update-service"></a>Windows Server Update Service
當您設定記錄分析 tooimport WSUS 群組成員資格，它會分析 hello 目標 hello OMS 代理程式的任何電腦群組成員資格。  如果您使用用戶端為目標，是連接的 tooOMS 且為任何 WSUS 目標群組一部分的任何電腦有其群組成員資格匯入 tooLog 分析。 如果您使用伺服器端為目標，hello OMS 代理程式應該安裝在 hello WSUS 伺服器 hello 群組成員資格資訊 toobe 匯入 tooOMS。  此成員資格持續地每 4 小時更新一次。 

設定記錄分析 tooimport Active Directory 安全性群組從 hello**電腦群組**記錄分析中的功能表**設定**。  選取 [Active Directory]，然後選取 [從電腦匯入 Active Directory 群組成員資格]。  不需要進一步的組態。

![來自 Active Directory 的電腦群組](media/log-analytics-computer-groups/configure-wsus.png)

當群組已經匯入時，hello 功能表清單 hello 與群組成員資格的電腦數目偵測到與 hello 匯入的群組數目。  您可以按一下這些連結 tooreturn hello 任一**ComputerGroup**這項資訊的記錄。

## <a name="managing-computer-groups"></a>管理電腦群組
您可以檢視電腦群組所建立的記錄搜尋，或從 hello hello Log Search API**電腦群組**記錄分析中的功能表**設定**。  按一下 hello **x**在 hello**移除**資料行 toodelete hello 電腦群組。  按一下 hello**檢視成員**傳回其成員的群組 toorun hello 群組記錄搜尋圖示。 

![已儲存的電腦群組](media/log-analytics-computer-groups/configure-saved.png)

toomodify hello 群組中，建立新群組以 hello 相同**類別**和**名稱**toooverwrite hello 原始群組。

## <a name="using-a-computer-group-in-a-log-search"></a>在記錄檔搜尋中使用電腦群組
您使用下列語法 toorefer tooa 電腦群組在記錄搜尋中的 hello。  指定 hello**類別**是選擇性的而且只需要有電腦群組以不同的類別目錄中名稱相同的 hello。 

    $ComputerGroups[Category: Name]

執行搜尋時，會先解析 hello hello 在搜尋中包含的任何電腦群組的成員。  Hello 群組根據 記錄搜尋，如果該搜尋是之前執行 hello 最上層的記錄搜尋執行 tooreturn hello hello 群組成員。

電腦群組通常會使用 hello **IN**子句在 hello 記錄搜尋中如 hello 下列範例所示：

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後在查詢中使用電腦群組將其別名做為函式，如 hello 下列範例所示：
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>電腦群組記錄
從 Active Directory 或 WSUS 建立每個電腦群組成員資格的 hello OMS 儲存機制中建立的記錄。  這些記錄都有一種**ComputerGroup**和 hello 下表中都有 hello 屬性。  如果電腦群組是根據記錄檔搜尋，則不會建立記錄。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| 電腦 |Hello 成員電腦的名稱。 |
| 群組 |Hello 群組的名稱。 |
| GroupFullName |完整路徑 toohello 群組包括 hello 來源與來源名稱。 |
| GroupSource |群組的收集來源。 <br><br>ActiveDirectory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |從收集 hello 來源 hello 群組的名稱。  針對 Active Directory，這是 hello 網域名稱。 |
| ManagementGroupName |SCOM 代理程式 hello 管理群組名稱。  若為其他代理程式，此為 AOI-\<工作區 ID\> |
| TimeGenerated |建立或更新的日期和時間的 hello 電腦群組。 |

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。  

