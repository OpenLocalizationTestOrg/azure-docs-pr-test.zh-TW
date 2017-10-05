---
title: "使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)"
description: "學習如何使用支援敏捷式軟體開發的方式來建立高級別複雜應用程式與 Azure App Service。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a><span data-ttu-id="f2aca-103">使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)</span><span class="sxs-lookup"><span data-stu-id="f2aca-103">Agile software development with Azure App Service</span></span>
<span data-ttu-id="f2aca-104">在本教學課程中，您將學習如何使用支援[敏捷式軟體開發](https://en.wikipedia.org/wiki/Agile_software_development)的方式，使用 [Azure App Service](/azure/app-service/) 建立高級別複雜應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-104">In this tutorial, you will learn how to create high-scale complex applications with [Azure App Service](/azure/app-service/) in a way that supports [agile software development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="f2aca-105">假設您已經知道如何 [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-105">It assumes that you already know how to [deploy complex applications predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="f2aca-106">技術程序限制通常會妨礙成功的實作敏捷式方法。</span><span class="sxs-lookup"><span data-stu-id="f2aca-106">Limitations in technical processes can often stand in the way of successful implementation of agile methodologies.</span></span> <span data-ttu-id="f2aca-107">如果在 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 中明智地結合部署的協調流程與管理，則 Azure App Service 與功能 (例如[持續發佈](app-service-continuous-deployment.md)、[預備環境](web-sites-staged-publishing.md) (位置) 和[監視](web-sites-monitor.md)) 是非常適合採用敏捷式軟體開發之開發人員的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f2aca-107">Azure App Service with features such as [continuous publishing](app-service-continuous-deployment.md), [staging environments](web-sites-staged-publishing.md) (slots), and [monitoring](web-sites-monitor.md), when coupled wisely with the orchestration and management of deployment in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), can be part of a great solution for developers who embrace agile software development.</span></span>

<span data-ttu-id="f2aca-108">下表是敏捷式開發相關需求以及 Azure 服務如何啟用它們的簡短清單。</span><span class="sxs-lookup"><span data-stu-id="f2aca-108">The following table is a short list of requirements associated with agile development, and how Azure services enable each of them.</span></span>

| <span data-ttu-id="f2aca-109">需求</span><span class="sxs-lookup"><span data-stu-id="f2aca-109">Requirement</span></span> | <span data-ttu-id="f2aca-110">如何讓 Azure</span><span class="sxs-lookup"><span data-stu-id="f2aca-110">How Azure enables</span></span> |
| --- | --- |
| <span data-ttu-id="f2aca-111">- 使用每個認可建置</span><span class="sxs-lookup"><span data-stu-id="f2aca-111">- Build with every commit</span></span><br><span data-ttu-id="f2aca-112">- 自動並快速地建置</span><span class="sxs-lookup"><span data-stu-id="f2aca-112">- Build automatically and fast</span></span> |<span data-ttu-id="f2aca-113">設定持續部署時，Azure App Service 可以根據 dev 分支作用為即時執行組建。</span><span class="sxs-lookup"><span data-stu-id="f2aca-113">When configured with continuous deployment, Azure App Service can function as live-running builds based on a dev branch.</span></span> <span data-ttu-id="f2aca-114">每次將程式碼推送至分支時，在 Azure 中就會自動建置和即時執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f2aca-114">Every time code is pushed to the branch, it is automatically built and running live in Azure.</span></span> |
| <span data-ttu-id="f2aca-115">- 將組建設為自我測試</span><span class="sxs-lookup"><span data-stu-id="f2aca-115">- Make builds self-testing</span></span> |<span data-ttu-id="f2aca-116">負載測試、Web 測試等可以使用 Azure 資源管理員範本進行部署。</span><span class="sxs-lookup"><span data-stu-id="f2aca-116">Load tests, web tests, etc., can be deployed with the Azure Resource Manager template.</span></span> |
| <span data-ttu-id="f2aca-117">- 在生產環境的複製品中執行測試</span><span class="sxs-lookup"><span data-stu-id="f2aca-117">- Perform tests in a clone of production environment</span></span> |<span data-ttu-id="f2aca-118">Azure 資源管理員範本可以用來建立 Azure 生產環境的複製品 (包括應用程式設定、連接字串範本、縮放等) 以透過快速且可預測的方式測試。</span><span class="sxs-lookup"><span data-stu-id="f2aca-118">Azure Resource Manager templates can be used to create clones of the Azure production environment (including app settings, connection string templates, scaling, etc.) for testing quickly and predictably.</span></span> |
| <span data-ttu-id="f2aca-119">- 輕鬆地檢視最新組建結果</span><span class="sxs-lookup"><span data-stu-id="f2aca-119">- View result of latest build easily</span></span> |<span data-ttu-id="f2aca-120">從儲存機制持續部署至 Azure，表示您可以在認可變更之後立即於即時應用程式中測試新程式碼。</span><span class="sxs-lookup"><span data-stu-id="f2aca-120">Continuous deployment to Azure from a repository means that you can test new code in a live application immediately after you commit your changes.</span></span> |
| <span data-ttu-id="f2aca-121">- 每天認可到主要分支</span><span class="sxs-lookup"><span data-stu-id="f2aca-121">- Commit to the main branch every day</span></span><br><span data-ttu-id="f2aca-122">- 自動化部署</span><span class="sxs-lookup"><span data-stu-id="f2aca-122">- Automate deployment</span></span> |<span data-ttu-id="f2aca-123">生產應用程式與儲存機制主要分支的連續整合會自動將主要分支的每次認可/合併部署至生產環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-123">Continuous integration of a production application with a repository’s main branch automatically deploys every commit/merge to the main branch to production.</span></span> |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="f2aca-124">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="f2aca-124">What you will do</span></span>
<span data-ttu-id="f2aca-125">您將逐步進行一般「開發-測試-預備-生產」工作流程，以將新變更發佈至 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 範例應用程式 (內含兩個 [Web 應用程式](/services/app-service/web/)：一個是前端 (FE)，另一個是 Web API 後端 (BE)) 和 [SQL 資料庫](/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-125">You will walk through a typical dev-test-stage-production workflow in order to publish new changes to the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) sample application, which consists of two [web apps](/services/app-service/web/), one being a frontend (FE) and the other being a Web API backend (BE), and a [SQL database](/services/sql-database/).</span></span> <span data-ttu-id="f2aca-126">您將使用下列部署架構：</span><span class="sxs-lookup"><span data-stu-id="f2aca-126">You will work with the following deployment architecture:</span></span>

![](./media/app-service-agile-software-development/what-1-architecture.png)

<span data-ttu-id="f2aca-127">若要將圖片放入文字：</span><span class="sxs-lookup"><span data-stu-id="f2aca-127">To put the picture into words:</span></span>

* <span data-ttu-id="f2aca-128">部署架構分成三個不同環境 (或 Azure 中的[資源群組](../azure-resource-manager/resource-group-overview.md))，其各有專屬 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)、[調整](web-sites-scale.md)設定和 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2aca-128">The deployment architecture is separated into three distinct environments (or [resource groups](../azure-resource-manager/resource-group-overview.md) in Azure), each with its own [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [scaling](web-sites-scale.md) settings, and SQL database.</span></span> 
* <span data-ttu-id="f2aca-129">您可以個別管理每個環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-129">Each environment can be managed separately.</span></span> <span data-ttu-id="f2aca-130">它們甚至可以存在於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f2aca-130">They can even exist in different subscriptions.</span></span>
* <span data-ttu-id="f2aca-131">預備和生產環境會實作為相同 App Service 應用程式的兩個位置。</span><span class="sxs-lookup"><span data-stu-id="f2aca-131">Staging and production are implemented as two slots of the same App Service app.</span></span> <span data-ttu-id="f2aca-132">主要分支是設定進行具有預備位置的連續整合。</span><span class="sxs-lookup"><span data-stu-id="f2aca-132">The master branch is set up for continuous integration with the staging slot.</span></span>
* <span data-ttu-id="f2aca-133">在預備位置 (含生產資料) 上驗證主要分支的認可時，已驗證的預備應用程式會交換到生產位置， [而不中斷](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-133">When a commit to master branch is verified on the staging slot (with production data), the verified staging app is swapped into the production slot [with no downtime](web-sites-staged-publishing.md).</span></span>

<span data-ttu-id="f2aca-134">生產和預備環境是由 [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json) 上的範本所定義。</span><span class="sxs-lookup"><span data-stu-id="f2aca-134">The production and staging environment is defined by the template at [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).</span></span>

<span data-ttu-id="f2aca-135">開發和測試環境是由 [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json) 上的範本所定義。</span><span class="sxs-lookup"><span data-stu-id="f2aca-135">The dev and test environments are defined by the template at [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).</span></span>

<span data-ttu-id="f2aca-136">您也將使用一般分支策略，其中，程式碼會從開發分支移至測試分支，然後移至主要分支 (就是所謂的提升品質)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-136">You will also use the typical branching strategy, with code moving from the dev branch up to the test branch, then to the master branch (moving up in quality, so to speak).</span></span>

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a><span data-ttu-id="f2aca-137">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f2aca-137">What you need</span></span>
* <span data-ttu-id="f2aca-138">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="f2aca-138">An Azure account</span></span>
* <span data-ttu-id="f2aca-139">一個 [GitHub](https://github.com/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="f2aca-139">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="f2aca-140">Git Shell (與 [GitHub for Windows](https://windows.github.com/)一起安裝) - 這可讓您在相同的工作階段中執行 Git 和 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="f2aca-140">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - enables you to run both the Git and PowerShell commands in the same session</span></span> 
* <span data-ttu-id="f2aca-141">最新 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 位元</span><span class="sxs-lookup"><span data-stu-id="f2aca-141">Latest [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits</span></span>
* <span data-ttu-id="f2aca-142">下列工具的基本了解：</span><span class="sxs-lookup"><span data-stu-id="f2aca-142">Basic understanding of the following tools:</span></span>
  * <span data-ttu-id="f2aca-143">[Azure Resource Manager ](../azure-resource-manager/resource-group-overview.md)範本部署 (另請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="f2aca-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (also see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="f2aca-144">Git</span><span class="sxs-lookup"><span data-stu-id="f2aca-144">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="f2aca-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2aca-145">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="f2aca-146">要完成此教學課程，您必須要有 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="f2aca-146">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="f2aca-147">您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/) ：您將取得可試用 Azure 付費服務的額度，且即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務，例如 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="f2aca-147">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="f2aca-148">您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="f2aca-148">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> <span data-ttu-id="f2aca-149">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-149">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f2aca-150">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="f2aca-150">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="set-up-your-production-environment"></a><span data-ttu-id="f2aca-151">設定生產環境</span><span class="sxs-lookup"><span data-stu-id="f2aca-151">Set up your production environment</span></span>
> [!NOTE]
> <span data-ttu-id="f2aca-152">本教學課程中使用的指令碼會自動從 GitHub 存放庫設定連續發佈。</span><span class="sxs-lookup"><span data-stu-id="f2aca-152">The script used in this tutorial automatically configures continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="f2aca-153">這需要您的 GitHub 認證已儲存在 Azure 中，否則，嘗試設定 Web 應用程式的原始檔控制設定時，指令碼部署會失敗。</span><span class="sxs-lookup"><span data-stu-id="f2aca-153">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment fails when attempting to configure source control settings for the web apps.</span></span> 
> 
> <span data-ttu-id="f2aca-154">若要在 Azure 中儲存您的 GitHub 認證，請在 [Azure 入口網站](https://portal.azure.com/)中建立 Web 應用程式，並[設定 GitHub 部署](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-154">To store your GitHub credentials in Azure, create a web app in the [Azure portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f2aca-155">您只需要做一次這個動作。</span><span class="sxs-lookup"><span data-stu-id="f2aca-155">You only need to do this once.</span></span> 
> 
> 

<span data-ttu-id="f2aca-156">在一般 DevOps 案例中，應用程式是在 Azure 中即時執行，而且您想要透過連續發行對它進行變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-156">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="f2aca-157">在此案例中，您會有您所開發、測試以及用來部署生產環境的範本。</span><span class="sxs-lookup"><span data-stu-id="f2aca-157">In this scenario, you have a template that you developed, tested, and used to deploy the production environment.</span></span> <span data-ttu-id="f2aca-158">您將在本節中設定它。</span><span class="sxs-lookup"><span data-stu-id="f2aca-158">You will set it up in this section.</span></span>

1. <span data-ttu-id="f2aca-159">建立 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 儲存機制的專屬分叉。</span><span class="sxs-lookup"><span data-stu-id="f2aca-159">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="f2aca-160">如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-160">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="f2aca-161">建立分叉之後，即可在瀏覽器中進行查看。</span><span class="sxs-lookup"><span data-stu-id="f2aca-161">Once your fork is created, you can see it in your browser.</span></span>
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="f2aca-162">開啟 Git Shell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f2aca-162">Open a Git Shell session.</span></span> <span data-ttu-id="f2aca-163">若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。</span><span class="sxs-lookup"><span data-stu-id="f2aca-163">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="f2aca-164">執行下列命令，以建立分叉的本機複製品：</span><span class="sxs-lookup"><span data-stu-id="f2aca-164">Create a local clone of your fork by executing the following command:</span></span>

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. <span data-ttu-id="f2aca-165">具有本機副本後，瀏覽至 *&lt;repository_root>*\ARMTemplates，然後執行 deploy.ps1 指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f2aca-165">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script as follows:</span></span>
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. <span data-ttu-id="f2aca-166">系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2aca-166">When prompted, type in the desired username and password for database access.</span></span>
   
   <span data-ttu-id="f2aca-167">您應該會看到各種 Azure 資源的佈建進度。</span><span class="sxs-lookup"><span data-stu-id="f2aca-167">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="f2aca-168">部署完成時，指令碼會在瀏覽器中啟動應用程式，並提供合適的嗶聲。</span><span class="sxs-lookup"><span data-stu-id="f2aca-168">When deployment completes, the script launches the application in the browser and give you a friendly beep.</span></span>
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > <span data-ttu-id="f2aca-169">查看 *&lt;repository_root>*\ARMTemplates\Deploy.ps1，以了解其如何產生具有唯一識別碼的資源。</span><span class="sxs-lookup"><span data-stu-id="f2aca-169">Take a look at *&lt;repository_root>*\ARMTemplates\Deploy.ps1, to see how it generates resources with unique IDs.</span></span> <span data-ttu-id="f2aca-170">您可以使用相同的方法來建立相同部署的複製品，而不需擔心衝突的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="f2aca-170">You can use the same approach to create clones of the same deployment without worrying about conflicting resource names.</span></span>
   > 
   > 
6. <span data-ttu-id="f2aca-171">回到 Git Shell 工作階段，並執行：</span><span class="sxs-lookup"><span data-stu-id="f2aca-171">Back in your Git Shell session, run:</span></span>
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. <span data-ttu-id="f2aca-172">指令碼完成時，請返回瀏覽至前端的位址 (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/)，以查看在生產環境中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-172">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="f2aca-173">登入 [Azure 入口網站](https://portal.azure.com/) ，並查看建立的內容。</span><span class="sxs-lookup"><span data-stu-id="f2aca-173">Log in to the [Azure portal](https://portal.azure.com/) and take a look at what’s created.</span></span>
   
   <span data-ttu-id="f2aca-174">您應可在相同的資源群組中看到兩個 Web 應用程式，其中一個的名稱具有 `Api` 後置詞。</span><span class="sxs-lookup"><span data-stu-id="f2aca-174">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="f2aca-175">如果您查看資源群組檢視，則也會看到 SQL Database 和伺服器、App Service 方案以及 Web 應用程式的預備位置。</span><span class="sxs-lookup"><span data-stu-id="f2aca-175">If you look at the resource group view, you also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="f2aca-176">瀏覽不同的資源，並將其與 *&lt;repository_root>*\ARMTemplates\ProdAndStage.json 比較以查看其在範本中的設定方式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-176">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

<span data-ttu-id="f2aca-177">您現在已設定生產環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-177">You have now set up the production environment.</span></span> <span data-ttu-id="f2aca-178">接下來，您將會開始執行應用程式的新更新。</span><span class="sxs-lookup"><span data-stu-id="f2aca-178">Next, you will kick off a new update to the application.</span></span>

## <a name="create-dev-and-test-branches"></a><span data-ttu-id="f2aca-179">建立開發和測試分支</span><span class="sxs-lookup"><span data-stu-id="f2aca-179">Create dev and test branches</span></span>
<span data-ttu-id="f2aca-180">現在，您已有在 Azure 內之生產環境中執行的複雜應用程式，您將根據敏捷式方法來更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-180">Now that you have a complex application running in production in Azure, you will make an update to your application in accordance with agile methodology.</span></span> <span data-ttu-id="f2aca-181">在本節中，您將建立需要進行必要更新的開發和測試分支。</span><span class="sxs-lookup"><span data-stu-id="f2aca-181">In this section, you will create the dev and test branches that you will need to make the required updates.</span></span>

1. <span data-ttu-id="f2aca-182">先建立測試環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-182">Create the test environment first.</span></span> <span data-ttu-id="f2aca-183">在 Git Shell 工作階段中，執行下列命令來建立稱為 **NewUpdate**的新分支環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-183">In your Git Shell session, run the following commands to create the environment for a new branch called **NewUpdate**.</span></span> 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. <span data-ttu-id="f2aca-184">系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2aca-184">When prompted, type in the desired username and password for database access.</span></span> 
   
   <span data-ttu-id="f2aca-185">部署完成時，指令碼會在瀏覽器中啟動應用程式，並提供合適的嗶聲。</span><span class="sxs-lookup"><span data-stu-id="f2aca-185">When deployment completes, the script launches the application in the browser and give you a friendly beep.</span></span> <span data-ttu-id="f2aca-186">您現在有新分支與其專屬測試環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-186">You now have a new branch with its own test environment.</span></span> <span data-ttu-id="f2aca-187">請花一點時間檢閱此測試環境的一些相關事項：</span><span class="sxs-lookup"><span data-stu-id="f2aca-187">Take a moment to review a few things about this test environment:</span></span>
   
   * <span data-ttu-id="f2aca-188">您可以在任何 Azure 訂用帳戶中建立它。</span><span class="sxs-lookup"><span data-stu-id="f2aca-188">You can create it in any Azure subscription.</span></span> <span data-ttu-id="f2aca-189">這表示可以分開管理生產環境和測試環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-189">That means the production environment can be managed separately from your test environment.</span></span>
   * <span data-ttu-id="f2aca-190">您的測試環境是即時在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="f2aca-190">Your test environment is running live in Azure.</span></span>
   * <span data-ttu-id="f2aca-191">您的測試環境等同於生產環境，差異在於預備位置和調整設定。</span><span class="sxs-lookup"><span data-stu-id="f2aca-191">Your test environment is identical to the production environment, except for the staging slots and the scaling settings.</span></span> <span data-ttu-id="f2aca-192">因為這些是 ProdandStage.json 與 Dev.json 之間的唯一差異，所以您可以得知這項資訊。</span><span class="sxs-lookup"><span data-stu-id="f2aca-192">You know it because they are the only differences between ProdandStage.json and Dev.json.</span></span>
   * <span data-ttu-id="f2aca-193">您可以在其專屬 App Service 方案與不同的價格層 (例如 **免費**) 中管理測試環境 。</span><span class="sxs-lookup"><span data-stu-id="f2aca-193">You can manage your test environment in its own App Service plan, with a different price tier (such as **Free**).</span></span>
   * <span data-ttu-id="f2aca-194">刪除這個測試環境，就像刪除資源群組一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="f2aca-194">Deleting this test environment is as simple as deleting the resource group.</span></span> <span data-ttu-id="f2aca-195">您將了解 [稍後](#delete)如何執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="f2aca-195">You will find out how to do this [later](#delete).</span></span>
3. <span data-ttu-id="f2aca-196">執行下列命令，以繼續建立開發分支：</span><span class="sxs-lookup"><span data-stu-id="f2aca-196">Go on to create a dev branch by running the following commands:</span></span>
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. <span data-ttu-id="f2aca-197">系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2aca-197">When prompted, type in the desired username and password for database access.</span></span> 
   
   <span data-ttu-id="f2aca-198">請花一點時間檢閱此開發環境的一些相關事項：</span><span class="sxs-lookup"><span data-stu-id="f2aca-198">Take a moment to review a few things about this dev environment:</span></span> 
   
   * <span data-ttu-id="f2aca-199">開發環境的組態與測試環境相同，因為它是使用相同的範本所部署。</span><span class="sxs-lookup"><span data-stu-id="f2aca-199">Your dev environment has a configuration identical to the test environment because it’s deployed using the same template.</span></span>
   * <span data-ttu-id="f2aca-200">在開發人員自己的 Azure 訂用帳戶中，可以建立每個開發環境，但分開管理測試環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-200">Each dev environment can be created in the developer’s own Azure subscription, leaving the test environment to be separately managed.</span></span>
   * <span data-ttu-id="f2aca-201">您的開發環境是即時在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="f2aca-201">Your dev environment is running live in Azure.</span></span>
   * <span data-ttu-id="f2aca-202">刪除開發環境，就像刪除資源群組一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="f2aca-202">Deleting the dev environment is as simple as deleting the resource group.</span></span> <span data-ttu-id="f2aca-203">您將了解 [稍後](#delete)如何執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="f2aca-203">You will find out how to do this [later](#delete).</span></span>

> [!NOTE]
> <span data-ttu-id="f2aca-204">有多位開發人員處理新的更新時，只要執行下列步驟，每一位都可以輕鬆地建立分支和專用開發環境：</span><span class="sxs-lookup"><span data-stu-id="f2aca-204">When you have multiple developers working on the new update, each of them can easily create a branch and dedicated dev environment with the following steps:</span></span>
> 
> 1. <span data-ttu-id="f2aca-205">在 GitHub 建立其在儲存機制中的專屬分叉 (請參閱 [分叉儲存機制](https://help.github.com/articles/fork-a-repo/))。</span><span class="sxs-lookup"><span data-stu-id="f2aca-205">Create their own fork of the repository in GitHub (see [Fork a Repo](https://help.github.com/articles/fork-a-repo/)).</span></span>
> 2. <span data-ttu-id="f2aca-206">複製其本機電腦上的分岔</span><span class="sxs-lookup"><span data-stu-id="f2aca-206">Clone the fork on their local machine</span></span>
> 3. <span data-ttu-id="f2aca-207">執行相同的命令，來建立其專屬開發分支和環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-207">Run the same commands to create their own dev branch and environment.</span></span>
> 
> 

<span data-ttu-id="f2aca-208">完成之後，GitHub 分岔應該會有三個分支：</span><span class="sxs-lookup"><span data-stu-id="f2aca-208">When you’re done, your GitHub fork should have three branches:</span></span>

![](./media/app-service-agile-software-development/test-1-github-view.png)

<span data-ttu-id="f2aca-209">而三個不同的資源群組中應該會有六個 Web 應用程式 (兩個一組，共三組)：</span><span class="sxs-lookup"><span data-stu-id="f2aca-209">And you should have six web apps (three sets of two) in three separate resource groups:</span></span>

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> <span data-ttu-id="f2aca-210">ProdandStage.json 指定生產環境來使用**標準**定價層，這適用於生產應用程式的延展性。</span><span class="sxs-lookup"><span data-stu-id="f2aca-210">ProdandStage.json specifies the production environment to use the **Standard** pricing tier, which is appropriate for scalability of the production application.</span></span>
> 
> 

## <a name="build-and-test-every-commit"></a><span data-ttu-id="f2aca-211">建置和測試每個認可</span><span class="sxs-lookup"><span data-stu-id="f2aca-211">Build and test every commit</span></span>
<span data-ttu-id="f2aca-212">範本檔 ProdAndStage.json 和 Dev.json 已經指定原始控制碼參數，其預設會設定 Web 應用程式的連續發行。</span><span class="sxs-lookup"><span data-stu-id="f2aca-212">The template files ProdAndStage.json and Dev.json already specify the source control parameters, which by default sets up continuous publishing for the web app.</span></span> <span data-ttu-id="f2aca-213">因此，GitHub 分支的每個認可都會觸發從該分支自動部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f2aca-213">Therefore, every commit to the GitHub branch triggers an automatic deployment to Azure from that branch.</span></span> <span data-ttu-id="f2aca-214">我們來看看您設定現在的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-214">Let’s see how your setup works now.</span></span>

1. <span data-ttu-id="f2aca-215">請確定您在本機儲存機制的 Dev 分支。</span><span class="sxs-lookup"><span data-stu-id="f2aca-215">Make sure that you’re in the Dev branch of the local repository.</span></span> <span data-ttu-id="f2aca-216">若要這樣做，請在 Git Shell 中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-216">To do this, run the following command in Git Shell:</span></span>
   
        git checkout Dev
2. <span data-ttu-id="f2aca-217">將程式碼變更為使用 [Bootstrap](http://getbootstrap.com/components/) 清單，以對應用程式的 UI 層進行變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-217">Make a change to the app’s UI layer by changing the code to use [Bootstrap](http://getbootstrap.com/components/) lists.</span></span> <span data-ttu-id="f2aca-218">開啟 *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml，並進行以下反白顯示的變更：</span><span class="sxs-lookup"><span data-stu-id="f2aca-218">Open *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml and make the following highlighted change:</span></span>
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > <span data-ttu-id="f2aca-219">如果您無法讀取上述的影像：</span><span class="sxs-lookup"><span data-stu-id="f2aca-219">If you can't read the preceding image:</span></span> 
    > 
    > * <span data-ttu-id="f2aca-220">在第 18 行，將 `check-list` 變更為 `list-group`。</span><span class="sxs-lookup"><span data-stu-id="f2aca-220">In line 18, change `check-list` to `list-group`.</span></span>
    > * <span data-ttu-id="f2aca-221">在第 19 行，將 `class="check-list-item"` 變更為 `class="list-group-item"`。</span><span class="sxs-lookup"><span data-stu-id="f2aca-221">In line 19, change `class="check-list-item"` to `class="list-group-item"`.</span></span>
    > 
    > 
3. <span data-ttu-id="f2aca-222">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-222">Save the change.</span></span> <span data-ttu-id="f2aca-223">回到 Git Shell，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-223">Back in Git Shell, run the following commands:</span></span>
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   <span data-ttu-id="f2aca-224">這些 git 命令與另一個原始檔控制系統中的「簽入程式碼」類似 (例如 TFS)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-224">These git commands are similar to "checking in your code" in another source control system like TFS.</span></span> <span data-ttu-id="f2aca-225">執行 `git push`時，新的認可會觸發自動將程式碼推送至 Azure，然後重建應用程式，以反映開發環境中的變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-225">When you run `git push`, the new commit triggers an automatic code push to Azure, which then rebuilds the application to reflect the change in the dev environment.</span></span>
4. <span data-ttu-id="f2aca-226">若要確認已將此程式碼推送至您的開發環境，請移至您開發環境的 Web 應用程式分頁，並查看 [部署] 組件。</span><span class="sxs-lookup"><span data-stu-id="f2aca-226">To verify that this code push to your dev environment has occurred, go to your dev environment’s web app page and look at the **Deployment** part.</span></span> <span data-ttu-id="f2aca-227">您應該可以在這裡看到最新認可的訊息。</span><span class="sxs-lookup"><span data-stu-id="f2aca-227">You should be able to see your latest commit message there.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. <span data-ttu-id="f2aca-228">在其中按一下 [瀏覽]  ，以查看 Azure 中即時應用程式的新變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-228">From there, click **Browse** to see the new change in the live application in Azure.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   <span data-ttu-id="f2aca-229">這對應用程式而言是相當小的變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-229">It's a minor change to the application.</span></span> <span data-ttu-id="f2aca-230">不過，複雜 Web 應用程式的新變更通常會有不想要和非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="f2aca-230">However, many times new changes to a complex web application have unintended and undesirable side effects.</span></span> <span data-ttu-id="f2aca-231">能夠輕鬆地測試即時組建中的每個認可，可讓您在客戶看到這些問題之前先找出它們。</span><span class="sxs-lookup"><span data-stu-id="f2aca-231">Being able to easily test every commit in live builds enables you to catch these issues before your customers see them.</span></span>

<span data-ttu-id="f2aca-232">現在，您應已熟悉開發人員在 **NewUpdate** 專案中如何實現，並可以輕鬆地建立專屬開發環境，然後建置每個認可並測試每個組建。</span><span class="sxs-lookup"><span data-stu-id="f2aca-232">By now, you should be comfortable with the realization that, as a developer on the **NewUpdate** project, you can create a dev environment for yourself, then build every commit and test every build.</span></span>

## <a name="merge-code-into-test-environment"></a><span data-ttu-id="f2aca-233">將程式碼合併至測試環境</span><span class="sxs-lookup"><span data-stu-id="f2aca-233">Merge code into test environment</span></span>
<span data-ttu-id="f2aca-234">準備好將程式碼從 Dev 分支推送至 NewUpdate 分支時，這是標準 git 程序：</span><span class="sxs-lookup"><span data-stu-id="f2aca-234">When you’re ready to push your code from Dev branch up to NewUpdate branch, it’s the standard git process:</span></span>

1. <span data-ttu-id="f2aca-235">在 GitHub 中，將 NewUpdate 的任何新認可合併至 Dev 分支 (例如其他開發人員所建立的認可)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-235">Merge any new commits to NewUpdate into the Dev branch in GitHub, such as commits created by other developers.</span></span> <span data-ttu-id="f2aca-236">GitHub 上的任何新認可都會在開發環境中觸發程式碼推送和建置。</span><span class="sxs-lookup"><span data-stu-id="f2aca-236">Any new commit on GitHub triggers a code push and build in the dev environment.</span></span> <span data-ttu-id="f2aca-237">您接著可以確定 Dev 分支中的程式碼仍能與 NewUpdate 分支中的最新位元運作。</span><span class="sxs-lookup"><span data-stu-id="f2aca-237">You can then make sure your code in Dev branch still works with the latest bits from NewUpdate branch.</span></span>
2. <span data-ttu-id="f2aca-238">在 GitHub 中，將所有新認可從 Dev 分支合併至 NewUpdate 分支。</span><span class="sxs-lookup"><span data-stu-id="f2aca-238">Merge all your new commits from Dev branch into NewUpdate branch on GitHub.</span></span> <span data-ttu-id="f2aca-239">這個動作會在測試環境中觸發程式碼推送和建置。</span><span class="sxs-lookup"><span data-stu-id="f2aca-239">This action triggers a code push and build in the test environment.</span></span> 

<span data-ttu-id="f2aca-240">請再次注意，因為連續部署已設定這些 git 分支，所以不需要採取任何其他動作 (例如執行整合建置)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-240">Note again that because continuous deployment is already set up with these git branches, you don’t need to take any other action like running integration builds.</span></span> <span data-ttu-id="f2aca-241">您只需要使用 git 執行標準原始檔控制作法，Azure 就會為您執行所有建置程序。</span><span class="sxs-lookup"><span data-stu-id="f2aca-241">You simply need to perform standard source control practices using git, and Azure performs all the build processes for you.</span></span>

<span data-ttu-id="f2aca-242">現在，請將您的程式碼推送至 **NewUpdate** 分支。</span><span class="sxs-lookup"><span data-stu-id="f2aca-242">Now, let’s push your code to **NewUpdate** branch.</span></span> <span data-ttu-id="f2aca-243">在 Git Shell 中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-243">In Git Shell, run the following commands:</span></span>

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

<span data-ttu-id="f2aca-244">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="f2aca-244">That’s it!</span></span> 

<span data-ttu-id="f2aca-245">前往您測試環境的 Web 應用程式分頁，以查看現在推送至測試環境的新認可 (合併至 NewUpdate 分支)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-245">Go to the web app page for your test environment to see your new commit (merged into NewUpdate branch) now pushed to the test environment.</span></span> <span data-ttu-id="f2aca-246">然後按一下 [瀏覽]  ，以查看現在於 Azure 中即時執行的樣式變更。</span><span class="sxs-lookup"><span data-stu-id="f2aca-246">Then, click **Browse** to see that the style change is now running live in Azure.</span></span>

## <a name="deploy-update-to-production"></a><span data-ttu-id="f2aca-247">將更新部署至生產環境</span><span class="sxs-lookup"><span data-stu-id="f2aca-247">Deploy update to production</span></span>
<span data-ttu-id="f2aca-248">將程式碼推送至預備和生產環境，應該與先前將程式碼所推送的測試環境相同。</span><span class="sxs-lookup"><span data-stu-id="f2aca-248">Pushing code to the staging and production environment should feel no different than what you’ve already done when you pushed code to the test environment.</span></span> <span data-ttu-id="f2aca-249">真的就是這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="f2aca-249">It's really that simple.</span></span> 

<span data-ttu-id="f2aca-250">在 Git Shell 中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-250">In Git Shell, run the following commands:</span></span>

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

<span data-ttu-id="f2aca-251">請記住，根據在 ProdandStage.json 中設定預備和生產環境的方式，新的程式碼會推送至 [預備] 位置並在該處執行。</span><span class="sxs-lookup"><span data-stu-id="f2aca-251">Remember that based on the way the staging and production environment is set up in ProdandStage.json, your new code is pushed to the **Staging** slot and is running there.</span></span> <span data-ttu-id="f2aca-252">因此，如果您導覽至預備位置的 URL，則會看到新的程式碼正在該處執行。</span><span class="sxs-lookup"><span data-stu-id="f2aca-252">So if you navigate to the staging slot’s URL, you see the new code running there.</span></span> <span data-ttu-id="f2aca-253">若要這樣做，請在 Git Shell 中執行下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f2aca-253">To do this, run the following cmdlet in Git Shell.</span></span>

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

<span data-ttu-id="f2aca-254">現在，在預備位置中驗證過更新之後，唯一需要執行的事項是將它交換至生產環境。</span><span class="sxs-lookup"><span data-stu-id="f2aca-254">And now, after you’ve verified the update in the staging slot, the only thing left to do is to swap it into production.</span></span> <span data-ttu-id="f2aca-255">在 Git Shell 中，只要執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-255">In Git Shell, just run the following commands:</span></span>

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

<span data-ttu-id="f2aca-256">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2aca-256">Congratulations!</span></span> <span data-ttu-id="f2aca-257">您已順利將新的更新發行至生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2aca-257">You’ve successfully published a new update to your production web application.</span></span> <span data-ttu-id="f2aca-258">不僅如此，完成的方式也只是輕鬆地建立開發和測試環境，以及建置和測試每個認可。</span><span class="sxs-lookup"><span data-stu-id="f2aca-258">What’s more is that did it by easily creating dev and test environments, and building and testing every commit.</span></span> <span data-ttu-id="f2aca-259">這些是敏捷式軟體開發的重要建置組塊。</span><span class="sxs-lookup"><span data-stu-id="f2aca-259">These are crucial building blocks for agile software development.</span></span>

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a><span data-ttu-id="f2aca-260">刪除開發和測試環境</span><span class="sxs-lookup"><span data-stu-id="f2aca-260">Delete dev and test environments</span></span>
<span data-ttu-id="f2aca-261">因為您刻意將開發和測試環境架構為獨立資源群組，所以可以很容易刪除它們。</span><span class="sxs-lookup"><span data-stu-id="f2aca-261">Because you have purposely architected your dev and test environments to be self-contained resource groups, it is easy to delete them.</span></span> <span data-ttu-id="f2aca-262">若要刪除您在本教學課程中建立的環境 (GitHub 分支和 Azure 構件)，則只要在 Git Shell 中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2aca-262">To delete the ones you created in this tutorial, both the GitHub branches and Azure artifacts, just run the following commands in Git Shell:</span></span>

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a><span data-ttu-id="f2aca-263">摘要</span><span class="sxs-lookup"><span data-stu-id="f2aca-263">Summary</span></span>
<span data-ttu-id="f2aca-264">對於許多想要採用 Azure 做為其應用程式平台的公司而言，敏捷式軟體開發是必要的。</span><span class="sxs-lookup"><span data-stu-id="f2aca-264">Agile software development is a must-have for many companies who want to adopt Azure as their application platform.</span></span> <span data-ttu-id="f2aca-265">在本教學課程中，您已經學會如何輕鬆地建立和終止生產環境的確切複本或接近複本，甚至針對複雜應用程式也是一樣。</span><span class="sxs-lookup"><span data-stu-id="f2aca-265">In this tutorial, you have learned how to create and tear down exact replicas or near replicas of the production environment with ease, even for complex applications.</span></span> <span data-ttu-id="f2aca-266">您也學到如何運用這項功能來建立開發程序，以建置和測試 Azure 中的每個認可。</span><span class="sxs-lookup"><span data-stu-id="f2aca-266">You have also learned how to leverage this ability to create a development process that can build and test every single commit in Azure.</span></span> <span data-ttu-id="f2aca-267">本教學課程希望示範如何最恰當地搭配使用 Azure App Service 和 Azure 資源管理員，來建立提供敏捷式方法的 DevOps 方案。</span><span class="sxs-lookup"><span data-stu-id="f2aca-267">This tutorial has hopefully shown you how you can best use Azure App Service and Azure Resource Manager together to create a DevOps solution that caters to agile methodologies.</span></span> <span data-ttu-id="f2aca-268">接下來，您可以透過執行進階 DevOps 技術 (例如 [在生產環境中測試](app-service-web-test-in-production-get-start.md))，建置此案例。</span><span class="sxs-lookup"><span data-stu-id="f2aca-268">Next, you can build on this scenario by performing advanced DevOps techniques such as [testing in production](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="f2aca-269">如需生產過程中測試的常見案例，請參閱 [Azure App Service 中的快速部署 (beta 測試)](app-service-web-test-in-production-controlled-test-flight.md)。</span><span class="sxs-lookup"><span data-stu-id="f2aca-269">For a common testing-in-production scenario, see [Flighting deployment (beta testing) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).</span></span>

## <a name="more-resources"></a><span data-ttu-id="f2aca-270">其他資源</span><span class="sxs-lookup"><span data-stu-id="f2aca-270">More resources</span></span>
* [<span data-ttu-id="f2aca-271">透過可預測方式在 Azure 中部署複雜應用程式</span><span class="sxs-lookup"><span data-stu-id="f2aca-271">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="f2aca-272">敏捷式開發作法：現代化開發週期的秘訣和訣竅</span><span class="sxs-lookup"><span data-stu-id="f2aca-272">Agile Development in Practice: Tips and Tricks for Modernized Development Cycle</span></span>](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [<span data-ttu-id="f2aca-273">使用資源管理員範本之 Azure Web 應用程式的進階部署策略</span><span class="sxs-lookup"><span data-stu-id="f2aca-273">Advanced deployment strategies for Azure Web Apps using Resource Manager templates</span></span>](http://channel9.msdn.com/Events/Build/2015/2-620)
* [<span data-ttu-id="f2aca-274">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="f2aca-274">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="f2aca-275">JSONLint - JSON 驗證程式</span><span class="sxs-lookup"><span data-stu-id="f2aca-275">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="f2aca-276">ARMClient - 設定 GitHub 發行至網站</span><span class="sxs-lookup"><span data-stu-id="f2aca-276">ARMClient – Set up GitHub publishing to site</span></span>](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [<span data-ttu-id="f2aca-277">分支 - 基本分支和合併</span><span class="sxs-lookup"><span data-stu-id="f2aca-277">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="f2aca-278">David Ebbo 的部落格</span><span class="sxs-lookup"><span data-stu-id="f2aca-278">David Ebbo’s Blog</span></span>](http://blog.davidebbo.com/)
* [<span data-ttu-id="f2aca-279">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2aca-279">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="f2aca-280">Azure 跨平台命令列工具</span><span class="sxs-lookup"><span data-stu-id="f2aca-280">Azure Cross-Platform Command-Line Tools</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="f2aca-281">在 Azure AD 中建立或編輯使用者</span><span class="sxs-lookup"><span data-stu-id="f2aca-281">Create or edit users in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [<span data-ttu-id="f2aca-282">專案 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="f2aca-282">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)

