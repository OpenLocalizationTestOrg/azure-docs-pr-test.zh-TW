---
title: "如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將容器化 Spring Boot 應用程式部署至 Azure"
description: "了解如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Spring Boot 應用程式部署至 Azure。"
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
ms.openlocfilehash: 883040590291cee94daa227fbc6715ad4be0b393
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="c758c-103">如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將容器化 Spring Boot 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="c758c-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="c758c-104">針對 [Apache Maven](http://maven.apache.org/)的 [適用於 Azure Web 應用程式的 Maven 外掛程式](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)提供 Azure App Service 到 Maven 專案的緊密整合，並且簡化開發人員將 Web 應用程式部署至 Azure App Service 的程序。</span><span class="sxs-lookup"><span data-stu-id="c758c-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service .</span></span>

<span data-ttu-id="c758c-105">本文示範如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Docker 容器中的範例 Spring Boot 應用程式部署至 Azure App Services。</span><span class="sxs-lookup"><span data-stu-id="c758c-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c758c-106">適用於 Azure Web 應用程式的 Maven 外掛程式目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="c758c-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="c758c-107">雖然未來計劃有額外功能，但是現在僅支援 FTP 發佈。</span><span class="sxs-lookup"><span data-stu-id="c758c-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="c758c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c758c-108">Prerequisites</span></span>

<span data-ttu-id="c758c-109">若要完成本教學課程中的步驟，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="c758c-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="c758c-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c758c-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c758c-111">[Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="c758c-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c758c-112">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c758c-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c758c-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="c758c-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c758c-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c758c-114">A [Git] client.</span></span>
* <span data-ttu-id="c758c-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c758c-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c758c-116">由於本教學課程的虛擬化需求，您無法遵循本文中關於虛擬機器的步驟；您必須在啟用虛擬化功能的情況下使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="c758c-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="c758c-117">在 Docker Web 應用程式上複製範例 Spring Boot</span><span class="sxs-lookup"><span data-stu-id="c758c-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="c758c-118">在本節中，您會在本機複製容器化 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="c758c-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c758c-119">開啟命令提示字元或終端機視窗，並建立本機目錄來保存您的 Spring Boot 應用程式，然後變更至該目錄；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c758c-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="c758c-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c758c-121">將 [Spring Boot on Docker Getting Started] 範例專案複製到您所建立的目錄中；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="c758c-122">將目錄變更至已完成的專案；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="c758c-123">使用 Maven 建立 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c758c-124">建立 Web 應用程式後，使用 Maven 啟動 Web 應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c758c-125">測試 Web 應用程式，方法是使用網頁瀏覽器在本機瀏覽它。</span><span class="sxs-lookup"><span data-stu-id="c758c-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c758c-126">例如，如果您有 curl 可用，可以使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c758c-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c758c-127">您應該會看到顯示下列訊息：**Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="c758c-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="c758c-128">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="c758c-128">Create an Azure service principal</span></span>

<span data-ttu-id="c758c-129">在本節中，您建立 Azure 服務主體，Maven 外掛程式會在將您的容器部署至 Azure 時使用該服務主體。</span><span class="sxs-lookup"><span data-stu-id="c758c-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="c758c-130">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c758c-130">Open a command prompt.</span></span>

1. <span data-ttu-id="c758c-131">使用 Azure CLI 登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="c758c-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="c758c-132">依照指示完成登入程序。</span><span class="sxs-lookup"><span data-stu-id="c758c-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="c758c-133">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="c758c-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="c758c-134">其中 `uuuuuuuu` 是使用者名稱，`pppppppp` 是服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="c758c-134">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="c758c-135">Azure 使用 JSON 回應，類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="c758c-135">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="c758c-136">當您設定 Maven 外掛程式以將您的容器部署至 Azure 時，您會使用此 JSON 回應中的值。</span><span class="sxs-lookup"><span data-stu-id="c758c-136">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="c758c-137">`aaaaaaaa`、`uuuuuuuu`、`pppppppp` 和 `tttttttt` 是預留位置值，在此範例中使用，在您於下一節設定 Maven `settings.xml` 檔案時，更方便將這些值對應至個別元素。</span><span class="sxs-lookup"><span data-stu-id="c758c-137">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="c758c-138">設定 Maven 以使用您的 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="c758c-138">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="c758c-139">在本節中，您使用 Azure 服務主體的值，設定將您的容器部署至 Azure 時，Maven 使用的驗證。</span><span class="sxs-lookup"><span data-stu-id="c758c-139">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="c758c-140">在文字編輯器中開啟您的 Maven`settings.xml` 檔案，這個檔案可能在如下列範例的路徑中：</span><span class="sxs-lookup"><span data-stu-id="c758c-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="c758c-141">將本教學課程上一節的 Azure 服務主體設定新增至 settings.xml 檔案中的 `<servers>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-141">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="c758c-142">其中：</span><span class="sxs-lookup"><span data-stu-id="c758c-142">Where:</span></span>
   <span data-ttu-id="c758c-143">元素</span><span class="sxs-lookup"><span data-stu-id="c758c-143">Element</span></span> | <span data-ttu-id="c758c-144">說明</span><span class="sxs-lookup"><span data-stu-id="c758c-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="c758c-145">指定將您的 Web 應用程式部署至 Azure 時，Maven 用來查閱安全性設定的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="c758c-145">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="c758c-146">包含服務主體的 `appId` 值。</span><span class="sxs-lookup"><span data-stu-id="c758c-146">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="c758c-147">包含服務主體的 `tenant` 值。</span><span class="sxs-lookup"><span data-stu-id="c758c-147">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="c758c-148">包含服務主體的 `password` 值。</span><span class="sxs-lookup"><span data-stu-id="c758c-148">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="c758c-149">定義目標 Azure 雲端環境，也就是此範例中的 `AZURE`。</span><span class="sxs-lookup"><span data-stu-id="c758c-149">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="c758c-150">(環境的完整清單可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得)</span><span class="sxs-lookup"><span data-stu-id="c758c-150">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="c758c-151">儲存並關閉 settings.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="c758c-151">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="c758c-152">選擇性：將您的本機 Docker 檔案部署到 Docker Hub</span><span class="sxs-lookup"><span data-stu-id="c758c-152">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="c758c-153">如果您有 Docker 帳戶，您可以在本機建立您的 Docker 容器映像，並將它推送到 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="c758c-153">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="c758c-154">若要這樣做，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c758c-154">To do so, use the following steps.</span></span>

1. <span data-ttu-id="c758c-155">在文字編輯器中開啟 Spring Boot 應用程式的 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c758c-155">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="c758c-156">找出 `<containerSettings>` 元素的 `<imageName>` 子元素。</span><span class="sxs-lookup"><span data-stu-id="c758c-156">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="c758c-157">使用 Docker 帳戶名稱更新 `${docker.image.prefix}` 值：</span><span class="sxs-lookup"><span data-stu-id="c758c-157">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="c758c-158">選擇下列其中一個部署方法：</span><span class="sxs-lookup"><span data-stu-id="c758c-158">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="c758c-159">在本機使用 Maven 建置您的容器映像，然後使用 Docker 將容器推送至 Docker Hub：</span><span class="sxs-lookup"><span data-stu-id="c758c-159">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="c758c-160">如果您已安裝[適用於 Maven 的 Docker 外掛程式]，您可以使用 `-DpushImage` 參數，自動建置您的容器映像並將其推送至 Docker Hub：</span><span class="sxs-lookup"><span data-stu-id="c758c-160">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="c758c-161">選擇性：將您的容器部署至 Azure 之前自訂 pom.xml</span><span class="sxs-lookup"><span data-stu-id="c758c-161">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="c758c-162">在文字編輯器中開啟 Spring Boot 應用程式的 `pom.xml` 檔案，然後找出 `azure-webapp-maven-plugin` 的 `<plugin>` 元素。</span><span class="sxs-lookup"><span data-stu-id="c758c-162">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c758c-163">此元素外觀會類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="c758c-163">This element should resemble the following example:</span></span>

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
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
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

<span data-ttu-id="c758c-164">您可以為 Maven 外掛程式修改數個值，這些元素的詳細描述可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得。</span><span class="sxs-lookup"><span data-stu-id="c758c-164">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c758c-165">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="c758c-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="c758c-166">元素</span><span class="sxs-lookup"><span data-stu-id="c758c-166">Element</span></span> | <span data-ttu-id="c758c-167">說明</span><span class="sxs-lookup"><span data-stu-id="c758c-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="c758c-168">指定[適用於 Azure Web 應用程式的 Maven 外掛程式]版本。</span><span class="sxs-lookup"><span data-stu-id="c758c-168">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c758c-169">您應該檢查 [Maven 中央存放庫](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)中所列的版本，確定您使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="c758c-169">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="c758c-170">指定 Azure 的驗證資訊，在此範例中包含 `<serverId>` 元素，其中包含 `azure-auth`，Maven 使用該值來查閱 Maven settings.xml 檔案 (您在本文稍早章節中定義) 中的 Azure 服務主體值。</span><span class="sxs-lookup"><span data-stu-id="c758c-170">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="c758c-171">指定目標資源群組，也就是此範例中的 `maven-plugin`。</span><span class="sxs-lookup"><span data-stu-id="c758c-171">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="c758c-172">如果該資源群組不存在，則系統會在部署期間建立它。</span><span class="sxs-lookup"><span data-stu-id="c758c-172">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="c758c-173">指定 Web 應用程式的目標名稱。</span><span class="sxs-lookup"><span data-stu-id="c758c-173">Specifies the target name for your web app.</span></span> <span data-ttu-id="c758c-174">在此範例中，目標名稱是 `maven-linux-app-${maven.build.timestamp}`，在此範例中會附加 `${maven.build.timestamp}` 尾碼以避免發生衝突。</span><span class="sxs-lookup"><span data-stu-id="c758c-174">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="c758c-175">(時間戳記是選擇性的；您可以為應用程式名稱指定任何唯一的字串。)</span><span class="sxs-lookup"><span data-stu-id="c758c-175">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="c758c-176">指定目標區域，在此範例中是 `westus`。</span><span class="sxs-lookup"><span data-stu-id="c758c-176">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="c758c-177">(完整清單位於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="c758c-177">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="c758c-178">指定將您的 Web 應用程式部署至 Azure 時，Maven 使用的任何唯一設定。</span><span class="sxs-lookup"><span data-stu-id="c758c-178">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="c758c-179">在此範例中，`<property>` 元素包含子元素的名稱/值組，指定應用程式的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c758c-179">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c758c-180">在此範例中變更連接埠號碼的設定，只有在您變更預設連接埠時才需要。</span><span class="sxs-lookup"><span data-stu-id="c758c-180">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="c758c-181">建置容器並部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="c758c-181">Build and deploy your container to Azure</span></span>

<span data-ttu-id="c758c-182">一旦您已設定本文上述章節中的所有設定，您已準備好將容器部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="c758c-182">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="c758c-183">若要這樣做，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c758c-183">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c758c-184">如果您對 pom.xml 檔案進行任何變更，從您稍早使用的命令提示字元或終端機視窗，使用 Maven 重新建置 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-184">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c758c-185">使用 Maven 將您的 Web 應用程式部署至 Azure；例如：</span><span class="sxs-lookup"><span data-stu-id="c758c-185">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c758c-186">Maven 會將您的 Web 應用程式部署至 Azure；如果 Web 應用程式不存在，系統會加以建立。</span><span class="sxs-lookup"><span data-stu-id="c758c-186">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c758c-187">如果您在 pom.xml 檔案的 `<region>` 元素中指定的區域，在您啟動部署時沒有足夠的可用伺服器，您可能會看到類似下列範例的錯誤：</span><span class="sxs-lookup"><span data-stu-id="c758c-187">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="c758c-188">如果發生這種情況，您可以指定另一個區域，然後重新執行 Maven 命令來部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c758c-188">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="c758c-189">已部署您的網站時，您就可以使用 [Azure 入口網站]來管理它。</span><span class="sxs-lookup"><span data-stu-id="c758c-189">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="c758c-190">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="c758c-190">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="c758c-192">Web 應用程式的 URL 會列在 Web 應用程式的 [概觀] 中：</span><span class="sxs-lookup"><span data-stu-id="c758c-192">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![決定 Web 應用程式的 URL][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="c758c-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c758c-194">Next steps</span></span>

<span data-ttu-id="c758c-195">如需本文所討論之各種技術的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="c758c-195">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c758c-196">[適用於 Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="c758c-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c758c-197">從 Azure CLI 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="c758c-197">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c758c-198">如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Spring Boot 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c758c-198">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="c758c-199">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="c758c-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c758c-200">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="c758c-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="c758c-201">[適用於 Maven 的 Docker 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="c758c-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

<span data-ttu-id="c758c-202">[Azure 命令列介面 (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="c758c-202">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="c758c-203">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="c758c-203">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="c758c-204">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="c758c-204">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="c758c-205">[適用於 Maven 的 Docker 外掛程式]: https://github.com/spotify/docker-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="c758c-205">[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin</span></span>
<span data-ttu-id="c758c-206">[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="c758c-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="c758c-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="c758c-207">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="c758c-208">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="c758c-208">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="c758c-209">[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="c758c-209">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="c758c-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="c758c-210">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="c758c-211">[適用於 Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="c758c-211">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
