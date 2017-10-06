---
標題： aaa"Azure Analysis Services 教學課程第 2 課： 取得資料 |Microsoft 文件"描述： 描述 tooget 和匯入資料如何 hello Azure Analysis Services 教學課程專案。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---

# <a name="lesson-2-get-data"></a>第 2 課：取得資料

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以在 SSDT tooconnect toohello AdventureWorksDW2014 範例資料庫、 選取資料、 預覽和篩選器，使用 取得資料並再匯入您的模型工作空間。  
  
「取得資料」可讓您從各種來源匯入資料︰Azure SQL Database、Oracle、Sybase、OData 摘要、Teradata、檔案等等。 您也可以使用 Power Query M 公式運算式來查詢資料。
  
本課程的估計時間 toocomplete: **10 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 1 課： 建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>建立連線  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate 連線 toohello AdventureWorksDW2014 資料庫  
  
1.  在 [表格式模型總管] 中，以滑鼠右鍵按一下 [資料來源] > [從資料來源匯入]。  
  
    這會啟動 取得資料，將引導您完成連接 tooa 資料來源。 如果您沒有看到表格式模型總管 中，在**方案總管 中**，連按兩下**Model.bim** tooopen hello 設計工具中的 hello 模型。 
    
    ![aas 第 2 課取得資料](../tutorials/media/aas-lesson2-getdata.png)
  
2.  在 [取得資料] 中，按一下 [資料庫] > [SQL Server 資料庫] > [連線]。  
  
3.  在 hello **SQL Server 資料庫**對話方塊，請在**伺服器**，輸入 hello hello hello AdventureWorksDW2014 資料庫的安裝所在的伺服器名稱，然後按一下**連接**。  

4.  出現提示時 tooenter 認證，需要 Analysis Services 會使用 tooconnect toohello 資料來源匯入和處理資料時的 toospecify hello 認證。 在 模擬模式 中，選取 模擬帳戶，輸入認證，然後按一下連線。 建議您使用的帳戶其中 hello 密碼尚未過期。

    ![aas 第 2 課帳戶](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > 使用 Windows 使用者帳戶和密碼提供 hello 連接 tooa 資料來源的最安全的方法。
  
5.  在導覽中，選取 hello **AdventureWorksDW2014**資料庫，然後再按一下**確定**。這會建立 hello 連線 toohello 資料庫。 
  
6.  在導覽中，選取 hello hello 下列資料表的核取方塊： **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**。  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
按一下 [確定] 之後，[查詢編輯器] 隨即開啟。 Hello 下一節，您可以選取只想 tooimport hello 資料。

  
## <a name="filter-hello-table-data"></a>篩選 hello 資料表的資料  
Hello AdventureWorksDW2014 範例資料庫中的資料表具有不必要 tooinclude 模型中的資料。 如果可能的話，您會想 toofilter 出 hello 模型所使用的不必要的資料 toosave 記憶體空間。 您篩選出部分 hello 資料表之資料行，所以未匯入至 hello 工作空間資料庫或 hello 模型資料庫之後已部署。 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>匯入之前 toofilter hello 資料表資料  
  
1.  在 [查詢編輯器] 中，選取 hello **DimCustomer**資料表。 在 hello 資料來源 （AdventureWorksDWQ2014 範例資料庫） 的 hello DimCustomer 資料表的檢視會顯示。 
  
2.  複選 (Ctrl + 按一下) **SpanishEducation**、**FrenchEducation**、**SpanishOccupation**、**FrenchOccupation**，按一下滑鼠右鍵，然後按一下移除資料行。 

    ![aas 第 2 課移除資料行](../tutorials/media/aas-lesson2-remove-columns.png)
  
    由於這些資料行的 hello 值相關的 tooInternet 銷售分析，沒有任何需要 tooimport 這些資料行。 去除不必要的資料行可讓您的模型變得更小且更有效率。  
  
4.  篩選其餘資料表移除下列資料行，每個資料表中的 hello hello:  
    
    **DimDate**
    
      |資料欄|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |資料欄|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |資料欄|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |資料欄|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |資料欄|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |資料欄|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>匯入 hello 選取資料表和資料行的資料  
現在，您已預覽並篩選掉不必要的資料，您可以匯入 hello 其他您想 hello 資料。 hello 精靈匯入 hello 資料表資料，以及資料表之間的任何關聯性。 Hello 模型中建立新的資料表和資料行並不會匯入您篩選掉的資料。  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>tooimport hello 選取資料表和資料行的資料  
  
1.  檢閱您的選擇。 如果一切看起來沒問題，請按一下 [匯入]。 hello 資料處理 對話方塊會顯示 hello 狀態正在從您的資料來源匯入至工作空間資料庫的資料。
  
    ![aas 第 2 課成功](../tutorials/media/aas-lesson2-success.png) 
  
2.  按一下 [關閉] 。  

  
## <a name="save-your-model-project"></a>儲存模型專案  
請務必 toofrequently 儲存模型專案。  
  
#### <a name="toosave-hello-model-project"></a>toosave hello 模型專案  
  
-   按一下 [檔案] > [全部儲存]。  
  
## <a name="whats-next"></a>後續步驟
[第 3 課：標記為日期資料表](../tutorials/aas-lesson-3-mark-as-date-table.md)。

  
  
