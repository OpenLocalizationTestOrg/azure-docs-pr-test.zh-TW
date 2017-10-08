---
title: "aaaUse hello Java SDK toodevelop 應用程式在 Azure Data Lake Store |Microsoft 文件"
description: "使用 Azure 資料湖存放區 Java SDK toocreate Data Lake Store 帳戶，並在 hello 資料湖存放區中執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="1deff-103">使用 Java 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1deff-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1deff-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="1deff-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1deff-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1deff-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1deff-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1deff-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1deff-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1deff-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1deff-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1deff-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1deff-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1deff-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1deff-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1deff-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1deff-111">Python</span><span class="sxs-lookup"><span data-stu-id="1deff-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="1deff-112">了解如何 toouse hello Azure 資料湖存放區 Java SDK tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔案，依此類推。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1deff-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="1deff-113">您可以存取在 Azure Data Lake Store 的 hello Java SDK API 文件[Azure 資料湖存放區 Java 應用程式開發介面文件](https://azure.github.io/azure-data-lake-store-java/javadoc/)。</span><span class="sxs-lookup"><span data-stu-id="1deff-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1deff-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="1deff-114">Prerequisites</span></span>
* <span data-ttu-id="1deff-115">Java Development Kit (JDK 7 或更新版本，使用 Java 1.7 版或更新版本)</span><span class="sxs-lookup"><span data-stu-id="1deff-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="1deff-116">Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1deff-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="1deff-117">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1deff-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="1deff-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="1deff-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="1deff-119">本教學課程使用 Maven 來處理組建和專案相依性。</span><span class="sxs-lookup"><span data-stu-id="1deff-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="1deff-120">雖然可能 toobuild 而不需要使用像是 Maven 或 Gradle 建置系統，這些系統確定可更容易 toomanage 相依性。</span><span class="sxs-lookup"><span data-stu-id="1deff-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="1deff-121">(選擇性) [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) 或 [Eclipse](https://www.eclipse.org/downloads/) 之類的 IDE。</span><span class="sxs-lookup"><span data-stu-id="1deff-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="1deff-122">如何使用 Azure Active Directory 驗證？</span><span class="sxs-lookup"><span data-stu-id="1deff-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="1deff-123">在本教學課程中，我們使用 Azure AD 應用程式用戶端秘密 tooretrieve 的 Azure Active Directory 權杖 （服務對服務驗證）。</span><span class="sxs-lookup"><span data-stu-id="1deff-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="1deff-124">我們會使用這個語彙基元 toocreate Data Lake Store 用戶端物件 tooperform 操作檔案和目錄作業。</span><span class="sxs-lookup"><span data-stu-id="1deff-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="1deff-125">如需有關如何使用 Azure Data Lake Store tooauthenticate hello 用戶端密碼的指示，我們要執行 hello 下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="1deff-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="1deff-126">建立 Azure AD Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1deff-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="1deff-127">擷取 hello 用戶端識別碼、 用戶端密碼和 hello Azure AD web 應用程式的權杖端點。</span><span class="sxs-lookup"><span data-stu-id="1deff-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="1deff-128">Hello Data Lake Store 檔案/資料夾，以便您想要從 Java 應用程式，您要建立 hello tooaccess 上設定 hello Azure AD web 應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="1deff-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="1deff-129">如需有關如何 tooperform 這些步驟，請參閱指示[建立 Active Directory 應用程式](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="1deff-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="1deff-130">Azure Active Directory 提供的其他選項也 tooretrieve 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="1deff-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="1deff-131">您可以選擇來自數個不同的驗證機制 toosuit 案例中，例如，在瀏覽器、 桌面應用程式，以發佈應用程式或伺服器應用程式在內部部署或 Azure 虛擬中執行的應用程式機器。</span><span class="sxs-lookup"><span data-stu-id="1deff-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="1deff-132">您也可以從不同類型的認證進行挑選，例如密碼、憑證、雙因子驗證等。此外，Azure Active Directory 可讓您 toosynchronize hello 雲端與內部部署 Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="1deff-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="1deff-133">如需詳細資訊，請參閱 [Azure Active Directory 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="1deff-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="1deff-134">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="1deff-134">Create a Java application</span></span>
<span data-ttu-id="1deff-135">hello 程式碼範例可用[GitHub 上](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/)逐步解說的 hello 存放區中建立檔案、 串連檔案、 下載檔案，並刪除一些檔案 hello 存放區中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="1deff-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="1deff-136">Hello 文件的本節逐步引導您 hello hello 程式碼的主要部分。</span><span class="sxs-lookup"><span data-stu-id="1deff-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="1deff-137">建立 Maven 專案使用[mvn 原型](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)從 hello 命令列或使用的 IDE。</span><span class="sxs-lookup"><span data-stu-id="1deff-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="1deff-138">如需如何 toocreate Java 專案使用 IntelliJ 指示，請參閱[這裡](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html)。</span><span class="sxs-lookup"><span data-stu-id="1deff-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="1deff-139">如需有關指示 toocreate 專案使用 Eclipse 中，請參閱[這裡](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm)。</span><span class="sxs-lookup"><span data-stu-id="1deff-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="1deff-140">新增下列相依性 tooyour Maven hello **pom.xml**檔案。</span><span class="sxs-lookup"><span data-stu-id="1deff-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="1deff-141">新增下列程式碼片段的文字之間 hello hello  **\</version >**標記和 hello  **\</專案 >**標記：</span><span class="sxs-lookup"><span data-stu-id="1deff-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="1deff-142">hello 第一個相依性為 toouse hello 資料湖存放區 SDK (`azure-data-lake-store-sdk`) 從 hello maven 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="1deff-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="1deff-143">hello 第二個相依性 (`slf4j-nop`) 是此應用程式的記錄架構 toouse toospecify。</span><span class="sxs-lookup"><span data-stu-id="1deff-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="1deff-144">hello 資料湖存放區 SDK 會使用[slf4j](http://www.slf4j.org/)記錄門面，可讓您選擇來自數個常用的記錄架構，log4j，像 Java 記錄、 等 logback，或任何記錄。</span><span class="sxs-lookup"><span data-stu-id="1deff-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="1deff-145">對於此範例中，我們將會停用記錄，因此我們使用 hello **slf4j nop**繫結。</span><span class="sxs-lookup"><span data-stu-id="1deff-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="1deff-146">toouse 其他應用程式中的記錄選項，請參閱[這裡](http://www.slf4j.org/manual.html#projectDep)。</span><span class="sxs-lookup"><span data-stu-id="1deff-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="1deff-147">加入 hello 應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="1deff-147">Add hello application code</span></span>
<span data-ttu-id="1deff-148">有三個主要部分 toohello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="1deff-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="1deff-149">取得 hello Azure Active Directory 權杖</span><span class="sxs-lookup"><span data-stu-id="1deff-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="1deff-150">使用 hello 語彙基元 toocreate Data Lake Store 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1deff-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="1deff-151">使用 hello Data Lake Store 用戶端 tooperform 作業。</span><span class="sxs-lookup"><span data-stu-id="1deff-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="1deff-152">步驟 1︰取得 Azure Active Directory 權杖。</span><span class="sxs-lookup"><span data-stu-id="1deff-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="1deff-153">hello 資料湖存放區 SDK 提供方便的方法可讓您管理 hello 安全性權杖所需 tootalk toohello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1deff-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="1deff-154">不過，hello SDK 不會要求使用只有這些方法。</span><span class="sxs-lookup"><span data-stu-id="1deff-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="1deff-155">您可以使用任何其他方法來取得 token，像是使用 hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java)，或您自己的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="1deff-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="1deff-156">toouse hello hello 您稍早建立的 Active Directory Web 應用程式的資料湖存放區 SDK tooobtain 語彙基元使用其中一種的 hello 子類別`AccessTokenProvider`(hello 下例使用`ClientCredsTokenProvider`)。</span><span class="sxs-lookup"><span data-stu-id="1deff-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="1deff-157">hello 權杖提供者快取 hello 認證在記憶體中，使用 tooobtain hello 語彙基元，並自動更新 hello 權杖，如果它是關於 tooexpire。</span><span class="sxs-lookup"><span data-stu-id="1deff-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="1deff-158">它是您自己的子類別可能 toocreate`AccessTokenProvider`因此語彙基元所取得您的客戶程式碼，但現在讓我們使用 hello 只提供一個 hello SDK 中。</span><span class="sxs-lookup"><span data-stu-id="1deff-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="1deff-159">取代**填滿的這裡**hello hello Azure Active Directory Web 應用程式的實際值。</span><span class="sxs-lookup"><span data-stu-id="1deff-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="1deff-160">步驟 2︰建立 Azure Data Lake Store 用戶端 (ADLStoreClient) 物件</span><span class="sxs-lookup"><span data-stu-id="1deff-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="1deff-161">建立[ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/)物件會要求您 toospecify hello Data Lake Store 帳戶名稱和 hello 權杖提供者 hello 最後一個步驟中產生。</span><span class="sxs-lookup"><span data-stu-id="1deff-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="1deff-162">請注意該 hello Data Lake Store 帳戶名稱必須 toobe 完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1deff-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="1deff-163">例如，以 **mydatalakestore.azuredatalakestore.net** 之類的資料取代 **FILL-IN-HERE**。</span><span class="sxs-lookup"><span data-stu-id="1deff-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="1deff-164">步驟 3： 使用 hello ADLStoreClient tooperform 檔案和目錄作業</span><span class="sxs-lookup"><span data-stu-id="1deff-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="1deff-165">hello 的下列程式碼包含範例程式碼片段的一些常見的作業。</span><span class="sxs-lookup"><span data-stu-id="1deff-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="1deff-166">您可以查看完整的 hello[資料湖存放區 Java SDK API 文件](https://azure.github.io/azure-data-lake-store-java/javadoc/)的 hello **ADLStoreClient**物件 toosee 其他作業。</span><span class="sxs-lookup"><span data-stu-id="1deff-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="1deff-167">請注意，檔案是使用標準 Java 串流進行讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="1deff-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="1deff-168">這表示可以分層任何 hello Java 資料流之上 hello Data Lake Store 串流 toobenefit 從標準的 Java 功能 （例如，列印資料流格式化的輸出，或任何 hello 壓縮或加密資料流上的其他功能top，等）。</span><span class="sxs-lookup"><span data-stu-id="1deff-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="1deff-169">步驟 4： 建置並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="1deff-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="1deff-170">toorun 從 ide 中，找出並按下 hello**執行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1deff-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="1deff-171">從 Maven，使用 toorun [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html)。</span><span class="sxs-lookup"><span data-stu-id="1deff-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="1deff-172">您可以從執行命令列建置 hello jar 在內的所有相依性與使用 hello 的獨立 jar tooproduce [Maven 組件外掛程式](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html)。</span><span class="sxs-lookup"><span data-stu-id="1deff-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="1deff-173">hello pom.xml 在 hello [github 上的範例原始程式碼](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml)如何範例 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="1deff-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1deff-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1deff-174">Next steps</span></span>
* [<span data-ttu-id="1deff-175">探索 JavaDoc hello Java SDK</span><span class="sxs-lookup"><span data-stu-id="1deff-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="1deff-176">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="1deff-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1deff-177">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1deff-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1deff-178">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1deff-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

