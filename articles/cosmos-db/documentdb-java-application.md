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
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="99a5e-104">建置 Java web 應用程式使用 Azure Cosmos DB 和 hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="99a5e-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99a5e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="99a5e-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="99a5e-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="99a5e-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="99a5e-107">Java</span><span class="sxs-lookup"><span data-stu-id="99a5e-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="99a5e-108">Python</span><span class="sxs-lookup"><span data-stu-id="99a5e-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="99a5e-109">此 Java web 應用程式教學課程會示範如何 toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務 toostore 及存取資料，從裝載於 Azure App Service Web 應用程式的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99a5e-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="99a5e-110">在本主題中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="99a5e-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="99a5e-111">如何 toobuild 在 Eclipse 中的基本 JavaServer 頁面 (JSP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99a5e-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="99a5e-112">以 hello Azure Cosmos DB toowork 服務使用 hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="99a5e-113">此 Java 應用程式教學課程會示範影響工作以 web 為基礎的 toocreate 工作管理應用程式，可讓您 toocreate、 擷取、 並將標記為完成，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="99a5e-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="99a5e-114">每個 hello ToDo 清單中的 hello 工作會儲存為 Azure Cosmos DB 中的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="99a5e-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![我的待辦事項清單 Java 應用程式](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="99a5e-116">本應用程式開發教學課程假設您先前已有使用 Java 的經驗。</span><span class="sxs-lookup"><span data-stu-id="99a5e-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="99a5e-117">如果您是新 tooJava 或 hello[必要條件工具](#Prerequisites)，我們建議您下載完整的 hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)專案從 GitHub 及建置使用[hello 這個 hello 結尾的指示發行項](#GetProject)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="99a5e-118">一旦建立它，您可以檢閱 hello 文章 toogain 深入了解 hello hello hello 專案內容中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="99a5e-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="99a5e-119"><a id="Prerequisites"></a>針對此 Java Web 應用程式教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="99a5e-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="99a5e-120">在開始此應用程式開發人員教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="99a5e-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="99a5e-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="99a5e-121">An active Azure account.</span></span> <span data-ttu-id="99a5e-122">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99a5e-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="99a5e-123">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="99a5e-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="99a5e-124">或</span><span class="sxs-lookup"><span data-stu-id="99a5e-124">OR</span></span>

    <span data-ttu-id="99a5e-125">Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="99a5e-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="99a5e-127">Eclipse IDE for Java EE Developers。</span><span class="sxs-lookup"><span data-stu-id="99a5e-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="99a5e-128">已啟用某個 Java Runtime Environment (例如 Tomcat 或 Jetty) 的 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="99a5e-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="99a5e-129">如果您要安裝這些工具 hello 第一次，coreservlets.com 提供 hello hello 快速入門 區段中的安裝程序的逐步解說，其[教學課程： 安裝 TomCat7 和使用 Eclipse 向](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html)發行項。</span><span class="sxs-lookup"><span data-stu-id="99a5e-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="99a5e-130"><a id="CreateDB"></a>步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="99a5e-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="99a5e-131">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="99a5e-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="99a5e-132">如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立 hello Java JSP 應用程式](#CreateJSP)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="99a5e-133"><a id="CreateJSP"></a>步驟 2： 建立 hello Java JSP 應用程式</span><span class="sxs-lookup"><span data-stu-id="99a5e-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="99a5e-134">toocreate hello JSP 應用程式：</span><span class="sxs-lookup"><span data-stu-id="99a5e-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="99a5e-135">首先，我們將從建立 Java 專案開始。</span><span class="sxs-lookup"><span data-stu-id="99a5e-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="99a5e-136">啟動 Eclipse，依序按一下 [檔案]、[新增] 和 [動態 Web 專案]。</span><span class="sxs-lookup"><span data-stu-id="99a5e-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="99a5e-137">如果您沒有看到**動態 Web 專案**列為可用的專案，請執行下列 hello： 按一下**檔案**，按一下 **新增**，按一下 **專案**...，展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java 應用程式開發](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="99a5e-139">輸入專案名稱在 hello**專案名稱**] 方塊中，在 hello**目標執行階段**下拉式選單，選擇性地選取 [值 (例如 Apache Tomcat v7.0)，然後按一下**完成**.</span><span class="sxs-lookup"><span data-stu-id="99a5e-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="99a5e-140">選取目標執行階段可讓您 toorun 您在本機透過 Eclipse 的專案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="99a5e-141">在 Eclipse 中，在 hello [專案總管] 檢視中，展開您的專案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="99a5e-142">在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="99a5e-143">在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="99a5e-144">保留 hello 父資料夾為**WebContent**示 hello 遵循圖例，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![建立新的 JSP 檔案 - Java Web 應用程式教學課程](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="99a5e-146">在 hello**選取 JSP 範本**對話方塊中的，為了這個教學課程，請選取在 hello**新增 JSP 檔案 (html)**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="99a5e-147">在 Eclipse 中，開啟 hello index.jsp 檔案，當新增文字 toodisplay **Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="99a5e-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="99a5e-148">在現有的 hello<body>項目。</span><span class="sxs-lookup"><span data-stu-id="99a5e-148">within hello existing <body> element.</span></span> <span data-ttu-id="99a5e-149">您已更新<body>內容應該看起來像下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="99a5e-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="99a5e-150">儲存 hello index.jsp 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="99a5e-151">如果您在步驟 2 中設定目標執行階段，您可以按一下**專案**然後**執行**toorun JSP 應用程式在本機上：</span><span class="sxs-lookup"><span data-stu-id="99a5e-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World – Java 應用程式教學課程](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="99a5e-153"><a id="InstallSDK"></a>步驟 3： 安裝 hello DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="99a5e-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="99a5e-154">hello hello DocumentDB Java SDK 和其相依性中的最簡單方式 toopull 是透過[Apache Maven](http://maven.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="99a5e-155">toodo，您將需要 tooconvert 專案 tooa maven 專案藉由完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="99a5e-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="99a5e-156">以滑鼠右鍵按一下 hello 專案總管 中的專案中，按一下**設定**，按一下 **轉換 tooMaven 專案**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="99a5e-157">在 hello**建立新的 POM**視窗中，接受 hello 預設值，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="99a5e-158">在**Project Explorer**，開啟 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="99a5e-159">在 hello**相依性**索引標籤上，在 hello**相依性** 窗格中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="99a5e-160">在 hello**選取相依性**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="99a5e-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="99a5e-161">在 hello**群組識別碼**方塊中，輸入 com.microsoft.azure。</span><span class="sxs-lookup"><span data-stu-id="99a5e-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="99a5e-162">在 hello**成品 Id**方塊中，輸入 azure documentdb。</span><span class="sxs-lookup"><span data-stu-id="99a5e-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="99a5e-163">在 hello**版本**方塊中，輸入 1.5.1。</span><span class="sxs-lookup"><span data-stu-id="99a5e-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![安裝 DocumentDB Java 應用程式 SDK](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="99a5e-165">群組識別碼和成品 Id 加入 hello 相依 XML 或文字編輯器透過直接 toohello pom.xml:</span><span class="sxs-lookup"><span data-stu-id="99a5e-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="99a5e-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="99a5e-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="99a5e-167">按一下**確定**Maven 安裝 hello DocumentDB Java SDK。</span><span class="sxs-lookup"><span data-stu-id="99a5e-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="99a5e-168">儲存 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="99a5e-169"><a id="UseService"></a>步驟 4： 使用 Java 應用程式中的 hello Azure Cosmos DB 服務</span><span class="sxs-lookup"><span data-stu-id="99a5e-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="99a5e-170">首先，我們定義 TodoItem.java hello TodoItem 物件：</span><span class="sxs-lookup"><span data-stu-id="99a5e-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="99a5e-171">在此專案中，我們會使用[專案 Lombok](http://projectlombok.org/) toogenerate hello 建構函式、 getter、 setter 和產生器。</span><span class="sxs-lookup"><span data-stu-id="99a5e-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="99a5e-172">或者，您可以手動撰寫此程式碼，或有 hello IDE 產生它。</span><span class="sxs-lookup"><span data-stu-id="99a5e-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="99a5e-173">tooinvoke hello Azure Cosmos 資料庫服務，您必須具現化新**DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="99a5e-174">一般而言，最好是最佳 tooreuse hello **DocumentClient** -而不是比建構新的用戶端針對每個後續的要求。</span><span class="sxs-lookup"><span data-stu-id="99a5e-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="99a5e-175">我們可以換行中的 hello 用戶端連線，重複使用 hello 用戶端**DocumentClientFactory**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="99a5e-176">DocumentClientFactory.java，在您需要 toopaste hello URI 與主索引鍵的值儲存在 tooyour 剪貼簿[步驟 1](#CreateDB)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="99a5e-177">將 [YOUR\_ENDPOINT\_HERE] 以您的 URI 取代，並將 [YOUR\_KEY\_HERE] 以您的主要金鑰取代。</span><span class="sxs-lookup"><span data-stu-id="99a5e-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="99a5e-178">現在讓我們來建立資料存取物件 (DAO) tooabstract 保存我們 ToDo 項目 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="99a5e-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="99a5e-179">若要 toosave ToDo 項目 tooa 集合，hello 用戶端必須 tooknow 哪一個資料庫與集合 toopersist 太 （做為參考的自我連結）。</span><span class="sxs-lookup"><span data-stu-id="99a5e-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="99a5e-180">一般情況下，它是最佳的 toocache hello 資料庫與集合盡可能 tooavoid 額外往返 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="99a5e-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="99a5e-181">hello 下列程式碼說明如何 tooretrieve 我們的資料庫，如果它存在，或如果不存在，請建立一個新的集合：</span><span class="sxs-lookup"><span data-stu-id="99a5e-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
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
4. <span data-ttu-id="99a5e-182">hello 下一個步驟為 toowrite toohello 集合中的某些程式碼 toopersist hello TodoItems。</span><span class="sxs-lookup"><span data-stu-id="99a5e-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="99a5e-183">在此範例中，我們將使用[Gson](https://code.google.com/p/google-gson/) tooserialize 和還原序列化 TodoItem 純舊 Java 物件 (POJOs) tooJSON 文件。</span><span class="sxs-lookup"><span data-stu-id="99a5e-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
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
5. <span data-ttu-id="99a5e-184">與 Azure Cosmos DB 資料庫和集合相同，文件也會由自我連結參照。</span><span class="sxs-lookup"><span data-stu-id="99a5e-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="99a5e-185">hello 下列 helper 函式可讓我們擷取文件的其他屬性 (例如"id")，而不是自我連結：</span><span class="sxs-lookup"><span data-stu-id="99a5e-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
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
6. <span data-ttu-id="99a5e-186">我們可以在步驟 5 tooretrieve TodoItem JSON 文件中使用識別碼 hello helper 方法，然後將它還原序列化 tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="99a5e-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
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
7. <span data-ttu-id="99a5e-187">我們也可以使用 hello DocumentClient tooget 集合或使用 DocumentDB SQL TodoItems 的清單：</span><span class="sxs-lookup"><span data-stu-id="99a5e-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
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
8. <span data-ttu-id="99a5e-188">有許多方式 tooupdate 文件以 hello DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="99a5e-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="99a5e-189">在 Todo 清單應用程式中，我們想要 toobe 無法 tootoggle 是否已完成的 TodoItem。</span><span class="sxs-lookup"><span data-stu-id="99a5e-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="99a5e-190">這可以藉由更新 hello hello 文件中的 「 完成 」 屬性來達成：</span><span class="sxs-lookup"><span data-stu-id="99a5e-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
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
9. <span data-ttu-id="99a5e-191">最後，我們想 hello 能力 toodelete TodoItem 從我們的清單。</span><span class="sxs-lookup"><span data-stu-id="99a5e-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="99a5e-192">toodo，我們可以使用我們稍早所說明的 hello helper 方法 tooretrieve hello 自我連結，然後告訴 hello 用戶端 toodelete 它：</span><span class="sxs-lookup"><span data-stu-id="99a5e-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
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

## <span data-ttu-id="99a5e-193"><a id="Wire"></a>步驟 5： 接線 hello hello Java 應用程式開發專案的其餘部分一起</span><span class="sxs-lookup"><span data-stu-id="99a5e-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="99a5e-194">我們已經完成 hello 有趣 bits-剩下的是 toobuild 快速的使用者介面，和裝設 tooour DAO。</span><span class="sxs-lookup"><span data-stu-id="99a5e-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="99a5e-195">首先，讓我們開始建置我們 DAO 控制器 toocall:</span><span class="sxs-lookup"><span data-stu-id="99a5e-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="99a5e-196">在更複雜的應用程式，hello 控制器可能包含複雜的商務邏輯 hello DAO 之上。</span><span class="sxs-lookup"><span data-stu-id="99a5e-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="99a5e-197">接下來，我們將建立 servlet tooroute HTTP 要求 toohello 控制器：</span><span class="sxs-lookup"><span data-stu-id="99a5e-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="99a5e-198">我們需要 web 使用者介面 toodisplay toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="99a5e-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="99a5e-199">讓我們重新撰寫 hello index.jsp 我們稍早建立：</span><span class="sxs-lookup"><span data-stu-id="99a5e-199">Let's re-write hello index.jsp we created earlier:</span></span>
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
4. <span data-ttu-id="99a5e-200">最後，某些用戶端 JavaScript tootie hello web 使用者介面和寫 hello servlet 一起：</span><span class="sxs-lookup"><span data-stu-id="99a5e-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
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
5. <span data-ttu-id="99a5e-201">好極了！</span><span class="sxs-lookup"><span data-stu-id="99a5e-201">Awesome!</span></span> <span data-ttu-id="99a5e-202">現在，剩下的是 tootest hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99a5e-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="99a5e-203">在本機執行 hello 應用程式，並加入一些 Todo 項目填入 hello 項目名稱和類別目錄，然後按一下**加入工作**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="99a5e-204">Hello 項目出現時，您可以更新是否已完成切換 hello 核取方塊，然後按一下**更新工作**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="99a5e-205"><a id="Deploy"></a>步驟 6： 部署您的 Java 應用程式 tooAzure 網站</span><span class="sxs-lookup"><span data-stu-id="99a5e-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="99a5e-206">Azure 網站讓部署 Java 應用程式變得相當簡單，您只需將應用程式匯出成 WAR 檔案，然後透過原始檔控制 (例如 Git) 或 FTP 上傳它即可。</span><span class="sxs-lookup"><span data-stu-id="99a5e-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="99a5e-207">tooexport 應用程式為 WAR 檔案，以滑鼠右鍵按一下您的專案中**專案總管**，按一下 **匯出**，然後按一下 **WAR 檔案**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="99a5e-208">在 hello**匯出 WAR**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="99a5e-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="99a5e-209">在 hello Web 專案中，輸入 azure documentdb 的 java 範例。</span><span class="sxs-lookup"><span data-stu-id="99a5e-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="99a5e-210">在 hello 目的地方塊中，選擇目的地 toosave hello WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="99a5e-211">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="99a5e-211">Click **Finish**.</span></span>
3. <span data-ttu-id="99a5e-212">既然您手中有 WAR 檔案，您可以直接將它上傳 tooyour Azure 網站的**webapps**目錄。</span><span class="sxs-lookup"><span data-stu-id="99a5e-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="99a5e-213">上傳 hello 檔案的指示，請參閱[新增 App Service Web 應用程式的 Java 應用程式 tooAzure](../app-service-web/web-sites-java-add-app.md)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="99a5e-214">一旦 hello WAR 檔案已上傳的 toohello webapps 目錄，hello 執行階段環境會偵測您已新增，並會自動載入。</span><span class="sxs-lookup"><span data-stu-id="99a5e-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="99a5e-215">tooview 成品，瀏覽 toohttp://YOUR\_網站\_NAME.azurewebsites.net/azure-java-sample/ 並開始將您的工作 ！</span><span class="sxs-lookup"><span data-stu-id="99a5e-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="99a5e-216"><a id="GetProject"></a>從 GitHub 取得 hello 專案</span><span class="sxs-lookup"><span data-stu-id="99a5e-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="99a5e-217">在本教學課程的所有 hello 範例都包含在 hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub 上的專案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="99a5e-218">tooimport hello todo 專案 Eclipse 中，請確定您有 hello 軟體和 hello 中列出的資源[必要條件](#Prerequisites)區段，然後執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="99a5e-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="99a5e-219">安裝 [專案 Lombok](http://projectlombok.org/)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="99a5e-220">Lombok 是使用的 toogenerate 建構函式、 getter、 setter hello 專案中。</span><span class="sxs-lookup"><span data-stu-id="99a5e-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="99a5e-221">一旦您已下載 hello lombok.jar 檔案，請按兩下該 tooinstall 它，或從 hello 命令列安裝它。</span><span class="sxs-lookup"><span data-stu-id="99a5e-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="99a5e-222">如果 Eclipse 已開啟，關閉它，並重新啟動它 tooload Lombok。</span><span class="sxs-lookup"><span data-stu-id="99a5e-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="99a5e-223">在 Eclipse 中，在 hello**檔案**功能表上，按一下 **匯入**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="99a5e-224">在 hello**匯入**視窗中，按一下**Git**，按一下**從 Git 專案**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="99a5e-225">在 hello**選取儲存機制來源**畫面上，按一下**複製 URI**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="99a5e-226">在 hello**來源 Git 儲存機制**畫面中 hello **URI**方塊、 輸入 https://github.com/Azure-Samples/java-todo-app.git，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="99a5e-227">在 hello**分支選取**畫面上，確認**主要**已選取，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="99a5e-228">在 hello**本機目的地**畫面上，按一下**瀏覽**tooselect hello 儲存機制可複製、，然後按一下資料夾**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="99a5e-229">在 hello**選取匯入專案精靈 toouse**畫面上，確認**匯入現有專案**已選取，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="99a5e-230">在 hello**匯入專案**螢幕、 取消選取 hello **DocumentDB**專案，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="99a5e-231">hello DocumentDB 專案包含 hello Azure Cosmos DB Java SDK，我們將會改為加入做為相依性。</span><span class="sxs-lookup"><span data-stu-id="99a5e-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="99a5e-232">在**Project Explorer**、 瀏覽 tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java 及 hello 主機和 MASTER_KEY 值取代為 hello URI 和主索引鍵您 Azure Cosmos DB 帳戶，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="99a5e-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="99a5e-233">如需詳細資訊，請參閱[步驟 1。建立 Azure Cosmos DB 資料庫帳戶](#CreateDB)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="99a5e-234">在**專案總管 中**，以滑鼠右鍵按一下 hello **azure documentdb 的 java 範例**，按一下**組建路徑**，然後按一下**設定組建路徑**.</span><span class="sxs-lookup"><span data-stu-id="99a5e-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="99a5e-235">在 hello **Java 組建路徑**畫面上，hello 右窗格中，選取 hello**文件庫**索引標籤，然後再按一下**新增外部 Jar**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="99a5e-236">瀏覽 toohello hello lombok.jar 檔案位置，然後按一下**開啟**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="99a5e-237">使用步驟 12 tooopen hello**屬性**視窗一次，然後在 hello 左窗格按一下**目標執行階段**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="99a5e-238">Hello 上**目標執行階段**畫面上，按一下**新增**，選取**Apache Tomcat v7.0**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="99a5e-239">使用步驟 12 tooopen hello**屬性**視窗一次，然後在 hello 左窗格按一下**專案 Facet**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="99a5e-240">在 hello**專案 Facet**畫面上，選取**動態 Web 模組**和**Java**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="99a5e-241">在 hello**伺服器**底部 hello 囉 」 畫面索引標籤上，以滑鼠右鍵按一下**Tomcat v7.0 伺服器在 localhost** ，然後按一下**加入和移除**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="99a5e-242">在 hello**加入和移除**視窗中，移動**azure documentdb 的 java 範例**toohello**設定**方塊，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="99a5e-243">在 hello**伺服器**索引標籤上，以滑鼠右鍵按一下**Tomcat v7.0 伺服器在 localhost**，然後按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="99a5e-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="99a5e-244">在瀏覽器中，瀏覽 toohttp://localhost:8080 / azure documentdb 的 java 範例 / 然後開始將加入 tooyour 工作清單。</span><span class="sxs-lookup"><span data-stu-id="99a5e-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="99a5e-245">請注意，如果您變更預設的連接埠值變更所選 8080 toohello 值。</span><span class="sxs-lookup"><span data-stu-id="99a5e-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="99a5e-246">toodeploy 您專案 tooan Azure 網站上，請參閱[步驟 6。部署您的應用程式 tooAzure 網站](#Deploy)。</span><span class="sxs-lookup"><span data-stu-id="99a5e-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
