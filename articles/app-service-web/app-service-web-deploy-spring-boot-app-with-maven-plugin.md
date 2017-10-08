---
title: "Azure Web Apps toodeploy Spring 開機應用程式 tooAzure 的 aaaHow toouse hello Maven 外掛程式"
description: "了解如何 toouse hello Maven 外掛程式 Azure Web Apps toodeploy Spring 開機應用程式 tooAzure。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>如何 toouse hello Maven 外掛程式 Azure Web Apps toodeploy Spring 開機應用程式 tooAzure

hello [Azure Web 應用程式的 Maven 外掛程式](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)如[Apache Maven](http://maven.apache.org/)提供緊密整合到 Maven 專案中，Azure 應用程式服務，並簡化開發人員 toodeploy web 應用程式的 hello 程序tooAzure 應用程式服務。

本文將示範使用 Azure Web Apps toodeploy hello Maven 外掛程式範例 Spring 開機應用程式 tooAzure 應用程式服務。

> [!NOTE]
>
> hello Azure Web 應用程式的 Maven 外掛程式是目前可供預覽。 現在，只有 FTP 發行支援，雖然 hello 未來計劃的額外功能。
>

## <a name="prerequisites"></a>必要條件

在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。
* hello [Azure 命令列介面 (CLI)]。
* 最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。
* Apache 的 [Maven] 建置工具 (第 3 版)。
* [Git] 用戶端。

## <a name="clone-hello-sample-spring-boot-web-app"></a>複製 hello 範例 Spring 開機 web 應用程式

在本節中，您會在本機複製已完成 Spring Boot 應用程式，並且進行測試。

1. 開啟命令提示字元或終端機視窗，並建立本機目錄 toohold 您 Spring 開機應用程式，並變更 toothat 目錄;例如：
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 或 --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. 複製 hello [Spring 開機入門]範例專案到 hello 目錄，您所建立的; 例如：
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. 變更目錄已完成的 toohello 專案;例如：
   ```shell
   cd gs-spring-boot/complete
   ```

1. 建置使用 Maven; hello JAR 檔案例如：
   ```shell
   mvn clean package
   ```

1. Hello web 應用程式建立後，開始使用 Maven; hello web 應用程式例如：
   ```shell
   mvn spring-boot:run
   ```

1. 藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。 例如，您可以使用下列命令，如果您有可用的 curl hello:
   ```shell
   curl http://localhost:8080
   ```

1. 您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**

## <a name="create-an-azure-service-principal"></a>建立 Azure 服務主體

在本節中，您建立 Azure 部署您的 web 應用程式 tooAzure 時 hello Maven 外掛程式使用的服務主體。

1. 開啟命令提示字元。

1. 登入您的 Azure 帳戶使用 hello Azure CLI:
   ```shell
   az login
   ```
   請遵循 hello 指示 toocomplete hello 登入程序。

1. 建立 Azure 服務主體：
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   其中`uuuuuuuu`是 hello 的使用者名稱和`pppppppp`hello hello 服務主體的密碼。

1. Azure 會使用類似下列範例中的 hello 的 JSON 回應：
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > 當您設定您的 web 應用程式 tooAzure hello Maven 外掛程式 toodeploy 時，您將使用此 JSON 回應 hello 值。 hello `aaaaaaaa`， `uuuuuuuu`， `pppppppp`，和`tttttttt`預留位置的值，也就是用於此範例 toomake 它更容易 toomap 這些 tootheir 個別項目的值設定您的 Maven 時`settings.xml`hello 中檔案的下一步一節。
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>設定您的 Azure 服務主體的 Maven toouse

在本節中，您可以使用 hello 值從 Maven 使用部署您的 web 應用程式 tooAzure 時您 Azure 服務主體 tooconfigure hello 的驗證。

1. 開啟您的 Maven`settings.xml`檔案文字編輯器中; 這個檔案可能是路徑，如下列範例中的 hello:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. 從這個教學課程 toohello hello 上一節中新增您的 Azure 服務主體設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   其中：
   元素 | 說明
   ---|---|---
   `<id>` | 指定 Maven 使用 toolook 註冊您的安全性設定，當您部署您的 web 應用程式 tooAzure 的唯一名稱。
   `<client>` | 包含 hello`appId`從您的服務主體的值。
   `<tenant>` | 包含 hello`tenant`從您的服務主體的值。
   `<key>` | 包含 hello`password`從您的服務主體的值。
   `<environment>` | 定義 hello 目標 Azure 雲端環境，也就是`AZURE`在此範例中。 (環境的完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件)

1. 儲存並關閉 hello *settings.xml*檔案。

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>選擇性： 部署您的 web 應用程式 tooAzure 之前自訂您 pom.xml

開啟 hello`pom.xml`在文字編輯器中，應用程式 Spring 開機檔案，然後找出 hello`<plugin>`元素`azure-webapp-maven-plugin`。 這個項目應該類似下列範例中的 hello:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

有數個值，您可以修改 hello Maven 外掛程式，而且每個這些元件的詳細的描述在 hello [Azure Web 應用程式的 Maven 外掛程式]文件。 也就是說，有數個值值得在這篇文章中反白顯示：

元素 | 說明
---|---|---
`<version>` | 指定 hello 版的 hello [Azure Web 應用程式的 Maven 外掛程式]。 您應該檢查 hello 版本列在 hello [Maven 中央儲存機制](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)您使用的 tooensure hello 最新版本。
`<authentication>` | 指定 Azure，這在此範例中包含的 hello 驗證資訊`<serverId>`包含項目`azure-auth`;Maven 使用 hello Azure 服務主體值的值 toolook 中您 Maven *settings.xml*在本文的前一節中所定義的檔案。
`<resourceGroup>` | 指定 hello 目標資源群組，也就是`maven-plugin`在此範例中。 如果不存在，會在部署期間建立 hello 資源群組。
`<appName>` | 指定 web 應用程式的 hello 目標名稱。 在此範例中，是 hello 目標名稱`maven-web-app-${maven.build.timestamp}`，其中 hello`${maven.build.timestamp}`尾碼會附加在這個範例 tooavoid 衝突。 （hello 時間戳記是選擇性的; 您可以指定任何唯一的字串 hello 應用程式名稱）。
`<region>` | 指定 hello 目標區域，而在此範例中`westus`。 (完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)
`<javaVersion>` | 指定 web 應用程式的 hello Java 執行階段版本。 (完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)
`<deploymentType>` | 指定 Web 應用程式的部署類型。 雖然其他部署類型的支援正在開發中，現在只有 `ftp` 受到支援。
`<resources>` | 指定資源和 Maven 使用時部署您的 web 應用程式 tooAzure 目標目的地。 在此範例中，兩個`<resource>`項目會指定 Maven 將部署 hello JAR 檔案，以您的 web 應用程式和 hello *web.config* hello Spring 開機專案檔案。

## <a name="build-and-deploy-your-web-app-tooazure"></a>建置和部署您的 web 應用程式 tooAzure

一旦您已設定的所有 hello 設定 hello 前面的本文區段中，您就準備好 toodeploy 您 web 應用程式 tooAzure。 toodo 因此，使用下列步驟的 hello:

1. 從 hello 命令提示字元或稍早所使用的終端機視窗，重建 hello JAR 檔案，如果您進行任何變更 toohello 使用 Maven *pom.xml*檔案; 例如：
   ```shell
   mvn clean package
   ```

1. 部署您的 web 應用程式 tooAzure 使用 Maven;例如：
   ```shell
   mvn azure-webapp:deploy
   ```

Maven 會部署您的 web 應用程式 tooAzure;如果 hello web 應用程式不存在，則會建立。

已部署您的網站，將無法 toomanage 它使用 hello [Azure 入口網站]。

* 您的 Web 應用程式會列在**應用程式服務** 中：

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* Hello URL 的 web 應用程式將會列在 hello 和**概觀**web 應用程式：

   ![決定您 web 應用程式的 hello URL][AP02]

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

如需有關 hello 本文所討論的各種技術，請參閱下列文章 hello:

* [Azure Web 應用程式的 Maven 外掛程式]

* [登入從 hello Azure CLI tooAzure](/azure/xplat-cli-connect)

* [如何 toouse hello Maven 外掛程式 toodeploy Azure Web 應用程式容器化的 Spring 開機應用程式 tooAzure](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [使用 Azure CLI 2.0 來建立 Azure 服務主體](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 設定參考](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure 入口網站]: https://portal.azure.com/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring 開機入門]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
