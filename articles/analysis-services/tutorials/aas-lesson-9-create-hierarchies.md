---
標題： aaa"Azure Analysis Services 教學課程第 9 課： 建立階層 |Microsoft 文件"描述： 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>第 9 課：建立階層

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂課中，您會建立階層。 階層是依層級排列的資料行群組；例如，地理階層可能有國家/地區、州、縣和市的子層級。 階層可以顯示不同於其他資料行，在報表用戶端應用程式欄位清單，讓用戶端更容易使用者 toonavigate 和包含在報表中。 詳細資訊，請參閱 toolearn[階層](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate 階層，使用中的 hello 模型設計師*圖表檢視*。 不支援在 [資料檢視] 中建立及管理階層。  
  
本課程的估計時間 toocomplete: **20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 8 課： 建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>建立階層  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>toocreate hello DimProduct 資料表內的類別目錄階層  
  
1.  在 hello 模型設計工具 （圖表檢視），以滑鼠右鍵按一下 hello **DimProduct**資料表 >**建立階層**。 新的階層會出現在 hello hello 資料表視窗底部。 重新命名階層 hello**類別**。  
  
2.  按一下並拖曳 hello **ProductCategoryName**新的資料行 toohello**類別**階層。  
  
3.  在 hello**類別**階層，以滑鼠右鍵按一下 hello **ProductCategoryName** > **重新命名**，然後輸入**類別**。  
  
    > [!NOTE]  
    > 重新命名階層中的資料行，無法重新命名 hello 資料表中的該資料行。 在階層中的資料行是只 hello hello 資料表中的資料行表示法。  
  
4.  按一下並拖曳 hello **ProductSubcategoryName**資料行 toohello**類別**階層。 將它重新命名為 **Subcategory**。 
  
5.  以滑鼠右鍵按一下 hello **ModelName**資料行 >**新增 toohierarchy**，然後選取**類別**。 將它重新命名為 **Model**。

6.  最後，會加入**[englishproductname]** toohello 類別目錄階層。 將它重新命名 **Product**。  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>toocreate hello DimDate 資料表中的階層  
  
1.  在 hello **DimDate**資料表中，建立名為階層**行事曆**。  
  
3.  加入下列資料行之 in-order hello:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  在 hello **DimDate**資料表中，建立**會計**階層。 包括下列資料行之 in-order hello:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  最後，在 hello **DimDate**資料表中，建立**ProductionCalendar**階層。 包括下列資料行之 in-order hello:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>後續步驟
[第 10 課：建立資料分割](../tutorials/aas-lesson-10-create-partitions.md)。 
  
  
