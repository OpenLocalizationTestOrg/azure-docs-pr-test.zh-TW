---
title: "適用於 Azure Cosmos DB 的 C++ 教學課程 | Microsoft Docs"
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="5f46c-104">Azure Cosmos DB：適用於 DocumentDB API 的 C++ 主控台應用程式教學課程</span><span class="sxs-lookup"><span data-stu-id="5f46c-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f46c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5f46c-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="5f46c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5f46c-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="5f46c-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f46c-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="5f46c-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="5f46c-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="5f46c-109">Java</span><span class="sxs-lookup"><span data-stu-id="5f46c-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="5f46c-110">C++</span><span class="sxs-lookup"><span data-stu-id="5f46c-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="5f46c-111">歡迎使用 Azure Cosmos DB DocumentDB API 背書、適用於 C++ SDK 的 C++ 教學課程！</span><span class="sxs-lookup"><span data-stu-id="5f46c-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="5f46c-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源，包括 C++ 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5f46c-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="5f46c-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="5f46c-113">We'll cover:</span></span>

* <span data-ttu-id="5f46c-114">建立及連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5f46c-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="5f46c-115">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5f46c-115">Setting up your application</span></span>
* <span data-ttu-id="5f46c-116">建立 C++ Azure Cosmos DB 資料庫</span><span class="sxs-lookup"><span data-stu-id="5f46c-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="5f46c-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="5f46c-117">Creating a collection</span></span>
* <span data-ttu-id="5f46c-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-118">Creating JSON documents</span></span>
* <span data-ttu-id="5f46c-119">查詢集合</span><span class="sxs-lookup"><span data-stu-id="5f46c-119">Querying the collection</span></span>
* <span data-ttu-id="5f46c-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-120">Replacing a document</span></span>
* <span data-ttu-id="5f46c-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-121">Deleting a document</span></span>
* <span data-ttu-id="5f46c-122">將 C++ Azure Cosmos DB 資料庫刪除</span><span class="sxs-lookup"><span data-stu-id="5f46c-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="5f46c-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="5f46c-123">Don't have time?</span></span> <span data-ttu-id="5f46c-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="5f46c-124">Don't worry!</span></span> <span data-ttu-id="5f46c-125">您可以在 [GitHub](https://github.com/stalker314314/DocumentDBCpp)上找到完整的方案。</span><span class="sxs-lookup"><span data-stu-id="5f46c-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="5f46c-126">請參閱 [取得完整的解決方案](#GetSolution) ，以取得簡要指示。</span><span class="sxs-lookup"><span data-stu-id="5f46c-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="5f46c-127">完成 C++ 教學課程之後，請使用此頁面底部的投票按鈕來提供意見。</span><span class="sxs-lookup"><span data-stu-id="5f46c-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="5f46c-128">如果想要我們直接與您連絡，歡迎在留言中留下電子郵件地址或[在此與我們聯繫](https://www.research.net/r/8BKRJ3Z)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="5f46c-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="5f46c-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="5f46c-130">C++ 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="5f46c-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="5f46c-131">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="5f46c-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="5f46c-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f46c-132">An active Azure account.</span></span> <span data-ttu-id="5f46c-133">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5f46c-134">[Visual Studio](https://www.visualstudio.com/downloads/)，並已安裝 C++ 語言元件。</span><span class="sxs-lookup"><span data-stu-id="5f46c-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="5f46c-135">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5f46c-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="5f46c-136">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f46c-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="5f46c-137">如果您已經擁有想要使用的帳戶，就可以跳到 [設定您的 C++ 應用程式](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="5f46c-138"><a id="SetupC++"></a>步驟 2︰設定您的 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="5f46c-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="5f46c-139">開啟 Visual Studio，在 [檔案] 功能表上，按一下 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="5f46c-140">在 [新增專案] 視窗中，於 [已安裝] 窗格中展開 [Visual C++]，按一下 [Win32]，然後按一下 [Win32 主控台應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="5f46c-141">將專案命名為 hellodocumentdb，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![新增專案精靈的螢幕擷取畫面](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="5f46c-143">當 Win32 應用程式精靈啟動時，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="5f46c-144">建立專案後，開啟 NuGet 套件管理員，方法是以滑鼠右鍵按一下 [方案總管] 中的 **hellodocumentdb** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![專案功能表上顯示管理 NuGet 套件的螢幕擷取畫面](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="5f46c-146">在 [NuGet: hellodocumentdb] 索引標籤上，按一下 [瀏覽]，然後搜尋「documentdbcpp」。</span><span class="sxs-lookup"><span data-stu-id="5f46c-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="5f46c-147">在結果中選取 DocumentDbCPP，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="5f46c-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="5f46c-148">此套件會安裝 C++ REST SDK 的參考，該 SDK 是 DocumentDbCPP 的相依項目。</span><span class="sxs-lookup"><span data-stu-id="5f46c-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![顯示已醒目提示 DocumentDbCpp 套件的螢幕擷取畫面](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="5f46c-150">套件新增至您的專案後，一切便已準備就緒，可以開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f46c-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="5f46c-151"><a id="Config"></a>步驟 3︰從 Azure 入口網站為您的 Azure Cosmos DB 資料庫複製連線詳細資料</span><span class="sxs-lookup"><span data-stu-id="5f46c-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="5f46c-152">讓 [Azure 入口網站](https://portal.azure.com)出現，並周遊至您所建立的 Azure Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f46c-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="5f46c-153">在下一個步驟中，我們需要從 Azure 入口網站取得的 URI 和主要金鑰，以便從我們的 C++ 程式碼片段建立連線。</span><span class="sxs-lookup"><span data-stu-id="5f46c-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Azure 入口網站中的 Azure Cosmos DB URI 和金鑰](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="5f46c-155"><a id="Connect"></a>步驟 4：連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5f46c-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="5f46c-156">在原始程式碼的 `#include "stdafx.h"` 之後新增下列標頭和命名空間。</span><span class="sxs-lookup"><span data-stu-id="5f46c-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="5f46c-157">接下來，將下列程式碼新增至 main 函式，並取代帳戶設定和主要金鑰，使其符合步驟 3 中的 Azure Cosmos DB 設定。</span><span class="sxs-lookup"><span data-stu-id="5f46c-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="5f46c-158">您現在具有程式碼，可將 documentdb 用戶端初始化，讓我們看看如何使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="5f46c-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="5f46c-159"><a id="CreateDBColl"></a>步驟 5︰建立 C++ 資料庫和集合</span><span class="sxs-lookup"><span data-stu-id="5f46c-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="5f46c-160">在執行此步驟之前，有人可能不熟悉 Azure Cosmos DB，因此我們先了解一下資料庫、集合和文件的互動方式。</span><span class="sxs-lookup"><span data-stu-id="5f46c-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="5f46c-161">[資料庫](documentdb-resources.md#databases)是分配到多個集合之文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="5f46c-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="5f46c-162">[集合](documentdb-resources.md#collections)是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="5f46c-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="5f46c-163">您可以在 [Azure Cosmos DB 階層式資源模型和概念](documentdb-resources.md)中，深入了解 Azure Cosmos DB 階層式資源模型和概念。</span><span class="sxs-lookup"><span data-stu-id="5f46c-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="5f46c-164">為了建立資料庫和對應的集合，請在 main 函式結尾新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f46c-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="5f46c-165">這會使用您在上一個步驟中宣告的用戶端組態，建立名為「FamilyRegistry」的資料庫和名為「FamilyCollection」的集合。</span><span class="sxs-lookup"><span data-stu-id="5f46c-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="5f46c-166"><a id="CreateDoc"></a>步驟 6：建立文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="5f46c-167">[文件](documentdb-resources.md#documents)是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="5f46c-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="5f46c-168">您現在可以將文件插入 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="5f46c-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="5f46c-169">您可以將下列程式碼複製到 main 函式結尾，以建立文件。</span><span class="sxs-lookup"><span data-stu-id="5f46c-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="5f46c-170">總結來說，此程式碼會建立 Azure Cosmos DB 資料庫、集合和文件，而您可以在 Azure 入口網站的文件總管中進行查詢。</span><span class="sxs-lookup"><span data-stu-id="5f46c-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++ 教學課程 - 說明帳戶、資料庫、集合和文件之間階層式關聯性的圖表](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="5f46c-172"><a id="QueryDB"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="5f46c-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="5f46c-173">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="5f46c-174">下列範例程式碼示範使用 SQL 語法所建立的查詢，您可以針對我們在上一個步驟中建立的文件執行該查詢。</span><span class="sxs-lookup"><span data-stu-id="5f46c-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="5f46c-175">函式會採用資料庫和集合以及文件用戶端的唯一識別碼或資源識別碼來做為引數。</span><span class="sxs-lookup"><span data-stu-id="5f46c-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="5f46c-176">請在 main 函式之前新增此程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f46c-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="5f46c-177"><a id="Replace"></a>步驟 8：取代文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="5f46c-178">Azure Cosmos DB 支援取代 JSON 文件，如下列程式碼所示範。</span><span class="sxs-lookup"><span data-stu-id="5f46c-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="5f46c-179">請在 executesimplequery 函式之後新增此程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f46c-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="5f46c-180"><a id="Delete"></a>步驟 9︰刪除文件</span><span class="sxs-lookup"><span data-stu-id="5f46c-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="5f46c-181">Azure Cosmos DB 支援刪除 JSON 文件，只要在 replacedocument 函式之後將下列程式碼複製並貼上即可。</span><span class="sxs-lookup"><span data-stu-id="5f46c-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="5f46c-182"><a id="DeleteDB"></a>步驟 10︰刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="5f46c-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="5f46c-183">刪除已建立的資料庫會移除資料庫和所有子系資源 (集合、文件等)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="5f46c-184">在 deletedocument 函式之後複製並貼上下列程式碼片段 (cleanup 函式)，即可移除資料庫和所有子系資源。</span><span class="sxs-lookup"><span data-stu-id="5f46c-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="5f46c-185"><a id="Run"></a>步驟 11：一起執行您的 C++ 應用程式！</span><span class="sxs-lookup"><span data-stu-id="5f46c-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="5f46c-186">我們現已新增程式碼來建立、查詢、修改和刪除不同的 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="5f46c-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="5f46c-187">現在讓我們將這一切連接起來，方法是從 hellodocumentdb.cpp 中的 main 函式對這些不同的函式新增呼叫以及一些診斷訊息。</span><span class="sxs-lookup"><span data-stu-id="5f46c-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="5f46c-188">若要這麼做，您可以使用下列程式碼取代應用程式的 main 函式。</span><span class="sxs-lookup"><span data-stu-id="5f46c-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="5f46c-189">這會覆寫您在步驟 3 中複製到程式碼的 account_configuration_uri 和 primary_key，因此請儲存該行，或從入口網站將這些值再次複製進來。</span><span class="sxs-lookup"><span data-stu-id="5f46c-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="5f46c-190">現在您應該能夠在 Visual Studio 中建置並執行您的程式碼，方法是按 F5 鍵，或是在終端機視窗中尋找應用程式並執行可執行檔。</span><span class="sxs-lookup"><span data-stu-id="5f46c-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="5f46c-191">您應該可以看到入門應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="5f46c-191">You should see the output of your get started app.</span></span> <span data-ttu-id="5f46c-192">該輸出應該會符合以下螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="5f46c-192">The output should match the following screenshot.</span></span>

![Azure Cosmos DB C++ 應用程式輸出](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="5f46c-194">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5f46c-194">Congratulations!</span></span> <span data-ttu-id="5f46c-195">您已完成 C++ 教學課程，並擁有您的第一個 Azure Cosmos DB 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="5f46c-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="5f46c-196"><a id="GetSolution"></a>取得完整的 C++ 教學課程方案</span><span class="sxs-lookup"><span data-stu-id="5f46c-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="5f46c-197">若要建置包含本文中所有範例的 GetStarted 方案，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5f46c-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="5f46c-198">[Azure Cosmos DB 帳戶][create-account]。</span><span class="sxs-lookup"><span data-stu-id="5f46c-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="5f46c-199">您可以在 GitHub 上找到 [GetStarted](https://github.com/stalker314314/DocumentDBCpp) 方案。</span><span class="sxs-lookup"><span data-stu-id="5f46c-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f46c-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f46c-200">Next steps</span></span>
* <span data-ttu-id="5f46c-201">了解如何[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="5f46c-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="5f46c-202">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="5f46c-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="5f46c-203">如需深入了解程式設計模型，請參閱 [Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)中的＜開發＞一節。</span><span class="sxs-lookup"><span data-stu-id="5f46c-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


