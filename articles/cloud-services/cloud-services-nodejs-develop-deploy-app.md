---
title: "Node.js 入門指南 | Microsoft Docs"
description: "了解如何建立簡單的 Node.js Web 應用程式，並將它部署至 Azure 雲端服務。"
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="2ddcc-103">建立 Node.js 應用程式並部署到 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="2ddcc-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="2ddcc-104">本教學課程示範如何建立在 Azure 雲端服務中執行的簡單 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="2ddcc-105">雲端服務是 Azure 中可擴充雲端應用程式的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="2ddcc-106">可以個別獨立管理和向外延展應用程式的前端和後端元件。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="2ddcc-107">雲端服務提供穩定代管各個角色的強固專用虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="2ddcc-108">如需雲端服務及其相較於 Azure 網站和虛擬機器的詳細資訊，請參閱 [Azure 網站、雲端服務與虛擬機器的比較]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="2ddcc-109">尋求建置簡單的網站？</span><span class="sxs-lookup"><span data-stu-id="2ddcc-109">Looking to build a simple website?</span></span> <span data-ttu-id="2ddcc-110">如果您只需要簡單的網站前端，請考慮[使用輕量型 Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="2ddcc-111">隨著 Web 應用程式擴大以及需求改變，您可以輕易地升級到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="2ddcc-112">按照本教學課程進行，您將建立在 Web 角色內代管的簡單 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="2ddcc-113">您將使用計算模擬器在本機測試您的應用程式，然後使用 PowerShell 命令列工具部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="2ddcc-114">應用程式是簡單的 "hello world" 應用程式：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-114">The application is a simple "hello world" application:</span></span>

![顯示 Hello World 網頁的網頁瀏覽器][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="2ddcc-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ddcc-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="2ddcc-117">本教學課程使用 Azure PowerShell (需要 Windows)。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="2ddcc-118">安裝並設定 [Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="2ddcc-119">下載並安裝 [Azure SDK for .NET 2.7]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="2ddcc-120">在安裝過程中，選取：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-120">In the install setup, select:</span></span>
  * <span data-ttu-id="2ddcc-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="2ddcc-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="2ddcc-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="2ddcc-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="2ddcc-123">建立 Azure 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="2ddcc-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="2ddcc-124">執行下列工作，建立新的 Azure 雲端服務專案以及基本的 Node.js 樣板：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="2ddcc-125">以系統管理員身分執行 **Windows PowerShell**；從 [開始功能表] 或 [開始畫面] 中，搜尋 [Windows PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="2ddcc-126">[連線 PowerShell] 至您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="2ddcc-127">輸入下列 PowerShell Cmdlet 來建立專案：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![New-AzureService helloworld 命令的結果][The result of the New-AzureService helloworld command]

    <span data-ttu-id="2ddcc-129">**New-AzureServiceProject** Cmdlet 會產生可將 Node.js 應用程式發佈至雲端服務的基本結構。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="2ddcc-130">其中包含發佈到 Azure 所需的設定檔。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="2ddcc-131">該 Cmdlet 也會將您的工作目錄變更為服務的目錄。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="2ddcc-132">Cmdlet 會建立下列檔案：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="2ddcc-133">**ServiceConfiguration.Cloud.cscfg**、**ServiceConfiguration.Local.cscfg** 和 **ServiceDefinition.csdef**：是發佈應用程式時需使用的 Azure 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="2ddcc-134">如需詳細資訊，請參閱 [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="2ddcc-135">**deploymentSettings.json**：儲存 Azure PowerShell 部署 Cmdlet 使用的本機設定。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="2ddcc-136">輸入下列命令以新增 Web 角色：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Add-AzureNodeWebRole 命令的輸出][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="2ddcc-138">**Add-AzureNodeWebRole** Cmdlet 可建立基本的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="2ddcc-139">也可修改 **.csfg** 和 **.csdef** 檔案，以新增新角色的組態項目。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ddcc-140">如果您未指定角色名稱，系統會使用預設名稱。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="2ddcc-141">您可以提供一個名稱做為第一個 Cmdlet 參數： `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="2ddcc-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="2ddcc-142">Node.js app 是在 **server.js** 檔案中定義，該檔案位於 Web 角色 (預設為 **WebRole1**) 的目錄中。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="2ddcc-143">程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="2ddcc-144">此程式碼基本上和 [nodejs.org] 網站上的「Hello World」範例一樣，但它使用雲端環境指派的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="2ddcc-145">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="2ddcc-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="2ddcc-146">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2ddcc-147">您可以[啟用自己的 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)或是[註冊免費帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="2ddcc-148">下載 Azure 發佈設定</span><span class="sxs-lookup"><span data-stu-id="2ddcc-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="2ddcc-149">若要將應用程式部署到 Azure，您必須先下載您 Azure 訂閱的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="2ddcc-150">執行下列 Azure PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="2ddcc-151">這將使用瀏覽器瀏覽到發佈設定下載頁面。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="2ddcc-152">可能提示您使用 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="2ddcc-153">若是如此，請使用與您的 Azure 訂閱相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="2ddcc-154">將下載的設定檔儲存到您可以輕鬆存取的檔案位置。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="2ddcc-155">執行下列 Cmdlet 來匯入您所下載的發佈設定檔：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="2ddcc-156">在匯入發佈設定之後，請考慮刪除下載的 .publishSettings 檔案，因為它包含了可能讓他人存取您帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="2ddcc-157">發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="2ddcc-157">Publish the application</span></span>
<span data-ttu-id="2ddcc-158">若要發佈，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="2ddcc-159">**-ServiceName** 指定部署的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="2ddcc-160">這必須是唯一名稱，否則發佈程序將失敗。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="2ddcc-161">**Get-Date** 命令會添加到應該讓名稱唯一的日期/時間字串。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="2ddcc-162">**-Location** 指定託管應用程式的資料中心。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="2ddcc-163">若要查看可用資料中心的清單，請使用 **Get-AzureLocation** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="2ddcc-164">**-Launch** 可在部署完成後，開啟瀏覽器視窗並瀏覽至託管服務。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="2ddcc-165">發佈成功後，您將看見如下的回應：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![Publish-AzureService 命令的輸出][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="2ddcc-167">第一次發佈應用程式時，從部署到可以使用需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="2ddcc-168">部署完成後，瀏覽器視窗將開啟，並瀏覽到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![顯示 hello world 頁面的瀏覽器視窗；URL 會指出此頁面裝載在 Azure 上。][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="2ddcc-170">您的應用程式現在成功在 Azure 上執行了！</span><span class="sxs-lookup"><span data-stu-id="2ddcc-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="2ddcc-171">**Publish-AzureServiceProject** Cmdlet 將執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="2ddcc-172">建立部署的封裝。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-172">Creates a package to deploy.</span></span> <span data-ttu-id="2ddcc-173">該封裝包含 node.js 應用程式資料夾中所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="2ddcc-174">建立新的 **儲存體帳戶** (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="2ddcc-175">Azure 儲存體帳戶將用來在部署期間儲存應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="2ddcc-176">部署完成後，即可安全刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="2ddcc-177">建立新的 **雲端服務** (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="2ddcc-178">**雲端服務** 是應用程式部署到 Azure 時代管應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="2ddcc-179">如需詳細資訊，請參閱 [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="2ddcc-180">將部署封裝發佈到 Azure。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="2ddcc-181">停止並刪除您的應用程式</span><span class="sxs-lookup"><span data-stu-id="2ddcc-181">Stopping and deleting your application</span></span>
<span data-ttu-id="2ddcc-182">部署您的應用程式後，您可能會想要將它停用，以便避免額外的成本。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="2ddcc-183">Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="2ddcc-184">部署應用程式之後，即使執行個體未執行而在停止狀態中，也會使用伺服器時間。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="2ddcc-185">在 Windows PowerShell 視窗中，使用下列 Cmdlet 停止上一個小節中建立的服務部署：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="2ddcc-186">停止服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="2ddcc-187">服務停止時，您將收到表示停止的訊息。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Stop-AzureService 命令的狀態][The status of the Stop-AzureService command]
2. <span data-ttu-id="2ddcc-189">若要刪除服務，請呼叫下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="2ddcc-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="2ddcc-190">出現提示時，輸入 **Y** 以刪除服務。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="2ddcc-191">刪除服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="2ddcc-192">刪除服務後，您將收到表示已刪除服務的訊息。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![Remove-AzureService 命令的狀態][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="2ddcc-194">刪除服務不會刪除初次發佈服務時建立的儲存體帳戶，而且將持續對使用的儲存體計費。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="2ddcc-195">如果沒有其他項目正在使用儲存體，您可以將它刪除。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ddcc-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ddcc-196">Next steps</span></span>
<span data-ttu-id="2ddcc-197">如需詳細資訊，請參閱 [Node.js 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="2ddcc-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="2ddcc-198">[Azure 網站、雲端服務與虛擬機器的比較]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="2ddcc-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="2ddcc-199">[使用輕量型 Web 應用程式]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="2ddcc-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="2ddcc-200">[Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="2ddcc-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="2ddcc-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="2ddcc-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="2ddcc-202">[連線 PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="2ddcc-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="2ddcc-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="2ddcc-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="2ddcc-204">[雲端服務]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="2ddcc-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="2ddcc-205">[Node.js 開發人員中心]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="2ddcc-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
