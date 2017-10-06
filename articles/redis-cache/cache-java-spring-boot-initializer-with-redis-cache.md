---
title: "aaaHow tooconfigure Spring 開機初始設定式應用程式 toouse Redis 快取"
description: "了解如何 tooconfigure Spring 開機應用程式建立 hello Spring Initializr toouse Azure Redis 快取。"
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "Spring, Spring Boot Starter, Redis 快取"
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>如何 tooconfigure Spring 開機初始設定式應用程式 toouse Redis 快取

## <a name="overview"></a>概觀

hello  **[Spring 架構]**是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。 Hello 更常用專案為基礎所建立的其中一個在該平台是[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。 toohelp 開發人員快速入門 Spring 開機，可在數個範例 Spring 開機封裝<https://github.com/spring-guides/>。 除了從基本 Spring 開機 hello 清單 toochoosing 專案、 hello  **[Spring Initializr]** 可協助開發人員快速入門建立自訂 Spring 開機應用程式。

本文將指導您完成建立 Redis 快取使用 hello Azure 入口網站，然後使用 hello **Spring Initializr** toocreate 自訂應用程式，並再建立 Java web 應用程式儲存和擷取資料使用程式Redis 快取。

## <a name="prerequisites"></a>必要條件

在本文中的順序 toofollow hello 步驟需要 hello 下列必要條件：

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。

* [Java 開發套件 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) \(英文\) 1.7 版或更新版本。

* [Apache Maven](http://maven.apache.org/) \(英文\) 3.0 版或更新版本。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上建立 Redis 快取

1. 瀏覽 toohello Azure 入口網站在<https://portal.azure.com/>按一下 hello 項目，如**+ 新增**。

   ![Azure 入口網站][AZ01]

1. 按一下 資料庫，然後按一下Redis 快取。

   ![Azure 入口網站][AZ02]

1. 在 hello**新增 Redis 快取**頁面上，輸入 hello **DNS 名稱**快取，然後指定您**訂用帳戶**，**資源群組**， **位置**，和**定價層**。 當您指定這些選項時，按一下 **建立**toocreate 您的快取。

   ![Azure 入口網站][AZ03]

1. 完成您的快取之後，您會看到它列在您的 Azure**儀表板**，以及在 hello 下**所有資源**，和**Redis 快取**頁面。 您可以按一下您在任何這些位置 tooopen hello 屬性 頁面上的快取的快取。

   ![Azure 入口網站][AZ04]

1. Hello 頁面，其中包含您的快取的內容 hello 清單出現時，按一下 **存取金鑰**和複製您的快取的存取金鑰。

   ![Azure 入口網站][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>建立自訂應用程式使用 hello Spring Initializr

1. 瀏覽過<https://start.spring.io/>。

1. 指定您想要 toogenerate **Maven**專案與**Java**，輸入 hello**群組**和**Aritifact**應用程式的名稱然後按一下hello 連結太**交換器 toohello 完整版**hello Spring Initializr。

   ![Spring Initializr 的基本選項][SI01]

   > [!NOTE]
   >
   > hello Spring Initializr 將使用 hello**群組**和**Aritifact**名稱 toocreate hello 套件名稱; 例如： *com.contoso.myazuredemo*。
   >

1. 捲動 toohello **Web**區段，並檢查 hello 方塊**Web**，然後捲動 toohello **NoSQL**區段，並檢查 hello 方塊**Redis**，然後捲動 toohello hello 頁面的底部，並按一下 hello 按鈕太**產生專案**。

   ![Spring Initializr 的完整選項][SI02]

1. 出現提示時，下載您的本機電腦上的 hello 專案 tooa 路徑。

   ![下載自訂的 Spring Boot 專案][SI03]

1. 您已經擷取您的本機系統上的 hello 檔案之後，自訂 Spring 開機應用程式就可以進行編輯。

   ![自訂的 Spring Boot 專案檔][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>設定自訂的 Spring 開機 toouse Redis 快取

1. 找出 hello *application.properties*檔案在 hello*資源*目錄的應用程式，或建立 hello 檔案，如果不存在。

   ![找出 hello application.properties 檔案][RE01]

1. 開啟 hello *application.properties*檔案在文字編輯器中，加入下列行 toohello 檔，hello 和 hello 範例值取代為 hello 適當的屬性，從您的快取：

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![編輯 hello application.properties 檔案][RE02]

1. 儲存並關閉 hello *application.properties*檔案。

1. 建立名為的資料夾*控制器*hello 來源 資料夾底下為您的封裝; 例如：

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -或-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. 建立新的檔案命名為*HelloController.java*在 hello*控制器*資料夾。 在文字編輯器中開啟 hello 檔案，並加入下列程式碼 tooit hello:

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   您將在其中需要 tooreplace `com.contoso.myazuredemo` hello 封裝名稱，為您的專案。

1. 儲存並關閉 hello *HelloController.java*檔案。

1. 使用 Maven 建置 Spring Boot 應用程式並加以執行；例如：

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. 藉由瀏覽 toohttp://localhost:8080 使用網頁瀏覽器，測試 hello web 應用程式或使用類似下列範例，如果您有可用的 curl hello hello 語法：

   ```shell
   curl http://localhost:8080
   ```

   您應該會看見 hello"Hello World ！" 訊息，系統將會從您的 Redis 快取動態擷取此訊息。

## <a name="next-steps"></a>後續步驟

如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:

* [部署 Spring 開機應用程式 toohello Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Spring 開機應用程式在叢集上執行 Kubernetes hello Azure 容器服務中](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

如需取得詳細資訊與 Java 在 Azure 上，使用 Redis 快取啟動，請參閱[如何 toouse Azure Redis 快取 java][Redis Cache with Java]。

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring 架構]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
