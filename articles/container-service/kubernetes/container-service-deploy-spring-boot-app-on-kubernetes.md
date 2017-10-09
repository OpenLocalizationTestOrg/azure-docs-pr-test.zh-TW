---
title: "aaaDeploy 上 Azure 容器服務中 Kubernetes Spring 開機應用程式 |Microsoft 文件"
description: "本教學課程將逐步引導您透過 hello 步驟 toodeploy Spring 開機應用程式在 Kubernetes 叢集中在 Microsoft Azure 上。"
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="61c21-103">Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="61c21-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="61c21-104">hello  **[Spring 架構]**是熱門的開放原始碼架構，可協助建立 web、 行動裝置版及 API 應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="61c21-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="61c21-105">本教學課程使用範例應用程式使用建立[Spring 開機]，慣例導向的方式使用 Spring tooget 快速入門。</span><span class="sxs-lookup"><span data-stu-id="61c21-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="61c21-106">**[Kubernetes]** 和 **[Docker]**  hello 部署、 調整及管理的應用程式執行的是協助開發人員的開放原始碼解決方案自動化在容器中。</span><span class="sxs-lookup"><span data-stu-id="61c21-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="61c21-107">本教學課程會逐步引導您雖然結合這些兩個常用、 開放原始碼技術，toodevelop 和部署 Spring 開機應用程式 tooMicrosoft Azure。</span><span class="sxs-lookup"><span data-stu-id="61c21-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="61c21-108">更具體來說，您使用 *[Spring 開機]*應用程式開發 *[Kubernetes]* 容器部署和 hello[Azure 容器服務 (ACS)] toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="61c21-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="61c21-109">Prerequisites</span></span>

* <span data-ttu-id="61c21-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="61c21-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="61c21-111">hello [Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="61c21-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="61c21-112">最新的 [Java 開發工具組 (JDK)]。</span><span class="sxs-lookup"><span data-stu-id="61c21-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="61c21-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="61c21-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="61c21-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="61c21-114">A [Git] client.</span></span>
* <span data-ttu-id="61c21-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="61c21-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="61c21-116">Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="61c21-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="61c21-117">Docker 快速入門的 web 應用程式上建立 hello Spring 開機</span><span class="sxs-lookup"><span data-stu-id="61c21-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="61c21-118">hello 步驟會逐步引導您建置 Spring 開機 web 應用程式，並在本機加以測試。</span><span class="sxs-lookup"><span data-stu-id="61c21-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="61c21-119">開啟命令提示字元，並建立本機目錄 toohold，您的應用程式，以及變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="61c21-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="61c21-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="61c21-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="61c21-121">複製 hello[上開始使用 Docker Spring 開機]到 hello 目錄中的範例專案。</span><span class="sxs-lookup"><span data-stu-id="61c21-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="61c21-122">變更目錄已完成的 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="61c21-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="61c21-123">使用 Maven toobuild 和執行的 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="61c21-124">測試 hello web 應用程式瀏覽 toohttp://localhost:8080，或與 hello 下列`curl`命令：</span><span class="sxs-lookup"><span data-stu-id="61c21-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="61c21-125">您應該會看到下列訊息顯示 hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="61c21-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="61c21-127">建立 Azure 容器登錄中使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="61c21-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="61c21-128">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="61c21-128">Open a command prompt.</span></span>

1. <span data-ttu-id="61c21-129">Azure 帳戶登入 tooyour 中：</span><span class="sxs-lookup"><span data-stu-id="61c21-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="61c21-130">本教學課程中所使用的 Azure 資源建立 hello 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="61c21-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="61c21-131">Hello 資源群組中建立私人 Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="61c21-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="61c21-132">hello 教學課程將為 Docker 映像 toothis 登錄在稍後步驟中，推入 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="61c21-133">以登錄的唯一名稱取代 `wingtiptoysregistry`。</span><span class="sxs-lookup"><span data-stu-id="61c21-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="61c21-134">推送您的應用程式 toohello 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="61c21-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="61c21-135">瀏覽 toohello Maven 安裝的設定目錄 (預設 ~/.m2/ 或 C:\Users\username\.m2) 並開啟 hello *settings.xml*使用文字編輯器的檔案。</span><span class="sxs-lookup"><span data-stu-id="61c21-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="61c21-136">擷取 hello Azure CLI hello 容器登錄中您的密碼。</span><span class="sxs-lookup"><span data-stu-id="61c21-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="61c21-137">加入您 Azure 容器登錄 id 和密碼 tooa 新`<server>`中 hello 集合*settings.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="61c21-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="61c21-138">hello`id`和`username`hello hello 登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="61c21-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="61c21-139">使用 hello `password` hello 前一個命令 （不含引號） 的值。</span><span class="sxs-lookup"><span data-stu-id="61c21-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="61c21-140">瀏覽 toohello 完成 Spring 開機應用程式的專案目錄 (例如，"*C:\SpringBoot\gs-spring-boot-docker\complete*「 或 」*/users/robert/SpringBoot/gs-spring-boot-docker /完成*")，並開啟 hello *pom.xml*使用文字編輯器的檔案。</span><span class="sxs-lookup"><span data-stu-id="61c21-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="61c21-141">更新 hello`<properties>`中 hello 集合*pom.xml* Azure 容器登錄檔案具有 hello 登入伺服器的值。</span><span class="sxs-lookup"><span data-stu-id="61c21-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="61c21-142">更新 hello`<plugins>`中 hello 集合*pom.xml*檔案，因此，hello`<plugin>`包含 hello 登入伺服器位址和登錄名稱 Azure 容器登錄。</span><span class="sxs-lookup"><span data-stu-id="61c21-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="61c21-143">瀏覽 toohello 完成 Spring 開機應用程式的專案目錄，然後執行下列命令 toobuild hello Docker 容器和推播 hello 映像 toohello 登錄 hello:</span><span class="sxs-lookup"><span data-stu-id="61c21-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="61c21-144">您可能會收到錯誤訊息，Maven 推播通知 hello 映像 tooAzure 時會 hello 以下的類似 tooone:</span><span class="sxs-lookup"><span data-stu-id="61c21-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="61c21-145">如果您收到這個錯誤，請登入 tooAzure 從 hello Docker 命令列。</span><span class="sxs-lookup"><span data-stu-id="61c21-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="61c21-146">然後推送您的容器：</span><span class="sxs-lookup"><span data-stu-id="61c21-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="61c21-147">使用 Azure CLI hello ACS 上建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="61c21-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="61c21-148">在 Azure Container Service 中建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="61c21-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="61c21-149">hello 下列命令會建立*kubernetes*叢集中 hello *wingtiptoys kubernetes*資源群組，以及*wingtiptoys containerservice*為 hello 叢集名稱，和*wingtiptoys kubernetes* hello DNS 前置詞為：</span><span class="sxs-lookup"><span data-stu-id="61c21-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="61c21-150">此命令可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="61c21-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="61c21-151">安裝`kubectl`使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="61c21-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="61c21-152">Linux 使用者與此命令時可能有 tooprefix`sudo`因為它太部署 hello Kubernetes CLI`/usr/local/bin`。</span><span class="sxs-lookup"><span data-stu-id="61c21-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="61c21-153">下載 hello 叢集組態資訊，因此您可以從 hello Kubernetes web 介面來管理您的叢集和`kubectl`。</span><span class="sxs-lookup"><span data-stu-id="61c21-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="61c21-154">部署 hello 映像 tooyour Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="61c21-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="61c21-155">本教學課程部署 hello 的應用程式使用`kubectl`，然後允許您 tooexplore hello 部署透過 hello Kubernetes web 介面。</span><span class="sxs-lookup"><span data-stu-id="61c21-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="61c21-156">部署與 hello Kubernetes web 介面</span><span class="sxs-lookup"><span data-stu-id="61c21-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="61c21-157">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="61c21-157">Open a command prompt.</span></span>

1. <span data-ttu-id="61c21-158">在預設瀏覽器中開啟 hello 組態網站 Kubernetes 叢集：</span><span class="sxs-lookup"><span data-stu-id="61c21-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="61c21-159">Hello Kubernetes 組態網站開啟時瀏覽器中，按一下 hello 連結太**容器化應用程式部署**:</span><span class="sxs-lookup"><span data-stu-id="61c21-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Kubernetes 設定網站][KB01]

1. <span data-ttu-id="61c21-161">當 hello**容器化應用程式部署**會顯示頁面，指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="61c21-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="61c21-162">a.</span><span class="sxs-lookup"><span data-stu-id="61c21-162">a.</span></span> <span data-ttu-id="61c21-163">選取 [Specify app details below] (指定以下的應用程式詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="61c21-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="61c21-164">b.</span><span class="sxs-lookup"><span data-stu-id="61c21-164">b.</span></span> <span data-ttu-id="61c21-165">輸入您的 Spring 開機應用程式名稱，以 hello**應用程式名稱**; 例如:"*gs spring 開機-docker*"。</span><span class="sxs-lookup"><span data-stu-id="61c21-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="61c21-166">c.</span><span class="sxs-lookup"><span data-stu-id="61c21-166">c.</span></span> <span data-ttu-id="61c21-167">從您登入伺服器和容器映像輸入稍早 hello**容器映像**; 例如:"*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"。</span><span class="sxs-lookup"><span data-stu-id="61c21-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="61c21-168">d.</span><span class="sxs-lookup"><span data-stu-id="61c21-168">d.</span></span> <span data-ttu-id="61c21-169">選擇**外部**hello**服務**。</span><span class="sxs-lookup"><span data-stu-id="61c21-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="61c21-170">e.</span><span class="sxs-lookup"><span data-stu-id="61c21-170">e.</span></span> <span data-ttu-id="61c21-171">指定您的外部和內部連接埠在 hello**連接埠**和**目標連接埠**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="61c21-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes 設定網站][KB02]


1. <span data-ttu-id="61c21-173">按一下**部署**toodeploy hello 容器。</span><span class="sxs-lookup"><span data-stu-id="61c21-173">Click **Deploy** toodeploy hello container.</span></span>

   ![部署容器][KB05]

1. <span data-ttu-id="61c21-175">應用程式一經部署，您就會看到 [服務] 底下列出您的 Spring Boot 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes 服務][KB06]

1. <span data-ttu-id="61c21-177">如果您按一下 hello 連結**外部端點**，您可以看到您在 Azure 上執行的 Spring 開機應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes 服務][KB07]

   ![在 Azure 上瀏覽範例應用程式][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="61c21-180">使用 kubectl 部署</span><span class="sxs-lookup"><span data-stu-id="61c21-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="61c21-181">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="61c21-181">Open a command prompt.</span></span>

1. <span data-ttu-id="61c21-182">在 hello Kubernetes 叢集中執行您的容器，使用 hello`kubectl run`命令。</span><span class="sxs-lookup"><span data-stu-id="61c21-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="61c21-183">可讓您的應用程式中 Kubernetes 的服務名稱和 hello 完整的映像名稱。</span><span class="sxs-lookup"><span data-stu-id="61c21-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="61c21-184">例如：</span><span class="sxs-lookup"><span data-stu-id="61c21-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="61c21-185">在這個命令中：</span><span class="sxs-lookup"><span data-stu-id="61c21-185">In this command:</span></span>

   * <span data-ttu-id="61c21-186">hello 容器名稱`gs-spring-boot-docker`指定 hello 之後立即`run`命令</span><span class="sxs-lookup"><span data-stu-id="61c21-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="61c21-187">hello`--image`參數會指定 hello 結合登入伺服器，做為映像名稱`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="61c21-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="61c21-188">公開外部使用 hello Kubernetes 叢集`kubectl expose`命令。</span><span class="sxs-lookup"><span data-stu-id="61c21-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="61c21-189">指定服務名稱、 hello 公開 TCP 使用連接埠 tooaccess hello 應用程式和您的應用程式所接聽的 hello 內部目標連接埠。</span><span class="sxs-lookup"><span data-stu-id="61c21-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="61c21-190">例如：</span><span class="sxs-lookup"><span data-stu-id="61c21-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="61c21-191">在這個命令中：</span><span class="sxs-lookup"><span data-stu-id="61c21-191">In this command:</span></span>

   * <span data-ttu-id="61c21-192">hello 容器名稱`gs-spring-boot-docker`指定 hello 之後立即`expose deployment`命令</span><span class="sxs-lookup"><span data-stu-id="61c21-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="61c21-193">hello`--type`參數指定該 hello 叢集會使用負載平衡器</span><span class="sxs-lookup"><span data-stu-id="61c21-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="61c21-194">hello`--port`參數會指定 hello 公開 TCP 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="61c21-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="61c21-195">您存取在此連接埠的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61c21-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="61c21-196">hello`--target-port`參數會指定 hello 內部 TCP 連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="61c21-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="61c21-197">hello 負載平衡器會將轉送要求 tooyour 應用程式在此連接埠。</span><span class="sxs-lookup"><span data-stu-id="61c21-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="61c21-198">Hello 應用程式部署之後 toohello 叢集中，查詢 hello 外部 IP 位址，並在網頁瀏覽器中開啟它：</span><span class="sxs-lookup"><span data-stu-id="61c21-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![在 Azure 上瀏覽範例應用程式][SB02]


## <a name="next-steps"></a><span data-ttu-id="61c21-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61c21-200">Next steps</span></span>

<span data-ttu-id="61c21-201">如需在 Azure 上使用 Spring 開機的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="61c21-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="61c21-202">部署 Spring 開機應用程式 toohello Azure App Service</span><span class="sxs-lookup"><span data-stu-id="61c21-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="61c21-203">部署在 Linux 上 hello Azure 容器服務中的 Spring 開機應用程式</span><span class="sxs-lookup"><span data-stu-id="61c21-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="61c21-204">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="61c21-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="61c21-205">Docker 範例專案在 hello Spring 開機的相關資訊，請參閱[上開始使用 Docker Spring 開機]。</span><span class="sxs-lookup"><span data-stu-id="61c21-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="61c21-206">hello 下列連結提供有關建立 Spring 開機應用程式的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="61c21-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="61c21-207">如需有關如何建立簡單的 Spring 開機應用程式的詳細資訊，請參閱 < 在 https://start.spring.io/ hello Spring Initializr。</span><span class="sxs-lookup"><span data-stu-id="61c21-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="61c21-208">hello 下列連結提供有關搭配 Azure 使用 Kubernetes 的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="61c21-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="61c21-209">在 Container Service 中開始使用 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="61c21-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="61c21-210">使用 hello Kubernetes web UI，使用 Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="61c21-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="61c21-211">使用 Kubernetes 命令列介面的詳細資訊位於 hello **kubectl**使用者指南 》，網址<https://kubernetes.io/docs/user-guide/kubectl/>。</span><span class="sxs-lookup"><span data-stu-id="61c21-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="61c21-212">hello Kubernetes 網站有幾篇文章會討論使用私人登錄中的映像：</span><span class="sxs-lookup"><span data-stu-id="61c21-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="61c21-213">[設定 Pod 的服務帳戶]</span><span class="sxs-lookup"><span data-stu-id="61c21-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="61c21-214">[命名空間]</span><span class="sxs-lookup"><span data-stu-id="61c21-214">[Namespaces]</span></span>
* <span data-ttu-id="61c21-215">[從私用登錄提取映像]</span><span class="sxs-lookup"><span data-stu-id="61c21-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="61c21-216">針對如何 toouse 自訂的 Docker 映像與 Azure 的其他範例，請參閱[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]。</span><span class="sxs-lookup"><span data-stu-id="61c21-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure 容器服務 (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[上開始使用 Docker Spring 開機]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring 架構]: https://spring.io/
[設定 Pod 的服務帳戶]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[命名空間]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[從私用登錄提取映像]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

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
