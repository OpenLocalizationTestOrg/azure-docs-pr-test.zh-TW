---
標題： aaa"Azure Analysis Services 教學課程第 5 課： 建立導出資料行 |Microsoft 文件"描述： 說明如何 toocreate 算出 hello Azure Analysis Services 教學課程專案中的資料行。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>第 5 課：建立計算結果欄

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂課中，您會在模型中新增計算結果欄來建立資料。 您可以建立導出資料行 （做為自訂的資料行） 時使用 取得資料，使用 hello 查詢編輯器中，或稍後在 hello 模型設計工具類似您執行以下。 詳細資訊，請參閱 toolearn[導出資料行](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)。
  
您會在三個不同的資料表中建立五個新的計算結果欄。 hello 步驟會稍有不同的每個工作顯示有許多種 toocreate 資料行、 重新命名，並將它們放在不同資料表中的位置。  

您會在這堂課中第一次使用 Data Analysis Expressions (DAX)。 DAX 是一種特殊語言，可以為表格式模型建立可靈活自訂的公式運算式。 在本教學課程中，您可以使用 DAX toocreate 導出資料行、 量值和角色篩選。 詳細資訊，請參閱 toolearn[表格式模型中的 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)。 
  
本課程的估計時間 toocomplete: **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 4 課： 建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。 
  
## <a name="create-calculated-columns"></a>建立計算結果欄  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>建立 hello DimDate 資料表中的 MonthCalendar 導出資料行  
  
1.  按一下 hello**模型**功能表 >**模型檢視** > **資料檢視**。  
  
    導出資料行只可以建立使用資料檢視中的 hello 模型設計師。  
  
2.  在 hello 模型設計師中，按一下 hello **DimDate**資料表 （標籤）。  
  
3.  以滑鼠右鍵按一下 hello **CalendarQuarter**資料行標頭，然後再按一下**插入資料行**。  
  
    新的資料行名為**導出資料行 1**插入的 toohello 剩下的 hello**日曆季**資料行。  
  
4.  在 hello hello 資料表上方的公式列中輸入下列 DAX 公式的 hello： 自動完成可協助您輸入 hello 完整限定的名稱的資料行和資料表，並列出 hello 可用函式。  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Hello 導出資料行中的所有 hello 資料列就會都填入值。 如果您向下捲動 hello 資料表，您會看到資料列可以有不同的值，這個資料行，根據每個資料列中的 hello 資料。    
  
5.  重新命名此資料行太**MonthCalendar**。 

    ![aas 第 5 課新增資料行](../tutorials/media/aas-lesson5-newcolumn.png) 
  
hello MonthCalendar 導出資料行會提供可排序月份名稱。  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>在 hello DimDate 資料表中建立 DayOfWeek 導出資料行  
  
1.  以 hello **DimDate**資料表仍為使用中，按一下 hello**資料行**功能表，然後再按一下**加入資料行**。  
  
2.  Hello 公式列中輸入下列公式的 hello:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    當您完成建立 hello 公式時，請按 ENTER。 toohello hello 資料表的最右邊加入 hello 新資料行。  
  
3.  Hello 資料行重新命名過**DayOfWeek**。  
  
4.  按一下 hello 欄標題，並拖曳 hello 資料行之間 hello **EnglishDayNameOfWeek**資料行和 hello **DayNumberOfMonth**資料行。  
  
    > [!TIP]  
    > 移動資料表中的資料行可讓您更輕鬆 toonavigate。  
  
hello DayOfWeek 導出資料行提供可排序的 hello 週間日名稱。  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>建立 hello DimProduct 資料表內的 ProductSubcategoryName 導出資料行  
  
  
1.  在 hello **DimProduct**資料表中，捲動 toohello hello 資料表的最右邊。 請注意 hello 最右側資料行名為**加入資料行**（斜體），請按一下 hello 資料行標題。  
  
2.  Hello 公式列中輸入下列公式的 hello:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Hello 資料行重新命名過**ProductSubcategoryName**。  
  
hello ProductSubcategoryName 導出資料行是使用的 toocreate hello DimProduct 資料表，其中包括 hello DimProductSubcategory 資料表中從 hello [englishproductsubcategoryname] 資料行的資料中的階層。 階層不可跨越多個資料表。 稍後您會在第 9 課中建立階層。  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>建立 hello DimProduct 資料表內的 ProductCategoryName 導出資料行  
  
1.  以 hello **DimProduct**資料表仍為使用中，按一下 hello**資料行**功能表，然後再按一下**加入資料行**。  
  
2.  Hello 公式列中輸入下列公式的 hello:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Hello 資料行重新命名過**ProductCategoryName**。  
  
hello ProductCategoryName 導出資料行是使用的 toocreate hello DimProduct 資料表，其中包括 hello DimProductCategory 資料表中從 hello [englishproductcategoryname] 資料行的資料中的階層。 階層不可跨越多個資料表。  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>在 hello FactInternetSales 資料表中建立 Margin 導出資料行  
  
1.  在 hello 模型設計師中，選取 hello **FactInternetSales**資料表。  
  
2.  建立新的導出資料行之間 hello **SalesAmount**資料行和 hello **TaxAmt**資料行。  
  
3.  Hello 公式列中輸入下列公式的 hello:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Hello 資料行重新命名過**邊界**。  
 
      ![aas 第 5 課新增獲利率](../tutorials/media/aas-lesson5-newmargin.png)
      
    hello Margin 導出資料行是每個銷售的使用的 tooanalyze 利率。  
  
## <a name="whats-next"></a>後續步驟
[第 6 課：建立量值](../tutorials/aas-lesson-6-create-measures.md)。
  
  
  
