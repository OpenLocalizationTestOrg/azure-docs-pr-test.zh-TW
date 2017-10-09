您現在可以使用 hello Azure 入口網站 toocreate 資料庫中的 hello 資料總管工具和集合。 

1. 在 hello Azure 入口網站，在 hello 左側瀏覽功能表中，按一下 **資料總管 （預覽）**。 

2. 在 hello**資料總管 （預覽）**刀鋒視窗中，按一下 **新集合**，然後提供下列資訊的 hello:

    ![hello Azure 入口網站的資料總管刀鋒伺服器](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    設定|建議的值|說明
    ---|---|---
    資料庫識別碼|工作|hello 新的資料庫名稱。 資料庫名稱必須包含從 1 到 255 個字元，且不能包含 /、\\、#、? 或尾端空格。
    集合識別碼|項目|hello 名稱為新的集合的。 集合名稱有 hello 相同字元的需求，資料庫識別碼。
    儲存體容量| 固定 (10 GB)|使用 hello 預設值。 此值為 hello hello 資料庫儲存容量。
    Throughput|400 RU|使用 hello 預設值。 如果您想要 tooreduce 延遲，您可以向上延展 hello 輸送量更新版本。
    資料分割索引鍵|/類別|資料分割索引鍵平均散發資料 tooeach 磁碟分割。 選取 hello 正確的資料分割索引鍵，請務必在建立高效能的集合。 詳細資訊，請參閱 toolearn[設計資料分割](../articles/cosmos-db/partition-data.md#designing-for-partitioning)。    
3. 您已經完成 hello 表單之後，請按一下**確定**。

資料檔案總管會顯示 hello 新資料庫與集合。 
