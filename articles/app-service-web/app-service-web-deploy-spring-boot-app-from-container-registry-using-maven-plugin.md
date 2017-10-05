---
title: "如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Azure Container Registry 中的 Spring Boot 應用程式部署至 Azure App Service"
description: "本教學課程將逐步引導您藉由使用 Maven 外掛程式，將 Azure Container Registry 中的 Spring Boot 應用程式部署到 Azure App Service。"
services: 
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
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: f47ee59d72ea49d62be2cb435ebaf8bc841e4198
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="14082-103">如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Azure Container Registry 中的 Spring Boot 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="14082-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="14082-104">**[Spring 架構]**是受歡迎的開放原始碼架構，可協助 Java 開發人員建立 Web、行動及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14082-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="14082-105">本教學課程使用以 [Spring Boot] 建立的範例應用程式，這是快速開始使用 Spring 的慣例方法。</span><span class="sxs-lookup"><span data-stu-id="14082-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="14082-106">本文示範如何將範例 Spring Boot 應用程式部署至 Azure Container Registry，然後使用適用於 Azure Web 應用程式的 Maven 外掛程式，將應用程式部署至 Azure App Services。</span><span class="sxs-lookup"><span data-stu-id="14082-106">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="14082-107">適用於 Azure Web 應用程式的 Maven 外掛程式目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="14082-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="14082-108">雖然未來計劃有額外功能，但是現在僅支援 FTP 發佈。</span><span class="sxs-lookup"><span data-stu-id="14082-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="14082-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="14082-109">Prerequisites</span></span>

<span data-ttu-id="14082-110">若要完成本教學課程中的步驟，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="14082-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="14082-111">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="14082-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="14082-112">[Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="14082-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="14082-113">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="14082-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="14082-114">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="14082-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="14082-115">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="14082-115">A [Git] client.</span></span>
* <span data-ttu-id="14082-116">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="14082-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="14082-117">由於本教學課程的虛擬化需求，您無法遵循本文中關於虛擬機器的步驟；您必須在啟用虛擬化功能的情況下使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="14082-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="14082-118">在 Docker Web 應用程式上複製範例 Spring Boot</span><span class="sxs-lookup"><span data-stu-id="14082-118">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="14082-119">在本節中，您會在本機複製容器化 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="14082-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="14082-120">開啟命令提示字元或終端機視窗，並建立本機目錄來保存您的 Spring Boot 應用程式，然後變更至該目錄；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="14082-121">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="14082-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="14082-122">將 [Spring Boot on Docker Getting Started] 範例專案複製到您所建立的目錄中；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="14082-123">將目錄變更至已完成的專案；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="14082-124">使用 Maven 建立 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="14082-125">建立 Web 應用程式後，使用 Maven 啟動 Web 應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="14082-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="14082-126">測試 Web 應用程式，方法是使用網頁瀏覽器在本機瀏覽它。</span><span class="sxs-lookup"><span data-stu-id="14082-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="14082-127">例如，如果您有 curl 可用，可以使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="14082-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="14082-128">您應該會看到顯示下列訊息：**Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="14082-128">You should see the following message displayed: **Hello Docker World**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="14082-130">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="14082-130">Create an Azure service principal</span></span>

<span data-ttu-id="14082-131">在本節中，您建立 Azure 服務主體，Maven 外掛程式會在將您的容器部署至 Azure 時使用該服務主體。</span><span class="sxs-lookup"><span data-stu-id="14082-131">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="14082-132">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="14082-132">Open a command prompt.</span></span>

1. <span data-ttu-id="14082-133">使用 Azure CLI 登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="14082-133">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="14082-134">依照指示完成登入程序。</span><span class="sxs-lookup"><span data-stu-id="14082-134">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="14082-135">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="14082-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="14082-136">其中 `uuuuuuuu` 是使用者名稱，`pppppppp` 是服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="14082-136">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="14082-137">Azure 使用 JSON 回應，類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="14082-137">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="14082-138">當您設定 Maven 外掛程式以將您的容器部署至 Azure 時，您會使用此 JSON 回應中的值。</span><span class="sxs-lookup"><span data-stu-id="14082-138">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="14082-139">`aaaaaaaa`、`uuuuuuuu`、`pppppppp` 和 `tttttttt` 是預留位置值，在此範例中使用，在您於下一節設定 Maven `settings.xml` 檔案時，更方便將這些值對應至個別元素。</span><span class="sxs-lookup"><span data-stu-id="14082-139">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="14082-140">使用 Azure CLI 建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="14082-140">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="14082-141">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="14082-141">Open a command prompt.</span></span>

1. <span data-ttu-id="14082-142">登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="14082-142">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="14082-143">為您將在這篇文章中使用的 Azure 資源建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="14082-143">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="14082-144">將此範例中的 `wingtiptoysresources` 取代為資源群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="14082-145">在 Spring Boot 應用程式的資源群組中建立私用 Azure Container Registry：</span><span class="sxs-lookup"><span data-stu-id="14082-145">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="14082-146">將此範例中的 `wingtiptoysregistry` 取代為容器登錄的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="14082-147">擷取容器登錄的密碼：</span><span class="sxs-lookup"><span data-stu-id="14082-147">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="14082-148">Azure 會回應您的密碼，例如：</span><span class="sxs-lookup"><span data-stu-id="14082-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="14082-149">將您的 Azure Container Registry 和 Azure 服務主體新增至您的 Maven 設定</span><span class="sxs-lookup"><span data-stu-id="14082-149">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="14082-150">在文字編輯器中開啟您的 Maven`settings.xml` 檔案，這個檔案可能在如下列範例的路徑中：</span><span class="sxs-lookup"><span data-stu-id="14082-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="14082-151">將這篇文章上一節的 Azure Container Registry 存取設定新增至 settings.xml 檔案中的 `<servers>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-151">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="14082-152">其中：</span><span class="sxs-lookup"><span data-stu-id="14082-152">Where:</span></span>
   <span data-ttu-id="14082-153">元素</span><span class="sxs-lookup"><span data-stu-id="14082-153">Element</span></span> | <span data-ttu-id="14082-154">說明</span><span class="sxs-lookup"><span data-stu-id="14082-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="14082-155">包含私用 Azure Container Registry 名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-155">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="14082-156">包含私用 Azure Container Registry 名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-156">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="14082-157">包含您在這篇文章上一節擷取的密碼。</span><span class="sxs-lookup"><span data-stu-id="14082-157">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="14082-158">將這篇文章稍早章節的 Azure 服務主體設定新增至 settings.xml 檔案中的 `<servers>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-158">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="14082-159">其中：</span><span class="sxs-lookup"><span data-stu-id="14082-159">Where:</span></span>
   <span data-ttu-id="14082-160">元素</span><span class="sxs-lookup"><span data-stu-id="14082-160">Element</span></span> | <span data-ttu-id="14082-161">說明</span><span class="sxs-lookup"><span data-stu-id="14082-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="14082-162">指定將您的 Web 應用程式部署至 Azure 時，Maven 用來查閱安全性設定的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-162">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="14082-163">包含服務主體的 `appId` 值。</span><span class="sxs-lookup"><span data-stu-id="14082-163">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="14082-164">包含服務主體的 `tenant` 值。</span><span class="sxs-lookup"><span data-stu-id="14082-164">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="14082-165">包含服務主體的 `password` 值。</span><span class="sxs-lookup"><span data-stu-id="14082-165">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="14082-166">定義目標 Azure 雲端環境，也就是此範例中的 `AZURE`。</span><span class="sxs-lookup"><span data-stu-id="14082-166">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="14082-167">(環境的完整清單可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得)</span><span class="sxs-lookup"><span data-stu-id="14082-167">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="14082-168">儲存並關閉 settings.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="14082-168">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="14082-169">建置您的 Docker 容器映像，並將它推送到您的 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="14082-169">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="14082-170">瀏覽至 Spring Boot 應用程式的已完成專案目錄 (例如，"*C:\SpringBoot\gs-spring-boot-docker\complete*" 或 "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*")，並使用文字編輯器開啟 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="14082-170">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="14082-171">使用本教學課程上一節的 Azure Container Registry 登入伺服器值來更新 pom.xml 檔案中的 `<properties>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-171">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="14082-172">其中：</span><span class="sxs-lookup"><span data-stu-id="14082-172">Where:</span></span>
   <span data-ttu-id="14082-173">元素</span><span class="sxs-lookup"><span data-stu-id="14082-173">Element</span></span> | <span data-ttu-id="14082-174">說明</span><span class="sxs-lookup"><span data-stu-id="14082-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="14082-175">指定私用 Azure Container Registry 名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-175">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="14082-176">指定私用 Azure Container Registry 的 URL，它是藉由將 ".azurecr.io" 附加至私用容器登錄的名稱來衍生。</span><span class="sxs-lookup"><span data-stu-id="14082-176">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="14082-177">確認 pom.xml 檔案中 Docker 外掛程式的 `<plugin>`，包含本教學課程上一個步驟中伺服器位址和登錄名稱的正確屬性。</span><span class="sxs-lookup"><span data-stu-id="14082-177">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="14082-178">例如：</span><span class="sxs-lookup"><span data-stu-id="14082-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="14082-179">其中：</span><span class="sxs-lookup"><span data-stu-id="14082-179">Where:</span></span>
   <span data-ttu-id="14082-180">元素</span><span class="sxs-lookup"><span data-stu-id="14082-180">Element</span></span> | <span data-ttu-id="14082-181">說明</span><span class="sxs-lookup"><span data-stu-id="14082-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="14082-182">指定屬性，該屬性包含私用 Azure Container Registry 的名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-182">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="14082-183">指定屬性，該屬性包含私用 Azure Container Registry 的 URL。</span><span class="sxs-lookup"><span data-stu-id="14082-183">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="14082-184">瀏覽至您 Spring Boot 應用程式的已完成專案目錄，然後執行下列命令來重建應用程式，並將容器推送到您的 Azure Container Registry：</span><span class="sxs-lookup"><span data-stu-id="14082-184">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="14082-185">選擇性：瀏覽至 [Azure 入口網站]，並確認在容器登錄中有名為 **gs-spring-boot-docker** 的 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="14082-185">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![確認在 Azure 入口網站中的容器][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="14082-187">自訂 pom.xml，然後建立容器並將其部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="14082-187">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="14082-188">在文字編輯器中開啟 Spring Boot 應用程式的 `pom.xml` 檔案，然後找出 `azure-webapp-maven-plugin` 的 `<plugin>` 元素。</span><span class="sxs-lookup"><span data-stu-id="14082-188">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="14082-189">此元素外觀會類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="14082-189">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="14082-190">您可以為 Maven 外掛程式修改數個值，這些元素的詳細描述可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得。</span><span class="sxs-lookup"><span data-stu-id="14082-190">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="14082-191">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="14082-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="14082-192">元素</span><span class="sxs-lookup"><span data-stu-id="14082-192">Element</span></span> | <span data-ttu-id="14082-193">說明</span><span class="sxs-lookup"><span data-stu-id="14082-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="14082-194">指定[適用於 Azure Web 應用程式的 Maven 外掛程式]版本。</span><span class="sxs-lookup"><span data-stu-id="14082-194">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="14082-195">您應該檢查 [Maven 中央存放庫](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)中所列的版本，確定您使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="14082-195">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="14082-196">指定 Azure 的驗證資訊，在此範例中包含 `<serverId>` 元素，其中包含 `azure-auth`，Maven 使用該值來查閱 Maven settings.xml 檔案 (您在本文稍早章節中定義) 中的 Azure 服務主體值。</span><span class="sxs-lookup"><span data-stu-id="14082-196">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="14082-197">指定目標資源群組，也就是此範例中的 `wingtiptoysresources`。</span><span class="sxs-lookup"><span data-stu-id="14082-197">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="14082-198">如果該資源群組不存在，則系統會在部署期間建立它。</span><span class="sxs-lookup"><span data-stu-id="14082-198">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="14082-199">指定 Web 應用程式的目標名稱。</span><span class="sxs-lookup"><span data-stu-id="14082-199">Specifies the target name for your web app.</span></span> <span data-ttu-id="14082-200">在此範例中，目標名稱是 `maven-linux-app-${maven.build.timestamp}`，在此範例中會附加 `${maven.build.timestamp}` 尾碼以避免發生衝突。</span><span class="sxs-lookup"><span data-stu-id="14082-200">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="14082-201">(時間戳記是選擇性的；您可以為應用程式名稱指定任何唯一的字串。)</span><span class="sxs-lookup"><span data-stu-id="14082-201">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="14082-202">指定目標區域，在此範例中是 `westus`。</span><span class="sxs-lookup"><span data-stu-id="14082-202">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="14082-203">(完整清單位於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="14082-203">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="14082-204">指定屬性，該屬性包含容器的名稱和 URL。</span><span class="sxs-lookup"><span data-stu-id="14082-204">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="14082-205">指定將您的 Web 應用程式部署至 Azure 時，Maven 使用的任何唯一設定。</span><span class="sxs-lookup"><span data-stu-id="14082-205">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="14082-206">在此範例中，`<property>` 元素包含子元素的名稱/值組，指定應用程式的連接埠。</span><span class="sxs-lookup"><span data-stu-id="14082-206">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="14082-207">在此範例中變更連接埠號碼的設定，只有在您變更預設連接埠時才需要。</span><span class="sxs-lookup"><span data-stu-id="14082-207">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="14082-208">如果您對 pom.xml 檔案進行任何變更，從您稍早使用的命令提示字元或終端機視窗，使用 Maven 重新建置 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-208">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="14082-209">使用 Maven 將您的 Web 應用程式部署至 Azure；例如：</span><span class="sxs-lookup"><span data-stu-id="14082-209">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="14082-210">Maven 會將您的 Web 應用程式部署至 Azure；如果 Web 應用程式不存在，系統會加以建立。</span><span class="sxs-lookup"><span data-stu-id="14082-210">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="14082-211">如果您在 pom.xml 檔案的 `<region>` 元素中指定的區域，在您啟動部署時沒有足夠的可用伺服器，您可能會看到類似下列範例的錯誤：</span><span class="sxs-lookup"><span data-stu-id="14082-211">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="14082-212">如果發生這種情況，您可以指定另一個區域，然後重新執行 Maven 命令來部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="14082-212">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="14082-213">已部署您的網站時，您就可以使用 [Azure 入口網站]來管理它。</span><span class="sxs-lookup"><span data-stu-id="14082-213">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="14082-214">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="14082-214">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="14082-216">Web 應用程式的 URL 會列在 Web 應用程式的 [概觀] 中：</span><span class="sxs-lookup"><span data-stu-id="14082-216">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![決定 Web 應用程式的 URL][AP02]

## <a name="next-steps"></a><span data-ttu-id="14082-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14082-218">Next steps</span></span>

<span data-ttu-id="14082-219">如需本文所討論之各種技術的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="14082-219">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="14082-220">[適用於 Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="14082-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="14082-221">從 Azure CLI 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="14082-221">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="14082-222">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="14082-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="14082-223">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="14082-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="14082-224">[適用於 Maven 的 Docker 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="14082-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="14082-225">[Azure 命令列介面 (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="14082-225">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="14082-226">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="14082-226">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="14082-227">[適用於 Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="14082-227">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
<span data-ttu-id="14082-228">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="14082-228">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="14082-229">[適用於 Maven 的 Docker 外掛程式]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="14082-229">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="14082-230">[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="14082-230">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="14082-231">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="14082-231">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="14082-232">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="14082-232">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="14082-233">[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="14082-233">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="14082-234">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="14082-234">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="14082-235">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="14082-235">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="14082-236">[Spring 架構]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="14082-236">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
