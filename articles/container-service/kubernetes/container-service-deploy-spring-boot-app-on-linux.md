---
title: "在 Azure Container Service 的 Linux 上部署 Spring Boot Web 應用程式 | Microsoft Docs"
description: "本教學課程會逐步引導您將 Spring Boot 應用程式部署為 Microsoft Azure 上之 Linux Web 應用程式的步驟。"
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
ms.openlocfilehash: 5f0b470bd46cfeaf00b3092dbe9db507ed50f622
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="1a609-103">將 Spring Boot 應用程式部署到 Azure Container Service 中的 Linux</span><span class="sxs-lookup"><span data-stu-id="1a609-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="1a609-104">**[Spring Framework]** 是一個開放原始碼解決方案，可協助 Java 開發人員建立企業級應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a609-104">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="1a609-105">[Spring Boot] 是建立在該平台基礎上更為熱門的專案之一，其中會提供用來建立獨立 Java 應用程式的簡化方法。</span><span class="sxs-lookup"><span data-stu-id="1a609-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="1a609-106">**[Docker]** 是開放原始碼解決方案，可協助開發人員自動化部署、調整及管理容器中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a609-106">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="1a609-107">本教學課程會逐步引導您使用 Docker 來開發 Spring Boot 應用程式，並且將其部署至 [Azure Container Service (ACS)] 中的 Linux 主機。</span><span class="sxs-lookup"><span data-stu-id="1a609-107">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a609-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1a609-108">Prerequisites</span></span>

<span data-ttu-id="1a609-109">若要完成本教學課程中的步驟，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="1a609-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="1a609-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1a609-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1a609-111">[Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="1a609-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="1a609-112">最新的 [Java 開發工具組 (JDK)]。</span><span class="sxs-lookup"><span data-stu-id="1a609-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="1a609-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="1a609-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="1a609-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1a609-114">A [Git] client.</span></span>
* <span data-ttu-id="1a609-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1a609-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1a609-116">由於本教學課程的虛擬化需求，您無法遵循本文中關於虛擬機器的步驟；您必須在啟用虛擬化功能的情況下使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="1a609-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="1a609-117">建立 Spring Boot on Docker Getting Started Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a609-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="1a609-118">下列步驟將引導您完成建立簡單 Spring Boot Web 應用程式，並在本機測試所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="1a609-118">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="1a609-119">開啟命令提示字元並建立本機目錄來保存您的應用程式，然後變更至該目錄；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="1a609-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="1a609-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="1a609-121">將 [Spring Boot on Docker Getting Started] 範例專案複製到您所建立的目錄中；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="1a609-122">將目錄變更至已完成的專案；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-122">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="1a609-123">使用 Maven 建立 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-123">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="1a609-124">建立 Web 應用程式之後，將目錄變更為 JAR 檔案所在的 `target` 目錄，並啟動 Web 應用程式；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-124">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="1a609-125">測試 Web 應用程式，方法是使用網頁瀏覽器在本機瀏覽它。</span><span class="sxs-lookup"><span data-stu-id="1a609-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="1a609-126">例如，如果您有 curl 可用，並將 Tomcat 伺服器設定為在連接埠 80 上執行：</span><span class="sxs-lookup"><span data-stu-id="1a609-126">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="1a609-127">您應該會看到顯示下列訊息：**Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="1a609-127">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="1a609-129">建立 Azure Container Registry 以用作私人 Docker 登錄</span><span class="sxs-lookup"><span data-stu-id="1a609-129">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="1a609-130">下列步驟會逐步引導您使用 Azure 入口網站來建立 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="1a609-130">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1a609-131">如果您想要使用 Azure CLI 而不是 Azure 入口網站，請遵循下列[使用 Azure CLI 2.0 建立私人 Docker 容器登錄](../../container-registry/container-registry-get-started-azure-cli.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="1a609-131">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="1a609-132">瀏覽至 [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="1a609-132">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="1a609-133">一旦您已在 Azure 入口網站登入您的帳戶後，就可以遵循[使用 Azure 入口網站建立私人 Docker 容器登錄]文章中的步驟，為便於了解，會在下列步驟中加以釋義。</span><span class="sxs-lookup"><span data-stu-id="1a609-133">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="1a609-134">依序按一下功能表的 [+ 新增] 圖示、[容器]，以及 [Azure Container Registry]。</span><span class="sxs-lookup"><span data-stu-id="1a609-134">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![建立新的 Azure Container Registry][AR01]

1. <span data-ttu-id="1a609-136">當 Azure Container Registry 範本的資訊頁面顯示時，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1a609-136">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![建立新的 Azure Container Registry][AR02]

1. <span data-ttu-id="1a609-138">當 [建立容器登錄] 頁面顯示時，輸入您的 [登錄名稱] 和 [資源群組]，針對 [管理使用者] 選擇 [啟用]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1a609-138">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![設定 Azure Container Registry 設定][AR03]

1. <span data-ttu-id="1a609-140">一旦建立容器登錄之後，瀏覽至 Azure 入口網站中的容器登錄，然後按一下 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="1a609-140">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="1a609-141">將後續步驟的使用者名稱和密碼記下。</span><span class="sxs-lookup"><span data-stu-id="1a609-141">Take note of the username and password for the next steps.</span></span>

   ![Azure Container Registry 存取金鑰][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="1a609-143">設定要使用 Azure Container Registry 存取金鑰的 Maven</span><span class="sxs-lookup"><span data-stu-id="1a609-143">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="1a609-144">瀏覽至您 Maven 安裝的設定目錄，並使用文字編輯器開啟 settings.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="1a609-144">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="1a609-145">將本教學課程上一節的 Azure Container Registry 存取設定新增至 settings.xml 檔案中的 `<servers>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-145">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="1a609-146">瀏覽至 Spring Boot 應用程式已完成的專案目錄 (例如，"*C:\SpringBoot\gs-spring-boot-docker\complete*" 或 "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*")，並使用文字編輯器開啟 *pom.xml* 檔案。</span><span class="sxs-lookup"><span data-stu-id="1a609-146">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="1a609-147">使用本教學課程上一節的 Azure Container Registry 登入伺服器值來更新 pom.xml 檔案中的 `<properties>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-147">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="1a609-148">更新 pom.xml 檔案中的 `<plugins>` 集合，以便 `<plugin>` 可包含本教學課程上一節的登入伺服器位址和 Azure Container Registry 的登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="1a609-148">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="1a609-149">例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-149">For example:</span></span>

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

1. <span data-ttu-id="1a609-150">瀏覽至您 Spring Boot 應用程式的已完成專案目錄，然後執行下列命令來重建應用程式，並將容器推送到您的 Azure Container Registry：</span><span class="sxs-lookup"><span data-stu-id="1a609-150">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="1a609-151">當您要將 Docker 容器推送至 Azure 時，可能會收到類似下列其中一項的錯誤訊息，即使已成功建立 Docker 容器也一樣：</span><span class="sxs-lookup"><span data-stu-id="1a609-151">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="1a609-152">如果發生這種情況，您可能需要從 Docker 命令列登入 Azure 帳戶；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-152">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="1a609-153">接著，您可以從命令列推送您的容器；例如：</span><span class="sxs-lookup"><span data-stu-id="1a609-153">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="1a609-154">使用您的容器映像在 Azure App Service 上建立 Linux 的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a609-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="1a609-155">瀏覽至 [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="1a609-155">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="1a609-156">依序按一下功能表的 [+ 新增] 圖示、[Web + 行動]，以及 [Linux 上的 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1a609-156">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![在 Azure 入口網站中建立新的 Web 應用程式][LX01]

1. <span data-ttu-id="1a609-158">當 [Linux 上的 Web 應用程式] 頁面顯示時，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1a609-158">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="1a609-159">a.</span><span class="sxs-lookup"><span data-stu-id="1a609-159">a.</span></span> <span data-ttu-id="1a609-160">為 [應用程式名稱] 輸入唯一名稱；例如："wingtiptoyslinux"。</span><span class="sxs-lookup"><span data-stu-id="1a609-160">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="1a609-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a609-161">b.</span></span> <span data-ttu-id="1a609-162">從下拉式清單選擇 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1a609-162">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="1a609-163">c.</span><span class="sxs-lookup"><span data-stu-id="1a609-163">c.</span></span> <span data-ttu-id="1a609-164">選擇現有 [資源群組]，或指定名稱以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a609-164">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="1a609-165">d.</span><span class="sxs-lookup"><span data-stu-id="1a609-165">d.</span></span> <span data-ttu-id="1a609-166">按一下 [設定容器]，並輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1a609-166">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="1a609-167">選擇 [私人登錄]。</span><span class="sxs-lookup"><span data-stu-id="1a609-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="1a609-168">**映像和選擇性標記**：從先前指定的容器名稱，例如："wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest"</span><span class="sxs-lookup"><span data-stu-id="1a609-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="1a609-169">**伺服器 URL**：從先前指定的容器登錄 URL，例如："https://wingtiptoysregistry.azurecr.io"</span><span class="sxs-lookup"><span data-stu-id="1a609-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="1a609-170">**登入使用者名稱**和**密碼**：從您在先前步驟中使用的**存取金鑰**指定您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="1a609-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="1a609-171">e.</span><span class="sxs-lookup"><span data-stu-id="1a609-171">e.</span></span> <span data-ttu-id="1a609-172">一旦您輸入上述所有資訊後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1a609-172">Once you have entered all of the above information, click **OK**.</span></span>

   ![設定 Web 應用程式設定][LX02]

1. <span data-ttu-id="1a609-174">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1a609-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1a609-175">Azure 會自動將網際網路要求對應到標準連接埠 80 或 8080 上執行的內嵌 Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a609-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="1a609-176">不過，如果您將內嵌 Tomcat 伺服器設定為在自訂連接埠上執行時，則必須將環境變數新增至您的 web 應用程式，其可定義內嵌 Tomcat 伺服器的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1a609-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="1a609-177">若要這樣做，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1a609-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="1a609-178">瀏覽至 [Azure 入口網站]並登入。</span><span class="sxs-lookup"><span data-stu-id="1a609-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="1a609-179">按一下 [應用程式服務] 的圖示。</span><span class="sxs-lookup"><span data-stu-id="1a609-179">Click the icon for **App Services**.</span></span> <span data-ttu-id="1a609-180">(請參閱下列映像中的項目 #1。)</span><span class="sxs-lookup"><span data-stu-id="1a609-180">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="1a609-181">從清單中選取 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a609-181">Select your web app from the list.</span></span> <span data-ttu-id="1a609-182">(下列映像中的項目 #2。)</span><span class="sxs-lookup"><span data-stu-id="1a609-182">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="1a609-183">按一下 [ **應用程式設定**]。</span><span class="sxs-lookup"><span data-stu-id="1a609-183">Click **Application Settings**.</span></span> <span data-ttu-id="1a609-184">(下列映像中的項目 #3。)</span><span class="sxs-lookup"><span data-stu-id="1a609-184">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="1a609-185">在 [應用程式設定] 區段中，新增名為 **PORT** 的新環境變數，並輸入值的自訂連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="1a609-185">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="1a609-186">(下列映像中的項目 #4。)</span><span class="sxs-lookup"><span data-stu-id="1a609-186">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="1a609-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1a609-187">Click **Save**.</span></span> <span data-ttu-id="1a609-188">(下列映像中的項目 #5。)</span><span class="sxs-lookup"><span data-stu-id="1a609-188">(Item #5 in the image below.)</span></span>
>
> ![在 Azure 入口網站中儲存自訂連接埠號碼][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="1a609-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a609-190">Next steps</span></span>

<span data-ttu-id="1a609-191">如需在 Azure 上使用 Spring Boot 應用程式的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="1a609-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="1a609-192">將 Spring Boot 應用程式部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1a609-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="1a609-193">將 Spring Boot 應用程式部署到 Azure Container Service 中的 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="1a609-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="1a609-194">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="1a609-194">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="1a609-195">如需 Spring Boot on Docker 範例專案的進一步詳細資訊，請參閱 [Spring Boot on Docker Getting Started]。</span><span class="sxs-lookup"><span data-stu-id="1a609-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="1a609-196">如需開始使用您自己的 Spring Boot 應用程式的說明，請參閱 **Spring Initializr** (網址為 https://start.spring.io/)。</span><span class="sxs-lookup"><span data-stu-id="1a609-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="1a609-197">如需開始建立簡單 Spring Boot 應用程式的相關詳細資訊，請參閱 Spring Initializr (網址為 https://start.spring.io/)。</span><span class="sxs-lookup"><span data-stu-id="1a609-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="1a609-198">如需如何搭配 Azure 使用自訂 Docker 映像的其他範例，請參閱[針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像]。</span><span class="sxs-lookup"><span data-stu-id="1a609-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="1a609-199">[Azure 命令列介面 (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="1a609-199">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="1a609-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="1a609-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="1a609-201">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="1a609-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="1a609-202">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="1a609-202">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="1a609-203">[使用 Azure 入口網站建立私人 Docker 容器登錄]: /azure/container-registry/container-registry-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="1a609-203">[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal</span></span>
<span data-ttu-id="1a609-204">[針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="1a609-204">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="1a609-205">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="1a609-205">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="1a609-206">[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="1a609-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="1a609-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="1a609-207">[Git]: https://github.com/</span></span>
<span data-ttu-id="1a609-208">[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="1a609-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="1a609-209">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="1a609-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="1a609-210">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="1a609-210">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="1a609-211">[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="1a609-211">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="1a609-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="1a609-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="1a609-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="1a609-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="1a609-214">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="1a609-214">[Spring Framework]: https://spring.io/</span></span>

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
