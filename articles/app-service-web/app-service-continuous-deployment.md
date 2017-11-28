---
title: "aaaContinuous 部署 tooAzure 應用程式服務 |Microsoft 文件"
description: "深入了解如何 tooenable 連續部署 tooAzure 應用程式服務。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="e09f4-103">連續部署 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="e09f4-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="e09f4-104">本教學課程示範如何 tooconfigure 連續部署工作流程的程式[Azure App Service]應用程式。</span><span class="sxs-lookup"><span data-stu-id="e09f4-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="e09f4-105">GitHub、 BitBucket 應用程式服務整合和[Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/)啟用連續部署，Azure 會提取 hello 最新的更新從您的專案中的工作流程發行 tooone 這些服務。</span><span class="sxs-lookup"><span data-stu-id="e09f4-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="e09f4-106">持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。</span><span class="sxs-lookup"><span data-stu-id="e09f4-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="e09f4-107">toofind 出 tooconfigure 連續部署，以手動方式從雲端儲存機制不列出 hello Azure 入口網站的方式 (例如[GitLab](https://gitlab.com/))，請參閱[設定連續部署使用手動操作步驟](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。</span><span class="sxs-lookup"><span data-stu-id="e09f4-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="e09f4-108"><a name="overview"></a>啟用持續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="e09f4-109">tooenable 連續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="e09f4-110">發行您的應用程式內容 toohello 儲存機制，用於連續部署。</span><span class="sxs-lookup"><span data-stu-id="e09f4-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="e09f4-111">如需有關發行您的專案 toothese 服務的詳細資訊，請參閱[建立的儲存機制 (GitHub)]，[建立的儲存機制 (BitBucket)]，和[開始使用 VSTS]。</span><span class="sxs-lookup"><span data-stu-id="e09f4-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="e09f4-112">在您的應用程式功能表] 刀鋒視窗中 hello [Azure 入口網站]，按一下 [**應用程式部署 > 部署選項**。</span><span class="sxs-lookup"><span data-stu-id="e09f4-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="e09f4-113">按一下**選擇來源**，然後選取 hello 部署來源。</span><span class="sxs-lookup"><span data-stu-id="e09f4-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="e09f4-114">tooconfigure App Service 部署的 VSTS 帳戶，請參閱這[教學課程](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)。</span><span class="sxs-lookup"><span data-stu-id="e09f4-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="e09f4-115">完成 hello 授權工作流程。</span><span class="sxs-lookup"><span data-stu-id="e09f4-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="e09f4-116">在 hello**部署來源**刀鋒視窗中，選擇 hello 專案，以及建立分支 toodeploy 從。</span><span class="sxs-lookup"><span data-stu-id="e09f4-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="e09f4-117">完成後，按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="e09f4-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="e09f4-118">啟用搭配 GitHub 或 BitBucket 的持續部署時，將會同時顯示公用和私人專案。</span><span class="sxs-lookup"><span data-stu-id="e09f4-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="e09f4-119">應用程式服務建立關聯性與 hello 選取儲存機制、 提取中從指定的分支，hello hello 檔案以及維護您 App Service 應用程式的儲存機制的複製品。</span><span class="sxs-lookup"><span data-stu-id="e09f4-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="e09f4-120">當您設定來自 hello Azure 入口網站的 VSTS 連續部署時，hello 的整合會使用應用程式服務的 hello [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)，已自動建置和部署的工作，與每個`git push`。</span><span class="sxs-lookup"><span data-stu-id="e09f4-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="e09f4-121">您不需要 tooseparately 設定於 VSTS 中的連續部署。</span><span class="sxs-lookup"><span data-stu-id="e09f4-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="e09f4-122">完成此程序，hello 之後**部署選項**應用程式 刀鋒視窗會顯示作用中的部署，表示部署成功。</span><span class="sxs-lookup"><span data-stu-id="e09f4-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="e09f4-123">已成功部署 tooverify hello 應用程式中，按一下 hello **URL**在 hello hello Azure 入口網站中的 hello 應用程式 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="e09f4-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="e09f4-124">從您選擇的 hello 儲存機制進行持續部署 tooverify 推送變更 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e09f4-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="e09f4-125">您的應用程式應該更新 tooreflect hello 變更，很快就完成 hello 發送 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e09f4-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="e09f4-126">您可以確認它已在 hello hello 更新提取**部署選項**刀鋒視窗中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e09f4-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="e09f4-127"><a name="VSsolution"></a>Visual Studio 方案的持續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="e09f4-128">推入 Visual Studio 方案 tooAzure App Service 是推送簡單 index.html 檔案一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="e09f4-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="e09f4-129">hello App Service 部署程序來簡化所有 hello 詳細資料，包括還原 NuGet 相依性和建置 hello 應用程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="e09f4-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="e09f4-130">您可以遵循的維護程式碼只能在您的 Git 儲存機制中的 hello 來源控制最佳作法，並讓負責 hello rest 應用程式服務部署。</span><span class="sxs-lookup"><span data-stu-id="e09f4-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="e09f4-131">hello 步驟推送服務是您 Visual Studio 方案 tooApp hello 相同如同 hello[上一節](#overview)，前提是您設定您的解決方案和儲存機制，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e09f4-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="e09f4-132">使用 hello Visual Studio 原始檔控制選項 toogenerate`.gitignore`例如 hello 圖檔，或手動新增`.gitignore`檔案中儲存機制根目錄中，以內容類似 toothis [.gitignore 範例](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)。</span><span class="sxs-lookup"><span data-stu-id="e09f4-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="e09f4-133">加入 hello 整個方案的目錄樹狀結構 tooyour 儲存機制，與 hello 儲存機制的根目錄中的 hello.sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="e09f4-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="e09f4-134">一旦您設定您的儲存機制，如所述，並在 Azure 中設定您的應用程式的其中一個 hello 線上 Git 儲存機制持續發行，您可以開發您的 ASP.NET 應用程式，Visual Studio 中的本機及持續只是藉由部署您的程式碼推送變更 tooyour 線上 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e09f4-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="e09f4-135"><a name="disableCD"></a>停用連續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="e09f4-136">toodisable 連續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="e09f4-137">在您的應用程式功能表] 刀鋒視窗中 hello [Azure 入口網站]，按一下 [**應用程式部署 > 部署選項**。</span><span class="sxs-lookup"><span data-stu-id="e09f4-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="e09f4-138">然後按一下 **中斷連線**在 hello**部署選項**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e09f4-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="e09f4-139">之後回答**是**toohello 確認訊息中，您可以傳回 tooyour 應用程式 刀鋒視窗，然後按一下**應用程式部署 > 部署選項**如果您想要 tooset 發行從其他來源。</span><span class="sxs-lookup"><span data-stu-id="e09f4-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e09f4-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="e09f4-140">Additional Resources</span></span>
* [<span data-ttu-id="e09f4-141">如何 tooinvestigate 常見問題與連續部署</span><span class="sxs-lookup"><span data-stu-id="e09f4-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="e09f4-142">[如何 toouse PowerShell for Azure]</span><span class="sxs-lookup"><span data-stu-id="e09f4-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="e09f4-143">[如何 toouse hello 用於 Mac 和 Linux 的 Azure 命令列工具]</span><span class="sxs-lookup"><span data-stu-id="e09f4-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="e09f4-144">[Git 文件]</span><span class="sxs-lookup"><span data-stu-id="e09f4-144">[Git documentation]</span></span>
* [<span data-ttu-id="e09f4-145">專案 Kudu</span><span class="sxs-lookup"><span data-stu-id="e09f4-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="e09f4-146">使用 Azure tooautomatically 產生 CI/CD 管線 toodeploy ASP.NET 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="e09f4-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="e09f4-147">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="e09f4-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e09f4-148">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="e09f4-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure 入口網站]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[如何 toouse PowerShell for Azure]: /powershell/azureps-cmdlets-docs
[如何 toouse hello 用於 Mac 和 Linux 的 Azure 命令列工具]:../cli-install-nodejs.md
[Git 文件]: http://git-scm.com/documentation

[建立的儲存機制 (GitHub)]: https://help.github.com/articles/create-a-repo
[建立的儲存機制 (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[開始使用 VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
