---
title: "使用 Azure App Service aaaAgile 軟體開發"
description: "深入了解如何 toocreate 高延展複雜的應用程式使用 Azure App Service 支援敏捷式軟體開發的方式。"
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
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a><span data-ttu-id="72e94-103">使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)</span><span class="sxs-lookup"><span data-stu-id="72e94-103">Agile software development with Azure App Service</span></span>
<span data-ttu-id="72e94-104">在此教學課程中，您將學習如何 toocreate 高延展複雜的應用程式與[Azure App Service](/azure/app-service/)支援的方式[敏捷式軟體開發](https://en.wikipedia.org/wiki/Agile_software_development)。</span><span class="sxs-lookup"><span data-stu-id="72e94-104">In this tutorial, you will learn how toocreate high-scale complex applications with [Azure App Service](/azure/app-service/) in a way that supports [agile software development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="72e94-105">它會假設您已經知道如何太[部署如預期般在 Azure 中的複雜應用程式](app-service-deploy-complex-application-predictably.md)。</span><span class="sxs-lookup"><span data-stu-id="72e94-105">It assumes that you already know how too[deploy complex applications predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="72e94-106">限制技術的處理序中通常可以獨立 hello 成功 agile 方法實作方式。</span><span class="sxs-lookup"><span data-stu-id="72e94-106">Limitations in technical processes can often stand in hello way of successful implementation of agile methodologies.</span></span> <span data-ttu-id="72e94-107">Azure App Service 功能，例如[持續發行](app-service-continuous-deployment.md)，[預備環境](web-sites-staged-publishing.md)（位置），和[監視](web-sites-monitor.md)、 結合請明智地與 hello 協調流程時及管理網站中的部署[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)，可以是很好的解決方案的一部分的開發採用敏捷式軟體開發人員。</span><span class="sxs-lookup"><span data-stu-id="72e94-107">Azure App Service with features such as [continuous publishing](app-service-continuous-deployment.md), [staging environments](web-sites-staged-publishing.md) (slots), and [monitoring](web-sites-monitor.md), when coupled wisely with hello orchestration and management of deployment in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), can be part of a great solution for developers who embrace agile software development.</span></span>

<span data-ttu-id="72e94-108">hello 表是靈活的開發與相關聯的需求的簡短清單以及 Azure 服務可讓每個。</span><span class="sxs-lookup"><span data-stu-id="72e94-108">hello following table is a short list of requirements associated with agile development, and how Azure services enable each of them.</span></span>

| <span data-ttu-id="72e94-109">需求</span><span class="sxs-lookup"><span data-stu-id="72e94-109">Requirement</span></span> | <span data-ttu-id="72e94-110">如何讓 Azure</span><span class="sxs-lookup"><span data-stu-id="72e94-110">How Azure enables</span></span> |
| --- | --- |
| <span data-ttu-id="72e94-111">- 使用每個認可建置</span><span class="sxs-lookup"><span data-stu-id="72e94-111">- Build with every commit</span></span><br><span data-ttu-id="72e94-112">- 自動並快速地建置</span><span class="sxs-lookup"><span data-stu-id="72e94-112">- Build automatically and fast</span></span> |<span data-ttu-id="72e94-113">設定持續部署時，Azure App Service 可以根據 dev 分支作用為即時執行組建。</span><span class="sxs-lookup"><span data-stu-id="72e94-113">When configured with continuous deployment, Azure App Service can function as live-running builds based on a dev branch.</span></span> <span data-ttu-id="72e94-114">每次推送 toohello 分支程式碼，則為自動建置及執行即時 Azure。</span><span class="sxs-lookup"><span data-stu-id="72e94-114">Every time code is pushed toohello branch, it is automatically built and running live in Azure.</span></span> |
| <span data-ttu-id="72e94-115">- 將組建設為自我測試</span><span class="sxs-lookup"><span data-stu-id="72e94-115">- Make builds self-testing</span></span> |<span data-ttu-id="72e94-116">負載測試、 web 測試等，您可以部署與 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="72e94-116">Load tests, web tests, etc., can be deployed with hello Azure Resource Manager template.</span></span> |
| <span data-ttu-id="72e94-117">- 在生產環境的複製品中執行測試</span><span class="sxs-lookup"><span data-stu-id="72e94-117">- Perform tests in a clone of production environment</span></span> |<span data-ttu-id="72e94-118">Azure 資源管理員範本可以使用的 toocreate 的複製程式碼 hello Azure 生產環境 （包括應用程式設定、 連接字串範本、 調整等） 來測試快速和預測的方式。</span><span class="sxs-lookup"><span data-stu-id="72e94-118">Azure Resource Manager templates can be used toocreate clones of hello Azure production environment (including app settings, connection string templates, scaling, etc.) for testing quickly and predictably.</span></span> |
| <span data-ttu-id="72e94-119">- 輕鬆地檢視最新組建結果</span><span class="sxs-lookup"><span data-stu-id="72e94-119">- View result of latest build easily</span></span> |<span data-ttu-id="72e94-120">從儲存機制的連續部署 tooAzure 表示，您可以測試新的程式碼中即時應用程式認可您的變更之後，立即。</span><span class="sxs-lookup"><span data-stu-id="72e94-120">Continuous deployment tooAzure from a repository means that you can test new code in a live application immediately after you commit your changes.</span></span> |
| <span data-ttu-id="72e94-121">-認可 toohello 主要分支中每一天</span><span class="sxs-lookup"><span data-stu-id="72e94-121">- Commit toohello main branch every day</span></span><br><span data-ttu-id="72e94-122">- 自動化部署</span><span class="sxs-lookup"><span data-stu-id="72e94-122">- Automate deployment</span></span> |<span data-ttu-id="72e94-123">持續整合與主要分支中的儲存機制的實際執行應用程式的自動部署每個認可/merge toohello 主要分支 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="72e94-123">Continuous integration of a production application with a repository’s main branch automatically deploys every commit/merge toohello main branch tooproduction.</span></span> |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="72e94-124">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="72e94-124">What you will do</span></span>
<span data-ttu-id="72e94-125">您將逐步進行一般的開發人員測試階段-生產工作流程中順序 toopublish 新變更 toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)範例應用程式，都包含兩個[web 應用程式](/services/app-service/web/)，一個是前端 (FE) 和hello 另一個則是 Web API 後端 （相當），和[SQL database](/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="72e94-125">You will walk through a typical dev-test-stage-production workflow in order toopublish new changes toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) sample application, which consists of two [web apps](/services/app-service/web/), one being a frontend (FE) and hello other being a Web API backend (BE), and a [SQL database](/services/sql-database/).</span></span> <span data-ttu-id="72e94-126">您可以使用下列部署架構 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-126">You will work with hello following deployment architecture:</span></span>

![](./media/app-service-agile-software-development/what-1-architecture.png)

<span data-ttu-id="72e94-127">tooput hello 圖片的文字：</span><span class="sxs-lookup"><span data-stu-id="72e94-127">tooput hello picture into words:</span></span>

* <span data-ttu-id="72e94-128">hello 部署架構分成三個不同環境 (或[資源群組](../azure-resource-manager/resource-group-overview.md)在 Azure 中)，每個都有它自己[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，[調整](web-sites-scale.md)設定，與 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="72e94-128">hello deployment architecture is separated into three distinct environments (or [resource groups](../azure-resource-manager/resource-group-overview.md) in Azure), each with its own [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [scaling](web-sites-scale.md) settings, and SQL database.</span></span> 
* <span data-ttu-id="72e94-129">您可以個別管理每個環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-129">Each environment can be managed separately.</span></span> <span data-ttu-id="72e94-130">它們甚至可以存在於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="72e94-130">They can even exist in different subscriptions.</span></span>
* <span data-ttu-id="72e94-131">預備和生產環境會實作為兩個位置的 hello 相同 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-131">Staging and production are implemented as two slots of hello same App Service app.</span></span> <span data-ttu-id="72e94-132">持續整合的 hello 主要分支會以 hello staging 位置設定。</span><span class="sxs-lookup"><span data-stu-id="72e94-132">hello master branch is set up for continuous integration with hello staging slot.</span></span>
* <span data-ttu-id="72e94-133">Hello 認可 toomaster 分支時驗證 hello staging （與實際資料） 的位置上，確認臨時的應用程式會為 hello 生產位置交換[不需停機](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="72e94-133">When a commit toomaster branch is verified on hello staging slot (with production data), hello verified staging app is swapped into hello production slot [with no downtime](web-sites-staged-publishing.md).</span></span>

<span data-ttu-id="72e94-134">hello 生產與預備環境由定義在 hello 範本[  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json)。</span><span class="sxs-lookup"><span data-stu-id="72e94-134">hello production and staging environment is defined by hello template at [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).</span></span>

<span data-ttu-id="72e94-135">hello 開發人員和測試環境由在 hello 範本定義[  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json)。</span><span class="sxs-lookup"><span data-stu-id="72e94-135">hello dev and test environments are defined by hello template at [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).</span></span>

<span data-ttu-id="72e94-136">您也會使用 hello 典型的分支策略，以從 hello dev 分支向上 toohello 測試 」 分支，然後 toohello （向上在品質上，因此 toospeak 移） 的主要分支的程式碼。</span><span class="sxs-lookup"><span data-stu-id="72e94-136">You will also use hello typical branching strategy, with code moving from hello dev branch up toohello test branch, then toohello master branch (moving up in quality, so toospeak).</span></span>

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a><span data-ttu-id="72e94-137">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="72e94-137">What you need</span></span>
* <span data-ttu-id="72e94-138">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="72e94-138">An Azure account</span></span>
* <span data-ttu-id="72e94-139">一個 [GitHub](https://github.com/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="72e94-139">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="72e94-140">Git 殼層 (隨[GitHub for Windows](https://windows.github.com/))-可讓您 toorun 兩者 hello Git 和 PowerShell 中的命令 hello 相同工作階段</span><span class="sxs-lookup"><span data-stu-id="72e94-140">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - enables you toorun both hello Git and PowerShell commands in hello same session</span></span> 
* <span data-ttu-id="72e94-141">最新 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 位元</span><span class="sxs-lookup"><span data-stu-id="72e94-141">Latest [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits</span></span>
* <span data-ttu-id="72e94-142">基本的了解的 hello 下列工具：</span><span class="sxs-lookup"><span data-stu-id="72e94-142">Basic understanding of hello following tools:</span></span>
  * <span data-ttu-id="72e94-143">[Azure Resource Manager ](../azure-resource-manager/resource-group-overview.md)範本部署 (另請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="72e94-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (also see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="72e94-144">Git</span><span class="sxs-lookup"><span data-stu-id="72e94-144">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="72e94-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72e94-145">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="72e94-146">您需要 Azure 帳戶 toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="72e94-146">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="72e94-147">您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且它們甚至用完之後，您可以保留 hello 帳戶並使用免費的 Azure 服務，例如 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-147">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="72e94-148">您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="72e94-148">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> <span data-ttu-id="72e94-149">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="72e94-149">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="72e94-150">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="72e94-150">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="set-up-your-production-environment"></a><span data-ttu-id="72e94-151">設定生產環境</span><span class="sxs-lookup"><span data-stu-id="72e94-151">Set up your production environment</span></span>
> [!NOTE]
> <span data-ttu-id="72e94-152">自動使用此教學課程中的 hello 指令碼會設定從 GitHub 儲存機制持續發行。</span><span class="sxs-lookup"><span data-stu-id="72e94-152">hello script used in this tutorial automatically configures continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="72e94-153">這會要求您的 GitHub 認證已儲存在 Azure 中，否則 hello 編寫指令碼部署會在失敗時嘗試 tooconfigure hello web 應用程式的原始檔控制設定。</span><span class="sxs-lookup"><span data-stu-id="72e94-153">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment fails when attempting tooconfigure source control settings for hello web apps.</span></span> 
> 
> <span data-ttu-id="72e94-154">toostore 您的 GitHub 認證在 Azure 中建立 web 應用程式在 hello [Azure 入口網站](https://portal.azure.com/)和[設定 GitHub 部署](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="72e94-154">toostore your GitHub credentials in Azure, create a web app in hello [Azure portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="72e94-155">您只需要 toodo 這一次。</span><span class="sxs-lookup"><span data-stu-id="72e94-155">You only need toodo this once.</span></span> 
> 
> 

<span data-ttu-id="72e94-156">在典型的 DevOps 案例中，您必須在 Azure 中，即時執行的應用程式而您想 toomake 變更 tooit 透過連續的發佈功能。</span><span class="sxs-lookup"><span data-stu-id="72e94-156">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="72e94-157">在此案例中，您有範本，您開發、 測試及使用 toodeploy hello 實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-157">In this scenario, you have a template that you developed, tested, and used toodeploy hello production environment.</span></span> <span data-ttu-id="72e94-158">您將在本節中設定它。</span><span class="sxs-lookup"><span data-stu-id="72e94-158">You will set it up in this section.</span></span>

1. <span data-ttu-id="72e94-159">建立您自己的 hello 分岔[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="72e94-159">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="72e94-160">如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。</span><span class="sxs-lookup"><span data-stu-id="72e94-160">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="72e94-161">建立分叉之後，即可在瀏覽器中進行查看。</span><span class="sxs-lookup"><span data-stu-id="72e94-161">Once your fork is created, you can see it in your browser.</span></span>
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="72e94-162">開啟 Git Shell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="72e94-162">Open a Git Shell session.</span></span> <span data-ttu-id="72e94-163">若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。</span><span class="sxs-lookup"><span data-stu-id="72e94-163">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="72e94-164">建立您分支的本機複本執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-164">Create a local clone of your fork by executing hello following command:</span></span>

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. <span data-ttu-id="72e94-165">您的本機複本之後，瀏覽過*&lt;repository_root >*\ARMTemplates 及執行的 hello deploy.ps1 指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="72e94-165">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script as follows:</span></span>
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. <span data-ttu-id="72e94-166">出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="72e94-166">When prompted, type in hello desired username and password for database access.</span></span>
   
   <span data-ttu-id="72e94-167">您應該會看到 hello 佈建各種不同的 Azure 資源的進度。</span><span class="sxs-lookup"><span data-stu-id="72e94-167">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="72e94-168">當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。</span><span class="sxs-lookup"><span data-stu-id="72e94-168">When deployment completes, hello script launches hello application in hello browser and give you a friendly beep.</span></span>
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > <span data-ttu-id="72e94-169">看看 *&lt;repository_root >*\ARMTemplates\Deploy.ps1、 toosee 方式會產生資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="72e94-169">Take a look at *&lt;repository_root>*\ARMTemplates\Deploy.ps1, toosee how it generates resources with unique IDs.</span></span> <span data-ttu-id="72e94-170">您可以使用相同的方法 toocreate 複製的 hello hello 相同部署而不需擔心衝突的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="72e94-170">You can use hello same approach toocreate clones of hello same deployment without worrying about conflicting resource names.</span></span>
   > 
   > 
6. <span data-ttu-id="72e94-171">回到 Git Shell 工作階段，並執行：</span><span class="sxs-lookup"><span data-stu-id="72e94-171">Back in your Git Shell session, run:</span></span>
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. <span data-ttu-id="72e94-172">Hello 指令碼完成時，請返回 toobrowse toohello 前端的位址 (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello 應用程式在生產環境中執行。</span><span class="sxs-lookup"><span data-stu-id="72e94-172">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="72e94-173">登入 toohello [Azure 入口網站](https://portal.azure.com/)，看看建立的內容。</span><span class="sxs-lookup"><span data-stu-id="72e94-173">Log in toohello [Azure portal](https://portal.azure.com/) and take a look at what’s created.</span></span>
   
   <span data-ttu-id="72e94-174">您應該在 hello 無法 toosee 兩個 web 應用程式相同的資源群組、 具有 hello `Api` hello 名稱中的後置詞。</span><span class="sxs-lookup"><span data-stu-id="72e94-174">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="72e94-175">如果您看一下 hello 資源群組檢視，您也看到 hello SQL 資料庫以及伺服器、 hello 應用程式服務方案及 hello 預備位置 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-175">If you look at hello resource group view, you also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="72e94-176">瀏覽 hello 不同的資源，並比較它們與 *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 範本中的設定方式。</span><span class="sxs-lookup"><span data-stu-id="72e94-176">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

<span data-ttu-id="72e94-177">您現在已設定 hello 實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-177">You have now set up hello production environment.</span></span> <span data-ttu-id="72e94-178">接下來，您會啟動新的更新 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-178">Next, you will kick off a new update toohello application.</span></span>

## <a name="create-dev-and-test-branches"></a><span data-ttu-id="72e94-179">建立開發和測試分支</span><span class="sxs-lookup"><span data-stu-id="72e94-179">Create dev and test branches</span></span>
<span data-ttu-id="72e94-180">既然您已在 Azure 中的生產環境中執行複雜的應用程式，您就會更新 tooyour 應用程式根據敏捷式軟體開發方法。</span><span class="sxs-lookup"><span data-stu-id="72e94-180">Now that you have a complex application running in production in Azure, you will make an update tooyour application in accordance with agile methodology.</span></span> <span data-ttu-id="72e94-181">在本節中，您將建立 hello 開發和測試，您將需要 toomake hello 需要更新的分支。</span><span class="sxs-lookup"><span data-stu-id="72e94-181">In this section, you will create hello dev and test branches that you will need toomake hello required updates.</span></span>

1. <span data-ttu-id="72e94-182">第一次建立 hello 測試環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-182">Create hello test environment first.</span></span> <span data-ttu-id="72e94-183">在您的 Git 殼層工作階段中執行的 hello 下列命令呼叫新的分支的 toocreate hello 環境**NewUpdate**。</span><span class="sxs-lookup"><span data-stu-id="72e94-183">In your Git Shell session, run hello following commands toocreate hello environment for a new branch called **NewUpdate**.</span></span> 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. <span data-ttu-id="72e94-184">出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="72e94-184">When prompted, type in hello desired username and password for database access.</span></span> 
   
   <span data-ttu-id="72e94-185">當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。</span><span class="sxs-lookup"><span data-stu-id="72e94-185">When deployment completes, hello script launches hello application in hello browser and give you a friendly beep.</span></span> <span data-ttu-id="72e94-186">您現在有新分支與其專屬測試環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-186">You now have a new branch with its own test environment.</span></span> <span data-ttu-id="72e94-187">採用目前 tooreview 此測試環境的相關的幾件事：</span><span class="sxs-lookup"><span data-stu-id="72e94-187">Take a moment tooreview a few things about this test environment:</span></span>
   
   * <span data-ttu-id="72e94-188">您可以在任何 Azure 訂用帳戶中建立它。</span><span class="sxs-lookup"><span data-stu-id="72e94-188">You can create it in any Azure subscription.</span></span> <span data-ttu-id="72e94-189">這表示 hello 實際執行環境可以從您的測試環境的個別加以管理。</span><span class="sxs-lookup"><span data-stu-id="72e94-189">That means hello production environment can be managed separately from your test environment.</span></span>
   * <span data-ttu-id="72e94-190">您的測試環境是即時在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="72e94-190">Your test environment is running live in Azure.</span></span>
   * <span data-ttu-id="72e94-191">您的測試環境是相同的 toohello 生產環境中，除了預備位置的 hello 與 hello 調整設定。</span><span class="sxs-lookup"><span data-stu-id="72e94-191">Your test environment is identical toohello production environment, except for hello staging slots and hello scaling settings.</span></span> <span data-ttu-id="72e94-192">您知道它因為它們是 hello ProdandStage.json 與稱為之間唯一的差異。</span><span class="sxs-lookup"><span data-stu-id="72e94-192">You know it because they are hello only differences between ProdandStage.json and Dev.json.</span></span>
   * <span data-ttu-id="72e94-193">您可以在其專屬 App Service 方案與不同的價格層 (例如 **免費**) 中管理測試環境 。</span><span class="sxs-lookup"><span data-stu-id="72e94-193">You can manage your test environment in its own App Service plan, with a different price tier (such as **Free**).</span></span>
   * <span data-ttu-id="72e94-194">刪除這個測試環境很簡單，只刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="72e94-194">Deleting this test environment is as simple as deleting hello resource group.</span></span> <span data-ttu-id="72e94-195">您將了解 toodo 這[稍後](#delete)。</span><span class="sxs-lookup"><span data-stu-id="72e94-195">You will find out how toodo this [later](#delete).</span></span>
3. <span data-ttu-id="72e94-196">請繼續的 toocreate 執行 dev 分支 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="72e94-196">Go on toocreate a dev branch by running hello following commands:</span></span>
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. <span data-ttu-id="72e94-197">出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="72e94-197">When prompted, type in hello desired username and password for database access.</span></span> 
   
   <span data-ttu-id="72e94-198">採用目前 tooreview 關於此開發人員環境的幾件事：</span><span class="sxs-lookup"><span data-stu-id="72e94-198">Take a moment tooreview a few things about this dev environment:</span></span> 
   
   * <span data-ttu-id="72e94-199">您的開發人員環境具有組態相同 toohello 測試環境，因為它已部署使用 hello 相同的範本。</span><span class="sxs-lookup"><span data-stu-id="72e94-199">Your dev environment has a configuration identical toohello test environment because it’s deployed using hello same template.</span></span>
   * <span data-ttu-id="72e94-200">每一個開發環境可以建立 hello 開發人員自己的 Azure 訂用帳戶中，保留 hello 測試環境 toobe 分開管理。</span><span class="sxs-lookup"><span data-stu-id="72e94-200">Each dev environment can be created in hello developer’s own Azure subscription, leaving hello test environment toobe separately managed.</span></span>
   * <span data-ttu-id="72e94-201">您的開發環境是即時在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="72e94-201">Your dev environment is running live in Azure.</span></span>
   * <span data-ttu-id="72e94-202">刪除 hello 開發人員環境很簡單，只刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="72e94-202">Deleting hello dev environment is as simple as deleting hello resource group.</span></span> <span data-ttu-id="72e94-203">您將了解 toodo 這[稍後](#delete)。</span><span class="sxs-lookup"><span data-stu-id="72e94-203">You will find out how toodo this [later](#delete).</span></span>

> [!NOTE]
> <span data-ttu-id="72e94-204">當有多位開發人員在 hello 新更新時，每個可以輕鬆地以 hello 步驟下建立分支和專用的開發環境：</span><span class="sxs-lookup"><span data-stu-id="72e94-204">When you have multiple developers working on hello new update, each of them can easily create a branch and dedicated dev environment with hello following steps:</span></span>
> 
> 1. <span data-ttu-id="72e94-205">建立自己的分岔 hello 儲存機制的 GitHub 中 (請參閱[分叉儲存機制](https://help.github.com/articles/fork-a-repo/))。</span><span class="sxs-lookup"><span data-stu-id="72e94-205">Create their own fork of hello repository in GitHub (see [Fork a Repo](https://help.github.com/articles/fork-a-repo/)).</span></span>
> 2. <span data-ttu-id="72e94-206">複製其本機電腦上的 「 分叉 」 hello</span><span class="sxs-lookup"><span data-stu-id="72e94-206">Clone hello fork on their local machine</span></span>
> 3. <span data-ttu-id="72e94-207">他們自己的 dev 分支和環境的相同命令 toocreate 執行 hello。</span><span class="sxs-lookup"><span data-stu-id="72e94-207">Run hello same commands toocreate their own dev branch and environment.</span></span>
> 
> 

<span data-ttu-id="72e94-208">完成之後，GitHub 分岔應該會有三個分支：</span><span class="sxs-lookup"><span data-stu-id="72e94-208">When you’re done, your GitHub fork should have three branches:</span></span>

![](./media/app-service-agile-software-development/test-1-github-view.png)

<span data-ttu-id="72e94-209">而三個不同的資源群組中應該會有六個 Web 應用程式 (兩個一組，共三組)：</span><span class="sxs-lookup"><span data-stu-id="72e94-209">And you should have six web apps (three sets of two) in three separate resource groups:</span></span>

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> <span data-ttu-id="72e94-210">ProdandStage.json 指定 hello 實際執行環境 toouse hello**標準**定價層，適用於 hello 實際執行應用程式的延展性。</span><span class="sxs-lookup"><span data-stu-id="72e94-210">ProdandStage.json specifies hello production environment toouse hello **Standard** pricing tier, which is appropriate for scalability of hello production application.</span></span>
> 
> 

## <a name="build-and-test-every-commit"></a><span data-ttu-id="72e94-211">建置和測試每個認可</span><span class="sxs-lookup"><span data-stu-id="72e94-211">Build and test every commit</span></span>
<span data-ttu-id="72e94-212">hello ProdAndStage.json 的範本檔案，稱為已指定 hello 來源控制參數，預設會設定持續發行 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-212">hello template files ProdAndStage.json and Dev.json already specify hello source control parameters, which by default sets up continuous publishing for hello web app.</span></span> <span data-ttu-id="72e94-213">因此，每個認可 toohello GitHub 分支會觸發自動部署 tooAzure，從該分支。</span><span class="sxs-lookup"><span data-stu-id="72e94-213">Therefore, every commit toohello GitHub branch triggers an automatic deployment tooAzure from that branch.</span></span> <span data-ttu-id="72e94-214">我們來看看您設定現在的運作方式。</span><span class="sxs-lookup"><span data-stu-id="72e94-214">Let’s see how your setup works now.</span></span>

1. <span data-ttu-id="72e94-215">請確定您在 hello Dev 分支的 hello 本機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="72e94-215">Make sure that you’re in hello Dev branch of hello local repository.</span></span> <span data-ttu-id="72e94-216">toodo 下列 Git 命令介面中的命令，執行的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-216">toodo this, run hello following command in Git Shell:</span></span>
   
        git checkout Dev
2. <span data-ttu-id="72e94-217">請變更 toohello 應用程式的 UI 層藉由變更 hello 程式碼 toouse [Bootstrap](http://getbootstrap.com/components/)列出。</span><span class="sxs-lookup"><span data-stu-id="72e94-217">Make a change toohello app’s UI layer by changing hello code toouse [Bootstrap](http://getbootstrap.com/components/) lists.</span></span> <span data-ttu-id="72e94-218">開啟 *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml 並進行 hello 反白顯示的變更之後：</span><span class="sxs-lookup"><span data-stu-id="72e94-218">Open *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml and make hello following highlighted change:</span></span>
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > <span data-ttu-id="72e94-219">如果您無法讀取 hello 上述映像：</span><span class="sxs-lookup"><span data-stu-id="72e94-219">If you can't read hello preceding image:</span></span> 
    > 
    > * <span data-ttu-id="72e94-220">在行 18，變更`check-list`太`list-group`。</span><span class="sxs-lookup"><span data-stu-id="72e94-220">In line 18, change `check-list` too`list-group`.</span></span>
    > * <span data-ttu-id="72e94-221">在行 19，變更`class="check-list-item"`太`class="list-group-item"`。</span><span class="sxs-lookup"><span data-stu-id="72e94-221">In line 19, change `class="check-list-item"` too`class="list-group-item"`.</span></span>
    > 
    > 
3. <span data-ttu-id="72e94-222">儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="72e94-222">Save hello change.</span></span> <span data-ttu-id="72e94-223">備份在 Git 命令介面中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-223">Back in Git Shell, run hello following commands:</span></span>
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   <span data-ttu-id="72e94-224">這些 git 命令如下太"正在檢查您的程式碼 」 中的另一個原始檔控制系統，例如 TFS。</span><span class="sxs-lookup"><span data-stu-id="72e94-224">These git commands are similar too"checking in your code" in another source control system like TFS.</span></span> <span data-ttu-id="72e94-225">當您執行`git push`，觸發程序的自動程式碼推入 tooAzure，哪些然後重建 hello hello 開發環境中的應用程式 tooreflect hello 變更 hello 新認可。</span><span class="sxs-lookup"><span data-stu-id="72e94-225">When you run `git push`, hello new commit triggers an automatic code push tooAzure, which then rebuilds hello application tooreflect hello change in hello dev environment.</span></span>
4. <span data-ttu-id="72e94-226">tooverify 發生此程式碼推入 tooyour 開發環境中，移至 tooyour 開發人員環境的 web 應用程式頁面，並查看 hello**部署**組件。</span><span class="sxs-lookup"><span data-stu-id="72e94-226">tooverify that this code push tooyour dev environment has occurred, go tooyour dev environment’s web app page and look at hello **Deployment** part.</span></span> <span data-ttu-id="72e94-227">您應該能夠 toosee 您最新的認可訊息有。</span><span class="sxs-lookup"><span data-stu-id="72e94-227">You should be able toosee your latest commit message there.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. <span data-ttu-id="72e94-228">從該處，請按一下**瀏覽**toosee hello hello Azure 中的即時應用程式中的新變更。</span><span class="sxs-lookup"><span data-stu-id="72e94-228">From there, click **Browse** toosee hello new change in hello live application in Azure.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   <span data-ttu-id="72e94-229">它是次要變更 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-229">It's a minor change toohello application.</span></span> <span data-ttu-id="72e94-230">不過，許多新的變更 tooa 複雜的 web 應用程式時間有非預期且非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="72e94-230">However, many times new changes tooa complex web application have unintended and undesirable side effects.</span></span> <span data-ttu-id="72e94-231">要能 tooeasily 測試即時組建中的每個認可可讓您 toocatch 這些問題之前，您的客戶會看到它們。</span><span class="sxs-lookup"><span data-stu-id="72e94-231">Being able tooeasily test every commit in live builds enables you toocatch these issues before your customers see them.</span></span>

<span data-ttu-id="72e94-232">現在，您應該熟悉 hello 實現，身為開發人員在 hello **NewUpdate**專案中，您可以建立，為您自己的開發環境，然後建置每次認可和測試每次建置。</span><span class="sxs-lookup"><span data-stu-id="72e94-232">By now, you should be comfortable with hello realization that, as a developer on hello **NewUpdate** project, you can create a dev environment for yourself, then build every commit and test every build.</span></span>

## <a name="merge-code-into-test-environment"></a><span data-ttu-id="72e94-233">將程式碼合併至測試環境</span><span class="sxs-lookup"><span data-stu-id="72e94-233">Merge code into test environment</span></span>
<span data-ttu-id="72e94-234">當您準備好 toopush 開發人員從程式碼分支向上 tooNewUpdate 分支時，它會是 hello 標準 git 程序：</span><span class="sxs-lookup"><span data-stu-id="72e94-234">When you’re ready toopush your code from Dev branch up tooNewUpdate branch, it’s hello standard git process:</span></span>

1. <span data-ttu-id="72e94-235">合併在 GitHub 中，例如建立其他開發人員所認可的 hello Dev 分支中的任何新的認可 tooNewUpdate。</span><span class="sxs-lookup"><span data-stu-id="72e94-235">Merge any new commits tooNewUpdate into hello Dev branch in GitHub, such as commits created by other developers.</span></span> <span data-ttu-id="72e94-236">GitHub 上的任何新認可觸發程式碼推播和 hello 開發環境中的組建。</span><span class="sxs-lookup"><span data-stu-id="72e94-236">Any new commit on GitHub triggers a code push and build in hello dev environment.</span></span> <span data-ttu-id="72e94-237">您接著可以確定 Dev 分支中的程式碼仍適用於從 NewUpdate 分支 hello 最新的位元。</span><span class="sxs-lookup"><span data-stu-id="72e94-237">You can then make sure your code in Dev branch still works with hello latest bits from NewUpdate branch.</span></span>
2. <span data-ttu-id="72e94-238">在 GitHub 中，將所有新認可從 Dev 分支合併至 NewUpdate 分支。</span><span class="sxs-lookup"><span data-stu-id="72e94-238">Merge all your new commits from Dev branch into NewUpdate branch on GitHub.</span></span> <span data-ttu-id="72e94-239">這個動作會觸發程式碼推播和 hello 測試環境中的組建。</span><span class="sxs-lookup"><span data-stu-id="72e94-239">This action triggers a code push and build in hello test environment.</span></span> 

<span data-ttu-id="72e94-240">請注意，一次與這些的 git 分支已設定連續部署，因為您不需要任何其他動作，例如執行整合組建的 tootake。</span><span class="sxs-lookup"><span data-stu-id="72e94-240">Note again that because continuous deployment is already set up with these git branches, you don’t need tootake any other action like running integration builds.</span></span> <span data-ttu-id="72e94-241">您只需要使用 git，tooperform 標準原始檔控制實務，Azure 會為您執行所有的 hello 建置處理序。</span><span class="sxs-lookup"><span data-stu-id="72e94-241">You simply need tooperform standard source control practices using git, and Azure performs all hello build processes for you.</span></span>

<span data-ttu-id="72e94-242">現在，讓我們推送您的程式碼太**NewUpdate**分支。</span><span class="sxs-lookup"><span data-stu-id="72e94-242">Now, let’s push your code too**NewUpdate** branch.</span></span> <span data-ttu-id="72e94-243">在 Git 命令介面中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-243">In Git Shell, run hello following commands:</span></span>

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

<span data-ttu-id="72e94-244">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="72e94-244">That’s it!</span></span> 

<span data-ttu-id="72e94-245">移 toohello web 應用程式頁面為您的測試環境 toosee 您新認可 （合併至 NewUpdate 分支） 現在推送 toohello 測試環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-245">Go toohello web app page for your test environment toosee your new commit (merged into NewUpdate branch) now pushed toohello test environment.</span></span> <span data-ttu-id="72e94-246">然後，按一下 **瀏覽**hello 樣式變更的 toosee 現在正在執行即時 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="72e94-246">Then, click **Browse** toosee that hello style change is now running live in Azure.</span></span>

## <a name="deploy-update-tooproduction"></a><span data-ttu-id="72e94-247">部署更新 tooproduction</span><span class="sxs-lookup"><span data-stu-id="72e94-247">Deploy update tooproduction</span></span>
<span data-ttu-id="72e94-248">將程式碼 toohello 推入暫存和實際執行環境應該感覺受到總公司什麼您已完成推送程式碼 toohello 測試環境時沒有任何差異。</span><span class="sxs-lookup"><span data-stu-id="72e94-248">Pushing code toohello staging and production environment should feel no different than what you’ve already done when you pushed code toohello test environment.</span></span> <span data-ttu-id="72e94-249">真的就是這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="72e94-249">It's really that simple.</span></span> 

<span data-ttu-id="72e94-250">在 Git 命令介面中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-250">In Git Shell, run hello following commands:</span></span>

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

<span data-ttu-id="72e94-251">請記住，根據 ProdandStage.json 設定 hello 預備和生產環境的 hello 方式、 新的程式碼都會被推送 toohello**暫存**位置，而且那里正在執行。</span><span class="sxs-lookup"><span data-stu-id="72e94-251">Remember that based on hello way hello staging and production environment is set up in ProdandStage.json, your new code is pushed toohello **Staging** slot and is running there.</span></span> <span data-ttu-id="72e94-252">因此如果您瀏覽 toohello 預備位置的 URL，您會看到那里執行 hello 新程式碼。</span><span class="sxs-lookup"><span data-stu-id="72e94-252">So if you navigate toohello staging slot’s URL, you see hello new code running there.</span></span> <span data-ttu-id="72e94-253">toodo 遵循 Git 命令介面中的 cmdlet，執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="72e94-253">toodo this, run hello following cmdlet in Git Shell.</span></span>

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

<span data-ttu-id="72e94-254">現在，我們已經確認 hello 暫存位置中的 hello 更新之後，hello 僅保留 toodo 是 tooswap 和它到實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="72e94-254">And now, after you’ve verified hello update in hello staging slot, hello only thing left toodo is tooswap it into production.</span></span> <span data-ttu-id="72e94-255">在 Git 殼層，只執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="72e94-255">In Git Shell, just run hello following commands:</span></span>

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

<span data-ttu-id="72e94-256">恭喜！</span><span class="sxs-lookup"><span data-stu-id="72e94-256">Congratulations!</span></span> <span data-ttu-id="72e94-257">您已成功發行新更新 tooyour 生產 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-257">You’ve successfully published a new update tooyour production web application.</span></span> <span data-ttu-id="72e94-258">不僅如此，完成的方式也只是輕鬆地建立開發和測試環境，以及建置和測試每個認可。</span><span class="sxs-lookup"><span data-stu-id="72e94-258">What’s more is that did it by easily creating dev and test environments, and building and testing every commit.</span></span> <span data-ttu-id="72e94-259">這些是敏捷式軟體開發的重要建置組塊。</span><span class="sxs-lookup"><span data-stu-id="72e94-259">These are crucial building blocks for agile software development.</span></span>

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a><span data-ttu-id="72e94-260">刪除開發和測試環境</span><span class="sxs-lookup"><span data-stu-id="72e94-260">Delete dev and test environments</span></span>
<span data-ttu-id="72e94-261">因為您刻意架構您的開發人員和測試環境 toobe 各自獨立的資源群組，很容易 toodelete 它們。</span><span class="sxs-lookup"><span data-stu-id="72e94-261">Because you have purposely architected your dev and test environments toobe self-contained resource groups, it is easy toodelete them.</span></span> <span data-ttu-id="72e94-262">toodelete hello 本教學課程，hello GitHub 分支和 Azure 的成品，您建立的項目只會執行下列命令在 Git 介面中的 hello:</span><span class="sxs-lookup"><span data-stu-id="72e94-262">toodelete hello ones you created in this tutorial, both hello GitHub branches and Azure artifacts, just run hello following commands in Git Shell:</span></span>

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a><span data-ttu-id="72e94-263">摘要</span><span class="sxs-lookup"><span data-stu-id="72e94-263">Summary</span></span>
<span data-ttu-id="72e94-264">敏捷式軟體開發是必備的許多公司想 tooadopt Azure 做為其應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="72e94-264">Agile software development is a must-have for many companies who want tooadopt Azure as their application platform.</span></span> <span data-ttu-id="72e94-265">在本教學課程中，您已經學會如何 toocreate 及撤除下確切的複本或附近的複本 hello 生產環境使用方便，甚至針對複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72e94-265">In this tutorial, you have learned how toocreate and tear down exact replicas or near replicas of hello production environment with ease, even for complex applications.</span></span> <span data-ttu-id="72e94-266">您也學會如何 tooleverage 這個能力 toocreate 開發程序可建立及測試在 Azure 中的每個單一認可。</span><span class="sxs-lookup"><span data-stu-id="72e94-266">You have also learned how tooleverage this ability toocreate a development process that can build and test every single commit in Azure.</span></span> <span data-ttu-id="72e94-267">本教學課程希望示範了如何最適合使用 Azure App Service 與 Azure 資源管理員一起 toocreate 皆代表 tooagile 方法 DevOps 方案。</span><span class="sxs-lookup"><span data-stu-id="72e94-267">This tutorial has hopefully shown you how you can best use Azure App Service and Azure Resource Manager together toocreate a DevOps solution that caters tooagile methodologies.</span></span> <span data-ttu-id="72e94-268">接下來，您可以透過執行進階 DevOps 技術 (例如 [在生產環境中測試](app-service-web-test-in-production-get-start.md))，建置此案例。</span><span class="sxs-lookup"><span data-stu-id="72e94-268">Next, you can build on this scenario by performing advanced DevOps techniques such as [testing in production](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="72e94-269">如需生產過程中測試的常見案例，請參閱 [Azure App Service 中的快速部署 (beta 測試)](app-service-web-test-in-production-controlled-test-flight.md)。</span><span class="sxs-lookup"><span data-stu-id="72e94-269">For a common testing-in-production scenario, see [Flighting deployment (beta testing) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).</span></span>

## <a name="more-resources"></a><span data-ttu-id="72e94-270">其他資源</span><span class="sxs-lookup"><span data-stu-id="72e94-270">More resources</span></span>
* [<span data-ttu-id="72e94-271">透過可預測方式在 Azure 中部署複雜應用程式</span><span class="sxs-lookup"><span data-stu-id="72e94-271">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="72e94-272">敏捷式開發作法：現代化開發週期的秘訣和訣竅</span><span class="sxs-lookup"><span data-stu-id="72e94-272">Agile Development in Practice: Tips and Tricks for Modernized Development Cycle</span></span>](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [<span data-ttu-id="72e94-273">使用資源管理員範本之 Azure Web 應用程式的進階部署策略</span><span class="sxs-lookup"><span data-stu-id="72e94-273">Advanced deployment strategies for Azure Web Apps using Resource Manager templates</span></span>](http://channel9.msdn.com/Events/Build/2015/2-620)
* [<span data-ttu-id="72e94-274">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="72e94-274">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="72e94-275">JSONLint-hello JSON 驗證程式</span><span class="sxs-lookup"><span data-stu-id="72e94-275">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="72e94-276">GitHub 發行 toosite ARMClient – 設定</span><span class="sxs-lookup"><span data-stu-id="72e94-276">ARMClient – Set up GitHub publishing toosite</span></span>](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [<span data-ttu-id="72e94-277">Git 分支 - 基本分支和合併</span><span class="sxs-lookup"><span data-stu-id="72e94-277">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="72e94-278">David Ebbo 的部落格</span><span class="sxs-lookup"><span data-stu-id="72e94-278">David Ebbo’s Blog</span></span>](http://blog.davidebbo.com/)
* [<span data-ttu-id="72e94-279">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72e94-279">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="72e94-280">Azure 跨平台命令列工具</span><span class="sxs-lookup"><span data-stu-id="72e94-280">Azure Cross-Platform Command-Line Tools</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="72e94-281">在 Azure AD 中建立或編輯使用者</span><span class="sxs-lookup"><span data-stu-id="72e94-281">Create or edit users in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [<span data-ttu-id="72e94-282">專案 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="72e94-282">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)

