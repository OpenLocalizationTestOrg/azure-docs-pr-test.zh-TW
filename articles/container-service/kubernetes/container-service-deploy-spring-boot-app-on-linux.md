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
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="fe591-103">部署在 Linux 上 hello Azure 容器服務中的 Spring 開機應用程式</span><span class="sxs-lookup"><span data-stu-id="fe591-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="fe591-104">hello  **[Spring 架構]**是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="fe591-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="fe591-105">其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，其中提供簡單的方法建立獨立的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe591-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="fe591-106">**[Docker]**  hello 部署、 調整及管理的應用程式容器中執行的是可協助開發人員的開放原始碼解決方案自動化。</span><span class="sxs-lookup"><span data-stu-id="fe591-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="fe591-107">本教學課程將引導您完成使用 Docker toodevelop 和 Spring 開機應用程式 tooa Linux 中部署主機 hello [Azure 容器服務 (ACS)]。</span><span class="sxs-lookup"><span data-stu-id="fe591-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe591-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fe591-108">Prerequisites</span></span>

<span data-ttu-id="fe591-109">在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="fe591-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="fe591-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="fe591-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="fe591-111">hello [Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="fe591-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="fe591-112">最新的 [Java 開發工具組 (JDK)]。</span><span class="sxs-lookup"><span data-stu-id="fe591-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="fe591-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="fe591-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="fe591-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe591-114">A [Git] client.</span></span>
* <span data-ttu-id="fe591-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe591-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe591-116">Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="fe591-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="fe591-117">Docker 快速入門的 web 應用程式上建立 hello Spring 開機</span><span class="sxs-lookup"><span data-stu-id="fe591-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="fe591-118">hello 下列步驟引導您完成必要的 toocreate 簡單的 Spring 開機 web 應用程式並在本機測試 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="fe591-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="fe591-119">開啟命令提示字元，並建立本機目錄 toohold，您的應用程式，以及變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="fe591-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="fe591-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="fe591-121">複製 hello[上開始使用 Docker Spring 開機]範例專案到 hello 目錄，您所建立的; 例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="fe591-122">變更目錄已完成的 toohello 專案;例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="fe591-123">建置使用 Maven; hello JAR 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="fe591-124">一旦建立 hello web 應用程式之後，變更目錄 toohello`target`目錄 hello JAR 檔案所在的位置，並啟動 hello web 應用程式; 例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="fe591-125">藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe591-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="fe591-126">例如，如果您有 curl 可用而且設定 hello Tomcat 伺服器 toorun 連接埠 80 上：</span><span class="sxs-lookup"><span data-stu-id="fe591-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="fe591-127">您應該會看到下列訊息顯示 hello: **Docker 您好 ！**</span><span class="sxs-lookup"><span data-stu-id="fe591-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="fe591-129">建立 Azure 容器登錄中 toouse 為私用 Docker 登錄</span><span class="sxs-lookup"><span data-stu-id="fe591-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="fe591-130">hello 下列步驟引導您完成使用 hello Azure 入口網站 toocreate Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="fe591-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe591-131">如果您想 toouse hello Azure CLI 而不是 hello Azure 入口網站，請依照下列中的 hello 步驟[建立私用 Docker 容器登錄中使用 Azure CLI 2.0 hello](../../container-registry/container-registry-get-started-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fe591-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="fe591-132">瀏覽 toohello [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="fe591-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="fe591-133">一旦您已登入 tooyour hello Azure 入口網站上的帳戶，您可以依照 hello 中的 hello 步驟[建立私用 Docker 容器登錄中使用 Azure 入口網站 hello]發行項，這會在下列步驟 hello paraphrasedsake 直接。</span><span class="sxs-lookup"><span data-stu-id="fe591-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="fe591-134">按一下功能表圖示 hello **+ 新增**，然後按一下**容器**，然後按一下 **Azure 容器登錄中**。</span><span class="sxs-lookup"><span data-stu-id="fe591-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![建立新的 Azure Container Registry][AR01]

1. <span data-ttu-id="fe591-136">Hello hello Azure 容器登錄中的範本資訊] 頁面出現時，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="fe591-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![建立新的 Azure Container Registry][AR02]

1. <span data-ttu-id="fe591-138">當 hello**容器登錄中建立**會顯示頁面中，輸入您**登錄名稱**和**資源群組**，選擇**啟用**的hello **Admin 使用者**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="fe591-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![設定 Azure Container Registry 設定][AR03]

1. <span data-ttu-id="fe591-140">一旦建立容器登錄之後，瀏覽 tooyour 容器登錄中的 hello Azure 入口網站中，然後按一下**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="fe591-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="fe591-141">記下 hello 使用者名稱和密碼的 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="fe591-141">Take note of hello username and password for hello next steps.</span></span>

   ![Azure Container Registry 存取金鑰][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="fe591-143">設定 Maven toouse Azure 容器登錄中存取金鑰</span><span class="sxs-lookup"><span data-stu-id="fe591-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="fe591-144">瀏覽 toohello Maven 安裝的設定目錄，並開啟 hello *settings.xml*使用文字編輯器的檔案。</span><span class="sxs-lookup"><span data-stu-id="fe591-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="fe591-145">從這個教學課程 toohello hello 上一節中加入您 Azure 容器登錄中的存取設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="fe591-146">瀏覽 Spring 開機應用程式，完成 toohello 專案目錄 (例如:"*C:\SpringBoot\gs-spring-boot-docker\complete*「 或 」*/users/robert/SpringBoot/gs-spring-boot-docker /完成*")，並開啟 hello *pom.xml*使用文字編輯器的檔案。</span><span class="sxs-lookup"><span data-stu-id="fe591-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="fe591-147">更新 hello`<properties>`中 hello 集合*pom.xml*檔案 hello 登入伺服器的值具有 Azure 容器登錄 hello 前一節，本教學課程; 例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="fe591-148">更新 hello`<plugins>`中 hello 集合*pom.xml*檔案，因此，hello`<plugin>`包含 hello 登入伺服器位址和登錄名稱 Azure 容器登錄從 hello 本教學課程的上一節。</span><span class="sxs-lookup"><span data-stu-id="fe591-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="fe591-149">例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-149">For example:</span></span>

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

1. <span data-ttu-id="fe591-150">瀏覽 toohello 完成 Spring 開機應用程式的專案目錄並執行下列命令 toorebuild hello 應用程式的 hello 並推送 hello 容器 tooyour Azure 容器登錄中：</span><span class="sxs-lookup"><span data-stu-id="fe591-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="fe591-151">當您要推入您的 Docker 容器 tooAzure 時，您可能會收到類似 tooone hello 遵循即使已成功建立您的 Docker 容器的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="fe591-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="fe591-152">如果發生這種情況，您可能需要 toosign tooyour hello Docker 命令列工具，從 Azure 帳戶中例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="fe591-153">您接著可以從 hello 命令列; 推送您的容器例如：</span><span class="sxs-lookup"><span data-stu-id="fe591-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="fe591-154">使用您的容器映像在 Azure App Service 上建立 Linux 的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe591-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="fe591-155">瀏覽 toohello [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="fe591-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="fe591-156">按一下功能表圖示 hello **+ 新增**，然後按一下 **Web + 行動**，然後按一下 **Linux 上的 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fe591-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![在 hello Azure 入口網站中建立新的 web 應用程式][LX01]

1. <span data-ttu-id="fe591-158">當 hello **Linux 上的 Web 應用程式**會顯示頁面中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe591-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="fe591-159">a.</span><span class="sxs-lookup"><span data-stu-id="fe591-159">a.</span></span> <span data-ttu-id="fe591-160">輸入唯一的名稱，如 hello**應用程式名稱**; 例如:"*wingtiptoyslinux*。 」</span><span class="sxs-lookup"><span data-stu-id="fe591-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="fe591-161">b.</span><span class="sxs-lookup"><span data-stu-id="fe591-161">b.</span></span> <span data-ttu-id="fe591-162">選擇您**訂用帳戶**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="fe591-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="fe591-163">c.</span><span class="sxs-lookup"><span data-stu-id="fe591-163">c.</span></span> <span data-ttu-id="fe591-164">選擇現有**資源群組**，或指定名稱 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fe591-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="fe591-165">d.</span><span class="sxs-lookup"><span data-stu-id="fe591-165">d.</span></span> <span data-ttu-id="fe591-166">按一下**設定容器**並輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe591-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="fe591-167">選擇 [私人登錄]。</span><span class="sxs-lookup"><span data-stu-id="fe591-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="fe591-168">**映像和選擇性標記**：從先前指定的容器名稱，例如："wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest"</span><span class="sxs-lookup"><span data-stu-id="fe591-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="fe591-169">**伺服器 URL**：從先前指定的容器登錄 URL，例如："https://wingtiptoysregistry.azurecr.io"</span><span class="sxs-lookup"><span data-stu-id="fe591-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="fe591-170">**登入使用者名稱**和**密碼**：從您在先前步驟中使用的**存取金鑰**指定您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="fe591-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="fe591-171">e.</span><span class="sxs-lookup"><span data-stu-id="fe591-171">e.</span></span> <span data-ttu-id="fe591-172">一旦您輸入所有 hello 上述資訊，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="fe591-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![設定 Web 應用程式設定][LX02]

1. <span data-ttu-id="fe591-174">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fe591-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe591-175">Azure 會自動對應網際網路要求 tooembedded Tomcat 伺服器 hello 標準連接埠 80 或 8080 上執行。</span><span class="sxs-lookup"><span data-stu-id="fe591-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="fe591-176">不過，如果您設定您的內嵌的 Tomcat 伺服器 toorun 自訂連接埠時，您會需要 tooadd 定義內嵌的 Tomcat 伺服器 hello 連接埠的環境變數 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe591-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="fe591-177">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe591-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="fe591-178">瀏覽 toohello [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="fe591-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="fe591-179">按一下 hello 圖示**應用程式服務**。</span><span class="sxs-lookup"><span data-stu-id="fe591-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="fe591-180">（請參閱下面的 hello 影像中的項目 #1）。</span><span class="sxs-lookup"><span data-stu-id="fe591-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="fe591-181">Hello 清單中選取您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe591-181">Select your web app from hello list.</span></span> <span data-ttu-id="fe591-182">（項目 #2 在 hello 圖。）</span><span class="sxs-lookup"><span data-stu-id="fe591-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="fe591-183">按一下 [ **應用程式設定**]。</span><span class="sxs-lookup"><span data-stu-id="fe591-183">Click **Application Settings**.</span></span> <span data-ttu-id="fe591-184">（項目 #3 hello 圖中。）</span><span class="sxs-lookup"><span data-stu-id="fe591-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="fe591-185">在 hello**應用程式設定**區段中，加入新的環境變數，名為**連接埠**和 hello 值輸入自訂連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="fe591-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="fe591-186">（項目 #4 hello 圖中。）</span><span class="sxs-lookup"><span data-stu-id="fe591-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="fe591-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fe591-187">Click **Save**.</span></span> <span data-ttu-id="fe591-188">（項目 #5 hello 圖中。）</span><span class="sxs-lookup"><span data-stu-id="fe591-188">(Item #5 in hello image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="fe591-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe591-190">Next steps</span></span>

<span data-ttu-id="fe591-191">如需在 Azure 上使用 Spring 開機應用程式的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="fe591-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="fe591-192">部署 Spring 開機應用程式 toohello Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fe591-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="fe591-193">Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="fe591-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="fe591-194">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="fe591-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="fe591-195">如需 Docker 範例專案的 hello Spring 開機進一步詳細資訊，請參閱[上開始使用 Docker Spring 開機]。</span><span class="sxs-lookup"><span data-stu-id="fe591-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="fe591-196">如需開始使用您自己 Spring 開機應用程式的說明，請參閱 hello **Spring Initializr** https://start.spring.io/ 在。</span><span class="sxs-lookup"><span data-stu-id="fe591-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="fe591-197">如需開始使用建立簡單的 Spring 開機應用程式的詳細資訊，請參閱 < 在 https://start.spring.io/ hello Spring Initializr。</span><span class="sxs-lookup"><span data-stu-id="fe591-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="fe591-198">針對如何 toouse 自訂的 Docker 映像與 Azure 的其他範例，請參閱[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]。</span><span class="sxs-lookup"><span data-stu-id="fe591-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

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
