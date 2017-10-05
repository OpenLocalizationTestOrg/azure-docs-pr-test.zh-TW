---
title: "如何將 Spring Boot Initializer 應用程式設定為使用 Redis 快取"
description: "了解如何將使用 Spring Initializr 所建立的 Spring Boot 應用程式設定為使用 Azure Redis 快取。"
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
ms.openlocfilehash: fb3fc96a2136b7c326bb0eb291b7204e7acf0190
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a>如何將 Spring Boot Initializer 應用程式設定為使用 Redis 快取

## <a name="overview"></a>概觀

**[Spring Framework]** 是開放原始碼解決方案，可協助 Java 開發人員建立企業級應用程式。 建立在該平台之基礎上的其中一個更熱門的專案是 [Spring Boot]，其中會提供用來建立獨立 Java 應用程式的簡化方法。 為了協助開發人員開始使用 Spring Boot，<https://github.com/spring-guides/> 上提供了數個範例 Spring Boot 套件。 除了從基本的 Spring Boot 專案清單中進行選擇，**[Spring Initializr]** 還能協助開發人員開始建立自訂的 Spring Boot 應用程式。

本文會逐步引導您使用 Azure 入口網站來建立 Redis 快取，然後使用 **Spring Initializr** 來建立自訂應用程式，接著再建立 Java Web 應用程式以使用 Redis 快取來儲存和擷取資料。

## <a name="prerequisites"></a>必要條件

若要遵循本文中的步驟，需要具備下列必要條件：

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。

* [Java 開發套件 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) \(英文\) 1.7 版或更新版本。

* [Apache Maven](http://maven.apache.org/) \(英文\) 3.0 版或更新版本。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上建立 Redis 快取

1. 瀏覽至 <https://portal.azure.com/> 上的 Azure 入口網站，然後按一下要 [+新增] 的項目。

   ![Azure 入口網站][AZ01]

1. 按一下 [資料庫]，然後按一下 [Redis 快取]。

   ![Azure 入口網站][AZ02]

1. 在 [新增 Redis 快取] 頁面上，輸入快取的 [DNS 名稱]，然後指定 [訂用帳戶]、[資源群組]、[位置]和 [定價層]。 當您指定這些選項之後，按一下 [建立] 以建立您的快取。

   ![Azure 入口網站][AZ03]

1. 在您的快取完成之後，您會看到它列在您的 Azure [儀表板] 上，以及 [所有資源] 和 [Redis 快取] 頁面下。 您可以按一下這些任何位置上的快取，來開啟快取的屬性頁面。

   ![Azure 入口網站][AZ04]

1. 當快取的屬性清單所在的頁面顯示出來時，按一下 [存取金鑰] 並複製快取的存取金鑰。

   ![Azure 入口網站][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a>使用 Spring Initializr 建立自訂應用程式

1. 瀏覽至 <https://start.spring.io/>。

1. 指定您想要使用 [Java] 產生 [Maven 專案]、輸入應用程式的 [群組] 和 [成品] 名稱，然後按一下 Spring Initializr 的 [切換至完整版本] 連結。

   ![Spring Initializr 的基本選項][SI01]

   > [!NOTE]
   >
   > Spring Initializr 會使用 [群組] 和 [成品] 名稱來建立套件名稱；例如：com.contoso.myazuredemo。
   >

1. 向下捲動至 [Web] 區段，並核取 [Web] 方塊，然後向下捲動至 [NoSQL] 區段，並核取 [Redis] 方塊，然後捲動至頁面底部，並按一下按鈕以 [產生專案]。

   ![Spring Initializr 的完整選項][SI02]

1. 出現提示時，將專案下載至本機電腦上的路徑。

   ![下載自訂的 Spring Boot 專案][SI03]

1. 當您在本機系統上擷取檔案之後，就可以開始編輯自訂的 Spring Boot 應用程式。

   ![自訂的 Spring Boot 專案檔][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a>將自訂 Spring Boot 設定為使用 Redis 快取

1. 在應用程式的 [資源] 目錄中尋找 application.properties 檔案，如果該檔案不存在，則加以建立。

   ![尋找 application.properties 檔案][RE01]

1. 在文字編輯器中開啟 *application.properties* 檔案、將下列數行新增至檔案中，然後使用快取中的適當屬性來取代範例值：

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6380

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![編輯 application.properties 檔案][RE02]

1. 儲存並關閉 *application.properties* 檔案。

1. 在套件的來源資料夾下建立名為 controller 的資料夾，例如：

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -或-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. 在 *controller* 資料夾中建立名稱為 *HelloController.java* 的新檔案。 在文字編輯器中開啟檔案，並加入下列程式碼：

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve the DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve the port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve the access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object to connect to your Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object to store/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string to your cache.
         jedis.set("greeting", "Hello World!");

         // Return the string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   其中，您必須使用專案的套件名稱來取代 `com.contoso.myazuredemo`。

1. 儲存並關閉 HelloController.java 檔案。

1. 使用 Maven 建置 Spring Boot 應用程式並加以執行；例如：

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. 使用網頁瀏覽器瀏覽至 http://localhost:8080 來測試 Web 應用程式；如果有可用的 curl，請使用類似下列範例的語法：

   ```shell
   curl http://localhost:8080
   ```

   您應該會從顯示的範例控制器中看到 "Hello World!" 訊息，系統將會從您的 Redis 快取動態擷取此訊息。

## <a name="next-steps"></a>後續步驟

如需在 Azure 上使用 Spring Boot 應用程式的詳細資訊，請參閱下列文章：

* [將 Spring Boot 應用程式部署到 Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [在 Azure Container Service 的 Kubernetes 叢集上執行 Spring Boot 應用程式](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。

如需有關在 Azure 上開始搭配使用 Redis 快取與 Java 的詳細資訊，請參閱[如何搭配使用 Azure Redis 快取與 Java][Redis Cache with Java]。

<!-- URL List -->

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
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
