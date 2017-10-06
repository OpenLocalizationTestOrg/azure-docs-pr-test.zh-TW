---
title: "aaaAzure 資源管理員為基礎的 PowerShell 命令的 Azure Web 應用程式 |Microsoft 文件"
description: "了解如何 toouse 會 hello 新的 Azure 資源管理員為基礎的 PowerShell 命令 toomanage Azure Web 應用程式。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="9648d-103">使用 Azure Resource Manager-Based PowerShell tooManage Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9648d-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9648d-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="9648d-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9648d-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="9648d-106">與 Microsoft Azure PowerShell 1.0.0 版新命令已經加入，可提供 hello 使用者 hello 能力 toouse Azure 資源管理員為基礎的 PowerShell 命令 toomanage Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9648d-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="9648d-107">toolearn 有關管理資源群組，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="9648d-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="9648d-108">toolearn 有關 hello 的參數與 hello PowerShell 指令程式選項的完整清單，請參閱 「 hello[完整的 Web 應用程式的 Azure 資源管理員為基礎的 PowerShell Cmdlet 的 Cmdlet 參考](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9648d-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="9648d-109">管理 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="9648d-110">建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-110">Create an App Service Plan</span></span>
<span data-ttu-id="9648d-111">toocreate 的應用程式服務計劃中，使用 hello**新增 AzureRmAppServicePlan** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9648d-112">以下是 hello 不同參數的說明：</span><span class="sxs-lookup"><span data-stu-id="9648d-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="9648d-113">**名稱**: hello 應用程式服務方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="9648d-114">**Location**：服務方案名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="9648d-115">**ResourceGroupName**： 包含 hello 新建立的應用程式服務計劃的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9648d-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="9648d-116">**層**: hello 預期定價層 （預設值是免費、 共用、 Basic、 Standard 和 Premium，其他選項包括）。</span><span class="sxs-lookup"><span data-stu-id="9648d-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="9648d-117">**WorkerSize**: hello 大小的背景工作 （預設值為小型 hello 層參數指定為 Basic、 Standard 或 Premium。</span><span class="sxs-lookup"><span data-stu-id="9648d-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="9648d-118">其他選項為 [中型] 和 [大型])。</span><span class="sxs-lookup"><span data-stu-id="9648d-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="9648d-119">**NumberofWorkers**: hello hello （預設值為 1） 的應用程式服務方案中的背景工作數目。</span><span class="sxs-lookup"><span data-stu-id="9648d-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="9648d-120">範例 toouse 這個指令程式：</span><span class="sxs-lookup"><span data-stu-id="9648d-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="9648d-121">在 App Service 環境中建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="9648d-122">toocreate 應用程式服務計劃在 app service 環境中，使用 hello 相同命令**新增 AzureRmAppServicePlan**命令 ASE 的資源群組名稱與額外的參數 toospecify hello ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="9648d-123">範例 toouse 這個指令程式：</span><span class="sxs-lookup"><span data-stu-id="9648d-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="9648d-124">深入了解應用程式服務環境中，核取 toolearn[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="9648d-125">列出現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-125">List Existing App Service Plans</span></span>
<span data-ttu-id="9648d-126">toolist hello 現有 app service 方案，使用**Get AzureRmAppServicePlan** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9648d-127">toolist 使用您的訂用帳戶，底下的所有應用程式服務方案：</span><span class="sxs-lookup"><span data-stu-id="9648d-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="9648d-128">toolist 所有應用程式服務方案的特定資源群組下，使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9648d-129">tooget 特定的應用程式服務方案，請使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="9648d-130">設定現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="9648d-131">toochange hello 設定現有的應用程式服務方案，使用 hello**組 AzureRmAppServicePlan** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="9648d-132">您可以變更 hello 層、 背景工作大小和 hello 背景工作數目</span><span class="sxs-lookup"><span data-stu-id="9648d-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="9648d-133">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="9648d-134">tooscale 現有應用程式服務計劃，請使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="9648d-135">變更 hello 背景工作大小的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="9648d-136">toochange hello 中現有的應用程式服務計劃，使用背景工作大小：</span><span class="sxs-lookup"><span data-stu-id="9648d-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="9648d-137">變更 hello 層的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="9648d-138">toochange hello 層現有應用程式服務計劃，使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="9648d-139">刪除現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="9648d-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="9648d-140">toodelete 現有的應用程式服務方案，所有指派給 web 應用程式需要 toobe 移動或刪除第一次。</span><span class="sxs-lookup"><span data-stu-id="9648d-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="9648d-141">然後使用 hello**移除 AzureRmAppServicePlan** cmdlet，您可以刪除 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="9648d-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="9648d-142">管理 App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="9648d-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="9648d-143">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-143">Create a Web App</span></span>
<span data-ttu-id="9648d-144">toocreate web 應用程式，使用 hello**新增 AzureRmWebApp** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9648d-145">以下是 hello 不同參數的說明：</span><span class="sxs-lookup"><span data-stu-id="9648d-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="9648d-146">**名稱**: hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="9648d-147">**AppServicePlan**: hello 服務計劃使用 toohost hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="9648d-148">**ResourceGroupName**： 裝載 hello 應用程式服務計劃的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9648d-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="9648d-149">**位置**: hello web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="9648d-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="9648d-150">範例 toouse 這個指令程式：</span><span class="sxs-lookup"><span data-stu-id="9648d-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="9648d-151">在 App Service 環境中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="9648d-152">toocreate web 應用程式中的應用程式服務環境 (ASE)。</span><span class="sxs-lookup"><span data-stu-id="9648d-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="9648d-153">使用 hello 相同**新增 AzureRmWebApp**命令額外參數 toospecify hello ASE 名稱與 hello hello ASE 所屬的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="9648d-154">深入了解應用程式服務環境中，核取 toolearn[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="9648d-155">刪除現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-155">Delete an existing Web App</span></span>
<span data-ttu-id="9648d-156">現有的 web 應用程式可以使用 hello toodelete**移除 AzureRmWebApp** cmdlet，您需要 toospecify hello hello web 應用程式名稱和 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9648d-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="9648d-157">列出現有的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="9648d-157">List existing Web Apps</span></span>
<span data-ttu-id="9648d-158">toolist hello 現有 web 應用程式，使用 hello **Get AzureRmWebApp** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9648d-159">toolist 您訂用帳戶，底下的所有 web 應用程式都使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="9648d-160">toolist 所有 web 應用程式的特定資源群組下，都使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9648d-161">tooget 是特定 web 應用程式中，使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="9648d-162">設定現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-162">Configure an existing Web App</span></span>
<span data-ttu-id="9648d-163">toochange hello 設定與現有的 web 應用程式的組態使用 hello**組 AzureRmWebApp** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9648d-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="9648d-164">如需參數的完整清單，請檢查 hello[指令程式參考連結](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="9648d-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="9648d-165">範例 (1): 使用這個指令程式 toochange 連接字串</span><span class="sxs-lookup"><span data-stu-id="9648d-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="9648d-166">範例 (2)：新增或變更應用程式設定</span><span class="sxs-lookup"><span data-stu-id="9648d-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="9648d-167">範例 (3): 在 64 位元模式中設定 hello web 應用程式 toorun</span><span class="sxs-lookup"><span data-stu-id="9648d-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="9648d-168">變更現有的 Web 應用程式的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="9648d-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="9648d-169">重新啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-169">Restart a web app</span></span>
<span data-ttu-id="9648d-170">toorestart web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="9648d-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="9648d-171">停止 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-171">Stop a web app</span></span>
<span data-ttu-id="9648d-172">toostop web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="9648d-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="9648d-173">啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9648d-173">Start a web app</span></span>
<span data-ttu-id="9648d-174">toostart web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="9648d-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="9648d-175">管理 Web 應用程式發行設定檔</span><span class="sxs-lookup"><span data-stu-id="9648d-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="9648d-176">每個 web 應用程式的發行設定檔可能是使用的 toopublish 您的應用程式，在發行設定檔上執行數項作業。</span><span class="sxs-lookup"><span data-stu-id="9648d-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="9648d-177">取得發行設定檔</span><span class="sxs-lookup"><span data-stu-id="9648d-177">Get Publishing Profile</span></span>
<span data-ttu-id="9648d-178">發行 web 應用程式中，使用的設定檔的 tooget hello:</span><span class="sxs-lookup"><span data-stu-id="9648d-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="9648d-179">此命令會回應 hello 發行設定檔 toohello 命令列也會輸出 hello 發行設定檔 tooa 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="9648d-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="9648d-180">重設發行設定檔</span><span class="sxs-lookup"><span data-stu-id="9648d-180">Reset Publishing Profile</span></span>
<span data-ttu-id="9648d-181">tooreset 兩者 hello 發行密碼，如 FTP 和 web deploy web 應用程式中，使用：</span><span class="sxs-lookup"><span data-stu-id="9648d-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="9648d-182">管理 Web 應用程式憑證</span><span class="sxs-lookup"><span data-stu-id="9648d-182">Manage Web App Certificates</span></span>
<span data-ttu-id="9648d-183">toolearn 有關 toomanage web 應用程式的憑證，請參閱[SSL 憑證繫結使用 PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="9648d-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9648d-184">Next Steps</span></span>
* <span data-ttu-id="9648d-185">toolearn 有關 Azure 資源管理員 PowerShell 支援，請參閱[使用 Azure PowerShell 的 Azure 資源管理員。](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="9648d-186">toolearn 有關應用程式服務環境，請參閱[簡介 tooApp Service 環境。](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="9648d-187">toolearn 有關管理應用程式服務 SSL 憑證，使用 PowerShell，請參閱[使用 PowerShell 的 SSL 憑證繫結。](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="9648d-188">請參閱 toolearn hello 的 Azure Web 應用程式，Azure 資源管理員為基礎的 PowerShell cmdlet 的完整清單的相關[Azure 指令程式參考的 Web 應用程式的 Azure 資源管理員 PowerShell Cmdlet。](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9648d-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="9648d-189">toolearn 有關管理應用程式服務使用 CLI，請參閱[Using Azure Resource Manager-Based XPlat CLI Azure Web 應用程式。](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9648d-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

