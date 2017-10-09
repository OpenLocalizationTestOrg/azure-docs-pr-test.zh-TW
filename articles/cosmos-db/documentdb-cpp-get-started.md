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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="70991-104">Azure Cosmos DB: C + + 主控台應用程式的教學課程 hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="70991-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70991-105">.NET</span><span class="sxs-lookup"><span data-stu-id="70991-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="70991-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="70991-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="70991-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="70991-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="70991-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="70991-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="70991-109">Java</span><span class="sxs-lookup"><span data-stu-id="70991-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="70991-110">C++</span><span class="sxs-lookup"><span data-stu-id="70991-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="70991-111">歡迎使用 toohello hello Azure Cosmos DB DocumentDB API 的 c + + 教學課程背書 SDK for c + + ！</span><span class="sxs-lookup"><span data-stu-id="70991-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="70991-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源，包括 C++ 資料庫。</span><span class="sxs-lookup"><span data-stu-id="70991-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="70991-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="70991-113">We'll cover:</span></span>

* <span data-ttu-id="70991-114">建立及連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="70991-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="70991-115">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="70991-115">Setting up your application</span></span>
* <span data-ttu-id="70991-116">建立 C++ Azure Cosmos DB 資料庫</span><span class="sxs-lookup"><span data-stu-id="70991-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="70991-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="70991-117">Creating a collection</span></span>
* <span data-ttu-id="70991-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="70991-118">Creating JSON documents</span></span>
* <span data-ttu-id="70991-119">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="70991-119">Querying hello collection</span></span>
* <span data-ttu-id="70991-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="70991-120">Replacing a document</span></span>
* <span data-ttu-id="70991-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="70991-121">Deleting a document</span></span>
* <span data-ttu-id="70991-122">刪除 hello c + + Azure Cosmos DB 資料庫</span><span class="sxs-lookup"><span data-stu-id="70991-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="70991-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="70991-123">Don't have time?</span></span> <span data-ttu-id="70991-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="70991-124">Don't worry!</span></span> <span data-ttu-id="70991-125">hello 完整解決方案位於[GitHub](https://github.com/stalker314314/DocumentDBCpp)。</span><span class="sxs-lookup"><span data-stu-id="70991-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="70991-126">請參閱[取得 hello 完整解決方案](#GetSolution)快速的指示。</span><span class="sxs-lookup"><span data-stu-id="70991-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="70991-127">您已經完成 hello c + + 教學課程之後，請使用 hello 投票按鈕下方的這個頁面 toogive hello 我們意見反應。</span><span class="sxs-lookup"><span data-stu-id="70991-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="70991-128">如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 在您的註解或[聯繫 toous 這裡](https://www.research.net/r/8BKRJ3Z)。</span><span class="sxs-lookup"><span data-stu-id="70991-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="70991-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="70991-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="70991-130">C + + hello 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="70991-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="70991-131">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="70991-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="70991-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="70991-132">An active Azure account.</span></span> <span data-ttu-id="70991-133">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="70991-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="70991-134">[Visual Studio](https://www.visualstudio.com/downloads/)，與 hello c + + 語言元件一起安裝。</span><span class="sxs-lookup"><span data-stu-id="70991-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="70991-135">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="70991-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="70991-136">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="70991-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="70991-137">如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[設定 c + + 應用程式以](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="70991-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="70991-138"><a id="SetupC++"></a>步驟 2︰設定您的 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="70991-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="70991-139">開啟 Visual Studio，然後在 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="70991-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="70991-140">在 hello**新專案**視窗中的，於 hello**已安裝**] 窗格中，展開**Visual c + +**，按一下 [ **Win32**，然後按一下 **Win32 主控台應用程式**。</span><span class="sxs-lookup"><span data-stu-id="70991-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="70991-141">將 hello 專案 hellodocumentdb，再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="70991-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Hello 新專案精靈的螢幕擷取畫面](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="70991-143">Hello Win32 應用程式精靈啟動時，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="70991-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="70991-144">一旦建立 hello 專案之後，開啟 hello NuGet 封裝管理員，以滑鼠右鍵按一下 hello **hellodocumentdb**專案中**方案總管 中**按一下**管理 NuGet 封裝**.</span><span class="sxs-lookup"><span data-stu-id="70991-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![螢幕擷取畫面顯示 hello [專案] 功能表上的 [管理 NuGet 封裝]](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="70991-146">在 hello **NuGet: hellodocumentdb**索引標籤上，按一下 **瀏覽**，然後搜尋*documentdbcpp*。</span><span class="sxs-lookup"><span data-stu-id="70991-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="70991-147">在 hello 結果中，選取 DocumentDbCPP，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="70991-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="70991-148">此套件會安裝參考 tooC + + REST SDK hello DocumentDbCPP 相依性。</span><span class="sxs-lookup"><span data-stu-id="70991-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![反白顯示的螢幕擷取畫面顯示 hello DocumentDbCpp 封裝](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="70991-150">一旦 hello 封裝已加入 tooyour 專案，我們會撰寫一些程式碼的所有組 toostart。</span><span class="sxs-lookup"><span data-stu-id="70991-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="70991-151"><a id="Config"></a>步驟 3︰從 Azure 入口網站為您的 Azure Cosmos DB 資料庫複製連線詳細資料</span><span class="sxs-lookup"><span data-stu-id="70991-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="70991-152">啟動[Azure 入口網站](https://portal.azure.com)而且周遊 toohello Azure Cosmos DB 資料庫帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="70991-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="70991-153">我們需要 hello URI 和 hello 的下一個步驟 tooestablish hello 連接在 Azure 入口網站的主索引鍵從我們的 c + + 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="70991-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI 與 hello Azure 入口網站中的索引鍵](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="70991-155"><a id="Connect"></a>步驟 4： 連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="70991-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="70991-156">新增下列標頭和命名空間 tooyour 原始碼之後, 的 hello `#include "stdafx.h"`。</span><span class="sxs-lookup"><span data-stu-id="70991-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="70991-157">接下來，加入 hello 下列程式碼 tooyour main 函式，並取代 hello 帳戶設定和主索引鍵 toomatch Azure Cosmos DB 設定從步驟 3。</span><span class="sxs-lookup"><span data-stu-id="70991-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="70991-158">您已經有 hello 程式碼 tooinitialize hello documentdb 用戶端，讓我們看看使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="70991-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="70991-159"><a id="CreateDBColl"></a>步驟 5︰建立 C++ 資料庫和集合</span><span class="sxs-lookup"><span data-stu-id="70991-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="70991-160">我們執行此步驟之前，請看一下資料庫、 集合和文件的使用者是新 tooAzure Cosmos DB 互動的方式。</span><span class="sxs-lookup"><span data-stu-id="70991-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="70991-161">[資料庫](documentdb-resources.md#databases)是分配到多個集合之文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="70991-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="70991-162">A[集合](documentdb-resources.md#collections)是 JSON 文件的容器和 hello 相關 JavaScript 應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="70991-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="70991-163">您可以了解更多關於 hello Azure Cosmos DB 階層式資源模型和概念[Azure Cosmos DB 階層式資源模型和概念](documentdb-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="70991-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="70991-164">toocreate 資料庫和對應集合加入下列程式碼 toohello 結尾至 main 函式的 hello。</span><span class="sxs-lookup"><span data-stu-id="70991-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="70991-165">這會建立名為 'FamilyRegistry' 和集合，稱為 'FamilyCollection' 使用您在宣告 hello 上一個步驟中的 hello 用戶端設定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="70991-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="70991-166"><a id="CreateDoc"></a>步驟 6：建立文件</span><span class="sxs-lookup"><span data-stu-id="70991-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="70991-167">[文件](documentdb-resources.md#documents)是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="70991-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="70991-168">您現在可以將文件插入 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="70991-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="70991-169">您可以藉由複製 hello hello 端 hello main 函式的下列程式碼來建立文件。</span><span class="sxs-lookup"><span data-stu-id="70991-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

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

<span data-ttu-id="70991-170">toosummarize，此程式碼會建立 Azure Cosmos DB 資料庫、 集合和文件，您可以查詢文件總管 中，在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="70991-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C + + 教學課程-圖表說明 hello hello 帳戶、 hello 資料庫、 hello 集合和 hello 文件之間的階層式關聯性](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="70991-172"><a id="QueryDB"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="70991-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="70991-173">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="70991-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="70991-174">hello 下列範例程式碼顯示 hello 上一個步驟中建立的查詢使用您可以針對 hello 文件執行的 SQL 語法。</span><span class="sxs-lookup"><span data-stu-id="70991-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="70991-175">hello 函式會引數 hello 唯一識別碼或資源識別碼 hello 資料庫及 hello 集合以及 hello 文件的用戶端。</span><span class="sxs-lookup"><span data-stu-id="70991-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="70991-176">請在 main 函式之前新增此程式碼。</span><span class="sxs-lookup"><span data-stu-id="70991-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="70991-177"><a id="Replace"></a>步驟 8：取代文件</span><span class="sxs-lookup"><span data-stu-id="70991-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="70991-178">Azure Cosmos DB 支援取代的 JSON 文件，如下列程式碼的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="70991-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="70991-179">Hello executesimplequery 函式後面，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="70991-179">Add this code after hello executesimplequery function.</span></span>

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

## <span data-ttu-id="70991-180"><a id="Delete"></a>步驟 9︰刪除文件</span><span class="sxs-lookup"><span data-stu-id="70991-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="70991-181">Azure DB Cosmos 支援刪除 JSON 文件，您可以透過複製及貼上下列程式碼 hello replacedocument 函式後面的 hello。</span><span class="sxs-lookup"><span data-stu-id="70991-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

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

## <span data-ttu-id="70991-182"><a id="DeleteDB"></a>步驟 10︰刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="70991-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="70991-183">正在刪除建立 hello 資料庫移除 hello 資料庫和所有子資源 （集合、 文件）。</span><span class="sxs-lookup"><span data-stu-id="70991-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="70991-184">複製並貼上下列程式碼片段 （函式清理） 之後 hello deletedocument 函式 tooremove hello 資料庫和所有 hello 子資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="70991-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="70991-185"><a id="Run"></a>步驟 11：一起執行您的 C++ 應用程式！</span><span class="sxs-lookup"><span data-stu-id="70991-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="70991-186">我們現在已新增的程式碼 toocreate、 查詢、 修改和刪除不同 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="70991-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="70991-187">讓我們現在連接這只要新增我們 hellodocumentdb.cpp 以及一些診斷訊息中的 main 函式呼叫 toothese 不同函式。</span><span class="sxs-lookup"><span data-stu-id="70991-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="70991-188">您可以以下列程式碼的 hello 取代 hello 應用程式的 main 函式來這麼做。</span><span class="sxs-lookup"><span data-stu-id="70991-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="70991-189">這個 hello account_configuration_uri 和 primary_key 您複製到步驟 3 中的 hello 程式碼寫入因此儲存該線條或複製 hello 值中的再次從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="70991-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

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

<span data-ttu-id="70991-190">您應該立即無法 toobuild 和按 F5 執行您的程式碼在 Visual Studio 中或或者在 hello 終端機視窗，尋找 hello 應用程式，並執行 hello 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="70991-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="70991-191">您應該會看到 hello 取得啟動應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="70991-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="70991-192">hello 輸出應符合下列螢幕擷取畫面的 hello。</span><span class="sxs-lookup"><span data-stu-id="70991-192">hello output should match hello following screenshot.</span></span>

![Azure Cosmos DB C++ 應用程式輸出](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="70991-194">恭喜！</span><span class="sxs-lookup"><span data-stu-id="70991-194">Congratulations!</span></span> <span data-ttu-id="70991-195">您已經完成 hello c + + 教學課程，將第一個 Azure Cosmos DB 主控台應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="70991-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="70991-196"><a id="GetSolution"></a>取得 hello 完成 c + + 教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="70991-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="70991-197">toobuild hello GetStarted 方案，其中包含本文章中的所有 hello 範例，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="70991-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="70991-198">[Azure Cosmos DB 帳戶][create-account]。</span><span class="sxs-lookup"><span data-stu-id="70991-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="70991-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) GitHub 上有可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="70991-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70991-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70991-200">Next steps</span></span>
* <span data-ttu-id="70991-201">了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="70991-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="70991-202">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="70991-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="70991-203">深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="70991-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


