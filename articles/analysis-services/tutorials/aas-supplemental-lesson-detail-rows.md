---
標題： aaa"Azure Analysis Services 教學課程的補充課程： 詳細資料列 |Microsoft 文件"描述： 描述如何 toocreate 詳細資料列運算式中的 hello Azure Analysis Services 教學課程。
服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>補充課程 - 詳細資料列

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這個補充課程中，您使用 DAX 編輯器 toodefine hello 自訂的詳細資料列運算式。 詳細資料列運算式是量值，屬性提供使用者有關 hello 彙總結果的量值的詳細資訊。 
  
本課程的估計時間 toocomplete: **10 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
此補充課程主題是表格式模型教學課程的一部分。 在執行前 hello 工作這個補充課程，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。  
  
## <a name="what-do-we-need-toosolve"></a>怎麼我們需要 toosolve？
讓我們看看 hello 詳細資料，我們 InternetTotalSales 量值，然後再加入詳細資料列運算式。

1.  在 SSDT 中，按一下 hello**模型**功能表 >**在 Excel 中的進行分析**tooopen Excel 並建立空白的樞紐分析表。
  
2.  在**樞紐分析表欄位**，新增 hello **InternetTotalSales**太量值從 hello FactInternetSales 資料表**值**， **CalendarYear**從 hello DimDate 資料表太**資料行**，和**EnglishCountryRegionName**太**列**。 我們的樞紐分析表現在可讓我們彙總結果從依區域和年份的 hello InternetTotalSales 量值。 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. 在 hello 樞紐分析表中，按兩下彙總值的年份和地區名稱。 這裡我們按兩下澳大利亞和 hello hello 值 2014 年。 包含資料 (但非實用資料) 的新工作表隨即開啟。

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
什麼我們想要 toosee 這裡是包含資料行和構成 toohello 彙總結果，我們 InternetTotalSales 量值的資料列的資料表。 toodo，我們可以加入詳細資料列運算式為 hello 量值的屬性。

## <a name="add-a-detail-rows-expression"></a>新增詳細資料列運算式

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate 詳細資料列運算式 
  
1. 在 SSDT 中，在 hello FactInternetSales 資料表的量值方格中，按一下 hello **InternetTotalSales**量值。 

2. 在**屬性** > **詳細資料列運算式**，按一下 hello 編輯器按鈕 tooopen hello DAX 編輯器。

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. 在 DAX 編輯器中，輸入下列運算式 hello:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    這個運算式會指定名稱，資料行，以及當使用者按兩下彙總的結果在樞紐分析表或報表中會傳回從 hello FactInternetSales 資料表和相關的資料表的量值結果。

4. 回在 Excel 中，刪除步驟 3 中建立的 hello 工作表，然後按兩下彙總的值。 這次 hello 量值定義的詳細資料列運算式內容，新的工作表會開啟包含更多有用的資料。

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. 重新部署您的模型。

  
## <a name="see-also"></a>另請參閱  
[SELECTCOLUMNS 函式 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[補充課程 - 動態安全性](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[補充課程 - 不完全階層](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
