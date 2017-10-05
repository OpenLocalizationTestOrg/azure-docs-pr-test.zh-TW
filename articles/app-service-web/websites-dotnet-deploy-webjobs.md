---
title: "使用 Visual Studio 部署 WebJob"
description: "了解如何使用 Visual Studio，將 Azure WebJob 部署至 Azure App Service Web Apps。"
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="6c9ec-103">使用 Visual Studio 部署 WebJob</span><span class="sxs-lookup"><span data-stu-id="6c9ec-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="6c9ec-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6c9ec-104">Overview</span></span>
<span data-ttu-id="6c9ec-105">本主題說明如何使用 Visual Studio 將主控台應用程式專案部署為 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中之 Web 應用程式的 [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="6c9ec-106">如需如何使用 [Azure 入口網站](https://portal.azure.com)部署 WebJob 的相關資訊，請參閱[使用 WebJob 執行背景工作](web-sites-create-web-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="6c9ec-107">當 Visual Studio 部署具有 WebJobs 功能的主控台應用程式專案時，它會執行兩個工作：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="6c9ec-108">將執行階段檔案複製到 Web 應用程式中的適當資料夾 (若是連續 WebJobs，則是 *App_Data/jobs/continuous*，若是排程和隨選 WebJobs，則是 *App_Data/jobs/triggered*)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="6c9ec-109">為已排定在特定時間執行的 WebJobs 設定 [Azure 排程器工作](#scheduler)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="6c9ec-110">(無需為連續 WebJobs 執行此動作。)</span><span class="sxs-lookup"><span data-stu-id="6c9ec-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="6c9ec-111">具有 WebJobs 功能的專案會新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="6c9ec-112">[Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="6c9ec-113">包含部署和排程器設定的 [webjob-publish-settings.json](#publishsettings) 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="6c9ec-115">您可以將這些項目新增至現有的主控台應用程式專案，或使用範本建立具有 WebJobs 功能的新主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="6c9ec-116">以 WebJob 的方式自我部署專案，或將專案連結到 Web 專案，因此每當您要部署 Web 專案時，專案便會自動部署。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="6c9ec-117">若要連結專案，Visual Studio 會在 Web 專案的 [webjobs-list.json](#webjobslist) 檔案中加上具有 WebJobs 功能的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram showing WebJob project linking to web project](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="6c9ec-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c9ec-119">Prerequisites</span></span>
<span data-ttu-id="6c9ec-120">安裝 Azure SDK for .NET 時，您便可在 Visual Studio 中使用 WebJobs 部署功能：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="6c9ec-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="6c9ec-122"><a id="convert"></a>啟用現有主控台應用程式專案的 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="6c9ec-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="6c9ec-123">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-123">You have two options:</span></span>

* <span data-ttu-id="6c9ec-124">[透過 Web 專案啟用自動部署](#convertlink)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="6c9ec-125">設定現有主控台應用程式專案，以便在您部署 Web 專案時，它會以 WebJob 的方式自動部署。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="6c9ec-126">當您要在與執行相關 Web 應用程式相同的 Web 應用程式中執行 WebJob 時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="6c9ec-127">[不透過 Web 專案啟用部署](#convertnolink)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="6c9ec-128">設定現有主控台應用程式專案以 WebJob 的方式自我部署，且不具 Web 專案的連結。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="6c9ec-129">當您要在 Web 應用程式中讓應用程式自行執行 WebJob，且 Web 應用程式中沒有正在執行的 Web 應用程式時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="6c9ec-130">為了調整不受 Web 應用程式資源影響的 WebJob 資源，您可能會想執行此動作。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="6c9ec-131"><a id="convertlink"></a> 透過 Web 專案啟用自動 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="6c9ec-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="6c9ec-132">以滑鼠右鍵按一下 [方案總管] 中的 Web 專案，然後依序按一下 [新增] > [Existing Project as Azure WebJob]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="6c9ec-134">[[Add Azure WebJob]](#configure) 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6c9ec-135">在 [專案名稱]  下拉式清單中，選取要新增為 WebJob 的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="6c9ec-137">完成 [[Add Azure WebJob]](#configure) 對話方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="6c9ec-138"><a id="convertnolink"></a> 不透過 Web 專案啟用 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="6c9ec-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="6c9ec-139">以滑鼠右鍵按一下 [方案總管] 中的主控台應用程式專案，然後按一下 [發行為 Azure WebJob]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="6c9ec-141">[[加入 Azure WebJob]](#configure) 對話方塊隨即出現，而且 [專案名稱] 方塊中已選取此專案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="6c9ec-142">完成 [[加入 Azure WebJob]](#configure) 對話方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="6c9ec-143">此時會出現 [發行 Web] 精靈。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="6c9ec-144">如果您不打算立即發行，請關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="6c9ec-145">您所輸入的設定會被儲存下來，以供[部署專案](#deploy)時使用。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="6c9ec-146"><a id="create"></a>建立具有 WebJobs 功能的新專案</span><span class="sxs-lookup"><span data-stu-id="6c9ec-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="6c9ec-147">若要建立具有 WebJobs 功能的新專案，您可以使用主控台應用程式專案範本，並如 [上一節](#convert)中所述來啟用 WebJobs 部署。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="6c9ec-148">另一種方式是，您可以使用 WebJobs 新專案範本：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="6c9ec-149">在獨立的 WebJob 中使用 WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="6c9ec-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="6c9ec-150">建立專案，並將專案設定為以 WebJob 的方式自我部署，且不具 Web 專案的連結。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="6c9ec-151">當您要在 Web 應用程式中讓應用程式自行執行 WebJob，且 Web 應用程式中沒有正在執行的 Web 應用程式時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="6c9ec-152">為了調整不受 Web 應用程式資源影響的 WebJob 資源，您可能會想執行此動作。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="6c9ec-153">在連結至 Web 專案的 WebJob 中使用 WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="6c9ec-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="6c9ec-154">建立專案，並設定在針對位於相同解決方案中的 Web 專案進行部署時，會自動以 WebJob 的方式部署此專案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="6c9ec-155">當您要在與執行相關 Web 應用程式相同的 Web 應用程式中執行 WebJob 時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="6c9ec-156">WebJobs 新專案範本自動安裝 NuGet 套件，並包括適用於 *WebJobs SDK* 的 [Program.cs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="6c9ec-157">如果您不想使用 WebJobs SDK，請移除或變更 *Program.cs* 中的 `host.RunAndBlock` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="6c9ec-158"><a id="createnolink"></a> 在獨立的 WebJob 中使用 WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="6c9ec-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="6c9ec-159">依序按一下 [檔案] > [新增專案]，然後在 [新增專案] 對話方塊中，依序按一下 [雲端] > [Azure WebJob (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![顯示 WebJob 範本的 [新增專案] 對話方塊](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="6c9ec-161">請依照稍早所示的指示，[將主控台應用程式專案設定成獨立的 WebJobs 專案](#convertnolink)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="6c9ec-162"><a id="createlink"></a> 在連結至 Web 專案的 WebJob 中使用 WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="6c9ec-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="6c9ec-163">以滑鼠右鍵按一下 [方案總管] 中的 Web 專案，然後依序按一下 [新增] > [New Azure WebJob Project]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="6c9ec-165">[[Add Azure WebJob]](#configure) 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6c9ec-166">完成 [[Add Azure WebJob]](#configure) 對話方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="6c9ec-167"><a id="configure"></a>[新增 Azure WebJob] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="6c9ec-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="6c9ec-168">[加入 Azure WebJob] 對話方塊可讓您輸入 WebJob 名稱和 WebJob 的執行模式設定。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![[加入 Azure WebJob] 對話方塊](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="6c9ec-170">此對話方塊中的欄位會對應至 Azure 入口網站中 [新增工作]  對話方塊上的欄位。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="6c9ec-171">如需詳細資訊，請參閱[使用 WebJobs 執行背景工作](web-sites-create-web-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6c9ec-172">如需命令列部署的詳細資訊，請參閱[啟用 Azure WebJobs 的命令列或連續傳遞](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="6c9ec-173">如果您部署了 WebJob，但之後決定變更 WebJob 的類型並重新部署，就必須刪除 webjobs-publish-settings.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="6c9ec-174">這樣會讓 Visual Studio 再次顯示發佈選項，您才能夠變更 WebJob 的類型。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="6c9ec-175">如果部署 WebJob，並在稍後將執行模式從連續變更為非連續 (或相反情形)，則在您重新部署時，Visual Studio 會在 Azure 中建立新的 WebJob。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="6c9ec-176">如果您變更其他排程設定但保持執行模式不變，或在排程和隨選模式之間切換，則 Visual Studio 會更新現有的工作，而非建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="6c9ec-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="6c9ec-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="6c9ec-178">設定 WebJobs 部署的主控台應用程式時，Visual Studio 會安裝 [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝，並將排程資訊儲存在 WebJobs 專案中專案 *Properties* 資料夾的 *webjob-publish-settings.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="6c9ec-179">以下是該檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="6c9ec-180">您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6c9ec-181">檔案結構描述會儲存在 [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) ，您可以在該處進行檢視。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="6c9ec-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="6c9ec-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="6c9ec-183">當您將具有 WebJobs 功能的專案連結到 Web 專案時，Visual Studio 會將 WebJobs 專案的名稱儲存在 Web 專案中 *Properties* 資料夾的 *webjobs-list.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="6c9ec-184">此清單可能包含多個 WebJobs 專案，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6c9ec-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="6c9ec-185">您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6c9ec-186">檔案結構描述會儲存在 [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) ，您可以在該處進行檢視。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="6c9ec-187"><a id="deploy"></a>部署 WebJobs 專案</span><span class="sxs-lookup"><span data-stu-id="6c9ec-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="6c9ec-188">已連結到 Web 專案的 WebJobs 專案會透過 Web 專案自動部署。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="6c9ec-189">如需 Web 專案部署的相關資訊，請參閱 [如何部署至 Web 應用程式](web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="6c9ec-190">若要自我部署 WebJobs 專案，請以滑鼠右鍵按一下 [方案總管] 中的專案，然後按一下 [發行為 Azure WebJob]。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="6c9ec-192">若是獨立的 WebJob，則 Web 專案所使用的相同 [發行 Web]  精靈隨即出現，但其中幾個設定可以變更。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="6c9ec-193"><a id="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c9ec-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="6c9ec-194">本文說明如何使用 Visual Studio 部署 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="6c9ec-195">如需如何部署 Azure WebJobs 的詳細資訊，請參閱 [Azure WebJobs - 建議的資源 - 部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)。</span><span class="sxs-lookup"><span data-stu-id="6c9ec-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

