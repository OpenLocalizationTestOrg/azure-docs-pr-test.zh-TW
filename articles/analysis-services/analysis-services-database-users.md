---
title: "aaaManage 資料庫角色和 Azure Analysis Services 中的使用者 |Microsoft 文件"
description: "了解如何 toomanage 資料庫角色和 Azure 中的 Analysis Services 伺服器上的使用者。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>管理資料庫角色和使用者

資料庫層級 hello 模型，所有使用者必須都屬於 tooa 角色。 角色定義與 hello 模型資料庫的特定權限的使用者。 任何使用者或安全性群組新增 tooa 角色必須有在 hello Azure AD 租用戶的帳戶相同的訂用帳戶與 hello 伺服器。

您如何定義角色是不同視 hello 工具使用，但 hello 效果是 hello 相同。

角色權限包括：
*  **系統管理員**位使用者擁有 hello 資料庫的完整權限。 具有系統管理員權限的資料庫角色與伺服器管理員不同。
*  **處理序**-使用者可以連線 tooand 執行 hello 資料庫上的處理作業和分析模型資料庫的資料。
*  **讀取**-使用者可以使用用戶端應用程式 tooconnect tooand 分析模型資料庫的資料。

建立表格式模型專案時，您會建立角色，並在 SSDT 中使用角色管理員新增使用者或群組 toothose 角色。 當部署的 tooa 伺服器，您使用 SSMS， [Analysis Services PowerShell 指令程式](https://msdn.microsoft.com/library/hh758425.aspx)，或[表格式模型指令碼語言](https://msdn.microsoft.com/library/mt614797.aspx)(TMSL) tooadd 或移除角色和使用者的成員。

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd 或管理角色和在 SSDT 中的使用者  
  
1.  在 SSDT > [表格式模型總管] 中，以滑鼠右鍵按一下 [角色]。  
  
2.  在 [角色管理員] 中，按一下 [新增]。  
  
3.  輸入 hello 角色的名稱。  
  
     根據預設，hello hello 預設角色名稱是以累加方式編號為每個新的角色。 建議您輸入清楚識別 hello 成員類型，例如 「 財務經理 」 或 「 人力資源專員的名稱。  
  
4.  選取其中一個 hello 下列權限：  
  
    |權限|說明|  
    |----------------|-----------------|  
    |**None**|成員無法修改 hello 模型結構描述，且無法查詢資料。|  
    |**讀取**|成員可以查詢資料 （根據資料列篩選），但無法修改 hello 模型結構描述。|  
    |**讀取和處理**|成員可以查詢資料 （根據資料列層級篩選） 和執行的處理 」 和 「 處理全部作業，但無法修改 hello 模型結構描述。|  
    |**處理程序**|成員可以執行「處理」和「全部處理」作業。 無法修改 hello 模型結構描述，也無法查詢資料。|  
    |**系統管理員**|成員可以修改 hello 模型結構描述，並查詢所有資料。|   
  
5.  如果您是 hello 角色建立具有讀取或讀取和處理序的權限，您可以透過使用 DAX 公式加入資料列篩選。 按一下 hello**資料列篩選器**索引標籤，然後選取資料表，再按一下 hello **DAX 篩選**欄位，並輸入 DAX 公式。
  
6.  按一下 [成員] >  [新增外部]。  
  
8.  在 [新增外部成員] 中，依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。 按一下 [確定] 並關閉 [角色管理員] 後，角色和角色成員就會出現在 [表格式模型總管] 中。 
 
     ![表格式模型總管中的角色和使用者](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. 部署 tooyour Azure Analysis Services 伺服器。


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd 或管理角色和在 SSMS 中的使用者
tooadd 角色和使用者 tooa 部署模型資料庫，您必須是伺服器連接的 toohello 伺服器系統管理員身分或已經是系統管理員權限的資料庫角色。

1. 在 [物件總館] 中，以滑鼠右鍵按一下 [角色] > [新增角色]。

2. 在 [建立角色] 中，輸入角色名稱和描述。

3. 選取權限。
   |權限|說明|  
   |----------------|-----------------|  
   |**完全控制 (系統管理員)**|成員可以修改 hello 模型結構描述中，處理，以及查詢的所有資料。| 
   |**處理資料庫**|成員可以執行「處理」和「全部處理」作業。 無法修改 hello 模型結構描述，也無法查詢資料。|  
   |**讀取**|成員可以查詢資料 （根據資料列篩選），但無法修改 hello 模型結構描述。|  
  
4. 按一下 [成員資格]，然後依照電子郵件地址輸入 Azure AD 租用戶中的使用者或群組。

     ![新增使用者](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. 如果您要建立 hello 角色具有讀取權限，您可以透過使用 DAX 公式加入資料列篩選。 按一下**資料列篩選器**選取資料表，然後輸入 DAX 公式在 hello **DAX 篩選**欄位。 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd 角色和使用者使用 TMSL 指令碼
您可以在 SSMS 中，或使用 PowerShell 的 hello 的 XMLA 視窗中執行 TMSL 指令碼。 使用 hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl)命令和 hello[角色](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl)物件。

**TMSL 指令碼範例**

在此範例中，B2B 外部的使用者和群組會加入 toohello 分析師角色擁有 hello SalesBI 資料庫的讀取權限。 同時 hello 外部使用者和群組必須在同一個租用戶的 Azure AD。

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd 角色和使用者使用 PowerShell
hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx)模組提供的工作特有的資料庫管理 cmdlet 和 hello 一般用途 Invoke-ascmd 指令程式可接受表格式模型指令碼語言 (TMSL) 查詢或指令碼。 hello 下列 cmdlet 可用來管理資料庫角色和使用者。
  
|Cmdlet|說明|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|加入成員 tooa 資料庫角色。| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|從資料庫角色移除成員。|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|執行 TMSL 指令碼。|

## <a name="row-filters"></a>資料列篩選條件  
資料列篩選條件定義特定角色的成員可以查詢資料表中的哪些資料列。 使用 DAX 公式，針對模型中的每個資料表定義資料列篩選條件。  
  
只能針對具有「讀取」和「讀取和處理」權限的角色定義資料列篩選條件。 根據預設，如果資料列篩選器沒有定義特定資料表中，成員可以查詢 hello 資料表中的所有資料列除非從另一個資料表套用交叉篩選。
  
 資料列篩選器需要 DAX 公式，必須評估 tooa TRUE/FALSE 值，該特定角色的成員可以查詢 toodefine hello 資料列。 無法查詢未包含在 hello DAX 公式的資料列。 例如，下列資料列篩選器運算式，hello 與 hello Customers 資料表*= 客戶 [Country] ="USA"*，hello 銷售 」 角色的成員只能看到 hello 美國的客戶。  
  
資料列篩選器套用 toohello 指定資料列和相關的資料列。 當資料表具有多個關聯性時，篩選會套用安全性為使用中的 hello 關聯性。 資料列篩選條件會與針對相關資料表定義的其他資料列篩選條件產生交集，例如：  
  
|資料表|DAX 運算式|  
|-----------|--------------------|  
|區域|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|交易|=Transactions[Year]=2016|  
  
 hello 最後的結果是成員可以查詢其中 hello 客戶位於 hello 美國、 hello 產品類別目錄是自行車，而 hello 年份是 2016年的資料列。 使用者無法查詢交易的交易之外 hello USA 不自行車或交易中所沒有 2016年除非授與這些權限的另一個角色的成員。
  
 您可以使用 hello 篩選*=FALSE()*，toodeny 存取 tooall 資料列，針對整個資料表。

## <a name="next-steps"></a>後續步驟
  [管理伺服器管理員](analysis-services-server-admins.md)   
  [使用 PowerShell 管理 Azure Analysis Services](analysis-services-powershell.md)  
  [表格式模型指令碼語言 (TMSL) 參考](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

