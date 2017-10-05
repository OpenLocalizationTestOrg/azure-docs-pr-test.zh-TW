---
title: "如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Spring Boot 應用程式部署至 Azure"
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
ms.openlocfilehash: dceb7edf788bd87b1de04aa435a12cd5853755b9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="68d70-103">如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將 Spring Boot 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="68d70-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="68d70-104">針對 [Apache Maven](http://maven.apache.org/) 的[適用於 Azure Web 應用程式的 Maven 外掛程式](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)提供 Azure App Service 到 Maven 專案的緊密整合，並且簡化開發人員將 Web 應用程式部署至 Azure App Service 的程序。</span><span class="sxs-lookup"><span data-stu-id="68d70-104">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="68d70-105">本文示範如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將範例 Spring Boot 應用程式部署至 Azure App Services。</span><span class="sxs-lookup"><span data-stu-id="68d70-105">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="68d70-106">適用於 Azure Web 應用程式的 Maven 外掛程式目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="68d70-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="68d70-107">雖然未來計劃有額外功能，但是現在僅支援 FTP 發佈。</span><span class="sxs-lookup"><span data-stu-id="68d70-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="68d70-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="68d70-108">Prerequisites</span></span>

<span data-ttu-id="68d70-109">若要完成本教學課程中的步驟，您必須具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="68d70-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="68d70-110">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="68d70-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="68d70-111">[Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="68d70-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="68d70-112">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="68d70-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="68d70-113">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="68d70-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="68d70-114">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="68d70-114">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="68d70-115">複製範例 Spring Boot Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="68d70-115">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="68d70-116">在本節中，您會在本機複製已完成 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="68d70-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="68d70-117">開啟命令提示字元或終端機視窗，並建立本機目錄來保存您的 Spring Boot 應用程式，然後變更至該目錄；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-117">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="68d70-118">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="68d70-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="68d70-119">將 [Spring Boot Getting Started] 範例專案複製到您建立的目錄中；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-119">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="68d70-120">將目錄變更至已完成的專案；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="68d70-121">使用 Maven 建立 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-121">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="68d70-122">建立 Web 應用程式後，使用 Maven 啟動 Web 應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-122">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="68d70-123">測試 Web 應用程式，方法是使用網頁瀏覽器在本機瀏覽它。</span><span class="sxs-lookup"><span data-stu-id="68d70-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="68d70-124">例如，如果您有 curl 可用，可以使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="68d70-124">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="68d70-125">您應該會看到顯示下列訊息：**Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="68d70-125">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="68d70-126">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="68d70-126">Create an Azure service principal</span></span>

<span data-ttu-id="68d70-127">在本節中，您建立 Azure 服務主體，Maven 外掛程式會在將您的 Web 應用程式部署至 Azure 時使用該服務主體。</span><span class="sxs-lookup"><span data-stu-id="68d70-127">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="68d70-128">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="68d70-128">Open a command prompt.</span></span>

1. <span data-ttu-id="68d70-129">使用 Azure CLI 登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="68d70-129">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="68d70-130">依照指示完成登入程序。</span><span class="sxs-lookup"><span data-stu-id="68d70-130">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="68d70-131">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="68d70-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="68d70-132">其中 `uuuuuuuu` 是使用者名稱，`pppppppp` 是服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="68d70-132">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="68d70-133">Azure 使用 JSON 回應，類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="68d70-133">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="68d70-134">當您設定 Maven 外掛程式以將您的 Web 應用程式部署至 Azure 時，您會使用此 JSON 回應中的值。</span><span class="sxs-lookup"><span data-stu-id="68d70-134">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="68d70-135">`aaaaaaaa`、`uuuuuuuu`、`pppppppp` 和 `tttttttt` 是預留位置值，在此範例中使用，在您於下一節設定 Maven `settings.xml` 檔案時，更方便將這些值對應至個別元素。</span><span class="sxs-lookup"><span data-stu-id="68d70-135">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="68d70-136">設定 Maven 以使用您的 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="68d70-136">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="68d70-137">在本節中，您使用 Azure 服務主體的值，設定將您的 Web 應用程式部署至 Azure 時，Maven 使用的驗證。</span><span class="sxs-lookup"><span data-stu-id="68d70-137">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="68d70-138">在文字編輯器中開啟您的 Maven`settings.xml` 檔案，這個檔案可能在如下列範例的路徑中：</span><span class="sxs-lookup"><span data-stu-id="68d70-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="68d70-139">將本教學課程上一節的 Azure 服務主體設定新增至 settings.xml 檔案中的 `<servers>` 集合；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-139">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="68d70-140">其中：</span><span class="sxs-lookup"><span data-stu-id="68d70-140">Where:</span></span>
   <span data-ttu-id="68d70-141">元素</span><span class="sxs-lookup"><span data-stu-id="68d70-141">Element</span></span> | <span data-ttu-id="68d70-142">說明</span><span class="sxs-lookup"><span data-stu-id="68d70-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="68d70-143">指定將您的 Web 應用程式部署至 Azure 時，Maven 用來查閱安全性設定的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="68d70-143">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="68d70-144">包含服務主體的 `appId` 值。</span><span class="sxs-lookup"><span data-stu-id="68d70-144">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="68d70-145">包含服務主體的 `tenant` 值。</span><span class="sxs-lookup"><span data-stu-id="68d70-145">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="68d70-146">包含服務主體的 `password` 值。</span><span class="sxs-lookup"><span data-stu-id="68d70-146">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="68d70-147">定義目標 Azure 雲端環境，也就是此範例中的 `AZURE`。</span><span class="sxs-lookup"><span data-stu-id="68d70-147">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="68d70-148">(環境的完整清單可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得)</span><span class="sxs-lookup"><span data-stu-id="68d70-148">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="68d70-149">儲存並關閉 settings.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="68d70-149">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="68d70-150">選擇性：將您的 Web 應用程式部署至 Azure 之前自訂 pom.xml</span><span class="sxs-lookup"><span data-stu-id="68d70-150">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="68d70-151">在文字編輯器中開啟 Spring Boot 應用程式的 `pom.xml` 檔案，然後找出 `azure-webapp-maven-plugin` 的 `<plugin>` 元素。</span><span class="sxs-lookup"><span data-stu-id="68d70-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="68d70-152">此元素外觀會類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="68d70-152">This element should resemble the following example:</span></span>

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

<span data-ttu-id="68d70-153">您可以為 Maven 外掛程式修改數個值，這些元素的詳細描述可於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件中取得。</span><span class="sxs-lookup"><span data-stu-id="68d70-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="68d70-154">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="68d70-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="68d70-155">元素</span><span class="sxs-lookup"><span data-stu-id="68d70-155">Element</span></span> | <span data-ttu-id="68d70-156">說明</span><span class="sxs-lookup"><span data-stu-id="68d70-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="68d70-157">指定[適用於 Azure Web 應用程式的 Maven 外掛程式]版本。</span><span class="sxs-lookup"><span data-stu-id="68d70-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="68d70-158">您應該檢查 [Maven 中央存放庫](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)中所列的版本，確定您使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="68d70-158">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="68d70-159">指定 Azure 的驗證資訊，在此範例中包含 `<serverId>` 元素，其中包含 `azure-auth`，Maven 使用該值來查閱 Maven settings.xml 檔案 (您在本文稍早章節中定義) 中的 Azure 服務主體值。</span><span class="sxs-lookup"><span data-stu-id="68d70-159">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="68d70-160">指定目標資源群組，也就是此範例中的 `maven-plugin`。</span><span class="sxs-lookup"><span data-stu-id="68d70-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="68d70-161">如果該資源群組不存在，則系統會在部署期間建立它。</span><span class="sxs-lookup"><span data-stu-id="68d70-161">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="68d70-162">指定 Web 應用程式的目標名稱。</span><span class="sxs-lookup"><span data-stu-id="68d70-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="68d70-163">在此範例中，目標名稱是 `maven-web-app-${maven.build.timestamp}`，在此範例中會附加 `${maven.build.timestamp}` 尾碼以避免發生衝突。</span><span class="sxs-lookup"><span data-stu-id="68d70-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="68d70-164">(時間戳記是選擇性的；您可以為應用程式名稱指定任何唯一的字串。)</span><span class="sxs-lookup"><span data-stu-id="68d70-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="68d70-165">指定目標區域，在此範例中是 `westus`。</span><span class="sxs-lookup"><span data-stu-id="68d70-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="68d70-166">(完整清單位於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="68d70-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="68d70-167">指定 Web 應用程式的 Java 執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="68d70-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="68d70-168">(完整清單位於[適用於 Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="68d70-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="68d70-169">指定 Web 應用程式的部署類型。</span><span class="sxs-lookup"><span data-stu-id="68d70-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="68d70-170">雖然其他部署類型的支援正在開發中，現在只有 `ftp` 受到支援。</span><span class="sxs-lookup"><span data-stu-id="68d70-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="68d70-171">指定當 Maven 將 Web 應用程式部署至 Azure 時使用的資源和目標目的地。</span><span class="sxs-lookup"><span data-stu-id="68d70-171">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="68d70-172">在此範例中，兩個 `<resource>` 元素會指定 Maven 將會部署 Web 應用程式的 JAR 檔案和 Spring Boot 專案的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="68d70-172">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="68d70-173">建置 Web 應用程式並將其部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="68d70-173">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="68d70-174">一旦您已設定本文上述章節中的所有設定，您已準備好將 Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="68d70-174">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="68d70-175">若要這樣做，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="68d70-175">To do so, use the following steps:</span></span>

1. <span data-ttu-id="68d70-176">如果您對 pom.xml 檔案進行任何變更，從您稍早使用的命令提示字元或終端機視窗，使用 Maven 重新建置 JAR 檔案；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-176">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="68d70-177">使用 Maven 將您的 Web 應用程式部署至 Azure；例如：</span><span class="sxs-lookup"><span data-stu-id="68d70-177">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="68d70-178">Maven 會將您的 Web 應用程式部署至 Azure；如果 Web 應用程式不存在，系統會加以建立。</span><span class="sxs-lookup"><span data-stu-id="68d70-178">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="68d70-179">已部署您的網站時，您就可以使用 [Azure 入口網站]來管理它。</span><span class="sxs-lookup"><span data-stu-id="68d70-179">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="68d70-180">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="68d70-180">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="68d70-182">Web 應用程式的 URL 會列在 Web 應用程式的 [概觀] 中：</span><span class="sxs-lookup"><span data-stu-id="68d70-182">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="68d70-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68d70-184">Next steps</span></span>

<span data-ttu-id="68d70-185">如需本文所討論之各種技術的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="68d70-185">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="68d70-186">[適用於 Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="68d70-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="68d70-187">從 Azure CLI 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="68d70-187">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="68d70-188">如何使用適用於 Azure Web 應用程式的 Maven 外掛程式，將容器化 Spring Boot 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="68d70-188">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="68d70-189">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="68d70-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="68d70-190">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="68d70-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

<span data-ttu-id="68d70-191">[Azure 命令列介面 (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="68d70-191">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
<span data-ttu-id="68d70-192">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="68d70-192">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="68d70-193">[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="68d70-193">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="68d70-194">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="68d70-194">[Git]: https://github.com/</span></span>
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
<span data-ttu-id="68d70-195">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="68d70-195">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="68d70-196">[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="68d70-196">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
[Spring Boot]: http://projects.spring.io/spring-boot/
<span data-ttu-id="68d70-197">[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="68d70-197">[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot</span></span>
[Spring Framework]: https://spring.io/
<span data-ttu-id="68d70-198">[適用於 Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span><span class="sxs-lookup"><span data-stu-id="68d70-198">[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin</span></span>

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
