---
title: "使用 Power BI Embedded aaaRow 層級安全性"
description: "資料列層級安全性與 Power BI Embedded 的詳細資料"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Power BI Embedded 的資料列層級安全性

資料列層級安全性 (RLS) 可以是報表或資料集，讓多個不同的使用者 toouse hello 所有文件都看到不同的資料時的相同報表中使用的 toorestrict 使用者存取 tooparticular 資料。 Power BI Embedded 現在支援使用 RLS 設定資料集。

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

在順序 tootake 優點 RLS，務必了解三個主要概念;使用者、 角色和規則。 讓我們仔細看看每個概念：

**使用者**– 這些 hello 實際使用者檢視報表。 Power BI Embedded，使用者所識別的應用程式權杖中的 hello username 屬性。

**角色**– 使用者所屬的 tooroles。 角色是規則的容器，並可命名為類似「業務經理」或「業務代表」的項目。 Power BI Embedded，使用者所識別的應用程式權杖中的 hello 角色屬性。

**規則**– 角色其規則，而且這些規則將套用的 toobe toohello 資料 hello 實際篩選。 可以像 “Country = USA” 一樣簡單，或是更動態的項目。

### <a name="example"></a>範例

這篇文章 hello 其餘部分，我們會提供撰寫 RLS，並再耗用，內嵌的應用程式中的範例。 我們的範例會使用 hello[零售分析範例](http://go.microsoft.com/fwlink/?LinkID=780547)PBIX 檔案。

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

我們零售分析範例會顯示特定零售鏈結中所有的 hello 商店的銷售。 沒有 RLS，不論哪個地區管理員登入並檢視 hello 報表，就會看到 hello 相同的資料。 每個區域經理只能看到 hello 銷售 hello 存放區所管理，以及 toodo 這判定資深管理，我們可以使用 RLS。

RLS 是在 Power BI Desktop 中撰寫。 Hello 資料集和報表會開啟時，我們可以切換 toodiagram 檢視 toosee hello 結構描述：

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

以下是幾件事 toonotice 與此結構描述：

* 所有量值，例如**Total Sales**，會儲存在 hello**銷售**事實資料表。
* 有四個額外的相關維度資料表︰**項目**、**時間**、**商店**和**區域**。
* hello 關聯性線條上的 hello 箭號表示篩選條件可以從一個資料表 tooanother 流動的方式。 比方說，如果篩選置於**時間 [Date]**，hello 目前結構描述中就會只往下篩選中 hello 值**銷售**資料表。 沒有其他資料表會受到這個篩選條件，因為所有的 hello 箭號 hello 關聯性線條點 toohello 銷售資料表並不會離開。
* hello**地區**資料表表示 hello 管理員的每個區域者：
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

根據此結構描述，如果我們套用篩選器 toohello**區域經理**中的資料行 hello 區域資料表，和該篩選條件符合 hello 使用者檢視 hello 報表，如果該篩選條件也將篩選向下 hello**存放區**和**銷售**資料表 tooonly 顯示該特定地區的資料管理員。

方式如下：

1. 在 [hello 模型] 索引標籤上按一下**管理角色**。  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. 建立新的角色，稱為 [經理] 。  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. 在 hello**地區**資料表輸入下列 DAX 運算式的 hello: **[區域經理] = username （）**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. 使用 toomake 確定 hello 規則，在 hello**模型**索引標籤上，按一下 **以角色身分檢視**，然後輸入 hello 下列：  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   hello 報表現在將會顯示資料如同您已登入為**Andrew Ma**。

套用 hello 篩選，在這裡，我們所做的 hello 方式關閉 hello 中的所有記錄會篩選**地區**，**存放區**，和**銷售**資料表。 不過，由於 hello 篩選方向 hello 之間的關聯性上**銷售**和**時間**，**銷售**和**項目**，和**項目**和**時間**將不會向下篩選資料表。

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

可能是 [確定]，這項需求，不過，如果我們不想其不具有任何銷售經理 toosee 項目，我們無法開啟雙向交叉篩選兩個方向的 hello 關聯性和流程 hello 安全性篩選。 作法是藉由編輯 hello 之間的關聯性**銷售**和**項目**，如下所示：

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

現在，篩選可以也傳送 hello Sales 資料表 toohello 從**項目**資料表：

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> 如果您使用 DirectQuery 模式為您的資料，您將需要 tooenable 雙向交叉篩選選取這兩個選項：

1. [檔案]  ->  [選項和設定]  ->  [預覽功能]  ->  [針對 DirectQuery 啟用兩個方向的交叉篩選]。
2. [檔案]  ->  [選項和設定]  ->  [DirectQuery]  ->  [允許 DirectQuery 模式中的不受限制量值]。

深入了解雙向交叉篩選，下載 hello toolearn[雙向交叉篩選 SQL Server Analysis Services 2016 和 Power BI Desktop 中](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx)白皮書。

這會結束所有的 hello 工作需要 toobe 完成在 Power BI Desktop 中，但沒有一個多份工作需要完成的 toobe toomake hello RLS 規則我們在 Power BI Embedded 定義工作。 使用者獲得驗證和授權您的應用程式和應用程式語彙基元是使用的 toogrant 該使用者存取 tooa 特定 Power BI Embedded 報表。 Power BI Embedded 對於您的使用者是誰，並沒有任何特定資訊。 RLS toowork，您將需要 toopass 某些額外的內容做為您的應用程式的權杖的一部分：

* **使用者名稱**（選用） – 使用 rls 這是可用的字串 toohelp 套用 RLS 規則時，請識別 hello 使用者。 請參閱「搭配使用資料列層級安全性和 Power BI Embedded」
* **角色**– 套用資料列層級安全性規則時，包含 hello 角色 tooselect 的字串。 如果傳遞多個角色，應該將它們傳遞為字串陣列。

使用 hello 建立 hello 語彙基元[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__)方法。 如果 hello username 屬性存在，則您也必須在角色中傳遞至少一個值。

例如，您可以變更 hello EmbedSample。 DashboardController 第 55 行可以從

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

to

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

hello 完整的應用程式語彙基元看起來像這樣：

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

現在，與所有的 hello 片段放在一起，當有人登入我們的應用程式 tooview 這份報表，他們只必須能夠 toosee hello 資料才會允許 toosee，本公司的資料列層級安全性所定義。

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>另請參閱

[資料列層級安全性 (RLS) 與 Power](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

