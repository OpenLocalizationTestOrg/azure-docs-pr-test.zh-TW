## <a name="repeatability-during-copy"></a>在複製期間的重複性
當複製資料 tooAzure SQL/SQL Server 從其他資料存放一個需求 tookeep 重複性注意 tooavoid 非預期的結果。 

複製資料 tooAzure SQL/SQL Server 資料庫，複製活動會依預設附加 hello 資料集 toohello 接收資料表預設。 例如，當複製資料，資料來源的 CSV （逗號分隔值） 檔案包含兩個記錄 tooAzure SQL/SQL Server 資料庫，這會是看起來像哪些 hello 資料表：

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

假設您在原始程式檔和更新的 hello 數量的向下 Tube 從 2 too4 找到錯誤 hello 原始程式檔中。 如果您重新執行 hello 資料配量，該期間內，您會看到兩個新的記錄會附加 tooAzure SQL/SQL Server 資料庫。 下面的 hello 假設 hello hello 資料表中的資料行都沒有 hello 主索引鍵條件約束。

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid，您必須利用以下 2 的機制，如下所示的 hello toospecify UPSERT 語意。

> [!NOTE]
> 配量可以重新執行自動 Azure Data Factory 中根據指定的 hello 重試原則。
> 
> 

### <a name="mechanism-1"></a>機制 1
您可以利用**sqlWriterCleanupScript**屬性 toofirst 執行配量時，請執行清理動作。 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

hello 清除指令碼就會執行第一個複製指定的配量會刪除 hello SQL 資料表對應 toothat 配量的 hello 資料的期間。 hello 活動接著會插入 hello 資料 hello SQL 資料表。 

如果 hello 配量是現在重新執行，則您會發現 hello 數量會更新為所需。

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

假設 hello 一般墊圈記錄被移除了 hello 原始 csv。 然後重新執行 hello 配量會產生下列結果 hello: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
新的執行任何動作必須 toobe 完成。 hello 複製活動已執行 hello 清除指令碼 toodelete hello 對應的資料為該扇區。 然後輸入 hello 讀取 hello csv （可再包含只有 1 筆記錄） 並插入 hello 資料表。 

### <a name="mechanism-2"></a>機制 2
> [!IMPORTANT]
> 目前 Azure SQL 資料倉儲不支援 sliceIdentifierColumnName。 

另一個機制 tooachieve 重複性，是由專用的資料行 (**sliceIdentifierColumnName**) 在 hello 為目標資料表。 Azure Data Factory tooensure hello 來源和目的地保持同步處理會使用這個資料行。 這個方法的效果時變更，或定義 hello 目的地 SQL 資料表結構描述的彈性。 

重複性基於 Azure Data Factory 會使用這個資料行和 hello 程序在 Azure Data Factory 不會進行任何結構描述變更 toohello 資料表。 方式 toouse 這種方法：

1. Hello 目的地 SQL 資料表中定義類型的二進位 (32) 的資料行。 此資料行不應該有任何條件約束。 此範例中我們將這個資料行命名為 'ColumnForADFuseOnly'。
2. 使用它 hello 複製活動中，如下所示：
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Azure Data Factory 會擴展這個資料行會根據其 tooensure hello 來源和目的地保持同步。 hello 這個資料行值不應該使用這個環境之外 hello 使用者。 

類似 toomechanism 1，複製活動便會自動清除 hello 從 hello 目的地 SQL 資料表配量，然後執行正常 hello 複製活動的 hello 資料第一次從該扇區的來源 toodestination tooinsert hello 資料。 

