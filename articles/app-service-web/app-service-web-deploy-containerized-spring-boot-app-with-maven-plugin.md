---
title: "Azure Web Apps toodeploy 容器化的 Spring 開機應用程式 tooAzure 的 aaaHow toouse hello Maven 外掛程式"
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
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="8283b-103">如何 toouse hello Maven 外掛程式 toodeploy Azure Web 應用程式容器化的 Spring 開機應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8283b-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="8283b-104">hello [Azure Web 應用程式的 Maven 外掛程式](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)如[Apache Maven](http://maven.apache.org/)提供緊密整合到 Maven 專案中，Azure 應用程式服務，並簡化開發人員 toodeploy web 應用程式的 hello 程序tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8283b-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="8283b-105">本文將示範使用 Azure Web Apps toodeploy hello Maven 外掛程式範例 Spring 開機應用程式在 Docker 容器 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8283b-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8283b-106">hello Azure Web 應用程式的 Maven 外掛程式是目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="8283b-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="8283b-107">現在，只有 FTP 發行支援，雖然 hello 未來計劃的額外功能。</span><span class="sxs-lookup"><span data-stu-id="8283b-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="8283b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="8283b-108">Prerequisites</span></span>

<span data-ttu-id="8283b-109">在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="8283b-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="8283b-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8283b-111">hello [Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="8283b-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="8283b-112">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8283b-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="8283b-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="8283b-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="8283b-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="8283b-114">A [Git] client.</span></span>
* <span data-ttu-id="8283b-115">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="8283b-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8283b-116">Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="8283b-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="8283b-117">Docker web 應用程式上的複製 hello 範例 Spring 開機</span><span class="sxs-lookup"><span data-stu-id="8283b-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="8283b-118">在本節中，您會在本機複製容器化 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="8283b-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="8283b-119">開啟命令提示字元或終端機視窗，並建立本機目錄 toohold 您 Spring 開機應用程式，並變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8283b-120">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="8283b-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="8283b-121">複製 hello[上開始使用 Docker Spring 開機]範例專案到 hello 目錄，您所建立的; 例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="8283b-122">變更目錄已完成的 toohello 專案;例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="8283b-123">建置使用 Maven; hello JAR 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8283b-124">Hello web 應用程式建立後，開始使用 Maven; hello web 應用程式例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8283b-125">藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8283b-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="8283b-126">例如，您可以使用下列命令，如果您有可用的 curl hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="8283b-127">您應該會看到下列訊息顯示 hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="8283b-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="8283b-128">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="8283b-128">Create an Azure service principal</span></span>

<span data-ttu-id="8283b-129">在本節中，您建立 Azure 部署容器 tooAzure 時 hello Maven 外掛程式使用的服務主體。</span><span class="sxs-lookup"><span data-stu-id="8283b-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="8283b-130">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="8283b-130">Open a command prompt.</span></span>

1. <span data-ttu-id="8283b-131">登入您的 Azure 帳戶使用 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="8283b-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="8283b-132">請遵循 hello 指示 toocomplete hello 登入程序。</span><span class="sxs-lookup"><span data-stu-id="8283b-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="8283b-133">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="8283b-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="8283b-134">其中`uuuuuuuu`是 hello 的使用者名稱和`pppppppp`hello hello 服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="8283b-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="8283b-135">Azure 會使用類似下列範例中的 hello 的 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="8283b-135">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="8283b-136">當您設定 hello Maven 外掛程式 toodeploy 容器 tooAzure 時，您將使用此 JSON 回應 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8283b-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="8283b-137">hello `aaaaaaaa`， `uuuuuuuu`， `pppppppp`，和`tttttttt`預留位置的值，也就是用於此範例 toomake 它更容易 toomap 這些 tootheir 個別項目的值設定您的 Maven 時`settings.xml`hello 中檔案的下一步一節。</span><span class="sxs-lookup"><span data-stu-id="8283b-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="8283b-138">設定您的 Azure 服務主體的 Maven toouse</span><span class="sxs-lookup"><span data-stu-id="8283b-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="8283b-139">在本節中，您可以使用 hello 值從 Maven 用來部署容器 tooAzure 您 Azure 服務主體 tooconfigure hello 的驗證。</span><span class="sxs-lookup"><span data-stu-id="8283b-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="8283b-140">開啟您的 Maven`settings.xml`檔案文字編輯器中; 這個檔案可能是路徑，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="8283b-141">從這個教學課程 toohello hello 上一節中新增您的 Azure 服務主體設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="8283b-142">其中：</span><span class="sxs-lookup"><span data-stu-id="8283b-142">Where:</span></span>
   <span data-ttu-id="8283b-143">元素</span><span class="sxs-lookup"><span data-stu-id="8283b-143">Element</span></span> | <span data-ttu-id="8283b-144">說明</span><span class="sxs-lookup"><span data-stu-id="8283b-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="8283b-145">指定 Maven 使用 toolook 註冊您的安全性設定，當您部署您的 web 應用程式 tooAzure 的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="8283b-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="8283b-146">包含 hello`appId`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="8283b-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="8283b-147">包含 hello`tenant`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="8283b-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="8283b-148">包含 hello`password`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="8283b-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="8283b-149">定義 hello 目標 Azure 雲端環境，也就是`AZURE`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="8283b-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="8283b-150">(環境的完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件)</span><span class="sxs-lookup"><span data-stu-id="8283b-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="8283b-151">儲存並關閉 hello *settings.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="8283b-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="8283b-152">選擇性： 部署您本機的 Docker 檔案 tooDocker 中樞</span><span class="sxs-lookup"><span data-stu-id="8283b-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="8283b-153">如果您有 Docker 帳戶，您可以建立您的 Docker 容器映像在本機，並直接將其推 tooDocker 中樞。</span><span class="sxs-lookup"><span data-stu-id="8283b-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="8283b-154">toodo 因此，使用下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="8283b-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="8283b-155">開啟 hello `pom.xml` Spring 開機應用程式在文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="8283b-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="8283b-156">找出 hello `<imageName>` hello 子項目`<containerSettings>`項目。</span><span class="sxs-lookup"><span data-stu-id="8283b-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="8283b-157">更新 hello`${docker.image.prefix}`使用 Docker 帳戶名稱的值：</span><span class="sxs-lookup"><span data-stu-id="8283b-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="8283b-158">選擇 hello 下列部署方法的其中一個：</span><span class="sxs-lookup"><span data-stu-id="8283b-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="8283b-159">在本機使用 Maven，來建置您的容器映像，然後使用 Docker toopush 您容器 tooDocker 中樞：</span><span class="sxs-lookup"><span data-stu-id="8283b-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="8283b-160">如果您擁有 hello [Maven 的 Docker 外掛程式]安裝，您可以自動建立和使用您容器映像 tooDocker 中樞 hello`-DpushImage`參數：</span><span class="sxs-lookup"><span data-stu-id="8283b-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="8283b-161">選擇性： 部署容器 tooAzure 之前自訂您 pom.xml</span><span class="sxs-lookup"><span data-stu-id="8283b-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="8283b-162">開啟 hello`pom.xml`在文字編輯器中，應用程式 Spring 開機檔案，然後找出 hello`<plugin>`元素`azure-webapp-maven-plugin`。</span><span class="sxs-lookup"><span data-stu-id="8283b-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="8283b-163">這個項目應該類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-163">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="8283b-164">有數個值，您可以修改 hello Maven 外掛程式，而且每個這些元件的詳細的描述在 hello [Azure Web 應用程式的 Maven 外掛程式]文件。</span><span class="sxs-lookup"><span data-stu-id="8283b-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="8283b-165">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="8283b-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="8283b-166">元素</span><span class="sxs-lookup"><span data-stu-id="8283b-166">Element</span></span> | <span data-ttu-id="8283b-167">說明</span><span class="sxs-lookup"><span data-stu-id="8283b-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="8283b-168">指定 hello 版的 hello [Azure Web 應用程式的 Maven 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="8283b-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="8283b-169">您應該檢查 hello 版本列在 hello [Maven 中央儲存機制](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)您使用的 tooensure hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="8283b-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="8283b-170">指定 Azure，這在此範例中包含的 hello 驗證資訊`<serverId>`包含項目`azure-auth`;Maven 使用 hello Azure 服務主體值的值 toolook 中您 Maven *settings.xml*在本文的前一節中所定義的檔案。</span><span class="sxs-lookup"><span data-stu-id="8283b-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="8283b-171">指定 hello 目標資源群組，也就是`maven-plugin`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="8283b-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="8283b-172">會在部署期間建立 hello 資源群組，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="8283b-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="8283b-173">指定 web 應用程式的 hello 目標名稱。</span><span class="sxs-lookup"><span data-stu-id="8283b-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="8283b-174">在此範例中，是 hello 目標名稱`maven-linux-app-${maven.build.timestamp}`，其中 hello`${maven.build.timestamp}`尾碼會附加在這個範例 tooavoid 衝突。</span><span class="sxs-lookup"><span data-stu-id="8283b-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="8283b-175">（hello 時間戳記是選擇性的; 您可以指定任何唯一的字串 hello 應用程式名稱）。</span><span class="sxs-lookup"><span data-stu-id="8283b-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="8283b-176">指定 hello 目標區域，而在此範例中`westus`。</span><span class="sxs-lookup"><span data-stu-id="8283b-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="8283b-177">(完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="8283b-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="8283b-178">部署您的 web 應用程式 tooAzure 時，請指定 Maven toouse 任何唯一的設定。</span><span class="sxs-lookup"><span data-stu-id="8283b-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="8283b-179">在此範例中，`<property>`元素包含子元素，指定您的應用程式的 hello 連接埠的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="8283b-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8283b-180">從 hello 預設變更 hello 連接埠時，才需要 hello 設定 toochange hello 連接埠號碼在此範例中。</span><span class="sxs-lookup"><span data-stu-id="8283b-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="8283b-181">建置和部署容器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8283b-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="8283b-182">一旦您已設定的所有 hello 設定 hello 前面的本文區段中，您就準備好 toodeploy 容器 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="8283b-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="8283b-183">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="8283b-184">從 hello 命令提示字元或稍早所使用的終端機視窗，重建 hello JAR 檔案，如果您進行任何變更 toohello 使用 Maven *pom.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8283b-185">部署您的 web 應用程式 tooAzure 使用 Maven;例如：</span><span class="sxs-lookup"><span data-stu-id="8283b-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="8283b-186">Maven 會部署您的 web 應用程式 tooAzure;如果 hello web 應用程式不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="8283b-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8283b-187">如果您指定在 hello hello 區`<region>`元素您*pom.xml*檔案沒有足夠可用的伺服器進行部署時，您可能會看到錯誤類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="8283b-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="8283b-188">如果發生這種情況，您可以指定另一個區域，然後重新執行 hello Maven 命令 toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8283b-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="8283b-189">已部署您的網站，將無法 toomanage 它使用 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="8283b-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="8283b-190">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="8283b-190">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="8283b-192">Hello URL 的 web 應用程式將會列在 hello 和**概觀**web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="8283b-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8283b-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8283b-194">Next steps</span></span>

<span data-ttu-id="8283b-195">如需有關 hello 本文所討論的各種技術，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="8283b-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="8283b-196">[Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="8283b-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="8283b-197">登入從 hello Azure CLI tooAzure</span><span class="sxs-lookup"><span data-stu-id="8283b-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="8283b-198">如何 toouse hello Maven 外掛程式 Azure Web Apps toodeploy Spring 開機應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="8283b-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="8283b-199">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="8283b-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="8283b-200">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="8283b-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="8283b-201">[Maven 的 Docker 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="8283b-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure 入口網站]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Maven 的 Docker 外掛程式]: https://github.com/spotify/docker-maven-plugin
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[上開始使用 Docker Spring 開機]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
