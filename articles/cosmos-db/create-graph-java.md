---
title: "使用 Java 建立 Azure Cosmos DB 圖形資料庫 | Microsoft Docs"
description: "提供 Java 程式碼範例，您可透過 Gremlin 用來連線及查詢 Azure Cosmos DB 中的圖形資料。"
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
ms.openlocfilehash: 0273072c7c10e219ab8d6c85eb252badafc17147
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-the-azure-portal"></a><span data-ttu-id="1622a-103">Azure Cosmos DB︰使用 Java 和 Azure 入口網站建立圖形資料庫</span><span class="sxs-lookup"><span data-stu-id="1622a-103">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>

<span data-ttu-id="1622a-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="1622a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1622a-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="1622a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1622a-106">本快速入門會使用 Azure Cosmos DB 適用的 Azure 入口網站工具建立圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="1622a-106">This quickstart creates a graph database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="1622a-107">本快速入門也會顯示如何使用 OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) 驅動程式，快速建立 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1622a-107">This quickstart also shows you how to quickly create a Java console app using a graph database using the OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="1622a-108">本快速入門中的指示可運用在任何足以執行 Java 應用程式的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="1622a-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="1622a-109">本快速入門可讓您熟悉在 UI 中或以程式設計方式建立和修改圖形資源 (不論您偏好哪種方式)。</span><span class="sxs-lookup"><span data-stu-id="1622a-109">This quickstart familiarizes you with creating and modifying graph resources in either the UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1622a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1622a-110">Prerequisites</span></span>

* [<span data-ttu-id="1622a-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="1622a-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="1622a-112">在 Ubuntu 上，執行 `apt-get install default-jdk` 來安裝 JDK。</span><span class="sxs-lookup"><span data-stu-id="1622a-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="1622a-113">務必設定 JAVA_HOME 環境變數，以指向 JDK 安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1622a-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="1622a-114">[下載](http://maven.apache.org/download.cgi)和[安裝 ](http://maven.apache.org/install.html) [Maven](http://maven.apache.org/) 二進位封存檔</span><span class="sxs-lookup"><span data-stu-id="1622a-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="1622a-115">在 Ubuntu 上，您可以執行 `apt-get install maven` 來安裝 Maven。</span><span class="sxs-lookup"><span data-stu-id="1622a-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="1622a-116">Git</span><span class="sxs-lookup"><span data-stu-id="1622a-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="1622a-117">在 Ubuntu 上，您可以執行 `sudo apt-get install git` 來安裝 Git。</span><span class="sxs-lookup"><span data-stu-id="1622a-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1622a-118">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="1622a-118">Create a database account</span></span>

<span data-ttu-id="1622a-119">您必須先使用 Azure Cosmos DB 建立 Gremlin (圖形) 資料庫帳戶，才可以建立圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="1622a-119">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="1622a-120">新增圖形</span><span class="sxs-lookup"><span data-stu-id="1622a-120">Add a graph</span></span>

<span data-ttu-id="1622a-121">您現在可以在 Azure 入口網站中使用 [資料總管] 工具，建立圖形資料庫。</span><span class="sxs-lookup"><span data-stu-id="1622a-121">You can now use the Data Explorer tool in the Azure portal to create a graph database.</span></span> 

1. <span data-ttu-id="1622a-122">在 Azure 入口網站的左導覽功能表中，按一下 [資料總管 (預覽)]。</span><span class="sxs-lookup"><span data-stu-id="1622a-122">In the Azure portal, in the left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="1622a-123">在 [資料總管 (預覽)] 刀鋒視窗中，按一下 [新增圖形]，然後使用下列資訊填入頁面：</span><span class="sxs-lookup"><span data-stu-id="1622a-123">In the **Data Explorer (Preview)** blade, click **New Graph**, then fill in the page using the following information:</span></span>

    ![Azure 入口網站中的資料總管](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="1622a-125">設定</span><span class="sxs-lookup"><span data-stu-id="1622a-125">Setting</span></span>|<span data-ttu-id="1622a-126">建議的值</span><span class="sxs-lookup"><span data-stu-id="1622a-126">Suggested value</span></span>|<span data-ttu-id="1622a-127">說明</span><span class="sxs-lookup"><span data-stu-id="1622a-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="1622a-128">資料庫識別碼</span><span class="sxs-lookup"><span data-stu-id="1622a-128">Database ID</span></span>|<span data-ttu-id="1622a-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="1622a-129">sample-database</span></span>|<span data-ttu-id="1622a-130">新資料庫的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1622a-130">The ID for your new database.</span></span> <span data-ttu-id="1622a-131">資料庫名稱的長度必須介於 1 到 255 個字元，且不能包含 `/ \ # ?` 或尾端空格。</span><span class="sxs-lookup"><span data-stu-id="1622a-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="1622a-132">圖形識別碼</span><span class="sxs-lookup"><span data-stu-id="1622a-132">Graph ID</span></span>|<span data-ttu-id="1622a-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="1622a-133">sample-graph</span></span>|<span data-ttu-id="1622a-134">新圖形的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1622a-134">The ID for your new graph.</span></span> <span data-ttu-id="1622a-135">圖形名稱與資料庫識別碼具有相同的字元需求。</span><span class="sxs-lookup"><span data-stu-id="1622a-135">Graph names have the same character requirements as database ids.</span></span>
    <span data-ttu-id="1622a-136">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1622a-136">Storage Capacity</span></span>| <span data-ttu-id="1622a-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="1622a-137">10 GB</span></span>|<span data-ttu-id="1622a-138">保留預設值。</span><span class="sxs-lookup"><span data-stu-id="1622a-138">Leave the default value.</span></span> <span data-ttu-id="1622a-139">這是資料庫的儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="1622a-139">This is the storage capacity of the database.</span></span>
    <span data-ttu-id="1622a-140">輸送量</span><span class="sxs-lookup"><span data-stu-id="1622a-140">Throughput</span></span>|<span data-ttu-id="1622a-141">400 RU</span><span class="sxs-lookup"><span data-stu-id="1622a-141">400 RUs</span></span>|<span data-ttu-id="1622a-142">保留預設值。</span><span class="sxs-lookup"><span data-stu-id="1622a-142">Leave the default value.</span></span> <span data-ttu-id="1622a-143">如果您想要降低延遲，稍後可以相應增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="1622a-143">You can scale up the throughput later if you want to reduce latency.</span></span>
    <span data-ttu-id="1622a-144">資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="1622a-144">Partition key</span></span>|<span data-ttu-id="1622a-145">保留空白</span><span class="sxs-lookup"><span data-stu-id="1622a-145">Leave blank</span></span>|<span data-ttu-id="1622a-146">針對本快速入門的目的，將資料分割索引鍵空白。</span><span class="sxs-lookup"><span data-stu-id="1622a-146">For the purpose of this quickstart, leave the partition key blank.</span></span>

3. <span data-ttu-id="1622a-147">填妥表單後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1622a-147">Once the form is filled out, click **OK**.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="1622a-148">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1622a-148">Clone the sample application</span></span>

<span data-ttu-id="1622a-149">現在，我們將從 GitHub 複製圖形應用程式、設定連接字串，然後加以執行。</span><span class="sxs-lookup"><span data-stu-id="1622a-149">Now let's clone a graph app from github, set the connection string, and run it.</span></span> <span data-ttu-id="1622a-150">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="1622a-150">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="1622a-151">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="1622a-151">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="1622a-152">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="1622a-152">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="1622a-153">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="1622a-153">Review the code</span></span>

<span data-ttu-id="1622a-154">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="1622a-154">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="1622a-155">開啟 \src\GetStarted 資料夾中的 `Program.java` 檔案，並尋找這些程式碼行。</span><span class="sxs-lookup"><span data-stu-id="1622a-155">Open the `Program.java` file from the \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="1622a-156">已從 `src/remote.yaml` 中的組態初始化 Gremlin `Client`。</span><span class="sxs-lookup"><span data-stu-id="1622a-156">The Gremlin `Client` is initialized from the configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="1622a-157">已使用 `client.submit` 方法執行一系列的 Gremlin 步驟。</span><span class="sxs-lookup"><span data-stu-id="1622a-157">A series of Gremlin steps are executed using the `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="1622a-158">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="1622a-158">Update your connection string</span></span>

1. <span data-ttu-id="1622a-159">開啟 src/remote.yaml 檔案。</span><span class="sxs-lookup"><span data-stu-id="1622a-159">Open the src/remote.yaml file.</span></span> 

3. <span data-ttu-id="1622a-160">在 src/remote.yaml 檔案中填入您的「主機」、「使用者名稱」和「密碼」值。</span><span class="sxs-lookup"><span data-stu-id="1622a-160">Fill in your *hosts*, *username*, and *password* values in the src/remote.yaml file.</span></span> <span data-ttu-id="1622a-161">不需要變更其餘的設定。</span><span class="sxs-lookup"><span data-stu-id="1622a-161">The rest of the settings do not need to be changed.</span></span>

    <span data-ttu-id="1622a-162">設定</span><span class="sxs-lookup"><span data-stu-id="1622a-162">Setting</span></span>|<span data-ttu-id="1622a-163">建議的值</span><span class="sxs-lookup"><span data-stu-id="1622a-163">Suggested value</span></span>|<span data-ttu-id="1622a-164">說明</span><span class="sxs-lookup"><span data-stu-id="1622a-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="1622a-165">主機</span><span class="sxs-lookup"><span data-stu-id="1622a-165">Hosts</span></span>|<span data-ttu-id="1622a-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="1622a-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="1622a-167">請參閱此表之後的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="1622a-167">See the screenshot following this table.</span></span> <span data-ttu-id="1622a-168">此值是 Azure 入口網站的 [概觀] 頁面上的 Gremlin URI 值，其以方括號括住並已移除尾端的 :443/。</span><span class="sxs-lookup"><span data-stu-id="1622a-168">This value is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="1622a-169">此值也可以從 [金鑰] 索引標籤擷取，方法是移除https://、將文件變更為圖形，並移除尾端的:443/ 來使用 URI 值。</span><span class="sxs-lookup"><span data-stu-id="1622a-169">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="1622a-170">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="1622a-170">Username</span></span>|<span data-ttu-id="1622a-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="1622a-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="1622a-172">`/dbs/<db>/colls/<coll>` 表單的資源，其中 `<db>` 是您現有的資料庫名稱，而 `<coll>` 是您現有的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="1622a-172">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="1622a-173">密碼</span><span class="sxs-lookup"><span data-stu-id="1622a-173">Password</span></span>|<span data-ttu-id="1622a-174">您的主要金鑰</span><span class="sxs-lookup"><span data-stu-id="1622a-174">*Your primary master key*</span></span>|<span data-ttu-id="1622a-175">請參閱此表之後的第二個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="1622a-175">See the second screenshot following this table.</span></span> <span data-ttu-id="1622a-176">此值是您的主要金鑰，可以從 Azure 入口網站 [金鑰] 頁面的 [主鑰金鑰] 方塊中擷取。</span><span class="sxs-lookup"><span data-stu-id="1622a-176">This value is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="1622a-177">使用方塊左側的複製按鈕來複製此值。</span><span class="sxs-lookup"><span data-stu-id="1622a-177">Copy the value using the copy button on the right side of the box.</span></span>

    <span data-ttu-id="1622a-178">對於 [主機] 值，從 [概觀] 頁面複製 [Gremlin URI] 值。</span><span class="sxs-lookup"><span data-stu-id="1622a-178">For the Hosts value, copy the **Gremlin URI** value from the **Overview** page.</span></span> <span data-ttu-id="1622a-179">如果是空的，請參閱上表「主機」列中有關從 [金鑰] 刀鋒視窗建立 Gremlin URI 的指示。</span><span class="sxs-lookup"><span data-stu-id="1622a-179">If it's empty, see the instructions in the Hosts row in the preceding table about creating the Gremlin URI from the Keys blade.</span></span>
<span data-ttu-id="1622a-180">![在 Azure 入口網站的 [概觀] 頁面上檢視和複製 Gremlin URI 值](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="1622a-180">![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="1622a-181">對於 [密碼] 值，從 [金鑰] 刀鋒視窗複製 [主要金鑰]：![在 Azure 入口網站的 [金鑰] 頁面上檢視和複製主要金鑰](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="1622a-181">For the Password value, copy the **Primary key** from the **Keys** blade: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="1622a-182">執行主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="1622a-182">Run the console app</span></span>

1. <span data-ttu-id="1622a-183">在 git 終端機視窗中，`cd` 至 azure-cosmos-db-graph-java-getting-started 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1622a-183">In the git terminal window, `cd` to the azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="1622a-184">在 git 終端機視窗中，輸入 `mvn package` 以安裝必要的 Java 套件。</span><span class="sxs-lookup"><span data-stu-id="1622a-184">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="1622a-185">在 git 終端機視窗中，於終端機視窗中執行 `mvn exec:java -D exec.mainClass=GetStarted.Program` 以啟動您的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1622a-185">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

<span data-ttu-id="1622a-186">終端機視窗會顯示要新增至圖形的頂點。</span><span class="sxs-lookup"><span data-stu-id="1622a-186">The terminal window displays the vertices being added to the graph.</span></span> <span data-ttu-id="1622a-187">程式完成後，請切換回您的網際網路瀏覽器中的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1622a-187">Once the program completes, switch back to the Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="1622a-188">檢閱並新增範例資料</span><span class="sxs-lookup"><span data-stu-id="1622a-188">Review and add sample data</span></span>

<span data-ttu-id="1622a-189">您現在可以移回 [資料總管] 並查看已新增到圖行的頂點，然後新增額外的資料點。</span><span class="sxs-lookup"><span data-stu-id="1622a-189">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="1622a-190">在 [資料總管] 中，展開 **sample-database**/**sample-graph**，按一下 [圖形]，然後按一下 [新增篩選條件]。</span><span class="sxs-lookup"><span data-stu-id="1622a-190">In Data Explorer, expand the **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![在 Azure 入口網站的 [資料總管] 中建立新文件](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="1622a-192">在 [結果] 清單中，請注意已新增到圖形的新使用者。</span><span class="sxs-lookup"><span data-stu-id="1622a-192">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="1622a-193">選取 **ben**，請注意，他已連線到 robin。</span><span class="sxs-lookup"><span data-stu-id="1622a-193">Select **ben** and notice that he's connected to robin.</span></span> <span data-ttu-id="1622a-194">您可以在圖形總管上移動頂點、放大和縮小，並展開圖形總管介面的大小。</span><span class="sxs-lookup"><span data-stu-id="1622a-194">You can move the vertices around on the graph explorer, zoom in and out, and expand the size of the graph explorer surface.</span></span> 

   ![Azure 入口網站的資料總管之圖形中的新頂點](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="1622a-196">讓我們使用 [資料總管] 將一些新使用者新增至圖形。</span><span class="sxs-lookup"><span data-stu-id="1622a-196">Let's add a few new users to the graph using the Data Explorer.</span></span> <span data-ttu-id="1622a-197">按一下 [新增頂點] 按鈕，將資料新增至您的圖形。</span><span class="sxs-lookup"><span data-stu-id="1622a-197">Click the **New Vertex** button to add data to your graph.</span></span>

   ![在 Azure 入口網站的 [資料總管] 中建立新文件](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="1622a-199">輸入 person 標籤，然後輸入下列索引鍵和值，以在圖形中建立第一個頂點。</span><span class="sxs-lookup"><span data-stu-id="1622a-199">Enter a label of *person* then enter the following keys and values to create the first vertex in the graph.</span></span> <span data-ttu-id="1622a-200">請注意，您可以在圖形中為每個人建立獨特的屬性。</span><span class="sxs-lookup"><span data-stu-id="1622a-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="1622a-201">只需要識別碼索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1622a-201">Only the id key is required.</span></span>

    <span data-ttu-id="1622a-202">key</span><span class="sxs-lookup"><span data-stu-id="1622a-202">key</span></span>|<span data-ttu-id="1622a-203">value</span><span class="sxs-lookup"><span data-stu-id="1622a-203">value</span></span>|<span data-ttu-id="1622a-204">注意事項</span><span class="sxs-lookup"><span data-stu-id="1622a-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="1622a-205">id</span><span class="sxs-lookup"><span data-stu-id="1622a-205">id</span></span>|<span data-ttu-id="1622a-206">ashley</span><span class="sxs-lookup"><span data-stu-id="1622a-206">ashley</span></span>|<span data-ttu-id="1622a-207">頂點的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1622a-207">The unique identifier for the vertex.</span></span> <span data-ttu-id="1622a-208">如果您未指定識別碼，系統會為您產生一個。</span><span class="sxs-lookup"><span data-stu-id="1622a-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="1622a-209">gender</span><span class="sxs-lookup"><span data-stu-id="1622a-209">gender</span></span>|<span data-ttu-id="1622a-210">female</span><span class="sxs-lookup"><span data-stu-id="1622a-210">female</span></span>| 
    <span data-ttu-id="1622a-211">tech</span><span class="sxs-lookup"><span data-stu-id="1622a-211">tech</span></span> | <span data-ttu-id="1622a-212">java</span><span class="sxs-lookup"><span data-stu-id="1622a-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="1622a-213">在本快速入門中，我們會建立非資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="1622a-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="1622a-214">不過，如果您藉由在集合建立期間指定資料分割索引鍵來建立資料分割集合，您就必須包含資料分割索引鍵作為每個新頂點的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1622a-214">However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="1622a-215">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1622a-215">Click **OK**.</span></span> <span data-ttu-id="1622a-216">您可能需要展開畫面，才能在螢幕底部看到 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1622a-216">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

6. <span data-ttu-id="1622a-217">再次按一下 [新增頂點] 並新增額外的新使用者。</span><span class="sxs-lookup"><span data-stu-id="1622a-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="1622a-218">輸入 person 標籤，然後輸入下列索引鍵和值：</span><span class="sxs-lookup"><span data-stu-id="1622a-218">Enter a label of *person* then enter the following keys and values:</span></span>

    <span data-ttu-id="1622a-219">key</span><span class="sxs-lookup"><span data-stu-id="1622a-219">key</span></span>|<span data-ttu-id="1622a-220">value</span><span class="sxs-lookup"><span data-stu-id="1622a-220">value</span></span>|<span data-ttu-id="1622a-221">注意事項</span><span class="sxs-lookup"><span data-stu-id="1622a-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="1622a-222">id</span><span class="sxs-lookup"><span data-stu-id="1622a-222">id</span></span>|<span data-ttu-id="1622a-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="1622a-223">rakesh</span></span>|<span data-ttu-id="1622a-224">頂點的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1622a-224">The unique identifier for the vertex.</span></span> <span data-ttu-id="1622a-225">如果您未指定識別碼，系統會為您產生一個。</span><span class="sxs-lookup"><span data-stu-id="1622a-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="1622a-226">gender</span><span class="sxs-lookup"><span data-stu-id="1622a-226">gender</span></span>|<span data-ttu-id="1622a-227">male</span><span class="sxs-lookup"><span data-stu-id="1622a-227">male</span></span>| 
    <span data-ttu-id="1622a-228">school</span><span class="sxs-lookup"><span data-stu-id="1622a-228">school</span></span>|<span data-ttu-id="1622a-229">MIT</span><span class="sxs-lookup"><span data-stu-id="1622a-229">MIT</span></span>| 

7. <span data-ttu-id="1622a-230">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1622a-230">Click **OK**.</span></span> 

8. <span data-ttu-id="1622a-231">按一下 [套用篩選條件] 並採用預設 `g.V()` 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="1622a-231">Click **Apply Filter** with the default `g.V()` filter.</span></span> <span data-ttu-id="1622a-232">所有使用者現在會顯示在 [結果] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1622a-232">All of the users now show in the **Results** list.</span></span> <span data-ttu-id="1622a-233">隨著您新增更多的資料，您可以使用篩選條件來限制您的結果。</span><span class="sxs-lookup"><span data-stu-id="1622a-233">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="1622a-234">[資料總管] 預設會使用 `g.V()` 來擷取圖形中的所有頂點，但您可以將其變更為不同的[圖形查詢](tutorial-query-graph.md) (例如 `g.V().count()`)，以 JSON 格式傳回圖形中所有頂點的計數。</span><span class="sxs-lookup"><span data-stu-id="1622a-234">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph, but you can change that to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span>

9. <span data-ttu-id="1622a-235">現在我們可以連線 rakesh 和 ashley。</span><span class="sxs-lookup"><span data-stu-id="1622a-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="1622a-236">請確定已在 [結果] 清單中選取 **ashley**，然後按一下右下方 [目標] 旁邊的編輯按鈕。</span><span class="sxs-lookup"><span data-stu-id="1622a-236">Ensure **ashley** in selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span></span> <span data-ttu-id="1622a-237">您可能需要加寬視窗，才可看到 [屬性] 區域。</span><span class="sxs-lookup"><span data-stu-id="1622a-237">You may need to widen your window to see the **Properties** area.</span></span>

   ![變更圖形中頂點的目標](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="1622a-239">在 [目標] 方塊中輸入 rakesh，並在 [邊緣標籤] 方塊中輸入「認識」，然後按一下核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1622a-239">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check box.</span></span>

   ![在 [資料總管] 中新增 ashley 與 rakesh 之間的連線](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="1622a-241">現在從 [結果] 清單中選取 **rakesh** 並查看 ashley 與 rakesh 是否已連線。</span><span class="sxs-lookup"><span data-stu-id="1622a-241">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![[資料總管] 中連線的兩個頂點](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="1622a-243">您也可以使用 [資料總管] 來建立預存程序、UDF 和觸發程序，以執行伺服器端商務邏輯及調整輸送量。</span><span class="sxs-lookup"><span data-stu-id="1622a-243">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="1622a-244">[資料總管] 會公開 API 中所有可用的內建程式設計資料存取，但可讓您在 Azure 入口網站中輕鬆存取您的資料。</span><span class="sxs-lookup"><span data-stu-id="1622a-244">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>



## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1622a-245">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="1622a-245">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1622a-246">清除資源</span><span class="sxs-lookup"><span data-stu-id="1622a-246">Clean up resources</span></span>

<span data-ttu-id="1622a-247">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="1622a-247">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="1622a-248">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="1622a-248">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1622a-249">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="1622a-249">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1622a-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1622a-250">Next steps</span></span>

<span data-ttu-id="1622a-251">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用 [資料總管] 來建立圖形，以及如何執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1622a-251">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="1622a-252">您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="1622a-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1622a-253">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="1622a-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

