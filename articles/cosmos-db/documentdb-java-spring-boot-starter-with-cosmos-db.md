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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>如何 toouse hello Azure Cosmos DB DocumentDB API 與 Spring 開機入門

## <a name="overview"></a>概觀

hello  **[Spring 架構]**是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。 其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。 toohelp 開發人員快速入門 Spring 開機，可在數個範例 Spring 開機封裝<https://github.com/spring-guides/>。 除了從基本 Spring 開機 hello 清單 toochoosing 專案、 hello  **[Spring Initializr]** 可協助開發人員快速入門建立自訂 Spring 開機應用程式。

Azure Cosmos DB 是一種全域分散式資料庫服務，可讓開發人員 toowork 與使用各種不同的標準 Api，像是 DocumentDB、 MongoDB、 圖表和資料表 Api 的資料。 Microsoft 的 Spring 開機入門可讓開發人員 toouse Spring 開機整合的應用程式輕鬆地以 Azure Cosmos DB 使用 DocumentDB Api。

這篇文章將示範如何建立使用 hello Azure 入口網站，然後使用 hello Azure Cosmos DB **Spring Initializr** toocreate 自訂 java 應用程式，然後再加入 hello Spring 開機入門功能 tooyour 自訂中的應用程式 toostore 資料並從使用 hello DocumentDB API 您 Azure Cosmos DB 擷取資料。

## <a name="prerequisites"></a>必要條件

在本文中的順序 toofollow hello 步驟需要 hello 下列必要條件：

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。

* [Java 開發套件 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) \(英文\) 1.7 版或更新版本。

* [Apache Maven](http://maven.apache.org/) \(英文\) 3.0 版或更新版本。

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站建立 Azure Cosmos DB

1. 瀏覽 toohello Azure 入口網站在<https://portal.azure.com/>按一下**+ 新增**。

   ![Azure 入口網站][AZ01]

1. 依序按一下 [資料庫] 和 [Azure Cosmos DB]。

   ![Azure 入口網站][AZ02]

1. 在 hello **Azure Cosmos DB**頁面上，輸入下列資訊的 hello:

   * 輸入唯一**識別碼**，您將會使用如 hello URI 為您的資料庫。 例如：*wingtiptoysdata.documents.azure.com*。
   * 選擇**SQL (文件 DB)** hello 應用程式開發介面。
   * 選擇 hello**訂用帳戶**想 toouse 為您的資料庫。
   * 指定是否新 toocreate**資源群組**為您的資料庫，或選擇現有的資源群組。
   * 指定 hello**位置**為您的資料庫。
   
   當您指定這些選項時，按一下 **建立**toocreate 您的資料庫。

   ![Azure 入口網站][AZ03]

1. 您的資料庫建立後，它會列在您的 Azure**儀表板**，以及在 hello 下**所有資源**和**Azure Cosmos DB**頁面。 您可以按一下任何這些位置 tooopen hello 屬性 頁面上的資料庫快取。

   ![Azure 入口網站][AZ04]

1. 顯示 hello 屬性頁面，為您的資料庫時，按一下**存取金鑰**複製您的 URI 和存取金鑰，為您的資料庫之後，您將 Spring 開機應用程式中使用這些值。

   ![Azure 入口網站][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>建立簡單的 Spring 開機應用程式以 hello Spring Initializr

1. 瀏覽過<https://start.spring.io/>。

1. 指定您想要 toogenerate **Maven**專案與**Java**，輸入 hello**群組**和**成品**應用程式的名稱和然後按一下hello 按鈕太**產生專案**。

   ![Spring Initializr 的基本選項][SI01]

   > [!NOTE]
   >
   > hello Spring Initializr 使用 hello**群組**和**成品**名稱 toocreate hello 套件名稱; 例如： *com.example.wintiptoys*。
   >

1. 出現提示時，下載您的本機電腦上的 hello 專案 tooa 路徑。

   ![下載自訂的 Spring Boot 專案][SI02]

1. 您已經擷取您的本機系統上的 hello 檔案之後，您簡單 Spring 開機應用程式就可以進行編輯。

   ![自訂的 Spring Boot 專案檔][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>設定您 Spring 開機應用程式 toouse hello Azure Spring 開機入門

1. 找出 hello *pom.xml*檔案 hello 目錄中的應用程式; 例如：

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -或-

   `/users/example/home/wingtiptoys/pom.xml`

   ![找出 hello pom.xml 檔案][PM01]

1. 開啟 hello *pom.xml*檔在文字編輯器中，並加入下列的行 toolist hello `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![編輯 hello pom.xml 檔案][PM02]

1. 儲存並關閉 hello *pom.xml*檔案。

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>設定您 Spring 開機應用程式 toouse Azure Cosmos DB

1. 找出 hello *application.properties*檔案在 hello*資源*目錄的應用程式; 例如：

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -或-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![找出 hello application.properties 檔案][RE01]

1. 開啟 hello *application.properties*檔案在文字編輯器中，加入下列行 toohello 檔，hello 和 hello 範例值取代為您資料庫的 hello 適當屬性：

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![編輯 hello application.properties 檔案][RE02]

1. 儲存並關閉 hello *application.properties*檔案。

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>新增範例程式碼 tooimplement 基本資料庫功能

在本節中，您建立兩個 Java 類別來儲存使用者資料，然後修改您的主應用程式類別 toocreate hello 使用者類別的執行個體，並將它儲存 tooyour 資料庫。

### <a name="define-a-basic-class-for-storing-user-data"></a>定義用來儲存使用者資料的基本類別

1. 建立新的檔案命名為*User.java*在 hello 與主應用程式的 Java 檔相同的目錄。

1. 開啟 hello *User.java*檔在文字編輯器中，並加入 hello 下列各行 toohello 檔案 toodefine 一般的使用者類別儲存和擷取您的資料庫中的值：

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

1. 儲存並關閉 hello *User.java*檔案。

### <a name="define-a-data-repository-interface"></a>定義資料存放庫介面

1. 建立新的檔案命名為*UserRepository.java*在 hello 與主應用程式的 Java 檔相同的目錄。

1. 開啟 hello *UserRepository.java*檔在文字編輯器中，並加入 hello 下列各行 toohello 檔案 toodefine 延伸 hello 預設 DocumentDB 儲存機制介面的使用者儲存機制介面：

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. 儲存並關閉 hello *UserRepository.java*檔案。

### <a name="modify-hello-main-application-class"></a>修改 hello 主應用程式類別

1. 您的應用程式; hello 封裝目錄中，找出 hello 主應用程式 Java 檔案例如：

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -或-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![找出 hello 應用程式的 Java 檔案][JV01]

1. 在文字編輯器中，開啟 hello 主應用程式的 Java 檔案並加入下列行 toohello 檔 hello:

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

1. 儲存並關閉 hello 主應用程式的 Java 檔案。

## <a name="build-and-test-your-app"></a>建置及測試您的應用程式

1. 開啟命令提示字元並變更目錄 toohello 資料夾其中您*pom.xml*檔案; 例如：

   `cd C:\SpringBoot\wingtiptoys`

   -或-

   `cd /users/example/home/wingtiptoys`

1. 使用 Maven 建置 Spring Boot 應用程式並加以執行；例如：

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. 您的應用程式將會顯示數個執行階段訊息，以及您應該會看到 hello 訊息`User: testFirstName testLastName`顯示 tooindicate 值已成功儲存並擷取從您的資料庫。

   ![Hello 應用程式的成功輸出][JV02]

1. 選用： 您可以使用 Azure Cosmos hello 屬性頁面從 DB hello Azure 入口網站 tooview hello 內容資料庫即可**Document Explorer**，然後選取並顯示 hello 清單 tooview hello 項目內容。

   ![使用 hello Document Explorer tooview 您的資料][JV03]

## <a name="next-steps"></a>後續步驟

如需使用 Azure Cosmos DB 和 Java 的詳細資訊，請參閱下列文章 hello:

* [Azure Cosmos DB 文件]。

* [Azure Cosmos DB： 建置 DocumentDB API 應用程式使用 Java 和 hello Azure 入口網站][Build a DocumentDB API app with Java]

如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:

* [適用於 Azure 的 Spring Boot DocumenDB Starter](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [部署 Spring 開機應用程式 toohello Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Spring 開機應用程式在叢集上執行 Kubernetes hello Azure 容器服務中](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

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
