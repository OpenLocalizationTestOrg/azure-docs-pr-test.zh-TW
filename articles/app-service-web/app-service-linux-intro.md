---
title: "aaaIntroduction tooAzure Linux 上的 Web 應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="53c30-104">簡介 tooAzure Linux 上的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="53c30-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="53c30-105">概觀</span><span class="sxs-lookup"><span data-stu-id="53c30-105">Overview</span></span>
<span data-ttu-id="53c30-106">客戶可以使用 Web 應用程式原生 Linux 上的 Linux toohost web 應用程式支援的應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="53c30-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="53c30-107">hello 下節列出 hello 目前支援的應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="53c30-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="53c30-108">特性</span><span class="sxs-lookup"><span data-stu-id="53c30-108">Features</span></span>
<span data-ttu-id="53c30-109">Web 應用程式，在 Linux 上目前支援下列應用程式堆疊的 hello:</span><span class="sxs-lookup"><span data-stu-id="53c30-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="53c30-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="53c30-110">Node.js</span></span>
    * <span data-ttu-id="53c30-111">4.4</span><span class="sxs-lookup"><span data-stu-id="53c30-111">4.4</span></span>
    * <span data-ttu-id="53c30-112">4.5</span><span class="sxs-lookup"><span data-stu-id="53c30-112">4.5</span></span>
    * <span data-ttu-id="53c30-113">6.2</span><span class="sxs-lookup"><span data-stu-id="53c30-113">6.2</span></span>
    * <span data-ttu-id="53c30-114">6.6</span><span class="sxs-lookup"><span data-stu-id="53c30-114">6.6</span></span>
    * <span data-ttu-id="53c30-115">6.9</span><span class="sxs-lookup"><span data-stu-id="53c30-115">6.9</span></span>
    * <span data-ttu-id="53c30-116">6.10</span><span class="sxs-lookup"><span data-stu-id="53c30-116">6.10</span></span>
    * <span data-ttu-id="53c30-117">6.11</span><span class="sxs-lookup"><span data-stu-id="53c30-117">6.11</span></span>
    * <span data-ttu-id="53c30-118">8.0</span><span class="sxs-lookup"><span data-stu-id="53c30-118">8.0</span></span>
    * <span data-ttu-id="53c30-119">8.1</span><span class="sxs-lookup"><span data-stu-id="53c30-119">8.1</span></span>
* <span data-ttu-id="53c30-120">PHP</span><span class="sxs-lookup"><span data-stu-id="53c30-120">PHP</span></span>
    * <span data-ttu-id="53c30-121">5.6</span><span class="sxs-lookup"><span data-stu-id="53c30-121">5.6</span></span>
    * <span data-ttu-id="53c30-122">7.0</span><span class="sxs-lookup"><span data-stu-id="53c30-122">7.0</span></span>
* <span data-ttu-id="53c30-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="53c30-123">.Net Core</span></span>
    * <span data-ttu-id="53c30-124">1.0</span><span class="sxs-lookup"><span data-stu-id="53c30-124">1.0</span></span>
    * <span data-ttu-id="53c30-125">1.1</span><span class="sxs-lookup"><span data-stu-id="53c30-125">1.1</span></span>
* <span data-ttu-id="53c30-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="53c30-126">Ruby</span></span>
    * <span data-ttu-id="53c30-127">2.3</span><span class="sxs-lookup"><span data-stu-id="53c30-127">2.3</span></span>

<span data-ttu-id="53c30-128">客戶可以使用下列工具來部署應用程式︰</span><span class="sxs-lookup"><span data-stu-id="53c30-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="53c30-129">FTP</span><span class="sxs-lookup"><span data-stu-id="53c30-129">FTP</span></span>
* <span data-ttu-id="53c30-130">本機 Git</span><span class="sxs-lookup"><span data-stu-id="53c30-130">Local Git</span></span>
* <span data-ttu-id="53c30-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="53c30-131">GitHub</span></span>
* <span data-ttu-id="53c30-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="53c30-132">Bitbucket</span></span>

<span data-ttu-id="53c30-133">調整應用程式大小︰</span><span class="sxs-lookup"><span data-stu-id="53c30-133">For application scaling:</span></span>

* <span data-ttu-id="53c30-134">客戶可以向上和向下調整 web 應用程式，藉由變更其 App Service 方案的 hello 層</span><span class="sxs-lookup"><span data-stu-id="53c30-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="53c30-135">客戶可以擴充應用程式及執行多個應用程式的執行個體 hello 範圍內的 SKU</span><span class="sxs-lookup"><span data-stu-id="53c30-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="53c30-136">如 Kudu hello 基本功能：</span><span class="sxs-lookup"><span data-stu-id="53c30-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="53c30-137">環境</span><span class="sxs-lookup"><span data-stu-id="53c30-137">Environments</span></span>
* <span data-ttu-id="53c30-138">部署</span><span class="sxs-lookup"><span data-stu-id="53c30-138">Deployments</span></span>
* <span data-ttu-id="53c30-139">基本主控台</span><span class="sxs-lookup"><span data-stu-id="53c30-139">Basic console</span></span>
* <span data-ttu-id="53c30-140">SSH</span><span class="sxs-lookup"><span data-stu-id="53c30-140">SSH</span></span>

<span data-ttu-id="53c30-141">針對 DevOps：</span><span class="sxs-lookup"><span data-stu-id="53c30-141">For devops:</span></span>

* <span data-ttu-id="53c30-142">預備環境</span><span class="sxs-lookup"><span data-stu-id="53c30-142">Staging environments</span></span>
* <span data-ttu-id="53c30-143">ACR 和 DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="53c30-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="53c30-144">限制</span><span class="sxs-lookup"><span data-stu-id="53c30-144">Limitations</span></span>
<span data-ttu-id="53c30-145">hello Azure 入口網站會顯示目前在 Linux 上的 Web 應用程式適用的唯一功能，並隱藏 hello rest。</span><span class="sxs-lookup"><span data-stu-id="53c30-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="53c30-146">因為我們啟用更多的功能，就會看見 hello 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="53c30-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="53c30-147">某些功能尚無法使用，例如虛擬網路整合、Azure Active Directory/第三方驗證或 Kudu 網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="53c30-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="53c30-148">一旦這些功能可供使用，我們將會更新我們的文件和部落格有關 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="53c30-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="53c30-149">這個公用預覽了目前僅限用於 hello 下列區域：</span><span class="sxs-lookup"><span data-stu-id="53c30-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="53c30-150">美國西部</span><span class="sxs-lookup"><span data-stu-id="53c30-150">West US</span></span>
* <span data-ttu-id="53c30-151">美國東部</span><span class="sxs-lookup"><span data-stu-id="53c30-151">East US</span></span>
* <span data-ttu-id="53c30-152">西歐</span><span class="sxs-lookup"><span data-stu-id="53c30-152">West Europe</span></span>
* <span data-ttu-id="53c30-153">北歐</span><span class="sxs-lookup"><span data-stu-id="53c30-153">North Europe</span></span>
* <span data-ttu-id="53c30-154">美國中南部</span><span class="sxs-lookup"><span data-stu-id="53c30-154">South Central US</span></span>
* <span data-ttu-id="53c30-155">美國中北部</span><span class="sxs-lookup"><span data-stu-id="53c30-155">North Central US</span></span>
* <span data-ttu-id="53c30-156">東南亞</span><span class="sxs-lookup"><span data-stu-id="53c30-156">Southeast Asia</span></span>
* <span data-ttu-id="53c30-157">東亞</span><span class="sxs-lookup"><span data-stu-id="53c30-157">East Asia</span></span>
* <span data-ttu-id="53c30-158">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="53c30-158">Australia East</span></span>
* <span data-ttu-id="53c30-159">日本東部</span><span class="sxs-lookup"><span data-stu-id="53c30-159">Japan East</span></span>
* <span data-ttu-id="53c30-160">巴西南部</span><span class="sxs-lookup"><span data-stu-id="53c30-160">Brazil South</span></span>
* <span data-ttu-id="53c30-161">印度南部</span><span class="sxs-lookup"><span data-stu-id="53c30-161">South India</span></span>

<span data-ttu-id="53c30-162">Web 應用程式，在 Linux 上 hello 專用的 app service 方案中才支援，而且沒有免費或共用層。</span><span class="sxs-lookup"><span data-stu-id="53c30-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="53c30-163">此外，一般和 Linux Web 應用程式的 App Service 方案互斥，因此，您無法在非 Linux App Service 方案中建立 Linux Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53c30-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="53c30-164">Web 應用程式，在 Linux 上必須建立資源群組不包含非 Linux hello 的 web 應用程式中相同的區域。</span><span class="sxs-lookup"><span data-stu-id="53c30-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="53c30-165">疑難排解</span><span class="sxs-lookup"><span data-stu-id="53c30-165">Troubleshooting</span></span> ##

<span data-ttu-id="53c30-166">當您的應用程式失敗 toostart 或您想 toocheck hello 記錄從您的應用程式時，請檢查的 hello Docker 記錄 hello LogFiles 目錄中。</span><span class="sxs-lookup"><span data-stu-id="53c30-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="53c30-167">您可以透過 SCM 網站或 FTP 來存取此目錄。</span><span class="sxs-lookup"><span data-stu-id="53c30-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="53c30-168">toolog hello`stdout`和`stderr`從您的容器，您需要 tooenable **Docker 容器記錄**下**診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="53c30-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![啟用記錄][2]

![使用 Kudu tooview Docker 記錄檔][1]

<span data-ttu-id="53c30-171">您可以存取 hello SCM 站台從**進階工具**在 hello**開發工具**功能表。</span><span class="sxs-lookup"><span data-stu-id="53c30-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53c30-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53c30-172">Next steps</span></span>
<span data-ttu-id="53c30-173">請參閱下列連結 tooget 開始使用 Linux 上的應用程式服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="53c30-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="53c30-174">您可以在[我們的論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)張貼問題和疑難。</span><span class="sxs-lookup"><span data-stu-id="53c30-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="53c30-175">Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像</span><span class="sxs-lookup"><span data-stu-id="53c30-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="53c30-176">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="53c30-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="53c30-177">在 Linux 上的 Azure App Service Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="53c30-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="53c30-178">在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="53c30-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="53c30-179">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="53c30-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="53c30-180">Linux 上的 Azure Web 應用程式 SSH 支援</span><span class="sxs-lookup"><span data-stu-id="53c30-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="53c30-181">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="53c30-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="53c30-182">在 Linux 上使用 Azure Web 應用程式連續部署 Docker 中樞</span><span class="sxs-lookup"><span data-stu-id="53c30-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png