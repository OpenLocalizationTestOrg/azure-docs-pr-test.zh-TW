---
title: "在 Linux 上的 Web 應用程式中使用 .NET Core | Microsoft Docs"
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
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="09d22-104">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="09d22-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="09d22-105">Linux 上的 [Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro)使用 Linux 作業系統提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="09d22-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="09d22-106">本教學課程包含逐步指示，說明如何在 Linux 上的 Azure web 應用程式上建立 [.NET Core](https://docs.microsoft.com/aspnet/core/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09d22-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Linux 上的 Web 應用程式][10]

<span data-ttu-id="09d22-108">您可以使用 Mac、Windows 或 Linux 電腦，依照下面步驟操作。</span><span class="sxs-lookup"><span data-stu-id="09d22-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09d22-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="09d22-109">Prerequisites</span></span> ##

<span data-ttu-id="09d22-110">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="09d22-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="09d22-111">安裝 [.NET Core SDK](https://www.microsoft.com/net/download/core)。</span><span class="sxs-lookup"><span data-stu-id="09d22-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="09d22-112">安裝 [Git](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="09d22-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="09d22-113">建立本機 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="09d22-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="09d22-114">啟動新的終端機工作階段。</span><span class="sxs-lookup"><span data-stu-id="09d22-114">Start a new terminal session.</span></span> <span data-ttu-id="09d22-115">建立名為 `hellodotnetcore` 的目錄，並將目前的目錄變更為該目錄。</span><span class="sxs-lookup"><span data-stu-id="09d22-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="09d22-116">接著輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="09d22-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="09d22-117">此命令會建立三個檔案 (hellodotnetcore.csproj、Program.cs 和 Startup.cs)，以及在目前的目錄下建立一個空資料夾 (wwwroot/)。</span><span class="sxs-lookup"><span data-stu-id="09d22-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="09d22-118">`.csproj` 檔案的內容應如下所示：</span><span class="sxs-lookup"><span data-stu-id="09d22-118">The content of `.csproj` file should look like the following:</span></span> 

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

<span data-ttu-id="09d22-119">由於此應用程式是 Web 應用程式，所以 ASP.NET Core 套件的參考會自動新增至 hellodotnetcore.csproj 檔案。</span><span class="sxs-lookup"><span data-stu-id="09d22-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="09d22-120">系統會根據所選的架構設定套件的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="09d22-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="09d22-121">因為使用 .NET Core 1.1，所以此範例會參考 ASP.NET Core 1.1.2 版。</span><span class="sxs-lookup"><span data-stu-id="09d22-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="09d22-122">在本機建置和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="09d22-122">Build and test the application locally</span></span> ##

<span data-ttu-id="09d22-123">您可以使用 `dotnet restore` 命令後面接著 `dotnet run` 命令，建置及執行 .NET Core 應用程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="09d22-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="09d22-124">當應用程式啟動時，它會顯示一則訊息，指出應用程式正在連接埠接聽連入要求。</span><span class="sxs-lookup"><span data-stu-id="09d22-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="09d22-125">測試瀏覽至`http://localhost:5000/`與瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="09d22-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="09d22-126">如果一切運作正常，您會看到 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="09d22-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="09d22-127">作為結果文字。</span><span class="sxs-lookup"><span data-stu-id="09d22-127">as the result text.</span></span>

![使用瀏覽器測試][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="09d22-129">在 Azure 入口網站中建立 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="09d22-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="09d22-130">首先，您必須建立空的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="09d22-130">First you need to create an empty web app.</span></span> <span data-ttu-id="09d22-131">登入 [Azure 入口網站](https://portal.azure.com/)，並[在 Linux 上建立新的 Web 應用程式](https://portal.azure.com/#create/Microsoft.AppSvcLinux)。</span><span class="sxs-lookup"><span data-stu-id="09d22-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![建立 Web 應用程式][1]

<span data-ttu-id="09d22-133">當 [建立] 頁面開啟時，提供您的 Web 應用程式詳細資料：</span><span class="sxs-lookup"><span data-stu-id="09d22-133">When the **Create** page opens, provide details about your web app:</span></span>

![選擇 .NET Core 執行階段堆疊][2]

<span data-ttu-id="09d22-135">使用下表作為指南來填寫 [建立] 頁面，然後選取 [確定] 和 [建立] 來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="09d22-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="09d22-136">設定</span><span class="sxs-lookup"><span data-stu-id="09d22-136">Setting</span></span>      | <span data-ttu-id="09d22-137">建議的值</span><span class="sxs-lookup"><span data-stu-id="09d22-137">Suggested value</span></span>  | <span data-ttu-id="09d22-138">說明</span><span class="sxs-lookup"><span data-stu-id="09d22-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="09d22-139">應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="09d22-139">App name</span></span> | <span data-ttu-id="09d22-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="09d22-140">hellodotnetcore</span></span>  | <span data-ttu-id="09d22-141">您的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="09d22-141">The name of your app.</span></span> <span data-ttu-id="09d22-142">此名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="09d22-142">This name must be unique.</span></span> |
| <span data-ttu-id="09d22-143">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="09d22-143">Subscription</span></span> | <span data-ttu-id="09d22-144">選擇現有的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="09d22-144">Choose an existing subscription</span></span> | <span data-ttu-id="09d22-145">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09d22-145">The Azure subscription.</span></span> |
| <span data-ttu-id="09d22-146">資源群組</span><span class="sxs-lookup"><span data-stu-id="09d22-146">Resource Group</span></span> | <span data-ttu-id="09d22-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="09d22-147">myResourceGroup</span></span> |  <span data-ttu-id="09d22-148">要包含 Web 應用程式的 Azue 資源群組。</span><span class="sxs-lookup"><span data-stu-id="09d22-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="09d22-149">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="09d22-149">App Service Plan</span></span> | <span data-ttu-id="09d22-150">現有的 App Service 方案名稱</span><span class="sxs-lookup"><span data-stu-id="09d22-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="09d22-151">App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="09d22-151">The App Service plan.</span></span>  |
| <span data-ttu-id="09d22-152">設定容器</span><span class="sxs-lookup"><span data-stu-id="09d22-152">Configure Container</span></span> | <span data-ttu-id="09d22-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="09d22-153">.NET Core 1.1</span></span> | <span data-ttu-id="09d22-154">此 Web 應用程式的容器類型：內建、Docker 或私人登錄。</span><span class="sxs-lookup"><span data-stu-id="09d22-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="09d22-155">映像來源</span><span class="sxs-lookup"><span data-stu-id="09d22-155">Image source</span></span>  | <span data-ttu-id="09d22-156">內建</span><span class="sxs-lookup"><span data-stu-id="09d22-156">Built-in</span></span>  |  <span data-ttu-id="09d22-157">映像的來源。</span><span class="sxs-lookup"><span data-stu-id="09d22-157">The source of the image.</span></span> |
| <span data-ttu-id="09d22-158">執行階段堆疊</span><span class="sxs-lookup"><span data-stu-id="09d22-158">Runtime Stack</span></span>  | <span data-ttu-id="09d22-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="09d22-159">.NET Core 1.1</span></span>  | <span data-ttu-id="09d22-160">執行階段堆疊和版本。</span><span class="sxs-lookup"><span data-stu-id="09d22-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="09d22-161">透過 Get 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="09d22-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="09d22-162">使用 Git，在 Linux 上將 .NET Core 應用程式部署至 Azure App Service Web App。</span><span class="sxs-lookup"><span data-stu-id="09d22-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="09d22-163">新的 Azure Web 應用程式已設定 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="09d22-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="09d22-164">將您的 Web 應用程式名稱插入後，瀏覽至下列 URL 就可以找到 Git 部署 URL︰</span><span class="sxs-lookup"><span data-stu-id="09d22-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="09d22-165">根據您的 web 應用程式名稱，Git URL 具有下列格式︰</span><span class="sxs-lookup"><span data-stu-id="09d22-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="09d22-166">執行下列命令，將本機應用程式部署至您的 Azure Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="09d22-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="09d22-167">您不需要推送 *bin /* 或 *obj/*目錄之下的任何檔案，因為當應用程式的原始程式檔推送至 Azure 時，會在雲端建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="09d22-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="09d22-168">建置程序完成之後，二進位檔案會複製到應用程式的目錄：/home/site/wwwroot/。</span><span class="sxs-lookup"><span data-stu-id="09d22-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="09d22-169">確認遠端部署作業報告成功。</span><span class="sxs-lookup"><span data-stu-id="09d22-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="09d22-170">推送作業可能需要一些時間，因為套件解決方案和建置程序會在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="09d22-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="09d22-171">您會看到數則狀態訊息，包括陳述已複製檔案的訊息。</span><span class="sxs-lookup"><span data-stu-id="09d22-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="09d22-172">輸出應如下所示：</span><span class="sxs-lookup"><span data-stu-id="09d22-172">The output should look similar to the following:</span></span>

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
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="09d22-173">一旦部署完成後，需重新啟動 Web 應用程式進行部署，才會生效。</span><span class="sxs-lookup"><span data-stu-id="09d22-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="09d22-174">若要這麼做，請移至 Azure 入口網站並巡覽至您 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="09d22-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="09d22-175">選取頁面中的 [重新啟動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="09d22-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="09d22-176">快顯視窗出現時，選取 [是] 進行確認。</span><span class="sxs-lookup"><span data-stu-id="09d22-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="09d22-177">您可以瀏覽您的 Web 應用程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="09d22-177">You can then browse your web app, as shown here:</span></span>

![在 Linux 上瀏覽已部署至 Azure App Service 的 .NET Core 應用程式][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="09d22-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09d22-179">Next steps</span></span>
* [<span data-ttu-id="09d22-180">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="09d22-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
