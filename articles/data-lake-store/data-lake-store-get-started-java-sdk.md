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
# <a name="get-started-with-azure-data-lake-store-using-java"></a>使用 Java 開始使用 Azure Data Lake Store
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

了解如何 toouse hello Azure 資料湖存放區 Java SDK tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔案，依此類推。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。

您可以存取在 Azure Data Lake Store 的 hello Java SDK API 文件[Azure 資料湖存放區 Java 應用程式開發介面文件](https://azure.github.io/azure-data-lake-store-java/javadoc/)。

## <a name="prerequisites"></a>必要條件
* Java Development Kit (JDK 7 或更新版本，使用 Java 1.7 版或更新版本)
* Azure Data Lake Store 帳戶。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。
* [Maven](https://maven.apache.org/install.html). 本教學課程使用 Maven 來處理組建和專案相依性。 雖然可能 toobuild 而不需要使用像是 Maven 或 Gradle 建置系統，這些系統確定可更容易 toomanage 相依性。
* (選擇性) [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) 或 [Eclipse](https://www.eclipse.org/downloads/) 之類的 IDE。

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>如何使用 Azure Active Directory 驗證？
在本教學課程中，我們使用 Azure AD 應用程式用戶端秘密 tooretrieve 的 Azure Active Directory 權杖 （服務對服務驗證）。 我們會使用這個語彙基元 toocreate Data Lake Store 用戶端物件 tooperform 操作檔案和目錄作業。 如需有關如何使用 Azure Data Lake Store tooauthenticate hello 用戶端密碼的指示，我們要執行 hello 下列高階步驟：

1. 建立 Azure AD Web 應用程式
2. 擷取 hello 用戶端識別碼、 用戶端密碼和 hello Azure AD web 應用程式的權杖端點。
3. Hello Data Lake Store 檔案/資料夾，以便您想要從 Java 應用程式，您要建立 hello tooaccess 上設定 hello Azure AD web 應用程式的存取。

如需有關如何 tooperform 這些步驟，請參閱指示[建立 Active Directory 應用程式](data-lake-store-authenticate-using-active-directory.md)。

Azure Active Directory 提供的其他選項也 tooretrieve 語彙基元。 您可以選擇來自數個不同的驗證機制 toosuit 案例中，例如，在瀏覽器、 桌面應用程式，以發佈應用程式或伺服器應用程式在內部部署或 Azure 虛擬中執行的應用程式機器。 您也可以從不同類型的認證進行挑選，例如密碼、憑證、雙因子驗證等。此外，Azure Active Directory 可讓您 toosynchronize hello 雲端與內部部署 Active Directory 使用者。 如需詳細資訊，請參閱 [Azure Active Directory 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)。 

## <a name="create-a-java-application"></a>建立 Java 應用程式
hello 程式碼範例可用[GitHub 上](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/)逐步解說的 hello 存放區中建立檔案、 串連檔案、 下載檔案，並刪除一些檔案 hello 存放區中的 hello 程序。 Hello 文件的本節逐步引導您 hello hello 程式碼的主要部分。

1. 建立 Maven 專案使用[mvn 原型](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)從 hello 命令列或使用的 IDE。 如需如何 toocreate Java 專案使用 IntelliJ 指示，請參閱[這裡](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html)。 如需有關指示 toocreate 專案使用 Eclipse 中，請參閱[這裡](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm)。 
2. 新增下列相依性 tooyour Maven hello **pom.xml**檔案。 新增下列程式碼片段的文字之間 hello hello  **\</version >**標記和 hello  **\</專案 >**標記：
   
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
   
    hello 第一個相依性為 toouse hello 資料湖存放區 SDK (`azure-data-lake-store-sdk`) 從 hello maven 儲存機制。 hello 第二個相依性 (`slf4j-nop`) 是此應用程式的記錄架構 toouse toospecify。 hello 資料湖存放區 SDK 會使用[slf4j](http://www.slf4j.org/)記錄門面，可讓您選擇來自數個常用的記錄架構，log4j，像 Java 記錄、 等 logback，或任何記錄。 對於此範例中，我們將會停用記錄，因此我們使用 hello **slf4j nop**繫結。 toouse 其他應用程式中的記錄選項，請參閱[這裡](http://www.slf4j.org/manual.html#projectDep)。

### <a name="add-hello-application-code"></a>加入 hello 應用程式程式碼
有三個主要部分 toohello 程式碼。

1. 取得 hello Azure Active Directory 權杖
2. 使用 hello 語彙基元 toocreate Data Lake Store 用戶端。
3. 使用 hello Data Lake Store 用戶端 tooperform 作業。

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>步驟 1︰取得 Azure Active Directory 權杖。
hello 資料湖存放區 SDK 提供方便的方法可讓您管理 hello 安全性權杖所需 tootalk toohello Data Lake Store 帳戶。 不過，hello SDK 不會要求使用只有這些方法。 您可以使用任何其他方法來取得 token，像是使用 hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java)，或您自己的自訂程式碼。

toouse hello hello 您稍早建立的 Active Directory Web 應用程式的資料湖存放區 SDK tooobtain 語彙基元使用其中一種的 hello 子類別`AccessTokenProvider`(hello 下例使用`ClientCredsTokenProvider`)。 hello 權杖提供者快取 hello 認證在記憶體中，使用 tooobtain hello 語彙基元，並自動更新 hello 權杖，如果它是關於 tooexpire。 它是您自己的子類別可能 toocreate`AccessTokenProvider`因此語彙基元所取得您的客戶程式碼，但現在讓我們使用 hello 只提供一個 hello SDK 中。

取代**填滿的這裡**hello hello Azure Active Directory Web 應用程式的實際值。

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>步驟 2︰建立 Azure Data Lake Store 用戶端 (ADLStoreClient) 物件
建立[ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/)物件會要求您 toospecify hello Data Lake Store 帳戶名稱和 hello 權杖提供者 hello 最後一個步驟中產生。 請注意該 hello Data Lake Store 帳戶名稱必須 toobe 完整的網域名稱。 例如，以 **mydatalakestore.azuredatalakestore.net** 之類的資料取代 **FILL-IN-HERE**。

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>步驟 3： 使用 hello ADLStoreClient tooperform 檔案和目錄作業
hello 的下列程式碼包含範例程式碼片段的一些常見的作業。 您可以查看完整的 hello[資料湖存放區 Java SDK API 文件](https://azure.github.io/azure-data-lake-store-java/javadoc/)的 hello **ADLStoreClient**物件 toosee 其他作業。

請注意，檔案是使用標準 Java 串流進行讀取和寫入。 這表示可以分層任何 hello Java 資料流之上 hello Data Lake Store 串流 toobenefit 從標準的 Java 功能 （例如，列印資料流格式化的輸出，或任何 hello 壓縮或加密資料流上的其他功能top，等）。

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

#### <a name="step-4-build-and-run-hello-application"></a>步驟 4： 建置並執行 hello 應用程式
1. toorun 從 ide 中，找出並按下 hello**執行** 按鈕。 從 Maven，使用 toorun [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html)。
2. 您可以從執行命令列建置 hello jar 在內的所有相依性與使用 hello 的獨立 jar tooproduce [Maven 組件外掛程式](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html)。 hello pom.xml 在 hello [github 上的範例原始程式碼](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml)如何範例 toodo 這。

## <a name="next-steps"></a>後續步驟
* [探索 JavaDoc hello Java SDK](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)

