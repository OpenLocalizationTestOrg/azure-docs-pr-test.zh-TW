---
title: "aaaDeploy 使用 Visual Studio 的 WebJobs"
description: "深入了解如何 toodeploy Azure WebJobs tooAzure App Service Web 應用程式使用 Visual Studio。"
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="21a22-103">使用 Visual Studio 部署 WebJob</span><span class="sxs-lookup"><span data-stu-id="21a22-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="21a22-104">概觀</span><span class="sxs-lookup"><span data-stu-id="21a22-104">Overview</span></span>
<span data-ttu-id="21a22-105">本主題說明如何 toouse Visual Studio toodeploy 主控台應用程式專案中的 tooa web 應用程式[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)為[Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226)。</span><span class="sxs-lookup"><span data-stu-id="21a22-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="21a22-106">如需如何使用 toodeploy WebJobs hello [Azure 入口網站](https://portal.azure.com)，請參閱[以 WebJobs 執行背景工作](web-sites-create-web-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="21a22-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="21a22-107">當 Visual Studio 部署具有 WebJobs 功能的主控台應用程式專案時，它會執行兩個工作：</span><span class="sxs-lookup"><span data-stu-id="21a22-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="21a22-108">複製執行階段檔案 toohello hello web 應用程式中適當的資料夾 (*App_Data/工作/連續*連續 web 工作，如*App_Data/工作/觸發*排程或隨選 Webjob 的)。</span><span class="sxs-lookup"><span data-stu-id="21a22-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="21a22-109">設定[Azure 排程器作業](#scheduler)個是在特定時間排程的 toorun 的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="21a22-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="21a22-110">(無需為連續 WebJobs 執行此動作。)</span><span class="sxs-lookup"><span data-stu-id="21a22-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="21a22-111">啟用 WebJobs 的專案具有下列項目加入的 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="21a22-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="21a22-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="21a22-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="21a22-113">包含部署和排程器設定的 [webjob-publish-settings.json](#publishsettings) 檔案。</span><span class="sxs-lookup"><span data-stu-id="21a22-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![顯示項目會成為 WebJob tooa 主控台應用程式 tooenable 部署的圖表](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="21a22-115">您可以加入這些項目 tooan，現有的主控台應用程式專案，或使用範本 toocreate 新的 Webjob 功能的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="21a22-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="21a22-116">您可以部署專案 webjob 本身，或將其連結 tooa web 專案，讓它自動將部署時部署 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="21a22-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="21a22-117">toolink 專案，Visual Studio 包含 hello hello 啟用 WebJobs 的專案名稱[webjobs list.json](#webjobslist) hello web 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="21a22-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![顯示連結 tooweb 專案 WebJob 專案的圖表](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="21a22-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="21a22-119">Prerequisites</span></span>
<span data-ttu-id="21a22-120">當您安裝 hello Azure SDK for.NET 時，可提供 Visual Studio 中使用 WebJobs 部署功能：</span><span class="sxs-lookup"><span data-stu-id="21a22-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="21a22-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="21a22-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="21a22-122"><a id="convert"></a>啟用現有主控台應用程式專案的 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="21a22-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="21a22-123">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="21a22-123">You have two options:</span></span>

* <span data-ttu-id="21a22-124">[透過 Web 專案啟用自動部署](#convertlink)。</span><span class="sxs-lookup"><span data-stu-id="21a22-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="21a22-125">設定現有主控台應用程式專案，以便在您部署 Web 專案時，它會以 WebJob 的方式自動部署。</span><span class="sxs-lookup"><span data-stu-id="21a22-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="21a22-126">當您想 toorun 您在 hello 中的 WebJob，請使用此選項讓您執行 hello 的相同 web 應用程式相關的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21a22-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="21a22-127">[不透過 Web 專案啟用部署](#convertnolink)。</span><span class="sxs-lookup"><span data-stu-id="21a22-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="21a22-128">設定現有的主控台應用程式專案 toodeploy webjob 單獨使用時，與沒有連結 tooa web 專案。</span><span class="sxs-lookup"><span data-stu-id="21a22-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="21a22-129">當您單獨使用時，想 toorun web 應用程式中的 WebJob 與 hello web 應用程式中執行任何 web 應用程式時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="21a22-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="21a22-130">您可能想要 toodo 這在順序 toobe 無法 tooscale WebJob 資源與您的 web 應用程式資源分開。</span><span class="sxs-lookup"><span data-stu-id="21a22-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="21a22-131"><a id="convertlink"></a> 透過 Web 專案啟用自動 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="21a22-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="21a22-132">中的以滑鼠右鍵按一下 hello web 專案**方案總管 中**，然後按一下**新增** > **現有 Azure WebJob 專案**。</span><span class="sxs-lookup"><span data-stu-id="21a22-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Existing Project as Azure WebJob](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="21a22-134">hello[新增 Azure WebJob](#configure)  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="21a22-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21a22-135">在 hello**專案名稱**下拉式清單中，選取 hello 主控台應用程式專案 tooadd webjob。</span><span class="sxs-lookup"><span data-stu-id="21a22-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="21a22-137">完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="21a22-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="21a22-138"><a id="convertnolink"></a> 不透過 Web 專案啟用 WebJobs 部署</span><span class="sxs-lookup"><span data-stu-id="21a22-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="21a22-139">以滑鼠右鍵按一下 hello 主控台應用程式專案中的**方案總管 中**，然後按一下**發行為 Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="21a22-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="21a22-141">hello[新增 Azure WebJob](#configure)  對話方塊隨即出現，並選取 hello 中的 hello 專案**專案名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="21a22-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="21a22-142">完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="21a22-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="21a22-143">hello**發行 Web**精靈 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="21a22-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="21a22-144">如果您不立即想 toopublish，關閉 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="21a22-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="21a22-145">您輸入的 hello 設定會儲存的當您想太[部署 hello 專案](#deploy)。</span><span class="sxs-lookup"><span data-stu-id="21a22-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="21a22-146"><a id="create"></a>建立具有 WebJobs 功能的新專案</span><span class="sxs-lookup"><span data-stu-id="21a22-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="21a22-147">toocreate 新的 Webjob 啟用專案，您可以使用 hello 主控台應用程式專案範本，並啟用 WebJobs 部署中所述[hello 上一節](#convert)。</span><span class="sxs-lookup"><span data-stu-id="21a22-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="21a22-148">或者，您可以使用 hello WebJobs 新專案範本：</span><span class="sxs-lookup"><span data-stu-id="21a22-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="21a22-149">使用獨立的 WebJob hello WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="21a22-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="21a22-150">建立專案並且設定該 toodeploy 本身 webjob，與沒有連結 tooa web 專案。</span><span class="sxs-lookup"><span data-stu-id="21a22-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="21a22-151">當您單獨使用時，想 toorun web 應用程式中的 WebJob 與 hello web 應用程式中執行任何 web 應用程式時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="21a22-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="21a22-152">您可能想要 toodo 這在順序 toobe 無法 tooscale WebJob 資源與您的 web 應用程式資源分開。</span><span class="sxs-lookup"><span data-stu-id="21a22-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="21a22-153">WebJob 連結的 tooa web 專案使用 hello WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="21a22-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="21a22-154">建立專案，會自動設定的 toodeploy webjob hello 部署相同方案中的 web 專案時。</span><span class="sxs-lookup"><span data-stu-id="21a22-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="21a22-155">當您想 toorun 您在 hello 中的 WebJob，請使用此選項讓您執行 hello 的相同 web 應用程式相關的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21a22-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="21a22-156">hello WebJobs 新專案範本自動安裝 NuGet 封裝，並包含程式碼中的*Program.cs* hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs)。</span><span class="sxs-lookup"><span data-stu-id="21a22-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="21a22-157">如果您不想 toouse hello WebJobs SDK，移除或變更 hello`host.RunAndBlock`陳述式中的*Program.cs*。</span><span class="sxs-lookup"><span data-stu-id="21a22-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="21a22-158"><a id="createnolink"></a>使用獨立的 WebJob hello WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="21a22-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="21a22-159">按一下**檔案** > **新專案**，然後在 hello**新專案**對話方塊中，按一下**雲端** >  **Azure WebJob (.NET Framework)**。</span><span class="sxs-lookup"><span data-stu-id="21a22-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![顯示 WebJob 範本的 [新增專案] 對話方塊](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="21a22-161">請依照稍早所示的 hello 指示太[進行獨立的 Webjob 專案 hello 主控台應用程式專案](#convertnolink)。</span><span class="sxs-lookup"><span data-stu-id="21a22-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="21a22-162"><a id="createlink"></a>WebJob 連結的 tooa web 專案使用 hello WebJobs 新專案範本</span><span class="sxs-lookup"><span data-stu-id="21a22-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="21a22-163">中的以滑鼠右鍵按一下 hello web 專案**方案總管 中**，然後按一下**新增** > **新增 Azure WebJob 專案**。</span><span class="sxs-lookup"><span data-stu-id="21a22-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="21a22-165">hello[新增 Azure WebJob](#configure)  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="21a22-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21a22-166">完整的 hello[新增 Azure WebJob](#configure)對話方塊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="21a22-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="21a22-167"><a id="configure"></a>hello 新增 Azure WebJob 對話方塊</span><span class="sxs-lookup"><span data-stu-id="21a22-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="21a22-168">hello**新增 Azure WebJob**對話方塊可讓您輸入 hello web 工作名稱和執行您 web 工作的模式設定。</span><span class="sxs-lookup"><span data-stu-id="21a22-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![[加入 Azure WebJob] 對話方塊](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="21a22-170">在這個對話方塊中的 hello 欄位對應上 hello toofields**新工作**hello Azure 入口網站 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="21a22-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="21a22-171">如需詳細資訊，請參閱[使用 WebJobs 執行背景工作](web-sites-create-web-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="21a22-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="21a22-172">如需命令列部署的詳細資訊，請參閱[啟用 Azure WebJobs 的命令列或連續傳遞](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)。</span><span class="sxs-lookup"><span data-stu-id="21a22-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="21a22-173">如果您部署 WebJob，然後決定您想 toochange hello 類型 WebJob 和重新部署時，您將需要 toodelete hello webjobs 發佈 settings.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="21a22-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="21a22-174">這會讓 Visual Studio 顯示 hello 同樣地，發行選項，因此您可以變更 WebJob hello 型別。</span><span class="sxs-lookup"><span data-stu-id="21a22-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="21a22-175">如果您部署 WebJob 和在之後變更 hello 執行的模式中從連續 toonon 連續或反之亦然，Visual Studio 會建立新的 WebJob 在 Azure 中重新部署時。</span><span class="sxs-lookup"><span data-stu-id="21a22-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="21a22-176">如果您變更排程的其他設定，但保留執行模式 hello 相同，或已排程和隨選之間切換，Visual Studio 更新 hello 現有的工作而非建立新的連線。</span><span class="sxs-lookup"><span data-stu-id="21a22-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="21a22-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="21a22-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="21a22-178">當您設定部署 WebJobs 的主控台應用程式時，Visual Studio 會安裝 hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet 封裝和排程資訊中的存放區*webjob 發行 settings.json* hello 專案檔案中的*屬性*hello Webjob 專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="21a22-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="21a22-179">以下是該檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="21a22-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="21a22-180">您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="21a22-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21a22-181">hello 檔案結構描述儲存在[http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json)而且可以那里檢視。</span><span class="sxs-lookup"><span data-stu-id="21a22-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="21a22-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="21a22-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="21a22-183">當您連結 WebJobs 啟用專案 tooa web 專案時，Visual Studio 會儲存 hello Webjob 專案的 hello 名稱*webjobs list.json* hello web 專案的檔案中*屬性*資料夾。</span><span class="sxs-lookup"><span data-stu-id="21a22-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="21a22-184">hello 清單可能包含多個 WebJobs 的專案，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="21a22-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="21a22-185">您可以編輯此檔案目錄，而 Visual Studio 會提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="21a22-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21a22-186">hello 檔案結構描述儲存在[http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json)而且可以那里檢視。</span><span class="sxs-lookup"><span data-stu-id="21a22-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="21a22-187"><a id="deploy"></a>部署 WebJobs 專案</span><span class="sxs-lookup"><span data-stu-id="21a22-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="21a22-188">您已連結 tooa web 專案的 Webjob 專案會自動部署與 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="21a22-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="21a22-189">Web 專案部署的相關資訊，請參閱[如何 toodeploy tooWeb 應用程式](web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="21a22-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="21a22-190">toodeploy Webjob 專案本身，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**按一下**發行為 Azure WebJob...**.</span><span class="sxs-lookup"><span data-stu-id="21a22-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![發行為 Azure WebJob](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="21a22-192">獨立的 web 工作，如 hello 相同**發行 Web**使用 web 專案會顯示，但使用較少的設定可用 toochange 精靈。</span><span class="sxs-lookup"><span data-stu-id="21a22-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="21a22-193"><a id="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="21a22-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="21a22-194">本文說明如何使用 Visual Studio toodeploy WebJobs。</span><span class="sxs-lookup"><span data-stu-id="21a22-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="21a22-195">如需有關如何 toodeploy Azure Webjob，請參閱[Azure WebJobs-資源-建議部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying)。</span><span class="sxs-lookup"><span data-stu-id="21a22-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

