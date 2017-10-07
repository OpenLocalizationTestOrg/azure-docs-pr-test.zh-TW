---
標題： aaa"Azure Analysis Services 教學課程第 6 課： 建立量值 |Microsoft 文件"描述： 描述 toocreate hello Azure Analysis Services 教學課程專案中的量值。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-6-create-measures"></a>第 6 課：建立量值

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以建立包含在模型中的量值 toobe。 類似 toohello 計算您所建立的資料行、 量值是透過使用 DAX 公式所建立的計算。 不過，與計算結果欄不同，量值評估是根據使用者選取的「篩選條件」。 例如，特定資料行或交叉分析篩選器 toohello 資料列標籤欄位加入樞紐分析表中。 Hello 篩選中的每個儲存格的值則會計算所套用的 hello 量值中。 量值是功能強大、 有彈性的計算，您想 tooinclude 中幾乎所有表格式模型 tooperform 動態計算數值資料上。 詳細資訊，請參閱 toolearn[量值](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular)。
  
toocreate 量值，使用 hello*量值方格*。 根據預設，每個資料表都有一個空白量值方格；不過，您通常不會為每個資料表建立量值。 hello 量值方格隨即出現在資料檢視中的 hello 模型設計師中的資料表下方。 toohide 或顯示 hello 量值方格資料表中，按一下 hello**資料表**功能表，然後再按一下**顯示量值方格**。  
  
您可以按一下 hello 量值方格中的空資料格，然後再 hello 公式列中輸入 DAX 公式建立量值。 當您按一下 ENTER toocomplete hello 公式，hello 量值，則會顯示 hello 資料格中。 您也可以建立資料行，即可使用標準彙總函式的量值，然後按一下 hello 加總 按鈕 (**∑**) hello 工具列上。 使用 hello 自動加總 功能建立的量值會出現在 hello 量值方格資料格正下方 hello 資料行，但是可以移動。  
  
在這一課，您會建立量值在 hello 公式列中，這兩個輸入 DAX 公式，而藉由使用 hello 自動加總功能。  
  
本課程的估計時間 toocomplete: **30 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 5 課： 建立導出資料行](../tutorials/aas-lesson-5-create-calculated-columns.md)。  
  
## <a name="create-measures"></a>建立量值  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate DaysCurrentQuarterToDate 中的量值 hello DimDate 資料表  
  
1.  在 hello 模型設計師中，按一下 hello **DimDate**資料表。  
  
2.  在 hello 量值方格中，按一下 hello 左上方的空資料格。  
  
3.  Hello 公式列中輸入下列公式的 hello:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    請注意 hello 左上資料格現在包含量值名稱， **DaysCurrentQuarterToDate**，後面接著 hello 結果**92**。
    
      ![aas 第 6 課新增量值](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    不同於導出資料行，量值公式與您可以輸入 hello 量值名稱，後面接著冒號，後面接著 hello 公式的運算式。

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate DaysInCurrentQuarter 中的量值 hello DimDate 資料表  
  
1.  以 hello **DimDate**資料表仍為使用中 hello 量值方格中的 hello 模型設計師中，按一下 hello hello 您建立的量值下方的空資料格。  
  
2.  Hello 公式列中輸入下列公式的 hello:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    在前一個期間建立一個不完整期間與 hello 之間的比率。 hello 公式必須計算 hello hello 期間已經過的比例，並比較它 toohello 相同比例 hello 中前一個期間。 在這種情況下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供 hello 比例經過 hello 中目前的期間。  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate hello FactInternetSales 資料表中的 InternetDistinctCountSalesOrder 量值  
  
1.  按一下 hello **FactInternetSales**資料表。   
  
2.  按一下 hello **SalesOrderNumber**資料行標題。  
  
3.  Hello 工具列上，按一下 hello 向下一步 toohello 自動加總 (**∑**) 按鈕，然後再選取**DistinctCount**。  
  
    hello 自動加總功能自動建立 hello 選資料行使用 hello DistinctCount 標準彙總公式的量值。  
    
       ![aas 第 6 課新增量值 2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  在 hello 量值方格中，按一下 hello 新量值，然後在 hello**屬性**視窗，請在**量值名稱**，hello 量值重新命名過**InternetDistinctCountSalesOrder**。 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>toocreate hello FactInternetSales 資料表中的其他量值  
  
1.  使用 hello 自動加總功能，建立並命名下列量值的 hello:  

    |資料欄|量值名稱|自動加總 (∑)|公式|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|總和|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|總和|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|總和|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|總和|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|總和|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|總和|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|總和|=SUM([Freight])|  
  
2.  按一下空白儲存格在 hello 量值方格中，而藉由使用 hello 公式列中建立，並中順序的名稱 hello 下列量值：  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
針對 hello FactInternetSales 資料表所建立的量值也可以使用的 tooanalyze 重大財務資料，例如銷售額、 成本與 hello 使用者選取的篩選所定義的項目獲利率。  
  
## <a name="whats-next"></a>後續步驟
[第 7 課：建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。  

  
