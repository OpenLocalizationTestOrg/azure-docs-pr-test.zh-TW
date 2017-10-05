---
title: "使用 Jenkins 來執行 Azure CLI | Microsoft Docs"
description: "了解如何在 Jenkins 管線中使用 Azure CLI 將 Java Web 應用程式部署到 Azure"
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
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="95446-103">使用 Jenkins 和 Azure CLI 來部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="95446-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="95446-104">若要將 Java Web 應用程式部署到 Azure，您可以在 [Jenkins 管線](https://jenkins.io/doc/book/pipeline/)中使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="95446-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="95446-105">在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰</span><span class="sxs-lookup"><span data-stu-id="95446-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95446-106">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="95446-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="95446-107">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="95446-107">Configure Jenkins</span></span>
> * <span data-ttu-id="95446-108">在 Azure 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="95446-109">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="95446-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="95446-110">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="95446-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="95446-111">執行管線並確認 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="95446-112">本教學課程需要 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="95446-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="95446-113">若要尋找版本，請執行 `az --version`。</span><span class="sxs-lookup"><span data-stu-id="95446-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="95446-114">如果您需要升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="95446-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="95446-115">建立及設定 Jenkins 執行個體</span><span class="sxs-lookup"><span data-stu-id="95446-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="95446-116">如果您還沒有 Jenkins Master，請從[解決方案範本](install-jenkins-solution-template.md)開始著手，此範本包含預設必要的 [Azure 認證](https://plugins.jenkins.io/azure-credentials)外掛程式。</span><span class="sxs-lookup"><span data-stu-id="95446-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="95446-117">「Azure 認證」外掛程式可讓您將 Microsoft Azure 服務主體認證儲存在 Jenkins 中。</span><span class="sxs-lookup"><span data-stu-id="95446-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="95446-118">在 1.2 版中，我們已新增支援，因此 Jenkins 管線可以取得 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="95446-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="95446-119">請確定您擁有的版本是 1.2 或更新版本：</span><span class="sxs-lookup"><span data-stu-id="95446-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="95446-120">在 Jenkins 儀表板中，按一下 [Manage Jenkins] \(管理 Jenkins\) -> [Plugin Manager] \(外掛程式管理員\)，然後搜尋 [Azure Credential] \(Azure 認證\)。</span><span class="sxs-lookup"><span data-stu-id="95446-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="95446-121">如果版本比 1.2 版舊，請更新外掛程式。</span><span class="sxs-lookup"><span data-stu-id="95446-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="95446-122">Jenkins Master 中也必須有 Java JDK 和 Maven。</span><span class="sxs-lookup"><span data-stu-id="95446-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="95446-123">若要安裝，請使用 SSH 來登入 Jenkins Master，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="95446-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="95446-124">將 Azure 服務主體新增到 Jenkins 認證</span><span class="sxs-lookup"><span data-stu-id="95446-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="95446-125">必須要有 Azure 認證，才能執行 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="95446-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="95446-126">在 Jenkins 儀表板中，按一下 [Credentials] \(認證\) -> [System] \(系統\) -> 。</span><span class="sxs-lookup"><span data-stu-id="95446-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="95446-127">按一下 [Global credentials(unrestricted)] \(全域認證 (不受限)\)。</span><span class="sxs-lookup"><span data-stu-id="95446-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="95446-128">按一下 [Add Credentials] \(新增認證\) 來填寫 [Subscription ID] \(訂用帳戶 ID\)、[Client ID] \(用戶端識別碼\)、[Client Secret] \(用戶端祕密\) 及 [OAuth 2.0 Token Endpoint] \(OAuth 2.0 權杖端點\)，以新增 [Microsoft Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="95446-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="95446-129">請提供一個要在後續步驟中使用的識別碼。</span><span class="sxs-lookup"><span data-stu-id="95446-129">Provide an ID for use in subsequent step.</span></span>

![新增認證](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="95446-131">建立 Azure App Service 來部署 Java Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="95446-132">使用 [az appservice plan create](/cli/azure/appservice/plan#create) CLI 命令，建立搭配**免費**定價層的 Azure App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="95446-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="95446-133">Appservice 方案會定義用來託管應用程式的實體資源。</span><span class="sxs-lookup"><span data-stu-id="95446-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="95446-134">所有指派給 Appservice 方案的應用程式都會共用這些資源，從而讓您節省託管多個應用程式的成本。</span><span class="sxs-lookup"><span data-stu-id="95446-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="95446-135">方案準備妥當時，Azure CLI 會顯示類似下列範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="95446-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="95446-136">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-136">Create an Azure Web app</span></span>

 <span data-ttu-id="95446-137">使用 [az webapp create](/cli/azure/appservice/web#create) CLI 命令，在 `myAppServicePlan` App Service 方案中建立 Web 應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="95446-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="95446-138">Web 應用程式定義會提供一個 URL 以存取您的應用程式，並設定數個選項將您的程式碼部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="95446-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="95446-139">使用您自己的唯一應用程式名稱來取代 `<app_name>` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="95446-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="95446-140">這個唯一名稱會是 Web 應用程式預設網域名稱的一部分，因此，這個名稱在 Azure 的所有應用程式中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="95446-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="95446-141">您可以先將自訂的網域名稱項目對應至 Web 應用程式，再將它公開給使用者。</span><span class="sxs-lookup"><span data-stu-id="95446-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="95446-142">Web 應用程式定義備妥之後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="95446-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="95446-143">設定 Java</span><span class="sxs-lookup"><span data-stu-id="95446-143">Configure Java</span></span> 

<span data-ttu-id="95446-144">使用 [az appservice web config update](/cli/azure/appservice/web/config#update) 命令來設定您的應用程式需要的 Java 執行階段組態。</span><span class="sxs-lookup"><span data-stu-id="95446-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="95446-145">下列命令會將 Web 應用程式設定為在最新的 Java 8 JDK 和 [Apache Tomcat](http://tomcat.apache.org/) 8.0 上執行。</span><span class="sxs-lookup"><span data-stu-id="95446-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="95446-146">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="95446-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="95446-147">開啟[適用於 Azure 的簡單 Java Web 應用程式](https://github.com/azure-devops/javawebappsample)存放庫。</span><span class="sxs-lookup"><span data-stu-id="95446-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="95446-148">為了將存放庫分支至您自己的 GitHub 帳戶，按一下右上角的 [分支] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95446-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="95446-149">在 GitHub Web UI 中，開啟 **Jenkinsfile** 檔案。</span><span class="sxs-lookup"><span data-stu-id="95446-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="95446-150">按一下鉛筆圖示來編輯此檔案，更新您 Web 應用程式的資源群組和名稱 (分別位於第 20 行和第 21 行)。</span><span class="sxs-lookup"><span data-stu-id="95446-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="95446-151">變更第 23 行以更新您 Jenkins 執行個體中的認證識別碼</span><span class="sxs-lookup"><span data-stu-id="95446-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="95446-152">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="95446-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="95446-153">在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。</span><span class="sxs-lookup"><span data-stu-id="95446-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="95446-154">為作業提供一個名稱，然後選取 [Pipeline] \(管線\)。</span><span class="sxs-lookup"><span data-stu-id="95446-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="95446-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="95446-155">Click **OK**.</span></span>
* <span data-ttu-id="95446-156">接著，按一下 [Pipeline] \(管線\) 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="95446-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="95446-157">針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。</span><span class="sxs-lookup"><span data-stu-id="95446-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="95446-158">針對 [SCM]，選取 [Git]。</span><span class="sxs-lookup"><span data-stu-id="95446-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="95446-159">輸入您分支存放庫的 GitHub URL：https:\<您的分支存放庫\>.git</span><span class="sxs-lookup"><span data-stu-id="95446-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="95446-160">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="95446-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="95446-161">測試您的管線</span><span class="sxs-lookup"><span data-stu-id="95446-161">Test your pipeline</span></span>
* <span data-ttu-id="95446-162">移至您建立的管線，按一下 [Build Now] \(立即建置\)</span><span class="sxs-lookup"><span data-stu-id="95446-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="95446-163">應該在幾秒內就會順利完成一個組建，您可以移至該組建，然後按一下 [Console Output] \(主控台輸出\) 來查看詳細資料</span><span class="sxs-lookup"><span data-stu-id="95446-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="95446-164">確認您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-164">Verify your web app</span></span>
<span data-ttu-id="95446-165">若要確認 WAR 檔案是否已順利部署到您的 Web 應用程式，</span><span class="sxs-lookup"><span data-stu-id="95446-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="95446-166">請開啟網頁瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="95446-166">Open a web browser:</span></span>

* <span data-ttu-id="95446-167">移至 http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="95446-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="95446-168">您會看見：</span><span class="sxs-lookup"><span data-stu-id="95446-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="95446-169">移至 http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (以任何數字取代 &lt;x> 和 &lt;y>) 以取得 x 和 y 的總和</span><span class="sxs-lookup"><span data-stu-id="95446-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![計算機：加法](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="95446-171">部署到 Linux 上的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="95446-172">既然您已知道如何在 Jenkins 管線中使用 Azure CLI，現在就可以修改指令碼來部署到 Linux 上的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95446-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="95446-173">Linux 上的 Web 應用程式支援不同的方式來進行部署，也就是使用 Docker。</span><span class="sxs-lookup"><span data-stu-id="95446-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="95446-174">若要部署，您必須提供一個 Dockerfile，此檔案會將您的 Web 應用程式與服務執行階段封裝成 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="95446-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="95446-175">外掛程式會接著建置該映像，將它推送到 Docker 登錄，然後將該映像部署到您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95446-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="95446-176">依照[這裡](/azure/app-service-web/app-service-linux-how-to-create-web-app)的步驟來建立在 Linux 上執行的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95446-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="95446-177">依照這篇[文章](https://docs.docker.com/engine/installation/linux/ubuntu/)中的指示，將 Docker 安裝在您的 Jenkins 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="95446-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="95446-178">使用[這裡](/azure/container-registry/container-registry-get-started-azure-cli)的步驟在 Azure 入口網站中建立「容器登錄」。</span><span class="sxs-lookup"><span data-stu-id="95446-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="95446-179">在您所分支的相同[適用於 Azure 的簡單 Java Web 應用程式](https://github.com/azure-devops/javawebappsample)存放庫中，編輯 **Jenkinsfile2** 檔案：</span><span class="sxs-lookup"><span data-stu-id="95446-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="95446-180">第 18 到 21 行：分別更新您的資源群組、Web 應用程式及 ACR。</span><span class="sxs-lookup"><span data-stu-id="95446-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="95446-181">第 24 行：將 \<azsrvprincipal\> 更新成您的認證識別碼</span><span class="sxs-lookup"><span data-stu-id="95446-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="95446-182">建立新的 Jenkins 管線，就像您在部署到 Windows 中的 Azure Web 應用程式時一樣，只是這次改用 **Jenkinsfile2**。</span><span class="sxs-lookup"><span data-stu-id="95446-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="95446-183">執行您的新作業。</span><span class="sxs-lookup"><span data-stu-id="95446-183">Run your new job.</span></span>
* <span data-ttu-id="95446-184">若要確認，請在 Azure CLI 中，執行：</span><span class="sxs-lookup"><span data-stu-id="95446-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="95446-185">您會收到下列結果︰</span><span class="sxs-lookup"><span data-stu-id="95446-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="95446-186">移至 http://&lt;app_name>.azurewebsites.net/api/calculator/ping。</span><span class="sxs-lookup"><span data-stu-id="95446-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="95446-187">您會看見此訊息：</span><span class="sxs-lookup"><span data-stu-id="95446-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="95446-188">移至 http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (以任何數字取代 &lt;x> 和 &lt;y>) 以取得 x 和 y 的總和</span><span class="sxs-lookup"><span data-stu-id="95446-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="95446-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95446-189">Next steps</span></span>
<span data-ttu-id="95446-190">在本教學課程中，您已設定一個 Jenkins 管線，此管線會簽出 GitHub 存放庫中的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="95446-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="95446-191">請執行 Maven 來建置一個 WAR 檔案，然後使用 Azure CLI 來部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="95446-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="95446-192">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="95446-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95446-193">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="95446-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="95446-194">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="95446-194">Configure Jenkins</span></span>
> * <span data-ttu-id="95446-195">在 Azure 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="95446-196">準備 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="95446-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="95446-197">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="95446-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="95446-198">執行管線並確認 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="95446-198">Run the pipeline and verify the web app</span></span>
