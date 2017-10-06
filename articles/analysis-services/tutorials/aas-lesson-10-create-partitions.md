---
標題： aaa"Azure Analysis Services 教學課程第 10 課： 建立資料分割 |Microsoft 文件"描述： 描述 toocreate hello Azure Analysis Services 教學課程專案中的資料分割。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>第 10 課：建立分割區

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以建立資料分割 toodivide hello FactInternetSales 資料表分成較小的邏輯部分可以是其他資料分割的處理 （重新整理） 獨立的。 根據預設，您在模型中包含每個資料表會有一個資料分割，其中包含所有 hello 資料表的資料行和資料列。 Hello FactInternetSales 資料表中，我們想 toodivide hello 資料依年份。hello 資料表的五年的每一個資料分割。 然後就可以獨立處理每個分割區。 詳細資訊，請參閱 toolearn[分割](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular)。 
  
本課程的估計時間 toocomplete: **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 9 課： 建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。  
  
## <a name="create-partitions"></a>建立分割區  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate hello FactInternetSales 資料表中的資料分割  
  
1.  在 [表格式模型總管] 中，展開 [資料表]，然後以滑鼠右鍵按一下 [FactInternetSales] > [分割區]。  
  
2.  在 [資料分割管理員] 中，按一下**複製**，然後變更太 hello 名稱**FactInternetSales2010**。
  
    因為要 hello 分割 tooinclude 那些資料列中的特定期間，hello 年度 2010，您必須修改 hello 查詢運算式。
  
4.  按一下**設計**tooopen 查詢編輯器，然後按一下hello **FactInternetSales2010**查詢。

5.  在預覽中，按一下向下箭號，在 hello hello **OrderDate**資料行標題，然後按一下**日期/時間篩選器** > **之間**。

    ![aas 第 10 課查詢編輯器](../tutorials/media/aas-lesson10-query-editor.png)

6.  在 hello 篩選的資料列 對話方塊中**顯示資料列，其中： OrderDate**，保留**之後或等於**，然後在 hello 日期欄位中，輸入**1/1/2010年**。 保留 hello**和**運算子選取，然後選取**之前**，然後在 hello 日期欄位中，輸入**2011 年 1 月 1 日**，然後按一下 **[確定]**。

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    請注意，在查詢編輯器的 APPLIED STEPS 中，您會看到另一個名為 Filtered Rows 步驟。 此篩選器是從 2010 tooselect 唯一訂單日期。

8.  按一下 [匯入] 。

    在 [資料分割管理員] 中，請注意 hello 運算式現在具有篩選資料列的額外子句的查詢。

    ![aas 第 10 課查詢](../tutorials/media/aas-lesson10-query.png)
  
    這個陳述式會指定此分割區應該包括只有 hello 資料 hello OrderDate 所在 hello 2010 日曆年度 hello 資料列篩選的子句中所指定資料列中。  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate hello 2011 年的資料分割  
  
1.  在 hello 資料分割清單中，按一下 hello **FactInternetSales2010**您所建立，資料分割，然後按一下**複製**。  Hello 磁碟分割名稱變更太**FactInternetSales2011**。 

    您不需要 toouse 查詢編輯器 toocreate 新的資料列篩選的子句。 因為您可以建立一份 hello 查詢 2010，您只需要 toodo 是 2011 在 hello 查詢中有些微變更。
  
2.  在**查詢運算式**、 為了讓這個資料分割 tooinclude 只有這些資料列中的 hello 2011 年、 取代 hello 子句篩選資料列中的 hello 年**2011年**和**2012**分別，例如：  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>針對 2013、 2012年和 2014 toocreate 分割區。  
  
- 請遵循 hello 先前步驟中，為 2012年、 2013年和 2014，變更該年份的 hello 年 hello 篩選資料列子句 tooinclude 唯一資料列中建立資料分割。 
  

## <a name="delete-hello-factinternetsales-partition"></a>刪除 hello FactInternetSales 磁碟分割
現在，您會有每年的資料分割，您可以刪除 hello FactInternetSales 磁碟分割。處理資料分割時，選擇所有的程序時，請避免重疊。

#### <a name="toodelete-hello-factinternetsales-partition"></a>toodelete hello FactInternetSales 磁碟分割
-  按一下 hello FactInternetSales 磁碟分割，然後再按一下**刪除**。



## <a name="process-partitions"></a>處理分割區  
在 [資料分割管理員] 中，請注意 hello**最後一個處理**hello 建立的顯示絕對不會處理這些資料分割的新資料分割的每個資料行。 當您建立資料分割時，則您應該執行處理資料分割或處理程序的資料表作業 toorefresh hello 資料，這些資料分割中。  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello FactInternetSales 資料分割  
  
1.  按一下**確定**tooclose 資料分割管理員。  
  
2.  按一下 hello **FactInternetSales**資料表，然後按一下 hello**模型**功能表 >**程序** > **處理資料分割**。  
  
3.  在 hello 處理資料分割對話方塊中，確認**模式**設定得**處理預設**。  
  
4.  選取 hello hello 核取**程序**每 hello 五個資料行資料分割，您所建立，然後再按一下**確定**。  

    ![aas 第 10 課處理分割區](../tutorials/media/aas-lesson10-process-partitions.png)
  
    如果系統提示您輸入模擬認證，請輸入 hello Windows 使用者名稱和您在第 2 課中指定的密碼。  
  
    hello**資料處理**對話方塊隨即出現並顯示每個資料分割的處理序詳細資料。 請注意，傳送給每個分割區的資料列數目都不同。 每個資料分割包含 hello 年 hello hello SQL 陳述式中 WHERE 子句中指定的資料列。 當處理完成時，請繼續並關閉 hello 資料處理 對話方塊。  
  
    ![aas 第 10 課處理完成](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>後續步驟
下一課中移 toohello:[第 11 課： 建立角色](../tutorials/aas-lesson-11-create-roles.md)。 
