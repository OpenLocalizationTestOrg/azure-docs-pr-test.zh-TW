---
title: "aaaNode.js 入門指南 |Microsoft 文件"
description: "了解如何 toocreate 簡單 Node.js web 應用程式，並將其部署 tooan Azure 雲端服務。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="d07f7-103">建置和部署 Node.js 應用程式 tooan Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="d07f7-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="d07f7-104">本教學課程示範如何 toocreate 簡單 Node.js 的 Azure 雲端服務中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d07f7-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="d07f7-105">雲端服務是可擴充的雲端應用程式在 Azure 中的 hello 建置組塊。</span><span class="sxs-lookup"><span data-stu-id="d07f7-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="d07f7-106">它們允許 hello 分開獨立管理和向外延展應用程式的前端和後端元件。</span><span class="sxs-lookup"><span data-stu-id="d07f7-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="d07f7-107">雲端服務提供穩定代管各個角色的強固專用虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d07f7-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="d07f7-108">如需有關雲端服務和如何比較 tooAzure 網站和虛擬機器的詳細資訊，請參閱[Azure 網站、 雲端服務和虛擬機器的比較]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="d07f7-109">要尋找 toobuild 簡單網站嗎？</span><span class="sxs-lookup"><span data-stu-id="d07f7-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="d07f7-110">如果您只需要簡單的網站前端，請考慮[使用輕量型 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="d07f7-111">當您 web 應用程式成長並變更您的需求，您可以輕鬆地升級 tooa 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d07f7-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="d07f7-112">按照本教學課程進行，您將建立在 Web 角色內代管的簡單 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d07f7-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="d07f7-113">您將會在本機上，使用 hello 計算模擬器 tootest 您的應用程式，然後部署使用 PowerShell 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="d07f7-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="d07f7-114">hello 應用程式是一個簡單的"hello world"應用程式：</span><span class="sxs-lookup"><span data-stu-id="d07f7-114">hello application is a simple "hello world" application:</span></span>

![網頁瀏覽器顯示 hello Hello World 網頁][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="d07f7-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="d07f7-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="d07f7-117">本教學課程使用 Azure PowerShell (需要 Windows)。</span><span class="sxs-lookup"><span data-stu-id="d07f7-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="d07f7-118">安裝並設定 [Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="d07f7-119">下載並安裝 hello [Azure SDK for.NET 2.7]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="d07f7-120">在 hello 安裝安裝程式中，選取：</span><span class="sxs-lookup"><span data-stu-id="d07f7-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="d07f7-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="d07f7-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="d07f7-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="d07f7-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="d07f7-123">建立 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="d07f7-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="d07f7-124">執行下列工作 toocreate 新的 Azure 雲端服務專案，以及基本 Node.js scaffolding hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="d07f7-125">執行**Windows PowerShell**以系統管理員身分; 從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="d07f7-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="d07f7-126">[連接 PowerShell] tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d07f7-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="d07f7-127">輸入下列 PowerShell cmdlet toocreate toocreate hello 專案 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![hello hello 新 AzureService helloworld 命令結果][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="d07f7-129">hello**新增 AzureServiceProject** cmdlet 會產生用於發佈 Node.js 應用程式 tooa 雲端服務的基本結構。</span><span class="sxs-lookup"><span data-stu-id="d07f7-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="d07f7-130">它包含發行 tooAzure 所需的設定檔。</span><span class="sxs-lookup"><span data-stu-id="d07f7-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="d07f7-131">hello cmdlet 也會變更您的工作目錄 toohello 目錄 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d07f7-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="d07f7-132">hello cmdlet 會建立下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="d07f7-133">**ServiceConfiguration.Cloud.cscfg**、**ServiceConfiguration.Local.cscfg** 和 **ServiceDefinition.csdef**：是發佈應用程式時需使用的 Azure 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="d07f7-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="d07f7-134">如需詳細資訊，請參閱 [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="d07f7-135">**deploymentSettings.json**： 儲存 hello Azure PowerShell 部署 cmdlet 所使用的本機設定。</span><span class="sxs-lookup"><span data-stu-id="d07f7-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="d07f7-136">輸入下列命令 tooadd 新的 web 角色的 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![hello 新增 AzureNodeWebRole 命令 hello 輸出][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="d07f7-138">hello**新增 AzureNodeWebRole** cmdlet 會建立基本的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d07f7-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="d07f7-139">它也會修改 hello **.csfg**和**.csdef**檔案 tooadd hello 新角色的組態項目。</span><span class="sxs-lookup"><span data-stu-id="d07f7-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d07f7-140">如果您未指定角色名稱，系統會使用預設名稱。</span><span class="sxs-lookup"><span data-stu-id="d07f7-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="d07f7-141">您可以提供名稱做為第一個指令程式參數 hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="d07f7-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="d07f7-142">hello 檔案中定義 hello Node.js 應用程式**立即轉譯 server.js**hello web 角色的 hello 目錄中 (**WebRole1**依預設)。</span><span class="sxs-lookup"><span data-stu-id="d07f7-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="d07f7-143">Hello 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="d07f7-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="d07f7-144">此程式碼為基本上相同 hello"Hello World"範例 hello 的 hello [nodejs.org]網站，但它會使用指派的 hello 雲端環境的 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="d07f7-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="d07f7-145">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d07f7-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="d07f7-146">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d07f7-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d07f7-147">您可以[啟用自己的 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)或是[註冊免費帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)。</span><span class="sxs-lookup"><span data-stu-id="d07f7-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="d07f7-148">下載 hello Azure 發行設定</span><span class="sxs-lookup"><span data-stu-id="d07f7-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="d07f7-149">toodeploy 您的應用程式 tooAzure，您必須先下載 hello 發行您的 Azure 訂用帳戶的設定。</span><span class="sxs-lookup"><span data-stu-id="d07f7-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="d07f7-150">執行下列 Azure PowerShell cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="d07f7-151">此選項會使用您的瀏覽器 toonavigate toohello 發佈設定 下載頁面。</span><span class="sxs-lookup"><span data-stu-id="d07f7-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="d07f7-152">您可以使用 Microsoft 帳戶的提示的 toolog。</span><span class="sxs-lookup"><span data-stu-id="d07f7-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="d07f7-153">如果是，使用與您 Azure 訂用帳戶相關聯的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d07f7-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="d07f7-154">儲存下載的 hello 設定檔 tooa 檔案位置可以輕易地存取。</span><span class="sxs-lookup"><span data-stu-id="d07f7-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="d07f7-155">執行下列 cmdlet tooimport hello 發行您所下載的設定檔：</span><span class="sxs-lookup"><span data-stu-id="d07f7-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="d07f7-156">匯入 hello 後發行設定，請考慮刪除 hello 下載.publishSettings 檔案，因為它包含資訊，可能會允許其他人 tooaccess 您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d07f7-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="d07f7-157">發行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d07f7-157">Publish hello application</span></span>
<span data-ttu-id="d07f7-158">toopublish，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="d07f7-159">**-ServiceName**指定 hello 部署的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d07f7-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="d07f7-160">這必須是唯一的名稱，否則 hello 發佈程序將會失敗。</span><span class="sxs-lookup"><span data-stu-id="d07f7-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="d07f7-161">hello **Get-date**命令 tacks 應該讓 hello 名稱唯一日期/時間字串。</span><span class="sxs-lookup"><span data-stu-id="d07f7-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="d07f7-162">**位置**指定將裝載 hello 應用程式中的 hello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="d07f7-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="d07f7-163">一份可用的資料中心，使用 hello toosee **Get AzureLocation** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d07f7-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="d07f7-164">**-啟動**開啟瀏覽器視窗，並完成部署之後，請瀏覽 toohello 裝載服務。</span><span class="sxs-lookup"><span data-stu-id="d07f7-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="d07f7-165">發行成功之後，您會看到類似 toohello 後的回應：</span><span class="sxs-lookup"><span data-stu-id="d07f7-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![hello Publish-azureservice 命令 hello 輸出][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="d07f7-167">它可以使用 hello 應用程式 toodeploy 幾分鐘的時間，並變成可用時第一次發行。</span><span class="sxs-lookup"><span data-stu-id="d07f7-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="d07f7-168">Hello 部署完成後，請在瀏覽器視窗會開啟，並瀏覽 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d07f7-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![瀏覽器視窗，以顯示 hello hello world 網頁。hello URL 表示 hello 頁面裝載於 Azure。][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="d07f7-170">您的應用程式現在成功在 Azure 上執行了！</span><span class="sxs-lookup"><span data-stu-id="d07f7-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="d07f7-171">hello**發行 AzureServiceProject** cmdlet 會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d07f7-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="d07f7-172">建立封裝 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="d07f7-172">Creates a package toodeploy.</span></span> <span data-ttu-id="d07f7-173">hello 套件包含所有應用程式資料夾中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d07f7-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="d07f7-174">建立新的 **儲存體帳戶** (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="d07f7-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="d07f7-175">hello Azure 儲存體帳戶是使用的 toostore hello 應用程式封裝，部署期間。</span><span class="sxs-lookup"><span data-stu-id="d07f7-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="d07f7-176">完成部署之後，您可以放心刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d07f7-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="d07f7-177">建立新的 **雲端服務** (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="d07f7-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="d07f7-178">A**雲端服務**是在其中裝載應用程式時，它已部署的 tooAzure hello 容器。</span><span class="sxs-lookup"><span data-stu-id="d07f7-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="d07f7-179">如需詳細資訊，請參閱 [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="d07f7-180">發行 hello 部署封裝 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d07f7-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="d07f7-181">停止並刪除您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d07f7-181">Stopping and deleting your application</span></span>
<span data-ttu-id="d07f7-182">部署後您的應用程式，您可能會想 toodisable 它如此您就不必付出的額外成本。</span><span class="sxs-lookup"><span data-stu-id="d07f7-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="d07f7-183">Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。</span><span class="sxs-lookup"><span data-stu-id="d07f7-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="d07f7-184">使用伺服器時間為您的應用程式部署之後，即使 hello 執行個體未執行而且處於 hello 停止狀態。</span><span class="sxs-lookup"><span data-stu-id="d07f7-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="d07f7-185">在 hello Windows PowerShell 視窗中，停止以 hello 下列 cmdlet 建立 hello 前一節中的 hello 服務部署：</span><span class="sxs-lookup"><span data-stu-id="d07f7-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="d07f7-186">停止 hello 服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d07f7-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="d07f7-187">Hello 服務停止時，您會收到訊息，指出 已停止。</span><span class="sxs-lookup"><span data-stu-id="d07f7-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![hello hello 停止 AzureService 命令狀態][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="d07f7-189">下列指令程式呼叫 hello toodelete hello 服務：</span><span class="sxs-lookup"><span data-stu-id="d07f7-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="d07f7-190">出現提示時，輸入**Y** toodelete hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d07f7-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="d07f7-191">刪除 hello 服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d07f7-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="d07f7-192">刪除 hello 服務之後您會收到指出 hello 服務已刪除的訊息。</span><span class="sxs-lookup"><span data-stu-id="d07f7-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![hello hello 移除 AzureService 命令狀態][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="d07f7-194">正在刪除 hello 服務不會刪除 hello hello 服務最初發行時所建立的儲存體帳戶，您仍須繼續支付儲存體使用 toobe。</span><span class="sxs-lookup"><span data-stu-id="d07f7-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="d07f7-195">如果沒有其他使用 hello 儲存體，您可能想 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="d07f7-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d07f7-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d07f7-196">Next steps</span></span>
<span data-ttu-id="d07f7-197">如需詳細資訊，請參閱 hello [Node.js 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="d07f7-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[Azure 網站、 雲端服務和虛擬機器的比較]: ../app-service-web/choose-web-site-cloud-service-vm.md
[使用輕量型 Web 應用程式]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK for.NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[連接 PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[雲端服務]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js 開發人員中心]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
