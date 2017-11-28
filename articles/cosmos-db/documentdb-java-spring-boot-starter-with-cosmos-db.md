---
title: "aaaHow toouse hello Azure Cosmos DB DocumentDB API 與 Spring 開機入門"
description: "了解如何 tooconfigure 建立的應用程式以 hello Azure Cosmos DB DocumentDB API hello Spring 開機初始設定式。"
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="557b6-104">如何 toouse hello Azure Cosmos DB DocumentDB API 與 Spring 開機入門</span><span class="sxs-lookup"><span data-stu-id="557b6-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="557b6-105">概觀</span><span class="sxs-lookup"><span data-stu-id="557b6-105">Overview</span></span>

<span data-ttu-id="557b6-106">hello  **[Spring 架構]**是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="557b6-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="557b6-107">其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="557b6-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="557b6-108">toohelp 開發人員快速入門 Spring 開機，可在數個範例 Spring 開機封裝<https://github.com/spring-guides/>。</span><span class="sxs-lookup"><span data-stu-id="557b6-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="557b6-109">除了從基本 Spring 開機 hello 清單 toochoosing 專案、 hello  **[Spring Initializr]** 可協助開發人員快速入門建立自訂 Spring 開機應用程式。</span><span class="sxs-lookup"><span data-stu-id="557b6-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="557b6-110">Azure Cosmos DB 是一種全域分散式資料庫服務，可讓開發人員 toowork 與使用各種不同的標準 Api，像是 DocumentDB、 MongoDB、 圖表和資料表 Api 的資料。</span><span class="sxs-lookup"><span data-stu-id="557b6-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="557b6-111">Microsoft 的 Spring 開機入門可讓開發人員 toouse Spring 開機整合的應用程式輕鬆地以 Azure Cosmos DB 使用 DocumentDB Api。</span><span class="sxs-lookup"><span data-stu-id="557b6-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="557b6-112">這篇文章將示範如何建立使用 hello Azure 入口網站，然後使用 hello Azure Cosmos DB **Spring Initializr** toocreate 自訂 java 應用程式，然後再加入 hello Spring 開機入門功能 tooyour 自訂中的應用程式 toostore 資料並從使用 hello DocumentDB API 您 Azure Cosmos DB 擷取資料。</span><span class="sxs-lookup"><span data-stu-id="557b6-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="557b6-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="557b6-113">Prerequisites</span></span>

<span data-ttu-id="557b6-114">在本文中的順序 toofollow hello 步驟需要 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="557b6-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="557b6-115">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="557b6-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="557b6-116">[Java 開發套件 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) \(英文\) 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="557b6-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="557b6-117">[Apache Maven](http://maven.apache.org/) \(英文\) 3.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="557b6-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="557b6-118">使用 hello Azure 入口網站建立 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="557b6-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="557b6-119">瀏覽 toohello Azure 入口網站在<https://portal.azure.com/>按一下**+ 新增**。</span><span class="sxs-lookup"><span data-stu-id="557b6-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure 入口網站][AZ01]

1. <span data-ttu-id="557b6-121">依序按一下 [資料庫] 和 [Azure Cosmos DB]。</span><span class="sxs-lookup"><span data-stu-id="557b6-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure 入口網站][AZ02]

1. <span data-ttu-id="557b6-123">在 hello **Azure Cosmos DB**頁面上，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="557b6-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="557b6-124">輸入唯一**識別碼**，您將會使用如 hello URI 為您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="557b6-125">例如：*wingtiptoysdata.documents.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="557b6-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="557b6-126">選擇**SQL (文件 DB)** hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="557b6-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="557b6-127">選擇 hello**訂用帳戶**想 toouse 為您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="557b6-128">指定是否新 toocreate**資源群組**為您的資料庫，或選擇現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="557b6-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="557b6-129">指定 hello**位置**為您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="557b6-130">當您指定這些選項時，按一下 **建立**toocreate 您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure 入口網站][AZ03]

1. <span data-ttu-id="557b6-132">您的資料庫建立後，它會列在您的 Azure**儀表板**，以及在 hello 下**所有資源**和**Azure Cosmos DB**頁面。</span><span class="sxs-lookup"><span data-stu-id="557b6-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="557b6-133">您可以按一下任何這些位置 tooopen hello 屬性 頁面上的資料庫快取。</span><span class="sxs-lookup"><span data-stu-id="557b6-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure 入口網站][AZ04]

1. <span data-ttu-id="557b6-135">顯示 hello 屬性頁面，為您的資料庫時，按一下**存取金鑰**複製您的 URI 和存取金鑰，為您的資料庫之後，您將 Spring 開機應用程式中使用這些值。</span><span class="sxs-lookup"><span data-stu-id="557b6-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure 入口網站][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="557b6-137">建立簡單的 Spring 開機應用程式以 hello Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="557b6-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="557b6-138">瀏覽過<https://start.spring.io/>。</span><span class="sxs-lookup"><span data-stu-id="557b6-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="557b6-139">指定您想要 toogenerate **Maven**專案與**Java**，輸入 hello**群組**和**成品**應用程式的名稱和然後按一下hello 按鈕太**產生專案**。</span><span class="sxs-lookup"><span data-stu-id="557b6-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Spring Initializr 的基本選項][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="557b6-141">hello Spring Initializr 使用 hello**群組**和**成品**名稱 toocreate hello 套件名稱; 例如： *com.example.wintiptoys*。</span><span class="sxs-lookup"><span data-stu-id="557b6-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="557b6-142">出現提示時，下載您的本機電腦上的 hello 專案 tooa 路徑。</span><span class="sxs-lookup"><span data-stu-id="557b6-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![下載自訂的 Spring Boot 專案][SI02]

1. <span data-ttu-id="557b6-144">您已經擷取您的本機系統上的 hello 檔案之後，您簡單 Spring 開機應用程式就可以進行編輯。</span><span class="sxs-lookup"><span data-stu-id="557b6-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![自訂的 Spring Boot 專案檔][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="557b6-146">設定您 Spring 開機應用程式 toouse hello Azure Spring 開機入門</span><span class="sxs-lookup"><span data-stu-id="557b6-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="557b6-147">找出 hello *pom.xml*檔案 hello 目錄中的應用程式; 例如：</span><span class="sxs-lookup"><span data-stu-id="557b6-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="557b6-148">-或-</span><span class="sxs-lookup"><span data-stu-id="557b6-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![找出 hello pom.xml 檔案][PM01]

1. <span data-ttu-id="557b6-150">開啟 hello *pom.xml*檔在文字編輯器中，並加入下列的行 toolist hello `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="557b6-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![編輯 hello pom.xml 檔案][PM02]

1. <span data-ttu-id="557b6-152">儲存並關閉 hello *pom.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="557b6-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="557b6-153">設定您 Spring 開機應用程式 toouse Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="557b6-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="557b6-154">找出 hello *application.properties*檔案在 hello*資源*目錄的應用程式; 例如：</span><span class="sxs-lookup"><span data-stu-id="557b6-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="557b6-155">-或-</span><span class="sxs-lookup"><span data-stu-id="557b6-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![找出 hello application.properties 檔案][RE01]

1. <span data-ttu-id="557b6-157">開啟 hello *application.properties*檔案在文字編輯器中，加入下列行 toohello 檔，hello 和 hello 範例值取代為您資料庫的 hello 適當屬性：</span><span class="sxs-lookup"><span data-stu-id="557b6-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![編輯 hello application.properties 檔案][RE02]

1. <span data-ttu-id="557b6-159">儲存並關閉 hello *application.properties*檔案。</span><span class="sxs-lookup"><span data-stu-id="557b6-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="557b6-160">新增範例程式碼 tooimplement 基本資料庫功能</span><span class="sxs-lookup"><span data-stu-id="557b6-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="557b6-161">在本節中，您建立兩個 Java 類別來儲存使用者資料，然後修改您的主應用程式類別 toocreate hello 使用者類別的執行個體，並將它儲存 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="557b6-162">定義用來儲存使用者資料的基本類別</span><span class="sxs-lookup"><span data-stu-id="557b6-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="557b6-163">建立新的檔案命名為*User.java*在 hello 與主應用程式的 Java 檔相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="557b6-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="557b6-164">開啟 hello *User.java*檔在文字編輯器中，並加入 hello 下列各行 toohello 檔案 toodefine 一般的使用者類別儲存和擷取您的資料庫中的值：</span><span class="sxs-lookup"><span data-stu-id="557b6-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="557b6-165">儲存並關閉 hello *User.java*檔案。</span><span class="sxs-lookup"><span data-stu-id="557b6-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="557b6-166">定義資料存放庫介面</span><span class="sxs-lookup"><span data-stu-id="557b6-166">Define a data repository interface</span></span>

1. <span data-ttu-id="557b6-167">建立新的檔案命名為*UserRepository.java*在 hello 與主應用程式的 Java 檔相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="557b6-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="557b6-168">開啟 hello *UserRepository.java*檔在文字編輯器中，並加入 hello 下列各行 toohello 檔案 toodefine 延伸 hello 預設 DocumentDB 儲存機制介面的使用者儲存機制介面：</span><span class="sxs-lookup"><span data-stu-id="557b6-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="557b6-169">儲存並關閉 hello *UserRepository.java*檔案。</span><span class="sxs-lookup"><span data-stu-id="557b6-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="557b6-170">修改 hello 主應用程式類別</span><span class="sxs-lookup"><span data-stu-id="557b6-170">Modify hello main application class</span></span>

1. <span data-ttu-id="557b6-171">您的應用程式; hello 封裝目錄中，找出 hello 主應用程式 Java 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="557b6-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="557b6-172">-或-</span><span class="sxs-lookup"><span data-stu-id="557b6-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![找出 hello 應用程式的 Java 檔案][JV01]

1. <span data-ttu-id="557b6-174">在文字編輯器中，開啟 hello 主應用程式的 Java 檔案並加入下列行 toohello 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="557b6-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="557b6-175">儲存並關閉 hello 主應用程式的 Java 檔案。</span><span class="sxs-lookup"><span data-stu-id="557b6-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="557b6-176">建置及測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="557b6-176">Build and test your app</span></span>

1. <span data-ttu-id="557b6-177">開啟命令提示字元並變更目錄 toohello 資料夾其中您*pom.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="557b6-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="557b6-178">-或-</span><span class="sxs-lookup"><span data-stu-id="557b6-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="557b6-179">使用 Maven 建置 Spring Boot 應用程式並加以執行；例如：</span><span class="sxs-lookup"><span data-stu-id="557b6-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="557b6-180">您的應用程式將會顯示數個執行階段訊息，以及您應該會看到 hello 訊息`User: testFirstName testLastName`顯示 tooindicate 值已成功儲存並擷取從您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="557b6-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Hello 應用程式的成功輸出][JV02]

1. <span data-ttu-id="557b6-182">選用： 您可以使用 Azure Cosmos hello 屬性頁面從 DB hello Azure 入口網站 tooview hello 內容資料庫即可**Document Explorer**，然後選取並顯示 hello 清單 tooview hello 項目內容。</span><span class="sxs-lookup"><span data-stu-id="557b6-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![使用 hello Document Explorer tooview 您的資料][JV03]

## <a name="next-steps"></a><span data-ttu-id="557b6-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="557b6-184">Next steps</span></span>

<span data-ttu-id="557b6-185">如需使用 Azure Cosmos DB 和 Java 的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="557b6-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="557b6-186">[Azure Cosmos DB 文件]。</span><span class="sxs-lookup"><span data-stu-id="557b6-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="557b6-187">[Azure Cosmos DB： 建置 DocumentDB API 應用程式使用 Java 和 hello Azure 入口網站][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="557b6-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="557b6-188">如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="557b6-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="557b6-189">適用於 Azure 的 Spring Boot DocumenDB Starter</span><span class="sxs-lookup"><span data-stu-id="557b6-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="557b6-190">部署 Spring 開機應用程式 toohello Azure App Service</span><span class="sxs-lookup"><span data-stu-id="557b6-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="557b6-191">Spring 開機應用程式在叢集上執行 Kubernetes hello Azure 容器服務中</span><span class="sxs-lookup"><span data-stu-id="557b6-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="557b6-192">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="557b6-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Cosmos DB 文件]: /azure/cosmos-db/
[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
