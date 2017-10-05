---
title: "Azure Web 應用程式的部署常見問題集 | Microsoft Docs"
description: "對於 Azure App Service 的 Web 應用程式功能之中的部署相關的常見問題集獲得解答。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 69f8c50f7f5889b75544deca19c54268fbf5eca7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a><span data-ttu-id="845de-103">Azure 中 Web 應用程式的部署常見問題集</span><span class="sxs-lookup"><span data-stu-id="845de-103">Deployment FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="845de-104">對於 [Azure App Service 的 Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)的部署問題，本文提供常見問題集的解答。</span><span class="sxs-lookup"><span data-stu-id="845de-104">This article has answers to frequently asked questions (FAQs) about deployment issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a><span data-ttu-id="845de-105">我剛開始使用 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="845de-105">I am just getting started with App Service web apps.</span></span> <span data-ttu-id="845de-106">如何發佈程式碼？</span><span class="sxs-lookup"><span data-stu-id="845de-106">How do I publish my code?</span></span>

<span data-ttu-id="845de-107">以下是發佈 Web 應用程式程式碼的一些選項：</span><span class="sxs-lookup"><span data-stu-id="845de-107">Here are some options for publishing your web app code:</span></span>

*   <span data-ttu-id="845de-108">使用 Visual Studio 進行部署。</span><span class="sxs-lookup"><span data-stu-id="845de-108">Deploy by using Visual Studio.</span></span> <span data-ttu-id="845de-109">如果您有 Visual Studio 解決方案，以滑鼠右鍵按一下 Web 應用程式專案，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="845de-109">If you have the Visual Studio solution, right-click the web application project, and then select **Publish**.</span></span>
*   <span data-ttu-id="845de-110">使用 FTP 用戶端進行部署。</span><span class="sxs-lookup"><span data-stu-id="845de-110">Deploy by using an FTP client.</span></span> <span data-ttu-id="845de-111">在 Azure 入口網站中，下載您想要部署程式碼之 Web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="845de-111">In the Azure portal, download the publish profile for the web app that you want to deploy your code to.</span></span> <span data-ttu-id="845de-112">然後，使用相同的發行設定檔 FTP 認證將檔案上傳至 \site\wwwroot。</span><span class="sxs-lookup"><span data-stu-id="845de-112">Then, upload the files to \site\wwwroot by using the same publish profile FTP credentials.</span></span>

<span data-ttu-id="845de-113">如需詳細資訊，請參閱[將應用程式部署到 App Service](web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="845de-113">For more information, see [Deploy your app to App Service](web-sites-deploy.md).</span></span>

## <a name="i-see-an-error-message-when-i-try-to-deploy-from-visual-studio-how-do-i-resolve-this"></a><span data-ttu-id="845de-114">當我嘗試從 Visual Studio 部署時，我看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="845de-114">I see an error message when I try to deploy from Visual Studio.</span></span> <span data-ttu-id="845de-115">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="845de-115">How do I resolve this?</span></span>

<span data-ttu-id="845de-116">如果您看到下列訊息，您可能是使用舊版的 SDK：「在資源群組 'YourResourceGroup' 中部署資源 'YourResourceName' 期間發生錯誤：MissingRegistrationForLocation：訂用帳戶未在位置「美國中部」註冊資源類型「組件」。</span><span class="sxs-lookup"><span data-stu-id="845de-116">If you see the following message, you might be using an older version of the SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: The subscription is not registered for the resource type 'components' in the location 'Central US'.</span></span> <span data-ttu-id="845de-117">請重新註冊此提供者以獲得此位置的存取權」。</span><span class="sxs-lookup"><span data-stu-id="845de-117">Please re-register for this provider in order to have access to this location.”</span></span> 

<span data-ttu-id="845de-118">若要解決這個錯誤，請升級為[最新的 SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="845de-118">To resolve this error, upgrade to the [latest SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="845de-119">如果您看到此訊息，而且您有最新的 SDK，請提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="845de-119">If you see this message and you have the latest SDK, submit a support request.</span></span>

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-to-app-service"></a><span data-ttu-id="845de-120">如何將 ASP.NET 應用程式從 Visual Studio 部署到 App Service？</span><span class="sxs-lookup"><span data-stu-id="845de-120">How do I deploy an ASP.NET application from Visual Studio to App Service?</span></span>
<a id="deployasp"></a>

<span data-ttu-id="845de-121">本教學課程[五分鐘內在 Azure 中建立第一個 ASP.NET Web 應用程式](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/)示範如何使用 Visual Studio 2015，將 ASP.NET Web 應用程式部署到 App Service 中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="845de-121">The tutorial [Create your first ASP.NET web app in Azure in five minutes](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) shows you how to deploy an ASP.NET web application to a web app in App Service by using Visual Studio 2015.</span></span>

## <a name="what-are-the-different-types-of-deployment-credentials"></a><span data-ttu-id="845de-122">不同類型的部署認證有哪些？</span><span class="sxs-lookup"><span data-stu-id="845de-122">What are the different types of deployment credentials?</span></span>

<span data-ttu-id="845de-123">App Service 支援兩種認證類型，用於本機 Git 部署和 FTP/S 部署。</span><span class="sxs-lookup"><span data-stu-id="845de-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span></span> <span data-ttu-id="845de-124">如需如何設定部署認證的詳細資訊，請參閱[設定 App Service 的部署認證](app-service-deployment-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="845de-124">For more information about how to configure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span></span>

## <a name="what-is-the-file-or-directory-structure-of-my-app-service-web-app"></a><span data-ttu-id="845de-125">我的 App Service Web 應用程式的檔案或目錄結構是什麼？</span><span class="sxs-lookup"><span data-stu-id="845de-125">What is the file or directory structure of my App Service web app?</span></span>

<span data-ttu-id="845de-126">如需您的 App Service 應用程式的檔案結構詳細資訊，請參閱 [Azure 中的檔案結構](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)。</span><span class="sxs-lookup"><span data-stu-id="845de-126">For information about the file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span></span>

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-the-disk-when-i-try-to-ftp-my-files"></a><span data-ttu-id="845de-127">當我嘗試 FTP 我的檔案時，如何解決「FTP 錯誤 550 - 磁碟空間不足」？</span><span class="sxs-lookup"><span data-stu-id="845de-127">How do I resolve "FTP Error 550 - There is not enough space on the disk" when I try to FTP my files?</span></span>

<span data-ttu-id="845de-128">如果您看到此訊息，可能是您即將用盡 Web 應用程式之服務方案中的磁碟配額。</span><span class="sxs-lookup"><span data-stu-id="845de-128">If you see this message, it's likely that you are running into a disk quota in the service plan for your web app.</span></span> <span data-ttu-id="845de-129">您可能需要根據您的磁碟空間需求，相應增加至較高服務層。</span><span class="sxs-lookup"><span data-stu-id="845de-129">You might need to scale up to a higher service tier based on your disk space needs.</span></span> <span data-ttu-id="845de-130">如需定價方案和資源限制的詳細資訊，請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="845de-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a><span data-ttu-id="845de-131">如何為 App Service Web 應用程式設定持續部署？</span><span class="sxs-lookup"><span data-stu-id="845de-131">How do I set up continuous deployment for my App Service web app?</span></span>

<span data-ttu-id="845de-132">您可以從數個資源設定持續部署，包括 Visual Studio Team Services、OneDrive、GitHub、Bitbucket、Dropbox 和其他 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="845de-132">You can set up continuous deployment from several resources, including Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span></span> <span data-ttu-id="845de-133">這些選項可在入口網站中使用。</span><span class="sxs-lookup"><span data-stu-id="845de-133">These options are available in the portal.</span></span> <span data-ttu-id="845de-134">[持續部署至 App Service](app-service-continuous-deployment.md) 是很有幫助的教學課程，說明如何設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="845de-134">[Continuous deployment to App Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how to set up continuous deployment.</span></span>

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a><span data-ttu-id="845de-135">如何針對從 GitHub 和 Bitbucket 持續部署的問題進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="845de-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span></span>

<span data-ttu-id="845de-136">如需調查從 GitHub 或 Bitbucket 持續部署之問題的協助，請參閱[調查持續部署](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)。</span><span class="sxs-lookup"><span data-stu-id="845de-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span></span>

## <a name="i-cant-ftp-to-my-site-and-publish-my-code-how-do-i-resolve-this"></a><span data-ttu-id="845de-137">我無法 FTP 至我的網站及發佈我的程式碼。</span><span class="sxs-lookup"><span data-stu-id="845de-137">I can't FTP to my site and publish my code.</span></span> <span data-ttu-id="845de-138">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="845de-138">How do I resolve this?</span></span>

<span data-ttu-id="845de-139">若要解決 FTP 問題：</span><span class="sxs-lookup"><span data-stu-id="845de-139">To resolve FTP issues:</span></span>

1. <span data-ttu-id="845de-140">請確認您輸入正確的主機名稱和認證。</span><span class="sxs-lookup"><span data-stu-id="845de-140">Verify that you are entering the correct host name and credentials.</span></span> <span data-ttu-id="845de-141">如需不同類型認證和使用方式的詳細資訊，請參閱[部署認證](https://github.com/projectkudu/kudu/wiki/Deployment-credentials)。</span><span class="sxs-lookup"><span data-stu-id="845de-141">For detailed information about different types of credentials and how to use them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span></span>
2. <span data-ttu-id="845de-142">請確認 FTP 連接埠未遭防火牆封鎖。</span><span class="sxs-lookup"><span data-stu-id="845de-142">Verify that the FTP ports are not blocked by a firewall.</span></span> <span data-ttu-id="845de-143">連接埠應該具有以下設定：</span><span class="sxs-lookup"><span data-stu-id="845de-143">The ports should have these settings:</span></span>
    * <span data-ttu-id="845de-144">FTP 控制連線連接埠︰21</span><span class="sxs-lookup"><span data-stu-id="845de-144">FTP control connection port: 21</span></span>
    * <span data-ttu-id="845de-145">FTP 資料連線連接埠︰989、10001-10300</span><span class="sxs-lookup"><span data-stu-id="845de-145">FTP data connection port: 989, 10001-10300</span></span>

## <a name="how-do-i-publish-my-code-to-app-service"></a><span data-ttu-id="845de-146">如何將我的程式碼發佈至 App Service？</span><span class="sxs-lookup"><span data-stu-id="845de-146">How do I publish my code to App Service?</span></span>

<span data-ttu-id="845de-147">「Azure 快速入門」的設計目的是協助您使用部署堆疊和您選擇的方法來部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="845de-147">The Azure Quickstart is designed to help you deploy your app by using the deployment stack and method of your choice.</span></span> <span data-ttu-id="845de-148">若要使用快速入門，請在 Azure 入口網站中移至 [設定] >  [應用程式部署]。</span><span class="sxs-lookup"><span data-stu-id="845de-148">To use the Quickstart, in the Azure portal, go to **Settings** > **App Deployment**.</span></span>

## <a name="why-does-my-app-sometimes-restart-after-deployment-to-app-service"></a><span data-ttu-id="845de-149">為什麼我的應用程式有時候會在部署至 App Service 之後重新啟動？</span><span class="sxs-lookup"><span data-stu-id="845de-149">Why does my app sometimes restart after deployment to App Service?</span></span>

<span data-ttu-id="845de-150">若要深入了解可能會造成重新啟動之應用程式部署的情況，請參閱[部署與執行階段問題](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts")。</span><span class="sxs-lookup"><span data-stu-id="845de-150">To learn about the circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span></span> <span data-ttu-id="845de-151">如本文章所述，App Service 會將檔案部署到 wwwroot 資料夾。</span><span class="sxs-lookup"><span data-stu-id="845de-151">As the article describes, App Service deploys files to the wwwroot folder.</span></span> <span data-ttu-id="845de-152">它永遠不會直接重新啟動您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="845de-152">It never directly restarts your app.</span></span>

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a><span data-ttu-id="845de-153">如何整合 Visual Studio Team Services 程式碼與 App Service？</span><span class="sxs-lookup"><span data-stu-id="845de-153">How do I integrate Visual Studio Team Services code with App Service?</span></span>

<span data-ttu-id="845de-154">您有兩個選項可以使用 Visual Studio Team Services 進行持續部署：</span><span class="sxs-lookup"><span data-stu-id="845de-154">You have two options for using continuous deployment with Visual Studio Team Services:</span></span>

*   <span data-ttu-id="845de-155">使用 Git 專案。</span><span class="sxs-lookup"><span data-stu-id="845de-155">Use a Git project.</span></span> <span data-ttu-id="845de-156">藉由使用該存放庫的部署選項以透過 App Service 連線。</span><span class="sxs-lookup"><span data-stu-id="845de-156">Connect via App Service by using the deployment options for that repo.</span></span>
*   <span data-ttu-id="845de-157">使用 Team Foundation 版本控制 (TFVC) 專案。</span><span class="sxs-lookup"><span data-stu-id="845de-157">Use a Team Foundation Version Control (TFVC) project.</span></span> <span data-ttu-id="845de-158">藉由使用 App Service 的組建代理程式來部署。</span><span class="sxs-lookup"><span data-stu-id="845de-158">Deploy by using the build agent for App Service.</span></span>

<span data-ttu-id="845de-159">這兩個選項的持續程式碼部署取決於現有的開發人員工作流程和簽入程序。</span><span class="sxs-lookup"><span data-stu-id="845de-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span></span> <span data-ttu-id="845de-160">如需詳細資訊，請參閱這些文章：</span><span class="sxs-lookup"><span data-stu-id="845de-160">For more information, see these articles:</span></span> 

*   [<span data-ttu-id="845de-161">實作您的應用程式到 Azure 網站的持續部署</span><span class="sxs-lookup"><span data-stu-id="845de-161">Implement continuous deployment of your app to an Azure website</span></span>](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [<span data-ttu-id="845de-162">設定 Visual Studio Team Services 帳戶，讓它可以部署到 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="845de-162">Set up a Visual Studio Team Services account so it can deploy to a web app</span></span>](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-to-deploy-my-app-to-app-service"></a><span data-ttu-id="845de-163">如何使用 FTP 或 FTPS 將我的應用程式部署到 App Service？</span><span class="sxs-lookup"><span data-stu-id="845de-163">How do I use FTP or FTPS to deploy my app to App Service?</span></span>

<span data-ttu-id="845de-164">如需使用 FTP 或 FTPS 將 Web 應用程式部署到 App Service 的詳細資訊，請參閱[使用 FTP/S 將您的應用程式部署到 App Service](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="845de-164">For information about using FTP or FTPS to deploy your web app to App Service, see [Deploy your app to App Service by using FTP/S](app-service-deploy-ftp.md).</span></span>
