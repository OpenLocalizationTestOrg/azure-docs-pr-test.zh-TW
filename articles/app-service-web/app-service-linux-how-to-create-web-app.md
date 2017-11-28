---
title: "aaaCreate Azure web 應用程式在 Linux 上執行 |Microsoft 文件"
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="8a905-104">建立在 Linux 上執行的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a905-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="8a905-105">使用 Azure 入口網站 toocreate hello 您 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a905-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="8a905-106">您可以開始在 Linux 上建立 web 應用程式，從 hello [Azure 入口網站](https://portal.azure.com)hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="8a905-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![開始在 hello Azure 入口網站上建立 web 應用程式][1]

<span data-ttu-id="8a905-108">接下來，hello**刀鋒視窗中建立**會開啟 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="8a905-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![刀鋒視窗中建立 hello][2]

1. <span data-ttu-id="8a905-110">命名您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a905-110">Give your web app a name.</span></span>
2. <span data-ttu-id="8a905-111">選擇現有的資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="8a905-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="8a905-112">(請參閱 hello 中的可用區域[限制 > 一節](app-service-linux-intro.md)。)</span><span class="sxs-lookup"><span data-stu-id="8a905-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="8a905-113">選擇現有的 Azure App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="8a905-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="8a905-114">(請參閱應用程式服務計劃在 hello[限制 > 一節](app-service-linux-intro.md)。)</span><span class="sxs-lookup"><span data-stu-id="8a905-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="8a905-115">選擇 hello 應用程式，您還要 toouse 堆疊。</span><span class="sxs-lookup"><span data-stu-id="8a905-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="8a905-116">您可以從 Node.js、PHP、.Net Core、 Ruby 數種版本中選擇。</span><span class="sxs-lookup"><span data-stu-id="8a905-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="8a905-117">當您建立 hello 應用程式之後時，您可以變更 hello 應用程式堆疊 hello 應用程式設定 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="8a905-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![應用程式設定][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="8a905-119">部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8a905-119">Deploy your web app</span></span>
<span data-ttu-id="8a905-120">選擇**部署選項**從 hello management 入口網站可讓您 hello 選項 toouse 本機 Git 或 GitHub 儲存機制 toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a905-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="8a905-121">hello 指示 hello 其餘部分是類似 toothose，非 Linux web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a905-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="8a905-122">您可以依照中的 hello 指示[本機 Git 部署](app-service-deploy-local-git.md)或[連續部署](app-service-continuous-deployment.md)toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a905-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="8a905-123">您也可以使用 FTP tooupload 應用程式的 tooyour 站台。</span><span class="sxs-lookup"><span data-stu-id="8a905-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="8a905-124">您可以取得 hello FTP 端點 web 應用程式從 hello 診斷記錄 區段中 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="8a905-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![診斷記錄檔][4]

## <a name="next-steps"></a><span data-ttu-id="8a905-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a905-126">Next steps</span></span>
* [<span data-ttu-id="8a905-127">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="8a905-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="8a905-128">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="8a905-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="8a905-129">在 Linux 上的 Azure App Service Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="8a905-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="8a905-130">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="8a905-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
