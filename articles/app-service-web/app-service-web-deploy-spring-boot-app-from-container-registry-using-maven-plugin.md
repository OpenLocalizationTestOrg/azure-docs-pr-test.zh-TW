---
title: "Azure Web Apps toodeploy Azure 容器登錄中 tooAzure App Service 中的 Spring 開機應用程式的 aaaHow toouse hello Maven 外掛程式"
description: "本教學課程將逐步引導您透過 hello 步驟 toodeploy Spring 開機應用程式在容器登錄中 Azure tooAzure tooAzure App Service 中使用 Maven 外掛程式。"
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
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="75ca6-103">如何 toouse hello Maven 外掛程式 Azure Web Apps toodeploy Azure 容器登錄中 tooAzure App Service 中的 Spring 開機應用程式</span><span class="sxs-lookup"><span data-stu-id="75ca6-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="75ca6-104">hello  **[Spring 架構]**是熱門的開放原始碼架構，可協助建立 web、 行動裝置版及 API 應用程式的 Java 開發人員。</span><span class="sxs-lookup"><span data-stu-id="75ca6-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="75ca6-105">本教學課程使用範例應用程式使用建立[Spring 開機]，慣例導向的方式使用 Spring tooget 快速入門。</span><span class="sxs-lookup"><span data-stu-id="75ca6-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="75ca6-106">本文示範如何 toodeploy 範例 Spring 開機應用程式 tooAzure 容器登錄，然後使用 hello Maven 外掛程式 Azure Web Apps toodeploy 您應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="75ca6-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="75ca6-107">hello Azure Web 應用程式的 Maven 外掛程式是目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="75ca6-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="75ca6-108">現在，只有 FTP 發行支援，雖然 hello 未來計劃的額外功能。</span><span class="sxs-lookup"><span data-stu-id="75ca6-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="75ca6-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="75ca6-109">Prerequisites</span></span>

<span data-ttu-id="75ca6-110">在順序 toocomplete hello 步驟本教學課程中，您需要下列必要條件 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="75ca6-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="75ca6-111">Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="75ca6-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="75ca6-112">hello [Azure 命令列介面 (CLI)]。</span><span class="sxs-lookup"><span data-stu-id="75ca6-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="75ca6-113">最新的 [Java 開發套件 (JDK)] 1.7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="75ca6-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="75ca6-114">Apache 的 [Maven] 建置工具 (第 3 版)。</span><span class="sxs-lookup"><span data-stu-id="75ca6-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="75ca6-115">[Git] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="75ca6-115">A [Git] client.</span></span>
* <span data-ttu-id="75ca6-116">[Docker] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="75ca6-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="75ca6-117">Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。</span><span class="sxs-lookup"><span data-stu-id="75ca6-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="75ca6-118">Docker web 應用程式上的複製 hello 範例 Spring 開機</span><span class="sxs-lookup"><span data-stu-id="75ca6-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="75ca6-119">在本節中，您會在本機複製容器化 Spring Boot 應用程式，並且進行測試。</span><span class="sxs-lookup"><span data-stu-id="75ca6-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="75ca6-120">開啟命令提示字元或終端機視窗，並建立本機目錄 toohold 您 Spring 開機應用程式，並變更 toothat 目錄;例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="75ca6-121">-- 或 --</span><span class="sxs-lookup"><span data-stu-id="75ca6-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="75ca6-122">複製 hello[上開始使用 Docker Spring 開機]範例專案到 hello 目錄，您所建立的; 例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="75ca6-123">變更目錄已完成的 toohello 專案;例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="75ca6-124">建置使用 Maven; hello JAR 檔案例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="75ca6-125">Hello web 應用程式建立後，開始使用 Maven; hello web 應用程式例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="75ca6-126">藉由瀏覽 tooit 使用網頁瀏覽器，在本機測試 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75ca6-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="75ca6-127">例如，您可以使用下列命令，如果您有可用的 curl hello:</span><span class="sxs-lookup"><span data-stu-id="75ca6-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="75ca6-128">您應該會看到下列訊息顯示 hello: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="75ca6-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="75ca6-130">建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="75ca6-130">Create an Azure service principal</span></span>

<span data-ttu-id="75ca6-131">在本節中，您建立 Azure 部署容器 tooAzure 時 hello Maven 外掛程式使用的服務主體。</span><span class="sxs-lookup"><span data-stu-id="75ca6-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="75ca6-132">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="75ca6-132">Open a command prompt.</span></span>

1. <span data-ttu-id="75ca6-133">登入您的 Azure 帳戶使用 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="75ca6-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="75ca6-134">請遵循 hello 指示 toocomplete hello 登入程序。</span><span class="sxs-lookup"><span data-stu-id="75ca6-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="75ca6-135">建立 Azure 服務主體：</span><span class="sxs-lookup"><span data-stu-id="75ca6-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="75ca6-136">其中`uuuuuuuu`是 hello 的使用者名稱和`pppppppp`hello hello 服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="75ca6-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="75ca6-137">Azure 會使用類似下列範例中的 hello 的 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="75ca6-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="75ca6-138">當您設定 hello Maven 外掛程式 toodeploy 容器 tooAzure 時，您將使用此 JSON 回應 hello 值。</span><span class="sxs-lookup"><span data-stu-id="75ca6-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="75ca6-139">hello `aaaaaaaa`， `uuuuuuuu`， `pppppppp`，和`tttttttt`預留位置的值，也就是用於此範例 toomake 它更容易 toomap 這些 tootheir 個別項目的值設定您的 Maven 時`settings.xml`hello 中檔案的下一步一節。</span><span class="sxs-lookup"><span data-stu-id="75ca6-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="75ca6-140">建立 Azure 容器登錄中使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="75ca6-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="75ca6-141">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="75ca6-141">Open a command prompt.</span></span>

1. <span data-ttu-id="75ca6-142">Azure 帳戶登入 tooyour 中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="75ca6-143">建立資源群組 hello Azure 資源，您將使用本文章中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="75ca6-144">將此範例中的 `wingtiptoysresources` 取代為資源群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="75ca6-145">Hello Spring 開機應用程式的資源群組中建立私人 Azure 容器登錄中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="75ca6-146">將此範例中的 `wingtiptoysregistry` 取代為容器登錄的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="75ca6-147">擷取您容器登錄中的 hello 密碼：</span><span class="sxs-lookup"><span data-stu-id="75ca6-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="75ca6-148">Azure 會回應您的密碼，例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="75ca6-149">加入您的 Azure 容器登錄和 Azure 服務主體 tooyour Maven 設定</span><span class="sxs-lookup"><span data-stu-id="75ca6-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="75ca6-150">開啟您的 Maven`settings.xml`檔案文字編輯器中; 這個檔案可能是路徑，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="75ca6-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="75ca6-151">從這個發行項 toohello hello 上一節中加入您 Azure 容器登錄中的存取設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="75ca6-152">其中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-152">Where:</span></span>
   <span data-ttu-id="75ca6-153">元素</span><span class="sxs-lookup"><span data-stu-id="75ca6-153">Element</span></span> | <span data-ttu-id="75ca6-154">說明</span><span class="sxs-lookup"><span data-stu-id="75ca6-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="75ca6-155">包含私用 Azure 容器登錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="75ca6-156">包含私用 Azure 容器登錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="75ca6-157">包含您擷取 hello 這個發行項的上一節中的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="75ca6-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="75ca6-158">從這個發行項 toohello 前一節中新增您的 Azure 服務主體設定`<servers>`中 hello 集合*settings.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="75ca6-159">其中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-159">Where:</span></span>
   <span data-ttu-id="75ca6-160">元素</span><span class="sxs-lookup"><span data-stu-id="75ca6-160">Element</span></span> | <span data-ttu-id="75ca6-161">說明</span><span class="sxs-lookup"><span data-stu-id="75ca6-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="75ca6-162">指定 Maven 使用 toolook 註冊您的安全性設定，當您部署您的 web 應用程式 tooAzure 的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="75ca6-163">包含 hello`appId`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="75ca6-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="75ca6-164">包含 hello`tenant`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="75ca6-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="75ca6-165">包含 hello`password`從您的服務主體的值。</span><span class="sxs-lookup"><span data-stu-id="75ca6-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="75ca6-166">定義 hello 目標 Azure 雲端環境，也就是`AZURE`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="75ca6-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="75ca6-167">(環境的完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件)</span><span class="sxs-lookup"><span data-stu-id="75ca6-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="75ca6-168">儲存並關閉 hello *settings.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="75ca6-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="75ca6-169">建置您的 Docker 容器映像，並將它推送 tooyour Azure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="75ca6-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="75ca6-170">瀏覽 Spring 開機應用程式，完成 toohello 專案目錄 （例如：「*C:\SpringBoot\gs-spring-boot-docker\complete*「 或 」*/users/robert/SpringBoot/gs-spring-boot-docker/complete*")，並開啟 hello *pom.xml*檔案文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="75ca6-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="75ca6-171">更新 hello`<properties>`中 hello 集合*pom.xml*檔案 hello 登入伺服器的值具有 Azure 容器登錄 hello 前一節，本教學課程; 例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="75ca6-172">其中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-172">Where:</span></span>
   <span data-ttu-id="75ca6-173">元素</span><span class="sxs-lookup"><span data-stu-id="75ca6-173">Element</span></span> | <span data-ttu-id="75ca6-174">說明</span><span class="sxs-lookup"><span data-stu-id="75ca6-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="75ca6-175">指定私用 Azure 容器登錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="75ca6-176">指定您私人 Azure 容器登錄中，藉由附加衍生 hello URL 」。 azurecr.io"toohello 私用容器登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="75ca6-177">確認`<plugin>`hello Docker 外掛程式中的程式*pom.xml*檔案包含本教學課程中的 hello hello 登入伺服器位址和登錄名稱的 hello 先前步驟中正確的屬性。</span><span class="sxs-lookup"><span data-stu-id="75ca6-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="75ca6-178">例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-178">For example:</span></span>

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
   <span data-ttu-id="75ca6-179">其中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-179">Where:</span></span>
   <span data-ttu-id="75ca6-180">元素</span><span class="sxs-lookup"><span data-stu-id="75ca6-180">Element</span></span> | <span data-ttu-id="75ca6-181">說明</span><span class="sxs-lookup"><span data-stu-id="75ca6-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="75ca6-182">指定 hello 屬性，其中包含私用 Azure 容器登錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="75ca6-183">指定 hello 屬性，其中包含私用 Azure 容器登錄 hello URL。</span><span class="sxs-lookup"><span data-stu-id="75ca6-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="75ca6-184">瀏覽 toohello 完成 Spring 開機應用程式的專案目錄並執行下列命令 toorebuild hello 應用程式的 hello 並推送 hello 容器 tooyour Azure 容器登錄中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="75ca6-185">選擇性： 瀏覽 toohello [Azure 入口網站]，並確認名為 Docker 容器映像**gs spring 開機-docker**容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="75ca6-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![確認在 Azure 入口網站中的容器][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="75ca6-187">自訂您 pom.xml，然後建立及部署容器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="75ca6-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="75ca6-188">開啟 hello`pom.xml`在文字編輯器中，應用程式 Spring 開機檔案，然後找出 hello`<plugin>`元素`azure-webapp-maven-plugin`。</span><span class="sxs-lookup"><span data-stu-id="75ca6-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="75ca6-189">這個項目應該類似下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="75ca6-189">This element should resemble hello following example:</span></span>

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

<span data-ttu-id="75ca6-190">有數個值，您可以修改 hello Maven 外掛程式，而且每個這些元件的詳細的描述在 hello [Azure Web 應用程式的 Maven 外掛程式]文件。</span><span class="sxs-lookup"><span data-stu-id="75ca6-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="75ca6-191">也就是說，有數個值值得在這篇文章中反白顯示：</span><span class="sxs-lookup"><span data-stu-id="75ca6-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="75ca6-192">元素</span><span class="sxs-lookup"><span data-stu-id="75ca6-192">Element</span></span> | <span data-ttu-id="75ca6-193">說明</span><span class="sxs-lookup"><span data-stu-id="75ca6-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="75ca6-194">指定 hello 版的 hello [Azure Web 應用程式的 Maven 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="75ca6-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="75ca6-195">您應該檢查 hello 版本列在 hello [Maven 中央儲存機制](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)您使用的 tooensure hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="75ca6-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="75ca6-196">指定 Azure，這在此範例中包含的 hello 驗證資訊`<serverId>`包含項目`azure-auth`;Maven 使用 hello Azure 服務主體值的值 toolook 中您 Maven *settings.xml*在本文的前一節中所定義的檔案。</span><span class="sxs-lookup"><span data-stu-id="75ca6-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="75ca6-197">指定 hello 目標資源群組，也就是`wingtiptoysresources`在此範例中。</span><span class="sxs-lookup"><span data-stu-id="75ca6-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="75ca6-198">會在部署期間建立 hello 資源群組，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="75ca6-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="75ca6-199">指定 web 應用程式的 hello 目標名稱。</span><span class="sxs-lookup"><span data-stu-id="75ca6-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="75ca6-200">在此範例中，是 hello 目標名稱`maven-linux-app-${maven.build.timestamp}`，其中 hello`${maven.build.timestamp}`尾碼會附加在這個範例 tooavoid 衝突。</span><span class="sxs-lookup"><span data-stu-id="75ca6-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="75ca6-201">（hello 時間戳記是選擇性的; 您可以指定任何唯一的字串 hello 應用程式名稱）。</span><span class="sxs-lookup"><span data-stu-id="75ca6-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="75ca6-202">指定 hello 目標區域，而在此範例中`westus`。</span><span class="sxs-lookup"><span data-stu-id="75ca6-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="75ca6-203">(完整清單位於 hello [Azure Web 應用程式的 Maven 外掛程式]文件。)</span><span class="sxs-lookup"><span data-stu-id="75ca6-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="75ca6-204">指定包含 hello 名稱和您的容器 URL 的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="75ca6-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="75ca6-205">部署您的 web 應用程式 tooAzure 時，請指定 Maven toouse 任何唯一的設定。</span><span class="sxs-lookup"><span data-stu-id="75ca6-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="75ca6-206">在此範例中，`<property>`元素包含子元素，指定您的應用程式的 hello 連接埠的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="75ca6-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="75ca6-207">從 hello 預設變更 hello 連接埠時，才需要 hello 設定 toochange hello 連接埠號碼在此範例中。</span><span class="sxs-lookup"><span data-stu-id="75ca6-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="75ca6-208">從 hello 命令提示字元或稍早所使用的終端機視窗，重建 hello JAR 檔案，如果您進行任何變更 toohello 使用 Maven *pom.xml*檔案; 例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="75ca6-209">部署您的 web 應用程式 tooAzure 使用 Maven;例如：</span><span class="sxs-lookup"><span data-stu-id="75ca6-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="75ca6-210">Maven 會部署您的 web 應用程式 tooAzure;如果 hello web 應用程式不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="75ca6-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="75ca6-211">如果您指定在 hello hello 區`<region>`元素您*pom.xml*檔案沒有足夠可用的伺服器進行部署時，您可能會看到錯誤類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="75ca6-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="75ca6-212">如果發生這種情況，您可以指定另一個區域，然後重新執行 hello Maven 命令 toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="75ca6-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="75ca6-213">已部署您的網站，將無法 toomanage 它使用 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="75ca6-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="75ca6-214">您的 Web 應用程式會列在**應用程式服務** 中：</span><span class="sxs-lookup"><span data-stu-id="75ca6-214">Your web app will be listed in **App Services**:</span></span>

   ![列在 Azure 入口網站應用程式服務中的 Web 應用程式][AP01]

* <span data-ttu-id="75ca6-216">Hello URL 的 web 應用程式將會列在 hello 和**概觀**web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="75ca6-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![決定您 web 應用程式的 hello URL][AP02]

## <a name="next-steps"></a><span data-ttu-id="75ca6-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75ca6-218">Next steps</span></span>

<span data-ttu-id="75ca6-219">如需有關 hello 本文所討論的各種技術，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="75ca6-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="75ca6-220">[Azure Web 應用程式的 Maven 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="75ca6-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="75ca6-221">登入從 hello Azure CLI tooAzure</span><span class="sxs-lookup"><span data-stu-id="75ca6-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="75ca6-222">使用 Azure CLI 2.0 來建立 Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="75ca6-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="75ca6-223">Maven 設定參考</span><span class="sxs-lookup"><span data-stu-id="75ca6-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="75ca6-224">[適用於 Maven 的 Docker 外掛程式]</span><span class="sxs-lookup"><span data-stu-id="75ca6-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure 入口網站]: https://portal.azure.com/
[Azure Web 應用程式的 Maven 外掛程式]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[適用於 Maven 的 Docker 外掛程式]: https://github.com/spotify/docker-maven-plugin
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[上開始使用 Docker Spring 開機]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
