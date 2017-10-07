---
標題： aaa"Azure Analysis Services 教學課程的補充課程： 不完全階層 |Microsoft 文件"描述： 描述如何 toofix 不完全階層 hello Azure Analysis Services 教學課程中。
服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>補充課程 - 不完全階層

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這堂補充課程中，您可解決對不同層級包含空白值 (成員) 的階層進行樞紐分析時的常見問題。 例如，組織中部門經理和非部門經理同時為高階經理的直屬主管。 或者，由國家/地區-區域-城市組成的地理階層，其中有些城市缺少上層的州或省，例如華盛頓特區、梵蒂岡。 當階層具有空白的成員時，它通常會向下延伸 toodifferent，或不完全的層級。

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Hello 1400 相容性層級的表格式模型具有其他**隱藏成員**屬性階層。 hello**預設**設定假設任何層級沒有空白的成員。 hello**隱藏空白成員**設定排除 hello 階層時加入的空白成員 tooa 樞紐分析表或報表。  
  
本課程的估計時間 toocomplete: **20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
此補充課程主題是表格式模型教學課程的一部分。 在執行前 hello 工作這個補充課程，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。 

如果您已建立 hello AW Internet Sales 專案 hello 教學課程的一部分，您的模型尚未包含任何資料或不完全階層。 toocomplete 這個補充課程中，您必須先 toocreate hello 藉由新增某些其他資料表的問題，請建立關聯性、 導出資料行、 量值和新的組織階層。 該部分大約需要 15 分鐘。 然後，您可以取得 toosolve 在短短幾分鐘內。  

## <a name="add-tables-and-objects"></a>新增資料表和物件
  
### <a name="tooadd-new-tables-tooyour-model"></a>tooadd 新資料表 tooyour 模型
  
1.  在 [表格式模型總管] 中，依序展開 [資料來源]，然後以滑鼠右鍵按一下您的連線 > [匯入新資料表]。
  
2.  在 導覽器 中，選取 DimEmployee 和 FactResellerSales，然後按一下確定。

3.  在 [查詢編輯器] 中，按一下 [匯入]

4.  建立 hello 遵循[關聯性](../tutorials/aas-lesson-4-create-relationships.md):

    | 表 1           | 資料欄       | 篩選方向   | 表 2     | 資料欄      | 作用中 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 預設值            | DimDate     | 日期        | 是    |
    | FactResellerSales | DueDate      | 預設值            | DimDate     | 日期        | 否     |
    | FactResellerSales | ShipDateKey  | 預設值            | DimDate     | 日期        | 否     |
    | FactResellerSales | ProductKey   | 預設值            | DimProduct  | ProductKey  | 是    |
    | FactResellerSales | EmployeeKey  | tooBoth 資料表 | DimEmployee | EmployeeKey | 是    |

5. 在 hello **DimEmployee**資料表中，建立 hello 遵循[導出資料行](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **路徑** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  在 hello **DimEmployee**資料表中，建立[階層](../tutorials/aas-lesson-9-create-hierarchies.md)名為**組織**。 新增資料行中的順序 hello: **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。

7.  在 hello **FactResellerSales**資料表中，建立 hello 遵循[量值](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  使用[在 Excel 中的進行分析](../tutorials/aas-lesson-12-analyze-in-excel.md)tooopen Excel，並自動建立樞紐分析表。

9.  在**樞紐分析表欄位**，新增 hello**組織**hello 階層**DimEmployee**太資料表**列**，和 hello **ResellerTotalSales**量值從 hello **FactResellerSales**太資料表**值**。

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    您可以看到 hello 樞紐分析表中，是不完全的資料列顯示 hello 階層。 有許多資料列中顯示空白的成員。

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>toofix hello 藉由設定 hello 隱藏成員屬性不完全階層

1.  在 [表格式模型總管] 中，依序展開 [資料表] > [DimEmployee] > [階層] > [組織]。

2.  在 [屬性] > [隱藏成員] 中，選取 [隱藏空白成員]。 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  上一步是在 Excel 中重新整理 hello 樞紐分析表。 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    現在看起來好多了！

## <a name="see-also"></a>另請參閱   
[第 9 課：建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)  
[補充課程 - 動態安全性](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[補充課程 - 詳細資料列](../tutorials/aas-supplemental-lesson-detail-rows.md)  