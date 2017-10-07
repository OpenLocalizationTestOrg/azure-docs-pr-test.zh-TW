---
title: "在 Azure App Service Web 應用程式在 Linux 上的 Ruby aaaUsing |Microsoft 文件"
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
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="14f51-104">在 Linux 上的 Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="14f51-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="14f51-105">與最新更新 tooour 後端 hello，我們引進了拼音 v.2.3 的支援。</span><span class="sxs-lookup"><span data-stu-id="14f51-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="14f51-106">Linux 的 web 應用程式設定 hello 組態，您可以變更 hello 應用程式堆疊。</span><span class="sxs-lookup"><span data-stu-id="14f51-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="14f51-107">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="14f51-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="14f51-108">從在 hello hello 新功能表[Azure 入口網站](https://portal.azure.com)，您可以選擇 toocreate Linux 上的 Web 應用程式從 hello Web + 行動電話選項 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="14f51-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![開始在 hello Azure 入口網站上建立 web 應用程式][1]

<span data-ttu-id="14f51-110">接下來，hello**刀鋒視窗中建立**會開啟 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="14f51-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![刀鋒視窗中建立 hello][2]

1. <span data-ttu-id="14f51-112">命名您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14f51-112">Give your web app a name.</span></span>
2. <span data-ttu-id="14f51-113">選擇現有的資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="14f51-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="14f51-114">(請參閱 hello 中的可用區域[限制 > 一節](app-service-linux-intro.md)。)</span><span class="sxs-lookup"><span data-stu-id="14f51-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="14f51-115">選擇現有的 Azure App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="14f51-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="14f51-116">(請參閱應用程式服務計劃在 hello[限制 > 一節](app-service-linux-intro.md)。)</span><span class="sxs-lookup"><span data-stu-id="14f51-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="14f51-117">選擇 hello Ruby hello 內建的執行階段堆疊。</span><span class="sxs-lookup"><span data-stu-id="14f51-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="14f51-118">取得建立拼音 web 應用程式之後，您可以部署 tooit 使用 Git 或 FTP。</span><span class="sxs-lookup"><span data-stu-id="14f51-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="14f51-119">深入了解 toolearn 建立 Ruby 應用程式，請檢查 hello [get 指南](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="14f51-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="14f51-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14f51-120">Next steps</span></span>
* [<span data-ttu-id="14f51-121">什麼是 Linux 上的 Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="14f51-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="14f51-122">本機 Git 部署 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="14f51-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="14f51-123">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="14f51-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="14f51-124">使用 Linux 上的 Azure Web 應用程式建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="14f51-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png