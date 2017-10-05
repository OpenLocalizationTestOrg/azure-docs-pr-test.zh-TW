---
title: "建立在 Linux 上執行的 Azure Web 應用程式 | Microsoft Docs"
description: "針對 Linux 上的 Azure Web 應用程式建立 Web 應用程式工作流程。"
keywords: "azure app service, web 應用程式, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="3f827-104">建立在 Linux 上執行的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f827-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="3f827-105">使用 Azure 入口網站建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f827-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="3f827-106">您可以從 [Azure 入口網站](https://portal.azure.com)開始建立 Linux 上的 Web 應用程式，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="3f827-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![在 Azure 入口網站上開始建立 Web 應用程式][1]

<span data-ttu-id="3f827-108">接著會開啟 [建立] 刀鋒視窗，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="3f827-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![[建立] 刀鋒視窗][2]

1. <span data-ttu-id="3f827-110">命名您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f827-110">Give your web app a name.</span></span>
2. <span data-ttu-id="3f827-111">選擇現有的資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="3f827-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="3f827-112">(請參閱[限制](app-service-linux-intro.md)一節中可用的區域。)</span><span class="sxs-lookup"><span data-stu-id="3f827-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="3f827-113">選擇現有的 Azure App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="3f827-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="3f827-114">(請參閱[限制](app-service-linux-intro.md)一節中的 App Service 方案附註。)</span><span class="sxs-lookup"><span data-stu-id="3f827-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="3f827-115">選擇您想要使用的應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="3f827-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="3f827-116">您可以從 Node.js、PHP、.Net Core、 Ruby 數種版本中選擇。</span><span class="sxs-lookup"><span data-stu-id="3f827-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="3f827-117">建立應用程式後，您可以從應用程式設定中變更應用程式堆疊，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="3f827-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![應用程式設定][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="3f827-119">部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f827-119">Deploy your web app</span></span>
<span data-ttu-id="3f827-120">從管理入口網站中選擇 [部署選項] 時，您可以選擇使用本機 Git 或 GitHub 存放庫來部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f827-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="3f827-121">其餘的指示類似非 Linux Web 應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="3f827-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="3f827-122">您可以依照[本機 Git 部署](app-service-deploy-local-git.md)或[連續部署](app-service-continuous-deployment.md)中的指示部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f827-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="3f827-123">您也可以使用 FTP 將應用程式上傳至您的網站。</span><span class="sxs-lookup"><span data-stu-id="3f827-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="3f827-124">您可以從 [診斷記錄檔] 區段取得 Web 應用程式的 FTP 端點，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="3f827-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![診斷記錄檔][4]

## <a name="next-steps"></a><span data-ttu-id="3f827-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f827-126">Next steps</span></span>
* [<span data-ttu-id="3f827-127">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="3f827-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="3f827-128">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="3f827-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="3f827-129">在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="3f827-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="3f827-130">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="3f827-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
