---
title: "使用 Java 的 Azure Cosmos DB 圖形資料庫 aaaCreate |Microsoft 文件"
description: "使用 Java 程式碼範例中，您可以使用 Gremlin Azure Cosmos DB 中使用 tooconnect tooand 查詢圖形資料的呈現。"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB： 建立圖表資料庫使用 Java 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門建立圖形 Azure Cosmos DB 資料庫使用 hello Azure 入口網站的工具。 本快速入門也會顯示如何 tooquickly 建立 Java 主控台應用程式使用圖形資料庫使用 hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver)驅動程式。 本快速入門中的 hello 指示之後只能在能夠執行 Java 任何作業系統上。 本快速入門能讓您熟悉建立和修改在 hello UI 或以程式設計的方式，無論是您的喜好設定的圖形資源。 

## <a name="prerequisites"></a>必要條件

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * 在 Ubuntu，執行`apt-get install default-jdk`tooinstall hello JDK。
    * 為確定 tooset hello JAVA_HOME 環境變數 toopoint toohello hello JDK 安裝的資料夾。
* [下載](http://maven.apache.org/download.cgi)和[安裝 ](http://maven.apache.org/install.html) [Maven](http://maven.apache.org/) 二進位封存檔
    * 您可以執行 Ubuntu， `apt-get install maven` tooinstall Maven。
* [Git](https://www.git-scm.com/)
    * 您可以執行 Ubuntu， `sudo apt-get install git` tooinstall Git。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

您可以建立圖表資料庫之前，您需要 toocreate Gremlin （圖形） 資料庫帳戶與 Azure Cosmos DB。

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>新增圖形

您現在可以使用 hello 資料總管工具 hello Azure 入口網站 toocreate 圖形資料庫中。 

1. 在 hello Azure 入口網站，在 hello 左側瀏覽功能表中，按一下 **資料總管 （預覽）**。 
2. 在 hello**資料總管 （預覽）**刀鋒視窗中，按一下**新圖形**，然後使用下列資訊的 hello hello 頁面中填入：

    ![在 hello Azure 入口網站中的資料總管](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    設定|建議的值|說明
    ---|---|---
    資料庫識別碼|sample-database|hello 新的資料庫識別碼。 資料庫名稱的長度必須介於 1 到 255 個字元，且不能包含 `/ \ # ?` 或尾端空格。
    圖形識別碼|sample-graph|新的圖形的 hello 識別碼。 圖形名稱具有 hello 相同字元做為資料庫 id 的需求。
    儲存體容量| 10 GB|保留 hello 預設值。 這是 hello hello 資料庫儲存容量。
    Throughput|400 RU|保留 hello 預設值。 您可以向上延展 hello 輸送量稍後如果您想要 tooreduce 延遲。
    資料分割索引鍵|保留空白|為了 hello 本快速入門，保留 hello 資料分割索引鍵為空白。

3. 一旦填寫 hello 表單，按一下 **確定**。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們複製從 github 設定 hello 連接字串，並執行它的圖形應用程式。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello`Program.java`從 hello \src\GetStarted 資料夾檔案，並尋找這行程式碼。 

* hello Gremlin`Client`初始化中的 hello 組態從`src/remote.yaml`。

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* 一系列的 Gremlin 步驟會執行使用 hello`client.submit`方法。

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

1. 開啟 hello src/remote.yaml 檔案。 

3. 填寫您*主機*， *username*，和*密碼*hello src/remote.yaml 檔案中的值。 hello 的其餘 hello 設定，不需要變更 toobe。

    設定|建議的值|說明
    ---|---|---
    主機|[***.graphs.azure.com]|請參閱本表格後的 hello 螢幕擷取畫面。 此值為 hello Gremlin URI 的 hello Azure 入口網站，以方括號，以 hello 尾端 hello [概觀] 頁面上： 443 / 已移除。<br><br>此值也可以擷取從 hello 金鑰 索引標籤，移除 https://、 變更文件 toographs 並移除尾端 hello 使用 hello URI 值： 443 /。
    使用者名稱|/dbs/sample-database/colls/sample-graph|hello hello 形式的資源`/dbs/<db>/colls/<coll>`其中`<db>`是現有的資料庫名稱和`<coll>`是現有的集合名稱。
    密碼|您的主要金鑰|請參閱本表格後續 hello 第二個螢幕擷取畫面。 這個值會是 hello 的您可以擷取 hello 金鑰 頁面上 hello 主要金鑰 方塊中的 Azure 入口網站的主要金鑰。 複製 hello 使用 hello [複製] 按鈕上 hello hello 方塊右邊的值。

    Hello 主機值，複製 hello **Gremlin URI**值從 hello**概觀**頁面。 如果是空的請參閱 hello 之前建立 hello Gremlin URI 從 hello 金鑰刀鋒視窗的相關資料表中的 hello 主機資料列中的 hello 指示。
![Hello Azure 入口網站 hello 概觀 頁面上檢視與複製 hello Gremlin URI 值](./media/create-graph-java/gremlin-uri.png)

    Hello 密碼值，複製 [hello**主索引鍵**從 hello**金鑰**刀鋒視窗：![主索引鍵 hello Azure 入口網站中的檢視與複製金鑰] 頁面](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>執行 hello 主控台應用程式

1. 在 hello git 終端機視窗， `cd` toohello azure-cosmos-db-graph-java-getting-started 資料夾。

2. 在 hello git 終端機視窗，輸入`mvn package`tooinstall hello 需要 Java 封裝。

3. Hello git 終端機視窗，在執行`mvn exec:java -D exec.mainClass=GetStarted.Program`在 hello 終端機視窗 toostart Java 應用程式。

hello 終端機視窗會顯示 hello 頂點加入 toohello 圖形。 Hello 程式完成之後，請切換後 toohello Azure 入口網站在網際網路瀏覽器中。 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>檢閱並新增範例資料

您現在可以移回 tooData 總管，並查看 hello 頂點加入 toohello 圖形，並加入其他資料點。

1. 在資料總管 中，展開 hello**範例資料庫**/**範例圖形**，按一下 **圖形**，然後按一下**套用篩選**. 

   ![Hello Azure 入口網站中，資料檔案總管中建立新文件](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. 在 hello**結果**清單中，您會發現 hello 新使用者加入 toohello 圖形。 選取**ben**並確認他已連線 toorobin 的注意。 您可以在 hello 圖表總管上移動 hello 頂點，放大和縮小，並展開 hello 圖表總管介面的 hello 大小。 

   ![Hello Azure 入口網站中的 hello 圖形中的資料檔案總管中的新端點](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. 讓我們加入一些新的使用者 toohello 圖形使用 hello 資料總管。 按一下 hello**新頂點**按鈕 tooadd 資料 tooyour 圖形。

   ![Hello Azure 入口網站中，資料檔案總管中建立新文件](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. 輸入的標籤*人員*然後輸入的 hello 下列索引鍵和值 toocreate hello 第一個頂點 hello 圖形中的。 請注意，您可以在圖形中為每個人建立獨特的屬性。 只有 hello 識別碼索引鍵為必要項目。

    key|value|注意事項
    ----|----|----
    id|ashley|hello hello 頂點的唯一識別碼。 如果您未指定識別碼，系統會為您產生一個。
    gender|female| 
    tech | java | 

    > [!NOTE]
    > 在本快速入門中，我們會建立非資料分割集合。 不過，如果您藉由指定資料分割索引鍵 hello 集合建立期間建立資料分割的集合，則您需要 tooinclude hello 資料分割索引鍵做為索引鍵中每個新的頂點。 

5. 按一下 [確定] 。 您可能需要 tooexpand 螢幕 toosee**確定**hello 底部囉 」 畫面上。

6. 再次按一下 [新增頂點] 並新增額外的新使用者。 輸入的標籤*人員*然後輸入 hello 下列索引鍵和值：

    key|value|注意事項
    ----|----|----
    id|rakesh|hello hello 頂點的唯一識別碼。 如果您未指定識別碼，系統會為您產生一個。
    gender|male| 
    school|MIT| 

7. 按一下 [確定] 。 

8. 按一下**套用篩選**hello 預設值`g.V()`篩選器。 所有 hello 使用者現在會顯示在 hello**結果**清單。 當您加入更多資料，您可以使用篩選器 toolimit 您的結果。 根據預設，使用資料總管`g.V()`tooretrieve 所有頂點圖形，但您可以都變更該 tooa 不同[graph 查詢](tutorial-query-graph.md)，例如`g.V().count()`，tooreturn JSON 格式的 hello 圖形中的所有 hello 頂點的計數。

9. 現在我們可以連線 rakesh 和 ashley。 請確定**ashley** hello 中選取**結果**清單，然後按一下 hello [編輯] 按鈕旁邊太**目標**上右下方。 您可能需要 toowiden 您視窗 toosee hello**屬性**區域。

   ![將頂點圖形中的 hello 目標變更](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. 在 [hello**目標**方塊中，輸入*rakesh*，在 hello**邊緣標籤**方塊中，輸入*知道*，然後按一下hello] 核取方塊。

   ![在 [資料總管] 中新增 ashley 與 rakesh 之間的連線](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. 現在選取**rakesh** hello 結果清單和 ashley 和 rakesh 是否已連線，請參閱。 

   ![[資料總管] 中連線的兩個頂點](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    您也可以使用資料總管 toocreate 預存程序，Udf，觸發程序 tooperform 伺服器端商務邏輯也做為標尺的輸送量。 資料總管會公開所有 hello 程式設計的內建資料存取提供 hello Api，但提供讓您輕鬆存取 tooyour 資料 hello Azure 入口網站中。



## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟： 

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管 中，而圖形，並執行應用程式。 您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。 

> [!div class="nextstepaction"]
> [使用 Gremlin 進行查詢](tutorial-query-graph.md)

