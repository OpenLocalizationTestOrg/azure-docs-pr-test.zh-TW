---
title: "如何搭配使用 io.js 和 Azure App Service Web Apps"
description: "了解如何搭配使用 Azure App Service 中的 Web 應用程式和 io.js。"
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="36727-103">如何搭配使用 io.js 和 Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="36727-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="36727-104">受歡迎的 Node 會將 [io.js] 功能的各種差異分散至 Joyent 的 Node.js 專案，包括更開放的控管模型、更快速的發行週期，以及更快速地採用全新和實驗性的 JavaScript 功能。</span><span class="sxs-lookup"><span data-stu-id="36727-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="36727-105">雖然 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 有許多預先安裝的 Node.js 版本，但它也允許使用者提供的 Node.js 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="36727-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="36727-106">本文討論兩種方法可用來啟用 App Service Web Apps 上的 io.js：使用擴充的部署指令碼(其會自動設定 Azure 來使用最新的可用 io.js 版本)，以及手動上傳 io.js 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="36727-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="36727-107">使用部署指令碼</span><span class="sxs-lookup"><span data-stu-id="36727-107">Using a Deployment Script</span></span>
<span data-ttu-id="36727-108">部署 Node.js 應用程式時，App Service Web Apps 會執行一些小型命令，以確保會正確設定環境。</span><span class="sxs-lookup"><span data-stu-id="36727-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="36727-109">使用部署指令碼，可自訂此程序來加入 io.js 的下載和組態。</span><span class="sxs-lookup"><span data-stu-id="36727-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="36727-110">[Io.js 部署指令碼](https://github.com/felixrieseberg/iojs-azure) 可在 GitHub 上取得。</span><span class="sxs-lookup"><span data-stu-id="36727-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="36727-111">若要在 Web 應用程式上啟用 io.js，只要將**.deployment**、**deploy.cmd** 和 **IISNode.yml** 複製到應用程式資料夾的根目錄，以及部署至 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="36727-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="36727-112">第一個檔案 **.deployment** 會在部署時指示 Web Apps 執行 **deploy.cmd**。</span><span class="sxs-lookup"><span data-stu-id="36727-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="36727-113">此指令碼會針對 Node.js 應用程式執行所有一般步驟，但也會下載最新版的 io.js。</span><span class="sxs-lookup"><span data-stu-id="36727-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="36727-114">最後， **IISNode.yml** 會設定 Web Apps 使用剛才下載的 io.js 二進位檔，而不是預先安裝的 Node.js 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="36727-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="36727-115">若要更新使用的 io.js 二進位檔，只要重新部署應用程式即可；每次部署應用程式時，指令碼都會下載新版 io.js。</span><span class="sxs-lookup"><span data-stu-id="36727-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="36727-116">使用手動安裝</span><span class="sxs-lookup"><span data-stu-id="36727-116">Using Manual Installation</span></span>
<span data-ttu-id="36727-117">手動安裝的自訂 io.js 版本只包括兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="36727-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="36727-118">首先，直接從 **io.js 散發** 下載 [win-x64]二進位檔。</span><span class="sxs-lookup"><span data-stu-id="36727-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="36727-119">需要兩個檔案 - **iojs.exe** 和 **iojs.lib**。</span><span class="sxs-lookup"><span data-stu-id="36727-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="36727-120">將這兩個檔案儲存至 Web 應用程式內的資料夾，例如儲存在 **bin/iojs**。</span><span class="sxs-lookup"><span data-stu-id="36727-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="36727-121">若要設定 Web Apps 使用 **iojs.exe**，而不是預先安裝的 Node 版本，請在應用程式的根目錄建立 **IISNode.yml** 檔案並加入下一行。</span><span class="sxs-lookup"><span data-stu-id="36727-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="36727-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36727-122">Next Steps</span></span>
<span data-ttu-id="36727-123">在本文中，您學到如何搭配使用 io.js 與 App Service Web Apps、使用這兩個提供的部署指令碼，以及手動安裝。</span><span class="sxs-lookup"><span data-stu-id="36727-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="36727-124">io.js 正在密集的開發中，而且比 Node.js 更頻繁地更新。</span><span class="sxs-lookup"><span data-stu-id="36727-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="36727-125">許多 Node.js 模組可能不適用於 io.js，請參閱 [GitHub 上的 io.js] 以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="36727-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="36727-126">變更的項目</span><span class="sxs-lookup"><span data-stu-id="36727-126">What's changed</span></span>
* <span data-ttu-id="36727-127">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="36727-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="36727-128">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36727-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="36727-129">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="36727-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="36727-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="36727-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="36727-131">[win-x64]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="36727-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="36727-132">[GitHub 上的 io.js]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="36727-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
