---
title: "aaaCreate Visual Studio 程式碼中的 ASP.NET Core web 應用程式"
description: "本教學課程說明如何 toocreate ASP.NET Core web 應用程式使用 Visual Studio 程式碼。"
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
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="a6308-103">在 Visual Studio Code 中建立 ASP.NET Core Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="a6308-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a6308-104">Overview</span></span>
<span data-ttu-id="a6308-105">本教學課程告訴您如何 toocreate ASP.NET Core web 應用程式使用[Visual Studio 程式碼 (VS Code)](http://code.visualstudio.com//Docs/whyvscode)並將它部署到太[Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="a6308-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="a6308-106">雖然這篇文章是指 tooweb 應用程式，它也適用於 tooAPI 應用程式和行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="a6308-107">ASP.NET Core 是大幅重新設計的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a6308-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="a6308-108">ASP.NET Core 是新的開放原始碼和跨平台架構，用於使用 .NET 建置新代雲端式 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="a6308-109">如需詳細資訊，請參閱[簡介 tooASP.NET 核心](http://docs.asp.net/latest/conceptual-overview/aspnet.html)。</span><span class="sxs-lookup"><span data-stu-id="a6308-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="a6308-110">如需有關 Azure App Service Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6308-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="a6308-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="a6308-111">Prerequisites</span></span>
* <span data-ttu-id="a6308-112">安裝 [VS Code](http://code.visualstudio.com/Docs/setup)。</span><span class="sxs-lookup"><span data-stu-id="a6308-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="a6308-113">安裝 Git - 您可以從下列位置安裝它：[Chocolatey](https://chocolatey.org/packages/git) 或 [git-scm.com](http://git-scm.com/downloads)。如果您是新 tooGit，選擇  [git scm.com](http://git-scm.com/downloads)太選取 hello 選項**從 hello Windows 命令提示字元使用 Git**。</span><span class="sxs-lookup"><span data-stu-id="a6308-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="a6308-114">一旦您安裝 Git，您還需要 tooset hello Git 使用者名稱和電子郵件時 （從 VS 程式碼中執行認可） 時，稍後在 hello 教學課程所需。</span><span class="sxs-lookup"><span data-stu-id="a6308-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="a6308-115">安裝 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a6308-115">Install ASP.NET Core</span></span>
<span data-ttu-id="a6308-116">ASP.NET Core 是精簡的 .NET 堆疊，可建置 OS X、Linux 和 Windows 上執行的新式雲端和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="a6308-117">已建置從 hello 地面向上 tooprovide 是其中一個已部署的 toohello 雲端，或執行在內部部署的應用程式是最佳化的開發架構。</span><span class="sxs-lookup"><span data-stu-id="a6308-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="a6308-118">其由額外負荷最低的模組化元件組成，以便您可以在建構解決方案時保留彈性。</span><span class="sxs-lookup"><span data-stu-id="a6308-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="a6308-119">本教學課程是設計的 tooget 您開始建置 hello 最新開發版本的 ASP.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="a6308-120">下列指示的 hello 是特定 tooWindows。</span><span class="sxs-lookup"><span data-stu-id="a6308-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="a6308-121">如需 OS X、Linux 和 Windows 的安裝指示，請參閱[開始使用 ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started)。</span><span class="sxs-lookup"><span data-stu-id="a6308-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="a6308-122">如需 OS X、Linux 和 Windows 的更詳細安裝指示，請參閱[安裝 ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)。</span><span class="sxs-lookup"><span data-stu-id="a6308-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="a6308-123">建立 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-123">Create hello web app</span></span>
<span data-ttu-id="a6308-124">本節說明如何 tooscaffold 新應用程式的 ASP.NET web 應用程式使用 hello.NET CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="a6308-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="a6308-125">輸入 hello 下列在 hello 命令提示字元 toocreate hello 專案資料夾，然後 scaffold hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 產生器](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="a6308-127">toorestore hello 必要的 NuGet 套件，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6308-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="a6308-128">在本機執行 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-128">Run hello web app locally</span></span>
<span data-ttu-id="a6308-129">現在，您有建立 hello web 應用程式，並擷取所有 hello NuGet 套件 hello 應用程式，您可以在本機執行 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="a6308-130">執行 hello 應用程式 (hello`dotnet run`過期時，命令將會建置 hello 應用程式):</span><span class="sxs-lookup"><span data-stu-id="a6308-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="a6308-131">開啟瀏覽器，並瀏覽 toohello 下列 URL。</span><span class="sxs-lookup"><span data-stu-id="a6308-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="a6308-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="a6308-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="a6308-133">hello hello web 應用程式的預設頁面會出現，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6308-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![在瀏覽器中的本機 Web 應用程式](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="a6308-135">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a6308-135">Close your browser.</span></span> <span data-ttu-id="a6308-136">在 hello**命令視窗**，按**Ctrl + C**向下 hello 應用程式，然後關閉 hello tooshut**命令視窗**。</span><span class="sxs-lookup"><span data-stu-id="a6308-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="a6308-137">在 hello Azure 入口網站中建立 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="a6308-138">hello 下列步驟將引導您完成在 hello Azure 入口網站中建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="a6308-139">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a6308-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6308-140">按一下**新增**hello 在左上方的 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a6308-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="a6308-141">按一下 [Web Apps] > [Web Apps]。</span><span class="sxs-lookup"><span data-stu-id="a6308-141">Click **Web Apps > Web App**.</span></span>
   
    ![Azure 的新 Web 應用程式](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="a6308-143">輸入 [名稱] 的值，例如 **SampleWebAppDemo**。</span><span class="sxs-lookup"><span data-stu-id="a6308-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="a6308-144">請注意，此名稱必須唯一，toobe hello 入口網站將會強制執行，當您嘗試 tooenter hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a6308-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="a6308-145">因此，如果您選取輸入不同的值，您將需要值的 toosubstitute 每次發生**SampleWebAppDemo**您在本教學課程中看到。</span><span class="sxs-lookup"><span data-stu-id="a6308-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="a6308-146">選取現有的 **App Service 方案** 或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="a6308-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="a6308-147">如果您建立新的計畫，請選取定價層、 位置和其他選項的 hello。</span><span class="sxs-lookup"><span data-stu-id="a6308-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="a6308-148">如需有關應用程式服務方案的詳細資訊，請參閱 hello 文章[Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6308-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure 的新 Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="a6308-150">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a6308-150">Click **Create**.</span></span>
   
    ![Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="a6308-152">啟用 Git 發行功能 hello 新 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="a6308-153">Git 是分散式的版本控制系統，您可以使用 toodeploy Azure App Service web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="a6308-154">想要儲存您的本機 Git 儲存機制，在 web 應用程式所撰寫的 hello 程式碼和您要部署您的程式碼 tooAzure 推送 tooa 遠端儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a6308-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="a6308-155">登入 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a6308-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6308-156">按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="a6308-156">Click **Browse**.</span></span>
3. <span data-ttu-id="a6308-157">按一下**Web 應用程式**tooview hello 與您 Azure 訂用帳戶相關聯的 web 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a6308-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="a6308-158">選取您在本教學課程中建立的 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="a6308-159">在 hello web 應用程式刀鋒視窗中，按一下 **設定** > **連續部署**。</span><span class="sxs-lookup"><span data-stu-id="a6308-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure Web 應用程式主機](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="a6308-161">按一下 [選擇來源] > [本機 Git 儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="a6308-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="a6308-162">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a6308-162">Click **OK**.</span></span>
   
    ![Azure 本機 Git 儲存機制](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="a6308-164">如果您先前尚未設定部署認證以供發佈 Web 應用程式或其他 App Service 應用程式，請立即設定：</span><span class="sxs-lookup"><span data-stu-id="a6308-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="a6308-165">按一下 [設定] > [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="a6308-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="a6308-166">hello**設定部署認證**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="a6308-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="a6308-167">建立使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a6308-167">Create a user name and password.</span></span>  <span data-ttu-id="a6308-168">稍後設定 Git 時，您將需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="a6308-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="a6308-169">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a6308-169">Click **Save**.</span></span>
9. <span data-ttu-id="a6308-170">在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="a6308-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="a6308-171">hello hello 遠端 Git 儲存機制的 URL，您將會部署 toois 下方顯示**GIT URL**。</span><span class="sxs-lookup"><span data-stu-id="a6308-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="a6308-172">複製 hello **GIT URL**供稍後使用 hello 教學課程中的值。</span><span class="sxs-lookup"><span data-stu-id="a6308-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="a6308-174">發行您的 web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="a6308-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="a6308-175">在本節中，您將建立的本機 Git 儲存機制，並從該儲存機制 tooAzure toodeploy 推送您的 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a6308-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="a6308-176">在 VS 程式碼中，選取 hello **Git** hello 左側的導覽列中的選項。</span><span class="sxs-lookup"><span data-stu-id="a6308-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![VS Code 中的 Git 圖示](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="a6308-178">選取**初始化 git 儲存機制**toomake 確定您的工作區是在 git 原始檔控制之下。</span><span class="sxs-lookup"><span data-stu-id="a6308-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![初始化 Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="a6308-180">開啟 hello 命令視窗，並變更您的 web 應用程式的目錄 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="a6308-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="a6308-181">然後，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6308-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="a6308-182">此命令可防止涉及 CRLF 行尾結束符號和 LF 行尾結束符號之文字的相關問題。</span><span class="sxs-lookup"><span data-stu-id="a6308-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="a6308-183">在 VS 程式碼中，加入 「 認可 」 訊息，按一下 hello**認可所有**核取圖示。</span><span class="sxs-lookup"><span data-stu-id="a6308-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Git 全部認可](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="a6308-185">Git 已完成處理之後，您會看到沒有列在底下的 hello Git 視窗中的檔案**變更**。</span><span class="sxs-lookup"><span data-stu-id="a6308-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git 沒有變更](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="a6308-187">變更後 toohello 命令視窗 hello 命令提示字元 toohello 目錄所指位置您 web 應用程式所在的位置。</span><span class="sxs-lookup"><span data-stu-id="a6308-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="a6308-188">建立使用您先前複製的 Git URL （結束".git"中） hello 推送更新 tooyour web 應用程式的遠端參考。</span><span class="sxs-lookup"><span data-stu-id="a6308-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="a6308-189">在本機，因此它們會自動附加的 tooyour push 命令從 VS 程式碼產生設定 Git toosave 您的認證。</span><span class="sxs-lookup"><span data-stu-id="a6308-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="a6308-190">輸入下列命令的 hello 推送變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a6308-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="a6308-191">這個初始的推播 tooAzure 之後, 您將會無法 toodo 所有 hello 發送都命令從 VS 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a6308-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="a6308-192">系統提示您輸入您稍早在 Azure 中建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="a6308-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="a6308-193">**注意：將看不到您的密碼。**</span><span class="sxs-lookup"><span data-stu-id="a6308-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="a6308-194">從上述命令 hello hello 輸出的最後一則訊息部署成功。</span><span class="sxs-lookup"><span data-stu-id="a6308-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="a6308-195">若要變更 tooyour 應用程式，您可以重新發行使用 hello 內建的 Git 功能選取 hello 的 VS 程式碼中直接**認可所有**選項後面 hello**推送**選項。</span><span class="sxs-lookup"><span data-stu-id="a6308-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="a6308-196">您會發現 hello**推送**選項可以在 hello 下拉式功能表的 下一步 toohello**認可所有**和**重新整理**按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6308-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="a6308-197">如果您需要在專案上的 toocollaborate，您應該考慮推送 tooGitHub 推送 tooAzure 之間。</span><span class="sxs-lookup"><span data-stu-id="a6308-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="a6308-198">在 Azure 中執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-198">Run hello app in Azure</span></span>
<span data-ttu-id="a6308-199">既然您已部署的 hello 應用程式裝載於 Azure 時，我們先執行您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6308-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="a6308-200">這有兩種方式可以完成：</span><span class="sxs-lookup"><span data-stu-id="a6308-200">This can be done in two ways:</span></span>

* <span data-ttu-id="a6308-201">開啟瀏覽器然後輸入 hello 名稱的 web 應用程式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6308-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="a6308-202">在 hello Azure 入口網站，找出 hello web 應用程式的 web 應用程式刀鋒視窗並按一下**瀏覽**tooview 您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a6308-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="a6308-203">預設瀏覽器</span><span class="sxs-lookup"><span data-stu-id="a6308-203">in your default browser.</span></span>

![Azure Web 應用程式](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="a6308-205">摘要</span><span class="sxs-lookup"><span data-stu-id="a6308-205">Summary</span></span>
<span data-ttu-id="a6308-206">在本教學課程中，您學到如何 toocreate VS 程式碼中的 web 應用程式並將其部署 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a6308-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="a6308-207">如需 VS 程式碼的詳細資訊，請參閱 hello 文件，[為何 Visual Studio 程式碼？](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="a6308-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="a6308-208">如需 App Service Web Apps 的相關資訊，請參閱 [Web Apps概觀](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6308-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

