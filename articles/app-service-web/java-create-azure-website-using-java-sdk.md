---
title: "aaaCreate 使用 hello Azure SDK for Java 的 Azure App Service 中的 Web 應用程式"
description: "了解如何 toocreate Web 應用程式以程式設計方式使用的 Azure App Service 上 hello Azure SDK for Java。"
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>使用 hello Azure SDK for Java 的 Azure App Service 中建立 Web 應用程式
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>概觀
本逐步解說示範如何建立 Web 應用程式中的 Java 應用程式的 Azure SDK toocreate [Azure App Service][Azure App Service]，然後部署應用程式 tooit。 其中包括兩個部分：

* 第 1 部分會示範如何 toobuild Java 應用程式，會建立 web 應用程式。
* 第 2 部分會示範如何 toocreate 簡單 JSP"Hello World"應用程式，然後使用 FTP 用戶端 toodeploy 程式碼 tooApp 服務。

## <a name="prerequisites"></a>必要條件
### <a name="software-installations"></a>軟體安裝
hello AzureWebDemo 本文中的應用程式程式碼撰寫使用 Azure Java SDK 0.7.0，您可以安裝使用 hello [Web Platform Installer] [ Web Platform Installer] (WebPI)。 此外，請確定 toouse hello 最新版本的 hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]。 安裝 hello SDK 之後，更新您的 Eclipse 專案中的 hello 相依性執行**更新索引**中**Maven 儲存機制**，再重新加入 hello 最新版本，每個封裝中 hello **相依性**視窗。 您可以按一下來確認您已安裝的軟體在 Eclipse 中的 hello 版本**協助 > 安裝詳細資料**; 您應該有至少 hello 下列版本：

* Package for Microsoft Azure Libraries for Java 0.7.0.20150309
* Eclipse IDE for Java EE Developers 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>在 Azure 中建立和設定雲端資源
在開始此程序之前，您會需要 toohave 作用中的 Azure 訂用帳戶，並設定預設的 Active Directory (AD) 在 Azure 上。

### <a name="create-an-active-directory-ad-in-azure"></a>在 Azure 中建立 Active Directory (AD)
如果您沒有 Azure 訂用帳戶已經有 Active Directory (AD)，登入 hello [Azure 傳統入口網站][ Azure classic portal]與您的 Microsoft 帳戶。 如果您有多個訂閱，按一下**訂閱**和選取 hello 預設目錄 hello 訂閱您想要 toouse 為這個專案。 然後按一下 **套用**tooswitch toothat 訂閱檢視。

1. 選取**Active Directory**從左邊的 hello 功能表。 按一下 [新增] > [目錄] > [自訂建立]。
2. 在 [新增目錄] 中，選取 [建立新目錄]。
3. 在 [ **名稱**] 中，輸入目錄名稱。
4. 在 [網域] 中，輸入網域名稱。 這是與您的目錄; 預設隨附的基本網域名稱它有 hello 表單`<domain_name>.onmicrosoft.com`。 您可以命名會根據 hello 目錄名稱或另一個您所擁有的網域名稱。 之後，您可以新增貴組織已使用的其他網域名稱。
5. 在 [ **國家或地區**] 中，選取您的地區設定。

如需 AD 詳細資訊，請參閱 [什麼是 Azure Active Directory][What is an Azure AD directory]？

### <a name="create-a-management-certificate-for-azure"></a>建立 Azure 的管理憑證
hello Azure SDK for Java 使用管理憑證 tooauthenticate 與 Azure 訂用帳戶。 這些是您使用 tooauthenticate 使用 hello 服務管理 API tooact 代表 hello 訂用帳戶擁有者 toomanage 訂用帳戶資源的用戶端應用程式的 X.509 v3 憑證。

此程序中的 hello 程式碼會使用自我簽署的憑證 tooauthenticate 與 Azure。 在此程序需要 toocreate 憑證，並將它上傳 toohello [Azure 傳統入口網站][ Azure classic portal]事先。 這牽涉到 hello 下列步驟：

* 產生代表您的用戶端憑證的 PFX 檔案，並將其儲存於本機。
* 從 hello PFX 檔案產生管理憑證 （CER 檔案）。
* 上傳 hello CER 檔案 tooyour Azure 訂用帳戶。
* 因為 Java 使用該使用憑證的格式 tooauthenticate 轉換 JKS，hello PFX 檔案。
* 撰寫 hello 應用程式的驗證程式碼，它會參考 toohello 本機 JKS 檔案。

當您完成此程序時，hello CER 憑證都位於您的 Azure 訂閱和 hello JKS 憑證都位於本機磁碟機上。 如需管理憑證的詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。

#### <a name="create-a-certificate"></a>建立憑證
toocreate 您自己的自我簽署的憑證，開啟命令主控台，在您的作業系統上，然後執行下列命令的 hello。

> **注意：** hello 電腦執行這個命令必須有 hello 安裝的 JDK。 此外，hello 路徑 toohello keytool hello hello JDK 安裝的位置而定。 如需詳細資訊，請參閱[金鑰和憑證管理工具 (keytool)] [ Key and Certificate Management Tool (keytool)] hello Java 線上文件中。
> 
> 

toocreate hello.pfx 檔案：

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

toocreate hello.cer 檔案：

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

其中：

* `<java-install-dir>`是您已安裝 Java hello 路徑 toohello 目錄。
* `<keystore-id>`hello 金鑰存放區項目識別項 (例如， `AzureRemoteAccess`)。
* `<cert-store-dir>`是您想在其中 toostore 憑證 hello 路徑 toohello 目錄 (例如`C:/Certificates`)。
* `<cert-file-name>`這是 hello hello 憑證檔案名稱 (例如`AzureWebDemoCert`)。
* `<password>`這是您選擇 tooprotect hello 憑證; hello 密碼它必須是至少 6 個字元。 您可以不輸入密碼，但不建議這麼做。
* `<dname>`hello X.500 辨別名稱 toobe 相關聯的別名，並當做 hello 簽發者和 hello 自我簽署憑證中的 [主旨] 欄位。

如需詳細資訊，請參閱 [建立和上傳 Azure 的管理憑證][Create and Upload a Management Certificate for Azure]。

#### <a name="upload-hello-certificate"></a>上傳 hello 憑證
tooupload 自我簽署的憑證 tooAzure，移 toohello**設定**hello 傳統入口網站，在頁面上，然後按一下 [hello**管理憑證**] 索引標籤。按一下**上傳**底部 hello hello 頁面上，瀏覽 toohello 建立 hello CER 檔案的位置。

#### <a name="convert-hello-pfx-file-into-jks"></a>Hello PFX 檔轉換成 JKS
在 hello （以系統管理員身分執行） 的 Windows 命令提示字元，cd toohello 目錄包含 hello 憑證並執行下列命令，hello 其中`<java-install-dir>`是您安裝 Java 在電腦的 hello 目錄：

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. 出現提示時，輸入 hello 目的地 keystore 的密碼;這會是 hello hello JKS 檔案的密碼。
2. 出現提示時，輸入 hello 來源 keystore 的密碼。這是您指定 hello PFX 檔案的 hello 密碼。

hello 兩個密碼並沒有 toobe hello 相同。 您可以不輸入密碼，但不建議這麼做。

## <a name="build-a-web-app-creation-application"></a>建置 Web 應用程式建立應用程式
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>建立 hello Eclipse 工作區和 Maven 專案
在本節中建立工作區和 Maven hello web 應用程式建立應用程式的專案，名為 AzureWebDemo。

1. 建立新的 Maven 專案。 按一下 [檔案] > [新增] > [Maven 專案]。 在 [新增 Maven 專案] 中，選取 [建立簡單專案] 和 [使用預設工作區位置]。
2. Hello 第二頁上**新 Maven 專案**，指定下列 hello:
   
   * 群組識別碼： `com.<username>.azure.webdemo`
   * 成品識別碼：AzureWebDemo
   * 版本：0.0.1-SNAPSHOT
   * 封裝：jar
   * 名稱：AzureWebDemo
     
     按一下 [完成] 。
3. Hello 新專案的 pom.xml 檔案總管中開啟專案。 選取 hello**相依性** 索引標籤。由於這是新專案，所以尚未列出任何封裝。
4. 檢視開啟 hello Maven 儲存機制。 按一下 [視窗] > [顯示檢視] > [其他] > [Maven] > [Maven 儲存機制]，然後按一下 [確定]。 hello **Maven 儲存機制**檢視將會出現在 hello hello IDE 底部。
5. 開啟**通用儲存機制**，以滑鼠右鍵按一下 hello**中央**儲存機制，並選取**重建索引**。
   
    ![][1]
   
    此步驟可能需要幾分鐘的時間視您的連線 hello 速度而定。 當 hello 索引重建作業時，您應該會看到 hello Microsoft Azure 套件 hello 中的**中央**Maven 儲存機制。
6. 在 [相依性] 中，按一下 [新增]。 在 [輸入群組識別碼...] 中輸入 `azure-management`。 選取的基本管理和應用程式服務 Web 應用程式管理的 hello 封裝：
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **注意：**新版本發行之後，您要更新 hello 相依性，如果您需要 toore-這份清單中加入每個 hello 相依性。
   > 按一下 之後**新增**並選取每個相依性，它會使用 hello 新版本號碼 hello**相依性**清單。
   > 
   > 

按一下 [確定] 。 hello Azure 的封裝，則會出現在 hello**相依性**清單。

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>呼叫 hello Azure SDK 撰寫 Java 程式碼 tooCreate Web 應用程式
接下來，撰寫 Java toocreate hello App Service web 應用程式會呼叫應用程式開發介面 hello Azure SDK 中的 hello 程式碼。

1. 建立 Java 類別 toocontain hello 主要進入點的程式碼。 在 專案總管 hello 專案節點上按一下滑鼠右鍵，然後選取**新增 > 類別**。
2. 在**新 Java 類別**，hello 類別命名`WebCreator`並檢查 hello**公用靜態 void main**核取方塊。 hello 選取項目應該會出現，如下所示：
   
    ![][2]
3. 按一下 [完成] 。 hello WebCreator.java 檔案會出現在 [專案總管] 中。

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>呼叫 hello Azure API tooCreate App Service Web 應用程式
#### <a name="add-necessary-imports"></a>新增必要匯入
在 WebCreator.java，加入下列匯入; hello這些匯入提供使用 Azure 應用程式開發介面存取 tooclasses hello 中的管理程式庫：

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>定義 hello 主要進入點類別
Hello 目的 hello AzureWebDemo 應用程式是 toocreate App Service Web 應用程式，因為此應用程式的名稱 hello 主要類別`WebAppCreator`。 這個類別會提供 hello 主要進入點呼叫的程式碼 hello Azure 服務管理 API toocreate hello web 應用程式。

新增下列 hello web 應用程式和網路空間的參數定義的 hello。 您將需要 tooprovide 您自己的 Azure 訂用帳戶 ID 和憑證資訊。

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

其中：

* `<subscription-id>`這是您想在其中 toocreate hello 資源 hello Azure 訂用帳戶識別碼。
* `<certificate-store-path>`是您的本機憑證存放區目錄中的 hello 路徑和檔名 toohello JKS 檔案。 例如，`C:/Certificates/CertificateName.jks` 適用於 Linux，而 `C:\Certificates\CertificateName.jks` 適用於 Windows。
* `<certificate-password>`這是您在建立 JKS 憑證時指定的 hello 密碼。
* `webAppName`可以是您選擇; 任何名稱此程序會使用 hello 名稱`WebDemoWebApp`。 hello 的完整網域名稱為 hello`webAppName`以 hello`domainName`附加，因此在此案例 hello 完整的網域是`webdemowebapp.azurewebsites.net`。
* `domainName` 應如上所述加以指定。
* `webSpaceName`應該有一個 hello 中定義的值 hello [WebSpaceNames] [ WebSpaceNames]類別。
* `appServicePlanName` 應如上所述加以指定。

> **注意：**每次執行此應用程式時，您需要 toochange hello 值`webAppName`和`appServicePlanName`（或刪除 hello hello Azure 入口網站上的 web 應用程式） 再執行一次 hello 應用程式。 否則，執行也會失敗，因為 hello 相同的資源已存在於 Azure。
> 
> 

#### <a name="define-hello-web-creation-method"></a>定義 hello web 建立方法
接下來，定義方法 toocreate hello web 應用程式。 這個方法， `createWebApp`，指定 hello web 應用程式與 hello 網路空間 hello 參數。 它也會建立並設定 hello App Service Web 應用程式管理用戶端，定義 hello [WebSiteManagementClient] [ WebSiteManagementClient]物件。 hello 管理用戶端就是索引鍵 toocreating Web 應用程式。 它提供可讓應用程式 toomanage 藉由呼叫 hello 服務管理 API 的 web 應用程式 （如建立、 更新和刪除，請執行作業） 的 RESTful web 服務。

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

hello 程式碼將輸出指出成功或失敗，hello 回應 hello HTTP 狀態，而且如果成功的話，會輸出 hello hello 建立 web 應用程式名稱。

#### <a name="define-hello-main-method"></a>定義 hello main （） 方法
提供 hello main （） 方法的程式碼的呼叫 createWebApp() toocreate hello web 應用程式。

最後，從 `main` 呼叫 `createWebApp`：

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>執行 hello 應用程式，並確認 web 應用程式建立
tooverify 執行應用程式，按一下**執行 > 執行**。 Hello 應用程式完成時執行，您應該會看到下列輸出 hello Eclipse 主控台中的 hello:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

登入 hello Azure 傳統入口網站並按一下**Web 應用程式**。 hello 新 web 應用程式應該會在幾分鐘內出現 hello Web 應用程式清單中。

## <a name="deploying-an-application-toohello-web-app"></a>部署應用程式 toohello Web 應用程式
您已執行 AzureWebDemo 並建立 hello 新 web 應用程式，登入 hello 傳統入口網站，按一下之後**Web 應用程式**，然後選取**WebDemoWebApp**在 hello **Web 應用程式**清單。 在 hello web 應用程式的儀表板 頁面上，按一下 **瀏覽**(或按一下 hello URL `webdemowebapp.azurewebsites.net`) toonavigate tooit。 您會看到空白預留位置 頁面上，因為沒有內容尚未被 toohello 已發行的 web 應用程式。

接下來您將建立"Hello World"應用程式，並將它部署 toohello web 應用程式。

### <a name="create-a-jsp-hello-world-application"></a>建立 JSP Hello World 應用程式
#### <a name="create-hello-application"></a>建立 hello 應用程式
順序 toodemonstrate toodeploy 應用程式 toohello web hello 如何在下列程序為您示範如何 toocreate 簡單"Hello World"Java 應用程式，並將它上傳 toohello App Service Web 應用程式建立您的應用程式。

1. 按一下 [檔案] > [新增] > [動態 Web 專案]。 將它命名為 `JSPHello` 您不需要 toochange 在這個對話方塊中的任何其他設定。 按一下 [完成] 。
   
    ![][3]
2. 在 專案總管 中，展開 hello **JSPHello**專案中，以滑鼠右鍵按一下**WebContent**，然後按一下**新增 > JSP 檔案**。 在 [hello] 新增 JSP 檔案對話方塊 hello 新檔案名稱中`index.jsp`。 按一下 [下一步] 。
3. 在 hello**選取 JSP 範本**對話方塊中，選取**新增 JSP 檔案 (html)**按一下**完成**。
4. 在 index.jsp 中，加入下列程式碼中 hello hello`<head>`和`<body>`標記區段：
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>在本機執行 hello Hello World 應用程式
執行此應用程式之前，您需要 tooconfigure 一些屬性。

1. 以滑鼠右鍵按一下 hello **JSPHello**專案，然後選取**屬性**。
2. 在 hello**屬性**對話方塊： 選取**Java 組建路徑**，選取 hello**順序和匯出**索引標籤上，核取**JRE 系統程式庫**，然後按一下**向上**toomove 它 toohello hello 清單的頂端。
   
    ![][4]
3. 此外在 hello**屬性**對話方塊： 選取**目標執行階段**按一下**新增**。
4. 在 hello**新的伺服器執行階段環境**對話方塊中，例如伺服器選取**Apache Tomcat v7.0**按一下**下一步**。 在 hello **Tomcat 伺服器**對話方塊中，設定**名稱**太`Apache Tomcat v7.0`，並設定**Tomcat 安裝目錄**toohello 目錄，您已經安裝 hello 版本您想要 toouse tomcat 伺服器。
   
    ![][5]
   
    按一下 [完成] 。
5. 接著您回復 toohello**目標執行階段**頁面 hello**屬性**對話方塊。 選取 [Apache Tomcat v7.0]，然後按一下 [確定]。
   
    ![][6]
6. 在 hello Eclipse**執行**功能表上，按一下 **執行**。 在 hello**執行身分**對話方塊中，選取**在伺服器上執行**。 在 hello**在伺服器上執行**對話方塊中，選取**Tomcat 伺服器 v7.0**:
   
    ![][7]
   
    按一下 [完成] 。
7. 當 hello 應用程式執行，您應該會看見 hello **JSPHello**頁面出現在 Eclipse 中的 localhost 視窗 (`http://localhost:8080/JSPHello/`)、 顯示 hello 下列訊息：
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>匯出 WAR hello 應用程式
可讓您可以將它部署 toohello web 應用程式，請為網頁封存檔 (WAR) 檔案匯出 hello web 專案檔。 hello 下列 web 專案檔位於 hello WebContent 資料夾中：

    META-INF
    WEB-INF
    index.jsp

1. Hello WebContent 資料夾上按一下滑鼠右鍵，然後選取**匯出**。
2. 在 hello**匯出選取** 對話方塊中，按一下**Web > WAR**檔案，然後按一下 **下一步**。
3. 在 [hello**匯出 WAR** ] 對話方塊中，在 hello 目前專案中，選取 hello src 目錄，並納入 hello hello 結尾的 hello WAR 檔案名稱。 例如：
   
    `<project-path>/JSPHello/src/JSPHello.war`

如需有關部署的 WAR 檔案的詳細資訊，請參閱[新增 App Service Web 應用程式的 Java 應用程式 tooAzure](web-sites-java-add-app.md)。

### <a name="deploying-hello-hello-world-application-using-ftp"></a>部署的 hello Hello World 應用程式使用 FTP
選取第三方 FTP 用戶端 toopublish hello 應用程式。 此程序描述兩個選項： hello Kudu 主控台內建在 Azure。和 FileZilla，方便、 圖形化使用者介面的常用工具。

> **注意：** hello Azure Toolkit for Eclipse 支援部署 toostorage 帳戶和雲端服務，但目前不支援部署 tooweb 應用程式。 您可以部署 toostorage 帳戶和雲端服務中所述，使用 Azure 部署專案[在 Eclipse 中建立 Azure Hello World 應用程式](http://msdn.microsoft.com/library/azure/hh690944.aspx)，但不適用於 tooweb 應用程式。 使用其他方法，例如 FTP 或 GitHub tootransfer 檔案 tooyour web 應用程式。
> 
> **注意：**我們不建議使用 FTP，從 hello Windows 命令提示字元 （hello 命令列 FTP.EXE 公用程式隨附於 Windows）。 使用作用中的 FTP，例如 FTP.EXE，FTP 用戶端通常會將 toowork 容錯移轉的防火牆。 作用中 FTP 指定以 LAN 為基礎的內部位址，toowhich FTP 伺服器可能會失敗 tooconnect。
> 
> 

如需有關部署 tooan App Service web 應用程式使用 FTP 的詳細資訊，請參閱下列主題中的 hello:

* [使用 FTP 公用程式部署](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>[設定部署認證] 來設定
請確定您已執行 hello **AzureWebDemo**應用程式 toocreate web 應用程式。 傳輸檔案 toothis 位置。

1. 登入 hello 傳統入口網站並按一下**Web 應用程式**。 請確定**WebDemoWebApp**會出現在 hello web 應用程式清單，並確定它正在執行。 按一下**WebDemoWebApp** tooopen 其**儀表板**頁面。
2. 在 hello**儀表板**頁面的 **快速概覽**，按一下 **設定部署認證**(如果您已經有部署認證，這樣會讀取**重設部署認證**)。
   
    部署認證與 Microsoft 帳戶相關聯。 您需要 toospecify 使用者名稱和密碼，您可以使用 toodeploy 使用 Git 和 FTP。 您可以使用這些認證 toodeploy tooany web 應用程式中所有的 Azure 訂用帳戶與您的 Microsoft 帳戶相關聯。 提供 Git 和 FTP 的部署認證 hello 對話方塊中，以及記錄 hello 使用者名稱和密碼，供日後使用。

#### <a name="get-ftp-connection-information"></a>取得 FTP 連線資訊
toouse FTP toodeploy 應用程式檔案 toohello 新建立的 web 應用程式，您需要 tooobtain 連接資訊。 有兩種方式 tooobtain 連接資訊。 一種方式是 toovisit hello web 應用程式的**儀表板**頁面; hello 另一種方式是 toodownload hello web 應用程式的發行設定檔。 hello 發行設定檔是 XML 檔案，提供您的 web 應用程式在 Azure App Service 中的資訊，例如 FTP 主機名稱和登入認證。 您可以使用此使用者名稱和密碼 toodeploy tooany web 應用程式不是只有此一個 hello Azure 帳戶相關聯的所有訂用帳戶中。

tooobtain FTP 連線資訊從 hello web 應用程式的刀鋒視窗中 hello [Azure 入口網站][Azure Portal]:

1. 在下**Essentials**，尋找並複製 hello **FTP 主機名稱**。 這是相似的 URI 太`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`。
2. 在 [基本功能] 之下，尋找並複製 [FTP/部署使用者名稱]。 這將會有 hello 形式*webappname\deployment-username*; 例如`WebDemoWebApp\deployer77`。

從 hello tooobtain FTP 連線資訊發行設定檔：

1. 在 hello web 應用程式的刀鋒視窗中，按一下 **取得發行設定檔**。 這會下載.publishsettings 檔案 tooyour 本機磁碟機。
2. 在 XML 編輯器或文字編輯器中開啟 hello.publishsettings 檔案，並尋找 hello`<publishProfile>`項目包含`publishMethod="FTP"`。 它看起來應該類似下列 hello:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. 請注意該 hello web 應用程式的`publishProfile`設定對應 toohello FileZilla 網站管理員設定，如下所示：

* `publishUrl`hello 與相同**FTP 主機名稱**，hello 您的設定值**主機**。
* `publishMethod="FTP"`表示您設定**通訊協定**太**FTP-檔案傳輸通訊協定**，和**加密**太**使用一般 FTP**。
* `userName`和`userPWD`是索引鍵的 hello 實際您指定當您重設 hello 的部署認證的使用者名稱和密碼值。 `userName`hello 與相同**部署 / FTP 使用者**。 它們會太對應**使用者**和**密碼**FileZilla 中。
* `ftpPassiveMode="True"`表示該 hello FTP 站台使用被動 FTP 傳送;選取**被動**上 hello**傳輸設定** 索引標籤。

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>設定 hello Web 應用程式 toohost Java 應用程式
發佈 hello 應用程式之前，您需要 toochange 一些組態設定，讓 hello web 應用程式可以裝載 Java 應用程式。

1. 在 hello 傳統入口網站移 toohello web 應用程式的**儀表板**頁面上，按一下 **設定**。 在 hello**設定**頁面上，指定下列設定的 hello。
2. 在**Java 版本**hello 預設值是**關閉**; 選取 hello Java 版本應用程式的目標，例如 1.7.0_51。 執行這項操作之後，也請確定**網頁容器**設定 tooa Tomcat 伺服器版本。
3. 在**預設文件**、 新增 index.jsp 和 toohello hello 清單頂端上移。 （hello 預設 web 應用程式的檔案是 hostingstart.html）。
4. 按一下 [儲存] 。

#### <a name="publish-your-application-using-kudu"></a>使用 Kudu 發佈您的應用程式
其中一種方式 toopublish hello 應用程式是 toouse hello Kudu 偵錯主控台內建在 Azure。 Kudu 為已知 toobe 穩定且一致的應用程式服務 Web 應用程式和 Tomcat 伺服器。 您可以存取 hello web 應用程式的 hello 主控台瀏覽下列表單的 hello tooa URL:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. 在此程序 hello Kudu 主控台位於下列 URL; hello瀏覽 toothis 位置：
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. 從 hello 上方功能表中，選取**偵錯主控台 > CMD**。
3. 在 hello 主控台命令列中，瀏覽過`/site/wwwroot`(或按一下`site`，然後`wwwroot`hello 頁面頂端的 hello hello 目錄檢視中):
   
    `cd /site/wwwroot`
4. 在您指定 [ **Java 版本**] 後，Tomcat 伺服器應建立 webapps 目錄。 在 hello 主控台命令列瀏覽 toohello webapps 目錄：
   
    `mkdir webapps`
   
    `cd webapps`
5. 拖曳從 JSPHello.war`<project-path>/JSPHello/src/`拖放到 hello Kudu 目錄檢視下`/site/wwwroot/webapps`。 請勿拖曳 toohello 」 將拖曳到此處 tooupload 和 zip 」 區域中，因為 Tomcat 會將它解壓縮。
   
   ![][8]

在第一個 JSPHello.war 會出現在 hello 目錄區域本身：

  ![][9]

短時間 （可能少於 5 分鐘） 內 Tomcat 伺服器會將 hello WAR 檔案解壓縮至打開包裝後的 JSPHello 目錄。 是否已將工具解壓縮並複製那里 index.jsp，按一下 hello 根目錄 toosee。 如果是這樣，瀏覽後 toohello webapps 目錄 toosee 是否 hello 解壓縮的 JSPHello 在建立目錄。 如果您未看見這些項目，請稍後並重複。

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>使用 FileZilla 發佈您的應用程式 (選用)
您可以使用 toopublish hello 應用程式的另一個工具是 FileZilla、 受歡迎的第三方 FTP 用戶端，以方便、 圖形化使用者介面。 如果您還沒有 FileZilla，可以從 [http://filezilla-project.org/](http://filezilla-project.org/) 下載並安裝此工具。 如需有關使用 hello 用戶端的詳細資訊，請參閱 hello [FileZilla 文件](https://wiki.filezilla-project.org/Documentation)和此部落格文章[FTP 用戶端-第 4 部分： FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx)。

1. 在 FileZilla 中，按一下 [檔案] > [網站管理員]。
2. 在 hello**網站管理員** 對話方塊中，按一下 **新站台**。 新的空白 FTP 站台會出現在**選取項目**提示您 tooprovide 名稱。 在此程序中，將它命名為 `AzureWebDemo-FTP`
   
    在 hello**一般**索引標籤上，指定下列設定的 hello:
   
   * **主機：** Enter hello **FTP 主機名稱**您複製從 hello 儀表板。
   * **連接埠：** （保持空白，這是被動傳輸以及 hello 伺服器將會決定 hello 連接埠 toouse。）
   * **通訊協定：** (FTP 檔案傳輸通訊協定)
   * **加密：** 使用一般 FTP
   * **登入類型：** 正常
   * **使用者：** Enter hello 部署 / FTP 使用者，您所複製的 hello 儀表板。 這是 hello 完整 FTP 使用者名稱，其具有 hello 表單*webappname\username*。
   * **密碼：**輸入 hello 密碼，您會指定當您將 hello 的部署認證。
     
     在 hello**傳輸設定**索引標籤上，選取**被動**。
3. 按一下 [ **連接**]。 如果成功，FileZilla 的主控台將顯示`Status: Connected`訊息和問題`LIST`命令 toolist hello 目錄內容。
4. 在 [hello**本機**站台] 面板中，選取 hello 來源目錄中的 hello JSPHello.war 檔案位於; hello 路徑會是類似 toohello 下列：
   
    `<project-path>/JSPHello/src/`
5. 在 [hello**遠端**站台] 面板中，選取 hello 目的地資料夾。 您將部署 hello WAR 檔案 toohello `webapps` hello web 應用程式的根目錄下的目錄。 瀏覽過`/site/wwwroot`，以滑鼠右鍵按一下`wwwroot`，然後選取**建立目錄**。 名稱 hello 目錄`webapps`並輸入該目錄。
6. 太傳輸 JSPHello.war`/site/wwwroot/webapps`。 選取在 hello JSPHello.war**本機**檔案清單，以滑鼠右鍵按一下它，然後選取**上傳**。 您應看見該檔案出現在 `/site/wwwroot/webapps`中。
7. Tomcat 伺服器複製 JSPHello.war toohello webapps 目錄之後，將會自動解除封裝 （解壓縮） hello hello WAR 檔案中的檔案。 雖然 Tomcat 伺服器一開始會解壓縮幾乎會立即，它可能需要很長時間 hello FTP 用戶端中的 hello 檔案 tooappear （可能是小時）。

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>在 hello Web 應用程式上執行 hello Hello World 應用程式
1. 您已經上傳 hello WAR 檔案，並確認已建立解壓縮 Tomcat 伺服器之後`JSPHello`目錄中，瀏覽過`http://webdemowebapp.azurewebsites.net/JSPHello`toorun hello 應用程式。
   
   > **注意：**如果您按一下**瀏覽**從 hello 傳統入口網站，您可能會收到 hello 預設網頁，指出 「 此基礎的 Java web 應用程式已成功建立。 」 順序 tooview hello 而不是 hello 預設網頁的應用程式輸出中，您可能有 toorefresh hello 網頁。
   > 
   > 
2. Hello 應用程式執行時，您應該會看到網頁以 hello 下列輸出：
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>清除 Azure 資源
此程序會建立 App Service Web 應用程式。 您還是必須支付 hello 資源存在於。 除非您計劃 toocontinue 使用 hello web 應用程式執行測試或開發，您應該考慮停止或刪除它。 已停止的 Web 應用程式仍將帶來少許費用，但您可以隨時予以重新啟動。 刪除 web 應用程式會清除您已上傳 tooit 的所有資料。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
