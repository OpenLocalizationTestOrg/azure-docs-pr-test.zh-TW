---
title: "aaaExecute hello Azure CLI jenkins |Microsoft 文件"
description: "了解如何 toouse Azure CLI toodeploy Java web 應用程式 tooAzure Jenkins 管線中"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="413d4-103">部署應用程式服務與 Jenkins tooAzure 和 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="413d4-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="413d4-104">toodeploy Java web 應用程式 tooAzure，您可以使用 Azure CLI 中[Jenkins 管線](https://jenkins.io/doc/book/pipeline/)。</span><span class="sxs-lookup"><span data-stu-id="413d4-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="413d4-105">在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰</span><span class="sxs-lookup"><span data-stu-id="413d4-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="413d4-106">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="413d4-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="413d4-107">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="413d4-107">Configure Jenkins</span></span>
> * <span data-ttu-id="413d4-108">在 Azure 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="413d4-109">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="413d4-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="413d4-110">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="413d4-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="413d4-111">執行 hello 管線，並確認 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="413d4-112">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="413d4-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="413d4-113">toofind hello 版本，執行`az --version`。</span><span class="sxs-lookup"><span data-stu-id="413d4-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="413d4-114">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="413d4-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="413d4-115">建立及設定 Jenkins 執行個體</span><span class="sxs-lookup"><span data-stu-id="413d4-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="413d4-116">如果您還沒有 Jenkins 主要，以 hello 開頭[方案範本](install-jenkins-solution-template.md)，其中包含所需的 hello [Azure 認證](https://plugins.jenkins.io/azure-credentials)預設的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="413d4-117">hello Azure 認證外掛程式可讓您 toostore Microsoft Azure 服務主體認證 Jenkins 中。</span><span class="sxs-lookup"><span data-stu-id="413d4-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="413d4-118">在 1.2 版中，我們會加入 hello 支援，因此該 Jenkins 管線可以取得 hello Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="413d4-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="413d4-119">請確定您擁有的版本是 1.2 或更新版本：</span><span class="sxs-lookup"><span data-stu-id="413d4-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="413d4-120">在 hello Jenkins 儀表板內，按一下**管理 Jenkins-> 外掛程式管理員->** 並搜尋**Azure 認證**。</span><span class="sxs-lookup"><span data-stu-id="413d4-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="413d4-121">如果 hello 版本早於 1.2，更新 hello 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="413d4-122">也需要 Java JDK 和 Maven hello Jenkins master 中。</span><span class="sxs-lookup"><span data-stu-id="413d4-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="413d4-123">tooinstall，登入使用 SSH tooJenkins master，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="413d4-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="413d4-124">加入 Azure 服務主體 tooJenkins 認證</span><span class="sxs-lookup"><span data-stu-id="413d4-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="413d4-125">Azure 的認證是需要的 tooexecute Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="413d4-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="413d4-126">在 hello Jenkins 儀表板內，按一下**認證-> 系統->** 。</span><span class="sxs-lookup"><span data-stu-id="413d4-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="413d4-127">按一下 [Global credentials(unrestricted)] \(全域認證 (不受限)\)。</span><span class="sxs-lookup"><span data-stu-id="413d4-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="413d4-128">按一下**新增認證**tooadd [Microsoft Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)填寫 hello 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點。</span><span class="sxs-lookup"><span data-stu-id="413d4-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="413d4-129">請提供一個要在後續步驟中使用的識別碼。</span><span class="sxs-lookup"><span data-stu-id="413d4-129">Provide an ID for use in subsequent step.</span></span>

![新增認證](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="413d4-131">建立 hello Java web 應用程式部署的 Azure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="413d4-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="413d4-132">建立 Azure App Service 方案以 hello**免費**定價層使用 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="413d4-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="413d4-133">hello 應用程式服務方案會定義 hello 使用的實體資源 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="413d4-134">指派 tooan 應用程式服務方案的所有應用程式共用這些資源，讓您 toosave 成本裝載多個應用程式時。</span><span class="sxs-lookup"><span data-stu-id="413d4-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="413d4-135">準備 hello 計劃時，Azure CLI 顯示類似的 hello 輸出 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="413d4-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="413d4-136">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-136">Create an Azure Web app</span></span>

 <span data-ttu-id="413d4-137">使用 hello [az webapp 建立](/cli/azure/appservice/web#create)CLI 命令 toocreate web 應用程式定義在 hello`myAppServicePlan`應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="413d4-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="413d4-138">hello web 應用程式定義您的應用程式提供 URL tooaccess，並設定數個選項 toodeploy 程式碼 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="413d4-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="413d4-139">替代 hello`<app_name>`預留位置自己唯一的應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="413d4-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="413d4-140">這個唯一名稱是 hello hello web 應用程式的預設網域名稱的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="413d4-141">公開 tooyour 使用者之前，您可以將自訂網域名稱項目 toohello web 應用程式的對應。</span><span class="sxs-lookup"><span data-stu-id="413d4-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="413d4-142">Hello web 應用程式定義就緒時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="413d4-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="413d4-143">設定 Java</span><span class="sxs-lookup"><span data-stu-id="413d4-143">Configure Java</span></span> 

<span data-ttu-id="413d4-144">設定您的應用程式需要具有 hello 的 hello Java 執行階段組態[az appservice web 組態更新](/cli/azure/appservice/web/config#update)命令。</span><span class="sxs-lookup"><span data-stu-id="413d4-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="413d4-145">hello 下列命令會設定 hello web 應用程式 toorun 上最近的 Java 8 JDK 和[Apache Tomcat](http://tomcat.apache.org/) 8.0。</span><span class="sxs-lookup"><span data-stu-id="413d4-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="413d4-146">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="413d4-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="413d4-147">開啟 hello[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="413d4-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="413d4-148">toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="413d4-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="413d4-149">在 GitHub Web UI 中，開啟 **Jenkinsfile** 檔案。</span><span class="sxs-lookup"><span data-stu-id="413d4-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="413d4-150">分別按一下 hello 鉛筆圖示 tooedit 此檔案 tooupdate hello 資源群組和 20 和 21 行上的 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="413d4-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="413d4-151">變更您 Jenkins 執行個體中的行 23 tooupdate 認證識別碼</span><span class="sxs-lookup"><span data-stu-id="413d4-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="413d4-152">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="413d4-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="413d4-153">在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。</span><span class="sxs-lookup"><span data-stu-id="413d4-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="413d4-154">提供 hello 工作的名稱，並選取**管線**。</span><span class="sxs-lookup"><span data-stu-id="413d4-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="413d4-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="413d4-155">Click **OK**.</span></span>
* <span data-ttu-id="413d4-156">按一下 hello**管線**索引標籤旁邊。</span><span class="sxs-lookup"><span data-stu-id="413d4-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="413d4-157">針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。</span><span class="sxs-lookup"><span data-stu-id="413d4-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="413d4-158">針對 [SCM]，選取 [Git]。</span><span class="sxs-lookup"><span data-stu-id="413d4-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="413d4-159">輸入您分岔的儲存機制的 hello GitHub URL: https:\<您分岔的儲存機制\>.git</span><span class="sxs-lookup"><span data-stu-id="413d4-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="413d4-160">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="413d4-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="413d4-161">測試您的管線</span><span class="sxs-lookup"><span data-stu-id="413d4-161">Test your pipeline</span></span>
* <span data-ttu-id="413d4-162">前往您所建立的 toohello 管線中，按一下**現在建置**</span><span class="sxs-lookup"><span data-stu-id="413d4-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="413d4-163">幾分鐘後，應該會成功建置，而且您可以移 toohello 組建，並按一下**主控台輸出**toosee hello 詳細資料</span><span class="sxs-lookup"><span data-stu-id="413d4-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="413d4-164">確認您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-164">Verify your web app</span></span>
<span data-ttu-id="413d4-165">已成功部署 tooverify hello WAR 檔案 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="413d4-166">請開啟網頁瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="413d4-166">Open a web browser:</span></span>

* <span data-ttu-id="413d4-167">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="413d4-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="413d4-168">您會看見：</span><span class="sxs-lookup"><span data-stu-id="413d4-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="413d4-169">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y</span><span class="sxs-lookup"><span data-stu-id="413d4-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![計算機：加法](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="413d4-171">部署 tooAzure Linux 上的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="413d4-172">您現在知道如何在您 Jenkins Azure CLI toouse 管線，您可以修改 hello 指令碼 toodeploy tooan on Linux 的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="413d4-173">Web 應用程式，在 Linux 上支援不同的方式 toodo hello 部署，也就是 toouse Docker。</span><span class="sxs-lookup"><span data-stu-id="413d4-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="413d4-174">toodeploy，您需要 tooprovide 將 Docker 映像封裝為 web 應用程式與服務執行階段的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="413d4-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="413d4-175">hello 外掛程式將再建置 hello 映像，直接將其推 tooa Docker 登錄和部署 hello 映像 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="413d4-176">請依照下列步驟 hello[這裡](/azure/app-service-web/app-service-linux-how-to-create-web-app)toocreate 在 Linux 上執行的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="413d4-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="413d4-177">Jenkins 執行個體上安裝 Docker，在這個 hello 指示[文章](https://docs.docker.com/engine/installation/linux/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="413d4-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="413d4-178">在 hello Azure 入口網站中建立容器登錄中，使用 hello 步驟[這裡](/azure/container-registry/container-registry-get-started-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="413d4-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="413d4-179">在 hello 相同[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)分叉時，儲存機制編輯 hello **Jenkinsfile2**檔案：</span><span class="sxs-lookup"><span data-stu-id="413d4-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="413d4-180">行 18-21，分別更新的資源群組、 web 應用程式，以及 ACR toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="413d4-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="413d4-181">第 24 行、 更新\<azsrvprincipal\> tooyour 認證識別碼</span><span class="sxs-lookup"><span data-stu-id="413d4-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="413d4-182">因為您未部署在 Windows 中，這個時間，使用 tooAzure web 應用程式時，建立新的 Jenkins 管線**Jenkinsfile2**改為。</span><span class="sxs-lookup"><span data-stu-id="413d4-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="413d4-183">執行您的新作業。</span><span class="sxs-lookup"><span data-stu-id="413d4-183">Run your new job.</span></span>
* <span data-ttu-id="413d4-184">tooverify，在 Azure CLI 執行：</span><span class="sxs-lookup"><span data-stu-id="413d4-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="413d4-185">您會收到 hello 下列結果：</span><span class="sxs-lookup"><span data-stu-id="413d4-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="413d4-186">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping。</span><span class="sxs-lookup"><span data-stu-id="413d4-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="413d4-187">您會看到 hello 訊息：</span><span class="sxs-lookup"><span data-stu-id="413d4-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="413d4-188">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y</span><span class="sxs-lookup"><span data-stu-id="413d4-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="413d4-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="413d4-189">Next steps</span></span>
<span data-ttu-id="413d4-190">在本教學課程中，您可以設定簽出 hello 原始碼 GitHub 儲存機制中的 Jenkins 管線。</span><span class="sxs-lookup"><span data-stu-id="413d4-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="413d4-191">執行 Maven toobuild war 檔案，然後使用 Azure CLI toodeploy tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="413d4-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="413d4-192">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="413d4-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="413d4-193">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="413d4-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="413d4-194">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="413d4-194">Configure Jenkins</span></span>
> * <span data-ttu-id="413d4-195">在 Azure 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="413d4-196">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="413d4-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="413d4-197">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="413d4-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="413d4-198">執行 hello 管線，並確認 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="413d4-198">Run hello pipeline and verify hello web app</span></span>
