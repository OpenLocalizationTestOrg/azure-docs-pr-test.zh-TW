---
title: "aaaFlighting 部署 （beta） 中測試 Azure 應用程式服務"
description: "了解 tooflight 中應用程式或 beta 版的新功能如何測試您的更新在此端對端教學課程。 它整合了 App Service 功能，例如持續性發佈、位置、流量路由及 Application Insights 整合。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="47fb4-104">Azure App Service 中的試驗部署 (beta 測試)</span><span class="sxs-lookup"><span data-stu-id="47fb4-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="47fb4-105">本教學課程示範如何 toodo*測試部署*藉由整合 hello 的各種功能[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)和[Azure Application Insights](/services/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-105">This tutorial shows you how toodo *flighting deployments* by integrating hello various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="47fb4-106">*試驗* 是以有限數量的實際客戶驗證新功能或變更的部署程序，同時也是生產案例中的主要測試。</span><span class="sxs-lookup"><span data-stu-id="47fb4-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="47fb4-107">它是 akin toobeta 測試和有時又稱為 「 受控制的測試途中 」。</span><span class="sxs-lookup"><span data-stu-id="47fb4-107">It is akin toobeta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="47fb4-108">許多具有網站空間的大型企業在執行 [靈活開發](https://en.wikipedia.org/wiki/Agile_software_development)時，都採用此方法及早驗證其應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="47fb4-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="47fb4-109">Azure App Service 可讓您使用連續發行生產環境中的 toointegrate 測試和 Application Insights tooimplement hello 相同 DevOps 案例。</span><span class="sxs-lookup"><span data-stu-id="47fb4-109">Azure App Service enables you toointegrate test in production with continous publishing and Application Insights tooimplement hello same DevOps scenario.</span></span> <span data-ttu-id="47fb4-110">此方法的優點包括：</span><span class="sxs-lookup"><span data-stu-id="47fb4-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="47fb4-111">**取得實際的回饋*之前*更新會發行的 tooproduction** -hello 只有在發行前比您發行時立即取得意見反應好的作法就取得意見反應。</span><span class="sxs-lookup"><span data-stu-id="47fb4-111">**Gain real feedback *before* updates are released tooproduction** - hello only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="47fb4-112">您可以為 hello 產品生命週期的早期測試具有真正的使用者流量與行為的更新。</span><span class="sxs-lookup"><span data-stu-id="47fb4-112">You can test updates with real user traffic and behaviors as early as you desire in hello product life cycle.</span></span>
* <span data-ttu-id="47fb4-113">**增強[持續性測試導向開發 (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - 透過 Application Insights 的持續性整合和工具整合生產環境中的測試，使用者驗證將可在您的產品生命週期內及早進行。</span><span class="sxs-lookup"><span data-stu-id="47fb4-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="47fb4-114">這有助於減少在手動測試執行上投入的時間。</span><span class="sxs-lookup"><span data-stu-id="47fb4-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="47fb4-115">**最佳化測試工作流程**-藉由自動化測試使用連續監視檢測生產環境中的，您可以可能完成 hello 目標的各種測試在單一處理序，例如[整合](https://en.wikipedia.org/wiki/Integration_testing)，[迴歸](https://en.wikipedia.org/wiki/Regression_testing)，[可用性](https://en.wikipedia.org/wiki/Usability_testing)，協助工具、 當地語系化、[效能](https://en.wikipedia.org/wiki/Software_performance_testing)，[安全性](https://en.wikipedia.org/wiki/Security_testing)，和[接受](https://en.wikipedia.org/wiki/Acceptance_testing)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish hello goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="47fb4-116">試驗部署牽涉到的不只是路由傳送即時流量而已。</span><span class="sxs-lookup"><span data-stu-id="47fb4-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="47fb4-117">在這類部署中您想 toogain 深入了解儘快，無論意外的錯誤、 效能降低、 使用者經驗的問題。</span><span class="sxs-lookup"><span data-stu-id="47fb4-117">In such a deployment you want toogain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="47fb4-118">切記，您面對的是實際的客戶。</span><span class="sxs-lookup"><span data-stu-id="47fb4-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="47fb4-119">因此 toodo 它權限，您必須確定您已設定您 flighting 部署 toogather 所有 hello 資料，您需要在順序 toomake 明智的決策下, 一個步驟。</span><span class="sxs-lookup"><span data-stu-id="47fb4-119">So toodo it right, you must make sure that you have set up your flighting deployment toogather all hello data you need in order toomake an informed decision for your next step.</span></span> <span data-ttu-id="47fb4-120">此教學課程會示範如何 toocollect 資料與 Application Insights，但是您可以使用 New Relic 或其他技術適合您的案例。</span><span class="sxs-lookup"><span data-stu-id="47fb4-120">This tutorial shows you how toocollect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="47fb4-121">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="47fb4-121">What you will do</span></span>
<span data-ttu-id="47fb4-122">在此教學課程中，您將學習如何 toobring hello 案例一起 tootest 遵循您在生產環境中的 App Service 應用程式：</span><span class="sxs-lookup"><span data-stu-id="47fb4-122">In this tutorial, you will learn how toobring hello following scenarios together tootest your App Service app in production:</span></span>

* <span data-ttu-id="47fb4-123">[生產流量路由傳送](app-service-web-test-in-production-get-start.md)tooyour beta 應用程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-123">[Route production traffic](app-service-web-test-in-production-get-start.md) tooyour beta app</span></span>
* <span data-ttu-id="47fb4-124">[檢測您的應用程式](../application-insights/app-insights-web-track-usage.md)tooobtain 實用的度量</span><span class="sxs-lookup"><span data-stu-id="47fb4-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) tooobtain useful metrics</span></span>
* <span data-ttu-id="47fb4-125">持續部署 beta 應用程式並追蹤即時應用程式計量</span><span class="sxs-lookup"><span data-stu-id="47fb4-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="47fb4-126">Hello 實際執行應用程式與 hello beta 應用程式 toosee 如何變更程式碼之間的比較度量轉譯 tooresults</span><span class="sxs-lookup"><span data-stu-id="47fb4-126">Compare metrics between hello production app and hello beta app toosee how code changes translate tooresults</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="47fb4-127">必要元件</span><span class="sxs-lookup"><span data-stu-id="47fb4-127">What you will need</span></span>
* <span data-ttu-id="47fb4-128">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="47fb4-128">An Azure account</span></span>
* <span data-ttu-id="47fb4-129">一個 [GitHub](https://github.com/) 帳戶</span><span class="sxs-lookup"><span data-stu-id="47fb4-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="47fb4-130">Visual Studio 2015-您可以下載 hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-130">Visual Studio 2015 - you can download hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="47fb4-131">Git 殼層 (隨[GitHub for Windows](https://windows.github.com/))-這可讓您 toorun hello 這兩個 hello Git 和 PowerShell 命令相同的工作階段</span><span class="sxs-lookup"><span data-stu-id="47fb4-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you toorun both hello Git and PowerShell commands in hello same session</span></span>
* <span data-ttu-id="47fb4-132">最新 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) 位元</span><span class="sxs-lookup"><span data-stu-id="47fb4-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="47fb4-133">Hello 下列的基本了解：</span><span class="sxs-lookup"><span data-stu-id="47fb4-133">Basic understanding of hello following:</span></span>
  * <span data-ttu-id="47fb4-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 範本部署 (請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="47fb4-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="47fb4-135">Git</span><span class="sxs-lookup"><span data-stu-id="47fb4-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="47fb4-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47fb4-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="47fb4-137">您需要 Azure 帳戶 toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="47fb4-137">You need an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="47fb4-138">您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且它們甚至用完之後，您可以保留 hello 帳戶並使用免費的 Azure 服務，例如 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="47fb4-139">您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="47fb4-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="47fb4-140">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="47fb4-140">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="47fb4-141">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="47fb4-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="47fb4-142">設定生產 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="47fb4-143">本教學課程中使用的 hello 指令碼將會自動設定從 GitHub 儲存機制持續發行。</span><span class="sxs-lookup"><span data-stu-id="47fb4-143">hello script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="47fb4-144">這會要求您的 GitHub 認證已儲存在 Azure 中，否則 hello 編寫指令碼部署嘗試 tooconfigure 原始檔控制設定 hello web 應用程式時將會失敗。</span><span class="sxs-lookup"><span data-stu-id="47fb4-144">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment will fail when attempting tooconfigure source control settings for hello web apps.</span></span>
>
> <span data-ttu-id="47fb4-145">toostore 您的 GitHub 認證在 Azure 中建立 web 應用程式在 hello [Azure 入口網站](https://portal.azure.com/)和[設定 GitHub 部署](app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-145">toostore your GitHub credentials in Azure, create a web app in hello [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="47fb4-146">您只需要 toodo 這一次。</span><span class="sxs-lookup"><span data-stu-id="47fb4-146">You only need toodo this once.</span></span>
>
>

<span data-ttu-id="47fb4-147">在典型的 DevOps 案例中，您必須在 Azure 中，即時執行的應用程式而您想 toomake 變更 tooit 透過連續的發佈功能。</span><span class="sxs-lookup"><span data-stu-id="47fb4-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="47fb4-148">在此案例中，您將部署 tooproduction 的範本，您所開發並測試過。</span><span class="sxs-lookup"><span data-stu-id="47fb4-148">In this scenario, you will deploy tooproduction a template that you have developed and tested.</span></span>

1. <span data-ttu-id="47fb4-149">建立您自己的 hello 分岔[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="47fb4-149">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="47fb4-150">如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="47fb4-151">建立分叉之後，即可在瀏覽器中進行查看。</span><span class="sxs-lookup"><span data-stu-id="47fb4-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="47fb4-152">開啟 Git Shell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="47fb4-152">Open a Git Shell session.</span></span> <span data-ttu-id="47fb4-153">若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。</span><span class="sxs-lookup"><span data-stu-id="47fb4-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="47fb4-154">建立您分支的本機複本執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="47fb4-154">Create a local clone of your fork by executing hello following command:</span></span>

     <span data-ttu-id="47fb4-155">git clone https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="47fb4-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="47fb4-156">您的本機複本之後，瀏覽過*&lt;repository_root >*\ARMTemplates，並執行的 hello deploy.ps1 下列指令碼以唯一的尾碼，如所示：</span><span class="sxs-lookup"><span data-stu-id="47fb4-156">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="47fb4-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span><span class="sxs-lookup"><span data-stu-id="47fb4-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="47fb4-158">出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="47fb4-158">When prompted, type in hello desired username and password for database access.</span></span> <span data-ttu-id="47fb4-159">請記住您的資料庫認證，因為您將需要 toospecify 它們一次當更新 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="47fb4-159">Remember your database credentials because you will need toospecify them again when updating hello resource group.</span></span>

   <span data-ttu-id="47fb4-160">您應該會看到 hello 佈建各種不同的 Azure 資源的進度。</span><span class="sxs-lookup"><span data-stu-id="47fb4-160">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="47fb4-161">當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。</span><span class="sxs-lookup"><span data-stu-id="47fb4-161">When deployment completes, hello script will launch hello application in hello browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="47fb4-162">回到 Git Shell 工作階段，並執行：</span><span class="sxs-lookup"><span data-stu-id="47fb4-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="47fb4-163">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="47fb4-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="47fb4-164">Hello 指令碼完成時，請返回 toobrowse toohello 前端的位址 (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello 應用程式在生產環境中執行。</span><span class="sxs-lookup"><span data-stu-id="47fb4-164">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="47fb4-165">登入 hello [Azure 入口網站](https://portal.azure.com/)，看看建立的內容。</span><span class="sxs-lookup"><span data-stu-id="47fb4-165">Log into hello [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="47fb4-166">您應該在 hello 無法 toosee 兩個 web 應用程式相同的資源群組、 具有 hello `Api` hello 名稱中的後置詞。</span><span class="sxs-lookup"><span data-stu-id="47fb4-166">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="47fb4-167">如果您看一下 hello 資源群組檢視，也會看到 hello SQL 資料庫以及伺服器、 hello 應用程式服務方案及 hello 預備位置 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-167">If you look at hello resource group view, you will also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="47fb4-168">瀏覽 hello 不同的資源，並比較它們與 *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 範本中的設定方式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-168">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="47fb4-169">您已設定 hello 生產環境應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-169">You have set up hello production app.</span></span>  <span data-ttu-id="47fb4-170">現在，我們假設您收到意見反應可用性不佳的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-170">Now, let's imagine that you receive feedback that usability is poor for hello app.</span></span> <span data-ttu-id="47fb4-171">讓您決定 tooinvestigate。</span><span class="sxs-lookup"><span data-stu-id="47fb4-171">So you decide tooinvestigate.</span></span> <span data-ttu-id="47fb4-172">您的應用程式 toogive 將 tooinstrument 您的意見反應。</span><span class="sxs-lookup"><span data-stu-id="47fb4-172">You're going tooinstrument your app toogive you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="47fb4-173">調查：檢測用戶端應用程式的監視/計量</span><span class="sxs-lookup"><span data-stu-id="47fb4-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="47fb4-174">在 Visual Studio 中開啟 *&lt;repository_root>*\src\MultiChannelToDo.sln。</span><span class="sxs-lookup"><span data-stu-id="47fb4-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="47fb4-175">以滑鼠右鍵按一下解決方案 > [管理解決方案的 NuGet 套件] > [還原]，以還原所有的 Nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="47fb4-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="47fb4-176">以滑鼠右鍵按一下**MultiChannelToDo.Web** > **加入 Application Insights 遙測** > **設定**> 變更資源群組tooToDoApp*&lt;your_suffix >* > **加入 Application Insights tooProject**。</span><span class="sxs-lookup"><span data-stu-id="47fb4-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
4. <span data-ttu-id="47fb4-177">在 hello Azure 入口網站，開啟 hello 刀鋒視窗中的 hello **MultiChannelToDo.Web** Application Insight 資源。</span><span class="sxs-lookup"><span data-stu-id="47fb4-177">In hello Azure Portal, open hello blade for hello **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="47fb4-178">接著在 hello**應用程式健全狀況**組件中，按一下**學習 toocollect 瀏覽器頁面載入資料的方式**> 複製程式碼。</span><span class="sxs-lookup"><span data-stu-id="47fb4-178">Then in hello **Application health** part, click **Learn how toocollect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="47fb4-179">新增 hello 複製 JS 檢測程式碼太*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml，hello 結尾之前`<heading>`標記。</span><span class="sxs-lookup"><span data-stu-id="47fb4-179">Add hello copied JS instrumentation code too*&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before hello closing `<heading>` tag.</span></span> <span data-ttu-id="47fb4-180">它應該包含 Application Insight 資源的 hello 唯一的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="47fb4-180">It should contain hello unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="47fb4-181">傳送自訂事件滑鼠按鍵的 tooApplication Insights 加入下列程式碼 toohello 底部主體 hello:</span><span class="sxs-lookup"><span data-stu-id="47fb4-181">Send custom events tooApplication Insights for mouse clicks by adding hello following code toohello bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="47fb4-182">這個 JavaScript 程式碼片段會傳送自訂事件 tooApplication Insights 每次使用者按一下 hello web 應用程式中的任何位置。</span><span class="sxs-lookup"><span data-stu-id="47fb4-182">This JavaScript snippet sends a custom event tooApplication Insights every time a user clicks anywhere in hello web app.</span></span>
7. <span data-ttu-id="47fb4-183">在 Git 命令介面中認可並推送您的變更 tooyour 分叉 GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="47fb4-183">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="47fb4-184">接著，等到用戶端 toorefresh 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="47fb4-184">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="47fb4-185">交換部署的 hello 應用程式變更 tooproduction:</span><span class="sxs-lookup"><span data-stu-id="47fb4-185">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="47fb4-186">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="47fb4-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="47fb4-187">瀏覽您所設定的 toohello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="47fb4-187">Browse toohello Application Insights resource that you configured.</span></span> <span data-ttu-id="47fb4-188">按一下 [自訂事件]。</span><span class="sxs-lookup"><span data-stu-id="47fb4-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="47fb4-189">如果您未看見自訂事件的計量，請等候數分鐘，然後按一下 [重新整理] 。</span><span class="sxs-lookup"><span data-stu-id="47fb4-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="47fb4-190">假設您看見如下的圖表：</span><span class="sxs-lookup"><span data-stu-id="47fb4-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="47fb4-191">和其下的 hello 事件方格：</span><span class="sxs-lookup"><span data-stu-id="47fb4-191">And hello event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="47fb4-192">根據 tooyour ToDoApp 應用程式程式碼，hello**按鈕**事件對應 toohello 送出按鈕及 hello**輸入**事件對應 toohello 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="47fb4-192">According tooyour ToDoApp application code, hello **BUTTON** event corresponds toohello submit button, and hello **INPUT** event corresponds toohello textbox.</span></span> <span data-ttu-id="47fb4-193">到目前為止都沒什麼問題。</span><span class="sxs-lookup"><span data-stu-id="47fb4-193">So far, things make sense.</span></span> <span data-ttu-id="47fb4-194">不過，您似乎沒有理想的按和按非常幾下滑鼠數量 hello 待辦項目上 (hello **LI**事件)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-194">However, it looks like there's a good amount of clicks and very few clicks on hello to-do items (hello **LI** events).</span></span>

<span data-ttu-id="47fb4-195">根據此，您表單 UI 是可點選 hello 的哪個部分，而且是因為 hello 資料指標的樣式的文字選取範圍，它將滑鼠指標停留在 hello 清單項目和它的圖示上時，您是有些使用者的假設產生混淆。</span><span class="sxs-lookup"><span data-stu-id="47fb4-195">Based on this, you form your hypothesis that some users are confused which part of hello UI is clickable and it is because hello cursor is styled for text selection when it hovers on hello list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="47fb4-196">您可能會認為此範例是人為的。</span><span class="sxs-lookup"><span data-stu-id="47fb4-196">This might be a contrived example.</span></span> <span data-ttu-id="47fb4-197">不過，您正在進行 toomake 改進 tooyour 應用程式，，然後再執行即時客戶從的 flighting 部署 tooget 可用性的意見反應。</span><span class="sxs-lookup"><span data-stu-id="47fb4-197">Nevertheless, you're going toomake an improvement tooyour app, and then perform a flighting deployment tooget usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="47fb4-198">檢測伺服器應用程式的監視/計量</span><span class="sxs-lookup"><span data-stu-id="47fb4-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="47fb4-199">由於本教學課程中所示範的 hello 案例只處理 hello 用戶端應用程式，這是一側正切函數。</span><span class="sxs-lookup"><span data-stu-id="47fb4-199">This is a tangent since hello scenario demonstrated in this tutorial only deals with hello client app.</span></span> <span data-ttu-id="47fb4-200">不過，為求完整起見，您將設定備份 hello 伺服器端應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-200">However, for completeness you will set up hello server-side app.</span></span>

1. <span data-ttu-id="47fb4-201">以滑鼠右鍵按一下**MultiChannelToDo** > **加入 Application Insights 遙測** > **設定**> 變更資源群組tooToDoApp*&lt;your_suffix >* > **加入 Application Insights tooProject**。</span><span class="sxs-lookup"><span data-stu-id="47fb4-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
2. <span data-ttu-id="47fb4-202">在 Git 命令介面中認可並推送您的變更 tooyour 分叉 GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="47fb4-202">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="47fb4-203">接著，等到用戶端 toorefresh 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="47fb4-203">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="47fb4-204">交換部署的 hello 應用程式變更 tooproduction:</span><span class="sxs-lookup"><span data-stu-id="47fb4-204">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="47fb4-205">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="47fb4-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="47fb4-206">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="47fb4-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a><span data-ttu-id="47fb4-207">調查： 新增特定位置的標記 tooyour 用戶端應用程式計量</span><span class="sxs-lookup"><span data-stu-id="47fb4-207">Investigate: Add slot-specific tags tooyour client app metrics</span></span>
<span data-ttu-id="47fb4-208">在本節中，您將設定 hello 不同的部署位置 toosend 位置特定遙測 toohello 相同的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="47fb4-208">In this section, you will configure hello different deployment slots toosend slot-specific telemetry toohello same Application Insights resource.</span></span> <span data-ttu-id="47fb4-209">如此一來，您可以比較遙測流量從不同位置 （部署環境） tooeasily 之間的資料，請參閱您的應用程式變更 hello 效果。</span><span class="sxs-lookup"><span data-stu-id="47fb4-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) tooeasily see hello effect of your app changes.</span></span> <span data-ttu-id="47fb4-210">在 hello 相同時間，因此您可以繼續 toomonitor 生產應用程式視需要您可以從 hello 其餘部分分離 hello 生產流量。</span><span class="sxs-lookup"><span data-stu-id="47fb4-210">At hello same time, you can separate hello production traffic from hello rest so you can continue toomonitor your production app as needed.</span></span>

<span data-ttu-id="47fb4-211">因為您要收集的資料上的用戶端行為，您將[加入 JavaScript 程式碼的遙測初始設定式 tooyour](../application-insights/app-insights-api-filtering-sampling.md) index.cshtml 中。</span><span class="sxs-lookup"><span data-stu-id="47fb4-211">Since you're gathering data on client behavior, you will [add a telemetry initializer tooyour JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="47fb4-212">如果您想 tootest 伺服器端效能，例如，您也可以執行同樣的伺服器上的程式碼中 (請參閱[應用程式的自訂事件和度量的 Insights API](../application-insights/app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-212">If you want tootest server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="47fb4-213">首先，新增 hello 程式碼字 hello 兩`//`註解以下 hello JavaScript 區塊中的，您會加入 toohello`<heading>`稍早標記。</span><span class="sxs-lookup"><span data-stu-id="47fb4-213">First, add hello code bewteen hello two `//` comments below in hello JavaScript block that you added toohello `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="47fb4-214">這個初始設定式程式碼會造成 hello`appInsights`物件 tooadd hello 呼叫的自訂屬性`Environment`tooevery 片段的遙測資料傳送。</span><span class="sxs-lookup"><span data-stu-id="47fb4-214">This initializer code causes hello `appInsights` object tooadd hello a custom property called `Environment` tooevery piece of telemetry it sends.</span></span>
2. <span data-ttu-id="47fb4-215">接著，在 Azure 中將此自訂屬性新增為 Web 應用程式的 [位置設定](web-sites-staged-publishing.md#AboutConfiguration) 。</span><span class="sxs-lookup"><span data-stu-id="47fb4-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="47fb4-216">toodo 下列命令，您的 Git 殼層工作階段中，執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="47fb4-216">toodo this, run hello following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="47fb4-217">在您的專案中的 hello Web.config 已經定義了 hello`environment`應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="47fb4-217">hello Web.config in your project already defines hello `environment` app setting.</span></span> <span data-ttu-id="47fb4-218">使用此設定，當您測試在本機，hello 應用程式時您的指標會加上`VS Debugger`。</span><span class="sxs-lookup"><span data-stu-id="47fb4-218">With this setting, when you test hello app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="47fb4-219">不過，當您變更 tooAzure，Azure 會尋找並使用 hello`environment`相反地，在 hello web 應用程式的組態中設定的應用程式和您的計量會標記為`Production`。</span><span class="sxs-lookup"><span data-stu-id="47fb4-219">However, when you push your changes tooAzure, Azure will find and use hello `environment` app setting in hello web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="47fb4-220">認可並推送您的程式碼變更 tooyour 分叉 github，並等候使用者 toouse hello 新應用程式 （需要 toorefresh hello 瀏覽器）。</span><span class="sxs-lookup"><span data-stu-id="47fb4-220">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="47fb4-221">因此會佔用大約 15 分鐘的新屬性 tooshow hello Application Insights 中`MultiChannelToDo.Web`資源。</span><span class="sxs-lookup"><span data-stu-id="47fb4-221">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. <span data-ttu-id="47fb4-222">現在，移 toohello**自訂事件**再次刀鋒視窗，然後篩選 hello 度量上`Environment=Production`。</span><span class="sxs-lookup"><span data-stu-id="47fb4-222">Now, go toohello **Custom events** blade again and filter hello metrics on `Environment=Production`.</span></span> <span data-ttu-id="47fb4-223">您現在應該能夠 toosee 中的所有 hello 新自訂事件 hello 生產都位置與此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="47fb4-223">You should now be able toosee all hello new custom events in hello production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="47fb4-224">按一下 hello**我的最愛**按鈕 toosave hello 目前計量瀏覽器設定 toosomething 喜歡**自訂事件： 生產**。</span><span class="sxs-lookup"><span data-stu-id="47fb4-224">Click hello **Favorites** button toosave hello current Metrics Explorer settings toosomething like **Custom events: Production**.</span></span> <span data-ttu-id="47fb4-225">後續您可以在此檢視與部署位置檢視之間輕鬆切換。</span><span class="sxs-lookup"><span data-stu-id="47fb4-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="47fb4-226">若要有更強大的分析能力，請考慮 [將 Application Insights 資源與 Power BI 整合](../application-insights/app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a><span data-ttu-id="47fb4-227">新增特定位置的標記 tooyour 伺服器應用程式計量</span><span class="sxs-lookup"><span data-stu-id="47fb4-227">Add slot-specific tags tooyour server app metrics</span></span>
<span data-ttu-id="47fb4-228">同樣地，為求完整起見，您將設定備份 hello 伺服器端應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-228">Again, for completeness you will set up hello server-side app.</span></span> <span data-ttu-id="47fb4-229">不同於檢測在 JavaScript 中的 hello 用戶端應用程式，hello 伺服器應用程式的特定位置的標記已檢測.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="47fb4-229">Unlike hello client app which is instrumented in JavaScript, slot-specific tags for hello server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="47fb4-230">開啟 *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs。</span><span class="sxs-lookup"><span data-stu-id="47fb4-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="47fb4-231">加入下面 」 之前 hello 左大括號命名空間中的 hello 程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="47fb4-231">Add hello code block below, just before hello closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="47fb4-232">藉由新增 hello 更正 hello 名稱解析錯誤`using`hello 檔案的下方 toohello 開頭的陳述式：</span><span class="sxs-lookup"><span data-stu-id="47fb4-232">Correct hello name resolution errors by adding hello `using` statements below toohello beginning of hello file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="47fb4-233">將程式碼 hello toohello hello 開頭加入`Application_Start()`方法：</span><span class="sxs-lookup"><span data-stu-id="47fb4-233">Add hello code below toohello beginning of hello `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="47fb4-234">認可並推送您的程式碼變更 tooyour 分叉 github，並等候使用者 toouse hello 新應用程式 （需要 toorefresh hello 瀏覽器）。</span><span class="sxs-lookup"><span data-stu-id="47fb4-234">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="47fb4-235">因此會佔用大約 15 分鐘的新屬性 tooshow hello Application Insights 中`MultiChannelToDo`資源。</span><span class="sxs-lookup"><span data-stu-id="47fb4-235">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="47fb4-236">更新：設定您的 Beta 分支：</span><span class="sxs-lookup"><span data-stu-id="47fb4-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="47fb4-237">開啟 *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json] 和 [尋找 hello`appsettings`資源 (搜尋`"name": "appsettings"`)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find hello `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="47fb4-238">資源共有 4 項，分別用於各個位置。</span><span class="sxs-lookup"><span data-stu-id="47fb4-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="47fb4-239">每個`appsettings`資源，新增`"environment": "[parameters('slotName')]"`應用程式設定的 hello toohello 結尾`properties`陣列。</span><span class="sxs-lookup"><span data-stu-id="47fb4-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting toohello end of hello `properties` array.</span></span> <span data-ttu-id="47fb4-240">別忘了以逗點 tooend hello 上的一行。</span><span class="sxs-lookup"><span data-stu-id="47fb4-240">Don't forget tooend hello previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="47fb4-241">您剛剛加入 hello `environment` hello 範本中設定 tooall hello 位置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-241">You have just added hello `environment` app setting tooall hello slots in hello template.</span></span>
3. <span data-ttu-id="47fb4-242">在 hello 同一個檔案中尋找 hello`slotconfignames`資源 (搜尋`"name": "slotconfignames"`)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-242">In hello same file, find hello `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="47fb4-243">資源共有 2 項，分別用於各個應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="47fb4-244">每個`slotconfignames`資源，新增`"environment"`toohello 結尾 hello`appSettingNames`陣列。</span><span class="sxs-lookup"><span data-stu-id="47fb4-244">For each `slotconfignames` resource, add `"environment"` toohello end of hello `appSettingNames` array.</span></span> <span data-ttu-id="47fb4-245">別忘了以逗點 tooend hello 上的一行。</span><span class="sxs-lookup"><span data-stu-id="47fb4-245">Don't forget tooend hello previous line with a comma.</span></span>

    <span data-ttu-id="47fb4-246">您剛才 hello`environment`應用程式設定搖桿 tooits 各自的部署位置的兩個應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-246">You have just made hello `environment` app setting stick tooits respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="47fb4-247">在您的 Git 殼層工作階段中執行的 hello 下列命令以 hello 相同資源群組的後置字元之前使用。</span><span class="sxs-lookup"><span data-stu-id="47fb4-247">In your Git Shell session, run hello following commands with hello same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="47fb4-248">出現提示時，指定與之前 hello 相同 SQL 資料庫認證。</span><span class="sxs-lookup"><span data-stu-id="47fb4-248">When prompted, specify hello same SQL database credentials as before.</span></span> <span data-ttu-id="47fb4-249">然後，當要求 tooupdate hello 資源群組、 型別`Y`，然後`ENTER`。</span><span class="sxs-lookup"><span data-stu-id="47fb4-249">Then, when asked tooupdate hello resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="47fb4-250">一旦 hello 指令碼完成，就會保留您所有 hello 原始的資源群組中的資源，但名為"beta"的新位置中建立以 hello 相同為 hello 「 預備 」 位置中 hello 開頭所建立的組態。</span><span class="sxs-lookup"><span data-stu-id="47fb4-250">Once hello script finishes, all your resources in hello original resource group are retained, but a new slot named "beta" is created in it with hello same configuration as hello "Staging" slot that was created in hello beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="47fb4-251">這個方法來建立不同的部署環境與不同中的 hello 方法[敏捷式軟體開發使用 Azure App Service](app-service-agile-software-development.md)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-251">This method of creating different deployment environments is different from hello method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="47fb4-252">使用此方法時，您會建立具有部署位置的部署環境，而使用該方法時，則建立具有資源群組的部署環境。</span><span class="sxs-lookup"><span data-stu-id="47fb4-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="47fb4-253">管理部署環境與資源群組可讓您 tookeep hello 實際執行環境 off-limits toodevelopers，但並不容易 toodo 測試實際執行環境，您可以輕鬆地使用插槽。</span><span class="sxs-lookup"><span data-stu-id="47fb4-253">Managing deployment environments with resource groups enables you tookeep hello production environment off-limits toodevelopers, but it's not easy toodo testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="47fb4-254">如果需要，也可以藉由下列程式碼建立 alpha 應用程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="47fb4-255">在本教學課程，只要繼續使用 beta 應用程式即可。</span><span class="sxs-lookup"><span data-stu-id="47fb4-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-toohello-beta-app"></a><span data-ttu-id="47fb4-256">更新： Push toohello beta 應用程式更新</span><span class="sxs-lookup"><span data-stu-id="47fb4-256">Update: Push your updates toohello beta app</span></span>
<span data-ttu-id="47fb4-257">備份您想 tooimprove tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-257">Back tooyour app that you want tooimprove.</span></span>

1. <span data-ttu-id="47fb4-258">確定您此時位於 beta 分支中</span><span class="sxs-lookup"><span data-stu-id="47fb4-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="47fb4-259">在 *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml、 尋找 hello`<li>`標記，並新增 hello`style="cursor:pointer"`屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="47fb4-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find hello `<li>` tag and add hello `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="47fb4-260">認可並推送 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="47fb4-260">commit and push tooAzure.</span></span>
4. <span data-ttu-id="47fb4-261">請確認該 hello 變更會立即反映 hello beta 插槽中瀏覽 toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/。</span><span class="sxs-lookup"><span data-stu-id="47fb4-261">Verify that hello change is now reflected in hello beta slot by navigating toohttp://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="47fb4-262">如果您沒有看到 hello 變更尚未重新整理瀏覽器 tooget hello 新 javascript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="47fb4-262">If you don't see hello change yet, refresh your browser tooget hello new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="47fb4-263">現在您擁有 hello beta 插槽中執行您的變更，您就準備好 tooperform flighting 部署。</span><span class="sxs-lookup"><span data-stu-id="47fb4-263">Now that you have your change running in hello beta slot, you are ready tooperform a flighting deployment.</span></span>

## <a name="validate-route-traffic-toohello-beta-app"></a><span data-ttu-id="47fb4-264">驗證： 路由流量 toohello beta 應用程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-264">Validate: Route traffic toohello beta app</span></span>
<span data-ttu-id="47fb4-265">在本節中，您將會路由傳送流量 toohello beta 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-265">In this section, you will route traffic toohello beta app.</span></span> <span data-ttu-id="47fb4-266">為了清楚的示範，您將 tooroute hello 使用者流量 tooit 的重要部分。</span><span class="sxs-lookup"><span data-stu-id="47fb4-266">For sake of clarity of demonstration, you're going tooroute a significant portion of hello user traffic tooit.</span></span> <span data-ttu-id="47fb4-267">事實上，hello tooroute 將取決於您特定的情況下您想要的流量。</span><span class="sxs-lookup"><span data-stu-id="47fb4-267">In reality, hello amount of traffic you want tooroute will depend on your specific situation.</span></span> <span data-ttu-id="47fb4-268">比方說，如果您的網站位於 microsoft.com hello 標尺，您可能需要小於您總流量順序 toogain 有用的資料中的一個百分比。</span><span class="sxs-lookup"><span data-stu-id="47fb4-268">For example, if your site is at hello scale of microsoft.com, then you may need less than one percent of your total traffic in order toogain useful data.</span></span>

1. <span data-ttu-id="47fb4-269">在您的 Git 殼層工作階段，執行下列命令 tooroute hello 一半 hello 生產流量 toohello beta 位置：</span><span class="sxs-lookup"><span data-stu-id="47fb4-269">In your Git Shell session, run hello following commands tooroute half of hello production traffic toohello beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="47fb4-270">hello`ReroutePercentage=50`屬性會指定 50%的 hello 生產流量將會路由的 toohello beta 應用程式的 URL (由 hello`ActionHostName`屬性)。</span><span class="sxs-lookup"><span data-stu-id="47fb4-270">hello `ReroutePercentage=50` property specifies that 50% of hello production traffic will be routed toohello beta app's URL (specified by hello `ActionHostName` property).</span></span>
2. <span data-ttu-id="47fb4-271">現在瀏覽 toohttp://ToDoApp*&lt;your_suffix >*。 名稱是.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="47fb4-271">Now navigate toohttp://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="47fb4-272">50%的 hello 流量現在應該重新導向的 toohello beta 位置。</span><span class="sxs-lookup"><span data-stu-id="47fb4-272">50% of hello traffic should now be redirected toohello beta slot.</span></span>
3. <span data-ttu-id="47fb4-273">在 Application Insights 資源中，篩選環境 hello 度量 ="beta"。</span><span class="sxs-lookup"><span data-stu-id="47fb4-273">In your Application Insights resource, filter hello metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="47fb4-274">如果您為另一個的我的最愛儲存此篩選的檢視，您可以輕鬆地翻轉實際伺服器與 beta 檢視之間的 hello 度量資料總管檢視。</span><span class="sxs-lookup"><span data-stu-id="47fb4-274">If you save this filtered view as another favorite, then you can easily flip hello metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="47fb4-275">在 Application Insights，您會看到類似 toohello 下列假設：</span><span class="sxs-lookup"><span data-stu-id="47fb4-275">Suppose in Application Insights you see something similar toohello following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="47fb4-276">這不只顯示有許多詳細 hello 點選`<li>`標記，但上似乎那里 toobe 的點選劇`<li>`標記。</span><span class="sxs-lookup"><span data-stu-id="47fb4-276">Not only is this showing that there are many more clicks on hello `<li>` tags, but there seems toobe a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="47fb4-277">您接著可以推斷人發現新的 hello`<li>`標記可點選而且現在會清除所有先前已完成任務 hello 應用程式中的。</span><span class="sxs-lookup"><span data-stu-id="47fb4-277">You can then conclude that people have discovered hello new `<li>` tags are clickable and are now clearing all their previously-completed tasks in hello app.</span></span>

<span data-ttu-id="47fb4-278">根據 flighting 部署的 hello 資料，您決定您的新 UI 可供生產環境。</span><span class="sxs-lookup"><span data-stu-id="47fb4-278">Based on hello data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="47fb4-279">實作：將新的程式碼移至生產環境</span><span class="sxs-lookup"><span data-stu-id="47fb4-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="47fb4-280">您要現在準備好 toomove 更新 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="47fb4-280">You're now ready toomove your update tooproduction.</span></span> <span data-ttu-id="47fb4-281">很棒的是，現在您已經知道，您的更新已經過驗證*之前*推入 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="47fb4-281">What's great is that now you know that your update has already been validated *before* it is pushed tooproduction.</span></span> <span data-ttu-id="47fb4-282">因此，現在您可以安心地加以部署。</span><span class="sxs-lookup"><span data-stu-id="47fb4-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="47fb4-283">您進行更新 toohello AngularJS 用戶端應用程式時，才會進行驗證 hello 用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="47fb4-283">Since you made an update toohello AngularJS client app, you only validated hello client-side code.</span></span> <span data-ttu-id="47fb4-284">如果您是 toomake 變更 toohello 後端 Web API 應用程式時，您也可以同樣地，輕鬆地驗證您的變更。</span><span class="sxs-lookup"><span data-stu-id="47fb4-284">If you were toomake changes toohello back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="47fb4-285">在 Git 命令介面中執行下列命令的 hello 移除 hello 流量路由規則：</span><span class="sxs-lookup"><span data-stu-id="47fb4-285">In Git Shell, remove hello traffic routing rule by running hello following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="47fb4-286">執行 hello Git 命令：</span><span class="sxs-lookup"><span data-stu-id="47fb4-286">Run hello Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="47fb4-287">等待幾分鐘，讓 hello 新的程式碼部署 toobe toohello 暫存位置，然後啟動 http://ToDoApp*&lt;your_suffix >*-hello 新更新的 staging.azurewebsites.net tooverify 就緒在 hello 預備環境中位置。</span><span class="sxs-lookup"><span data-stu-id="47fb4-287">Wait for a few minutes for hello new code toobe deployed toohello staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net tooverify that hello new update is warmed up in hello staging slot.</span></span> <span data-ttu-id="47fb4-288">請記住分岔的主要分支都是由該 hello 連結 toohello 暫存位置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="47fb4-288">Remember that hello your fork's master branch is linked toohello staging slot of your app.</span></span>
4. <span data-ttu-id="47fb4-289">現在，交換預備位置到實際執行環境的 hello</span><span class="sxs-lookup"><span data-stu-id="47fb4-289">Now, swap hello staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="47fb4-290">摘要</span><span class="sxs-lookup"><span data-stu-id="47fb4-290">Summary</span></span>
<span data-ttu-id="47fb4-291">Azure App Service 方便 toomedium-小型企業 tootest 其客戶對向應用程式在生產環境中，項目具有大型企業中傳統上完成。</span><span class="sxs-lookup"><span data-stu-id="47fb4-291">Azure App Service makes it easy for small- toomedium-sized businesses tootest their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="47fb4-292">希望本教學課程已提供您 hello 您需要 toobring 一起應用程式服務和 Application Insights toomake 可能測試部署和甚至是其他在實際執行的測試案例，DevOps 世界中的知識。</span><span class="sxs-lookup"><span data-stu-id="47fb4-292">Hopefully, this tutorial has given you hello knowledge you need toobring together App Service and Application Insights toomake possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="47fb4-293">其他資源</span><span class="sxs-lookup"><span data-stu-id="47fb4-293">More resources</span></span>
* [<span data-ttu-id="47fb4-294">敏捷式軟體開發 (Agile Software Development) 與 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="47fb4-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="47fb4-295">針對 Azure App Service 中的 Web 應用程式設定預備環境</span><span class="sxs-lookup"><span data-stu-id="47fb4-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="47fb4-296">透過可預測方式在 Azure 中部署複雜應用程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="47fb4-297">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="47fb4-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="47fb4-298">JSONLint-hello JSON 驗證程式</span><span class="sxs-lookup"><span data-stu-id="47fb4-298">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="47fb4-299">Git 分支 - 基本分支和合併</span><span class="sxs-lookup"><span data-stu-id="47fb4-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="47fb4-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="47fb4-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="47fb4-301">專案 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="47fb4-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
