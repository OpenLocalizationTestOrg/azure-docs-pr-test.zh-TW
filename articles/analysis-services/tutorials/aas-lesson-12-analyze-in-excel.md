---
標題： aaa"Azure Analysis Services 教學課程第 12 課： 在 Excel 中分析 |Microsoft 文件"描述： 描述如何在 hello toouse 在 Excel 中進行分析 Azure Analysis Services 教學課程專案。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>第 12 課：在 Excel 中進行分析

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以使用 Excel 功能 tooopen Microsoft Excel 中的 hello 分析、 自動建立連線 toohello 模型工作空間，並自動將樞紐分析表 toohello 工作表。 在 excel 中的 hello 分析的目的在於 tooprovide 模型的快速簡便方式 tootest hello 效率設計先前 toodeploying 模型。 在這堂課中，您不會執行任何資料分析。 hello 本課程的目的是 toofamiliarize，hello 模型所撰寫，與 hello 工具您可以使用 tootest 模型設計。   
  
這一課，Excel 必須安裝在 hello toocomplete 與 SSDT 相同的電腦。
  
本課程的估計時間 toocomplete:**五分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 11 課： 建立角色](../tutorials/aas-lesson-11-create-roles.md)。  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>瀏覽使用 hello 預設和網際網路銷售檢視方塊  
在這些首要工作中，您瀏覽您的模型使用這兩個 hello 預設檢視方塊，包含所有模型物件，並使用 hello 網際網路銷售檢視方塊您稍早。 hello 網際網路銷售檢視方塊排除 hello Customer 資料表物件。  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse 使用 hello 預設檢視方塊  
  
1.  按一下 hello**模型**功能表 >**在 Excel 中的進行分析**。  
  
2.  在 hello**在 Excel 中的進行分析**對話方塊中，按一下**確定**。  
  
    Excel 會開啟新的活頁簿。 會使用 hello 目前的使用者帳戶建立資料來源連接和 hello 預設檢視方塊是使用的 toodefine 可檢視的欄位。 樞紐分析表會自動加入 toohello 工作表。  
  
3.  在 Excel 中，在 hello**樞紐分析表欄位清單**，請注意 hello **DimDate**和**FactInternetSales**量值群組會出現。 hello **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**，**DimProductSubcategory**，和**FactInternetSales**具有其各自的資料行的資料表也會出現。  
  
4.  關閉 Excel 而不儲存 hello 活頁簿。  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse 使用 hello 網際網路銷售檢視方塊  
  
1.  按一下 hello**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在 hello**在 Excel 中的進行分析**對話方塊中，保留**目前 Windows 使用者**選取，然後在 hello**觀點來看**下拉式清單方塊中，選取**網際網路銷售額**，然後按一下**確定**。 
    
    ![aas 第 12 課檢視方塊](../tutorials/media/aas-lesson12-perspective.png)
    
3.  在 Excel 中，在**樞紐分析表欄位**，請注意 hello DimCustomer 資料表排除 hello 欄位清單。  
    
    ![aas 第 12 課欄位](../tutorials/media/aas-lesson12-fields.png)
    
4.  關閉 Excel 而不儲存 hello 活頁簿。  
  
## <a name="browse-by-using-roles"></a>使用角色來瀏覽  
角色是任何表格式模型的重要部分。 若沒有至少一個角色 toowhich 使用者會新增為成員，使用者無法存取並分析資料，使用您的模型。 在 excel 中的 hello 分析方式為您提供定義 tootest hello 角色。  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse 使用 hello Sales Manager 使用者角色  
  
1.  在 SSDT 中，按一下 hello**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在**指定 hello 使用者名稱或角色 toouse tooconnect toohello 模型**，選取**角色**，然後在 hello 下拉式清單方塊中，選取**銷售經理**，然後按一下 **確定**。  
  
    Excel 會開啟新的活頁簿。 將會自動建立樞紐分析表。 hello 樞紐分析表欄位清單包含所有 hello 可用資料欄位在新的模型。  
      
3.  關閉 Excel 而不儲存 hello 活頁簿。  
  
## <a name="whats-next"></a>後續步驟
下一課中移 toohello: [13 課： 部署](../tutorials/aas-lesson-13-deploy.md)。

  
  
  
