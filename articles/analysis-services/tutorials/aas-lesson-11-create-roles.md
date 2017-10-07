---
標題： aaa"Azure Analysis Services 教學課程第 11 課： 建立角色 |Microsoft 文件"描述： 描述如何在 toocreate 角色 hello Azure Analysis Services 教學課程專案。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>第 11 課：建立角色

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂課中，您會建立角色。 角色提供模型資料庫物件和資料安全性，方法是限制存取 tooonly 這些使用者角色的成員。 每個角色都定義有單一權限︰「無」、「讀取」、「讀取和處理」、「處理」或「系統管理員」。 在製作模型期間可以使用 [角色管理員] 來定義角色。 在部署模型之後，您可以使用 SQL Server Management Studio (SSMS) 來管理角色。 詳細資訊，請參閱 toolearn[角色](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)。
  
> [!NOTE]  
> 建立角色時，則不需要 toocomplete 本教學課程。 根據預設，您目前登入的 hello 帳戶具有 hello 模型系統管理員權限。 不過，在您的組織 toobrowse 使用報表用戶端中的其他使用者，您必須建立至少一個角色具有讀取權限，並將這些使用者新增為成員。  
  
您可建立三個角色︰  
  
-   **銷售經理**– 此角色可包含您要為其 toohave 讀取權限 tooall 模型物件和資料的組織中的使用者。  
  
-   **Sales Analyst US** – 此角色可包含您想 toobe 無法 toobrowse 資料的組織中的使用者相關 toosales hello 美國中的。 此角色中，您可以使用 DAX 公式的 toodefine*資料列篩選器*，以限制僅針對 hello 美國成員 toobrowse 資料。  
  
-   **系統管理員**– 此角色可包含您想要的 toohave 系統管理員權限，這允許無限制的存取和權限 tooperform 系統管理工作 hello 模型資料庫上的使用者。  
  
因為您組織中的 Windows 使用者和群組帳戶是唯一的您可以從特定組織 toomembers 新增帳戶。 不過，本教學課程，您可以也留 hello 成員。 您稍後在第 12 課中測試的每個角色的 hello 效果： 在 Excel 中進行分析。  
  
本課程的估計時間 toocomplete: **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 10 課： 建立資料分割](../tutorials/aas-lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>建立角色  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate Sales Manager 使用者角色  
  
1.  在 [表格式模型總管] 中，以滑鼠右鍵按一下 [角色] > [角色]。  
  
2.  在 [角色管理員] 中，按一下 [新增]。  
  
3.  按一下 hello 新角色，然後在 hello**名稱**資料行，hello 角色重新命名過**銷售經理**。  
  
4.  在 hello**權限**資料行中，按一下 hello 下拉式清單中，然後選取 hello**讀取**權限。 

    ![aas 第 11 課新的角色](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。 在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate Sales Analyst US 使用者角色  
  
1.  在 [角色管理員] 中，按一下 [新增]。    
  
2.  Hello 角色重新命名過**Sales Analyst US**。  
  
3.  將 [讀取] 權限授與此角色。  
  
4.  按一下 hello 資料列篩選器 索引標籤，然後 hello **DimGeography**資料表僅 hello DAX 篩選資料行中，下列公式的型別 hello:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    資料列篩選公式必須解析 tooa 布林 (TRUE/FALSE) 值。 使用這個公式，就指定的資料列 hello Country Region Code 值為"US"可見的 toohello 使用者。  
    ![aas 第 11 課角色篩選](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。 在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate 系統管理員使用者角色  
  
1.  按一下 [新增] 。  
  
2.  Hello 角色重新命名過**管理員**。  
  
3.  將 [系統管理員] 權限授與此角色。  
  
4.  選擇性： 按一下 hello**成員**索引標籤，然後再按一下**新增**。 在 hello**選取使用者或群組**對話方塊方塊中，輸入 hello Windows 使用者或群組從您的組織想要 tooinclude hello 角色中的。 
  
  
## <a name="whats-next"></a>後續步驟
[第 12 課：在 Excel 中進行分析](../tutorials/aas-lesson-12-analyze-in-excel.md)

  
  
