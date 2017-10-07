---
標題： aaa"Azure Analysis Services 教學課程第 7 課： 建立關鍵效能指標 |Microsoft 文件"描述： 描述如何在 toocreate 關鍵效能指標 hello Azure Analysis Services 教學課程專案。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>第 7 課：建立關鍵效能指標

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂課中，您可以建立關鍵效能指標 (KPI)。 Kpi 是所定義的值使用的 toogauge 效能*基底*量值，針對*目標*由量值或絕對值定義的值。 在報表用戶端應用程式中，Kpi 可以商務專業人士提供快速簡便方式 toounderstand 商務成功或 tooidentify 趨勢的摘要。 詳細資訊，請參閱 toolearn [Kpi](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
本課程的估計時間 toocomplete: **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 6 課： 建立量值](../tutorials/aas-lesson-6-create-measures.md)。   
  
## <a name="create-key-performance-indicators"></a>建立關鍵效能指標  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate InternetCurrentQuarterSalesPerformance KPI  
  
1.  在 hello 模型設計師中，按一下 hello **FactInternetSales**資料表。  
  
2.  在 hello 量值方格中，按一下空白儲存格。  
  
3.  在 hello 上方公式列 hello 資料表中，輸入下列公式的 hello: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    此量值做為 hello hello KPI 的基底量值。  
  
4.  以滑鼠右鍵按一下 [InternetCurrentQuarterSalesPerformance] > [建立 KPI]。   
  
5.  在 hello 關鍵效能指標 (KPI) 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.1**。  
  
7.  在 [hello] 左側 （下） 滑動軸欄位中，輸入**1**，然後在 hello 右側 （上） 滑動軸欄位中，輸入**1.07**。  
  
8.  在**選取圖示樣式**、 選取 hello 菱形 （紅色）、 三角形 （黃色）、 圓形 （綠色） 圖示類型。
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > 請注意 hello 可展開**描述**hello 可用圖示樣式下方的標籤。 描述用於 hello 各種 KPI 元素 toomake 它們更容易識別用戶端應用程式。  
  
9. 按一下**確定**toocomplete hello KPI。  
  
    在 hello 量值方格中，請注意 hello 圖示下一步 toohello **InternetCurrentQuarterSalesPerformance**量值。 這個圖示表示此量值做為 KPI 的基準值。  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate InternetCurrentQuarterMarginPerformance KPI  
  
1.  在 hello 量值方格中的 hello **FactInternetSales**資料表中，按一下空白儲存格。  
  
2.  在 hello 上方公式列 hello 資料表中，輸入下列公式的 hello:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  以滑鼠右鍵按一下 [InternetCurrentQuarterMarginPerformance] > [建立 KPI]。  
  
4.  在 hello 關鍵效能指標 (KPI) 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.25**。   
  
5.  在 hello 左側 （下） 滑動軸欄位中，投影片直到 hello 欄位會顯示**0.8**，然後投影片 hello 在直到 hello 欄位會顯示，以滑鼠右鍵 （高） 滑動軸欄位，和**1.03**。  
  
6.  在**選取圖示樣式**hello 菱形 （紅色）、 三角形 （黃色）、 圓形 （綠色） 圖示類型，選取，然後按一下**確定**。  
  
## <a name="whats-next"></a>後續步驟
[第 8 課：建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)。
  
  
