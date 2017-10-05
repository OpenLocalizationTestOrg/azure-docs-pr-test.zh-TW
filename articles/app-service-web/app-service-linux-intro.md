---
title: "Linux 上的 Azure Web 應用程式簡介 | Microsoft Docs"
description: "深入了解 Linux 上的 Azure Web 應用程式。"
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="64536-104">Linux 上的 Azure Web 應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="64536-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="64536-105">概觀</span><span class="sxs-lookup"><span data-stu-id="64536-105">Overview</span></span>
<span data-ttu-id="64536-106">針對支援的應用程式堆疊，客戶可以使用 Linux 上的 Web 應用程式，以原生方式將 Web Apps 裝載於 Linux。</span><span class="sxs-lookup"><span data-stu-id="64536-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="64536-107">下節列出目前支援的應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="64536-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="64536-108">特性</span><span class="sxs-lookup"><span data-stu-id="64536-108">Features</span></span>
<span data-ttu-id="64536-109">Linux 上的 Web 應用程式目前支援下列應用程式堆疊︰</span><span class="sxs-lookup"><span data-stu-id="64536-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="64536-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="64536-110">Node.js</span></span>
    * <span data-ttu-id="64536-111">4.4</span><span class="sxs-lookup"><span data-stu-id="64536-111">4.4</span></span>
    * <span data-ttu-id="64536-112">4.5</span><span class="sxs-lookup"><span data-stu-id="64536-112">4.5</span></span>
    * <span data-ttu-id="64536-113">6.2</span><span class="sxs-lookup"><span data-stu-id="64536-113">6.2</span></span>
    * <span data-ttu-id="64536-114">6.6</span><span class="sxs-lookup"><span data-stu-id="64536-114">6.6</span></span>
    * <span data-ttu-id="64536-115">6.9</span><span class="sxs-lookup"><span data-stu-id="64536-115">6.9</span></span>
    * <span data-ttu-id="64536-116">6.10</span><span class="sxs-lookup"><span data-stu-id="64536-116">6.10</span></span>
    * <span data-ttu-id="64536-117">6.11</span><span class="sxs-lookup"><span data-stu-id="64536-117">6.11</span></span>
    * <span data-ttu-id="64536-118">8.0</span><span class="sxs-lookup"><span data-stu-id="64536-118">8.0</span></span>
    * <span data-ttu-id="64536-119">8.1</span><span class="sxs-lookup"><span data-stu-id="64536-119">8.1</span></span>
* <span data-ttu-id="64536-120">PHP</span><span class="sxs-lookup"><span data-stu-id="64536-120">PHP</span></span>
    * <span data-ttu-id="64536-121">5.6</span><span class="sxs-lookup"><span data-stu-id="64536-121">5.6</span></span>
    * <span data-ttu-id="64536-122">7.0</span><span class="sxs-lookup"><span data-stu-id="64536-122">7.0</span></span>
* <span data-ttu-id="64536-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="64536-123">.Net Core</span></span>
    * <span data-ttu-id="64536-124">1.0</span><span class="sxs-lookup"><span data-stu-id="64536-124">1.0</span></span>
    * <span data-ttu-id="64536-125">1.1</span><span class="sxs-lookup"><span data-stu-id="64536-125">1.1</span></span>
* <span data-ttu-id="64536-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="64536-126">Ruby</span></span>
    * <span data-ttu-id="64536-127">2.3</span><span class="sxs-lookup"><span data-stu-id="64536-127">2.3</span></span>

<span data-ttu-id="64536-128">客戶可以使用下列工具來部署應用程式︰</span><span class="sxs-lookup"><span data-stu-id="64536-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="64536-129">FTP</span><span class="sxs-lookup"><span data-stu-id="64536-129">FTP</span></span>
* <span data-ttu-id="64536-130">本機 Git</span><span class="sxs-lookup"><span data-stu-id="64536-130">Local Git</span></span>
* <span data-ttu-id="64536-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="64536-131">GitHub</span></span>
* <span data-ttu-id="64536-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="64536-132">Bitbucket</span></span>

<span data-ttu-id="64536-133">調整應用程式大小︰</span><span class="sxs-lookup"><span data-stu-id="64536-133">For application scaling:</span></span>

* <span data-ttu-id="64536-134">客戶可以變更 App Service 方案中的階層，即可相應增加和減少 Web 應用程式的規模</span><span class="sxs-lookup"><span data-stu-id="64536-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="64536-135">客戶可以將應用程式相應放大，在其 SKU 的範圍內執行多個應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="64536-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="64536-136">針對 Kudu，有一些基本功能︰</span><span class="sxs-lookup"><span data-stu-id="64536-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="64536-137">環境</span><span class="sxs-lookup"><span data-stu-id="64536-137">Environments</span></span>
* <span data-ttu-id="64536-138">部署</span><span class="sxs-lookup"><span data-stu-id="64536-138">Deployments</span></span>
* <span data-ttu-id="64536-139">基本主控台</span><span class="sxs-lookup"><span data-stu-id="64536-139">Basic console</span></span>
* <span data-ttu-id="64536-140">SSH</span><span class="sxs-lookup"><span data-stu-id="64536-140">SSH</span></span>

<span data-ttu-id="64536-141">針對 DevOps：</span><span class="sxs-lookup"><span data-stu-id="64536-141">For devops:</span></span>

* <span data-ttu-id="64536-142">預備環境</span><span class="sxs-lookup"><span data-stu-id="64536-142">Staging environments</span></span>
* <span data-ttu-id="64536-143">ACR 和 DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="64536-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="64536-144">限制</span><span class="sxs-lookup"><span data-stu-id="64536-144">Limitations</span></span>
<span data-ttu-id="64536-145">Azure 入口網站只會顯示 Linux 上的 Web 應用程式目前可用的功能，並隱藏其餘部分。</span><span class="sxs-lookup"><span data-stu-id="64536-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="64536-146">隨著我們啟用更多功能，您會在入口網站中看到它們。</span><span class="sxs-lookup"><span data-stu-id="64536-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="64536-147">某些功能尚無法使用，例如虛擬網路整合、Azure Active Directory/第三方驗證或 Kudu 網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="64536-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="64536-148">一旦這些功能提供使用後，我們將會在文件和部落格中更新關於變更的消息。</span><span class="sxs-lookup"><span data-stu-id="64536-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="64536-149">目前只在下列區域提供此公開預覽版本：</span><span class="sxs-lookup"><span data-stu-id="64536-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="64536-150">美國西部</span><span class="sxs-lookup"><span data-stu-id="64536-150">West US</span></span>
* <span data-ttu-id="64536-151">美國東部</span><span class="sxs-lookup"><span data-stu-id="64536-151">East US</span></span>
* <span data-ttu-id="64536-152">西歐</span><span class="sxs-lookup"><span data-stu-id="64536-152">West Europe</span></span>
* <span data-ttu-id="64536-153">北歐</span><span class="sxs-lookup"><span data-stu-id="64536-153">North Europe</span></span>
* <span data-ttu-id="64536-154">美國中南部</span><span class="sxs-lookup"><span data-stu-id="64536-154">South Central US</span></span>
* <span data-ttu-id="64536-155">美國中北部</span><span class="sxs-lookup"><span data-stu-id="64536-155">North Central US</span></span>
* <span data-ttu-id="64536-156">東南亞</span><span class="sxs-lookup"><span data-stu-id="64536-156">Southeast Asia</span></span>
* <span data-ttu-id="64536-157">東亞</span><span class="sxs-lookup"><span data-stu-id="64536-157">East Asia</span></span>
* <span data-ttu-id="64536-158">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="64536-158">Australia East</span></span>
* <span data-ttu-id="64536-159">日本東部</span><span class="sxs-lookup"><span data-stu-id="64536-159">Japan East</span></span>
* <span data-ttu-id="64536-160">巴西南部</span><span class="sxs-lookup"><span data-stu-id="64536-160">Brazil South</span></span>
* <span data-ttu-id="64536-161">印度南部</span><span class="sxs-lookup"><span data-stu-id="64536-161">South India</span></span>

<span data-ttu-id="64536-162">Linux 上的 Web Apps 只在「專用」App Service 方案中才支援，而且沒有「免費」或「共用」層。</span><span class="sxs-lookup"><span data-stu-id="64536-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="64536-163">此外，一般和 Linux Web 應用程式的 App Service 方案互斥，因此，您無法在非 Linux App Service 方案中建立 Linux Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64536-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="64536-164">只有同一區域沒有非 Linux Web Apps 的資源群組中，才能建立 Linux 上的 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="64536-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="64536-165">疑難排解</span><span class="sxs-lookup"><span data-stu-id="64536-165">Troubleshooting</span></span> ##

<span data-ttu-id="64536-166">當您的應用程式無法啟動或您想要檢查應用程式的記錄時，請檢查 LogFiles 目錄中的 Docker 記錄。</span><span class="sxs-lookup"><span data-stu-id="64536-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="64536-167">您可以透過 SCM 網站或 FTP 來存取此目錄。</span><span class="sxs-lookup"><span data-stu-id="64536-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="64536-168">若要從您的容器記錄 `stdout` 和 `stderr`，您必須啟用 [診斷記錄] 下的 [Docker 容器記錄]。</span><span class="sxs-lookup"><span data-stu-id="64536-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![啟用記錄][2]

![Using Kudu to view Docker logs][1]

<span data-ttu-id="64536-171">您可以在 [開發工具] 功能表中從 [進階工具] 存取 SCM 網站。</span><span class="sxs-lookup"><span data-stu-id="64536-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64536-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64536-172">Next steps</span></span>
<span data-ttu-id="64536-173">請參閱下列連結以開始使用 Linux 上的 App Service。</span><span class="sxs-lookup"><span data-stu-id="64536-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="64536-174">您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。</span><span class="sxs-lookup"><span data-stu-id="64536-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="64536-175">如何針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="64536-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="64536-176">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="64536-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="64536-177">在 Linux 上的 Azure App Service Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="64536-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="64536-178">在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="64536-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="64536-179">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="64536-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="64536-180">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="64536-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="64536-181">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="64536-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="64536-182">在 Linux 上使用 Azure Web 應用程式連續部署 Docker 中樞</span><span class="sxs-lookup"><span data-stu-id="64536-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png