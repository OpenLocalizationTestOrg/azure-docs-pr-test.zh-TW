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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="4f46f-103">如何 toouse hello Maven 外掛程式 Azure Web Apps toodeploy Spring 開機應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f46f-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="4f46f-104">hello [Azure Web 應用程式的 Maven 外掛程式](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)如[Apache Maven](http://maven.apache.org/)提供緊密整合到 Maven 專案中，Azure 應用程式服務，並簡化開發人員 toodeploy web 應用程式的 hello 程序tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="4f46f-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="4f46f-105">本文將示範使用 Azure Web Apps toodeploy hello Maven 外掛程式範例 Spring 開機應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="4f46f-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4f46f-106">hello Azure Web 應用程式的 Maven 外掛程式是目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="4f46f-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="4f46f-107">現在，只有 FTP 發行支援，雖然 hello 未來計劃的額外功能。</span><span class="sxs-lookup"><span data-stu-id="4f46f-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="4f46f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="4f46f-108">Prerequisites</span></span>

<span data-ttu-id="4f46f-109">在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="4f46f-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="4f46f-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4f46f-111">hello [Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="4f46f-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="4f46f-112">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4f46f-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="4f46f-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="4f46f-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="4f46f-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4f46f-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="4f46f-115">複製 hello 範例 Spring 開機 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4f46f-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="4f46f-116">在本節中，您會在本機複製已完成 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="4f46f-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="4f46f-117">開啟命令提示字元或終端機視窗，並建立本機目錄 toohold 您 Spring 開機應用程式，並變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="4f46f-118">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="4f46f-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="4f46f-119">複製 hello [Spring 開機入門]範例專案到 hello 目錄，您所建立的; 例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="4f46f-120">變更目錄已完成的 toohello 專案;例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="4f46f-121">建置使用 Maven; hello JAR 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="4f46f-122">Hello web 應用程式建立後，開始使用 Maven; hello web 應用程式例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="4f46f-123">藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4f46f-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="4f46f-124">例如，您可以使用下列命令，如果您有可用的 curl hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="4f46f-125">您應該會看到下列訊息顯示 hello:**從 Spring 開機 Greetings ！**</span><span class="sxs-lookup"><span data-stu-id="4f46f-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="4f46f-126">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="4f46f-126">Create an Azure service principal</span></span>

<span data-ttu-id="4f46f-127">在本節中，您建立 Azure 部署您的 web 應用程式 tooAzure 時 hello Maven 外掛程式使用的服務主體。</span><span class="sxs-lookup"><span data-stu-id="4f46f-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="4f46f-128">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="4f46f-128">Open a command prompt.</span></span>

1. <span data-ttu-id="4f46f-129">登入您的 Azure 帳戶使用 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="4f46f-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="4f46f-130">請遵循 hello 指示 toocomplete hello 登入程序。</span><span class="sxs-lookup"><span data-stu-id="4f46f-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="4f46f-131">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="4f46f-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="4f46f-132">其中`uuuuuuuu`是 hello 的使用者名稱和`pppppppp`hello hello 服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="4f46f-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="4f46f-133">Azure 會使用類似下列範例中的 hello 的 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="4f46f-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="4f46f-134">當您設定您的 web 應用程式 tooAzure hello Maven 外掛程式 toodeploy 時，您將使用此 JSON 回應 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4f46f-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="4f46f-135">hello `aaaaaaaa`， `uuuuuuuu`， `pppppppp`，和`tttttttt`預留位置的值，也就是用於此範例 toomake 它更容易 toomap 這些 tootheir 個別項目的值設定您的 Maven 時`settings.xml`hello 中檔案的下一步一節。</span><span class="sxs-lookup"><span data-stu-id="4f46f-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="4f46f-136">設定您的 Azure 服務主體的 Maven toouse</span><span class="sxs-lookup"><span data-stu-id="4f46f-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="4f46f-137">在本節中，您可以使用 hello 值從 Maven 使用部署您的 web 應用程式 tooAzure 時您 Azure 服務主體 tooconfigure hello 的驗證。</span><span class="sxs-lookup"><span data-stu-id="4f46f-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="4f46f-138">開啟您的 Maven`settings.xml`檔案文字編輯器中; 這個檔案可能是路徑，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="4f46f-139">從這個教學課程 toohello hello 上一節中新增您的 Azure 服務主體設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="4f46f-140">其中：</span><span class="sxs-lookup"><span data-stu-id="4f46f-140">Where:</span></span>
   <span data-ttu-id="4f46f-141">元素</span><span class="sxs-lookup"><span data-stu-id="4f46f-141">Element</span></span> | <span data-ttu-id="4f46f-142">說明</span><span class="sxs-lookup"><span data-stu-id="4f46f-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="4f46f-143">指定 Maven 使用 toolook 註冊您的安全性設定，當您部署您的 web 應用程式 tooAzure 的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="4f46f-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="4f46f-144">包含 hello`appId`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="4f46f-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="4f46f-145">包含 hello`tenant`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="4f46f-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="4f46f-146">包含 hello`password`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="4f46f-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="4f46f-147">定義 hello 目標 Azure 雲端環境，也就是`AZURE`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="4f46f-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="4f46f-148">(環境的完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件)</span><span class="sxs-lookup"><span data-stu-id="4f46f-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="4f46f-149">儲存並關閉 hello *settings.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="4f46f-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="4f46f-150">選擇性： 部署您的 web 應用程式 tooAzure 之前自訂您 pom.xml</span><span class="sxs-lookup"><span data-stu-id="4f46f-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="4f46f-151">開啟 hello`pom.xml`在文字編輯器中，應用程式 Spring 開機檔案，然後找出 hello`<plugin>`元素`azure-webapp-maven-plugin`。</span><span class="sxs-lookup"><span data-stu-id="4f46f-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="4f46f-152">這個項目應該類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-152">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="4f46f-153">有數個值，您可以修改 hello Maven 外掛程式，而且每個這些元件的詳細的描述在 hello [Azure Web 應用程式的 Maven 外掛程式]文件。</span><span class="sxs-lookup"><span data-stu-id="4f46f-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="4f46f-154">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="4f46f-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="4f46f-155">元素</span><span class="sxs-lookup"><span data-stu-id="4f46f-155">Element</span></span> | <span data-ttu-id="4f46f-156">說明</span><span class="sxs-lookup"><span data-stu-id="4f46f-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="4f46f-157">指定 hello 版的 hello [Azure Web 應用程式的 Maven 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="4f46f-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="4f46f-158">您應該檢查 hello 版本列在 hello [Maven 中央儲存機制](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)您使用的 tooensure hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="4f46f-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="4f46f-159">指定 Azure，這在此範例中包含的 hello 驗證資訊`<serverId>`包含項目`azure-auth`;Maven 使用 hello Azure 服務主體值的值 toolook 中您 Maven *settings.xml*在本文的前一節中所定義的檔案。</span><span class="sxs-lookup"><span data-stu-id="4f46f-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="4f46f-160">指定 hello 目標資源群組，也就是`maven-plugin`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="4f46f-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="4f46f-161">如果不存在，會在部署期間建立 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="4f46f-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="4f46f-162">指定 web 應用程式的 hello 目標名稱。</span><span class="sxs-lookup"><span data-stu-id="4f46f-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="4f46f-163">在此範例中，是 hello 目標名稱`maven-web-app-${maven.build.timestamp}`，其中 hello`${maven.build.timestamp}`尾碼會附加在這個範例 tooavoid 衝突。</span><span class="sxs-lookup"><span data-stu-id="4f46f-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="4f46f-164">（hello 時間戳記是選擇性的; 您可以指定任何唯一的字串 hello 應用程式名稱）。</span><span class="sxs-lookup"><span data-stu-id="4f46f-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="4f46f-165">指定 hello 目標區域，而在此範例中`westus`。</span><span class="sxs-lookup"><span data-stu-id="4f46f-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="4f46f-166">(完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="4f46f-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="4f46f-167">指定 web 應用程式的 hello Java 執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="4f46f-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="4f46f-168">(完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="4f46f-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="4f46f-169">指定 Web 應用程式的部署類型。</span><span class="sxs-lookup"><span data-stu-id="4f46f-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="4f46f-170">雖然其他部署類型的支援正在開發中，現在只有 `ftp` 受到支援。</span><span class="sxs-lookup"><span data-stu-id="4f46f-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="4f46f-171">指定資源和 Maven 使用時部署您的 web 應用程式 tooAzure 目標目的地。</span><span class="sxs-lookup"><span data-stu-id="4f46f-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="4f46f-172">在此範例中，兩個`<resource>`項目會指定 Maven 將部署 hello JAR 檔案，以您的 web 應用程式和 hello *web.config* hello Spring 開機專案檔案。</span><span class="sxs-lookup"><span data-stu-id="4f46f-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="4f46f-173">建置和部署您的 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f46f-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="4f46f-174">一旦您已設定的所有 hello 設定 hello 前面的本文區段中，您就準備好 toodeploy 您 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4f46f-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="4f46f-175">toodo 因此，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="4f46f-176">從 hello 命令提示字元或稍早所使用的終端機視窗，重建 hello JAR 檔案，如果您進行任何變更 toohello 使用 Maven *pom.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="4f46f-177">部署您的 web 應用程式 tooAzure 使用 Maven;例如：</span><span class="sxs-lookup"><span data-stu-id="4f46f-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="4f46f-178">Maven 會部署您的 web 應用程式 tooAzure;如果 hello web 應用程式不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="4f46f-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="4f46f-179">已部署您的網站，將無法 toomanage 它使用 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="4f46f-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="4f46f-180">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="4f46f-180">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="4f46f-182">Hello URL 的 web 應用程式將會列在 hello 和**概觀**web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="4f46f-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4f46f-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f46f-184">Next steps</span></span>

<span data-ttu-id="4f46f-185">如需有關 hello 本文所討論的各種技術，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="4f46f-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="4f46f-186">[Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="4f46f-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="4f46f-187">登入從 hello Azure CLI tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f46f-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="4f46f-188">如何 toouse hello Maven 外掛程式 toodeploy Azure Web 應用程式容器化的 Spring 開機應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f46f-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="4f46f-189">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="4f46f-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="4f46f-190">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="4f46f-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

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
