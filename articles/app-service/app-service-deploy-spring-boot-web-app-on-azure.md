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
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="848ee-103">部署 Spring 開機應用程式 toohello Azure App Service</span><span class="sxs-lookup"><span data-stu-id="848ee-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="848ee-104">hello  **[Spring 架構]**是開放原始碼解決方案，可協助 Java 開發人員建立企業級應用程式，且其中一個是建立在該平台之上的 hello 更常用專案[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="848ee-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="848ee-105">本教學課程將逐步引導您透過建立 hello 範例 Spring 開機開始使用 web 應用程式，並將它部署到太[Azure App Service]。</span><span class="sxs-lookup"><span data-stu-id="848ee-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="848ee-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="848ee-106">Prerequisites</span></span>

<span data-ttu-id="848ee-107">在訂單 toocomplete hello 步驟本教學課程中，您需要 toohave hello 下列：</span><span class="sxs-lookup"><span data-stu-id="848ee-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="848ee-108">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="848ee-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="848ee-109">最新的 [Java 開發工具組 (JDK)]。</span><span class="sxs-lookup"><span data-stu-id="848ee-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="848ee-110">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="848ee-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="848ee-111">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="848ee-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="848ee-112">建立 hello Spring 開機開始使用 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="848ee-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="848ee-113">hello 下列步驟將引導您完成必要的 toocreate 簡單的 Spring 開機 web 應用程式並在本機測試 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="848ee-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="848ee-114">開啟命令提示字元，並建立本機目錄 toohold，您的應用程式，以及變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="848ee-115">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="848ee-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="848ee-116">複製 hello [Spring 開機入門]範例專案到您剛建立; hello 目錄，例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="848ee-117">變更目錄已完成的 toohello 專案;例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="848ee-118">建置使用 Maven; hello JAR 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="848ee-119">一旦建立 hello web 應用程式之後，變更目錄 toohello JAR 檔案，然後啟動 hello web 應用程式。例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="848ee-120">藉由瀏覽 toohttp://localhost:8080 使用網頁瀏覽器，測試 hello web 應用程式或使用類似下列範例，如果您有可用的 curl hello hello 語法：</span><span class="sxs-lookup"><span data-stu-id="848ee-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="848ee-121">您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**</span><span class="sxs-lookup"><span data-stu-id="848ee-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![瀏覽範例應用程式][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="848ee-123">建立 Azure Web 應用程式以搭配 Java 使用</span><span class="sxs-lookup"><span data-stu-id="848ee-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="848ee-124">hello 下列步驟將逐步引導您完成 hello 步驟 toocreate Azure Web 應用程式、 設定所需的 hello 設定 Java，並設定 FTP 認證。</span><span class="sxs-lookup"><span data-stu-id="848ee-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="848ee-125">瀏覽 toohello [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="848ee-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="848ee-126">一旦您已經登入您的帳戶在 hello Azure 入口網站上，按一下 [hello] 功能表圖示**應用程式服務**:</span><span class="sxs-lookup"><span data-stu-id="848ee-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure 入口網站][AZ01]

1. <span data-ttu-id="848ee-128">當 hello**應用程式服務**頁面隨即顯示，請按一下**+ 加**toocreate 新的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="848ee-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![建立應用程式服務][AZ02]

1. <span data-ttu-id="848ee-130">顯示 hello 清單中的 web 應用程式範本時，按一下 hello hello 連結基本的 Microsoft Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="848ee-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Web 應用程式範本][AZ03]

1. <span data-ttu-id="848ee-132">Hello hello Web 應用程式範本資訊] 頁面出現時，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="848ee-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![建立 Web 應用程式][AZ04]

1. <span data-ttu-id="848ee-134">為您的 Web 應用程式提供唯一的名稱並指定任何其他設定，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="848ee-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![建立 Web 應用程式設定][AZ05]

1. <span data-ttu-id="848ee-136">一旦建立您的 web 應用程式之後，按一下 [hello] 功能表圖示**應用程式服務**，然後按一下您剛建立的 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="848ee-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![列出 Web 應用程式][AZ06]

1. <span data-ttu-id="848ee-138">顯示您的 web 應用程式時，請使用下列步驟的 hello 指定 hello Java 版本：</span><span class="sxs-lookup"><span data-stu-id="848ee-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="848ee-139">a.</span><span class="sxs-lookup"><span data-stu-id="848ee-139">a.</span></span> <span data-ttu-id="848ee-140">按一下 hello**應用程式設定**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="848ee-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="848ee-141">b.</span><span class="sxs-lookup"><span data-stu-id="848ee-141">b.</span></span> <span data-ttu-id="848ee-142">選擇**Java 8** hello Java 版本。</span><span class="sxs-lookup"><span data-stu-id="848ee-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="848ee-143">c.</span><span class="sxs-lookup"><span data-stu-id="848ee-143">c.</span></span> <span data-ttu-id="848ee-144">選擇**Newest** hello 次要的 Java 版本。</span><span class="sxs-lookup"><span data-stu-id="848ee-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="848ee-145">d.</span><span class="sxs-lookup"><span data-stu-id="848ee-145">d.</span></span> <span data-ttu-id="848ee-146">選擇**最新的 Tomcat 8.5** hello web 容器。</span><span class="sxs-lookup"><span data-stu-id="848ee-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="848ee-147">（這個容器不實際上會使用;Azure 會使用從 Spring 開機應用程式的 hello 容器）。</span><span class="sxs-lookup"><span data-stu-id="848ee-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="848ee-148">e.</span><span class="sxs-lookup"><span data-stu-id="848ee-148">e.</span></span> <span data-ttu-id="848ee-149">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="848ee-149">Click **Save**.</span></span>

   ![應用程式設定][AZ07]

1. <span data-ttu-id="848ee-151">使用下列步驟的 hello 指定 FTP 的部署認證：</span><span class="sxs-lookup"><span data-stu-id="848ee-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="848ee-152">a.</span><span class="sxs-lookup"><span data-stu-id="848ee-152">a.</span></span> <span data-ttu-id="848ee-153">按一下 hello**部署認證**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="848ee-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="848ee-154">b.</span><span class="sxs-lookup"><span data-stu-id="848ee-154">b.</span></span> <span data-ttu-id="848ee-155">指定您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="848ee-155">Specify your username and password.</span></span>

   <span data-ttu-id="848ee-156">c.</span><span class="sxs-lookup"><span data-stu-id="848ee-156">c.</span></span> <span data-ttu-id="848ee-157">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="848ee-157">Click **Save**.</span></span>

   ![指定部署認證][AZ08]

1. <span data-ttu-id="848ee-159">使用下列步驟的 hello 擷取您的 FTP 連線資訊：</span><span class="sxs-lookup"><span data-stu-id="848ee-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="848ee-160">a.</span><span class="sxs-lookup"><span data-stu-id="848ee-160">a.</span></span> <span data-ttu-id="848ee-161">按一下 hello**部署認證**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="848ee-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="848ee-162">b.</span><span class="sxs-lookup"><span data-stu-id="848ee-162">b.</span></span> <span data-ttu-id="848ee-163">複製完整的 FTP 使用者名稱和 URL，並加以儲存供 hello 這個教學課程的下一節。</span><span class="sxs-lookup"><span data-stu-id="848ee-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![FTP URL 和認證][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="848ee-165">部署您 Spring 開機 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="848ee-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="848ee-166">hello 下列步驟將引導您完成 hello 步驟 toodeploy 您 Spring 開機 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="848ee-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="848ee-167">開啟 Windows [記事本] 之類的文字編輯器，貼上 hello 文字之後在新的文件，然後將 hello 檔案儲存為*web.config*:</span><span class="sxs-lookup"><span data-stu-id="848ee-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
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

1. <span data-ttu-id="848ee-168">在您儲存 hello 後*web.config*檔案 tooyour 系統，tooyour web 應用程式，透過使用 hello URL、 使用者名稱和密碼從 hello 前面一節，本教學課程的 FTP 連接。</span><span class="sxs-lookup"><span data-stu-id="848ee-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="848ee-169">例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="848ee-170">變更 hello 遠端目錄 toohello 根資料夾的 web 應用程式 (這是在*/站台/wwwroot*)，然後複製從 Spring 開機應用程式的 hello JAR 檔案，並 hello *web.config*前面。</span><span class="sxs-lookup"><span data-stu-id="848ee-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="848ee-171">例如：</span><span class="sxs-lookup"><span data-stu-id="848ee-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="848ee-172">部署您 JAR 之後和*web.config*檔案 tooyour web 應用程式，您需要 toorestart 使用 hello Azure 入口網站的 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="848ee-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="848ee-173">藉由瀏覽 tooyour web 應用程式的 URL，使用網頁瀏覽器，測試 hello web 應用程式，或使用類似下列範例，如果您有可用的 curl hello hello 語法：</span><span class="sxs-lookup"><span data-stu-id="848ee-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="848ee-174">您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**</span><span class="sxs-lookup"><span data-stu-id="848ee-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![瀏覽範例應用程式][SB02]

## <a name="next-steps"></a><span data-ttu-id="848ee-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="848ee-176">Next steps</span></span>

<span data-ttu-id="848ee-177">如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="848ee-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="848ee-178">在 hello Azure 容器服務中部署 Linux 上 Spring 開機應用程式</span><span class="sxs-lookup"><span data-stu-id="848ee-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="848ee-179">Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="848ee-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="848ee-180">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="848ee-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="848ee-181">如需使用 FTP depoying web 應用程式 tooAzure 的詳細資訊，請參閱[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure]。</span><span class="sxs-lookup"><span data-stu-id="848ee-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="848ee-182">如需 hello Spring 開機範例專案進一步詳細資訊，請參閱[Spring 開機入門]。</span><span class="sxs-lookup"><span data-stu-id="848ee-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="848ee-183">如需開始使用您自己 Spring 開機應用程式的說明，請參閱 hello **Spring Initializr** https://start.spring.io/ 在。</span><span class="sxs-lookup"><span data-stu-id="848ee-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="848ee-184">如需如何設定 Web 應用程式之其他設定的詳細資訊，請參閱[在 Azure App Service 中設定 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="848ee-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

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
