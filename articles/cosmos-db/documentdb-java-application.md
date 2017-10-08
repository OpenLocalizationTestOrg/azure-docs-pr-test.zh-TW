---
title: "aaaJava 應用程式開發人員教學課程使用 Azure Cosmos DB |Microsoft 文件"
description: "此 Java web 應用程式教學課程會示範如何 toouse hello Azure Cosmos DB hello DocumentDB API toostore 及和 Azure 網站上主控的 Java 應用程式存取資料。"
keywords: "應用程式開發、資料庫教學課程、java 應用程式、java web 應用程式教學課程、documentdb、azure、Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>建置 Java web 應用程式使用 Azure Cosmos DB 和 hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

此 Java web 應用程式教學課程會示範如何 toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務 toostore 及存取資料，從裝載於 Azure App Service Web 應用程式的 Java 應用程式。 在本主題中，您將了解：

* 如何 toobuild 在 Eclipse 中的基本 JavaServer 頁面 (JSP) 應用程式。
* 以 hello Azure Cosmos DB toowork 服務使用 hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)。

此 Java 應用程式教學課程會示範影響工作以 web 為基礎的 toocreate 工作管理應用程式，可讓您 toocreate、 擷取、 並將標記為完成，hello 下列影像所示。 每個 hello ToDo 清單中的 hello 工作會儲存為 Azure Cosmos DB 中的 JSON 文件。

![我的待辦事項清單 Java 應用程式](./media/documentdb-java-application/image1.png)

> [!TIP]
> 本應用程式開發教學課程假設您先前已有使用 Java 的經驗。 如果您是新 tooJava 或 hello[必要條件工具](#Prerequisites)，我們建議您下載完整的 hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)專案從 GitHub 及建置使用[hello 這個 hello 結尾的指示發行項](#GetProject)。 一旦建立它，您可以檢閱 hello 文章 toogain 深入了解 hello hello hello 專案內容中的程式碼。  
> 
> 

## <a id="Prerequisites"></a>針對此 Java Web 應用程式教學課程的必要條件
在開始此應用程式開發人員教學課程之前，您必須擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)

    或

    Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。
* [Eclipse IDE for Java EE Developers。](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [已啟用某個 Java Runtime Environment (例如 Tomcat 或 Jetty) 的 Azure 網站。](../app-service-web/web-sites-java-get-started.md)

如果您要安裝這些工具 hello 第一次，coreservlets.com 提供 hello hello 快速入門 區段中的安裝程序的逐步解說，其[教學課程： 安裝 TomCat7 和使用 Eclipse 向](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html)發行項。

## <a id="CreateDB"></a>步驟 1：建立 Azure Cosmos DB 帳戶
我們將從建立 Azure Cosmos DB 帳戶開始著手。 如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立 hello Java JSP 應用程式](#CreateJSP)。

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>步驟 2： 建立 hello Java JSP 應用程式
toocreate hello JSP 應用程式：

1. 首先，我們將從建立 Java 專案開始。 啟動 Eclipse，依序按一下 [檔案]、[新增] 和 [動態 Web 專案]。 如果您沒有看到**動態 Web 專案**列為可用的專案，請執行下列 hello： 按一下**檔案**，按一下 **新增**，按一下 **專案**...，展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。
   
    ![JSP Java 應用程式開發](./media/documentdb-java-application/image10.png)
2. 輸入專案名稱在 hello**專案名稱**] 方塊中，在 hello**目標執行階段**下拉式選單，選擇性地選取 [值 (例如 Apache Tomcat v7.0)，然後按一下**完成**. 選取目標執行階段可讓您 toorun 您在本機透過 Eclipse 的專案。
3. 在 Eclipse 中，在 hello [專案總管] 檢視中，展開您的專案。 在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。
4. 在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**。 保留 hello 父資料夾為**WebContent**示 hello 遵循圖例，然後按一下**下一步**。
   
    ![建立新的 JSP 檔案 - Java Web 應用程式教學課程](./media/documentdb-java-application/image11.png)
5. 在 hello**選取 JSP 範本**對話方塊中的，為了這個教學課程，請選取在 hello**新增 JSP 檔案 (html)**，然後按一下**完成**。
6. 在 Eclipse 中，開啟 hello index.jsp 檔案，當新增文字 toodisplay **Hello World ！** 在現有的 hello<body>項目。 您已更新<body>內容應該看起來像下列程式碼的 hello:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. 儲存 hello index.jsp 檔案。
8. 如果您在步驟 2 中設定目標執行階段，您可以按一下**專案**然後**執行**toorun JSP 應用程式在本機上：
   
    ![Hello World – Java 應用程式教學課程](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>步驟 3： 安裝 hello DocumentDB Java SDK
hello hello DocumentDB Java SDK 和其相依性中的最簡單方式 toopull 是透過[Apache Maven](http://maven.apache.org/)。

toodo，您將需要 tooconvert 專案 tooa maven 專案藉由完成下列步驟的 hello:

1. 以滑鼠右鍵按一下 hello 專案總管 中的專案中，按一下**設定**，按一下 **轉換 tooMaven 專案**。
2. 在 hello**建立新的 POM**視窗中，接受 hello 預設值，然後按一下**完成**。
3. 在**Project Explorer**，開啟 hello pom.xml 檔案。
4. 在 hello**相依性**索引標籤上，在 hello**相依性** 窗格中，按一下 **新增**。
5. 在 hello**選取相依性**視窗中，執行下列 hello:
   
   * 在 hello**群組識別碼**方塊中，輸入 com.microsoft.azure。
   * 在 hello**成品 Id**方塊中，輸入 azure documentdb。
   * 在 hello**版本**方塊中，輸入 1.5.1。
     
   ![安裝 DocumentDB Java 應用程式 SDK](./media/documentdb-java-application/image13.png)
     
   * 群組識別碼和成品 Id 加入 hello 相依 XML 或文字編輯器透過直接 toohello pom.xml:
     
        <dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency>
6. 按一下**確定**Maven 安裝 hello DocumentDB Java SDK。
7. 儲存 hello pom.xml 檔案。

## <a id="UseService"></a>步驟 4： 使用 Java 應用程式中的 hello Azure Cosmos DB 服務
1. 首先，我們定義 TodoItem.java hello TodoItem 物件：
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    在此專案中，我們會使用[專案 Lombok](http://projectlombok.org/) toogenerate hello 建構函式、 getter、 setter 和產生器。 或者，您可以手動撰寫此程式碼，或有 hello IDE 產生它。
2. tooinvoke hello Azure Cosmos 資料庫服務，您必須具現化新**DocumentClient**。 一般而言，最好是最佳 tooreuse hello **DocumentClient** -而不是比建構新的用戶端針對每個後續的要求。 我們可以換行中的 hello 用戶端連線，重複使用 hello 用戶端**DocumentClientFactory**。 DocumentClientFactory.java，在您需要 toopaste hello URI 與主索引鍵的值儲存在 tooyour 剪貼簿[步驟 1](#CreateDB)。 將 [YOUR\_ENDPOINT\_HERE] 以您的 URI 取代，並將 [YOUR\_KEY\_HERE] 以您的主要金鑰取代。
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. 現在讓我們來建立資料存取物件 (DAO) tooabstract 保存我們 ToDo 項目 tooAzure Cosmos DB。
   
    若要 toosave ToDo 項目 tooa 集合，hello 用戶端必須 tooknow 哪一個資料庫與集合 toopersist 太 （做為參考的自我連結）。 一般情況下，它是最佳的 toocache hello 資料庫與集合盡可能 tooavoid 額外往返 toohello 資料庫。
   
    hello 下列程式碼說明如何 tooretrieve 我們的資料庫，如果它存在，或如果不存在，請建立一個新的集合：
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. hello 下一個步驟為 toowrite toohello 集合中的某些程式碼 toopersist hello TodoItems。 在此範例中，我們將使用[Gson](https://code.google.com/p/google-gson/) tooserialize 和還原序列化 TodoItem 純舊 Java 物件 (POJOs) tooJSON 文件。
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. 與 Azure Cosmos DB 資料庫和集合相同，文件也會由自我連結參照。 hello 下列 helper 函式可讓我們擷取文件的其他屬性 (例如"id")，而不是自我連結：
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. 我們可以在步驟 5 tooretrieve TodoItem JSON 文件中使用識別碼 hello helper 方法，然後將它還原序列化 tooa POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. 我們也可以使用 hello DocumentClient tooget 集合或使用 DocumentDB SQL TodoItems 的清單：
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. 有許多方式 tooupdate 文件以 hello DocumentClient。 在 Todo 清單應用程式中，我們想要 toobe 無法 tootoggle 是否已完成的 TodoItem。 這可以藉由更新 hello hello 文件中的 「 完成 」 屬性來達成：
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. 最後，我們想 hello 能力 toodelete TodoItem 從我們的清單。 toodo，我們可以使用我們稍早所說明的 hello helper 方法 tooretrieve hello 自我連結，然後告訴 hello 用戶端 toodelete 它：
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>步驟 5： 接線 hello hello Java 應用程式開發專案的其餘部分一起
我們已經完成 hello 有趣 bits-剩下的是 toobuild 快速的使用者介面，和裝設 tooour DAO。

1. 首先，讓我們開始建置我們 DAO 控制器 toocall:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    在更複雜的應用程式，hello 控制器可能包含複雜的商務邏輯 hello DAO 之上。
2. 接下來，我們將建立 servlet tooroute HTTP 要求 toohello 控制器：
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. 我們需要 web 使用者介面 toodisplay toohello 使用者。 讓我們重新撰寫 hello index.jsp 我們稍早建立：
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. 最後，某些用戶端 JavaScript tootie hello web 使用者介面和寫 hello servlet 一起：
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. 好極了！ 現在，剩下的是 tootest hello 應用程式。 在本機執行 hello 應用程式，並加入一些 Todo 項目填入 hello 項目名稱和類別目錄，然後按一下**加入工作**。
6. Hello 項目出現時，您可以更新是否已完成切換 hello 核取方塊，然後按一下**更新工作**。

## <a id="Deploy"></a>步驟 6： 部署您的 Java 應用程式 tooAzure 網站
Azure 網站讓部署 Java 應用程式變得相當簡單，您只需將應用程式匯出成 WAR 檔案，然後透過原始檔控制 (例如 Git) 或 FTP 上傳它即可。

1. tooexport 應用程式為 WAR 檔案，以滑鼠右鍵按一下您的專案中**專案總管**，按一下 **匯出**，然後按一下 **WAR 檔案**。
2. 在 hello**匯出 WAR**視窗中，執行下列 hello:
   
   * 在 hello Web 專案中，輸入 azure documentdb 的 java 範例。
   * 在 hello 目的地方塊中，選擇目的地 toosave hello WAR 檔案。
   * 按一下 [完成] 。
3. 既然您手中有 WAR 檔案，您可以直接將它上傳 tooyour Azure 網站的**webapps**目錄。 上傳 hello 檔案的指示，請參閱[新增 App Service Web 應用程式的 Java 應用程式 tooAzure](../app-service-web/web-sites-java-add-app.md)。
   
    一旦 hello WAR 檔案已上傳的 toohello webapps 目錄，hello 執行階段環境會偵測您已新增，並會自動載入。
4. tooview 成品，瀏覽 toohttp://YOUR\_網站\_NAME.azurewebsites.net/azure-java-sample/ 並開始將您的工作 ！

## <a id="GetProject"></a>從 GitHub 取得 hello 專案
在本教學課程的所有 hello 範例都包含在 hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub 上的專案。 tooimport hello todo 專案 Eclipse 中，請確定您有 hello 軟體和 hello 中列出的資源[必要條件](#Prerequisites)區段，然後執行下列 hello:

1. 安裝 [專案 Lombok](http://projectlombok.org/)。 Lombok 是使用的 toogenerate 建構函式、 getter、 setter hello 專案中。 一旦您已下載 hello lombok.jar 檔案，請按兩下該 tooinstall 它，或從 hello 命令列安裝它。
2. 如果 Eclipse 已開啟，關閉它，並重新啟動它 tooload Lombok。
3. 在 Eclipse 中，在 hello**檔案**功能表上，按一下 **匯入**。
4. 在 hello**匯入**視窗中，按一下**Git**，按一下**從 Git 專案**，然後按一下**下一步**。
5. 在 hello**選取儲存機制來源**畫面上，按一下**複製 URI**。
6. 在 hello**來源 Git 儲存機制**畫面中 hello **URI**方塊、 輸入 https://github.com/Azure-Samples/java-todo-app.git，，然後按一下**下一步**。
7. 在 hello**分支選取**畫面上，確認**主要**已選取，然後按一下**下一步**。
8. 在 hello**本機目的地**畫面上，按一下**瀏覽**tooselect hello 儲存機制可複製、，然後按一下資料夾**下一步**。
9. 在 hello**選取匯入專案精靈 toouse**畫面上，確認**匯入現有專案**已選取，然後按一下**下一步**。
10. 在 hello**匯入專案**螢幕、 取消選取 hello **DocumentDB**專案，然後再按一下**完成**。 hello DocumentDB 專案包含 hello Azure Cosmos DB Java SDK，我們將會改為加入做為相依性。
11. 在**Project Explorer**、 瀏覽 tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java 及 hello 主機和 MASTER_KEY 值取代為 hello URI 和主索引鍵您 Azure Cosmos DB 帳戶，然後儲存 hello 檔案。 如需詳細資訊，請參閱[步驟 1。建立 Azure Cosmos DB 資料庫帳戶](#CreateDB)。
12. 在**專案總管 中**，以滑鼠右鍵按一下 hello **azure documentdb 的 java 範例**，按一下**組建路徑**，然後按一下**設定組建路徑**.
13. 在 hello **Java 組建路徑**畫面上，hello 右窗格中，選取 hello**文件庫**索引標籤，然後再按一下**新增外部 Jar**。 瀏覽 toohello hello lombok.jar 檔案位置，然後按一下**開啟**，然後按一下**確定**。
14. 使用步驟 12 tooopen hello**屬性**視窗一次，然後在 hello 左窗格按一下**目標執行階段**。
15. Hello 上**目標執行階段**畫面上，按一下**新增**，選取**Apache Tomcat v7.0**，然後按一下**確定**。
16. 使用步驟 12 tooopen hello**屬性**視窗一次，然後在 hello 左窗格按一下**專案 Facet**。
17. 在 hello**專案 Facet**畫面上，選取**動態 Web 模組**和**Java**，然後按一下 **確定**。
18. 在 hello**伺服器**底部 hello 囉 」 畫面索引標籤上，以滑鼠右鍵按一下**Tomcat v7.0 伺服器在 localhost** ，然後按一下**加入和移除**。
19. 在 hello**加入和移除**視窗中，移動**azure documentdb 的 java 範例**toohello**設定**方塊，然後再按一下**完成**。
20. 在 hello**伺服器**索引標籤上，以滑鼠右鍵按一下**Tomcat v7.0 伺服器在 localhost**，然後按一下**重新啟動**。
21. 在瀏覽器中，瀏覽 toohttp://localhost:8080 / azure documentdb 的 java 範例 / 然後開始將加入 tooyour 工作清單。 請注意，如果您變更預設的連接埠值變更所選 8080 toohello 值。
22. toodeploy 您專案 tooan Azure 網站上，請參閱[步驟 6。部署您的應用程式 tooAzure 網站](#Deploy)。

[1]: media/documentdb-java-application/keys.png
