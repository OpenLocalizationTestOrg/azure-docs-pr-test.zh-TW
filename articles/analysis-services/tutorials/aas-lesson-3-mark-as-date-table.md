---
標題： aaa"Azure Analysis Services 教學課程第 3 課： 標記為日期資料表 |Microsoft 文件"描述： 描述如何 toomark 日期資料表 hello Azure Analysis Services 教學課程專案中。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>第 3 課：標記為日期資料表

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在「第 2 課：取得資料」中，您已匯入名為 DimDate 的維度資料表。 雖然此資料表在您的模型中名為 DimDate，但可以也稱為「日期資料表」，因為它包含日期和時間資料。  
  
每當您使用 DAX 時間智慧函式時 (像是稍後您建立量值時)，您必須指定一些屬性，其中包括「日期資料表」和該資料表中的唯一識別碼「日期資料行」。
  
在這一課，您將標示為 hello hello DimDate 資料表*日期資料表*和 hello 日期資料行 （在 hello Date 資料表） 做為 hello*日期資料行*（唯一識別碼）。  

Hello 日期資料表和日期資料行標示之前，它會是您的模型更容易 toounderstand 有點例行性 toomake 恰好 toodo。 請注意，在 hello DimDate 資料表的資料行**FullDateAlternateKey**。 此資料行包含一個資料列包含 hello 資料表中每個日曆年度中每一天。 您在量值公式和報告中常會用到此資料行。 但是，FullDateAlternateKey 並不是此資料行的理想識別項。 您將它重新命名過**日期**，讓它更容易 tooidentify，並在公式中包含。 可能的話，它是個不錯的主意 toorename 物件如資料表和資料行 toomake 它們更容易 tooidentify SSDT 和用戶端報表應用程式，例如 Power BI 與 Excel 中的。 
  
本課程的估計時間 toocomplete:**三分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 2 課： 取得資料](../tutorials/aas-lesson-2-get-data.md)。 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename hello FullDateAlternateKey 資料行

1.  在 hello 模型設計師中，按一下 hello **DimDate**資料表。

2.  按兩下 hello hello 標頭**FullDateAlternateKey**資料行，然後重新命名過**日期**。

  
### <a name="tooset-mark-as-date-table"></a>tooset 標記為日期資料表  
  
1.  選取 hello**日期**資料行，然後在 hello**屬性**視窗底下**資料型別**，請確定**日期**已選取。  
  
2.  按一下 hello**資料表**功能表，然後按一下**日期**，然後按一下**標記為日期資料表**。  
  
3.  在 hello**標記為日期資料表**對話方塊中的，在 hello**日期**清單方塊中，選取 hello**日期**hello 唯一識別碼資料行。 依預設通常會選取它。 按一下 [確定] 。 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>後續步驟
[第 4 課：建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。
  
