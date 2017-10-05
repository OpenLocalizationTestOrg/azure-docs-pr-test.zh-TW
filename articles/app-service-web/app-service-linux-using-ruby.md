---
title: "在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby | Microsoft Docs"
description: "在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby。"
keywords: "azure app service, web 應用程式, 常見問題集, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="c1f6c-104">在 Linux 上的 Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="c1f6c-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="c1f6c-105">在最後更新我們的後端時，我們開始支援 Ruby 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="c1f6c-106">您可以設定 Linux Web 應用程式的組態，以變更應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="c1f6c-107">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c1f6c-107">Using the Azure portal</span></span> ##

<span data-ttu-id="c1f6c-108">從 [Azure 入口網站](https://portal.azure.com)的 [新增] 功能表中，您可以從 [Web + 行動] 選項，選擇在 Linux 上建立 Web 應用程式，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="c1f6c-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![在 Azure 入口網站上開始建立 Web 應用程式][1]

<span data-ttu-id="c1f6c-110">接著會開啟 [建立] 刀鋒視窗，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="c1f6c-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![[建立] 刀鋒視窗][2]

1. <span data-ttu-id="c1f6c-112">命名您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-112">Give your web app a name.</span></span>
2. <span data-ttu-id="c1f6c-113">選擇現有的資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="c1f6c-114">(請參閱[限制](app-service-linux-intro.md)一節中可用的區域。)</span><span class="sxs-lookup"><span data-stu-id="c1f6c-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="c1f6c-115">選擇現有的 Azure App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="c1f6c-116">(請參閱[限制](app-service-linux-intro.md)一節中的 App Service 方案附註。)</span><span class="sxs-lookup"><span data-stu-id="c1f6c-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="c1f6c-117">從內建的執行階段堆疊中選擇 Ruby。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="c1f6c-118">在建立您的 Ruby Web 應用程式之後，您可以使用 Git 或 FTP 來部署。</span><span class="sxs-lookup"><span data-stu-id="c1f6c-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="c1f6c-119">若要深入了解建立 Ruby 應用程式，請參閱[使用者入門指南](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c1f6c-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1f6c-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1f6c-120">Next steps</span></span>
* [<span data-ttu-id="c1f6c-121">什麼是 Linux 上的 Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="c1f6c-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="c1f6c-122">本機 Git 部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c1f6c-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="c1f6c-123">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="c1f6c-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="c1f6c-124">使用 Linux 上的 Azure Web 應用程式建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="c1f6c-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png