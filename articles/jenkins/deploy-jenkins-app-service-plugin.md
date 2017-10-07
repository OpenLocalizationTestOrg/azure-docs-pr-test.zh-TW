---
title: "aaaDeploy tooAzure 使用 Jenkins 外掛程式的應用程式服務 |Microsoft 文件"
description: "了解如何 toouse Azure 應用程式服務 Jenkins 外掛程式 toodeploy Java web 應用程式 tooAzure Jenkins 中"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="be2cd-103">部署使用 Jenkins 外掛程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="be2cd-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="be2cd-104">toodeploy Java web 應用程式 tooAzure，您可以使用 Azure CLI 中[Jenkins 管線](/azure/jenkins/execute-cli-jenkins-pipeline)或者您可以使用的 hello [Azure 應用程式服務 Jenkins 外掛程式](https://plugins.jenkins.io/azure-app-service)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="be2cd-105">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="be2cd-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be2cd-106">設定 Jenkins toodeploy tooAzure 透過 FTP 的應用程式服務</span><span class="sxs-lookup"><span data-stu-id="be2cd-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="be2cd-107">設定透過 Docker 的 Linux 上的 Jenkins toodeploy tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="be2cd-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="be2cd-108">建立及設定 Jenkins 執行個體</span><span class="sxs-lookup"><span data-stu-id="be2cd-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="be2cd-109">如果您還沒有 Jenkins 主要，以 hello 開頭[方案範本](install-jenkins-solution-template.md)，其中包括 JDK8 和下列必要的外掛程式 hello:</span><span class="sxs-lookup"><span data-stu-id="be2cd-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="be2cd-110">[Jenkins Git 用戶端外掛程式](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="be2cd-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="be2cd-111">[Docker Commons 外掛程式](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="be2cd-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="be2cd-112">[Azure 認證](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="be2cd-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="be2cd-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="be2cd-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="be2cd-114">您可以使用 hello (比方說，C#、 PHP、 Java 和 node.js 等等） 支援的所有語言 Azure App Service 中的應用程式服務外掛程式 toodeploy Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="be2cd-115">在此教學課程中，我們會使用 hello 範例 Java 應用程式，[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="be2cd-116">toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="be2cd-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="be2cd-117">Java JDK 和 Maven 不需要建置 hello Java 專案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="be2cd-118">請確定您將安裝 hello 元件在 hello Jenkins master 或 hello VM 代理程式中，如果您使用另一個用於連續整合。</span><span class="sxs-lookup"><span data-stu-id="be2cd-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="be2cd-119">tooinstall，登入使用 SSH toohello Jenkins 執行個體，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be2cd-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="be2cd-120">針對部署 tooApp Linux 上的服務，您也需要 tooinstall Docker hello Jenkins master 或用於建置 hello VM 代理程式上。</span><span class="sxs-lookup"><span data-stu-id="be2cd-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="be2cd-121">Toothis 文章 tooinstall Docker，請參閱： https://docs.docker.com/engine/installation/linux/ubuntu/。</span><span class="sxs-lookup"><span data-stu-id="be2cd-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="be2cd-122">加入 Azure 服務主體 tooJenkins 認證</span><span class="sxs-lookup"><span data-stu-id="be2cd-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="be2cd-123">Azure 服務主體是所需的 toodeploy tooAzure。</span><span class="sxs-lookup"><span data-stu-id="be2cd-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="be2cd-124">使用[Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)或[Azure 入口網站](/azure/azure-resource-manager/resource-group-create-service-principal-portal)toocreate Azure 服務主體</span><span class="sxs-lookup"><span data-stu-id="be2cd-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="be2cd-125">在 hello Jenkins 儀表板內，按一下**認證-> 系統->** 。</span><span class="sxs-lookup"><span data-stu-id="be2cd-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="be2cd-126">按一下 [Global credentials(unrestricted)] \(全域認證 (不受限)\)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="be2cd-127">按一下**新增認證**tooadd 填寫 hello 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點的 Microsoft Azure 服務主體。</span><span class="sxs-lookup"><span data-stu-id="be2cd-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="be2cd-128">請提供要在後續步驟中使用的識別碼 (**mySp**)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="be2cd-129">Azure App Service 外掛程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-129">Azure App Service plugin</span></span>

<span data-ttu-id="be2cd-130">Azure App Service 外掛程式 v1.0 支援以連續部署 tooAzure Web 應用程式透過：</span><span class="sxs-lookup"><span data-stu-id="be2cd-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="be2cd-131">Git 和 FTP</span><span class="sxs-lookup"><span data-stu-id="be2cd-131">Git and FTP</span></span>
* <span data-ttu-id="be2cd-132">適用於 Linux 上 Web 應用程式的 Docker</span><span class="sxs-lookup"><span data-stu-id="be2cd-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="be2cd-133">設定 Jenkins toodeploy 透過 FTP 使用 hello Jenkins 儀表板的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="be2cd-134">toodeploy 您專案 tooAzure Web 應用程式，您可以上傳您的組建成品 （例如，在 Java 中.war 檔案） 使用 Git 或 FTP。</span><span class="sxs-lookup"><span data-stu-id="be2cd-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="be2cd-135">之前設定 Jenkins hello 工作，您需要 Azure App Service 方案和 Web 應用程式執行 hello Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="be2cd-136">建立 Azure App Service 方案以 hello**免費**定價層使用 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="be2cd-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="be2cd-137">hello 應用程式服務方案會定義 hello 使用的實體資源 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="be2cd-138">指派 tooan 應用程式服務方案的所有應用程式共用這些資源，讓您 toosave 成本裝載多個應用程式時。</span><span class="sxs-lookup"><span data-stu-id="be2cd-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="be2cd-139">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-139">Create a Web App.</span></span> <span data-ttu-id="be2cd-140">可以是使用 hello [Azure 入口網站](/azure/app-service-web/web-sites-configure)或使用 hello 下列 Az CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="be2cd-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="be2cd-141">請確定您設定您的應用程式需要的 hello Java 執行階段組態。</span><span class="sxs-lookup"><span data-stu-id="be2cd-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="be2cd-142">下列 Azure CLI 命令的 hello 設定 hello web 應用程式 toorun 上最近的 Java 8 JDK 和[Apache Tomcat](http://tomcat.apache.org/) 8.0。</span><span class="sxs-lookup"><span data-stu-id="be2cd-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="be2cd-143">設定 hello Jenkins 工作</span><span class="sxs-lookup"><span data-stu-id="be2cd-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="be2cd-144">在 Jenkins 儀表板中建立新的**自由樣式**專案</span><span class="sxs-lookup"><span data-stu-id="be2cd-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="be2cd-145">設定**原始程式碼管理**toouse 本機分岔[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)藉由提供 hello**儲存機制 URL**。</span><span class="sxs-lookup"><span data-stu-id="be2cd-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="be2cd-146">例如：http://github.com/&lt;yourID>/javawebappsample。</span><span class="sxs-lookup"><span data-stu-id="be2cd-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="be2cd-147">加入使用 Maven 建置步驟 toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="be2cd-148">新增**執行殼層**即可達到此目的。</span><span class="sxs-lookup"><span data-stu-id="be2cd-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="be2cd-149">例如，我們需要額外的步驟 toorename hello *.war 中的檔案目標資料夾 tooROOT.war。</span><span class="sxs-lookup"><span data-stu-id="be2cd-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="be2cd-150">選取 [發行 Azure Web 應用程式] 來新增建置後動作。</span><span class="sxs-lookup"><span data-stu-id="be2cd-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="be2cd-151">供應、"mySp 」、 儲存在上一個步驟中的 hello Azure 服務主體。</span><span class="sxs-lookup"><span data-stu-id="be2cd-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="be2cd-152">在**應用程式組態**區段中，選擇您的訂用帳戶中的 hello 資源群組和 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="be2cd-153">hello 外掛程式會自動偵測 hello Web 應用程式是否為 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="be2cd-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="be2cd-154">Windows Web 應用程式中，會顯示 hello 選項 「 發行檔案 」。</span><span class="sxs-lookup"><span data-stu-id="be2cd-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="be2cd-155">填滿 hello 檔案中，您想 toodeploy （例如 war 封裝如果您使用 Java。）[來源目錄] 和 [目標目錄] 是選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="be2cd-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="be2cd-156">hello 參數可讓您 toospecify 來源和目標資料夾上傳檔案時。</span><span class="sxs-lookup"><span data-stu-id="be2cd-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="be2cd-157">Azure 上的 Java Web 應用程式會在 Tomcat 伺服器中執行。</span><span class="sxs-lookup"><span data-stu-id="be2cd-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="be2cd-158">因此，您會將 war 套件上傳到 webapps 資料夾。</span><span class="sxs-lookup"><span data-stu-id="be2cd-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="be2cd-159">這個範例中，將設定**來源目錄**太 「 目標 」 和 「 webapps 」 提供的**目標目錄**。</span><span class="sxs-lookup"><span data-stu-id="be2cd-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="be2cd-160">如果您想 toodeploy tooa 插槽生產以外，您也可以設定**插槽**名稱。</span><span class="sxs-lookup"><span data-stu-id="be2cd-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="be2cd-161">儲存 hello 專案並建置該檔案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-161">Save hello project and build it.</span></span> <span data-ttu-id="be2cd-162">組建完成時，您的 web 應用程式是部署的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="be2cd-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="be2cd-163">使用 Jenkins 管線來透過 FTP 部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="be2cd-164">hello 外掛程式是管線已備妥。</span><span class="sxs-lookup"><span data-stu-id="be2cd-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="be2cd-165">您可以參考 tooa hello GitHub 儲存機制中的範例。</span><span class="sxs-lookup"><span data-stu-id="be2cd-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="be2cd-166">在 GitHub Web UI 中，開啟 **Jenkinsfile_ftp_plugin** 檔案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="be2cd-167">分別按一下 hello 鉛筆圖示 tooedit 這個檔案 tooupdate hello 資源群組與上一行 11 和 12 的 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="be2cd-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="be2cd-168">變更您 Jenkins 執行個體中的行 14 tooupdate 認證識別碼。</span><span class="sxs-lookup"><span data-stu-id="be2cd-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="be2cd-169">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="be2cd-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="be2cd-170">在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="be2cd-171">提供 hello 工作的名稱，並選取**管線**。</span><span class="sxs-lookup"><span data-stu-id="be2cd-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="be2cd-172">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="be2cd-172">Click **OK**.</span></span>
3. <span data-ttu-id="be2cd-173">按一下 hello**管線**索引標籤旁邊。</span><span class="sxs-lookup"><span data-stu-id="be2cd-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="be2cd-174">針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="be2cd-175">針對 [SCM]，選取 [Git]。</span><span class="sxs-lookup"><span data-stu-id="be2cd-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="be2cd-176">輸入您分岔的儲存機制的 hello GitHub URL: https:&lt;您分岔的儲存機制 >.git</span><span class="sxs-lookup"><span data-stu-id="be2cd-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="be2cd-177">更新**指令碼路徑**太"Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="be2cd-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="be2cd-178">按一下**儲存**與 hello 執行的工作。</span><span class="sxs-lookup"><span data-stu-id="be2cd-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="be2cd-179">設定透過 Docker 的 Linux 上的 Jenkins toodeploy Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="be2cd-180">除了透過 Git/FTP，Linux 上的 Web 應用程式還支援使用 Docker 來進行部署。</span><span class="sxs-lookup"><span data-stu-id="be2cd-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="be2cd-181">使用 Docker toodeploy 需要 tooprovide 將 docker 映像封裝為 web 應用程式與服務執行階段的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="be2cd-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="be2cd-182">然後 hello 外掛程式建置 hello 映像、 將其發送 tooa docker 登錄和部署 hello 映像 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="be2cd-183">Linux 上的 Web 應用程式也支援 Git 和 FTP 等傳統方式，但這些方式只適用於內建語言 (.NET Core、Node.js、PHP 和 Ruby)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="be2cd-184">至於其他語言，您需要 toopackage 應用程式程式碼和服務執行階段一起到 docker 映像和使用 docker toodeploy。</span><span class="sxs-lookup"><span data-stu-id="be2cd-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="be2cd-185">之前設定 Jenkins hello 工作，您必須在 Linux 上的 Azure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="be2cd-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="be2cd-186">容器登錄中也需要的 toostore 並管理私人 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="be2cd-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="be2cd-187">您可以使用 DockerHub；我們會在此範例中使用 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="be2cd-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="be2cd-188">您可以依照 hello 步驟[這裡](/azure/app-service-web/app-service-linux-how-to-create-web-app)toocreate Linux 上的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="be2cd-189">Azure 容器登錄中是受管理 [Docker 登錄] (https://docs.docker.com/registry/) 為基礎的服務 hello 開放原始碼 Docker 登錄 2.0。</span><span class="sxs-lookup"><span data-stu-id="be2cd-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="be2cd-190">請遵循 [這裡] hello 步驟 （/ azure/container-registry/container-registry-get-started-azure-cli） 的詳細指引 toodo 讓。</span><span class="sxs-lookup"><span data-stu-id="be2cd-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="be2cd-191">您也可以使用 DockerHub。</span><span class="sxs-lookup"><span data-stu-id="be2cd-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="be2cd-192">使用 docker toodeploy:</span><span class="sxs-lookup"><span data-stu-id="be2cd-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="be2cd-193">在 Jenkins 儀表板中建立新的自由樣式專案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="be2cd-194">設定**原始程式碼管理**toouse 本機分岔[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)藉由提供 hello**儲存機制 URL**。</span><span class="sxs-lookup"><span data-stu-id="be2cd-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="be2cd-195">例如：http://github.com/&lt;yourid>/javawebappsample。</span><span class="sxs-lookup"><span data-stu-id="be2cd-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="be2cd-196">加入使用 Maven 建置步驟 toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="be2cd-197">這樣做將**執行殼層**並加入下列行中的 hello**命令**:</span><span class="sxs-lookup"><span data-stu-id="be2cd-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="be2cd-198">選取 [發行 Azure Web 應用程式] 來新增建置後動作。</span><span class="sxs-lookup"><span data-stu-id="be2cd-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="be2cd-199">提供， **mySp**，做為 Azure 認證的上一個步驟中儲存的 hello Azure 服務主體。</span><span class="sxs-lookup"><span data-stu-id="be2cd-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="be2cd-200">在**應用程式組態**區段中，選擇您的訂用帳戶中的 hello 資源群組和 Linux 的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="be2cd-201">選擇透過 Docker 來發行。</span><span class="sxs-lookup"><span data-stu-id="be2cd-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="be2cd-202">填寫 **Dockerfile** 路徑。</span><span class="sxs-lookup"><span data-stu-id="be2cd-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="be2cd-203">您可以保留 hello 預設 「 / Dockerfile 」 的**Docker 登錄 URL**、 https:// hello 格式提供&lt;myRegistry >。 azurecr.io，如果您使用 Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="be2cd-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="be2cd-204">如果您使用 DockerHub，請讓它保持空白。</span><span class="sxs-lookup"><span data-stu-id="be2cd-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="be2cd-205">如**登錄認證**，新增 hello Azure 容器登錄中的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="be2cd-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="be2cd-206">您可以藉由執行下列 Azure CLI 命令的 hello 取得 hello 使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="be2cd-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="be2cd-207">hello 第一個命令會啟用 hello 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="be2cd-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="be2cd-208">docker 映像名稱和標記中的 hello**進階**是選擇性的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be2cd-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="be2cd-209">根據預設，可取得的映像名稱從 hello 映像從 $BUILD_NUMBER 產生您在 Azure 入口網站 （在 Docker 容器設定。） hello 標記中設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="be2cd-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="be2cd-210">請確定您指定其中一個 Azure 入口網站中的 hello 映像名稱，或提供的值**Docker 映像**中**進階** 索引標籤。在此範例中，請在 Docker 映像 中提供「&lt;yourRegistry>.azurecr.io/calculator」，並讓 Docker 映像標記 保持空白。</span><span class="sxs-lookup"><span data-stu-id="be2cd-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="be2cd-211">請注意，如果您使用內建的 Docker 映像設定，部署將會失敗。</span><span class="sxs-lookup"><span data-stu-id="be2cd-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="be2cd-212">請確定您變更 docker 設定 toouse 自訂映像中的 Azure 入口網站上的 Docker 容器設定。</span><span class="sxs-lookup"><span data-stu-id="be2cd-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="be2cd-213">內建影像，請使用檔案上傳方法 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="be2cd-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="be2cd-214">類似的 toofile 上傳方法，您可以選擇生產環境以外的不同位置。</span><span class="sxs-lookup"><span data-stu-id="be2cd-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="be2cd-215">儲存並建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-215">Save and build hello project.</span></span> <span data-ttu-id="be2cd-216">您會看到您的容器映像推入 tooyour 登錄和 web 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="be2cd-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="be2cd-217">部署 tooWeb 透過使用 Jenkins 管線的 Docker 的 Linux 上的應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="be2cd-218">在 GitHub Web UI 中，開啟 **Jenkinsfile_container_plugin** 檔案。</span><span class="sxs-lookup"><span data-stu-id="be2cd-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="be2cd-219">分別按一下 hello 鉛筆圖示 tooedit 這個檔案 tooupdate hello 資源群組與上一行 11 和 12 的 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="be2cd-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="be2cd-220">變更線條 13 tooyour 容器登錄伺服器</span><span class="sxs-lookup"><span data-stu-id="be2cd-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="be2cd-221">變更您 Jenkins 執行個體中的行 16 tooupdate 認證識別碼</span><span class="sxs-lookup"><span data-stu-id="be2cd-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="be2cd-222">建立 Jenkins 管線</span><span class="sxs-lookup"><span data-stu-id="be2cd-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="be2cd-223">在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="be2cd-224">提供 hello 工作的名稱，並選取**管線**。</span><span class="sxs-lookup"><span data-stu-id="be2cd-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="be2cd-225">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="be2cd-225">Click **OK**.</span></span>
3. <span data-ttu-id="be2cd-226">按一下 hello**管線**索引標籤旁邊。</span><span class="sxs-lookup"><span data-stu-id="be2cd-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="be2cd-227">針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。</span><span class="sxs-lookup"><span data-stu-id="be2cd-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="be2cd-228">針對 [SCM]，選取 [Git]。</span><span class="sxs-lookup"><span data-stu-id="be2cd-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="be2cd-229">輸入您分岔的儲存機制的 hello GitHub URL: https:&lt;您分岔的儲存機制 >.git</span><span class="sxs-lookup"><span data-stu-id="be2cd-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="be2cd-230">第 7 更新**指令碼路徑**太"Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="be2cd-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="be2cd-231">按一下**儲存**與 hello 執行的工作。</span><span class="sxs-lookup"><span data-stu-id="be2cd-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="be2cd-232">確認您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be2cd-232">Verify your web app</span></span>

1. <span data-ttu-id="be2cd-233">已成功部署 tooverify hello WAR 檔案 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be2cd-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="be2cd-234">請開啟網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="be2cd-234">Open a web browser.</span></span>
2. <span data-ttu-id="be2cd-235">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 您會看到：</span><span class="sxs-lookup"><span data-stu-id="be2cd-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="be2cd-236">Web 應用程式的 歡迎使用 tooJava!!!</span><span class="sxs-lookup"><span data-stu-id="be2cd-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="be2cd-237">此應用程式已更新！</span><span class="sxs-lookup"><span data-stu-id="be2cd-237">This is updated!</span></span>
   <span data-ttu-id="be2cd-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="be2cd-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="be2cd-239">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y</span><span class="sxs-lookup"><span data-stu-id="be2cd-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![計算機：加法](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="be2cd-241">Linux 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="be2cd-241">For App service on Linux</span></span>

* <span data-ttu-id="be2cd-242">tooverify，在 Azure CLI 執行：</span><span class="sxs-lookup"><span data-stu-id="be2cd-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="be2cd-243">您會收到 hello 下列結果：</span><span class="sxs-lookup"><span data-stu-id="be2cd-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="be2cd-244">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping。</span><span class="sxs-lookup"><span data-stu-id="be2cd-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="be2cd-245">您會看到 hello 訊息：</span><span class="sxs-lookup"><span data-stu-id="be2cd-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="be2cd-246">移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y</span><span class="sxs-lookup"><span data-stu-id="be2cd-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="be2cd-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be2cd-247">Next steps</span></span>

<span data-ttu-id="be2cd-248">在本教學課程中，您可以使用 hello Azure App Service 外掛程式 toodeploy tooAzure。</span><span class="sxs-lookup"><span data-stu-id="be2cd-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="be2cd-249">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="be2cd-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="be2cd-250">設定 Jenkins toodeploy 透過 FTP 的 Azure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="be2cd-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="be2cd-251">設定透過 Docker 的 Linux 上的 Jenkins toodeploy tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="be2cd-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
