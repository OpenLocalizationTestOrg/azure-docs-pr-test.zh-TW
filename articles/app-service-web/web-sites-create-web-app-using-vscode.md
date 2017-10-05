---
title: "在 Visual Studio Code 中建立 ASP.NET Core Web 應用程式"
description: "本教學課程說明如何使用 Visual Studio Code 建立 ASP.NET Core Web 應用程式。"
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="17b4b-103">在 Visual Studio Code 中建立 ASP.NET Core Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17b4b-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="17b4b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="17b4b-104">Overview</span></span>
<span data-ttu-id="17b4b-105">本教學課程示範如何使用 [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) 建立 ASP.NET Core Web 應用程式，並將其部署到 [Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="17b4b-106">雖然這篇文章主要針對 Web Apps，但也適用於 API Apps 和 Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="17b4b-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="17b4b-107">ASP.NET Core 是大幅重新設計的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="17b4b-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="17b4b-108">ASP.NET Core 是新的開放原始碼和跨平台架構，用於使用 .NET 建置新代雲端式 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="17b4b-109">如需詳細資訊，請參閱 [ASP.NET Core 簡介](http://docs.asp.net/latest/conceptual-overview/aspnet.html)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="17b4b-110">如需有關 Azure App Service Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="17b4b-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="17b4b-111">Prerequisites</span></span>
* <span data-ttu-id="17b4b-112">安裝 [VS Code](http://code.visualstudio.com/Docs/setup)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="17b4b-113">安裝 Git - 您可以從下列位置安裝它：[Chocolatey](https://chocolatey.org/packages/git) 或 [git-scm.com](http://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="17b4b-114">如果您不熟悉 Git，請選擇 [git-scm.com](http://git-scm.com/downloads)，然後選取 [從 Windows 命令提示字元使用 Git] 選項。</span><span class="sxs-lookup"><span data-stu-id="17b4b-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="17b4b-115">一旦您安裝 Git，也需要設定 Git 使用者名稱和電子郵件，因為稍後教學課程將需要用到 (從 VS Code 執行認可時)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="17b4b-116">安裝 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="17b4b-116">Install ASP.NET Core</span></span>
<span data-ttu-id="17b4b-117">ASP.NET Core 是精簡的 .NET 堆疊，可建置 OS X、Linux 和 Windows 上執行的新式雲端和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="17b4b-118">它已從頭建置，以將最佳化的開發架構提供給已部署至雲端或執行內部部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="17b4b-119">其由額外負荷最低的模組化元件組成，以便您可以在建構解決方案時保留彈性。</span><span class="sxs-lookup"><span data-stu-id="17b4b-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="17b4b-120">本教學課程旨在讓您使用最新開發版本的 ASP.NET Core 開始建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="17b4b-121">下列是 Windows 特有的指示。</span><span class="sxs-lookup"><span data-stu-id="17b4b-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="17b4b-122">如需 OS X、Linux 和 Windows 的安裝指示，請參閱[開始使用 ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="17b4b-123">如需 OS X、Linux 和 Windows 的更詳細安裝指示，請參閱[安裝 ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="17b4b-124">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17b4b-124">Create the web app</span></span>
<span data-ttu-id="17b4b-125">本節說明如何使用 .NET CLI 工具建立新的應用程式 ASP.NET Web 應用程式的結構。</span><span class="sxs-lookup"><span data-stu-id="17b4b-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="17b4b-126">在命令提示字元輸入下列命令，來建立專案資料夾，並建立應用程式的結構。</span><span class="sxs-lookup"><span data-stu-id="17b4b-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 產生器](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="17b4b-128">若要還原必要的 NuGet 套件，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="17b4b-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="17b4b-129">在本機執行 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17b4b-129">Run the web app locally</span></span>
<span data-ttu-id="17b4b-130">既然您已建立 Web 應用程式，並擷取應用程式的所有 NuGet 封裝，就可以在本機執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="17b4b-131">執行應用程式 (`dotnet run` 命令過期時，將會建置應用程式)：</span><span class="sxs-lookup"><span data-stu-id="17b4b-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="17b4b-132">開啟瀏覽器並瀏覽至下列 URL。</span><span class="sxs-lookup"><span data-stu-id="17b4b-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="17b4b-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="17b4b-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="17b4b-134">Web 應用程式的預設頁面將出現，如下所示。</span><span class="sxs-lookup"><span data-stu-id="17b4b-134">The default page of the web app will appear as follows.</span></span>
   
    ![在瀏覽器中的本機 Web 應用程式](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="17b4b-136">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="17b4b-136">Close your browser.</span></span> <span data-ttu-id="17b4b-137">在 [命令視窗] 中，按下 **Ctrl+C** 來關閉應用程式，以及關閉 [命令視窗]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="17b4b-138">在 Azure 入口網站中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17b4b-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="17b4b-139">下列步驟將引導您在 Azure 入口網站中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="17b4b-140">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="17b4b-141">按一下入口網站左上角的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="17b4b-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="17b4b-142">按一下 [Web Apps] > [Web Apps]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-142">Click **Web Apps > Web App**.</span></span>
   
    ![Azure 的新 Web 應用程式](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="17b4b-144">輸入 [名稱] 的值，例如 **SampleWebAppDemo**。</span><span class="sxs-lookup"><span data-stu-id="17b4b-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="17b4b-145">請注意，此名稱必須是唯一的，而且當您嘗試輸入名稱時，入口網站將會強制執行此要求。</span><span class="sxs-lookup"><span data-stu-id="17b4b-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="17b4b-146">因此，如果選取或輸入不同值，您將需要以該值取代每次出現的 **SampleWebAppDemo** ，您會在本教學課程中看到。</span><span class="sxs-lookup"><span data-stu-id="17b4b-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="17b4b-147">選取現有的 **App Service 方案** 或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="17b4b-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="17b4b-148">如果您建立新方案，請選取定價層、位置和其他選項。</span><span class="sxs-lookup"><span data-stu-id="17b4b-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="17b4b-149">如需 App Service 方案的詳細資訊，請參閱文章： [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure 的新 Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="17b4b-151">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="17b4b-151">Click **Create**.</span></span>
   
    ![Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="17b4b-153">啟用新 Web 應用程式的 Git 發佈</span><span class="sxs-lookup"><span data-stu-id="17b4b-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="17b4b-154">Git 是一個您可用來部署 Azure App Service Web 應用程式的分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="17b4b-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="17b4b-155">您將會在本機 Git 儲存機制中儲存您為 Web 應用程式撰寫的程式碼，並藉由發送至遠端儲存機制，將您的程式碼部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="17b4b-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="17b4b-156">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="17b4b-157">按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="17b4b-157">Click **Browse**.</span></span>
3. <span data-ttu-id="17b4b-158">按一下 [Web Apps]  ，檢視與 Azure 訂用帳戶相關聯之 Web 應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="17b4b-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="17b4b-159">選取您已在本教學課程中建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="17b4b-160">在 Web 應用程式刀鋒視窗中，按一下 [設定] > [連續部署]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure Web 應用程式主機](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="17b4b-162">按一下 [選擇來源] > [本機 Git 儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="17b4b-163">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="17b4b-163">Click **OK**.</span></span>
   
    ![Azure 本機 Git 儲存機制](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="17b4b-165">如果您先前尚未設定部署認證以供發佈 Web 應用程式或其他 App Service 應用程式，請立即設定：</span><span class="sxs-lookup"><span data-stu-id="17b4b-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="17b4b-166">按一下 [設定] > [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="17b4b-167">[設定部署認證]  刀鋒視窗會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="17b4b-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="17b4b-168">建立使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="17b4b-168">Create a user name and password.</span></span>  <span data-ttu-id="17b4b-169">稍後設定 Git 時，您將需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="17b4b-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="17b4b-170">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="17b4b-170">Click **Save**.</span></span>
9. <span data-ttu-id="17b4b-171">在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="17b4b-172">做為部署目的地的遠端 Git 儲存機制的 URL，會顯示在 [GIT URL] 下方。</span><span class="sxs-lookup"><span data-stu-id="17b4b-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="17b4b-173">複製 [GIT URL]  值以供教學課程稍後使用。</span><span class="sxs-lookup"><span data-stu-id="17b4b-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="17b4b-175">將您的 Web 應用程式發佈至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="17b4b-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="17b4b-176">在本節中，您將建立本機 Git 儲存機制，並從該儲存機制發送至 Azure，以將 Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="17b4b-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="17b4b-177">在 VS Code 中，選取導覽列左側的 [Git]  選項。</span><span class="sxs-lookup"><span data-stu-id="17b4b-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![VS Code 中的 Git 圖示](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="17b4b-179">選取 [初始化 git 儲存機制]  ，確定您的工作區受到 git 原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="17b4b-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![初始化 Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="17b4b-181">開啟 [命令視窗]，並切換至 Web 應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="17b4b-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="17b4b-182">然後，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="17b4b-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="17b4b-183">此命令可防止涉及 CRLF 行尾結束符號和 LF 行尾結束符號之文字的相關問題。</span><span class="sxs-lookup"><span data-stu-id="17b4b-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="17b4b-184">在 VS Code 中，新增認可訊息，然後按一下 **全部認可** 核取圖示。</span><span class="sxs-lookup"><span data-stu-id="17b4b-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Git 全部認可](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="17b4b-186">Git 完成處理之後，您會看到沒有檔案列在 Git 視窗的 [變更] 之下。</span><span class="sxs-lookup"><span data-stu-id="17b4b-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git 沒有變更](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="17b4b-188">變更回命令提示字元指向您的 Web 應用程式所在目錄的 [命令視窗]。</span><span class="sxs-lookup"><span data-stu-id="17b4b-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="17b4b-189">使用您稍早複製的 Git URL (結尾是 ".git")，建立遠端參考，以便將更新發送至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="17b4b-190">設定讓 Git 將認證儲存在本機，以便將它們自動附加至您從 VS Code 產生的推送命令。</span><span class="sxs-lookup"><span data-stu-id="17b4b-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="17b4b-191">輸入下列命令，將您的變更推播至 Azure。</span><span class="sxs-lookup"><span data-stu-id="17b4b-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="17b4b-192">在對 Azure 進行這項初始推送之後，您便可以從 VS Code 執行所有推送命令。</span><span class="sxs-lookup"><span data-stu-id="17b4b-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="17b4b-193">系統會提示您輸入先前在 Azure 建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="17b4b-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="17b4b-194">**注意：將看不到您的密碼。**</span><span class="sxs-lookup"><span data-stu-id="17b4b-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="17b4b-195">上述命令的輸出結尾會出現部署成功的訊息。</span><span class="sxs-lookup"><span data-stu-id="17b4b-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="17b4b-196">如果您變更應用程式，則可以使用內建 Git 功能在 VS 程式碼中直接重新發佈，方法是依序選取 [全部認可] 選項和 [推送] 選項。</span><span class="sxs-lookup"><span data-stu-id="17b4b-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="17b4b-197">您會發現 [全部認可] 和 [重新整理] 按鈕旁邊之下拉式功能表中可用的 [推送] 選項。</span><span class="sxs-lookup"><span data-stu-id="17b4b-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="17b4b-198">如果您需要與他人對專案進行共同作業，則應該考慮在推送至 Azure 之間推送至 GitHub。</span><span class="sxs-lookup"><span data-stu-id="17b4b-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="17b4b-199">在 Azure 中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="17b4b-199">Run the app in Azure</span></span>
<span data-ttu-id="17b4b-200">既然您已部署 Web 應用程式，讓我們執行裝載於 Azure 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="17b4b-201">這有兩種方式可以完成：</span><span class="sxs-lookup"><span data-stu-id="17b4b-201">This can be done in two ways:</span></span>

* <span data-ttu-id="17b4b-202">開啟瀏覽器並輸入 Web 應用程式的名稱，如下所示。</span><span class="sxs-lookup"><span data-stu-id="17b4b-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="17b4b-203">在 Azure 入口網站中，找出您 Web 應用程式的 Web 應用程式刀鋒視窗，然後按一下 [瀏覽]  來檢視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b4b-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="17b4b-204">預設瀏覽器</span><span class="sxs-lookup"><span data-stu-id="17b4b-204">in your default browser.</span></span>

![Azure Web 應用程式](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="17b4b-206">摘要</span><span class="sxs-lookup"><span data-stu-id="17b4b-206">Summary</span></span>
<span data-ttu-id="17b4b-207">在本教學課程中，您學到如何在 VS Code 建立 Web 應用程式，並將其部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="17b4b-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="17b4b-208">如需有關 VS Code 的詳細資訊，請參閱文章：[為什選擇 Visual Studio Code？](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="17b4b-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="17b4b-209">如需 App Service Web Apps 的相關資訊，請參閱 [Web Apps概觀](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="17b4b-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

