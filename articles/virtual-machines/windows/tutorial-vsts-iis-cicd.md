---
title: "aaaCreate CI/CD 中的管線 Team Services 與 Azure |Microsoft 文件"
description: "了解 toocreate Visual Studio Team Services 的持續整合及部署 web 應用程式 tooIIS Windows VM 上的傳送管線的方式"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="708ca-103">使用 Visual Studio Team Services 和 IIS 建立持續整合管線</span><span class="sxs-lookup"><span data-stu-id="708ca-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="708ca-104">tooautomate hello 建置、 測試及部署應用程式開發階段，您可以使用持續整合和部署 (CI/CD) 管線。</span><span class="sxs-lookup"><span data-stu-id="708ca-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="708ca-105">在本教學課程中，您可以使用 Visual Studio Team Services 以及 Azure 中執行 IIS 的 Windows 虛擬機器 (VM) 建立 CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="708ca-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="708ca-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="708ca-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="708ca-107">發佈 ASP.NET web 應用程式 tooa Team Services 專案</span><span class="sxs-lookup"><span data-stu-id="708ca-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="708ca-108">建立以程式碼認可所觸發的組建定義</span><span class="sxs-lookup"><span data-stu-id="708ca-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="708ca-109">在 Azure 的虛擬機器上安裝和設定 IIS</span><span class="sxs-lookup"><span data-stu-id="708ca-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="708ca-110">在 Team Services 中加入 hello IIS 執行個體 tooa 部署群組</span><span class="sxs-lookup"><span data-stu-id="708ca-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="708ca-111">建立發行定義 toopublish 新 web 部署套件 tooIIS</span><span class="sxs-lookup"><span data-stu-id="708ca-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="708ca-112">測試 hello CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="708ca-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="708ca-113">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="708ca-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="708ca-114">執行`Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="708ca-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="708ca-115">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="708ca-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="708ca-116">在 Team Services 中建立專案</span><span class="sxs-lookup"><span data-stu-id="708ca-116">Create project in Team Services</span></span>
<span data-ttu-id="708ca-117">Visual Studio Team Services 可讓您進行簡單的共同作業與開發，不需要維護內部部署的程式碼管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="708ca-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="708ca-118">Team Services 提供雲端的程式碼測試、組建和 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="708ca-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="708ca-119">您可以選擇版本控制存放庫和最符合您的程式碼開發的整合式開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="708ca-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="708ca-120">此教學課程中，您可以使用免費帳戶 toocreate 基本的 ASP.NET web 應用程式和 CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="708ca-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="708ca-121">如果您還沒有 Team Services 帳戶，請[建立帳戶](http://go.microsoft.com/fwlink/?LinkId=307137)。</span><span class="sxs-lookup"><span data-stu-id="708ca-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="708ca-122">toomanage hello 程式碼認可程序，組建定義，並發行定義建立專案、 Team Services 中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="708ca-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="708ca-123">在 Web 瀏覽器中開啟 Team Services 儀表板，選擇 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="708ca-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="708ca-124">輸入*myWebApp* hello**專案名稱**。</span><span class="sxs-lookup"><span data-stu-id="708ca-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="708ca-125">保留所有其他預設值 toouse *Git*版本控制和*Agile*工作項目處理序。</span><span class="sxs-lookup"><span data-stu-id="708ca-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="708ca-126">選擇 hello 太**分享***小組成員*，然後選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="708ca-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="708ca-127">一旦建立您的專案，選擇 hello 選項太**初始化與讀我檔案或 gitignore**，然後**初始化**。</span><span class="sxs-lookup"><span data-stu-id="708ca-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="708ca-128">在新專案，選擇 **儀表板**hello 頂端，然後選取**Visual Studio 中開啟**。</span><span class="sxs-lookup"><span data-stu-id="708ca-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="708ca-129">建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="708ca-129">Create ASP.NET web application</span></span>
<span data-ttu-id="708ca-130">在 hello 先前步驟中，您可以建立 Team Services 中的專案。</span><span class="sxs-lookup"><span data-stu-id="708ca-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="708ca-131">hello 最後一個步驟會在 Visual Studio 中開啟新的專案。</span><span class="sxs-lookup"><span data-stu-id="708ca-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="708ca-132">管理您的程式碼中的認可 hello **Team Explorer**視窗。</span><span class="sxs-lookup"><span data-stu-id="708ca-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="708ca-133">建立新專案的本機副本，然後從範本建立 ASP.NET web 應用程式，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="708ca-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="708ca-134">選取**複製**toocreate Team Services 專案的本機 git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="708ca-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![從 Team Services 專案複製存放庫](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="708ca-136">在 [解決方案] 下，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="708ca-136">Under **Solutions**, select **New**.</span></span>

    ![建立 Web 應用程式解決方案](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="708ca-138">選取**Web**範本，然後選擇 hello **ASP.NET Web 應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="708ca-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="708ca-139">輸入您的應用程式的名稱，例如*myWebApp*，並取消核取方塊 hello**為方案建立目錄**。</span><span class="sxs-lookup"><span data-stu-id="708ca-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="708ca-140">Hello 選項是否可用，取消核取方塊 hello 太**加入 Application Insights tooproject**。</span><span class="sxs-lookup"><span data-stu-id="708ca-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="708ca-141">Application Insights 需要您 tooauthorize Azure Application Insights web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="708ca-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="708ca-142">tookeep 簡單在本教學課程中，它略過此程序。</span><span class="sxs-lookup"><span data-stu-id="708ca-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="708ca-143">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="708ca-143">Select **OK**.</span></span>
4. <span data-ttu-id="708ca-144">選擇**MVC** hello 範本清單中。</span><span class="sxs-lookup"><span data-stu-id="708ca-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="708ca-145">選擇 [變更驗證]，選擇 [不需要驗證]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="708ca-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="708ca-146">選取**確定**toocreate 您的方案。</span><span class="sxs-lookup"><span data-stu-id="708ca-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="708ca-147">在 hello **Team Explorer**視窗中，選擇**變更**。</span><span class="sxs-lookup"><span data-stu-id="708ca-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![認可本機變更 tooTeam 服務 git 儲存機制](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="708ca-149">在 hello [認可] 文字方塊中輸入訊息例如*初始認可*。</span><span class="sxs-lookup"><span data-stu-id="708ca-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="708ca-150">選擇**全部認可並同步處理**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="708ca-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="708ca-151">建立組建定義</span><span class="sxs-lookup"><span data-stu-id="708ca-151">Create build definition</span></span>
<span data-ttu-id="708ca-152">在 Team Services 中，您可以使用組建定義 toooutline 建置您的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="708ca-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="708ca-153">在本教學課程中，我們會建立基本的定義會使用我們的原始程式碼，建置 hello 的解決方案，然後建立 web 部署套件，我們可以在 IIS 伺服器上使用 toorun hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="708ca-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="708ca-154">在您的 Team Services 專案，選擇 **建置和發行**hello 頂端，然後選取**建置**。</span><span class="sxs-lookup"><span data-stu-id="708ca-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="708ca-155">選取 [+新增定義]。</span><span class="sxs-lookup"><span data-stu-id="708ca-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="708ca-156">選擇 hello **ASP.NET （預覽）**範本，然後選取**套用**。</span><span class="sxs-lookup"><span data-stu-id="708ca-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="708ca-157">保留所有 hello 預設工作的值。</span><span class="sxs-lookup"><span data-stu-id="708ca-157">Leave all hello default task values.</span></span> <span data-ttu-id="708ca-158">在下**取得來源**，確保該 hello *myWebApp*儲存機制和*主要*會選取分支。</span><span class="sxs-lookup"><span data-stu-id="708ca-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![在 Visual Studio Team Services 中建立組建定義](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="708ca-160">在 hello**觸發程序**索引標籤上，移動 hello 滑桿**啟用此觸發程序**太*啟用*。</span><span class="sxs-lookup"><span data-stu-id="708ca-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="708ca-161">儲存 hello 組建定義和佇列新組建選取**儲存，並佇列**，然後**儲存，並佇列**一次。</span><span class="sxs-lookup"><span data-stu-id="708ca-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="708ca-162">保留 hello 預設值，然後選取**佇列**。</span><span class="sxs-lookup"><span data-stu-id="708ca-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="708ca-163">監看式當 hello 建置排定在託管的代理程式，然後開始 toobuild。</span><span class="sxs-lookup"><span data-stu-id="708ca-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="708ca-164">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="708ca-164">hello output is similar toohello following example:</span></span>

![Team Services 專案的成功組建](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="708ca-166">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="708ca-166">Create virtual machine</span></span>
<span data-ttu-id="708ca-167">平台 toorun tooprovide ASP.NET web 應用程式，您需要執行 IIS 的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="708ca-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="708ca-168">Team Services 會使用代理程式 toointeract hello IIS 執行個體認可程式碼，並觸發組建。</span><span class="sxs-lookup"><span data-stu-id="708ca-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="708ca-169">使用[此指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json)建立 Windows Server 2016 VM。</span><span class="sxs-lookup"><span data-stu-id="708ca-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="708ca-170">它會採用 hello 指令碼 toorun 幾分鐘，並建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="708ca-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="708ca-171">一旦建立 hello VM 之後，開啟的通訊埠 80 web 流量[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="708ca-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="708ca-172">tooconnect tooyour VM，取得與 hello 公用 IP 位址[Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="708ca-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="708ca-173">建立遠端桌面工作階段 tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="708ca-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="708ca-174">開啟 hello VM，**系統管理員 PowerShell**命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="708ca-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="708ca-175">安裝 IIS 和所需的 .NET 功能，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="708ca-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="708ca-176">建立部署群組</span><span class="sxs-lookup"><span data-stu-id="708ca-176">Create deployment group</span></span>
<span data-ttu-id="708ca-177">toopush 出 hello web 部署封裝 toohello IIS 伺服器，您在 Team Services 中定義部署群組。</span><span class="sxs-lookup"><span data-stu-id="708ca-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="708ca-178">此群組可讓您的伺服器是新組建的 hello 目標認可完成服務和組建的程式碼 tooTeam toospecify。</span><span class="sxs-lookup"><span data-stu-id="708ca-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="708ca-179">在 Team Services 中，選擇 [組建及發行]，然後選取 [部署群組]。</span><span class="sxs-lookup"><span data-stu-id="708ca-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="708ca-180">選擇 [新增部署群組]。</span><span class="sxs-lookup"><span data-stu-id="708ca-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="708ca-181">輸入 hello 群組的名稱，例如*myIIS*，然後選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="708ca-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="708ca-182">在 hello**登錄機器**區段中，確定*Windows*選取，則核取 hello 方塊太**hello 指令碼中的個人存取權杖用於驗證**。</span><span class="sxs-lookup"><span data-stu-id="708ca-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="708ca-183">選取**複製指令碼 tooclipboard**。</span><span class="sxs-lookup"><span data-stu-id="708ca-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="708ca-184">新增 IIS VM toohello 部署群組</span><span class="sxs-lookup"><span data-stu-id="708ca-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="708ca-185">透過建立 hello 部署群組，將每個 IIS 執行個體 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="708ca-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="708ca-186">Team Services 產生的指令碼下載並設定代理程式上 hello VM 接收新的 web 部署封裝，然後將它套用 tooIIS。</span><span class="sxs-lookup"><span data-stu-id="708ca-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="708ca-187">在 hello**系統管理員 PowerShell**貼上您的 VM 上的工作階段，並執行 Team Services 從複製的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="708ca-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="708ca-188">當提示的 tooconfigure 標記 hello 代理程式，選擇*Y*輸入*web*。</span><span class="sxs-lookup"><span data-stu-id="708ca-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="708ca-189">當提示 hello 使用者帳戶，請按*傳回*tooaccept hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="708ca-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="708ca-190">等候 hello 訊息的指令碼 toofinish *vstsagent.account.computername 服務已順利啟動*。</span><span class="sxs-lookup"><span data-stu-id="708ca-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="708ca-191">在 hello**部署群組**頁面 hello**建置和發行**功能表中，開啟 hello *myIIS*部署群組。</span><span class="sxs-lookup"><span data-stu-id="708ca-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="708ca-192">在 hello**機器**索引標籤上，確認已列出您的 VM。</span><span class="sxs-lookup"><span data-stu-id="708ca-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![VM 成功加入 tooTeam 服務部署群組](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="708ca-194">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="708ca-194">Create release definition</span></span>
<span data-ttu-id="708ca-195">toopublish 組建，您的發行定義中建立 Team Services。</span><span class="sxs-lookup"><span data-stu-id="708ca-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="708ca-196">您的應用程式的成功組建會自動觸發此定義。</span><span class="sxs-lookup"><span data-stu-id="708ca-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="708ca-197">您選擇 hello 部署群組 toopush 您的 web deploy 封裝，並定義 hello 適當的 IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="708ca-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="708ca-198">選擇 [組建及發行]，然後選取 [組建]。</span><span class="sxs-lookup"><span data-stu-id="708ca-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="708ca-199">選擇 hello 先前步驟中建立的組建定義。</span><span class="sxs-lookup"><span data-stu-id="708ca-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="708ca-200">在下**最近完成**，請選擇 hello 最新的組建，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="708ca-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="708ca-201">選擇**是**toocreate 發行定義。</span><span class="sxs-lookup"><span data-stu-id="708ca-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="708ca-202">選擇 hello**空**範本，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="708ca-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="708ca-203">請確認 hello 專案和來源組建定義就會填入您的專案。</span><span class="sxs-lookup"><span data-stu-id="708ca-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="708ca-204">選取 hello**連續部署**核取方塊，然後選取 **建立**。</span><span class="sxs-lookup"><span data-stu-id="708ca-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="708ca-205">選取 hello 下拉式方塊旁邊太**+ 加入工作**選擇*新增部署群組階段*。</span><span class="sxs-lookup"><span data-stu-id="708ca-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![在 Team Services 中加入工作 toorelease 定義](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="708ca-207">選擇**新增**下一步太**IIS Web 應用程式 Deploy(Preview)**，然後選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="708ca-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="708ca-208">選取 hello**部署群組上執行**父工作。</span><span class="sxs-lookup"><span data-stu-id="708ca-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="708ca-209">如**部署群組**，選取 hello 部署群組，您建立更早版本，例如*myIIS*。</span><span class="sxs-lookup"><span data-stu-id="708ca-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="708ca-210">在 hello**機器標記**方塊中，選取**新增**選擇 hello *web*標記。</span><span class="sxs-lookup"><span data-stu-id="708ca-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![用於 IIS 的發行定義部署群組工作](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="708ca-212">選取 hello**部署： IIS Web 應用程式部署**工作 tooconfigure IIS 執行個體的設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="708ca-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="708ca-213">在 [網站名稱] 輸入 Default Web Site。</span><span class="sxs-lookup"><span data-stu-id="708ca-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="708ca-214">保留所有 hello 其他預設設定。</span><span class="sxs-lookup"><span data-stu-id="708ca-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="708ca-215">選擇 [儲存]，然後選取 [確定] 兩次。</span><span class="sxs-lookup"><span data-stu-id="708ca-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="708ca-216">建立發行並發佈</span><span class="sxs-lookup"><span data-stu-id="708ca-216">Create a release and publish</span></span>
<span data-ttu-id="708ca-217">您現在可以將您的 Web 部署套件當做新發行加以推送。</span><span class="sxs-lookup"><span data-stu-id="708ca-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="708ca-218">此步驟中進行通訊的每個執行個體是 hello 部署群組的一部分，將推入 hello web hello 代理程式部署套件，然後設定 IIS toorun hello 更新 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="708ca-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="708ca-219">在您的發行定義中，選取 [+ 發行]，然後選擇 [建立發行]。</span><span class="sxs-lookup"><span data-stu-id="708ca-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="708ca-220">確認 hello 最新組建在 hello 下拉式清單中，選取連同**自動部署： 建立版本之後**。</span><span class="sxs-lookup"><span data-stu-id="708ca-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="708ca-221">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="708ca-221">Select **Create**.</span></span>
3. <span data-ttu-id="708ca-222">小型橫幅會顯示您的發行定義的 hello 頂端像是*發行 ' Release 1' 已建立*。</span><span class="sxs-lookup"><span data-stu-id="708ca-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="708ca-223">選取 hello 發行連結。</span><span class="sxs-lookup"><span data-stu-id="708ca-223">Select hello release link.</span></span>
4. <span data-ttu-id="708ca-224">開啟 hello**記錄**toowatch hello 發行進度索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="708ca-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![成功的 Team Services 發行和 Web 部署封裝推送](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="708ca-226">Hello 發行完成之後，請開啟網頁瀏覽器，並輸入您的 VM hello 公用 IIP 位址。</span><span class="sxs-lookup"><span data-stu-id="708ca-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="708ca-227">您的 ASP.NET Web 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="708ca-227">Your ASP.NET web application is running.</span></span>

    ![IIS VM 上執行的 ASP.NET Web 應用程式](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="708ca-229">測試 hello 整個 CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="708ca-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="708ca-230">在 IIS 上執行您 web 應用程式，現在請 hello 整個 CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="708ca-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="708ca-231">您在 Visual Studio 和認可您的程式碼，組建就會觸發然後觸發更新 web 的版本進行變更後將部署套件 tooIIS:</span><span class="sxs-lookup"><span data-stu-id="708ca-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="708ca-232">在 Visual Studio 中，開啟 [hello**方案總管] 中**視窗。</span><span class="sxs-lookup"><span data-stu-id="708ca-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="708ca-233">瀏覽 tooand 開啟*myWebApp |檢視 |首頁 |Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="708ca-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="708ca-234">編輯第 6 行 tooread:</span><span class="sxs-lookup"><span data-stu-id="708ca-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="708ca-235">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="708ca-235">Save hello file.</span></span>
5. <span data-ttu-id="708ca-236">開啟 hello **Team Explorer**視窗中，選取 hello *myWebApp*專案，然後選擇 **變更**。</span><span class="sxs-lookup"><span data-stu-id="708ca-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="708ca-237">輸入 「 認可 」 訊息，例如*測試 CI/CD 管線*，然後選擇 **認可所有和同步處理**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="708ca-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="708ca-238">Team Services 工作區中，則會從 hello 程式碼認可觸發新組建。</span><span class="sxs-lookup"><span data-stu-id="708ca-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="708ca-239">選擇 [組建及發行]，然後選取 [組建]。</span><span class="sxs-lookup"><span data-stu-id="708ca-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="708ca-240">選擇您的組建定義，然後選取 hello**排入佇列 （&) 執行**hello 為組建 toowatch 建置進行時。</span><span class="sxs-lookup"><span data-stu-id="708ca-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="708ca-241">Hello 建置成功之後，就會觸發新的版本。</span><span class="sxs-lookup"><span data-stu-id="708ca-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="708ca-242">選擇**建置和發行**，然後**版本**toosee hello web deploy 封裝推入 tooyour IIS VM。</span><span class="sxs-lookup"><span data-stu-id="708ca-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="708ca-243">選取 hello**重新整理**圖示 tooupdate hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="708ca-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="708ca-244">當 hello*環境*欄會顯示綠色的核取記號，hello 版本已成功部署 tooIIS。</span><span class="sxs-lookup"><span data-stu-id="708ca-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="708ca-245">toosee 套用您的變更，請重新整理您的瀏覽器中的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="708ca-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![從 CI/CD 管線在 IIS VM 上執行的 ASP.NET Web 應用程式](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="708ca-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="708ca-247">Next steps</span></span>

<span data-ttu-id="708ca-248">在本教學課程中，您在 Team Services 中建立 ASP.NET web 應用程式和設定的組建和發行定義 toodeploy 新 web deploy 封裝 tooIIS 在每個程式碼認可。</span><span class="sxs-lookup"><span data-stu-id="708ca-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="708ca-249">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="708ca-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="708ca-250">發佈 ASP.NET web 應用程式 tooa Team Services 專案</span><span class="sxs-lookup"><span data-stu-id="708ca-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="708ca-251">建立以程式碼認可所觸發的組建定義</span><span class="sxs-lookup"><span data-stu-id="708ca-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="708ca-252">在 Azure 的虛擬機器上安裝和設定 IIS</span><span class="sxs-lookup"><span data-stu-id="708ca-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="708ca-253">在 Team Services 中加入 hello IIS 執行個體 tooa 部署群組</span><span class="sxs-lookup"><span data-stu-id="708ca-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="708ca-254">建立發行定義 toopublish 新 web 部署套件 tooIIS</span><span class="sxs-lookup"><span data-stu-id="708ca-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="708ca-255">測試 hello CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="708ca-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="708ca-256">如何前進 toohello 下一個教學課程 toolearn toosecure web 伺服器使用 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="708ca-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="708ca-257">使用 SSL 保護網路伺服器</span><span class="sxs-lookup"><span data-stu-id="708ca-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)