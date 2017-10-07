---
title: "aaaHow toouse io.js 與 Azure App Service Web 應用程式"
description: "深入了解如何 toouse io.js 具有 Azure App Service 中的 web 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="76ced-103">如何使用 Azure App Service Web 應用程式的 toouse io.js</span><span class="sxs-lookup"><span data-stu-id="76ced-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="76ced-104">hello 熱門節點分岔[io.js]各種差異 tooJoyent 的 Node.js 專案，包括多開啟的控管模型、 更快的發行週期和新功能和實驗 JavaScript 功能更快速採用的功能。</span><span class="sxs-lookup"><span data-stu-id="76ced-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="76ced-105">雖然 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 有許多預先安裝的 Node.js 版本，但它也允許使用者提供的 Node.js 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="76ced-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="76ced-106">本文將討論兩個方法可讓 hello io.js App Service Web 應用程式上使用： hello 使用擴充的部署指令碼，它會自動設定 Azure toouse hello 最新可用 io.js 版本，以及 hello io.js 二進位檔手動上的傳。</span><span class="sxs-lookup"><span data-stu-id="76ced-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="76ced-107">使用部署指令碼</span><span class="sxs-lookup"><span data-stu-id="76ced-107">Using a Deployment Script</span></span>
<span data-ttu-id="76ced-108">部署時的 Node.js 應用程式，App Service Web 應用程式執行小型 hello 環境的 tooensure 已正確設定的命令的數目。</span><span class="sxs-lookup"><span data-stu-id="76ced-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="76ced-109">使用部署指令碼，此程序可以是自訂的 tooinclude hello 下載和 io.js 的組態。</span><span class="sxs-lookup"><span data-stu-id="76ced-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="76ced-110">hello [io.js 部署指令碼](https://github.com/felixrieseberg/iojs-azure)可在 GitHub 上取得。</span><span class="sxs-lookup"><span data-stu-id="76ced-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="76ced-111">web 應用程式上的 tooenable io.js 直接複製**.deployment**， **deploy.cmd**和**IISNode.yml** toohello 根應用程式資料夾的 tooWeb 應用程式並部署。</span><span class="sxs-lookup"><span data-stu-id="76ced-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="76ced-112">hello 第一個檔案， **.deployment**，指示 Web 應用程式 toorun **deploy.cmd**一旦部署之後。</span><span class="sxs-lookup"><span data-stu-id="76ced-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="76ced-113">此指令碼執行 Node.js 應用程式的 hello 一般步驟，但也會下載 io.js hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="76ced-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="76ced-114">最後， **IISNode.yml**設定 Web 應用程式 toouse 只是下載的 hello io.js 二進位而不是預先安裝 Node.js 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="76ced-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="76ced-115">tooupdate hello 用於 io.js 二進位檔，只要重新部署應用程式-hello 指令碼會下載新版本的 io.js 每一次 hello 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="76ced-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="76ced-116">使用手動安裝</span><span class="sxs-lookup"><span data-stu-id="76ced-116">Using Manual Installation</span></span>
<span data-ttu-id="76ced-117">hello 手動安裝的自訂 io.js 版本包括只有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="76ced-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="76ced-118">首先，下載 hello **win x64**二進位直接從 hello [io.js 發佈]。</span><span class="sxs-lookup"><span data-stu-id="76ced-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="76ced-119">需要兩個檔案 - **iojs.exe** 和 **iojs.lib**。</span><span class="sxs-lookup"><span data-stu-id="76ced-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="76ced-120">儲存這兩個檔案，tooa 內您 web 應用程式，例如在**bin/iojs**。</span><span class="sxs-lookup"><span data-stu-id="76ced-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="76ced-121">tooconfigure Web 應用程式 toouse **iojs.exe**預先安裝的節點版本，您不必建立**IISNode.yml** hello 根應用程式的檔案，然後加入下列行 hello。</span><span class="sxs-lookup"><span data-stu-id="76ced-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="76ced-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76ced-122">Next Steps</span></span>
<span data-ttu-id="76ced-123">在這篇文章您學會如何使用 App Service Web 應用程式，使用這兩個 toouse io.js 提供部署指令碼，以及在手動安裝。</span><span class="sxs-lookup"><span data-stu-id="76ced-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="76ced-124">io.js 正在密集的開發中，而且比 Node.js 更頻繁地更新。</span><span class="sxs-lookup"><span data-stu-id="76ced-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="76ced-125">許多 Node.js 模組可能不適用於 io.js，請參閱 [GitHub 上的 io.js] 以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="76ced-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="76ced-126">變更的項目</span><span class="sxs-lookup"><span data-stu-id="76ced-126">What's changed</span></span>
* <span data-ttu-id="76ced-127">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="76ced-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="76ced-128">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="76ced-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="76ced-129">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="76ced-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js 發佈]: https://iojs.org/dist/
[GitHub 上的 io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
