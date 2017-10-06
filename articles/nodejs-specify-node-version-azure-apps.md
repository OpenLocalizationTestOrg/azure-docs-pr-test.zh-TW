---
title: "aaaSpecifying Node.js 版本"
description: "了解如何 toospecify hello Node.js 的 Azure 網站和雲端服務所使用的版本"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="8ea42-103">在 Azure 應用程式中指定 Node.js 版本</span><span class="sxs-lookup"><span data-stu-id="8ea42-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="8ea42-104">當裝載 Node.js 應用程式，您可能想 tooensure 應用程式使用特定版本的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="8ea42-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="8ea42-105">有數種方式 tooaccomplish 這在 Azure 上裝載的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ea42-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="8ea42-106">預設版本</span><span class="sxs-lookup"><span data-stu-id="8ea42-106">Default versions</span></span>
<span data-ttu-id="8ea42-107">Azure 提供的 hello Node.js 版本會經常更新。</span><span class="sxs-lookup"><span data-stu-id="8ea42-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="8ea42-108">除非另行指定，hello hello 中所指定的預設版本`WEBSITE_NODE_DEFAULT_VERSION`將使用環境變數。</span><span class="sxs-lookup"><span data-stu-id="8ea42-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="8ea42-109">toooverride 此預設值，遵循本文章的下列各節中的 hello 步驟</span><span class="sxs-lookup"><span data-stu-id="8ea42-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="8ea42-110">如果您要裝載您的應用程式在 Azure 雲端服務 （web 或背景工作角色） 為 hello hello 應用程式部署的第一次，Azure 會嘗試 toouse hello 相同版本的 Node.js，因為您已安裝在開發環境上如果它比對其中一個在 Azure 上可用的 hello 預設版本。</span><span class="sxs-lookup"><span data-stu-id="8ea42-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="8ea42-111">以 package.json 進行版本設定</span><span class="sxs-lookup"><span data-stu-id="8ea42-111">Versioning with package.json</span></span>
<span data-ttu-id="8ea42-112">您可以指定使用新增下列 tooyour hello Node.js toobe hello 版本**package.json**檔案：</span><span class="sxs-lookup"><span data-stu-id="8ea42-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="8ea42-113">其中*版本*是 hello 特定版本號碼 toouse。</span><span class="sxs-lookup"><span data-stu-id="8ea42-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="8ea42-114">您可以針對 version 指定較複雜的條件，例如：</span><span class="sxs-lookup"><span data-stu-id="8ea42-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="8ea42-115">因為 0.6.22 不是其中一個用於裝載環境的 hello hello 版本，hello 最新軟體版本的 hello 0.8 是可用的數列將會改用-0.8.4。</span><span class="sxs-lookup"><span data-stu-id="8ea42-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="8ea42-116">版本控制網站與應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8ea42-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="8ea42-117">如果您裝載在網站中的 hello 應用程式，您可以設定 hello 環境變數**WEBSITE_NODE_DEFAULT_VERSION** toohello 所需的版本。</span><span class="sxs-lookup"><span data-stu-id="8ea42-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="8ea42-118">以 PowerShell 進行雲端服務版本設定</span><span class="sxs-lookup"><span data-stu-id="8ea42-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="8ea42-119">如果您正在裝載在雲端服務中，hello 應用程式，而且部署 hello 應用程式使用 Azure PowerShell，您可以使用覆寫 hello 預設 Node.js 版本 hello**組 AzureServiceProjectRole** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8ea42-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="8ea42-120">例如：</span><span class="sxs-lookup"><span data-stu-id="8ea42-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="8ea42-121">請注意 hello 上述陳述式中的 hello 參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8ea42-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="8ea42-122">您可以確認已選取 hello 正確版本的 Node.js 藉由檢查 hello**引擎**中角色的屬性**package.json**。</span><span class="sxs-lookup"><span data-stu-id="8ea42-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="8ea42-123">您也可以使用 hello **Get AzureServiceProjectRoleRuntime** tooretrieve Node.js 版本適用於裝載的雲端服務的應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="8ea42-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="8ea42-124">一定要驗證 hello Node.js 取決於您的專案版本在此清單中。</span><span class="sxs-lookup"><span data-stu-id="8ea42-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="8ea42-125">對 Azure 網站使用自訂版本</span><span class="sxs-lookup"><span data-stu-id="8ea42-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="8ea42-126">雖然 Azure 提供的 Node.js 的數個預設版本，您可能想 toouse 並非預設提供的版本。</span><span class="sxs-lookup"><span data-stu-id="8ea42-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="8ea42-127">如果您的應用程式裝載為 Azure 網站中，您可以完成這項作業使用 hello **iisnode.yml**檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea42-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="8ea42-128">hello 下列步驟逐步解說使用自訂版本 Node.Js 的 Azure 網站中的 hello 程序：</span><span class="sxs-lookup"><span data-stu-id="8ea42-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="8ea42-129">建立新的目錄，然後再建立**立即轉譯 server.js** hello 目錄內的檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea42-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="8ea42-130">hello**立即轉譯 server.js**檔案應包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8ea42-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="8ea42-131">這會顯示當您瀏覽 hello 網站所使用的 hello Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="8ea42-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="8ea42-132">建立新的網站和附註 hello hello 站台名稱。</span><span class="sxs-lookup"><span data-stu-id="8ea42-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="8ea42-133">例如，hello 下列方式使用 hello [Azure 命令列工具]toocreate 名為新的 Azure 網站**mywebsite**，然後再啟用 hello 網站的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="8ea42-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="8ea42-134">建立新的目錄名稱為**bin**做為子系包含 hello hello 目錄**立即轉譯 server.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea42-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="8ea42-135">下載 hello 特定版本**node.exe** （hello Windows 版本），您會希望 toouse 與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ea42-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="8ea42-136">例如，下列使用 hello **curl** toodownload 版本 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="8ea42-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="8ea42-137">儲存 hello **node.exe**檔案 hello **bin**先前建立的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8ea42-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="8ea42-138">建立**iisnode.yml**相同檔案中 hello 目錄為 hello**立即轉譯 server.js**檔案，然後再加入下列內容 toohello hello **iisnode.yml**檔案：</span><span class="sxs-lookup"><span data-stu-id="8ea42-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="8ea42-139">這個路徑是在 hello **node.exe**一旦發行您的應用程式 toohello Azure 網站中您的專案檔案會位於位置。</span><span class="sxs-lookup"><span data-stu-id="8ea42-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="8ea42-140">發行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ea42-140">Publish your application.</span></span> <span data-ttu-id="8ea42-141">比方說，因為我建立新的網站與 hello-git 參數之前，hello 下列命令會新增 hello 應用程式檔案 toomy 本機 Git 儲存機制，並再將其推送 toohello 網站儲存機制：</span><span class="sxs-lookup"><span data-stu-id="8ea42-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="8ea42-142">Hello 應用程式具有發行之後，請在瀏覽器中開啟 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="8ea42-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="8ea42-143">您應該會看見 "Hello from Azure running node version: v0.8.1" 訊息。</span><span class="sxs-lookup"><span data-stu-id="8ea42-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ea42-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ea42-144">Next Steps</span></span>
<span data-ttu-id="8ea42-145">既然您了解 toospecify hello 版本的 Node.js 應用程式所使用的方式，了解如何太[模組使用]，[建置和部署 Node.js 的網站](app-service-web/app-service-web-get-started-nodejs.md)，和[toouse hello Azure 的方式適用於 Mac 和 Linux 的命令列工具]。</span><span class="sxs-lookup"><span data-stu-id="8ea42-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="8ea42-146">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](https://azure.microsoft.com/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="8ea42-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[toouse hello Azure 的方式適用於 Mac 和 Linux 的命令列工具]:cli-install-nodejs.md
[Azure 命令列工具]:cli-install-nodejs.md
[模組使用]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
