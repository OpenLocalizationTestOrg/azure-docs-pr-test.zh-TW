---
title: "aaaDeploy Spring 開機應用程式 toohello Azure App Service |Microsoft 文件"
description: "本教學課程將引導開發人員透過 hello 步驟 toodeploy hello Spring 開機開始使用 web 應用程式 tooAzure 應用程式服務。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>部署 Spring 開機應用程式 toohello Azure App Service

hello  **[Spring 架構]**是開放原始碼解決方案，可協助 Java 開發人員建立企業級應用程式，且其中一個是建立在該平台之上的 hello 更常用專案[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。

本教學課程將逐步引導您透過建立 hello 範例 Spring 開機開始使用 web 應用程式，並將它部署到太[Azure App Service]。

### <a name="prerequisites"></a>必要條件

在訂單 toocomplete hello 步驟本教學課程中，您需要 toohave hello 下列：

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。
* 最新的 [Java 開發工具組 (JDK)]。
* Apache 的 [Maven] 建置工具 (第 3 版)。
* [Git] 用戶端。

## <a name="create-hello-spring-boot-getting-started-web-app"></a>建立 hello Spring 開機開始使用 web 應用程式

hello 下列步驟將引導您完成必要的 toocreate 簡單的 Spring 開機 web 應用程式並在本機測試 hello 步驟。

1. 開啟命令提示字元，並建立本機目錄 toohold，您的應用程式，以及變更 toothat 目錄;例如：
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 或 --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. 複製 hello [Spring 開機入門]範例專案到您剛建立; hello 目錄，例如：
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. 變更目錄已完成的 toohello 專案;例如：
   ```
   cd gs-spring-boot
   cd complete
   ```

1. 建置使用 Maven; hello JAR 檔案例如：
   ```
   mvn package
   ```

1. 一旦建立 hello web 應用程式之後，變更目錄 toohello JAR 檔案，然後啟動 hello web 應用程式。例如：
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. 藉由瀏覽 toohttp://localhost:8080 使用網頁瀏覽器，測試 hello web 應用程式或使用類似下列範例，如果您有可用的 curl hello hello 語法：
   ```
   curl http://localhost:8080
   ```

1. 您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**

   ![瀏覽範例應用程式][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>建立 Azure Web 應用程式以搭配 Java 使用

hello 下列步驟將逐步引導您完成 hello 步驟 toocreate Azure Web 應用程式、 設定所需的 hello 設定 Java，並設定 FTP 認證。

1. 瀏覽 toohello [Azure 入口網站]並登入。

1. 一旦您已經登入您的帳戶在 hello Azure 入口網站上，按一下 [hello] 功能表圖示**應用程式服務**:
   
   ![Azure 入口網站][AZ01]

1. 當 hello**應用程式服務**頁面隨即顯示，請按一下**+ 加**toocreate 新的應用程式服務。

   ![建立應用程式服務][AZ02]

1. 顯示 hello 清單中的 web 應用程式範本時，按一下 hello hello 連結基本的 Microsoft Web 應用程式。

   ![Web 應用程式範本][AZ03]

1. Hello hello Web 應用程式範本資訊] 頁面出現時，按一下 [**建立**。

   ![建立 Web 應用程式][AZ04]

1. 為您的 Web 應用程式提供唯一的名稱並指定任何其他設定，然後按一下 [建立]。

   ![建立 Web 應用程式設定][AZ05]

1. 一旦建立您的 web 應用程式之後，按一下 [hello] 功能表圖示**應用程式服務**，然後按一下您剛建立的 web 應用程式：

   ![列出 Web 應用程式][AZ06]

1. 顯示您的 web 應用程式時，請使用下列步驟的 hello 指定 hello Java 版本：

   a. 按一下 hello**應用程式設定**功能表項目。

   b. 選擇**Java 8** hello Java 版本。

   c. 選擇**Newest** hello 次要的 Java 版本。

   d. 選擇**最新的 Tomcat 8.5** hello web 容器。 （這個容器不實際上會使用;Azure 會使用從 Spring 開機應用程式的 hello 容器）。

   e. 按一下 [儲存] 。

   ![應用程式設定][AZ07]

1. 使用下列步驟的 hello 指定 FTP 的部署認證：

   a. 按一下 hello**部署認證**功能表項目。

   b. 指定您的使用者名稱和密碼。

   c. 按一下 [儲存] 。

   ![指定部署認證][AZ08]

1. 使用下列步驟的 hello 擷取您的 FTP 連線資訊：

   a. 按一下 hello**部署認證**功能表項目。

   b. 複製完整的 FTP 使用者名稱和 URL，並加以儲存供 hello 這個教學課程的下一節。

   ![FTP URL 和認證][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>部署您 Spring 開機 web 應用程式 tooAzure

hello 下列步驟將引導您完成 hello 步驟 toodeploy 您 Spring 開機 web 應用程式 tooAzure。

1. 開啟 Windows [記事本] 之類的文字編輯器，貼上 hello 文字之後在新的文件，然後將 hello 檔案儲存為*web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. 在您儲存 hello 後*web.config*檔案 tooyour 系統，tooyour web 應用程式，透過使用 hello URL、 使用者名稱和密碼從 hello 前面一節，本教學課程的 FTP 連接。 例如：
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. 變更 hello 遠端目錄 toohello 根資料夾的 web 應用程式 (這是在*/站台/wwwroot*)，然後複製從 Spring 開機應用程式的 hello JAR 檔案，並 hello *web.config*前面。 例如：
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. 部署您 JAR 之後和*web.config*檔案 tooyour web 應用程式，您需要 toorestart 使用 hello Azure 入口網站的 web 應用程式：

   ![][AZ10]

1. 藉由瀏覽 tooyour web 應用程式的 URL，使用網頁瀏覽器，測試 hello web 應用程式，或使用類似下列範例，如果您有可用的 curl hello hello 語法：
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. 您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**

   ![瀏覽範例應用程式][SB02]

## <a name="next-steps"></a>後續步驟

如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:

* [在 hello Azure 容器服務中部署 Linux 上 Spring 開機應用程式](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

如需使用 FTP depoying web 應用程式 tooAzure 的詳細資訊，請參閱[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure]。

如需 hello Spring 開機範例專案進一步詳細資訊，請參閱[Spring 開機入門]。

如需開始使用您自己 Spring 開機應用程式的說明，請參閱 hello **Spring Initializr** https://start.spring.io/ 在。

如需如何設定 Web 應用程式之其他設定的詳細資訊，請參閱[在 Azure App Service 中設定 Web 應用程式]。

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure 入口網站]: https://portal.azure.com/
[在 Azure App Service 中設定 Web 應用程式]: /azure/app-service-web/web-sites-configure
[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring 開機入門]: https://github.com/spring-guides/gs-spring-boot
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
