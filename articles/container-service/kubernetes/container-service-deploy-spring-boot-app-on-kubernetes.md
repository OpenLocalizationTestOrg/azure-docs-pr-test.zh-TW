---
title: "在 Azure Container Service 的 Kubernetes 上部署 Spring Boot 應用程式 | Microsoft Docs"
description: "本教學課程會逐步引導您將 Spring Boot 應用程式部署為 Microsoft Azure 上之 Kubernetes 叢集的步驟。"
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
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="3b4f2-103">將 Spring Boot 應用程式部署到 Azure Container Service 中的 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="3b4f2-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="3b4f2-104">**[Spring 架構]**是受歡迎的開放原始碼架構，可協助 Java 開發人員建立 Web、行動及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="3b4f2-105">本教學課程使用以 [Spring Boot] 建立的範例應用程式，這是快速開始使用 Spring 的慣例方法。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="3b4f2-106">**[Kubernetes]** 和 **[Docker]** 是開放原始碼解決方案，可協助開發人員自動化部署、調整及管理在容器中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="3b4f2-107">本教學課程會逐步引導您結合這兩項受歡迎的開放原始碼技術，以開發 Spring Boot 應用程式並把它部署到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="3b4f2-108">更具體來說，您使用 *[Spring Boot]* 開發應用程式、用 *[Kubernetes]* 部署容器，以及用 [Azure Container Service (ACS)] 裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b4f2-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b4f2-109">Prerequisites</span></span>

* <span data-ttu-id="3b4f2-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3b4f2-111">[Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3b4f2-112">最新的 [Java 開發工具組 (JDK)]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="3b4f2-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3b4f2-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-114">A [Git] client.</span></span>
* <span data-ttu-id="3b4f2-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3b4f2-116">由於本教學課程的虛擬化需求，您無法遵循本文中關於虛擬機器的步驟；您必須在啟用虛擬化功能的情況下使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="3b4f2-117">建立 Spring Boot on Docker Getting Started Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3b4f2-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="3b4f2-118">下列步驟會引導您建置 Spring Boot Web 應用程式，並在本機加以測試。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="3b4f2-119">開啟命令提示字元並建立本機目錄來保存您的應用程式，然後變更至該目錄；例如：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3b4f2-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="3b4f2-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3b4f2-121">將 [Spring Boot on Docker Getting Started] 範例專案複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="3b4f2-122">將目錄變更至已完成的專案。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="3b4f2-123">使用 Maven 來建置及執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="3b4f2-124">瀏覽至 http://localhost:8080 來測試 Web 應用程式，或使用下列 `curl` 命令：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3b4f2-125">您應該會看到顯示下列訊息：**Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="3b4f2-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="3b4f2-127">使用 Azure CLI 建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3b4f2-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="3b4f2-128">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-128">Open a command prompt.</span></span>

1. <span data-ttu-id="3b4f2-129">登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="3b4f2-130">為此教學課程中使用的 Azure 資源建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="3b4f2-131">在資源群組中建立私用的 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="3b4f2-132">本教學課程會在稍後的步驟中，將範例應用程式推送為此登錄的 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="3b4f2-133">以登錄的唯一名稱取代 `wingtiptoysregistry`。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="3b4f2-134">將應用程式推送至容器登錄</span><span class="sxs-lookup"><span data-stu-id="3b4f2-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="3b4f2-135">巡覽至您 Maven 安裝的設定目錄 (預設為 ~/.m2/ 或 C:\Users\使用者名稱\.m2)，並使用文字編輯器開啟 *settings.xml* 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="3b4f2-136">從 Azure CLI 擷取容器登錄的密碼。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="3b4f2-137">將您的 Azure Container Registry 識別碼和密碼新增至 *settings.xml* 檔案的新 `<server>` 集合中。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="3b4f2-138">`id` 和 `username` 是登錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="3b4f2-139">使用上一個命令的 `password` 值 (不含引號)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="3b4f2-140">巡覽至 Spring Boot 應用程式已完成的專案目錄 (例如，"*C:\SpringBoot\gs-spring-boot-docker\complete*" 或 "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*")，並使用文字編輯器開啟 *pom.xml* 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="3b4f2-141">使用 Azure Container Registry 的登入伺服器值來更新 *pom.xml* 檔案中的 `<properties>` 集合。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="3b4f2-142">更新 *pom.xml* 檔案中的 `<plugins>` 集合，以便 `<plugin>` 包含 Azure Container Registry 的登入伺服器位址和登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="3b4f2-143">巡覽至 Spring Boot 應用程式已完成的專案目錄，然後執行下列命令來建置 Docker 容器，並將映像推送到登錄：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="3b4f2-144">當 Maven 將映像推送至 Azure 時，您可能會收到與下列其中之一相似的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="3b4f2-145">如果發生此錯誤，請從 Docker 命令列登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="3b4f2-146">然後推送您的容器：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="3b4f2-147">使用 Azure CLI 在 ACS 上建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="3b4f2-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="3b4f2-148">在 Azure Container Service 中建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="3b4f2-149">下列命令會在 *wingtiptoys-kubernetes* 資源群組中建立*kubernetes* 叢集，以 *wingtiptoys-containerservice* 為叢集名稱，*wingtiptoys-kubernetes* 為 DNS 前置詞：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="3b4f2-150">此命令可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="3b4f2-151">使用 Azure CLI 安裝 `kubectl`。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="3b4f2-152">Linux 使用者在此命令前可能要加上 `sudo`，因為它會將 Kubernetes CLI 部署到 `/usr/local/bin`。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="3b4f2-153">下載叢集設定資訊，以便從 Kubernetes Web 介面和 `kubectl` 管理您的叢集。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="3b4f2-154">部署 Kubernetes 叢集的映像</span><span class="sxs-lookup"><span data-stu-id="3b4f2-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="3b4f2-155">本教學課程使用 `kubectl` 部署應用程式，然後讓您透過 Kubernetes web 介面瀏覽部署。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="3b4f2-156">使用 Kubernetes Web 介面部署</span><span class="sxs-lookup"><span data-stu-id="3b4f2-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="3b4f2-157">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-157">Open a command prompt.</span></span>

1. <span data-ttu-id="3b4f2-158">在預設瀏覽器中開啟 Kubernetes 叢集的設定網站：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="3b4f2-159">當 Kubernetes 設定網站在您的瀏覽器中開啟時，請按一下連結以**部署容器化應用程式**：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes 設定網站][KB01]

1. <span data-ttu-id="3b4f2-161">當 [Deploy a containerized app] (部署容器化應用程式) 頁面出現時，請指定下列選項：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="3b4f2-162">a.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-162">a.</span></span> <span data-ttu-id="3b4f2-163">選取 [Specify app details below] (指定以下的應用程式詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="3b4f2-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-164">b.</span></span> <span data-ttu-id="3b4f2-165">在 [應用程式名稱] 中輸入您的 Spring Boot 應用程式名稱，例如："*gs-spring-boot-docker*"。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="3b4f2-166">c.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-166">c.</span></span> <span data-ttu-id="3b4f2-167">在 [容器映像] 中輸入先前的登入伺服器和容器映像，例如："*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="3b4f2-168">d.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-168">d.</span></span> <span data-ttu-id="3b4f2-169">針對 [服務] 選擇 [外部]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="3b4f2-170">e.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-170">e.</span></span> <span data-ttu-id="3b4f2-171">在 [連接埠] 和 [目標連接埠] 文字方塊中指定您的外部和內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes 設定網站][KB02]


1. <span data-ttu-id="3b4f2-173">按一下 [部署] 來部署容器。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-173">Click **Deploy** to deploy the container.</span></span>

   ![部署容器][KB05]

1. <span data-ttu-id="3b4f2-175">應用程式一經部署，您就會看到 [服務] 底下列出您的 Spring Boot 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes 服務][KB06]

1. <span data-ttu-id="3b4f2-177">如果按一下**外部端點**連結，您會看到您的 Spring Boot 應用程式在 Azure 上執行。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes 服務][KB07]

   ![在 Azure 上瀏覽範例應用程式][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="3b4f2-180">使用 kubectl 部署</span><span class="sxs-lookup"><span data-stu-id="3b4f2-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="3b4f2-181">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-181">Open a command prompt.</span></span>

1. <span data-ttu-id="3b4f2-182">使用 `kubectl run` 命令在 Kubernetes 叢集中執行容器。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="3b4f2-183">為您在 Kubernetes 中的應用程式提供服務名稱和完整的映像名稱。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="3b4f2-184">例如：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="3b4f2-185">在這個命令中：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-185">In this command:</span></span>

   * <span data-ttu-id="3b4f2-186">容器名稱 `gs-spring-boot-docker` 直接指定在 `run` 命令後面</span><span class="sxs-lookup"><span data-stu-id="3b4f2-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="3b4f2-187">`--image` 參數指定合併的登入伺服器和映像名稱為 `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="3b4f2-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="3b4f2-188">使用 `kubectl expose` 命令向外部公開您的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="3b4f2-189">指定您的服務名稱、用來存取應用程式的公開 TCP 通訊埠，以及應用程式接聽的內部目標連接埠。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="3b4f2-190">例如：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="3b4f2-191">在這個命令中：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-191">In this command:</span></span>

   * <span data-ttu-id="3b4f2-192">容器名稱 `gs-spring-boot-docker` 直接指定在 `expose deployment` 命令後面</span><span class="sxs-lookup"><span data-stu-id="3b4f2-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="3b4f2-193">`--type` 參數指定叢集使用負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3b4f2-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="3b4f2-194">`--port` 參數指定公開的 TCP 通訊埠 80。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="3b4f2-195">您會在此連接埠存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-195">You access the app on this port.</span></span>

   * <span data-ttu-id="3b4f2-196">`--target-port` 參數指定內部 TCP 通訊埠 8080。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="3b4f2-197">負載平衡器會在此連接埠上將要求轉送到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="3b4f2-198">一旦應用程式部署至叢集，請查詢外部 IP 位址，並在網頁瀏覽器中開啟它：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![在 Azure 上瀏覽範例應用程式][SB02]


## <a name="next-steps"></a><span data-ttu-id="3b4f2-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b4f2-200">Next steps</span></span>

<span data-ttu-id="3b4f2-201">如需在 Azure 上使用 Spring Boot 的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="3b4f2-202">將 Spring Boot 應用程式部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3b4f2-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="3b4f2-203">將 Spring Boot 應用程式部署到 Azure Container Service 中的 Linux</span><span class="sxs-lookup"><span data-stu-id="3b4f2-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="3b4f2-204">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="3b4f2-205">如需 Spring Boot on Docker 範例專案的詳細資訊，請參閱 [Spring Boot on Docker Getting Started]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="3b4f2-206">下列連結提供建立 Spring Boot 應用程式的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="3b4f2-207">如需建立簡易 Spring Boot 應用程式的詳細資訊，請參閱 Spring Initializr (網址為 https://start.spring.io/)。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="3b4f2-208">下列連結提供以 Azure 使用 Kubernetes 的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="3b4f2-209">在 Container Service 中開始使用 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="3b4f2-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="3b4f2-210">使用 Kubernetes Web UI 和 Azure Container Service </span><span class="sxs-lookup"><span data-stu-id="3b4f2-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="3b4f2-211">使用 Kubernetes 命令列介面的詳細資訊，請參閱 **kubectl** 使用者指南，網址為 <https://kubernetes.io/docs/user-guide/kubectl/>。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="3b4f2-212">Kubernetes 網站有幾篇文章討論在私用登錄中使用映像：</span><span class="sxs-lookup"><span data-stu-id="3b4f2-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="3b4f2-213">[設定 Pod 的服務帳戶]</span><span class="sxs-lookup"><span data-stu-id="3b4f2-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="3b4f2-214">[命名空間]</span><span class="sxs-lookup"><span data-stu-id="3b4f2-214">[Namespaces]</span></span>
* <span data-ttu-id="3b4f2-215">[從私用登錄提取映像]</span><span class="sxs-lookup"><span data-stu-id="3b4f2-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="3b4f2-216">如需如何以 Azure 使用自訂 Docker 映像的其他範例，請參閱[針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像]。</span><span class="sxs-lookup"><span data-stu-id="3b4f2-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="3b4f2-217">[Azure 命令列介面 (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="3b4f2-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="3b4f2-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="3b4f2-219">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="3b4f2-220">[針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="3b4f2-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="3b4f2-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="3b4f2-222">[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="3b4f2-223">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="3b4f2-224">[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="3b4f2-225">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="3b4f2-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="3b4f2-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="3b4f2-228">[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="3b4f2-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="3b4f2-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="3b4f2-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="3b4f2-231">[Spring 架構]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="3b4f2-232">[設定 Pod 的服務帳戶]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="3b4f2-233">[命名空間]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="3b4f2-234">[從私用登錄提取映像]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span><span class="sxs-lookup"><span data-stu-id="3b4f2-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
