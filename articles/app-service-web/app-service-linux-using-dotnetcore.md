---
title: "在 Linux 上的 Web 應用程式的.NET Core aaaUse |Microsoft 文件"
description: "在 Linux 上的 Web 應用程式中使用 .NET Core。"
keywords: "azure app service, Web 應用程式, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="498e5-104">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="498e5-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="498e5-105">[Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro)on Linux 會提供可高度擴充、 自我修補 web 主控服務，使用 hello Linux 作業系統。</span><span class="sxs-lookup"><span data-stu-id="498e5-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="498e5-106">本教學課程包含逐步解說顯示如何 toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) on Linux 的 Azure web 應用程式為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498e5-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Linux 上的 Web 應用程式][10]

<span data-ttu-id="498e5-108">您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="498e5-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="498e5-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="498e5-109">Prerequisites</span></span> ##

<span data-ttu-id="498e5-110">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="498e5-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="498e5-111">安裝 hello [.NET Core SDK](https://www.microsoft.com/net/download/core)。</span><span class="sxs-lookup"><span data-stu-id="498e5-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="498e5-112">安裝 [Git](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="498e5-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="498e5-113">建立本機 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="498e5-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="498e5-114">啟動新的終端機工作階段。</span><span class="sxs-lookup"><span data-stu-id="498e5-114">Start a new terminal session.</span></span> <span data-ttu-id="498e5-115">建立名為目錄`hellodotnetcore`，並變更目前目錄 tooit hello。</span><span class="sxs-lookup"><span data-stu-id="498e5-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="498e5-116">然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="498e5-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="498e5-117">此命令會建立三個檔案 (*hellodotnetcore.csproj*， *Program.cs*，和*Startup.cs*) 和一個空的資料夾 (*wwwroot /*)在 hello 目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="498e5-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="498e5-118">內容的 hello`.csproj`檔案應該看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="498e5-118">hello content of `.csproj` file should look like hello following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="498e5-119">此應用程式是 web 應用程式，因為 ASP.NET Core 套件已自動參考 tooan 加入 toohello *hellodotnetcore.csproj*檔案。</span><span class="sxs-lookup"><span data-stu-id="498e5-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="498e5-120">根據選擇 framework toohello 設定 hello 套件 hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="498e5-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="498e5-121">因為使用 .NET Core 1.1，所以此範例會參考 ASP.NET Core 1.1.2 版。</span><span class="sxs-lookup"><span data-stu-id="498e5-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="498e5-122">建置和測試本機 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="498e5-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="498e5-123">您可以建置並執行.NET Core 應用程式以 hello`dotnet restore`命令，接著 hello`dotnet run`命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="498e5-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="498e5-124">Hello 應用程式啟動時，它會顯示訊息，指出 hello 應用程式正在接聽連接埠 tooincoming 要求。</span><span class="sxs-lookup"><span data-stu-id="498e5-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="498e5-125">測試瀏覽過`http://localhost:5000/`與瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="498e5-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="498e5-126">如果一切運作正常，您會看到 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="498e5-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="498e5-127">為 hello 結果文字。</span><span class="sxs-lookup"><span data-stu-id="498e5-127">as hello result text.</span></span>

![使用瀏覽器測試][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="498e5-129">在 hello Azure 入口網站中建立.NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="498e5-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="498e5-130">首先，您需要 toocreate 空 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="498e5-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="498e5-131">登入 toohello [Azure 入口網站](https://portal.azure.com/)並建立新[Linux 上的 Web 應用程式](https://portal.azure.com/#create/Microsoft.AppSvcLinux)。</span><span class="sxs-lookup"><span data-stu-id="498e5-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![建立 Web 應用程式][1]

<span data-ttu-id="498e5-133">當 hello**建立**頁面開啟時，提供您的 web 應用程式的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="498e5-133">When hello **Create** page opens, provide details about your web app:</span></span>

![選擇 .NET Core 執行階段堆疊][2]

<span data-ttu-id="498e5-135">使用 hello 下表作為指南 toofill 出 hello**建立**頁面上，然後選取 **確定**和**建立**toocreate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="498e5-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="498e5-136">設定</span><span class="sxs-lookup"><span data-stu-id="498e5-136">Setting</span></span>      | <span data-ttu-id="498e5-137">建議的值</span><span class="sxs-lookup"><span data-stu-id="498e5-137">Suggested value</span></span>  | <span data-ttu-id="498e5-138">說明</span><span class="sxs-lookup"><span data-stu-id="498e5-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="498e5-139">應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="498e5-139">App name</span></span> | <span data-ttu-id="498e5-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="498e5-140">hellodotnetcore</span></span>  | <span data-ttu-id="498e5-141">hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="498e5-141">hello name of your app.</span></span> <span data-ttu-id="498e5-142">此名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="498e5-142">This name must be unique.</span></span> |
| <span data-ttu-id="498e5-143">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="498e5-143">Subscription</span></span> | <span data-ttu-id="498e5-144">選擇現有的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="498e5-144">Choose an existing subscription</span></span> | <span data-ttu-id="498e5-145">hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="498e5-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="498e5-146">資源群組</span><span class="sxs-lookup"><span data-stu-id="498e5-146">Resource Group</span></span> | <span data-ttu-id="498e5-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="498e5-147">myResourceGroup</span></span> |  <span data-ttu-id="498e5-148">hello Azure 資源群組 toocontain hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="498e5-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="498e5-149">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="498e5-149">App Service Plan</span></span> | <span data-ttu-id="498e5-150">現有的 App Service 方案名稱</span><span class="sxs-lookup"><span data-stu-id="498e5-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="498e5-151">hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="498e5-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="498e5-152">設定容器</span><span class="sxs-lookup"><span data-stu-id="498e5-152">Configure Container</span></span> | <span data-ttu-id="498e5-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="498e5-153">.NET Core 1.1</span></span> | <span data-ttu-id="498e5-154">hello 此 web 應用程式的容器類型： 內建、 Docker 或私人登錄中。</span><span class="sxs-lookup"><span data-stu-id="498e5-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="498e5-155">映像來源</span><span class="sxs-lookup"><span data-stu-id="498e5-155">Image source</span></span>  | <span data-ttu-id="498e5-156">內建</span><span class="sxs-lookup"><span data-stu-id="498e5-156">Built-in</span></span>  |  <span data-ttu-id="498e5-157">hello hello 映像的來源。</span><span class="sxs-lookup"><span data-stu-id="498e5-157">hello source of hello image.</span></span> |
| <span data-ttu-id="498e5-158">執行階段堆疊</span><span class="sxs-lookup"><span data-stu-id="498e5-158">Runtime Stack</span></span>  | <span data-ttu-id="498e5-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="498e5-159">.NET Core 1.1</span></span>  | <span data-ttu-id="498e5-160">執行階段堆疊時會 hello 和版本。</span><span class="sxs-lookup"><span data-stu-id="498e5-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="498e5-161">透過 Get 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="498e5-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="498e5-162">在 Linux 上使用 Git toodeploy hello.NET Core 應用程式 tooAzure App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="498e5-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="498e5-163">hello 新 Azure web 應用程式已經有 Git 部署設定。</span><span class="sxs-lookup"><span data-stu-id="498e5-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="498e5-164">您可以藉由瀏覽下列 URL 並插入您的 web 應用程式名稱的 toohello 找到 hello Git 部署 URL:</span><span class="sxs-lookup"><span data-stu-id="498e5-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="498e5-165">hello Git URL 具有下列根據您的 web 應用程式名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="498e5-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="498e5-166">執行下列命令 toodeploy hello 本機應用程式 tooyour Azure web 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="498e5-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="498e5-167">您不需要 toopush 之下任何檔案*bin /*或*obj /*目錄 hello 雲端中建置應用程式，因為當 hello 應用程式的原始程式檔會推入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="498e5-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="498e5-168">Hello 建置程序完成之後，二進位檔案會複製到在 hello 應用程式的目錄*/住家/網站/wwwroot/*。</span><span class="sxs-lookup"><span data-stu-id="498e5-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="498e5-169">確認 hello 遠端部署作業報告成功。</span><span class="sxs-lookup"><span data-stu-id="498e5-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="498e5-170">推入作業可能需要一些時間，因為封裝解析度和建置在 hello 雲端中執行的程序。</span><span class="sxs-lookup"><span data-stu-id="498e5-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="498e5-171">您會看到數則狀態訊息，包括陳述已複製檔案的訊息。</span><span class="sxs-lookup"><span data-stu-id="498e5-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="498e5-172">hello 輸出應該看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="498e5-172">hello output should look similar toohello following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="498e5-173">Hello 部署完成後，請重新啟動您的 web 應用程式，hello 部署 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="498e5-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="498e5-174">toodo 這個移 toohello Azure 入口網站及瀏覽 toohello**概觀**web 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="498e5-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="498e5-175">選取 hello**重新啟動**hello 頁面中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="498e5-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="498e5-176">快顯視窗出現時，選取**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="498e5-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="498e5-177">您可以瀏覽您的 Web 應用程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="498e5-177">You can then browse your web app, as shown here:</span></span>

![瀏覽.NET Core 應用程式部署 tooAzure Linux 上的應用程式服務][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="498e5-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="498e5-179">Next steps</span></span>
* [<span data-ttu-id="498e5-180">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="498e5-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
