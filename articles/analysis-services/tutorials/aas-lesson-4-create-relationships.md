---
標題： aaa"Azure Analysis Services 教學課程第 4 課： 建立關聯性 |Microsoft 文件"描述： 描述 toocreate 關聯性中的 hello Azure Analysis Services 教學課程專案的方式。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>第 4 課：建立關聯性

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以驗證 hello 匯入資料時自動建立的關聯性，並加入不同資料表之間的新關聯性。 關聯性是如何在這些資料表中的 hello 資料相互關聯的方式所建立的兩個資料表之間的連接。 例如，hello DimProduct 資料表和 hello DimProductSubcategory 資料表有每項產品所屬 tooa 子類別目錄的 hello 事實為基礎的關聯性。 詳細資訊，請參閱 toolearn[關聯性](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular)。
  
本課程的估計時間 toocomplete: **10 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 3 課： 標記為日期資料表](../tutorials/aas-lesson-3-mark-as-date-table.md)。 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>檢閱現有的關聯性和新增關聯性  
當您匯入資料時使用 取得資料時，您會從 hello AdventureWorksDW2014 資料庫了七個資料表。 一般而言，當您從關聯式來源匯入資料，會與 hello 資料一起自動匯入現有的關聯性。 不過，在繼續製作模型之前，您應該確認資料表之間的關聯性已正確建立。 本教學課程中，您會新增三個新的關聯性。  
  
#### <a name="tooreview-existing-relationships"></a>tooreview 現有的關聯性  
  
1.  按一下 hello**模型**功能表 >**模型檢視** > **圖表檢視**。  

    hello 模型設計師現在會出現在圖表檢視中，以圖形格式顯示所有 hello 資料表之間會線條您匯入。 資料表之間的 hello 線條表示匯入 hello 資料時自動建立的 hello 關聯性。
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    最大數量的 hello 資料表儘可能包含使用中的 hello 模型設計師中的 hello 右下角迷你地圖控制項。 您也可以按一下並拖曳資料表 toodifferent 位置，將資料表彼此更靠近結合在一起，或依照特定順序排列。 移動資料表不會影響 hello 已經 hello 資料表之間的關聯性。 tooview 所有 hello 資料行在特定資料表中，按一下並拖曳資料表邊緣 tooexpand 或讓較小。  
  
2.  按一下 hello 之間 hello 實線**DimCustomer**資料表和 hello **DimGeography**資料表。 這兩個資料表之間的 hello 實線顯示此關聯性為作用中，也就是說，它預設會使用計算 DAX 公式時。  
  
    請注意 hello **GeographyKey** hello 中的資料行**DimCustomer**資料表和 hello **GeographyKey** hello 中的資料行**DimGeography**資料表現在都出現的方塊內。 Hello 關聯性中，會使用這些資料行。 hello 關聯性的屬性現在也會出現在 hello**屬性**視窗。  
  
    > [!TIP]  
    > 此外 toousing hello 模型設計師圖表檢視中的，您也可以使用 hello 管理關聯性對話方塊方塊 tooshow hello 之間的關聯性的資料表中的所有資料表。 在 [表格式模型總管] 中，以滑鼠右鍵按一下 [關聯性] > [管理關聯性]。
  
3.  請確認下列關聯性的 hello 時所建立的 hello 資料表的每個從 hello AdventureWorksDW 資料庫匯入：  
  
    |Active|資料表|相關的查閱資料表|  
    |----------|---------|------------------------|  
    |是|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |是|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |是|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |是|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |是|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    如果遺漏任何 hello 關聯性，請確認您的模型包含下表中的 hello: DimCustomer、 DimDate、 DimGeography、 DimProduct、 DimProductCategory、 DimProductSubcategory 和 FactInternetSales。 如果從相同資料來源連接會在匯入的 hello 資料表分隔時間，這些資料表之間的任何關聯性不會建立，並必須手動建立。  

### <a name="take-a-closer-look"></a>進一步了解
在圖表檢視中，請注意箭號，星號，並且顯示 hello 資料表之間的關聯性的 hello 行上的數字。

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

hello 箭號會顯示 hello 篩選方向。 hello 星號顯示此資料表是 hello 多側中 hello 關聯性的基數和 hello 一個顯示此資料表是 hello hello 關聯性的一方。 如果您需要 tooedit 關聯性;例如，變更 hello 關聯性的基數或篩選方向中，按兩下 hello 關聯性線條 tooopen hello 編輯關聯性 對話方塊。

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

這些功能是為了進階資料模型化，而且是本教學課程的 hello 範圍外。 詳細資訊，請參閱 toolearn[雙向交叉篩選中 Analysis Services 表格式模型的](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services)。

在某些情況下，您可能需要特定的商務邏輯 toocreate 模型 toosupport 中資料表之間的其他關聯性。 此教學課程中，您需要 toocreate 三個額外之間的關聯性 hello FactInternetSales 資料表和 hello DimDate 資料表。  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd 資料表之間的新關聯性  
  
1.  Hello 模型設計師，在 hello **FactInternetSales**資料表，按一下並按住 hello **OrderDate**資料行，然後拖曳 hello 游標 toohello**日期**hello中的資料行**DimDate**資料表，然後再放開。  

    實線顯示您已建立作用中的關聯性之間 hello **OrderDate** hello 中的資料行**Internet Sales**資料表和 hello**日期**hello 中的資料行**日期**資料表。 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > 在建立關聯性時，會自動選取 hello 主資料表與 hello 查閱相關的資料表之間的 hello 基數和篩選方向。  
  
2.  在 hello **FactInternetSales**資料表、 按住 hello **DueDate**資料行，然後拖曳 hello 游標 toohello**日期**hello 中的資料行**DimDate**資料表，然後再放開。  
  
    此時會顯示您已建立 hello 之間的非使用中關聯性出現虛線**DueDate** hello 中的資料行**FactInternetSales**資料表和 hello**日期**中的資料行hello **DimDate**資料表。 您在資料表之間可以有多個關聯性，但一次只能有一個關聯性是作用中。 非使用中關聯性可以進行自訂的 DAX 運算式中 active tooperform 特殊的彙總。  
  
3.  最後，再建立一個關聯性。 在 hello **FactInternetSales**資料表、 按住 hello **ShipDate**資料行，然後拖曳 hello 游標 toohello**日期**hello 中的資料行**DimDate**資料表，然後再放開。  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>後續步驟
[第 5 課：建立計算結果欄](../tutorials/aas-lesson-5-create-calculated-columns.md)。
  
  
  
