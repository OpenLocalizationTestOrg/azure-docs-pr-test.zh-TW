---
title: "aaaC + + 的 Azure Cosmos DB 教學課程 |Microsoft 文件"
description: "C++ 教學課程，將使用 Azure Cosmos DB 背書的 C++ SDK 來建立 C++ 資料庫和主控台應用程式。 Azure Cosmos DB 是全球級的資料庫服務。"
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Azure Cosmos DB: C + + 主控台應用程式的教學課程 hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

歡迎使用 toohello hello Azure Cosmos DB DocumentDB API 的 c + + 教學課程背書 SDK for c + + ！ 完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源，包括 C++ 資料庫。

本文將討論：

* 建立及連接 tooan Azure Cosmos DB 帳戶
* 設定您的應用程式
* 建立 C++ Azure Cosmos DB 資料庫
* 建立集合
* 建立 JSON 文件
* 查詢 hello 集合
* 取代文件
* 刪除文件
* 刪除 hello c + + Azure Cosmos DB 資料庫

沒有時間嗎？ 別擔心！ hello 完整解決方案位於[GitHub](https://github.com/stalker314314/DocumentDBCpp)。 請參閱[取得 hello 完整解決方案](#GetSolution)快速的指示。

您已經完成 hello c + + 教學課程之後，請使用 hello 投票按鈕下方的這個頁面 toogive hello 我們意見反應。 

如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 在您的註解或[聯繫 toous 這裡](https://www.research.net/r/8BKRJ3Z)。 

讓我們開始吧！

## <a name="prerequisites-for-hello-c-tutorial"></a>C + + hello 教學課程的必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。
* [Visual Studio](https://www.visualstudio.com/downloads/)，與 hello c + + 語言元件一起安裝。

## <a name="step-1-create-an-azure-cosmos-db-account"></a>步驟 1：建立 Azure Cosmos DB 帳戶
讓我們來建立 Azure Cosmos DB 帳戶。 如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[設定 c + + 應用程式以](#SetupNode)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>步驟 2︰設定您的 C++ 應用程式
1. 開啟 Visual Studio，然後在 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。 
2. 在 hello**新專案**視窗中的，於 hello**已安裝**] 窗格中，展開**Visual c + +**，按一下 [ **Win32**，然後按一下 **Win32 主控台應用程式**。 將 hello 專案 hellodocumentdb，再按一下**確定**。 
   
    ![Hello 新專案精靈的螢幕擷取畫面](media/documentdb-cpp-get-started/hello.png)
3. Hello Win32 應用程式精靈啟動時，按一下**完成**。
4. 一旦建立 hello 專案之後，開啟 hello NuGet 封裝管理員，以滑鼠右鍵按一下 hello **hellodocumentdb**專案中**方案總管 中**按一下**管理 NuGet 封裝**. 
   
    ![螢幕擷取畫面顯示 hello [專案] 功能表上的 [管理 NuGet 封裝]](media/documentdb-cpp-get-started/nuget.png)
5. 在 hello **NuGet: hellodocumentdb**索引標籤上，按一下 **瀏覽**，然後搜尋*documentdbcpp*。 在 hello 結果中，選取 DocumentDbCPP，hello 下列螢幕擷取畫面所示。 此套件會安裝參考 tooC + + REST SDK hello DocumentDbCPP 相依性。  
   
    ![反白顯示的螢幕擷取畫面顯示 hello DocumentDbCpp 封裝](media/documentdb-cpp-get-started/cpp.png)
   
    一旦 hello 封裝已加入 tooyour 專案，我們會撰寫一些程式碼的所有組 toostart。   

## <a id="Config"></a>步驟 3︰從 Azure 入口網站為您的 Azure Cosmos DB 資料庫複製連線詳細資料
啟動[Azure 入口網站](https://portal.azure.com)而且周遊 toohello Azure Cosmos DB 資料庫帳戶的密碼。 我們需要 hello URI 和 hello 的下一個步驟 tooestablish hello 連接在 Azure 入口網站的主索引鍵從我們的 c + + 程式碼片段。 

![Azure Cosmos DB URI 與 hello Azure 入口網站中的索引鍵](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>步驟 4： 連接 tooan Azure Cosmos DB 帳戶
1. 新增下列標頭和命名空間 tooyour 原始碼之後, 的 hello `#include "stdafx.h"`。
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. 接下來，加入 hello 下列程式碼 tooyour main 函式，並取代 hello 帳戶設定和主索引鍵 toomatch Azure Cosmos DB 設定從步驟 3。 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    您已經有 hello 程式碼 tooinitialize hello documentdb 用戶端，讓我們看看使用 Azure Cosmos DB 資源。

## <a id="CreateDBColl"></a>步驟 5︰建立 C++ 資料庫和集合
我們執行此步驟之前，請看一下資料庫、 集合和文件的使用者是新 tooAzure Cosmos DB 互動的方式。 [資料庫](documentdb-resources.md#databases)是分配到多個集合之文件儲存體的邏輯容器。 A[集合](documentdb-resources.md#collections)是 JSON 文件的容器和 hello 相關 JavaScript 應用程式邏輯。 您可以了解更多關於 hello Azure Cosmos DB 階層式資源模型和概念[Azure Cosmos DB 階層式資源模型和概念](documentdb-resources.md)。

toocreate 資料庫和對應集合加入下列程式碼 toohello 結尾至 main 函式的 hello。 這會建立名為 'FamilyRegistry' 和集合，稱為 'FamilyCollection' 使用您在宣告 hello 上一個步驟中的 hello 用戶端設定的資料庫。

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>步驟 6：建立文件
[文件](documentdb-resources.md#documents)是使用者定義的 (任意) JSON 內容。 您現在可以將文件插入 Azure Cosmos DB。 您可以藉由複製 hello hello 端 hello main 函式的下列程式碼來建立文件。 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

toosummarize，此程式碼會建立 Azure Cosmos DB 資料庫、 集合和文件，您可以查詢文件總管 中，在 Azure 入口網站中。 

![C + + 教學課程-圖表說明 hello hello 帳戶、 hello 資料庫、 hello 集合和 hello 文件之間的階層式關聯性](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>步驟 7︰查詢 Azure Cosmos DB 資源
Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。 hello 下列範例程式碼顯示 hello 上一個步驟中建立的查詢使用您可以針對 hello 文件執行的 SQL 語法。

hello 函式會引數 hello 唯一識別碼或資源識別碼 hello 資料庫及 hello 集合以及 hello 文件的用戶端。 請在 main 函式之前新增此程式碼。

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Replace"></a>步驟 8：取代文件
Azure Cosmos DB 支援取代的 JSON 文件，如下列程式碼的 hello 所示。 Hello executesimplequery 函式後面，加入下列程式碼。

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <a id="Delete"></a>步驟 9︰刪除文件
Azure DB Cosmos 支援刪除 JSON 文件，您可以透過複製及貼上下列程式碼 hello replacedocument 函式後面的 hello。 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="DeleteDB"></a>步驟 10︰刪除資料庫
正在刪除建立 hello 資料庫移除 hello 資料庫和所有子資源 （集合、 文件）。

複製並貼上下列程式碼片段 （函式清理） 之後 hello deletedocument 函式 tooremove hello 資料庫和所有 hello 子資源的 hello。

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>步驟 11：一起執行您的 C++ 應用程式！
我們現在已新增的程式碼 toocreate、 查詢、 修改和刪除不同 Azure Cosmos DB 資源。  讓我們現在連接這只要新增我們 hellodocumentdb.cpp 以及一些診斷訊息中的 main 函式呼叫 toothese 不同函式。

您可以以下列程式碼的 hello 取代 hello 應用程式的 main 函式來這麼做。 這個 hello account_configuration_uri 和 primary_key 您複製到步驟 3 中的 hello 程式碼寫入因此儲存該線條或複製 hello 值中的再次從 hello 入口網站。 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

您應該立即無法 toobuild 和按 F5 執行您的程式碼在 Visual Studio 中或或者在 hello 終端機視窗，尋找 hello 應用程式，並執行 hello 可執行檔。 

您應該會看到 hello 取得啟動應用程式的輸出。 hello 輸出應符合下列螢幕擷取畫面的 hello。

![Azure Cosmos DB C++ 應用程式輸出](media/documentdb-cpp-get-started/console.png)

恭喜！ 您已經完成 hello c + + 教學課程，將第一個 Azure Cosmos DB 主控台應用程式 ！

## <a id="GetSolution"></a>取得 hello 完成 c + + 教學課程解決方案
toobuild hello GetStarted 方案，其中包含本文章中的所有 hello 範例，您需要下列 hello:

* [Azure Cosmos DB 帳戶][create-account]。
* hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) GitHub 上有可用的解決方案。

## <a name="next-steps"></a>後續步驟
* 了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* 深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。

[create-account]: create-documentdb-dotnet.md#create-account


