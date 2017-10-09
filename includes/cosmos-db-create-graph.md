您現在可以使用 hello 資料總管工具 hello Azure 入口網站 toocreate 圖形資料庫中。 

1. 在 hello Azure 入口網站，在 hello 左側瀏覽功能表中，按一下 **資料總管 （預覽）**。 
2. 在 hello**資料總管 （預覽）**刀鋒視窗中，按一下**新圖形**，然後使用下列資訊的 hello hello 頁面中填入。

    ![在 hello Azure 入口網站中的資料總管](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    設定|建議的值|說明
    ---|---|---
    資料庫識別碼|sample-database|hello 新的資料庫識別碼。 資料庫名稱的長度必須介於 1 到 255 個字元，且不能包含 `/ \ # ?` 或尾端空格。
    圖形識別碼|sample-graph|新的圖形的 hello 識別碼。 圖形名稱具有 hello 相同字元做為資料庫 id 的需求。
    儲存體容量| 10 GB|保留 hello 預設值。 這是 hello hello 資料庫儲存容量。
    Throughput|400 RU|保留 hello 預設值。 您可以向上延展 hello 輸送量稍後如果您想要 tooreduce 延遲。
    資料分割索引鍵|/userid|資料分割索引鍵，將會平均分散資料 tooeach 磁碟分割。 選取正確資料分割索引鍵，請務必在建立高效能的 hello 繪製，深入了解在[設計資料分割](../articles/cosmos-db/partition-data.md#designing-for-partitioning)。

3. 一旦填寫 hello 表單，按一下 **確定**。
