---
title: "持續部署至 Azure App Service | Microsoft Docs"
description: "了解如何啟用持續部署至 Azure App Service。"
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
ms.openlocfilehash: 7d978e623aaff25a9400090bd3ac18ed560d2ebf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="4386c-103">持續部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4386c-103">Continuous Deployment to Azure App Service</span></span>
<span data-ttu-id="4386c-104">本教學課程將示範如何為您的 [Azure App Service] 應用程式設定連續部署工作流程。</span><span class="sxs-lookup"><span data-stu-id="4386c-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="4386c-105">App Service 與 BitBucket、GitHub 及 [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) 整合，可啟用持續部署工作流程，其中 Azure 會從您已發佈至這其中一個服務的專案中提取最新更新。</span><span class="sxs-lookup"><span data-stu-id="4386c-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span></span> <span data-ttu-id="4386c-106">持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。</span><span class="sxs-lookup"><span data-stu-id="4386c-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="4386c-107">若要了解如何從 Azure 入口網站未列出的雲端存放庫中手動設定連續部署 (例如 [GitLab](https://gitlab.com/))，請參閱[使用手動步驟設定連續部署](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。</span><span class="sxs-lookup"><span data-stu-id="4386c-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="4386c-108"><a name="overview"></a>啟用持續部署</span><span class="sxs-lookup"><span data-stu-id="4386c-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="4386c-109">若要啟用持續部署，</span><span class="sxs-lookup"><span data-stu-id="4386c-109">To enable continuous deployment,</span></span>

1. <span data-ttu-id="4386c-110">將您的應用程式內容發佈至將用於持續部署的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4386c-110">Publish your app content to the repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="4386c-111">如需將專案發佈至這些服務的詳細資訊，請參閱[建立儲存機制 (GitHub)]、[建立儲存機制 (BitBucket)]及[開始使用 VSTS]。</span><span class="sxs-lookup"><span data-stu-id="4386c-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="4386c-112">在 [Azure 入口網站]中您應用程式的功能表刀鋒視窗中，按一下 [應用程式部署] > [部署選項]。</span><span class="sxs-lookup"><span data-stu-id="4386c-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="4386c-113">按一下 [選擇來源]，然後選取部署來源。</span><span class="sxs-lookup"><span data-stu-id="4386c-113">Click **Choose Source**, then select the deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="4386c-114">若要設定適用於 App Service 部署的 VSTS 帳戶，請參閱這個 [教學課程](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)。</span><span class="sxs-lookup"><span data-stu-id="4386c-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="4386c-115">完成授權工作流程。</span><span class="sxs-lookup"><span data-stu-id="4386c-115">Complete the authorization workflow.</span></span>
4. <span data-ttu-id="4386c-116">在 [部署來源] 刀鋒視窗中，選擇專案以及要從中部署的分支。</span><span class="sxs-lookup"><span data-stu-id="4386c-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span></span> <span data-ttu-id="4386c-117">完成後，按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="4386c-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="4386c-118">啟用搭配 GitHub 或 BitBucket 的持續部署時，將會同時顯示公用和私人專案。</span><span class="sxs-lookup"><span data-stu-id="4386c-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="4386c-119">App Service 會建立與所選儲存機制的關聯、從指定的分支提取檔案，並維護適用於 App Service 應用程式的儲存機制複本。</span><span class="sxs-lookup"><span data-stu-id="4386c-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="4386c-120">從 Azure 入口網站設定 VSTS 持續部署時，整合會使用 App Service [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)，它已經利用每個 `git push` 自動建置和部署工作。</span><span class="sxs-lookup"><span data-stu-id="4386c-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="4386c-121">您不需要在 VSTS 中分別設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="4386c-121">You do not need to separately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="4386c-122">此程序完成之後，應用程式刀鋒視窗的 [部署選項] 應用程式刀鋒視窗將會顯示作用中的部署，表示部署成功。</span><span class="sxs-lookup"><span data-stu-id="4386c-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="4386c-123">若要確認已成功部署應用程式，請按一下 Azure 入口網站中應用程式刀鋒視窗頂端的 [URL]。</span><span class="sxs-lookup"><span data-stu-id="4386c-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span></span>
6. <span data-ttu-id="4386c-124">若要確認從您選擇的儲存機制進行連續部署，將變更推送至儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4386c-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span></span> <span data-ttu-id="4386c-125">在推送至儲存機制完成後不久，您的應用程式應該會更新以反映變更。</span><span class="sxs-lookup"><span data-stu-id="4386c-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span></span> <span data-ttu-id="4386c-126">您可以在應用程式的 [部署選項] 刀鋒視窗上確認它是否已提取更新。</span><span class="sxs-lookup"><span data-stu-id="4386c-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="4386c-127"><a name="VSsolution"></a>Visual Studio 方案的持續部署</span><span class="sxs-lookup"><span data-stu-id="4386c-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="4386c-128">將 Visual Studio 方案推送至 Azure App Service，就像推送簡單的 index.html 檔案一樣容易。</span><span class="sxs-lookup"><span data-stu-id="4386c-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="4386c-129">App Service 部署程序會簡化所有細節，包含還原 NuGet 相依性，以及建置應用程式二進位檔。</span><span class="sxs-lookup"><span data-stu-id="4386c-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span></span> <span data-ttu-id="4386c-130">您可以只在 Git 儲存機制中遵循維護程式碼的原始檔控制最佳做法，然後讓 App Service 部署負責執行剩餘的部分。</span><span class="sxs-lookup"><span data-stu-id="4386c-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span></span>

<span data-ttu-id="4386c-131">將您的 Visual Studio 方案推送至 App Service 的步驟和 [上一節](#overview)的一樣，可提供您設定方案和儲存機制的步驟，如下：</span><span class="sxs-lookup"><span data-stu-id="4386c-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="4386c-132">使用 Visual Studio 原始檔控制選項來產生 `.gitignore` 檔案 (如下圖所示)，或使用類似這個 [.gitignore 範例](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)的內容，在您的儲存機制根目錄中手動新增 `.gitignore` 檔案。</span><span class="sxs-lookup"><span data-stu-id="4386c-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="4386c-133">使用儲存機制根目錄中的 .sln 檔案，將整個解決方案的目錄樹狀結構新增至您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4386c-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span></span>

<span data-ttu-id="4386c-134">一旦您設定儲存機制 (如前所述) 並在 Azure 中設定應用程式，以便從其中一個線上 Git 儲存機制持續發佈之後，就能夠在 Visual Studio 中本機開發 ASP.NET 應用程式，並且只需將變更推送至線上 Git 儲存機制，就能持續部署您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4386c-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span></span>

## <span data-ttu-id="4386c-135"><a name="disableCD"></a>停用連續部署</span><span class="sxs-lookup"><span data-stu-id="4386c-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="4386c-136">若要停用持續部署，</span><span class="sxs-lookup"><span data-stu-id="4386c-136">To disable continuous deployment,</span></span>

1. <span data-ttu-id="4386c-137">在 [Azure 入口網站]中您應用程式的功能表刀鋒視窗中，按一下 [應用程式部署] > [部署選項]。</span><span class="sxs-lookup"><span data-stu-id="4386c-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="4386c-138">然後按一下 [部署選項] 刀鋒視窗中的 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="4386c-138">Then click **Disconnect** in the **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="4386c-139">在確認訊息中回答 [是] 之後，如果您要設定從其他來源發佈，您可以返回應用程式的刀鋒視窗，然後按一下 [應用程式部署] > [部署選項]。</span><span class="sxs-lookup"><span data-stu-id="4386c-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4386c-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="4386c-140">Additional Resources</span></span>
* [<span data-ttu-id="4386c-141">如何調查連續部署的常見問題</span><span class="sxs-lookup"><span data-stu-id="4386c-141">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="4386c-142">[如何使用適用於 Azure 的 PowerShell]</span><span class="sxs-lookup"><span data-stu-id="4386c-142">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="4386c-143">[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]</span><span class="sxs-lookup"><span data-stu-id="4386c-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="4386c-144">[Git 文件]</span><span class="sxs-lookup"><span data-stu-id="4386c-144">[Git documentation]</span></span>
* [<span data-ttu-id="4386c-145">專案 Kudu</span><span class="sxs-lookup"><span data-stu-id="4386c-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="4386c-146">使用 Azure 自動產生 CI/CD 管線，以部署 ASP.NET 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="4386c-146">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="4386c-147">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4386c-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4386c-148">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="4386c-148">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="4386c-149">[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="4386c-149">[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span></span>
<span data-ttu-id="4386c-150">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4386c-150">[Azure portal]: https://portal.azure.com</span></span>
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="4386c-151">[如何使用適用於 Azure 的 PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="4386c-151">[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="4386c-152">[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="4386c-152">[How to use the Azure Command-Line Tools for Mac and Linux]:../cli-install-nodejs.md</span></span>
<span data-ttu-id="4386c-153">[Git 文件]: http://git-scm.com/documentation</span><span class="sxs-lookup"><span data-stu-id="4386c-153">[Git Documentation]: http://git-scm.com/documentation</span></span>

<span data-ttu-id="4386c-154">[建立儲存機制 (GitHub)]: https://help.github.com/articles/create-a-repo</span><span class="sxs-lookup"><span data-stu-id="4386c-154">[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo</span></span>
<span data-ttu-id="4386c-155">[建立儲存機制 (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span><span class="sxs-lookup"><span data-stu-id="4386c-155">[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span></span>
<span data-ttu-id="4386c-156">[開始使用 VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview</span><span class="sxs-lookup"><span data-stu-id="4386c-156">[Get started with VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview</span></span>
