---
title: "使用 Azure Cosmos DB 進行 Java 應用程式開發教學課程 | Microsoft Docs"
description: "本 Java Web 應用程式教學課程示範如何使用 Azure Cosmos DB 和 DocumentDB API，來儲存和存取 Azure 網站上所託管的 Java 應用程式資料。"
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
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="fbc71-104">使用 Azure Cosmos DB 和 DocumentDB API 來建置 Java Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fbc71-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc71-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fbc71-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="fbc71-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="fbc71-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="fbc71-107">Java</span><span class="sxs-lookup"><span data-stu-id="fbc71-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="fbc71-108">Python</span><span class="sxs-lookup"><span data-stu-id="fbc71-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="fbc71-109">本 Java Web 應用程式教學課程示範如何使用 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務，來儲存和存取 Azure App Service Web Apps 上所託管的 Java 應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="fbc71-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="fbc71-110">在本主題中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="fbc71-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="fbc71-111">如何在 Eclipse 中建置基本的 JavaServer Pages (JSP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbc71-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="fbc71-112">如何透過 [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)，使用 Azure Cosmos DB 服務。</span><span class="sxs-lookup"><span data-stu-id="fbc71-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="fbc71-113">本 Java 應用程式教學課程會示範如何建立以 Web 為基礎的工作管理應用程式，方便您建立、抓取以及將工作標示為完成，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="fbc71-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="fbc71-114">在 Azure Cosmos DB 中，[待辦事項] 清單中的每項工作都會以 JSON 文件的形式儲存。</span><span class="sxs-lookup"><span data-stu-id="fbc71-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![我的待辦事項清單 Java 應用程式](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="fbc71-116">本應用程式開發教學課程假設您先前已有使用 Java 的經驗。</span><span class="sxs-lookup"><span data-stu-id="fbc71-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="fbc71-117">如果您不熟悉 Java 或[必備工具](#Prerequisites)，我們建議您從 GitHub 下載完整的[待辦事項](https://github.com/Azure-Samples/documentdb-java-todo-app)專案，並使用[本文結尾的指示](#GetProject)開始建置。</span><span class="sxs-lookup"><span data-stu-id="fbc71-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="fbc71-118">建置完成後，您可以檢閱文件，以加深對專案內容中程式碼的了解。</span><span class="sxs-lookup"><span data-stu-id="fbc71-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="fbc71-119"><a id="Prerequisites"></a>針對此 Java Web 應用程式教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="fbc71-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="fbc71-120">開始進行本應用程式開發教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="fbc71-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="fbc71-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fbc71-121">An active Azure account.</span></span> <span data-ttu-id="fbc71-122">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fbc71-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fbc71-123">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="fbc71-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="fbc71-124">或</span><span class="sxs-lookup"><span data-stu-id="fbc71-124">OR</span></span>

    <span data-ttu-id="fbc71-125">本機安裝的 [Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="fbc71-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="fbc71-127">Eclipse IDE for Java EE Developers。</span><span class="sxs-lookup"><span data-stu-id="fbc71-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="fbc71-128">已啟用某個 Java Runtime Environment (例如 Tomcat 或 Jetty) 的 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="fbc71-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="fbc71-129">如果您是第一次安裝這些工具，coreservlets.com 提供了安裝程序的的逐步解說，請參閱其 [教學課程：安裝 TomCat7 並與 Eclipse 搭配使用](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) 一文中的 [快速入門] 區段。</span><span class="sxs-lookup"><span data-stu-id="fbc71-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="fbc71-130"><a id="CreateDB"></a>步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="fbc71-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="fbc71-131">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="fbc71-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="fbc71-132">如果您已經擁有帳戶，或如果您正在使用 Azure Cosmos DB 模擬器來進行本教學課程，可以跳到[步驟 2：建立 Java JSP 應用程式](#CreateJSP)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="fbc71-133"><a id="CreateJSP"></a>步驟 2：建立 Java JSP 應用程式</span><span class="sxs-lookup"><span data-stu-id="fbc71-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="fbc71-134">建立 JSP 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fbc71-134">To create the JSP application:</span></span>

1. <span data-ttu-id="fbc71-135">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="fbc71-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="fbc71-136">啟動 Eclipse，依序按一下 [檔案]、[新增] 和 [動態 Web 專案]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="fbc71-137">如果您在可用專案中沒有看到 [動態 Web 專案]，請執行下列動作：依序按一下 [檔案]、[新增]、[專案]，展開 [Web]，按一下 [動態 Web 專案]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java 應用程式開發](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="fbc71-139">在 [專案名稱] 方塊中輸入專案名稱，然後在 [目標執行階段] 下拉式選單中，選擇性地選取值 (例如 Apache Tomcat v7.0)，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="fbc71-140">選取目標執行階段可讓您透過 Eclipse 在本機執行專案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="fbc71-141">在 Eclipse 的 [專案總管] 檢視中，展開您的專案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="fbc71-142">在 [WebContent] 上按一下滑鼠右鍵、按一下 [新增]，然後按一下 [JSP 檔案]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="fbc71-143">在 [新增 JSP 檔案] 對話方塊中，將檔案命名為 **index.jsp**。</span><span class="sxs-lookup"><span data-stu-id="fbc71-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="fbc71-144">將上層資料夾保持為 **WebContent**，如下圖所示，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![建立新的 JSP 檔案 - Java Web 應用程式教學課程](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="fbc71-146">在 [選取 JSP 範本] 對話方塊中，基於本教學課程的目的，選取 [新增 JSP 檔案 (html)]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="fbc71-147">在 Eclipse 中開啟 index.jsp 檔案時，請加入文字以顯示 **Hello World!**。</span><span class="sxs-lookup"><span data-stu-id="fbc71-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="fbc71-148">(在現有 <body> 元素內)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-148">within the existing <body> element.</span></span> <span data-ttu-id="fbc71-149">您已更新的 <body> 內容看起來應該與下列程式碼類似：</span><span class="sxs-lookup"><span data-stu-id="fbc71-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="fbc71-150">儲存 index.jsp 檔案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="fbc71-151">如果您在步驟 2 中已設定目標執行階段，就可以依序按一下 [專案] 和 [執行]，即可在本機執行您的 JSP 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fbc71-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World – Java 應用程式教學課程](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="fbc71-153"><a id="InstallSDK"></a>步驟 3：安裝 DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="fbc71-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="fbc71-154">導入 DocumentDB Java SDK 及其相依性的最簡單方式就是透過 [Apache Maven](http://maven.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="fbc71-155">若要這樣做，您必須完成下列步驟以將專案轉換成 maven 專案：</span><span class="sxs-lookup"><span data-stu-id="fbc71-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="fbc71-156">在 [專案總管] 中，以滑鼠右鍵按一下您的專案，按一下 [設定]，然後按一下 [轉換成 Maven 專案]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="fbc71-157">在 [建立新的 POM] 視窗中，接受預設值，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="fbc71-158">在 [專案總管] 中，開啟 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="fbc71-159">在 [相依性] 窗格的 [相依性] 索引標籤中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="fbc71-160">在 [選取相依性]  視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fbc71-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="fbc71-161">在 [群組識別碼] 方塊中，輸入 com.microsoft.azure。</span><span class="sxs-lookup"><span data-stu-id="fbc71-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="fbc71-162">在 [構件識別碼] 方塊中，輸入 azure-documentdb。</span><span class="sxs-lookup"><span data-stu-id="fbc71-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="fbc71-163">在 [版本] 方塊中，輸入 1.5.1。</span><span class="sxs-lookup"><span data-stu-id="fbc71-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![安裝 DocumentDB Java 應用程式 SDK](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="fbc71-165">或透過文字編輯器，將群組識別碼和構件識別碼的相依性 XML 直接新增至 pom.xml：</span><span class="sxs-lookup"><span data-stu-id="fbc71-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="fbc71-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="fbc71-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="fbc71-167">按一下 [確定]，Maven 便會開始安裝 DocumentDB Java SDK。</span><span class="sxs-lookup"><span data-stu-id="fbc71-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="fbc71-168">儲存 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="fbc71-169"><a id="UseService"></a>步驟 4：在 Java 應用程式中使用 Azure Cosmos DB 服務</span><span class="sxs-lookup"><span data-stu-id="fbc71-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="fbc71-170">首先，讓我們在 TodoItem.java 中定義 TodoItem 物件：</span><span class="sxs-lookup"><span data-stu-id="fbc71-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="fbc71-171">在此專案中，我們會使用 [Project Lombok](http://projectlombok.org/) 來產生建構函式、getter、setter 及產生器。</span><span class="sxs-lookup"><span data-stu-id="fbc71-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="fbc71-172">或者，您也可以手動撰寫此程式碼，或讓 IDE 產生它。</span><span class="sxs-lookup"><span data-stu-id="fbc71-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="fbc71-173">若要叫用 Azure Cosmos DB 服務，您必須將新的 **DocumentClient**具現化。</span><span class="sxs-lookup"><span data-stu-id="fbc71-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="fbc71-174">一般而言，最好是重複使用 **DocumentClient** ，而不要針對每個後續要求建構新的用戶端。</span><span class="sxs-lookup"><span data-stu-id="fbc71-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="fbc71-175">我們可以將用戶端包裝在 **DocumentClientFactory**中以重複使用用戶端。</span><span class="sxs-lookup"><span data-stu-id="fbc71-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="fbc71-176">您必須在 DocumentClientFactory.java 中，貼上您在[步驟 1](#CreateDB) 中儲存到剪貼簿的 URI 和主要金鑰值。</span><span class="sxs-lookup"><span data-stu-id="fbc71-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="fbc71-177">將 [YOUR\_ENDPOINT\_HERE] 以您的 URI 取代，並將 [YOUR\_KEY\_HERE] 以您的主要金鑰取代。</span><span class="sxs-lookup"><span data-stu-id="fbc71-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="fbc71-178">現在，讓我們建立「資料存取物件」(DAO)，以將我們的待辦事項提取保存至 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="fbc71-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="fbc71-179">為了將 ToDo 項目儲存至集合，用戶端必須知道要保存至哪個資料庫和集合 (會被自我連結參照)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="fbc71-180">一般而言，最好是儘可能快取資料庫和集合，以避免對資料庫進行額外的來回存取。</span><span class="sxs-lookup"><span data-stu-id="fbc71-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="fbc71-181">下列程式碼說明如何抓取我們的資料庫和集合 (如果存在)，或建立一個新的資料庫或集合 (如果不存在)：</span><span class="sxs-lookup"><span data-stu-id="fbc71-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="fbc71-182">下一步是撰寫一些程式碼以將 TodoItems 保存至集合。</span><span class="sxs-lookup"><span data-stu-id="fbc71-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="fbc71-183">在此範例中，我們將使用 [Gson](https://code.google.com/p/google-gson/) 將 TodoItem Plain Old Java Objects (POJO) 序列化及還原序列化成 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="fbc71-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="fbc71-184">與 Azure Cosmos DB 資料庫和集合相同，文件也會由自我連結參照。</span><span class="sxs-lookup"><span data-stu-id="fbc71-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="fbc71-185">下列 helper 函式可讓我們依另一個屬性 (例如 "id") 抓取文件，而不是依自我連結：</span><span class="sxs-lookup"><span data-stu-id="fbc71-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. <span data-ttu-id="fbc71-186">我們可以使用步驟 5 中的 helper 方法來依 id 抓取 TodoItem JSON 文件，然後再將其還原序列化成 POJO：</span><span class="sxs-lookup"><span data-stu-id="fbc71-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="fbc71-187">我們也可以使用 DocumentDB SQL，以 DocumentClient 取得集合或 TodoItems 的清單：</span><span class="sxs-lookup"><span data-stu-id="fbc71-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="fbc71-188">以 DocumentClient 更新文件的方法有很多個。</span><span class="sxs-lookup"><span data-stu-id="fbc71-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="fbc71-189">在我們的待辦事項清單應用程式中，我們希望能夠切換顯示 TodoItem 是否已完成。</span><span class="sxs-lookup"><span data-stu-id="fbc71-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="fbc71-190">這個目的可以藉由更新文件中的 "complete" 屬性來達成：</span><span class="sxs-lookup"><span data-stu-id="fbc71-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="fbc71-191">最後，我們希望能夠從清單中刪除 TodoItem。</span><span class="sxs-lookup"><span data-stu-id="fbc71-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="fbc71-192">若要這樣做，我們可以使用我們稍早撰寫的 helper 方法來抓取自我連結，然後告訴用戶端將它刪除：</span><span class="sxs-lookup"><span data-stu-id="fbc71-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="fbc71-193"><a id="Wire"></a>步驟 5：將 Java 應用程式開發專案的其他部分串接在一起</span><span class="sxs-lookup"><span data-stu-id="fbc71-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="fbc71-194">既然我們已經完成主要的部分，剩下的就是建置一個快速的使用者介面，然後將其串接到我們的 DAO。</span><span class="sxs-lookup"><span data-stu-id="fbc71-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="fbc71-195">首先，讓我們著手建置一個控制器來呼叫我們的 DAO：</span><span class="sxs-lookup"><span data-stu-id="fbc71-195">First, let's start with building a controller to call our DAO:</span></span>
   
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
   
    <span data-ttu-id="fbc71-196">在較複雜的應用程式中，除了 DAO 之外，控制器可能還有複雜的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="fbc71-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="fbc71-197">接著，我們將建立一個可將 HTTP 要求遞送至控制器的 Servlet：</span><span class="sxs-lookup"><span data-stu-id="fbc71-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
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
3. <span data-ttu-id="fbc71-198">我們需要一個可對使用者顯示的 Web 使用者介面。</span><span class="sxs-lookup"><span data-stu-id="fbc71-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="fbc71-199">讓我們重新撰寫稍早建立的 index.jsp：</span><span class="sxs-lookup"><span data-stu-id="fbc71-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="fbc71-200">最後，撰寫一些用戶端 JavaScript，以將 Web 使用者介面與 Servlet 繫結在一起：</span><span class="sxs-lookup"><span data-stu-id="fbc71-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. <span data-ttu-id="fbc71-201">好極了！</span><span class="sxs-lookup"><span data-stu-id="fbc71-201">Awesome!</span></span> <span data-ttu-id="fbc71-202">現在只剩下測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="fbc71-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="fbc71-203">在本機執行應用程式，並填入項目名稱和類別，然後按一下 [ **新增工作**] 來新增一些待辦事項。</span><span class="sxs-lookup"><span data-stu-id="fbc71-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="fbc71-204">當項目出現時，您可以切換勾選核取方塊，然後按一下 [更新工作] ，來更新其完成狀態。</span><span class="sxs-lookup"><span data-stu-id="fbc71-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="fbc71-205"><a id="Deploy"></a>步驟 6：將 Java 應用程式部署至 Azure 網站</span><span class="sxs-lookup"><span data-stu-id="fbc71-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="fbc71-206">Azure 網站讓部署 Java 應用程式變得相當簡單，您只需將應用程式匯出成 WAR 檔案，然後透過原始檔控制 (例如 Git) 或 FTP 上傳它即可。</span><span class="sxs-lookup"><span data-stu-id="fbc71-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="fbc71-207">若要將應用程式匯出成 WAR 檔案，請以滑鼠右鍵按一下您在**專案總管**中的專案，按一下 [匯出]，然後按一下 [WAR 檔案]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="fbc71-208">在 [WAR 匯出]  視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fbc71-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="fbc71-209">在 [Web 專案] 方塊中，輸入 azure-documentdb-java-sample。</span><span class="sxs-lookup"><span data-stu-id="fbc71-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="fbc71-210">在 [目的地] 方塊中，選擇用來儲存 WAR 檔案的目的地。</span><span class="sxs-lookup"><span data-stu-id="fbc71-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="fbc71-211">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="fbc71-211">Click **Finish**.</span></span>
3. <span data-ttu-id="fbc71-212">現在您手上已經有了 WAR 檔案，您只需將它上傳至您 Azure 網站的 **webapps** 目錄即可。</span><span class="sxs-lookup"><span data-stu-id="fbc71-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="fbc71-213">如需上傳檔案的相關指示，請參閱[將 Java 應用程式新增至 Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="fbc71-214">將 WAR 檔案上傳至 webapps 目錄之後，執行階段環境便會偵測到您已新增它，並自動將其載入。</span><span class="sxs-lookup"><span data-stu-id="fbc71-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="fbc71-215">若要檢視您已完成的產品，請瀏覽至 http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/，並開始新增您的工作！</span><span class="sxs-lookup"><span data-stu-id="fbc71-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="fbc71-216"><a id="GetProject"></a>從 GitHub 取得的專案</span><span class="sxs-lookup"><span data-stu-id="fbc71-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="fbc71-217">本教學課程中的所有範例都包含在 GitHub 上的 [待辦事項](https://github.com/Azure-Samples/documentdb-java-todo-app) 專案中。</span><span class="sxs-lookup"><span data-stu-id="fbc71-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="fbc71-218">若要將 todo 專案匯入 Eclipse，請確認您擁有 [必要條件](#Prerequisites) 區段中所列出的軟體和資源，然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fbc71-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="fbc71-219">安裝 [專案 Lombok](http://projectlombok.org/)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="fbc71-220">Lombok 可用來在專案中產生建構函式、getter、setter。</span><span class="sxs-lookup"><span data-stu-id="fbc71-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="fbc71-221">下載 lombok.jar 檔案之後，請連按兩下進行安裝，或從命令列進行安裝。</span><span class="sxs-lookup"><span data-stu-id="fbc71-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="fbc71-222">如果 Eclipse 為開啟狀態，請將它關閉並重新啟動以載入 Lombok。</span><span class="sxs-lookup"><span data-stu-id="fbc71-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="fbc71-223">在 Eclipse 的 [檔案] 功能表上，按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="fbc71-224">在 [匯入] 視窗中，依序按一下 [Git]、[使用 Git 的專案] 和 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="fbc71-225">在 [選取儲存機制來源] 畫面上，按一下 [複製 URI]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="fbc71-226">在 [來源 Git 存放庫] 畫面的 [URI] 方塊中，輸入 https://github.com/Azure-Samples/java-todo-app.git，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="fbc71-227">在 [分支選取] 畫面上，確定已選取 [主要]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="fbc71-228">在 [本機目的地] 畫面上，按一下 [瀏覽] 以選取可以複製儲存機制的資料夾，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="fbc71-229">在 [選取要用於匯入專案的精靈] 畫面上，確定已選取 [匯入現有的專案]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="fbc71-230">在 [匯入專案] 畫面上，取消選取 **DocumentDB** 專案，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="fbc71-231">DocumentDB 專案包含 Azure Cosmos DB Java SDK，我們將會改成新增為相依性。</span><span class="sxs-lookup"><span data-stu-id="fbc71-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="fbc71-232">在 [專案總管] 中，瀏覽至 azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java，並將 [主機] 和 [MASTER_KEY] 值取代為您 Azure Cosmos DB 帳戶的 [URI] 和 [主要金鑰]，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fbc71-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="fbc71-233">如需詳細資訊，請參閱[步驟 1。建立 Azure Cosmos DB 資料庫帳戶](#CreateDB)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="fbc71-234">在 [專案總管] 中，以滑鼠右鍵按一下 **azure-documentdb-java-sample**，按一下 [組建路徑]，然後按一下 [設定組建路徑]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="fbc71-235">在 [Java 組建路徑] 畫面的右側窗格中，選取 [程式庫] 索引標籤，然後按一下 [新增外部 JAR]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="fbc71-236">瀏覽至 lombok.jar 檔案的位置，按一下 [開啟]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="fbc71-237">使用步驟 12 重新開啟 [屬性] 視窗，然後在左側窗格中按一下 [目標執行階段]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="fbc71-238">在 [目標執行階段] 畫面上，按一下 [新增]，選取 [Apache Tomcat v7.0]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="fbc71-239">使用步驟 12 重新開啟 [屬性] 視窗，然後在左側窗格中按一下 [專案 Facet]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="fbc71-240">在 [專案 Facet] 畫面上，選取 [動態 Web 模組] 和 [Java]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="fbc71-241">在螢幕底部的 [伺服器] 索引標籤上，以滑鼠右鍵按一下 [在 localhost 的 Tomcat v7.0 伺服器]，然後按一下 [新增和移除]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="fbc71-242">在 [新增和移除] 視窗中，將 [azure-documentdb-java-sample] 移至 [已設定] 方塊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="fbc71-243">在 [伺服器] 索引標籤上，以滑鼠右鍵按一下 [Tomcat v7.0 Server at localhost] \(在 localhost 的 Tomcat v7.0 伺服器)，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="fbc71-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="fbc71-244">在瀏覽器中，瀏覽至 http://localhost:8080/azure-documentdb-java-sample/，並開始新增至您的工作清單。</span><span class="sxs-lookup"><span data-stu-id="fbc71-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="fbc71-245">請注意，如果您之前變更預設的連接埠值，請將 8080 變更為您所選取的值。</span><span class="sxs-lookup"><span data-stu-id="fbc71-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="fbc71-246">若要將您的專案部署至 Azure 網站，請參閱[步驟 6：將應用程式部署至 Azure 網站](#Deploy)。</span><span class="sxs-lookup"><span data-stu-id="fbc71-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
