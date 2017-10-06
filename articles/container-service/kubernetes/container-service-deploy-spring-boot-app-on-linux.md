---
title: "aaaDeploy Spring 開機 Web 應用程式在 Azure 容器服務中的 Linux 上 |Microsoft 文件"
description: "本教學課程將引導您透過 hello 步驟 toodeploy Spring 開機應用程式為 Linux web 應用程式在 Microsoft Azure 上。"
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>部署在 Linux 上 hello Azure 容器服務中的 Spring 開機應用程式

hello  **[Spring 架構]**是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。 其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。

**[Docker]**  hello 部署、 調整及管理的應用程式容器中執行的是可協助開發人員的開放原始碼解決方案自動化。

本教學課程將引導您完成使用 Docker toodevelop 和 Spring 開機應用程式 tooa Linux 中部署主機 hello [Azure 容器服務 (ACS)]。

## <a name="prerequisites"></a>必要條件

在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。
* hello [Azure 命令列介面 (CLI)]。
* 最新的 [Java 開發工具組 (JDK)]。
* Apache 的 [Maven] 建置工具 (第 3 版)。
* [Git] 用戶端。
* [Docker] 用戶端。

> [!NOTE]
>
> Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Docker 快速入門的 web 應用程式上建立 hello Spring 開機

hello 下列步驟引導您完成必要的 toocreate 簡單的 Spring 開機 web 應用程式並在本機測試 hello 步驟。

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

1. 複製 hello[上開始使用 Docker Spring 開機]範例專案到 hello 目錄，您所建立的; 例如：
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 變更目錄已完成的 toohello 專案;例如：
   ```
   cd gs-spring-boot-docker/complete
   ```

1. 建置使用 Maven; hello JAR 檔案例如：
   ```
   mvn package
   ```

1. 一旦建立 hello web 應用程式之後，變更目錄 toohello`target`目錄 hello JAR 檔案所在的位置，並啟動 hello web 應用程式; 例如：
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. 藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。 例如，如果您有 curl 可用而且設定 hello Tomcat 伺服器 toorun 連接埠 80 上：
   ```
   curl http://localhost
   ```

1. 您應該會看到下列訊息顯示 hello: **Docker 您好 ！**

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>建立 Azure 容器登錄中 toouse 為私用 Docker 登錄

hello 下列步驟引導您完成使用 hello Azure 入口網站 toocreate Azure 容器登錄中。

> [!NOTE]
>
> 如果您想 toouse hello Azure CLI 而不是 hello Azure 入口網站，請依照下列中的 hello 步驟[建立私用 Docker 容器登錄中使用 Azure CLI 2.0 hello](../../container-registry/container-registry-get-started-azure-cli.md)。
>

1. 瀏覽 toohello [Azure 入口網站]並登入。

   一旦您已登入 tooyour hello Azure 入口網站上的帳戶，您可以依照 hello 中的 hello 步驟[建立私用 Docker 容器登錄中使用 Azure 入口網站 hello]發行項，這會在下列步驟 hello paraphrasedsake 直接。

1. 按一下功能表圖示 hello **+ 新增**，然後按一下**容器**，然後按一下 **Azure 容器登錄中**。
   
   ![建立新的 Azure Container Registry][AR01]

1. Hello hello Azure 容器登錄中的範本資訊] 頁面出現時，按一下 [**建立**。 

   ![建立新的 Azure Container Registry][AR02]

1. 當 hello**容器登錄中建立**會顯示頁面中，輸入您**登錄名稱**和**資源群組**，選擇**啟用**的hello **Admin 使用者**，然後按一下**建立**。

   ![設定 Azure Container Registry 設定][AR03]

1. 一旦建立容器登錄之後，瀏覽 tooyour 容器登錄中的 hello Azure 入口網站中，然後按一下**便捷鍵**。 記下 hello 使用者名稱和密碼的 hello 接下來的步驟。

   ![Azure Container Registry 存取金鑰][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>設定 Maven toouse Azure 容器登錄中存取金鑰

1. 瀏覽 toohello Maven 安裝的設定目錄，並開啟 hello *settings.xml*使用文字編輯器的檔案。

1. 從這個教學課程 toohello hello 上一節中加入您 Azure 容器登錄中的存取設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. 瀏覽 Spring 開機應用程式，完成 toohello 專案目錄 (例如:"*C:\SpringBoot\gs-spring-boot-docker\complete*「 或 」*/users/robert/SpringBoot/gs-spring-boot-docker /完成*")，並開啟 hello *pom.xml*使用文字編輯器的檔案。

1. 更新 hello`<properties>`中 hello 集合*pom.xml*檔案 hello 登入伺服器的值具有 Azure 容器登錄 hello 前一節，本教學課程; 例如：

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. 更新 hello`<plugins>`中 hello 集合*pom.xml*檔案，因此，hello`<plugin>`包含 hello 登入伺服器位址和登錄名稱 Azure 容器登錄從 hello 本教學課程的上一節。 例如：

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. 瀏覽 toohello 完成 Spring 開機應用程式的專案目錄並執行下列命令 toorebuild hello 應用程式的 hello 並推送 hello 容器 tooyour Azure 容器登錄中：

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> 當您要推入您的 Docker 容器 tooAzure 時，您可能會收到類似 tooone hello 遵循即使已成功建立您的 Docker 容器的錯誤訊息：
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 如果發生這種情況，您可能需要 toosign tooyour hello Docker 命令列工具，從 Azure 帳戶中例如：
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 您接著可以從 hello 命令列; 推送您的容器例如：
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>使用您的容器映像在 Azure App Service 上建立 Linux 的 Web 應用程式

1. 瀏覽 toohello [Azure 入口網站]並登入。

1. 按一下功能表圖示 hello **+ 新增**，然後按一下 **Web + 行動**，然後按一下 **Linux 上的 Web 應用程式**。
   
   ![在 hello Azure 入口網站中建立新的 web 應用程式][LX01]

1. 當 hello **Linux 上的 Web 應用程式**會顯示頁面中，輸入下列資訊的 hello:

   a. 輸入唯一的名稱，如 hello**應用程式名稱**; 例如:"*wingtiptoyslinux*。 」

   b. 選擇您**訂用帳戶**hello 下拉式清單中。

   c. 選擇現有**資源群組**，或指定名稱 toocreate 新的資源群組。

   d. 按一下**設定容器**並輸入下列資訊的 hello:

      * 選擇 [私人登錄]。

      * **映像和選擇性標記**：從先前指定的容器名稱，例如："wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest"

      * **伺服器 URL**：從先前指定的容器登錄 URL，例如："https://wingtiptoysregistry.azurecr.io"

      * **登入使用者名稱**和**密碼**：從您在先前步驟中使用的**存取金鑰**指定您的登入認證。
   
   e. 一旦您輸入所有 hello 上述資訊，請按一下**確定**。

   ![設定 Web 應用程式設定][LX02]

1. 按一下 [建立] 。

> [!NOTE]
>
> Azure 會自動對應網際網路要求 tooembedded Tomcat 伺服器 hello 標準連接埠 80 或 8080 上執行。 不過，如果您設定您的內嵌的 Tomcat 伺服器 toorun 自訂連接埠時，您會需要 tooadd 定義內嵌的 Tomcat 伺服器 hello 連接埠的環境變數 tooyour web 應用程式。 toodo 因此，使用下列步驟的 hello:
>
> 1. 瀏覽 toohello [Azure 入口網站]並登入。
> 
> 2. 按一下 hello 圖示**應用程式服務**。 （請參閱下面的 hello 影像中的項目 #1）。
>
> 3. Hello 清單中選取您的 web 應用程式。 （項目 #2 在 hello 圖。）
>
> 4. 按一下 [ **應用程式設定**]。 （項目 #3 hello 圖中。）
>
> 5. 在 hello**應用程式設定**區段中，加入新的環境變數，名為**連接埠**和 hello 值輸入自訂連接埠號碼。 （項目 #4 hello 圖中。）
>
> 6. 按一下 [儲存] 。 （項目 #5 hello 圖中。）
>
> ![在 hello Azure 入口網站中儲存自訂連接埠號碼][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>後續步驟

如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:

* [部署 Spring 開機應用程式 toohello Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務](container-service-deploy-spring-boot-app-on-kubernetes.md)

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

如需 Docker 範例專案的 hello Spring 開機進一步詳細資訊，請參閱[上開始使用 Docker Spring 開機]。

如需開始使用您自己 Spring 開機應用程式的說明，請參閱 hello **Spring Initializr** https://start.spring.io/ 在。

如需開始使用建立簡單的 Spring 開機應用程式的詳細資訊，請參閱 < 在 https://start.spring.io/ hello Spring Initializr。

針對如何 toouse 自訂的 Docker 映像與 Azure 的其他範例，請參閱[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]。

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure 容器服務 (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure 入口網站]: https://portal.azure.com/
[建立私用 Docker 容器登錄中使用 Azure 入口網站 hello]: /azure/container-registry/container-registry-get-started-portal
[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[上開始使用 Docker Spring 開機]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
